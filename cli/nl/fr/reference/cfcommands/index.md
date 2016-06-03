---

 

copyright:

  years: 2015, 2016

 

---
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Commandes Cloud Foundry (cf)

*Dernière mise à jour : 29 janvier 2016*

Vous pouvez utiliser des commandes Cloud Foundry (cf) pour gérer vos applications.
{:shortdesc}

Les informations ci-après répertorient les commandes cf les plus fréquemment utilisées pour gérer des applications. Pour répertorier toutes les
commandes cf et afficher l'aide associée, utilisez `cf help`. Utilisez `cf nom_commande -h` afin d'afficher des informations d'aide
détaillées pour une commande particulière.

*Remarque :* sur votre réseau, si un serveur proxy HTTP se trouve entre l'hôte qui exécute les commandes cf et le noeud final d'API Cloud
Foundry, vous devez
spécifier le nom d'hôte ou l'adresse IP du serveur proxy en définissant la variable d'environnement `HTTP_PROXY`. Pour plus de détails, voir [Using the cf CLI with an HTTP Proxy Server](http://docs.cloudfoundry.org/devguide/installcf/http-proxy.html).

## cf api

Affiche ou spécifie l'adresse URL du noeud final d'API de {{site.data.keyword.Bluemix_notm}}.
```
cf api URLServeurBluemix
```
<dl>
<dt>URLServeurBluemix</dt>
<dd>Adresse URL du noeud final d'API Bluemix que vous devez spécifier lorsque vous vous connectez à {{site.data.keyword.Bluemix_notm}}. En général,
cette adresse URL est https://api.{DomainName}. 
Si vous voulez afficher l'adresse URL du noeud final de l'API que vous utilisez actuellement, il n'est pas nécessaire de spécifier ce paramètre pour la
commande cf api.</dd>
<dt>*--skip-ssl-validation*</dt>
<dd>Désactive le processus de validation SSL. L'utilisation de ce paramètre peut entraîner des problèmes de sécurité.</dd>
<dt>*--unset*</dt>
<dd>Supprime les informations de connexion pour tous les noeuds finaux d'API.</dd>
</dl>

## cf apps

Répertorie toutes les applications que vous avez déployées dans l'espace en cours. Le statut de
chaque application est également affiché.

