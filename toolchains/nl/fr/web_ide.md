---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Edition de code avec Eclipse Orion {{site.data.keyword.webide}}
{: #web_ide}

Dernière mise à jour : 9 septembre 2016
{: .last-updated}

Eclipse Orion {{site.data.keyword.webide}} est un environnement de développement basé navigateur dans lequel vous pouvez faire du développement pour le Web. Vous pouvez développer en JavaScript, HTML et CSS en vous aidant de l'assistant de contenu, de la validation de code et du contrôle des erreurs. {{site.data.keyword.webide}} fonctionne avec quasiment toutes les langues et offre une mise en évidence de syntaxe pour la plupart des [types de fichier (Lien s'ouvrant dans une nouvelle fenêtre)](https://hub.jazz.net/docs/overview/#dev_support){: new_window}. Le contrôle des sources est généré via Git ou Jazz SCM, et vous pouvez déployer le code en local afin de tester et déboguer vos applications.
{:shortdesc}

Mais surtout, {{site.data.keyword.webide}} est basé sur le Web. Vous n'avez rien à installer, rien à gérer, et rien à mettre à l'échelle. Vous pouvez faire du développement depuis n'importe quel endroit, dans la mesure où vous disposez d'une connexion Internet.

## Configuration de l'éditeur
{: #editorsetup}

{{site.data.keyword.webide}} est personnalisable : vous pouvez choisir les schémas de couleurs, les outils techniques et les paramètres correspondant à vos besoins de développement. Pour afficher et modifier les paramètres, depuis le menu de gauche, cliquez sur l'icône **Paramètres** <img class="inline" src="./images/webide_settings_icon.png"  alt="Icône des paramètres">.

Si vous avez fréquemment besoin de changer certains paramètres lors de l'édition, vous pouvez accéder à ces paramètres rapidement via l'icône **Paramètres de l'éditeur local** <img class="inline" src="./images/webide_local_settings_icon.png"  alt="Icône Paramètres de l'éditeur local"> située dans le coin supérieur droit de l'éditeur.

![Paramètres de l'éditeur local](images/webide_local_editor_settings.png)

Par défaut, les paramètres de style et de taille de police de l'éditeur sont toujours affichés. Pour inclure d'autres paramètres de l'éditeur dans le menu, procédez comme suit :

1. Cliquez sur l'icône **Paramètres de l'éditeur local** <img class="inline" src="./images/webide_local_settings_icon.png"  alt="Icône Paramètres de l'éditeur local">.

2. Cliquez sur **Paramètres de l'éditeur**.

3. Pour inclure ou exclure un paramètre du menu **Paramètres de l'éditeur local**, cliquez sur la pastille en regard du paramètre.

![Activation/désactivation des Paramètres de l'éditeur](images/webide_editor_settings_toggle.png)


## Edition de code
{: #editcode}

{{site.data.keyword.webide}} comporte deux sections principales. La première section correspond au navigateur de fichiers, situé à gauche, qui affiche vos fichiers de projet dans une structure arborescente. Depuis le navigateur de fichiers, vous pouvez créer, renommer, supprimer et gérer vos fichiers et dossiers.

**Conseil :** Pour télécharger des fichiers dans le navigateur de fichiers, faites-les glisser depuis votre ordinateur vers le navigateur.

La seconde section correspond à la sous-fenêtre de l'éditeur, située sur la droite. L'éditeur fournit plusieurs fonctions de codage, notamment l'assistant de contenu et la validation de la syntaxe.

![Web IDE](images/webide.png)

### Utilisation de plusieurs fichiers
1. Pour utiliser deux fichiers en même temps, cliquez sur l'icône **Changer le mode de fractionnement de l'éditeur** <img class="inline" src="./images/webide_split_editor_icon.png"  alt="Icône Fractionner l'éditeur"> situé en haut de l'éditeur.
2. Dans le menu qui s'ouvre, sélectionnez une vue.

 Une fois que vous avez sélectionné une vue, si un fichier était déjà ouvert dans l'éditeur, il s'affiche dans les deux vues.

 Pour ouvrir ou changer un fichier affiché dans l'une des vues de l'éditeur :
 1. Placez le curseur sur la vue que vous souhaitez changer.
 2. Dans le navigateur de fichiers, cliquez sur un fichier.

### Raccourcis-clavier
La plupart des commandes de {{site.data.keyword.webide}} sont accessibles uniquement via des raccourcis-clavier.

Pour afficher la liste des raccourcis-clavier dans l'éditeur, appuyez sur Alt+Maj+?. Si vous utilisez un système Mac OS, appuyez sur Ctrl+Maj+?.

## Gestion du code source
{: #sourcecontrol}

{{site.data.keyword.webide}} est intégré aux outils de gestion du code source. Pour utiliser votre référentiel Git, cliquez sur l'icône **Référentiel Git** <img class="inline" src="./images/webide_git_icon.png"  alt="Icône Référentiel Git">. Pour plus d'informations, voir [Source control with Git (Lien s'ouvrant dans une nouvelle fenêtre)](https://hub.jazz.net/docs/git/){: new_window}.


## Déploiement d'une application depuis votre espace de travail
{: #deploy}

1. Pour déployer votre application, depuis la barre d'exécution, sélectionnez ou [créez (Lien s'ouvrant dans une nouvelle fenêtre)](https://hub.jazz.net/tutorials/livesync/#launch_configuration){: new_window} une configuration de lancement.
1. Cliquez sur l'icône de déploiement <img class="inline" src="./images/webide_deploy_button.png"  alt="Icône de déploiement">. Une instance de votre application est déployée à l'aide du contenu actuel de votre espace de travail et de l'environnement défini dans votre configuration de lancement. 
2. Une fois voter application déployée, vous pouvez utiliser la barre d'exécution pour arrêter, redémarrer ou déboguer votre application, consulter des journaux, etc.
![ Barre d'exécution](images/webide_runbar.png)

<!-- LH: I'm commenting out the following list because I think this information is obvious from the UI. I also updated the preceding sentence to mention a few things that you can do from the run bar.

 * Stop the app: <img  class="inline" src="./images/webide_stop_button.png"  alt="The stop icon">
 * Open the deployed app: <img class="inline" src="./images/webide_open_app_url.png"  alt="The open app URL icon">
 * View the logs of the deployed app: <img class="inline" src="./images/webide_view_logs.png"  alt="The view logs icon">
 * Open the app's Dashboard: <img  class="inline" src="./images/webide_open_dashboard.png"  alt="The open dashboard icon">
 * If you are developing a Node.js app, enable Live Edit mode: <img  class="inline"  src="./images/webide_enable_live_edit.png"  alt="The enable live edit slider">
 * With Live Edit mode enabled, restart the app quickly, without redeployment: <img  class="inline" src="./images/webide_live_edit_restart.png"  alt="The Live Edit restart icon">
 * With Live Edit mode enabled, access the debugger: <img  class="inline" src="./images/webide_debug_icon.png"  alt="The debug icon"> -->

 ## Edition hors de {{site.data.keyword.webide}}
{: #editlocal}

Pour utiliser un éditeur en dehors de {{site.data.keyword.webide}}, configurez {{site.data.keyword.Bluemix_live}} de façon à utiliser directement vos fichiers de projet dans l'outil de votre choix. {{site.data.keyword.Bluemix_live_notm}} est une application de ligne de commande qui synchronise les changements sur votre système de fichiers local avec votre espace de travail cloud dans {{site.data.keyword.jazzhub}}. 

### En premier lieu 

Téléchargez et installez l'[interface de ligne de commande {{site.data.keyword.Bluemix_live_notm}} (Lien s'ouvrant dans une nouvelle fenêtre)](http://livesyncdownload.ng.bluemix.net){: new_window}.

### Synchronisation de votre environnement local avec {{site.data.keyword.Bluemix_notm}}
{: #edit_local_download}

1. Ouvrez une fenêtre de ligne de commande.
2. Connectez-vous à {{site.data.keyword.Bluemix_notm}}:

	```
	bl login
	```
	{: pre}

3. Lorsque vous y êtes invité, entrez vos IBMid et mot de passe.
4. Affichez la liste de vos projets {{site.data.keyword.Bluemix_notm}} : 

	```
	bl projects
	```
	{: pre}

4. Synchronisez votre environnement local avec votre projet sur {{site.data.keyword.Bluemix_notm}} :

	```
	bl sync projectName
	```
	{: pre}

où `projectName` correspond au nom de votre application {{site.data.keyword.Bluemix_notm}}.

Une fois l'édition terminée, entrez `q` pour mettre fin à la synchronisation.

### Activation de la fonction Desktop Sync pour éditer du code en local

La fonction Desktop Sync est similaire au mode d'édition directe (Live Edit) de la ligne de commande. Vous avez besoin de la fonction Desktop Sync pour le débogage sur la ligne de commande.
1. Dans une autre fenêtre de ligne de commande, activez la fonction Desktop Sync :

	```
	cd localDirectory
	bl start
	```
	{: codeblock}

2. Utilisez la configuration de lancement créée dans {{site.data.keyword.webide}}. Une fois la configuration de lancement sélectionnée, la fonction Desktop Sync est activée dans votre environnement local. Dans la fenêtre de ligne de commande que vous venez d'ouvrir, vous pouvez voir l'URL de l'application, l'URL de débogage, l'URL de gestion, ainsi que l'état de {{site.data.keyword.Bluemix_live_notm}}.

3. Actualisez le navigateur et vérifiez que vous pouvez voir les modifications sauvegardées dans des fichiers statiques de l'espace de travail local. 

### Désactivation de la fonction Desktop Sync

1. Dans la deuxième fenêtre de ligne de commande, entrez `bl stop`.
2. Dans la première fenêtre de ligne de commande, entrez `q`.
