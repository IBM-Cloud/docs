---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-04"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Implémentation de flux
{: #openwhisk_feeds}

{{site.data.keyword.openwhisk_short}} rend en charge une API ouverte, dans laquelle tous les utilisateurs peuvent exposer un service de producteur d'événement sous forme de **flux** dans un **package**.   Cette section décrit les options d'architecture et d'implémentation pour la mise à disposition de votre propre flux.

Ce document s'adresse aux utilisateurs avancés d'{{site.data.keyword.openwhisk_short}} qui souhaitent publier leurs propres flux.  La plupart des utilisateurs d'{{site.data.keyword.openwhisk_short}} peuvent ignorer cette section.

## Architecture de flux

Il existe aux moins trois modèles d'architecture pour la création d'un flux : **Points d'ancrage**, **Interrogation** et **Connexions**.

### Points d'ancrage
Dans le modèle *Points d'ancrage*, nous configurons un flux à l'aide d'une fonction de [webhook](https://en.wikipedia.org/wiki/Webhook) exposée par un autre service.   Dans cette stratégie, nous configurons un webhook sur un service externe afin d'envoyer des données directement à une adresse URL pour exécuter un déclencheur.  Il s'agit de loin de l'option la plus simple et la plus attrayante pour l'implémentation de flux à faible fréquence.

<!-- The github feed is implemented using webhooks.  Put a link here when we have the open repo ready -->

### Interrogation
Dans le modèle "Interrogation", nous définissons une *action* {{site.data.keyword.openwhisk_short}} de sorte qu'elle interroge un noeud final régulièrement afin d'extraire de nouvelles données. Ce modèle est relativement facile à générer, mais la fréquence des événements sera évidemment limitée par l'intervalle d'interrogation.

### Connexions
Dans le modèle "Connexions", nous établissons un service distinct quelque part, qui maintient une connexion permanente à une source de flux.    L'implémentation reposant sur la connexion peut interagir avec un noeud final de service via une interrogation longue, ou pour configurer une notification push.

<!-- Our cloudant changes feed is connection based.  Put a link here to
an open repo -->

<!-- What is the foundation for the Message Hub feed? If it is "connections" then lets put a link here as well -->

## Différence entre un flux et un déclencheur

Les flux et les déclencheurs sont étroitement liés, mais ce sont des concepts techniquement distincts.   

- {{site.data.keyword.openwhisk_short}} traite des **événements** qui transitent dans le système.

- Techniquement, un **déclencheur** désigne une classe d'événements.   Chaque événement appartient à un déclencheur et un seul ; par analogie, un déclencheur ressemble à une *rubrique* dans les systèmes de publication/abonnement reposant sur des rubriques. Une **règle** *T -> A* a la signification suivante : "à chaque fois qu'un événement provenant du déclencheur *T* arrive, appeler l'action *A* avec le contenu du déclencheur.

- Un **flux** est un flot d'événements qui appartiennent tous à un déclencheur *T*. Il est contrôlé par une **action de flux** qui gère la création, la suppression, l'interruption et la reprise du flot d'événements comprenant un flux. En règle générale, l'action de flux interagit avec des services externes qui produisent les événements, via une API REST qui gère les notifications.

##  Implémentation d'actions de flux

L'*action de flux* est une *action* {{site.data.keyword.openwhisk_short}} normale, mais elle doit accepter les paramètres suivants :
* **lifecycleEvent** : 'CREATE', 'DELETE', 'PAUSE' ou 'UNPAUSE'.
* **triggerName** : nom complet du déclencheur qui contient les événements produits depuis ce flux.
* **authKey** : données d'identification pour l'authentification de base de l'utilisateur {{site.data.keyword.openwhisk_short}} à qui appartient le déclencheur susmentionné.

L'action de flux peut également accepter tout autre paramètre dont elle a besoin pour gérer le flux.  Par exemple, l'action de flux changes de cloudant peut recevoir des paramètres tels que *'dbname'*, *'username'*, etc.

Lorsque l'utilisateur crée un déclencheur depuis l'interface de ligne de commande avec le paramètre **--feed**, le système appelle automatiquement l'action de flux avec les paramètres appropriés.

Par exemple, supposez que l'utilisateur a créé une liaison `mycloudant` pour le package `cloudant` avec son nom d'utilisateur et son mot de passe comme paramètres liés. Lorsque l'utilisateur exécute la commande suivante depuis l'interface de ligne de commande :

`wsk trigger create T --feed mycloudant/changes -p dbName myTable`

le système effectue "en coulisses" une opération équivalente à :

`wsk action invoke mycloudant/changes -p lifecycleEvent CREATE -p triggerName T -p authKey <userAuthKey> -p password <password value from mycloudant binding> -p username <username value from mycloudant binding> -p dbName mytype`

L'action de flux appelée *changes* admet ces paramètres et doit effectuer toute action nécessaire à la définition d'un flot d'événements depuis Cloudant, avec la configuration appropriée, dirigé vers le déclencheur *T*.    

Pour le flux *changes* de Cloudant, l'action communique directement avec un service de *déclencheur cloudant* que nous avons implémenté avec une architecture reposant sur les connexions.   Les autres architectures sont présentées plus loin.

Un protocole d'action de flux similaire existe pour `wsk trigger delete`.    

## Implémentation de flux avec des points d'ancrage

Il est facile de configurer un flux via un point d'ancrage si le producteur d'événement prend en charge une fonction de webhook/rappel.

Avec cette méthode, il n'est *pas nécessaire* de maintenir un service persistant hors d'{{site.data.keyword.openwhisk_short}}.  La gestion des flux s'exécute naturellement par le biais d'*actions de flux* {{site.data.keyword.openwhisk_short}} sans état, qui négocient directement avec une API de webhook tierce.

Lorsqu'elle est appelée avec `CREATE`, l'action de flux installe simplement un webhook pour un autre service et demande au service distant d'envoyer des notifications à l'URL `fireTrigger` appropriée dans {{site.data.keyword.openwhisk_short}}.

Le webhook doit envoyer les notifications à une adresse URL telle que :

`POST /namespaces/{espace_nom}/triggers/{nom_déclencheur}`

Le formulaire associé à la demande d'envoi est interprété comme un document JSON définissant des paramètres pour l'événement déclencheur. Les règles {{site.data.keyword.openwhisk_short}} transmettent ces paramètres de déclencheur pour que des actions soient déclenchées suite à l'événement.

## Implémentation de flux avec le modèle Interrogation

Il est possible de configurer une *action* {{site.data.keyword.openwhisk_short}} afin d'interroger une source de flux entièrement dans {{site.data.keyword.openwhisk_short}}, sans qu'il ne soit nécessaire de maintenir des connexions ou un service externe persistants.

Pour les flux pour lesquels aucun webhook n'est disponible mais qui n'ont pas besoin de gérer un volume élevé de demandes simultanées ou qui ne requièrent pas de temps de réponse courts, l'interrogation est une option attrayante.

Pour configurer un flux reposant sur l'interrogation, l'action de flux effectue les opérations suivantes lorsqu'elle est appelée pour `CREATE` :

1.   L'action de flux configure un déclencheur périodique (*D*) avec la fréquence souhaitée, à l'aide du flux `whisk.system/alarms`.
2.   Le développeur de flux crée une action `pollMyService` qui interroge simplement le service distant et renvoie les nouveaux événements, le cas échéant.
3.  L'action de flux configure une *règle* *T -> pollMyService*.

Cette procédure implémente un déclencheur reposant sur l'interrogation qui n'utilise que des actions {{site.data.keyword.openwhisk_short}}, sans recourir à un service distinct.

## Implémentation de flux via le modèle Connexions

Les deux choix d'architecture précédents sont simples et faciles à implémenter. Cependant, si vous voulez créer un flux dont les performances sont élevées, il n'existe pas d'alternative aux connexions permanentes et à l'interrogation longue, ou à des techniques similaires.

Etant donné que les actions {{site.data.keyword.openwhisk_short}} doivent être de courte durée, une action ne peut pas maintenir une connexion permanente à un tiers. A la place, nous devons utiliser un service distinct
(hors d'{{site.data.keyword.openwhisk_short}}) qui s'exécute en permanence. Il s'agit de *services fournisseurs*.  Un service fournisseur peut maintenir des connexions à des sources d'événement tierces qui prennent en charge l'interrogation longue ou d'autres notifications reposant sur les connexions.

Le service fournisseur doit fournir une API REST qui permet à l'*action de flux* {{site.data.keyword.openwhisk_short}} de contrôler le flux.   Il agit comme un proxy entre le fournisseur d'événements et {{site.data.keyword.openwhisk_short}} ; lorsqu'il reçoit des événements d'un tiers, il les envoie à {{site.data.keyword.openwhisk_short}} en exécutant un déclencheur.

Le flux *changes* de Cloudant en est un exemple canonique : il établit un service `cloudanttrigger` qui fait office de médiateur entre les notifications Cloudant sur une connexion permanente et des déclencheurs {{site.data.keyword.openwhisk_short}}.
<!-- TODO: add a reference to the open source implementation -->

Le flux *alarm* est implémenté avec un modèle similaire.

L'architecture reposant sur les connexions est l'option qui permet les performances les plus élevées, mais elle impose une surcharge plus importante sur les opérations par rapport aux architectures reposant sur l'interrogation et des points d'ancrage.   