Supposez que vous disposez d'une instance pour une application. La colonne des instances de la réponse générée par la commande cf apps comporte la
valeur 1/1 si votre application est en cours d'exécution et 0/1 si elle est arrêtée. Si elle comporte ?/1, qui indique que l''état de l'instance d'application est inconnu, vous pouvez copier l'adresse URL de l'application dans votre
navigateur afin de vérifier si votre application répond, ou n'afficher que les derniers lignes du journal avec la commande `cf logs
nom_app` pour déterminer si l'application génère un contenu de journal.

## cf bind-service

Lie une instance de service existante à votre application.
```
cf bind-service nom_app instance_service
```

Par exemple, si vous disposez d'une instance de service appelée `mon_dataworks` dans votre organisation et votre espace en cours, vous
pouvez utiliser `cf bind-service mon_app
mon_dataworks` pour lier cette instance de service à votre application.

<dl>
<dt>nom_app</dt>
<dd>Nom de l'application.</dd>
<dt>instance_service</dt>
<dd>Nom de l'instance de service existante.</dd>
</dl>

## cf create-service

Crée une instance de service.
```
cf create-service nom_service plan_service instance_service
```
Par exemple, vous pouvez utiliser `cf create-service DataWorks free mon_dataworks` pour créer une instance du service
{{site.data.keyword.dataworks_short}} avec un plan gratuit.

<dl>
<dt>nom_service</dt>
<dd>Nom du service.</dd>
<dt>plan_service</dt>
<dd>Nom du plan de service.</dd>
<dt>instance_service</dt>
<dd>Nom à utiliser pour la nouvelle instance de service que vous créez.</dd>
</dl>

## cf create-space

Crée un espace.
```
cf create-space nom_espace
```
<dl>
<dt>nom_espace</dt>
<dd>Nom de l'espace.</dd>
<dt>*-o*</dt>
<dd>Nom de l'organisation dans laquelle créer un espace.</dd>
<dt>*-q*</dt>
<dd>Quota à affecter au nouvel espace. S'il n'est pas spécifié, un quota par défaut est affecté automatiquement.</dd>
</dl>

## cf delete

Supprime une application existante.
```
cf delete nom_app
```
<dl>
<dt>nom_app</dt>
<dd>Nom de l'application.<dd>
<dt>*-f*</dt>
<dd>Force la suppression de l'application sans confirmation. Ce paramètre est facultatif.</dd>
<dt>*-r*</dt>
<dd>Supprime tous les noms de domaine associés à l'application. Ce paramètre est facultatif.</dd>
</dl>

## cf delete-space

Supprime un espace.
```
cf delete-space nom_espace
```
<dl>
<dt>nom_espace</dt>
<dd>Nom de l'espace.</dd>
<dt>*-f*</dt>
<dd>Force la suppression de l'espace sans confirmation. Ce paramètre est facultatif.</dd>
*Remarque :* la suppression d'un espace est une opération irréversible.
</dl>

## cf events

Affiche les événements d'exécution liés à une application.
```
cf events nom_app
```
<dl>
<dt>nom_app</dt>
<dd>Nom de l'application.</dd>
</dl>

## cf help

Affiche les informations d'aide pour toutes les commandes cf ou pour une commande cf spécifique si le paramètre nom_commande est utilisé.
```
cf help nom_commande
```
<dl>
<dt>nom_commande</dt>
<dd>Nom d'une commande. Si vous voulez afficher l'aide propre à une commande, vous pouvez utiliser ce paramètre.</dd>
<dd>Si vous ne spécifiez pas ce paramètre, l'aide de toutes les commandes cf s'affiche.</dd>
</dl>


## cf login

Vous connecte à {{site.data.keyword.Bluemix_notm}}.
```
cf login
```
Vous pouvez utiliser un ou plusieurs des paramètres suivants lorsque vous émettez la commande cf login :
<dl>
<dt>*-a* https://api.{DomainName}</dt>
<dd>Adresse URL du noeud final d'API de {{site.data.keyword.Bluemix_notm}}. Ce paramètre est facultatif.</dd>
<dt>*-u*nom_utilisateur</dt>
<dd>Votre nom d'utilisateur. Ce paramètre est facultatif.</dd>
<dt>*-p*mot_de_passe</dt>
<dd>Votre mot de passe.</dd>
<dd>*Important :* si vous indiquez un mot de passe avec le paramètre *-p* dans l'interface de ligne de commande, le mot
de passe peut être enregistré dans l'historique de la ligne de commande. Pour des raisons de sécurité, évitez de fournir le mot de passe
avec le paramètre -p. A la place,
entrez le mot de passe lorsque l'interface de ligne de commande vous y invite.</dd>
<dt>*-o*nom_organisation</dt>
<dd>Nom de l'organisation à laquelle vous voulez vous connecter.</dd>
<dt>*-s*nom_espace</dt>
<dd>Nom de l'espace auquel vous voulez vous connecter.</dd>
<dt>*--skip-ssl-validation*</dt>
<dd>Désactive le processus de validation SSL. L'utilisation de ce paramètre peut entraîner des problèmes de sécurité.</dd>
</dl>

*Remarque :* si vous indiquez votre mot de passe dans le paramètre *-p* de cette commande, votre mot de passe peut être
enregistré dans le fichier
historique de la commande shell et peut être visible pour les autres utilisateurs du système d'exploitation local.


## cf logs

Affiche les flux de journalisation de sortie standard et d'erreur standard d'une application.
```
cf logs nom_app
```
<dl>
<dt>nom_app</dt>
<dd>Nom de l'application.</dd>
<dt>*--recent*</dt>
<dd>Extrait les journaux récents.</dd>
</dl>

## cf marketplace

Répertorie tous les services disponibles sur la place de marché. Les services répertoriés par cette commande apparaissent également dans le catalogue
{{site.data.keyword.Bluemix_notm}}.
```
cf marketplace
```

## cf push

Déploie une nouvelle application dans Bluemix ou met à jour une application existante dans Bluemix.
```
cf push nom_app 
```
<dl>
<dt>nom_app</dt>
<dd>Nom de l'application.</dd>
<dt>*-b*nom_pack_construction</dt>
<dd>Nom du pack de construction. nom_pack_construction peut être le nom d'un pack de construction personnalisé ou une adresse URL Git, par exemple
`mon_pack_construction` ou `https://github.com/heroku/heroku-buildpack-play.git`.
</dd>
<dt>*-c*commande_démarrage</dt>
<dd>Commande de démarrage de votre application. Pour utiliser la commande de démarrage par défaut, spécifiez la valeur null pour cette option. Par exemple :</dd>
<dd>```
cf push nom_app -c null
```</dd>
<dd>Vous pouvez aussi utiliser cette option pour exécuter des fichiers script. Par exemple :
```
cf push nom_app -c “bash ./<run.sh>"
```</dd>
<dt>*-f* chemin_manifeste</dt>
<dd>Chemin d'accès au fichier manifeste. Le fichier manifeste par défaut est manifest.yml sous le répertoire racine de votre application.</dd>
<dt>*-i*nombre_instances</dt>
<dd>Nombre d'instances.</dd>
<dt>*-k*limite_disque</dt>
<dd>Limite de disque pour l'application, par exemple *256M*, *1024M* ou *1G*.</dd>
<dt>*-m*limite_mémoire</dt>
<dd>Limite de mémoire pour l'application, par exemple *256M*,
*1024M* ou *1G*.</dd>
<dt>*-n*nom_hôte</dt>
<dd>Nom d'hôte pour l'application, par exemple *mon-sous-domaine*.</dd>
<dt>*-p*chemin_app</dt>
<dd>Chemin d'accès au répertoire de l'application ou au fichier archive de l'application.</dd>
<dt>*-t*délai_attente</dt>
<dd>Délai maximal de démarrage de l'application, en secondes. Il se peut que d'autres délais d'attente côté serveur remplacent cette valeur.</dd>
<dt>*-s* nom_pile</dt>
<dd>Pile pour l'exécution des applications. Une pile est un système de fichiers préconfiguré incluant le système d'exploitation. Utilisez `cf
stacks` pour afficher les piles disponibles dans {{site.data.keyword.Bluemix_notm}}.</dd>
<dt>*--no-hostname*</dt>
<dd>Mappe le domaine de système Bluemix à cette application.</dd>
<dt>*--no-manifest*</dt>
<dd>Ignore le fichier manifeste par défaut.</dd>
<dt>*--no-route*</dt>
<dd>Ne mappe pas de route à cette application.</dd>
<dt>*--no-start*</dt>
<dd>Ne démarre pas l'application une fois qu'elle est déployée.</dd>
<dt>*--random-route*</dt>
<dd>Crée une route aléatoire pour l'application.</dd>
</dl>

