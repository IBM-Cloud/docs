---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Options de configuration
{: #configuration_options}
{: shortdesc}

Une variété d'options sont à votre disposition pour configurer le pack de construction sdk-for-nodejs. 

## Scripts NPM
{: #npm_scripts}
NPM est doté d'une fonction permettant d'exécuter des scripts, y compris les scripts de **pré-installation** et de **post-installation** qui sont appliqués avant et après l'installation de node_modules.  Pour des détails complets, consultez [npm-scripts ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.npmjs.com/misc/scripts).

## Comportement du cache
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
