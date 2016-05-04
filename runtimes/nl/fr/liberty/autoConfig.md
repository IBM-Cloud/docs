---

Copyright :
  Années : 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Configuration automatique des services liés
{: #auto_config}

*Dernière mise à jour : 31 mars 2016*

Vous pouvez lier divers services à votre application Liberty. Les services peuvent être gérés par le conteneur, gérés par l'application, ou les deux, selon le souhait du développeur.

Un service géré par l'application désigne un service complètement géré par l'application, sans aucune assistance de Liberty. L'application lit normalement la variable VCAP_SERVICES pour obtenir des informations sur le service lié et accède directement au service. L'application fournit tout le code d'accès client nécessaire. Il n'existe aucune dépendance par rapport aux fonctions Liberty ou à la configuration du fichier server.xml. La configuration automatique par le pack de construction Liberty ne s'applique pas aux services de ce type.

Un service géré par le conteneur désigne un service qui est géré par le contexte d'exécution Liberty. Dans certains cas, l'application peut rechercher le service lié dans JNDI, alors que dans d'autres cas, le service est utilisé directement par Liberty lui-même. Le pack de construction Liberty lit VCAP_SERVICES afin d'obtenir des informations sur les services liés. Pour chaque service géré par le conteneur, le pack de construction effectue trois opérations :

* Génère des [variables de cloud](optionsForPushing.html#accessing_info_of_bound_services) pour le service lié.
* Il installe les fonctions Liberty et le code d'accès  client requis pour accéder au service lié.
* Il génère ou met à jour les sections du fichier server.xml qui sont requises par le service.

Ce processus est dénommé configuration automatique.
Le pack de construction Liberty se charge de la configuration automatique des types de service suivants :

* [SQL Database](../../services/SQLDB/index.html#SQLDB)
* Base de données ClearDB MySQL
* [MySQL](../../services/MySQL/index.html#MySQL)
* ElephantSQL
* [PostgreSQL](../../services/PostgreSQL/index.html#PostgreSQL)
* [Cloudant NoSQL Database](../../services/Cloudant/index.html#Cloudant)
* MongoLab
* [dashDB](../../services/dashDB/index.html#dashDB)
* [Data Cache](../../services/DataCache/index.html#data_cache)
* [Session Cache](../../services/SessionCache/index.html#session_cache)
* [MQ Light](../../services/MQLight/index.html#mqlight010)
* [Monitoring and Analytics](../..//services/monana/index.html#gettingstartedtemplate)
* [Auto-Scaling](../../services/Auto-Scaling/index.html#autoscaling)
* [Single Sign On](../../services/SingleSignOn/index.html#sso_gettingstarted)
* [New Relic](newRelic.html)
* [Dynatrace](dynatrace.html)

Comme mentionné, certains services peuvent être soit gérés par l'application, soit gérés par le conteneur. Mongo et SQLDB sont des exemples de tels services. Par défaut, le pack de construction Liberty suppose que ces services sont gérés par le conteneur et les configure automatiquement. Si vous souhaitez que le service soit géré par l'application, vous pouvez résilier la configuration automatique du service en configurant la variable d'environnement services_autoconfig_excludes. Pour plus d'informations, voir [Résiliation de la configuration automatique des services](autoConfig.html#opting_out).

## Installation des fonctions Liberty et du code d'accès client
{: #installation_of_liberty_features}

Lorsque vous créez une liaison à un service géré par le conteneur, le service peut nécessiter une configuration de fonctions Liberty dans la section featureManager du fichier server.xml. Le pack de construction Liberty met à jour la section featureManager et installe les fichiers binaires de support requis. Si le service requiert des fichiers Jar de pilote client, ces fichiers Jar sont téléchargés à un emplacement prédéterminé dans le répertoire d'installation de
Liberty.

Pour plus d'informations, voir la documentation relative au type de service lié.

## Génération ou mise à jour des sections de configuration dans le fichier server.xml
{: #generating_or_updating_serverxml}

Lorsque vous envoyez une application autonome par commande push, le pack de construction Liberty génère la section server.xml comme décrit dans la rubrique [Options pour l'envoi par commande push d'applications Liberty](optionsForPushing.html#options_for_pushing) vers Bluemix. Lorsque vous envoyez une application autonome par commande push et que vous la liez à des services gérés par conteneur, le pack de construction Liberty génère les sections server.xml requises pour les services liés.

Lorsque vous fournissez un fichier server.xml et que vous créez une liaison avec des services gérés par conteneur, le pack de construction Liberty effectue les opérations suivantes :

* Génération de la configuration pour les services liés si le fichier server.xml fourni ne comporte pas de sections de configuration pour ces services.
* Mise à jour de la configuration des services liés si le fichier server.xml fourni comporte déjà des sections de configuration pour ces services.

Pour plus d'informations, voir la documentation relative au type de service lié.

## Résiliation de la configuration automatique des services
{: #opting_out}

Dans certains cas, vous ne souhaiterez peut-être pas que le pack de construction Liberty configure automatiquement les services qui ont été liés. Considérez les scénarios suivants :

* Votre application utilise la base de données MongoDB, mais vous désirez que l'application gère directement la connexion à la base de données. L'application contient le fichier Jar de pilote client requis. Vous ne voulez pas que le pack de construction Liberty configure automatiquement le service Mongo.
* Vous avez soumis un fichier server.xml comportant les sections de configuration pour l'instance SQLDB car vous avez besoin d'une configuration de source de données non standard. Vous ne voulez pas que le pack de construction Liberty mette à jour le fichier server.xml, mais vous souhaitez tout de même qu'il vérifie que le logiciel de prise en charge est installé.

Pour résilier la configuration automatique des services, utilisez alors la variable d'environnement services_autoconfig_excludes. Vous pouvez inclure cette variable d'environnement dans un fichier manifest.yml ou la définir à l'aide du client cf.

Vous pouvez résilier la configuration automatique des services sur une base individuelle. Vous pouvez opter pour une résiliation complète (comme dans le scénario Mongo) ou pour une résiliation des mises à jour de la configuration du fichier server.xml (comme dans le scénario SQLDB). La valeur que vous spécifiez dans la variable d'environnement services_autoconfig_excludes est une chaîne dotée des caractéristiques suivantes :

* La chaîne peut contenir des spécifications pour un ou plusieurs services.
* La spécification de la résiliation pour un service donné est type_service=option, où :
  * type_service est le label du service tel que mentionné dans VCAP_SERVICES.
  * L'option peut recevoir soit la valeur "all", soit la valeur "config".
* Si la chaîne contient une spécification de résiliation pour plusieurs services, les spécifications individuelles doivent être séparées par un espace unique.

Plus formellement, la syntaxe de la chaîne est la suivante :

```
    Opt_out_string :: <spécification_type_service[<délimiteur>spécification_type_service]*
    <spécification_type_service> :: <type_service>=<option>
    <type_service> :: type de service (label du service tel qu'il figure dans VCAP_SERVICES)
    <option> :: all | config
    <délimiteur> :: un seul espace
```
{: #codeblock}

**Important** : Le type de service que vous indiquez doit correspondre au libellé des services tel qu'il figure dans la variable d'environnement VCAP_SERVICES. Le caractère espace n'est pas admis.
**Important** : Aucun espace n'est autorisé dans une entrée <spécification_type_service>. L'unique utilisation admise d'un espace est pour la séparation de plusieurs instances de <spécification_type_service>.

Utilisez l'option "all" pour résilier toutes les actions de configuration automatique de services, comme dans le scénario Mongo ci-dessus. Utilisez l'option "config" pour ne résilier que les actions de mise à jour de configuration, comme dans le scénario SQLDB ci-dessus.

Voici quelques de résiliation de configuration automatique dans un fichier manifest.yml pour les scénarios Mongo et SQLDB.

```
    env:
      services_autoconfig_excludes: mongodb-2.2=all

    env:
      services_autoconfig_excludes: sqldb=config

    env:
      services_autoconfig_excludes: sqldb=config mongodb-2.2=all
```
{: #codeblock}

Ci-dessous figurent des exemples de définition de la variable d'environnement services_autoconfig_excludes pour l'application myapp à l'aide de l'interface de ligne de commande.

```
    $ cf set-env myapp services_autoconfig_excludes sqldb=config
    $ cf set-env myapp services_autoconfig_excludes "sqldb=config mongodb-2.2=all"
```
{: #codeblock}

# rellinks
## general
* [Environnement d'exécution Liberty](index.html)
* [Présentation de Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