## cf scale

Affiche ou change le nombre d'instances, la limite d'espace disque et la limite de mémoire pour une application.
```
cf scale nom_app -i nombre_instances -k limite_disque -m limite_mémoire
```
<dl>
<dt>nom_app</dt>
<dd>Nom de l'application.</dd>
<dt>*-i*nombre_instances</dt>
<dd>Nombre d'instances.</dd>
<dt>*-k*limite_disque</dt>
<dd>Limite de disque pour l'application, par exemple *256M*, *1024M* ou *1G*.</dd>
<dt>*-m*limite_mémoire</dt>
<dd>Limite de mémoire pour l'application, par exemple *256M*,
*1024M* ou *1G*.</dd>
<dt>*-f*</dt>
<dd>Force l'application à redémarrer sans invite.</dd>
</dl>

## cf services

Répertorie tous les services disponibles dans l'espace en cours.
```
cf services
```

## cf set-env

Définit une variable d'environnement pour une application.
```
cf set-env nom_app nom_var valeur_var
```
<dl>
<dt>nom_app</dt>
<dd>Nom de l'application.</dd>
<dt>nom_var</dt>
<dd>Nom de la variable d'environnement.</dd>
<dt>valeur_var</dt>
<dd>Valeur de la variable d'environnement.</dd>
</dl>

## cf stacks

Répertorie toutes les piles. Une pile est un système de fichiers préconfiguré incluant un système
d'exploitation pouvant exécuter des applications.
```
cf stacks
```

## cf stop

Arrête une application.
```
cf stop nom_app
```
<dl>
<dt>nom_app</dt>
<dd>Nom de l'application.</dd>
</dl>

## cf -v

Affiche la version de l'interface de ligne de commande cf.
```
cf -v
```

# rellinks
{: #rellinks}
## general 
{: #general}
* [Fiche de référence rapide - Commandes cf](ftp://public.dhe.ibm.com/cloud/bluemix/cli_reference_card.pdf)
