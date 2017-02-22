---



copyright:

  years: 2015，2017

lastupdated: "2016-03-02"



---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:download: .download}

# Commencer à coder avec Git

Vous pouvez créer un référentiel Git hébergé qui se déploie automatiquement dans {{site.data.keyword.Bluemix}}. Ensuite, vous pouvez modifier le code qui s'exécute dans votre application en envoyant par commande push les modifications dans le référentiel Git.
{:shortdesc}

1. Pour commencer, dans la vue d'ensemble de l'application, cliquez sur **Ajouter le référentiel et le pipeline Git**, ou dans la version classique de {{site.data.keyword.Bluemix_notm}}, cliquez sur **AJOUTER UN REFERENTIEL GIT**.
2. Dans la fenêtre qui s'ouvre, vérifiez que la case **Remplir le référentiel avec le package d'applications du module de démarrage et activer le pipeline Build & Deploy** est cochée. Le référentiel Git est créé. Si le code de démarrage est disponible, il est chargé dans le référentiel. De plus, l'application est déployée par le service Delivery Pipeline qui s'exécute dans {{site.data.keyword.jazzhub}}.
3. Pour mettre à jour votre application, vous pouvez utiliser la ligne de commande ou l'environnement de développement intégré Web.
   **Si vous utilisez la ligne de commande :**
   a. Clonez votre référentiel Git à partir de l'adresse URL Git figurant dans la vue d'ensemble de l'application.
   b. Dans l'éditeur de votre choix, mettez à jour le code.
   c. Depuis l'interface de ligne de commande Git, envoyez vos modifications par commande push.

   **Si vous utilisez l'environnement de développement intégré Web :**
   a. Dans la vue d'ensemble de l'application, cliquez sur **Editer le code**. Votre projet s'ouvre dans l'environnement de développement intégré Web.
   b. Apportez les modifications requises, puis envoyez-les par commande push à l'aide du support Git intégré.

L'application mise à jour est redéployée dans {{site.data.keyword.Bluemix_notm}}.

Pour des instructions détaillées, voir [Set up Git integration and auto-deploy in DevOps Services ![icône de lien externe](../icons/launch-glyph.svg)](https://hub.jazz.net/tutorials/jazzeditor/#git_integration_and_autodeployment){: new_window}.

## Vous avez ajouté un référentiel Git ? Essayez {{site.data.keyword.Bluemix_notm}} Live Sync.

Si vous construisez une application Node.js, vous pouvez utiliser {{site.data.keyword.Bluemix_notm}} Live Sync pour mettre à jour rapidement l'instance d'application dans {{site.data.keyword.Bluemix_notm}} et procéder au développement comme sur le bureau.

Pour en savoir plus sur {{site.data.keyword.Bluemix_notm}} Live Sync, voir [{{site.data.keyword.Bluemix_notm}} Live Sync](/docs/develop/bluemixlive.html). Pour plus de détails sur les commandes, voir la [documentation sur l'interface de ligne de commande {{site.data.keyword.Bluemix_notm}} Live Sync](/docs/cli/reference/bl/index.html). Pour utiliser {{site.data.keyword.Bluemix_notm}} Live Sync avec l'environnement de développement intégré Web, voir [Live Edit](/docs/develop/bluemixlive.html).

Avant de commencer, téléchargez et installez la ligne de commande bl de {{site.data.keyword.Bluemix_notm}} Live Sync.

**Important :** l'outil de ligne de commande bl est disponible uniquement pour Windows 7 et 8 et Mac OS X version 10.9 ou ultérieure.

<p>
<a class="xref" href="http://livesyncdownload.ng.bluemix.net/downloads/blive_setup.msi" target="_blank" title="(Ouverture dans un nouvel onglet ou une nouvelle fenêtre)"><img class="image" src="images/bl_gs_icons_windows_b.svg" alt="Bouton de téléchargement de la ligne de commande bl Windows" /> </a> <a class="xref" href="http://livesyncdownload.ng.bluemix.net/downloads/BluemixLive.pkg" target="_blank" title="(Ouverture dans un nouvel onglet ou une nouvelle fenêtre)"><img class="image" src="images/bl_gs_icons_mac-osx_b.svg" alt="Bouton de téléchargement de la ligne de commande bl Mac" /> </a>
</p>

1. Sur une ligne de commande, connectez-vous en tapant la commande suivante :
```
bl login
```
Lorsque vous y êtes invité, entrez votre {{site.data.keyword.ibmid}} et votre mot de passe.

2. Affichez la liste des projets disponibles pour la synchronisation {{site.data.keyword.Bluemix_notm}} Live Sync en entrant la commande suivante :
```
bl projects
```
Recherchez le nom de projet dans la liste qui correspond à votre application. Le nom de projet suit le format de votre *alias* | *nom d'application*.

3. Synchronisez votre environnement local avec votre projet dans {{site.data.keyword.Bluemix_notm}} à l'aide de la commande ci-après. Si vous êtes le propriétaire du projet, il suffit de spécifier nom-de-votre-application pour nom_projet.
<!--- this command needs italicized parameters projectName localDirectory and yellow on 'local' -->
```
bl sync nom_projet -d répertoire_local --verbose
```
Cette commande continue de s'exécuter (et la synchronisation continue) jusqu'à ce que vous entriez la lettre "q". L'option --verbose affiche les informations de journalisation et de statut. Si l'un de vos arguments contient un espace, placez-le entre apostrophes.

4. Dans une autre fenêtre de ligne de commande, dans votre répertoire local, déployez l'application dans {{site.data.keyword.Bluemix_notm}} en mode édition directe avec la commande suivante :
```
bl start
```

Lorsque vous modifiez les fichiers dans votre répertoire local, les modifications sont propagées automatiquement dans l'application exécutée dans {{site.data.keyword.Bluemix_notm}} et dans l'espace de travail de cloud de projet. Si vous devez redémarrer l'application de noeud, vous pouvez utiliser la commande suivante :
```
bl start --restart
```
