---

copyright:
  years: 2015, 2017
lastupdated: "2017-3-31"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Edition de code avec l'interface Eclipse Orion IDE
{: #web_ide}

Eclipse Orion {{site.data.keyword.webide}} est un environnement de développement basé navigateur dans lequel vous pouvez faire du développement pour le Web. Vous pouvez développer en JavaScript, HTML et CSS en vous aidant de l'assistant de contenu, de la validation de code et du contrôle des erreurs. L'interface {{site.data.keyword.webide}} fonctionne avec quasiment toutes les langues et propose la mise en évidence de syntaxe pour la plupart des types de fichier. Le contrôle des sources est intégré et vous pouvez déployer le code en local afin de tester et déboguer vos applications.
{:shortdesc}

Mais surtout, {{site.data.keyword.webide}} est basé sur le Web. Vous n'avez rien à installer, rien à gérer ni rien à mettre à l'échelle. Vous pouvez faire du développement depuis n'importe quel endroit, dans la mesure où vous disposez d'une connexion Internet.

## Configuration de l'éditeur
{: #editorsetup}

{{site.data.keyword.webide}} est personnalisable : vous pouvez choisir les schémas de couleurs, les outils techniques et les paramètres correspondant à vos besoins de développement. Pour afficher et modifier les paramètres, dans le menu de gauche, cliquez sur l'icône **Paramètres**
<img class="inline" src="images/webide_settings_icon_light_small.png"  alt="The settings icon">.

Si vous changez souvent certains paramètres au cours de l'édition, vous pouvez accéder à ces paramètres rapidement via l'icône **Paramètres de l'éditeur local** <img class="inline" src="images/webide_local_settings_icon_light_small.png"  alt="Local Editor Settings icon">. 

![Paramètres de l'éditeur local](images/webide_local_editor_settings_light.png)

Par défaut, les paramètres de style et de taille de police de l'éditeur sont toujours affichés. Pour inclure d'autres paramètres de l'éditeur dans le menu, procédez comme suit :

1. Cliquez sur l'icône **Paramètres de l'éditeur local** <img class="inline" src="images/webide_local_settings_icon_light_small.png"  alt="Local Editor Settings icon">.

2. Cliquez sur **Paramètres de l'éditeur**.

3. Pour inclure ou exclure un paramètre du menu **Paramètres de l'éditeur local**, cliquez sur l'étoile en regard de chaque paramètre.

![Activation/désactivation des Paramètres de l'éditeur](images/webide_editor_settings_toggle_light.png)


## Edition de code
{: #editcode}

{{site.data.keyword.webide}} comporte deux sections principales. La première section correspond au navigateur de fichiers, qui affiche vos fichiers de projet dans une structure arborescente. Depuis le navigateur de fichiers, vous pouvez créer, renommer, supprimer et gérer vos fichiers et dossiers.

**Conseil :** Pour télécharger des fichiers dans le navigateur de fichiers, faites-les glisser depuis votre ordinateur vers le navigateur.

La seconde section correspond à la sous-fenêtre de l'éditeur. L'éditeur fournit plusieurs fonctions de codage, notamment l'assistant de contenu et la validation de la syntaxe.

![Web IDE](images/webide_light.png)

### Utilisation de plusieurs fichiers
1. Pour utiliser deux fichiers en même temps, cliquez sur l'icône **Changer le mode de fractionnement de l'éditeur** <img class="inline" src="images/webide_split_editor_icon_light_small.png"  alt="Split Editor icon">.
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

{{site.data.keyword.webide}} est intégré aux outils de gestion du code source. Pour utiliser votre référentiel Git, cliquez sur l'icône **Référentiel Git** <img class="inline" src="images/webide_git_icon_light_small.png"  alt="The Git Repository icon">. 

 **Conseil** : Si vous utilisez l'interface {{site.data.keyword.webide}} avec des chaînes d'outils ouvertes, votre espace de travail est prérempli avec vos référentiels GitHub, {{site.data.keyword.ghe_short}} ou Git Repos and Issue Tracking. Les référentiels associés à votre chaîne d'outils en cours sont mis en évidence.


## Déploiement d'une application depuis votre espace de travail
{: #deploy}

1. Pour déployer votre application, depuis la barre d'exécution, sélectionnez ou créez une configuration de lancement.
1. Cliquez sur l'icône de déploiement <img class="inline" src="images/webide_deploy_button_light_small.png"  alt="Icône de déploiement">. Une instance de votre application est déployée à l'aide du contenu actuel de votre espace de travail et de l'environnement défini dans votre configuration de lancement. 
2. Une fois voter application déployée, vous pouvez utiliser la barre d'exécution pour arrêter, redémarrer ou déboguer votre application, consulter des journaux, etc.
![ Barre d'exécution](images/webide_runbar_light.png)    

<!-- 3/6/2016: bl commands don't work with V2/CD 
## Editing outside of the {{site.data.keyword.webide}}
{: #editlocal}

To use an editor besides the {{site.data.keyword.webide}}, set up {{site.data.keyword.Bluemix_live}} so that you can work directly with your project files in any tool. {{site.data.keyword.Bluemix_live_notm}} is a command-line application that synchronizes the changes in your local file system with your cloud workspace in {{site.data.keyword.jazzhub}}. 

### Before you begin 

Download and install the [{{site.data.keyword.Bluemix_live_notm}} command-line interface![External link icon](../../icons/launch-glyph.svg "External link icon")](http://livesyncdownload.ng.bluemix.net){: new_window}.

### Synchronizing your local environment with {{site.data.keyword.Bluemix_notm}}
{: #edit_local_download}

1. Open a command-line window.
2. Sign in to {{site.data.keyword.Bluemix_notm}}:

	```
	bl login
	```
	{: pre}

3. When you are prompted, enter your IBMid and password.
4. View a list of your {{site.data.keyword.Bluemix_notm}} projects: 

	```
	bl projects
	```
	{: pre}

4. Synchronize your local environment with your project on {{site.data.keyword.Bluemix_notm}}:

	```
	bl sync projectName
	```
	{: pre}

where `projectName` is your {{site.data.keyword.Bluemix_notm}} app's name.

When you are finished editing, enter `q` to end synchronization.

### Enabling the Desktop Sync feature to edit code locally

The Desktop Sync feature is like Live Edit mode for the command line. You need the Desktop Sync feature to debug on the command line.
1. In another command-line window, enable the Desktop Sync feature:

	```
	cd localDirectory
	bl start
	```
	{: codeblock}

2. Use the launch configuration that you created in the {{site.data.keyword.webide}}. After you select the launch configuration, the Desktop Sync feature is enabled in your local environment. In the command-line window that you just opened, you can view the app's URL, the debug URL, the manage URL, and view the {{site.data.keyword.Bluemix_live_notm}} state.

3. Refresh the browser and verify that you can see the changes that you saved to static files in the local workspace. 

### Disabling the Desktop Sync feature

1. In the second command-line window, enter `bl stop`.
2. In the first command-line window, enter `q`.

--> 
