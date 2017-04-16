---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# SDK for Nodejs
{: #nodejs_runtime}

L'environnement d'exécution Node.js sur {{site.data.keyword.Bluemix}} utilise la technologie du pack de construction sdk-for-nodejs.
Le pack de construction sdk-for-nodejs fournit un environnement d'exécution complet pour les applis Node.js.
{: shortdesc}

Le pack de construction sdk-for-nodejs est utilisé lorsque l'application contient un fichier **package.json** dans le répertoire racine.

## Application de démarrage
{: #starter_application}

{{site.data.keyword.Bluemix}} contient une application de démarrage Node.js.  L'application de démarrage Node.js est une appli Node.js simple qui peut servir de modèle pour votre appli. Vous pouvez expérimenter cette application de démarrage et effectuer des modifications, puis les envoyer par commande push vers l'environnement Bluemix. Pour obtenir de l'aide sur son utilisation, voir [Utilisation des applications de démarrage](/docs/cfapps/starter_app_usage.html).

## Commande de démarrage
{: #starup_commmand}

La méthode recommandée pour définir une commande de démarrage pour votre application Node.js Bluemix consiste à utiliser
un fichier **Procfile** ou **package.json**.

Pour définir une commande de démarrage dans votre fichier **Procfile**, suivez le modèle ci-dessous. Ici, app.js correspond au script startup.js de votre application.
```
web: node app.js
```
{: codeblock}

Sauvegardez
le fichier **Procfile** dans le répertoire racine de votre application.

S'il n'existe pas de fichier **Procfile**, le pack de construction Node.js d'IBM
Bluemix recherche une entrée scripts.start dans le fichier **package.json**. Dans l'exemple ci-dessous, app.js est le script js de démarrage de votre application.
```
{
    ...   
    "scripts": {
      "start": "node app.js"
    }
}
```
{: codeblock}

Si une entrée de script de démarrage existe dans le fichier **package.json**, un fichier **Procfile** est généré
automatiquement. Le contenu du fichier **Procfile** généré automatiquement est le suivant :
```
    web: npm start
```
{: codeblock}

Pour plus d'informations sur les fichiers **Procfile** et **package.json**, voir [Tips for Node.js Applications ](https://docs.cloudfoundry.org/buildpacks/node/node-tips.html).

## Astuces pour l'exécution locale de votre application Node.js
{: #hints}

Les informations ci-dessous permettent d'exécuter l'application Node.js à la fois en local et sur Bluemix.

L'exemple suivant montre une partie du code source d'un fichier **js** :
```
var port = (process.env.PORT || 3000);
```
{: codeblock}

Avec ce code, lorsque l'application s'exécute sur Bluemix, la variable d'environnement PORT contient la valeur de port interne à Bluemix, sur laquelle l'appli est à l'écoute des connexions entrantes. Lorsque l'application s'exécute en local, PORT n'est pas définie. La valeur **3000** est donc utilisée comme numéro de port. Le code rédigé ainsi permet d'exécuter l'application localement à des fins de test et sur Bluemix sans autres modifications.

## Mode Hors ligne
{: #offline_mode}

Voir [Mode Hors ligne](offlineMode.html) pour plus d'informations sur le contrôle de l'accès du pack de construction aux sites externes. 

## App Management
{{site.data.keyword.Bluemix}} fournit un certain nombre d'utilitaires pour la gestion et le débogage de l'appli Node.js. Pour plus de détails, voir [App Management](/docs/manageapps/app_mng.html).

## Versions disponibles
{: #available_versions}

{{site.data.keyword.Bluemix}} fournit tous les
[contextes d'exécution Node.js disponibles actuellement](http://nodejs.org/dist/). Pour ceux-ci, IBM propose des versions comportant des améliorations et des correctifs. Pour plus d'informations, voir [Mises à jour les plus récentes du pack de construction Node.js](/docs/runtimes/nodejs/updates.html).

Le pack de construction IBM Node.js met en cache les versions de l'environnement d'exécution IBM. Par conséquent, si vous utilisez l'environnement d'exécution IBM SDK for Node.js dans votre
application, vous obtenez de meilleures performances pour l'application lorsque celle-ci est envoyée dans Bluemix.

Utilisez le paramètre **node** de la section **engines** du fichier **package.json** pour définir la version
de l'environnement d'exécution Node.js à exécuter.

Utilisez le paramètre **npm** de la section **engines** du fichier **package.json** pour définir une version de npm différente de celle qui est intégrée à Node.js.  

Voir l'exemple suivant :

```
{
  "name": "myapp",
  "description": "this is my app",
  "version": "0.1",
  "engines": {
     "node": "4.2.4",
     "npm": "2.11.3"
  }
}
```
{: codeblock}

La version de Node doit toujours être précisée dans le fichier **package.json**. Si elle est omise, la version la plus
récente est utilisée.

## Options de configuration
{: #configuration_options}

### Scripts NPM
{: #npm_scripts}
NPM est doté d'une fonction permettant d'exécuter des scripts, y compris les scripts de **pré-installation** et de **post-installation** qui sont appliqués avant et après l'installation de node_modules.  Voir [npm-scripts](https://docs.npmjs.com/misc/scripts) pour plus d'informations.

### Comportement du cache
{: #cache_behavior}
{{site.data.keyword.Bluemix}} gère un répertoire de cache par application node, qui est conservé d'une génération à l'autre. Le cache stocke les dépendances résolues pour qu'elles ne soient pas téléchargées et installées à chaque déploiement de l'appli.  Supposons, par exemple, que myapp dépende d'**express**.  Lors du premier déploiement de myapp, le module **express** est téléchargé.  Lors des déploiements suivants, l'instance d'**express** mise en cache est utilisée. Le comportement par défaut consiste à mettre en cache tous les modules node_modules installés par NPM et tous les composants bower_components installés par bower.

Utilisez la variable NODE_MODULES_CACHE pour déterminer si le pack de construction Node utilise ou ignore le cache des générations précédentes. La valeur par défaut est true.  Pour désactiver la mise en cache, définissez NODE_MODULES_CACHE sur false, par exemple par la ligne de commande cf :
```
    $ cf set-env myapp NODE_MODULES_CACHE false
```
{: codeblock}

Notez que les modules node_modules qui font partie intégrante de votre application ne sont pas mis en cache.

Vous pouvez utiliser un tableau **cacheDirectories** dans votre fichier **package.json** de niveau supérieur pour contrôler avec une granularité fine la liste des modules mis en cache.  Lorsque l'élément de tableau**cacheDirectories** est présent dans **package.json**, seuls les modules qu'il contient seront mis en cache.  Dans l'exemple suivant, seuls les modules node_modules et bower_components sont mis en cache.
```
{
  "cacheDirectories": ["node_modules","bower_components"],
  ...
}
```
{: codeblock}

### MODE FIPS
{: #fips_mode}

Les packs de construction Nodejs versions v3.2-20160315-1257 et ultérieur prennent en charge [FIPS](https://en.wikipedia.org/wiki/Federal_Information_Processing_Standards).  Pour utiliser un moteur de noeud activé par FIPS, affectez la valeur true à la variable d'environnement FIPS_MODE.
Par exemple :

```
    $ cf set-env myapp FIPS_MODE true
```
{: codeblock}

Il est important de comprendre que lorsque la variable d'environnement FIPS_MODE a pour valeur true, certains modules de noeud peuvent ne pas fonctionner.  Par exemple, les **modules de noeud qui utilisent [MD5](https://en.wikipedia.org/wiki/MD5) échoueront**, par exemple, [Express](http://expressjs.com/).  Pour Express, le fait d'affecter la valeur false à [etag](http://expressjs.com/en/api.html) dans votre application Express peut vous permettre de contourner ce problème. Ainsi, vous pouvez introduire la commande suivante dans votre code :
```
    app.set('etag', false);
```
{: codeblock}
Voir cet [article stackoverflow](http://stackoverflow.com/questions/15191511/disable-etag-header-in-express-node-js) pour plus d'informations.

**REMARQUE** : Les variables d'environnement [App Management](/docs/manageapps/app_mng.html) et FIPS_MODE *NE PEUVENT PAS* être utilisées en même temps. Si la variable d'environnement BLUEMIX_APP_MGMT_ENABLE est définie et que la variable d'environnement FIPS_MODE a pour valeur true, la reconstitution de l'application échoue.

Il existe diverses méthodes permettant de vérifier l'état de FIPS_MODE :
<ul>
<li> Vous pouvez rechercher dans le fichier staging_task.log de votre application un message semblable à celui présenté ci-dessous :    

  <pre>
  Installing FIPS-enabled IBM SDK for Node.js (4.4.3) from cache
  </pre>
  {: codeblock}

Ce message indique qu'un moteur node.js activé par FIPS est en cours d'exécution, ce qui ne signifie pas nécessairement que FIPS est actif.
</li>

<li> Vous pouvez vérifier la valeur de **process.versions.openssl**. Par exemple :

  <pre>
  console.log('ssl version is [' +process.versions.openssl +']');
  </pre>
  {: codeblock}

Si la version de SSL contient "fips", la version de SSL utilisée prend en charge FIPS.  
</li>

<li> Pour node.js version 6 ou ultérieure, vous pouvez vérifier la valeur renvoyée par crypto.fips dans du code tel que le suivant :

  <pre>
  console.log('crypto.fips== [' +crypto.fips +']');
  </pre>
  {: codeblock}

Si la valeur renvoyée est 1, cela signifie que FIPS est utilisé. Notez que crypto.fips renverra *undefined* pour les versions de node.js antérieures à la version 6.
</li>
</ul>

#### Nodejs v4
{: #nodejs_v4_fips}

Le tableau suivant explique le comportement de node.js V4 avec FIPS :

|                 | Résultat        |
| :-------------- | :------------ |
|FIPS_MODE=true   |success (1)    |
|FIPS_MODE !=true |success (2)    |

* success (1)
  * FIPS est utilisé.
  * Le fichier staging_task.log contiendra le message *Installing FIPS-enabled IBM SDK for Node.js*.
  * La valeur renvoyée par process.versions.openssl contiendra "fips".
* success (2)
  * FIPS n'est *PAS* utilisé.
  * Le fichier staging_task.log ne contiendra *PAS* le message *Installing FIPS-enabled IBM SDK for Node.js*.
  * La valeur renvoyée par process.versions.openssl ne contiendra *PAS* "fips".

#### Nodejs v6
{: #nodejs_v6_fips}

Pour exécuter le mode FIPS avec Node.js version 6 en plus de définir **FIPS_MODE=true**, vous devez également inclure **--enable-fips** dans votre commande start, comme dans l'exemple suivant :
```
{
    ...   
    "scripts": {
      "start": "node --enable-fips app.js"
    }
}
```
{: codeblock}

Le tableau suivant explique le comportement de node.js V6 avec FIPS :

|                 |--enable-fips  |NO --enable-fips |
| :-------------- | :------------ | :-------------- |
|FIPS_MODE=true   |success (1)    |success (2)      |
|FIPS_MODE !=true |failure (3)    |success (4)      |

* success (1)
  * FIPS est utilisé.
  * Le fichier staging_task.log contiendra le message *Installing FIPS-enabled IBM SDK for Node.js*.
  * La valeur renvoyée par process.versions.openssl contiendra "fips".
  * crypto.fips renverra 1 pour indiquer que FIPS est utilisé.
* success (2)
  * FIPS n'est *PAS* utilisé.
  * Le fichier staging_task.log contiendra le message *Installing FIPS-enabled IBM SDK for Node.js*.
  * La valeur renvoyée par process.versions.openssl contiendra "fips".
  * crypto.fips renverra 0 pour indiquer que FIPS n'est *PAS* utilisé.
* failure (3)
  * FIPS n'est *PAS* utilisé.
  * Le fichier staging_task.log ne contiendra *PAS* le message *Installing FIPS-enabled IBM SDK for Node.js*.
  * La reconstitution échouera avec le message "ERR node: bad option: --enable-fips".
* success (4)
  * FIPS n'est *PAS* utilisé.
  * Le fichier staging_task.log ne contiendra *PAS* le message *Installing FIPS-enabled IBM SDK for Node.js*.
  * La valeur renvoyée par process.versions.openssl ne contiendra *PAS* "fips".
  * crypto.fips renverra 0 pour indiquer que FIPS n'est *PAS* utilisé.


## Packs de construction Node.js

Bluemix fournit plusieurs versions du pack de construction Node.js.
* Le pack de construction **sdk-for-nodejs** créé par IBM est le pack de construction par défaut utilisé pour les applications Node.js dans Bluemix.
* **nodejs_buildpack** est un pack de construction de communauté fourni par la communauté Cloud Foundry.

Le pack de construction **sdk-for-nodejs** a
priorité sur le pack de construction **nodejs_buildpack** dans Bluemix. Si vous
voulez utiliser le pack de construction **nodejs_buildpack** avec votre application au lieu du pack de construction **sdk-for-nodejs**, vous devez indiquer votre pack de construction, par exemple à l'aide de la commande **cf push**
et de l'option -b.

Généralement, le pack de construction **sdk-for-nodejs** en cours et une version antérieure sont disponibles.  Pour voir l'ensemble des packs de construction disponibles, utilisez la commande**cf buildpacks**.  Par exemple :
<pre>
      cf buildpacks
      Getting buildpacks...

      buildpack                      position          enabled          locked          filename   

      sdk_for_nodejs                            2          true      false    buildpack_sdk-for-nodejs_v2.8-20151209-1403.zip   
      nodejs_buildpack                          5          true      false    nodejs_buildpack-cached-v1.5.0.zip   
      sdk-for-nodejs_v2_7-20151118-1003         17         true      false    buildpack_sdk-for-nodejs_v2.7-20151118-1003.zip
</pre>
{: codeblock}

# rellinks
{: #rellinks}
## general
{: #general}
* [Mises à jour les plus récentes du pack de construction Node.js](/docs/runtimes/nodejs/updates.html)
* [App Management](/docs/manageapps/app_mng.html)
* [Node.js](https://nodejs.org)
* [IBM API Connect](https://strongloop.com/)
