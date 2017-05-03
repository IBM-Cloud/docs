---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-11"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Mode Hors ligne pour node.js
{: #offline_mode}

Quand une application node.js est envoyée par push vers {{site.data.keyword.Bluemix}}, le kit SDK pour le pack de construction Node.js télécharge des artefacts depuis des ressources externes (modules de noeuds depuis NPM, par exemple).  Dans certaines
situations, comme avec [Bluemix dédié](/docs/dedicated/index.html#dedicated) et
[Bluemix local](/docs/local/index.html#local), vous pouvez vouloir ne pas accéder à des sites externes à Bluemix, ou préférer avoir un contrôle plus explicite sur ces derniers.  
{: shortdesc}

Les sites externes accessibles au pack de construction node.js sont répertoriés ci-dessous. Dans les environnements [Bluemix dédié](/docs/dedicated/index.html#dedicated) et
[Bluemix local](/docs/local/index.html#local), ces sites peuvent avoir besoin d'être mis en *liste blanche*.

* http://nodejs.org/ peut être utilisé pour déterminer les versions du moteur de noeud disponibles.
* https://s3pository.heroku.com sert à extraire les versions du moteur de noeud non incluses dans le pack de construction.
*  https://www.npmjs.com/package/npm et https://semver.herokuapp.com sont utilisés pour extraire les versions de npm non incluses dans le pack de construction.
* https://iojs.org permet d'extraire une version antérieure d'un noeud qui n'est pas contenue dans le pack de construction ou non disponible sur https://semver.herokuapp.com.
* https://registry.npmjs.org est utilisé pour extraire des modules de noeud comme express.

Pour réduire l'ensemble des sites mis en liste blanche, configurez vos applications de noeud pour utiliser une version de moteur de noeud qui est incluse  dans le pack de construction du kit SDK pour Node.js.  Voir [Dernières mises à jour](./updates.html) pour connaître l'ensemble des versions de moteur de noeud incluses dans le pack de construction.  Si vous procédez ainsi, seul le site https://registry.npmjs.org sera requis pour télécharger les modules de noeud.

Sachez que quand de nouvelles versions du pack de construction du kit SDK pour Node.js sont installées, l'ensemble des versions de moteur de noeud disponibles est mis au niveau des nouvelles versions,  ce qui risque de rendre nécessaire une reconfiguration de votre application de noeud pour spécifier une nouvelle version du moteur de noeud.


## Applications hors ligne
{: #offline_applications}

Pour éliminer le besoin d'accéder à https://registry.npmjs.org, vous pouvez inclure dans votre application tous les modules de noeud dont cette dernière a besoin.  Pour ce faire, exécutez **npm install** pour tous les modules requis par votre application et incluez le répertoire *node_modules* au sein de votre application envoyée par push.

Notez que vos dépendances peuvent avoir des dépendances qui, elles mêmes, auront des dépendances et ainsi de suite, mais package.json ne contient que les dépendances de niveau supérieur. Si l'une des dépendances utilise une plage de package.json et qu'une nouvelle version de celle-ci est publiée, les modules de votre répertoire node_modules peuvent devenir obsolètes. *Shrinkwrap* vous permet de verrouiller toutes les versions de dépendances afin d'empêcher que cela ne se produise.  Pour utiliser shrinkwrap, démarrez avec un répertoire node_modules propre ou vide puis,  dans le répertoire racine de votre projet, exécutez :
0. npm install
1. npm dedupe
2. npm shrinkwrap

Il est possible que le fichier *package.json* en soit modifié et que le fichier *npm-shrinkwrap.json* soit ajouté à votre répertoire racine.
Dès que vous effectuez un changement dans les dépendances du fichier *package.json*, répétez les étapes *dedupe* et *shringwrap*.

## Utilisation d'un proxy
{: #working_with_proxy}

Dans certains environnements, comme [Bluemix dédié](/docs/dedicated/index.html#dedicated) et
[Bluemix local](/docs/local/index.html#local), un proxy peut être configuré. Voir
[Utilisation d'un proxy](/docs/manageapps/workingWithProxy.html) pour plus de détails.
