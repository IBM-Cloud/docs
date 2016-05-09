---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# A propos de {{site.data.keyword.openwhisk}}

*Dernière mise à jour : 22 février 2016*

Les sections ci-après présentent {{site.data.keyword.openwhisk}} en détail.
{: shortdesc}

## Fonctionnement d'{{site.data.keyword.openwhisk_short}}
{: #openwhisk_how}

{{site.data.keyword.openwhisk_short}} est une plateforme de calcul gérée par des événements et qui exécute un code en réponse à des événements
ou à des appels directs.

La figure ci-dessous présente l'architecture générale d'{{site.data.keyword.openwhisk_short}}.

![Architecture d'{{site.data.keyword.openwhisk_short}}](OpenWhisk.png)

Par exemple, les événements peuvent être des modifications apportées aux enregistrements d'une base de données, des relevés de capteur IoT
dépassant une certaine température, de nouvelles validations de code dans un référentiel GitHub ou des demandes HTTP simples provenant
d'applications Web ou mobiles. Les événements provenant de sources d'événements externes et internes sont canalisés via un déclencheur, et des règles
permettent de réagir à ces événements par le biais d'actions.

Les actions peuvent être de petits fragments de code JavaScript ou Swift, ou des fichiers binaires personnalisés imbriqués dans un conteneur Docker. Les
actions dans {{site.data.keyword.openwhisk_short}} sont instantanément déployées et exécutées à chaque fois qu'un déclencheur est exécuté. Plus le
nombre de déclencheurs exécutés est élevé, plus le nombre d'actions appelées est élevé. Si aucun déclencheur n'est exécuté, aucun code d'action n'est
exécuté et par conséquent, aucun frais n'est engendré.

En plus d'associer des actions à des déclencheurs, il est possible d'appeler une action directement à l'aide de l'API
{{site.data.keyword.openwhisk_short}}, de l'interface de ligne de commande ou du logiciel SDK pour iOS. Des actions peuvent également être
assemblées sans qu'il ne soit nécessaire d'écrire un code. Chaque action de la chaîne est appelée séquentiellement ; la sortie d'une action est transmise
en tant qu'entrée à l'action suivante dans la séquence.

Avec les machines virtuelles ou les conteneurs à exécution longue classiques, il est courant de déployer plusieurs machines virtuelles ou conteneurs
pour assurer la résilience en cas d'indisponibilité d'une instance unique. Toutefois, {{site.data.keyword.openwhisk_short}} propose un modèle
alternatif sans coût supplémentaire lié à la résilience. L'exécution des actions à la demande assure une évolutivité inhérente et une utilisation
optimale car le nombre d'actions en cours d'exécution correspond toujours à la fréquence de déclenchement. De plus, le développeur se consacre désormais
uniquement à son code et ne se préoccupe pas de la surveillance, de la mise à jour et de la sécurisation de l'infrastructure de serveur, de
stockage, de réseau et de système d'exploitation sous-jacente.

Des intégrations à des services et à des fournisseurs d'événements supplémentaires peuvent être ajoutées à l'aide de packages. Un package est un
regroupement de flux et d'actions. Un flux est un élément de code qui configure une source d'événements externe en vue de l'exécution d'événements
déclencheurs. Par exemple, un déclencheur créé avec un flux de modifications Cloudant configure un service de sorte qu'il exécute le déclencheur à chaque
fois qu'un document est modifié ou ajouté dans une base de données Cloudant. Les actions dans les packages représentent une logique réutilisable
qu'un fournisseur de services peut mettre à disposition pour que les développeurs puissent utiliser le service en tant que source d'événements, mais
aussi appeler les API de ce service.

Un catalogue de packages existant permet d'améliorer les applications avec des fonctions utiles et d'accéder à des services externes dans
l'écosystème rapidement. Cloudant, The Weather Company, Slack et GitHub sont des exemples de service externe compatibles avec {{site.data.keyword.openwhisk_short}}.


## Scénarios d'utilisation courants
{: #openwhisk_use_cases}

Le modèle d'exécution proposé par {{site.data.keyword.openwhisk_short}} prend en charge divers scénarios d'utilisation. Les sections ci-après
présentent des exemples classiques.

### Décomposition d'applications en microservices
La nature modulaire et intrinsèquement évolutive d'{{site.data.keyword.openwhisk_short}} en fait un service idéal pour
l'implémentation d'éléments de logique granulaires dans les actions. Par exemple, {{site.data.keyword.openwhisk_short}} peut être utile pour éliminer des tâches (d'arrière-plan) dont la charge est intensive et
potentiellement pointues, et pour implémenter ces tâches en tant qu'actions.

### Système de back end mobile
De nombreuses applications mobiles requièrent une logique côté serveur. Etant donné que les développeurs d'applications mobiles ne possèdent
généralement pas d'expérience en matière de logique côté serveur et préfèrent se consacrer à l'exécution de l'application sur le périphérique,
l'utilisation
d'{{site.data.keyword.openwhisk_short}} comme système de back end côté serveur constitue une bonne solution. De plus, la prise en charge intégrée
de Swift permet aux développeurs de réutiliser leurs compétences en programmation iOS.

### Traitement de données
Etant donné la quantité de données désormais disponible, le développement d'applications doit pouvoir traiter de nouvelles données, et
éventuellement y
réagir. Cette exigence inclut le traitement d'enregistrements de base de données structurés ainsi que de vidéos, d'images ou de documents non structurés.

### IoT
Souvent, les scénarios Internet of Things dépendent intrinsèquement d'un capteur. Par exemple, une action dans
{{site.data.keyword.openwhisk_short}} peut être déclenchée s'il est nécessaire de réagir à un relevé de capteur dépassant une température
particulière.



