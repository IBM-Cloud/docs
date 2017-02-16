---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-11"
---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Déploiement d'applications
{: #deployingapps}

Vous pouvez déployer des applications dans {{site.data.keyword.Bluemix}} via diverses méthodes, notamment en utilisant l'interface de ligne de commande et des environnements de développement intégré (IDE). Vous pouvez également utiliser des manifestes d'application afin de déployer des applications. L'utilisation d'un manifeste d'application vous permet de réduire le nombre d'informations de déploiement que vous devez spécifier à chaque fois que vous déployez une application dans {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Déploiement d'application
{: #appdeploy}

Le déploiement d'une application dans {{site.data.keyword.Bluemix_notm}} comporte deux étapes : la constitution de l'application et le démarrage de l'application.

Cloud Foundry prend en charge Diego, la nouvelle architecture d'exécution par défaut qui fournit plusieurs fonctions améliorant le développement d'applications pour l'hébergement et la construction de plateformes de cloud. Cette mise à jour de l'architecture améliore le fonctionnement globale et les performances de la plateforme Cloud Foundry. La nouvelle architecture prend en charge plusieurs technologies de conteneur d'applications, notamment Garden et Windows, un SSH qui permet de se connecter directement au conteneur d'applications, ainsi que d'autres modifications innovantes. Pour plus d'informations sur la mise à niveau récente de cette architecture, voir [{{site.data.keyword.Bluemix_notm}} Cloud Foundry: Diego is live ![icône de lien externe](../icons/launch-glyph.svg)](https://www.ibm.com/blogs/bluemix/2017/01/bluemix-cloud-foundry-diego-live/){: new_window}.


Toutes les nouvelles applications que vous créez s'exécutent sur Diego, et vous devez commencer à migrer vos applications existantes qui s'exécutent sur des agents DEA vers la nouvelle architecture Diego.

**Remarque** : l'architecture Diego Cloud Foundry affecte tous les environnements de région {{site.data.keyword.Bluemix_notm}} publics. Les environnements {{site.data.keyword.Bluemix_notm}} dédié et {{site.data.keyword.Bluemix_notm}} local seront mis à jour ultérieurement.

### Constitution d'une application
{: #diego}

Lors de la phase de constitution, Diego s'occupe de tous les aspects liés
à l'orchestration des conteneurs d'applications. Lorsque vous envoyez une
application par commande push, le contrôleur de cloud envoie une demande de
constitution à Diego, qui reprend à son tour l'allocation des instances de
l'application. Le back end Diego orchestre les conteneurs d'applications afin
de garantir la cohérence entre le long terme et la tolérance aux pannes, qui
équilibre la charge sur une série de machines virtuelles appelées cellules. Diego
garantit en outre aux utilisateurs un accès aux journaux de leurs
applications. Tous les composants Diego sont conçus pour être mis en cluster,
ce qui signifie que vous pouvez créer différentes zones de disponibilité.

Pour valider la santé des applications, Diego prend en charge les
vérifications PORT qui étaient utilisées pour l'agent DEA. Il est cependant conçu
pour pouvoir fonctionner avec davantage d'options génériques comme les
diagnostics d'intégrité basés sur les URL, qui devraient être activés
ultérieurement.

#### Constitution d'une nouvelle application
{: #stageapp}

Toutes les nouvelles applications sont déployées dans l'architecture
Diego. Pour constituer une nouvelle application, déployez cette dernière avec
la commande **cf push** :

  1. Déployez l'application :
  ```
  $ cf push NOM_APPLICATION
  ```

Pour plus de détails sur la commande **cf push**, voir [cf push](/docs/cli/reference/cfcommands/index.html#cf_push).

### Migration d'une application existante vers Diego
{: #migrateapp}

Diego est l'architecture Cloud Foundry par défaut pour
{{site.data.keyword.Bluemix_notm}} ; la prise en charge des agents DEA
va être supprimée, vous devez donc migrer toutes vos applications existantes en
les mettant à jour chacune à leur tour. Commencez la migration de vos
applications vers Diego en mettant chaque application à jour avec l'indicateur
Diego. L'application
tente immédiatement de s'exécuter sur Diego et arrête de s'exécuter sur les
agents DEA. 

Lors de la mise à jour d'une application de l'architecture DEA
vers Diego, il se peut que vous deviez faire face à un bref temps
d'indisponibilité, ou un temps d'indisponibilité prolongé si l'application
n'est pas compatible avec Diego. Pour réduire le temps d'indisponibilité, effectuez un [déploiement Blue-Green](/docs/manageapps/updapps.html#blue_green) en déployant une copie de votre application dans Diego, puis en permutant les routes et en retirant l'application de l'agent DEA.

Pour migrer votre application vers Diego, procédez comme suit :

 1.  Installez l'[interface de ligne de commande cf ![icône de lien externe](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window} et le plug-in [Diego-Enabler CLI Plugin ![icône de lien externe](../icons/launch-glyph.svg)](https://github.com/cloudfoundry-incubator/Diego-Enabler){:new_window}.
 2. Consultez la [liste des problèmes connus](depapps.html#knownissues).
 3. Définissez l'indicateur Diego pour que votre application
s'exécute sur Diego :
  ```
  $ cf enable-diego NOM_APPLICATION
  ```

Une fois l'application mise à jour, vérifiez qu'elle est démarrée. Si
l'application migrée ne parvient pas à démarrer, elle reste hors ligne jusqu’à
ce que vous ayez identifié et résolu le problème. Vous devez ensuite la
redémarrer.

IBM vous informera de la période de migration obligatoire à venir à
l'occasion de la suppression de la prise en charge de l'architecture DEA. Si, à
ce moment-là, vous n'avez pas encore migré vos applications, l'équipe
chargée des opérations les migrera pour vous.
  
Pour savoir sur quel back-end l'application est exécutée, utilisez la
commande suivante :

  ```
  $ cf has-diego-enabled NOM_APPLICATION
  ```

#### Problèmes connus liés à la migration vers Diego
{: #knownissues}

Vous risquez de rencontrer les problèmes connus suivants lors de la
migration de vos applications vers Diego :

  * Les applications de type travailleur déployées avec l’option `--no-route` ne sont pas indiquées comme en bon état de fonctionnement. Pour éviter cela, désactivez le diagnostic d'intégrité basé sur les ports à l'aide de la commande `cf set-health-check NOM_APP none`.
  * La commande **cf files** n'est plus prise en
charge. La commande **cf ssh** est utilisée à la place. Pour plus de détails sur la commande **cf ssh**, voir [cf ssh](/docs/cli/reference/cfcommands/index.html#cf_ssh).
  * Certaines applications peuvent utiliser un nombre élevé de
descripteurs de fichier (i-nodes). Si vous rencontrez ce problème, vous devez
augmenter le quota de disque de votre application à l'aide de la commande
`cf scale NOM_APP [-k DISK]`.

Pour obtenir la liste complète des problèmes connus, reportez-vous à la page de la documentation de Cloud Foundry [Migrating to Diego ![icône de lien externe](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/diego-design-notes/blob/master/migrating-to-diego.md){: new_window}.

Tant que la prise en charge de l'ancienne architecture DEA
n'est pas supprimée, vous pouvez exécuter la commande suivante pour revenir aux
agents DEA : `cf disable-diego NOM_APPLICATION`. Vous
pouvez également encore déployer de nouvelles applications dans
l'architecture DEA jusqu'à ce que sa prise en charge soit supprimée :

**Remarque** : l'[interface de ligne de commande cf ![icône de lien externe](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window} et le plug-in [Diego-Enabler CLI Plugin ![icône de lien externe](../icons/launch-glyph.svg)](https://github.com/cloudfoundry-incubator/Diego-Enabler){:new_window} doivent être tous les deux installés pour que vous puissiez utiliser la commande `disable-diego`.

1. Déployez l'application sans la démarrer :
```
$ cf push NOM_APPLICATION --no-start
```
2. Exécutez la commande disable-diego :
```
$ cf disable-diego NOM_APPLICATION
```
3. Démarrez l'application :
```
$ cf start NOM_APPLICATION
```

### Démarrage d'une application
{: #startapp}

Lorsqu'une application est démarrée, l'instance ou les instances du
conteneur d'applications sont créées. Dans le cas des applications exécutées
sur Diego, vous pouvez utiliser la commande **cf ssh** ou
**cf scp** pour accéder au système de fichiers du conteneur
d'applications qui inclut les journaux. La commande **cf
files** ne fonctionne pas pour les applications exécutées dans
l'architecture Diego.

**Remarque** : si certaines applications sont toujours
exécutées sur les agents DEA, vous pouvez utiliser la commande **cf
files** pour afficher les fichiers du conteneur d'applications
jusqu'à ce que la prise en charge des agents DEA soit supprimée.

Si l'application ne parvient pas à démarrer, elle est arrêtée et la
totalité du contenu du conteneur d'applications est supprimée. Par conséquent, si une application s'arrête ou que le processus de constitution d'une application échoue, vous ne pourrez pas utiliser ses fichiers journaux.

Si les journaux de votre application ne sont plus disponibles et que vous
ne pouvez donc plus utiliser la commande **cf ssh**,
**cf scp** ou **cf files** pour examiner
la cause des erreurs de constitution dans le conteneur d'applications, vous
pouvez utiliser à la place la commande **cf logs**. La commande **cf logs** utilise le regroupeur de journaux de Cloud Foundry pour collecter les informations de vos journaux d'application et de vos journaux système ; vous pouvez examiner ce qui a été collecté dans la mémoire tampon du regroupeur de journaux. Pour plus d'informations sur le regroupeur de journaux, voir [Logging in Cloud Foundry ![icône de lien externe](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html){:new_window}.

**Remarque :** La taille de la mémoire tampon est limitée. Si une application s'exécute pendant longtemps et n'est pas redémarrée, il se
peut que des journaux ne s'affichent pas lorsque vous entrez la commande
`cf logs nom_app --recent`, car il est possible que la mémoire
tampon des journaux ait été nettoyée. Par conséquent, pour déboguer les erreurs
de constitution d'une application volumineuse, vous pouvez entrer la commande
`cf logs nom_app` sur une ligne de commande distincte de
l'interface de ligne de commande cf afin d'effectuer le suivi des journaux
lorsque vous déployez l'application.

Si vous rencontrez des problèmes lors de la constitution de vos applications dans {{site.data.keyword.Bluemix_notm}}, vous pouvez suivre la procédure [Débogage des erreurs de constitution](/docs/debug/index.html#debugging-staging-errors) afin de résoudre le problème.


## Déploiement d'applications avec la commande cf
{: #dep_apps}

Lorsque vous déployez vos applications sur {{site.data.keyword.Bluemix_notm}} depuis l'interface de ligne de commande, un pack de construction doit être fourni comme environnement d'exécution en fonction du langage et de l'infrastructure de votre application. Vous pouvez également utiliser le service Delivery Pipeline afin de déployer des applications dans {{site.data.keyword.Bluemix_notm}}.

{{site.data.keyword.Bluemix_notm}} fournit des packs de construction intégrés qui prennent en charge Java et Node.js. Si vous utilisez ces langages et infrastructures, vous n'avez pas besoin de spécifier le pack de construction lorsque vous déployez votre application à l'aide de l'interface de ligne de commande. Etant donné que {{site.data.keyword.Bluemix_notm}} repose sur Cloud Foundry, la commande utilise par défaut ces packs de construction.

Si vous utilisez un pack de construction externe, vous devez spécifier son URL à l'aide de l'option **-b** lorsque vous déployez votre application sur {{site.data.keyword.Bluemix_notm}} depuis l'invite de commande.

  * Pour déployer des packages serveur Liberty dans {{site.data.keyword.Bluemix_notm}}, utilisez la commande suivante depuis votre répertoire source :

  ```
  cf push
  ```

  Pour plus d'informations sur le pack de construction Liberty, voir [Liberty for Java](/docs/runtimes/liberty/index.html).

  * Pour déployer des applications Java Tomcat dans {{site.data.keyword.Bluemix_notm}}, utilisez la commande suivante :

  ```
  cf push nom_app -b https://github.com/cloudfoundry/java-buildpack.git -p chemin_app
  ```

  * Pour déployer des packages WAR dans {{site.data.keyword.Bluemix_notm}}, utilisez la commande suivante :

  ```
  cf push nom_app -p app.war
  ```
  Ou bien, spécifiez un répertoire contenant vos fichiers d'application avec la commande suivante :

  ```
  cf push nom_app -p "./app"
  ```

  * Pour déployer des applications Node.js dans {{site.data.keyword.Bluemix_notm}}, utilisez la commande
suivante :

  ```
  cf push nom_app -p chemin_app
  ```

Un fichier `package.json` doit se trouver dans votre application Node.js pour que l'application soit reconnue par le pack de construction Node.js. Le fichier `app.js` est le script d'entrée pour l'application et peut être spécifié dans le fichier `package.json`. L'exemple suivant représente un fichier `package.json` simple :

  ```
  {
        "name": "MyUniqueNodejs01",
        "version": "0.0.1",
        "description": "A sample package.json file",
        "dependencies": {
                "express": ">=3.4.7 <4",
                "jade": ">=1.1.4"
        },
        "scripts": {
                "start": "node app.js"
        },
        "engines": {
                "node": ">=0.10.0"
        },
        "repository": {}
  }
  ```

  Pour plus d'informations sur le fichier
`package.json`, voir
[package.json
![icône de lien externe](../icons/launch-glyph.svg)](https://www.npmjs.org/doc/files/package.json.html){:new_window}.

  * Pour déployer des applications PHP, Ruby ou Python dans {{site.data.keyword.Bluemix_notm}}, utilisez la commande suivante depuis le répertoire contenant la source de votre application :

  ```
  cf push nom_app
  ```

### Déploiement d'une application dans plusieurs espaces

Une application est propre à l'espace dans lequel elle est déployée. Vous ne pouvez pas déplacer ou copier une application d'un espace à un autre dans {{site.data.keyword.Bluemix_notm}}. Pour déployer une application dans plusieurs espaces, vous devez la déployer dans chaque espace que vous voulez utiliser comme suit :

  1. Accédez à l'espace dans lequel vous souhaitez déployer votre application en utilisant la commande **cf target** avec l'option **-s** :

  ```
  cf target -s <nom_espace>
  ```

  2. Accédez au répertoire de l'application et déployez votre application avec la commande **cf push**, où nom_app doit être unique dans votre domaine.

  ```
  cf push nom_app
  ```

## Manifeste d'application
{: #appmanifest}

Les manifestes d'application contiennent des options qui sont appliquées à la commande **cf push**. Vous pouvez utiliser un manifeste d'application afin de réduire le nombre d'informations de déploiement que vous devez spécifier chaque fois que vous envoyez par commande push une application sur {{site.data.keyword.Bluemix_notm}}.

Dans les manifestes d'application, vous pouvez spécifier des options, comme le nombre d'instances d'application à créer, la quantité de mémoire et le quota de disque à allouer aux applications, ainsi que d'autres variables d'environnement pour l'application. Vous pouvez aussi utiliser des manifestes d'application pour automatiser le déploiement d'applications. Le nom par défaut d'un fichier manifeste est `manifest.yml`.

### Options prises en charge dans le fichier manifeste

Le tableau suivant décrit les options prises en charge que vous pouvez utiliser dans un fichier manifeste d'application. Si vous décidez d'utiliser un nom de fichier différent de `manifest.yml`, vous devez utiliser l'option **-f** avec la commande **cf push**. Dans l'exemple suivant, le nom du fichier est `appManifest.yml` :

```
cf push -f appManifest.yml
```

<p>  </p>


|Options	|Description	|Utilisation ou exemple|
|:----------|:--------------|:---------------|
|**buildpack**	|Adresse URL ou nom du pack de construction personnalisé.	|`buildpack: ` *URL_pack_construction*|
|**disk_quota**	|Quota de disque alloué à une application. La valeur par défaut est 1 G.	|`disk_quota: 500M`|
|**domain**	|Nom de domaine de l'application dans {{site.data.keyword.Bluemix_notm}}.	|`domain:` ng.bluemix.net|
|**host**	|Nom d'hôte de l'application dans {{site.data.keyword.Bluemix_notm}}. Cette valeur doit être unique dans l'environnement {{site.data.keyword.Bluemix_notm}}.	|`host: ` *nom_hôte*|
|**name**	|Nom de l'application dans {{site.data.keyword.Bluemix_notm}}. Cette valeur doit être unique dans l'environnement {{site.data.keyword.Bluemix_notm}}.	|`name: ` *nom_app*|
|**path**	|Emplacement de votre application. Cette valeur peut être un chemin relatif ou absolu.	|`path: ` *chemin_application*|
|**command**	|Commande de démarrage personnalisée pour votre application ou commande d'exécution des fichiers script.	|`command:` *commande_personnalisée* `command:` *bash ./run.sh*|
|**memory**	|Quantité de mémoire à allouer à l'application. La valeur par défaut est 1G.	|`memory: 512M`|
|**instances**	|Nombre d'instances à créer pour votre application.	|`instances: 2`|
|**timeout**	|Délai de démarrage maximal de l'application, en secondes. La valeur par défaut est 60 secondes.	|`timeout: 80`|
|**no-route**	|Valeur booléenne permettant d'empêcher d'affecter une route à l'application si l'application s'exécute seulement en arrière-plan. La valeur par défaut est **false**.	|`no-route: true`|
|**random-route**	|Valeur booléenne permettant d'affecter une route aléatoire à l'application. La valeur par défaut est **false**.	|`random-route: true`|
|**services**	|Services à lier à l'application.	|`services:   - mysql_maptest`|
|**env**	|Variables d'environnement personnalisées pour l'application.|`env: DEV_ENV: production`|
{: caption="Table 1. Supported options in the manifest YAML file" caption-side="top"}

### Exemple de fichier `manifest.yml`

L'exemple ci-dessous illustre un fichier manifeste pour une application Node.js
utilisant le pack de construction de communauté intégré Node.js dans {{site.data.keyword.Bluemix_notm}}.

```
--- - name: myNodejsapp
  memory: 256M
  disk_quota: 512M
  path: /dev/myNodejsApp
  buildpack: nodejs_buildpack
  host: nodejs001
  domain: mybluemix.net
  command: node app.js
  timeout: 80
  services:
  - mongo_8917
  env:
    env_type: production
```
{:codeblock}

## Variables d'environnement
{: #app_env}

Les variables d'environnement contiennent les informations relatives à l'environnement d'une application déployée dans {{site.data.keyword.Bluemix_notm}}. En plus des variables d'environnement définies par un *agent DEA (Droplet Execution Agent)* et les packs de construction, vous pouvez aussi
définir des variables d'environnement propres à l'application dans {{site.data.keyword.Bluemix_notm}}.

Vous pouvez afficher les variables d'environnement suivantes d'une application
{{site.data.keyword.Bluemix_notm}} en cours d'exécution en utilisant la commande **cf env** ou
l'interface utilisateur de {{site.data.keyword.Bluemix_notm}} :

  * Les variables définies par l'utilisateur, propres à une application. Pour savoir comment ajouter une variable définie par l'utilisateur à une application, voir [Ajout de variables d'environnement définies par l'utilisateur ![icône de lien externe](../icons/launch-glyph.svg)](#ud_env){:new_window}.

  * La variable VCAP_SERVICES, qui contient les informations de connexion pour l'accès à une instance de service. Si votre application est liée à
plusieurs services, la variable VCAP_SERVICES inclut les informations de connexion pour chaque instance de service. Exemple :

  ```
  {
   "VCAP_SERVICES": {
    "AppScan Dynamic Analyzer": [
     {
      "credentials": {
       "bindingid": "0ab3162a-867e-4137-a2e7-39463a89472e",
       "password": "xE/jh/PlRj3ruuy8RCl8JNyEywaivRH1xXSZcbVExKg="
      },
      "label": "AppScan Dynamic Analyzer",
      "name": "AppScan Dynamic Analyzer-9q",
      "plan": "standard",
      "tags": [
       "Security",
       "security",
       "ibm_created"
      ]
     }
    ],
    "mysql-5.5": [
     {
      "credentials": {
       "host": "23.246.200.38",
       "hostname": "23.246.200.38",
       "name": "d296abcc06c9e418b94abcaafdf547620",
       "password": "peRiYCG4ZYqu3",
       "port": 3307,
       "uri": "mysql://uzpGf7eGJ7mtB:peRiYCG4ZYqu3@23.246.200.38:3307/d296abcc06c9e418b94abcaafdf547620",
       "user": "uzpGf7eGJ7mtB",
       "username": "uzpGf7eGJ7mtB"
      },
      "label": "mysql-5.5",
      "name": "mysql-ix",
      "plan": "300",
      "tags": [
       "mysql",
       "relational",
       "data_management",
       "ibm_experimental"
      ]
     }
    ]
   }
  }
  ```

Vous avez aussi accès aux variables d'environnement qui sont définies par l'agent DEA et les packs de construction.

Les variables suivantes sont définies par l'agent DEA :

<dl>
  <dt><strong>HOME</strong></dt>
  <dd>Répertoire racine de l'application déployée.</dd>
  <dt><strong>MEMORY_LIMIT</strong></dt>
  <dd>Quantité de mémoire maximale que chaque instance de votre application peut utiliser. Vous pouvez spécifier la valeur dans un fichier <span class="ph filepath">manifest.yml</span> d'application ou sur la ligne de commande lorsque vous envoyez l'application par commande push.</dd>
  <dt><strong>PORT</strong></dt>
  <dd>Port sur l'agent DEA pour communication avec l'application. L'agent DEA affecte un port à l'application en phase de constitution.</dd>
  <dt><strong>PWD</strong></dt>
  <dd>Répertoire de travail en cours dans lequel le pack de construction s'exécute.</dd>
  <dt><strong>TMPDIR</strong></dt>
  <dd>Répertoire où sont stockés les fichiers de transfert et temporaires.</dd>
  <dt><strong>USER</strong></dt>
  <dd>ID utilisateur sous lequel s'exécute l'agent DEA.</dd>
  <dt><strong>VCAP_APP_HOST</strong></dt>
  <dd>Adresse IP de l'hôte DEA.</dd>
  <dt><strong>VCAP_APPLICATION</strong></dt>
  <dd>Chaîne JSON contenant des informations sur l'application déployée. Ces informations incluent le nom de l'application, les URI, les limites de mémoire, l'horodatage auquel l'application est parvenue à son statut en cours, etc. Par exemple :
  <pre class="pre codeblock"><code>
  {
    "limits": {
        "mem": 512,
        "disk": 1024,
        "fds": 16384
    },
    "application_version": "df111903-7d95-4c20-96d9-aad4e97d2a9a",
    "application_name": "testapp",
    "application_uris": [
        "testapp.AppDomainName.mybluemix.net"
    ],
    "version": "df111903-7d95-4c20-96d9-aad4e97d2a9a",
    "name": "testapp",
    "space_name": "dev",
    "space_id": "c6ed3a8e-436b-43ac-9f96-b676ee335000",
    "uris": [
        "testapp.AppDomainName.mybluemix.net"
    ],
    "users": null,
    "application_id": "e984bb73-4c4e-414b-84b7-c28c87f84003",
    "instance_id": "09f50e22848d4ec0b943e9e487c23569",
    "instance_index": 0,
    "host": "0.0.0.0",
    "port": 61399,
    "started_at": "2015-01-16 06:50:51 +0000",
    "started_at_timestamp": 1421391051,
    "start": "2015-01-16 06:50:51 +0000",
    "state_timestamp": 1421391051
}
</code></pre></dd>
  <dt><strong>VCAP_SERVICES</strong></dt>
  <dd>Chaîne JSON contenant des informations sur le service lié à l'application déployée. Par exemple :
  <pre class="pre codeblock"><code>
  {
    "mysql-5.5": [
        {
            "name": "mysql-ix",
            "label": "mysql-5.5",
            "tags": [
                "mysql",
                "relational",
                "data_management",
                "ibm_experimental"
            ],
            "plan": "300",
            "credentials": {
                "name": "d296abcc06c9e418b94abcaafdf547620",
                "hostname": "23.246.200.38",
                "host": "23.246.200.38",
                "port": 3307,
                "user": "uzpGf7eGJ7mtB",
                "username": "uzpGf7eGJ7mtB",
                "password": "peRiYCG4ZYqu3",
                "uri": "mysql://uzpGf7eGJ7mtB:peRiYCG4ZYqu3@23.246.200.38:3307/d296abcc06c9e418b94abcaafdf547620"
            }
        }
    ]
}
</code></pre></dd>

</dl>

Les variables définies par les packs de construction sont différentes pour chaque pack de construction. Pour connaître les autres packs de construction compatibles, voir [Buildpacks ![icône de lien externe](../icons/launch-glyph.svg)](https://github.com/cloudfoundry-community/cf-docs-contrib/wiki/Buildpacks){:new_window}.

<ul>
    <li>Les variables suivantes sont définies par le pack de construction Liberty :

	  <dl>
	  <dt><strong>JAVA_HOME</strong></dt>
	  <dd>Emplacement du logiciel SDK Java qui exécute l'application.</dd>
	  <dt><strong>IBM_JAVA_OPTIONS</strong></dt>
	  <dd>Options du logiciel SDK Java à utiliser lors de l'exécution de l'application.</dd>
	  <dt><strong>IBM_JAVA_COMMAND_LINE</strong></dt>
	  <dd>Commande Java permettant de démarrer une instance de serveur de profil Liberty dans l'agent DEA.</dd>
	  <dt><strong>WLP_USR_DIR</strong></dt>
	  <dd>Emplacement des ressources partagées et des définitions de serveur lors du démarrage d'une instance de serveur de profil Liberty dans l'agent DEA.</dd>
	  <dt><strong>WLP_OUTPUT_DIR</strong></dt>
	  <dd>Emplacement de la sortie générée, par exemple des fichiers journaux et du répertoire de travail d'une instance de serveur de profil Liberty en cours d'exécution.</dd>
	  </dl>
</li>   
<li>Les variables suivantes sont définies par le pack de construction Node.js :
	<dl>
	<dt><strong>BUILD_DIR</strong></dt>
	<dd>Répertoire de l'environnement d'exécution Node.js.</dd>
	<dt><strong>CACHE_DIR</strong></dt>
	<dd>Répertoire utilisé par l'environnement d'exécution Node.js pour la mise en cache.</dd>
	<dt><strong>PATH</strong></dt>
	<dd>Chemin de système utilisé par l'environnement d'exécution Node.js.</dd>
	</dl>
</li>
</li>
</ul>

Vous pouvez utiliser l'exemple de code Node.js suivant pour obtenir la valeur de la variable d'environnement VCAP_SERVICES :

```
if (process.env.VCAP_SERVICES) {
    var env = JSON.parse (process.env.VCAP_SERVICES);
    myvar = env.foo[bar].foo;
}
```

Pour plus d'informations sur chaque variable d'environnement, voir [Cloud Foundry Environment Variables ![icône de lien externe](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/devguide/deploy-apps/environment-variable.html){:new_window}.

## Personnalisation des déploiements d'application
{: #customize_dep}

Vous pouvez personnaliser les tâches de déploiement de vos applications. Par exemple, vous pouvez spécifier les commandes de démarrage de vos applications et configurer l'environnement de démarrage de votre application.
{:shortdesc}

### Spécification de commandes de démarrage

Vous pouvez spécifier des commandes de démarrage pour votre application de l'une des façons ci-après. Les commandes de démarrage que vous indiquez remplacent les commandes par défaut fournies par le pack de construction.

**Remarque :** si vous voulez que les commandes de démarrage du pack de construction soient prioritaires, spécifiez **null** comme commande de démarrage.

  * Utilisez la commande **cf push** et spécifiez le paramètre -c. Par exemple, lorsque vous déployez une application Node.js, vous pouvez spécifier la commande de démarrage **node app.js** avec le paramètre -c :

  ```
  cf push nom_app -p chemin_app -c "node app.js"
  ```

  * Utilisez le paramètre command dans le fichier `manifest.yml`. Par exemple, lorsque vous déployez une application Node.js, vous pouvez spécifier la commande de démarrage **node app.js** dans le fichier manifeste :

  ```
  command: node app.js
  ```


### Ajout de variables d'environnement définies par l'utilisateur
{: #ud_env}

Variables d'environnement définies par l'utilisateur spécifiques à une application. Vous disposez des options suivantes pour ajouter une variable d'environnement définie par l'utilisateur à une application en cours d'exécution :

  * Utilisez l'interface utilisateur {{site.data.keyword.Bluemix_notm}}. Procédez comme suit :
    1. Dans le tableau de bord {{site.data.keyword.Bluemix_notm}}, cliquez sur la vignette de votre application. La page des détails de l'application s'affiche.
	2. Cliquez sur **Variables d'environnement**.
	3. Cliquez sur **DEFINI PAR L'UTILISATEUR**, puis cliquez sur **AJOUTER**.
	4. Remplissez les zones obligatoires, puis cliquez sur **SAUVEGARDER**.
  * Utilisez l'interface de ligne de commande cf. Ajoutez une variable définie par l'utilisateur en utilisant la commande `cf set-env`. Exemple :
    ```
    cf set-env nom_app nom_var_env valeur_var_env
    ```

  * Utilisez le fichier `manifest.yml`. Ajoutez des paires de valeurs dans le fichier. Exemple :
    ```
	env:
      VAR1:valeur1
      VAR2:valeur2
    ```

Une fois que vous avez ajouté une variable d'environnement définie par l'utilisateur, vous pouvez utiliser l'exemple de code Node.js suivant pour
obtenir la valeur de la variable que vous avez définie :

```
var myEnv = process.env.nom_var_env;
console.log("My user defined = " + myEnv);
```

### Configuration de l'environnement de démarrage

Pour configurer l'environnement de démarrage de votre application,
vous pouvez ajouter des scripts shell dans le répertoire `/.profile.d`. Le répertoire `/.profile.d` est situé sous le répertoire de construction de votre application. Les scripts du répertoire `/.profile.d` sont exécutés par {{site.data.keyword.Bluemix_notm}} avant le démarrage de
l'application. Par exemple, vous pouvez associer la variable d'environnement NODE_ENV à la valeur **production** en plaçant un fichier
`node_env.sh` comportant le contenu suivant sous le répertoire `/.profile.d` :

```
export NODE_ENV=production;
```

###Empêcher le téléchargement de fichiers et de répertoires

Lorsque vous utilisez l'interface de ligne de commande cf pour déployer une application, vous pouvez réduire le temps de téléchargement en
ignorant
certains fichiers et répertoires que {{site.data.keyword.Bluemix_notm}} peut obtenir ailleurs. Pour empêcher le
téléchargement de ces fichiers et répertoires dans {{site.data.keyword.Bluemix_notm}}, vous pouvez créer un
fichier `.cfignore` dans le répertoire racine de votre application.

**Remarque :** le fichier `.cfignore` doit être au format UTF-8.

Le fichier `.cfignore` contient les noms des
fichiers et des répertoires à ignorer (un par ligne). Vous pouvez utiliser l'astérisque (*) comme caractère générique. Lorsque vous spécifiez un
répertoire, tous les fichiers et sous-répertoires qu'il contient sont également ignorés. Par exemple, le contenu suivant dans le fichier `.cfignore` indique qu'aucun fichier `.swp` et qu'aucun
fichier et sous-répertoire se trouvant dans le répertoire `tmp/` ne sera téléchargé dans
{{site.data.keyword.Bluemix_notm}}.

```
*.swp
tmp/
```

# Liens connexes
{: #rellinks}

## Liens connexes
{: #general}

* [Deploying with Application Manifests ![icône de lien externe](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html){:new_window}
* [CF Manifest Generator ![icône de lien externe](../icons/launch-glyph.svg)](http://cfmanigen.mybluemix.net/){:new_window}
* [Getting Started with cf v6 ![icône de lien externe](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/devguide/installcf/whats-new-v6.html){:new_window}
* [Initiation à IBM Continuous Delivery Pipeline for
Bluemix](/docs/services/DeliveryPipeline/index.html#getstartwithCD)
