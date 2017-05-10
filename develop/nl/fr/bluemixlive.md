---



copyright:
  years: 2015，2017
lastupdated: "2017-4-7"

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}

#{{site.data.keyword.Bluemix_notm}} Live Sync
{: #live-sync}

 
Si vous construisez une application Node.js, vous pouvez utiliser {{site.data.keyword.Bluemix}} Live Sync pour mettre rapidement à jour l'instance d'application dans {{site.data.keyword.Bluemix_notm}} et procéder au développement sans avoir à effectuer un redéploiement manuel.   
{: shortdesc}

Lorsque vous apportez une modification, vous pouvez immédiatement voir cette modification dans votre application {{site.data.keyword.Bluemix_notm}} en cours d'exécution. {{site.data.keyword.Bluemix_notm}} Live Sync fonctionne 
<!--from both the command line and -->
dans l'interface IDE Web Eclipse Orion. Vous pouvez déboguer des applications écrites en Node.js avec {{site.data.keyword.Bluemix_notm}} Live Sync.  

{{site.data.keyword.Bluemix_notm}} Live Sync se compose de deux fonctions.
<!--three -->

<!--
**Desktop Sync**  

You can synchronize any desktop directory tree with a cloud-based project workspace similar to the way Dropbox works. The Web IDE directly edits the same cloud-based workspace, so both stay in sync. Desktop Sync works for any kind of application. To use Desktop Sync, you need to download and install the BL command line interface.  
-->

**Live Edit**

Vous pouvez modifier une application Node.js qui s'exécute dans {{site.data.keyword.Bluemix_notm}} et tester immédiatement les modifications dans votre navigateur. Les modifications que vous apportez dans l'interface IDE Web sont immédiatement propagées dans le système de fichiers de l'application.  

**Debug**  

Lorsqu'une application Node.js est en mode édition directe, vous pouvez ouvrir un shell et la déboguer. Vous pouvez éditer le code dynamiquement, insérer des points d'arrêt, parcourir le code, redémarrer le contexte d'exécution, et effectuer d'autres opérations à l'aide du débogueur Node Inspector.  

<!-- You can use Desktop Sync to keep your desktop workspace in sync with the cloud-based project workspace that you edit directly with the Web IDE. -->

Vous pouvez utiliser Live Edit pour propager les modifications apportées dans votre espace de travail de projet reposant sur le cloud de votre application en cours d'exécution. 
<!-- You can use one or both of these features. And if you use Desktop Sync or -->
Si vous utilisez Live Edit pour placer votre application en mode édition directe, vous pouvez déboguer l'application en cours d'exécution.


Le processus Bluemix Live Sync est illustré dans le diagramme ci-dessous.    

Figure 1. Le processus Bluemix Live Sync
    

![Image du processus Bluemix Live Sync](images/bluemix-live-sync.png)

Si vous développez une application Java qui s'exécute dans Liberty, vous pouvez procéder au débogage à distance avec [Eclipse Tools for Bluemix](/docs/manageapps/eclipsetools/eclipsetools.html#eclipsetools).

<!--
##Desktop Sync {: #desktop-sync}

You can use the Desktop Sync feature of Bluemix Live Sync to quickly update the application instance on {{site.data.keyword.Bluemix_notm}} and develop as you would on your desktop.

Desktop Sync has the following considerations:
* Desktop Sync runs on these operating systems:
  * Windows 7 or 8
  * Mac OS X version 10.9 or later   
      **Note:** Windows requires .NET Framework version 4.5. If you do not have .NET installed, you are prompted to install it when you install the {{site.data.keyword.Bluemix_notm}} Live Sync command line interface (CLI).  
* You do not need to clone your Git repository.
* No matter what type of application you are developing, you can synchronize your desktop project with the cloud workspace.
* If your application is written in Node.js, you can propagate changes to running applications.

For more details on the commands, see [Bluemix Live Sync (bl) commands](bluemixlive.html#bl-commands).

<ol>
<li>Sign up for a free <a class="xref" href="https://hub.jazz.net/" target="_blank" title="(Opens in a new tab or window)">Bluemix DevOps Services account<img class="image" src="../icons/launch-glyph.svg" alt="External link icon"/></a>.</li>
<li>Download and install the {{site.data.keyword.Bluemix_notm}} Live Sync bl command line.   
<p>
<a class="xref" href="http://livesyncdownload.ng.bluemix.net/downloads/blive_setup.msi" target="_blank" title="(Opens in a new tab or window)"><img class="image" src="images/bl_gs_icons_windows_b.svg" alt="Download the Windows bl command line button" /> </a>
<a class="xref" href="http://livesyncdownload.ng.bluemix.net/downloads/BluemixLive.pkg" target="_blank" title="(Opens in a new tab or window)"><img class="image" src="images/bl_gs_icons_mac-osx_b.svg" alt="Download the Mac bl command line button" /> </a>
</p>  

<strong>Important:</strong> The bl command line tool is available only for Windows 7 and 8 and Mac OS X version 10.9 or later. </li>

<li>On a command line, log in using the following command. You will be prompted for your user ID and password.  
<pre class="codeblock">bl login</pre>

<strong>Note:</strong> Your user ID for DevOps Services can be either an IBMid or a federated ID (corporate ID). If you use federated authentication, to log in to your Bluemix Live Sync command-line client, you must use a personal access token instead of a password. If you don't use federated authentication, your IBMid and password work with all clients. For more information about creating a personal access token, see <a class="xref" href="https://developer.ibm.com/devops-services/2016/06/23/whats-federated-authentication-and-how-does-it-affect-me/" target="_blank" title="(Opens in a new tab or window)">What's federated authentication and how does it affect me?<img class="image" src="../icons/launch-glyph.svg" alt="External link icon"/></a>.
</li>

<li>See the list of projects that are available for {{site.data.keyword.Bluemix_notm}} Live Sync synchronization by entering the following command:
<pre class="codeblock">bl projects</pre>
<p>Find the project name in the list that matches your application. The project name has the format of your <i>alias</i> | <i>your application name</i>. </p>
</li>
<li>Synchronize your local environment with your project on {{site.data.keyword.Bluemix_notm}} by entering the following command. If you are the owner of the project, you only need to specify your-application-name for projectName.
<pre class="codeblock">bl sync projectName -d localDirectory &ndash&ndashverbose</pre>
<p>This command continues to run (and synchronization continues) until you enter a "q". The &ndash&ndashverbose option displays the logging and status information. If any of your arguments contain a space, you need to enclose the name in quotes. </p></li>
<li>In another command line window, in your local directory, deploy the application to {{site.data.keyword.Bluemix_notm}} in Live Edit mode by entering the following command:
<pre class="codeblock">bl start</pre>
</li>
</ol>

When you change the files in your local directory, the changes are automatically propagated to both the application that is running on {{site.data.keyword.Bluemix_notm}} and the project cloud workspace. If you need to restart the Node application, then you can use the following command:
```
bl start &ndash&ndashrestart
```
-->

##Live Edit {: #live-edit}

Si vous construisez une application Node.js, lorsque vous apportez des modifications à votre projet dans l'environnement de développement intégré Web, la fonction Live Edit de {{site.data.keyword.Bluemix_notm}} Live Sync peut mettre à jour rapidement l'instance d'application qui s'exécute dans {{site.data.keyword.Bluemix_notm}}. Live Edit vous permet de procéder au développement comme sur le bureau, sans redéploiement.

La fonction Live Edit est prise en charge uniquement pour les applications Node.js.

Dans l'interface IDE Web Eclipse Orion, dans la barre d'exécution, cliquez sur **Live Edit**.

![Image de la barre d'exécution avec Live Edit](images/bluemix-live-sync-light.png)

Live Edit permet de prévisualiser rapidement les modifications apportées aux applications Node.js qui s'exécutent dans {{site.data.keyword.Bluemix_notm}}. Lorsque vous mettez à jour votre code alors que la fonction Live Edit est activée, vous pouvez actualiser la fenêtre de navigateur de votre application Web pour afficher ces modifications quelques secondes après les avoir effectuées.

<!--
For a tutorial on using the Live Edit feature of {{site.data.keyword.Bluemix_notm}} Live Sync, see the tutorial [Test and debug a Node.js app with Bluemix Live Sync![External link icon](../icons/launch-glyph.svg "External link icon")](https://hub.jazz.net/tutorials/livesync){:new_window}.
-->

Lorsque vous modifiez les fichiers dans votre environnement de développement intégré Web, ceux-ci sont redéployés automatiquement dans votre application qui s'exécute dans {{site.data.keyword.Bluemix_notm}}. Si vous devez redémarrer l'application de noeud, vous pouvez utiliser le bouton **Redémarrer** dans la barre d'exécution.

**REMARQUE :** pour une expérience plus cohérente lors de l'utilisation de la fonction Live Edit de {{site.data.keyword.Bluemix_notm}} Live Sync, 256 Mo de mémoire supplémentaire sont requis et seront ajoutés.

##{{site.data.keyword.Bluemix_notm}} Live Debug {: #live-debug}

Vous pouvez accéder à la fonction Debug de {{site.data.keyword.Bluemix_notm}} Live Sync lorsque {{site.data.keyword.Bluemix_notm}} Live Sync est activé pour votre application Node.js.

La fonction debug permet d'éditer le code, d'insérer des points d'arrêt, de parcourir le code, de redémarrer le contexte d'exécution et d'effectuer d'autres opérations de manière dynamique, pendant que votre application est exécutée par {{site.data.keyword.Bluemix_notm}}. Vous pouvez développer votre application de façon incrémentielle avec agilité en effectuant votre choix dans une longue liste de services {{site.data.keyword.Bluemix_notm}}.

{{site.data.keyword.Bluemix_notm}} Live Debug inclut les fonctions suivantes :

* Le contrôle du contexte d'exécution d'application
* Le débogage à l'aide de [node-inspector![](../icons/launch-glyph.svg "")](https://github.com/node-inspector/node-inspector){:new_window}
* L'accès au shell

###Contrôle du contexte d'exécution d'application {: #app-runtime}

Avec le contrôle du contexte d'exécution d'application, vous pouvez utiliser la fonction Debug afin d'inspecter l'état de l'application au démarrage. Cette capacité est utile lorsque vous traitez les incidents liés à une application qui tombe en panne au démarrage.

Lorsque vous développez votre application, vous pouvez choisir une action parmi les suivantes :

* Procéder à un redémarrage rapide de l'application
* Suspendre l'application avant l'exécution du code de l'application

###Debug {: #debug}

La fonction Debug inclut les capacités suivantes :

**Restriction :** Google Chrome est requis.

* Définir des points d'arrêt dans le code de l'application pour interrompre l'exécution à une ligne spécifique.
* Editer les conditions de point d'arrêt pour interrompre l'exécution uniquement lorsque certains critères sont remplis.
* Inspecter l'état des zones et des variables locales.
* Afficher immédiatement la sortie de débogage des appels de `console.log()`. Cette action est plus rapide que la surveillance des journaux cf.
* Utiliser l'éditeur de code source intégré pour apporter des modifications immédiates mais temporaires au code d'application en cours d'exécution.

###Shell {: #shell}

Cet outil permet d'accéder au conteneur dans lequel votre application est en cours d'exécution via un shell. Avec ce terminal, vous pouvez exécuter des commandes shell de diagnostic à distance afin d'administrer votre application.

Surveillez l'utilisation de la mémoire et de l'unité centrale dans l'instance qui utilise des commandes Linux standard, comme **top**, **ps** et **kill**.

###Configuration d'une application pour activer {{site.data.keyword.Bluemix_notm}} Live Debug {: #configure_app_debug}

L'application doit utiliser le pack de construction IBM SDK for Node.js. Les packs de construction personnalisés ne sont pas pris en charge.

1. Autorisez le pack de construction à détecter la commande de démarrage de l'application. La commande start doit être détectée automatiquement par le pack de construction et ne doit pas être définie dans le fichier `manifest.yml`.  

    a. Vérifiez que le fichier `package.json` contient un script de démarrage, qui inclut une commande start pour l'application.  
    b. Si le fichier `manifest.yml` de l'application contient une commande, définissez la valeur null.  

2. Définissez la variable d'environnement.  

    a. Dans le fichier `manifest.yml`, ajoutez la variable suivante :
	```
	env:
      ENABLE_BLUEMIX_DEV_MODE: "true"
	```

3. Augmentez la mémoire.  

    a. Dans le fichier `manifest.yml` de l'application, ajoutez 128M ou plus à la valeur spécifiée pour l'attribut de mémoire :

Une fois {{site.data.keyword.Bluemix_notm}} Live Debug installé, vous pouvez utiliser les outils de débogage.

Déployez l'application, puis ouvrez `https://app-host.mybluemix.net/bluemix-debug/manage` pour accéder à l'interface utilisateur de débogage {{site.data.keyword.Bluemix_notm}}. Lorsque vous êtes invité à vous authentifier, entrez votre ID utilisateur et votre jeton d'accès personnel ou votre mot de passe IBMid.    

<!--
   **Note**: Your user ID for DevOps Services can be either an IBMid or a federated ID (corporate ID). If you use federated authentication, to log in to your Bluemix Live Sync command-line client, you must use a personal access token instead of a password. If you don't use federated authentication, your IBMid and password work with all clients. For more information about creating a personal access token, see [What's federated authentication and how does it affect me?![External link icon](../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/devops-services/2016/06/23/whats-federated-authentication-and-how-does-it-affect-me/){:new_window}
   -->

###Restauration des configurations d'application et désactivation de Bluemix Live Debug {: #restore_live_debug}

1. Supprimez la variable d'environnement ENABLE_BLUEMIX_DEV_MODE du fichier `manifest.yml` de l'application.

2. Restaurez la commande de démarrage et la valeur de mémoire d'origine de l'application.

3. Déployez l'application.

<!--
## {{site.data.keyword.Bluemix_notm}} Live Sync (bl) commands  {: #bl-commands}

If you are building a Node.js application, you can use {{site.data.keyword.Bluemix_live}} to quickly update the application instance running on {{site.data.keyword.Bluemix_notm}} and develop as you would on the desktop without redeploying. When you make a change, you can see that change in your running {{site.data.keyword.Bluemix_notm}} application immediately. The {{site.data.keyword.Bluemix_live}} command line interface is called *bl*.
{:shortdesc}

You can use **bl** command line interface commands to complete the following tasks:

* Start and stop an application that is running on {{site.data.keyword.Bluemix_notm}}.
* Create a new cloud-based project from your desktop.
* Sync changes from your desktop to the cloud-based project workspace and to the application running on {{site.data.keyword.Bluemix_notm}}.
* See the list of projects available for synchronization.
* See the status of running applications.

For more information on downloading and using the bl command, see [Bluemix Live Sync](/docs/develop/bluemixlive.html).

## bl commands
{: #bl_commands}

The {{site.data.keyword.Bluemix_live}} command line, **bl**, has the following syntax:

```
bl command [arguments] [options] [&ndash&ndashhelp]
```
{: pre}

**Commands**

l *login*: Log in to {{site.data.keyword.Bluemix_notm}}.

lo *logout*: Log out of {{site.data.keyword.Bluemix_notm}}.

s *sync*: Start the synchronization process between the desktop and the server.

c *create*: Create a private project, link it to the Git repo in this directory, and deploy the contents to {{site.data.keyword.Bluemix_notm}}.

p *projects*: List all the projects that are available for synchronizing.

st *start*: Start the application instance in {{site.data.keyword.Bluemix_notm}}.

sp *stop*: Stop the application instance in {{site.data.keyword.Bluemix_notm}}.

ss *status*: List the status of the running application instance in {{site.data.keyword.Bluemix_notm}}.


**Arguments**

Arguments for the command.


**Options**

Options for the command.

**Global Options**

*&ndash&ndashhelp*: Display the help page for the specified command

*&ndash&ndashverbose*: Enable verbose logging.

**Note:** If any of your arguments or options contain a space, enclose the value in double quotation marks.

## Help
{: bl_help}

```
bl [ command ] &ndash&ndashhelp | &ndash&ndashh
```
{: pre}

**Usage**

Use this command to display help about a command or the command list.

**Examples**

Display the list of commands:

```
bl &ndash&ndashhelp
```
{: pre}

Display detailed information about the sync command:

```
bl sync &ndash&ndashhelp
```
{: pre}

## Login
{: bl_login}

```
bl login | l [ -u username ] [-p password ][ -s server ]
```
{: pre}

**Purpose**

Use this command to log in to {{site.data.keyword.Bluemix_notm}}. The log in needs to be done only one time per session.

**Warning:** Providing your password as a command line option is discouraged as it is visible to others and recorded as a part of your command history.

**Note:** You must sign up for a free [Bluemix DevOps Services![External link icon](../icons/launch-glyph.svg "External link icon")](https://hub.jazz.net/){:new_window} account before logging in.

**Options**

-u *username*: Your user ID to log in to {{site.data.keyword.Bluemix_notm}}.

-p *password*: Your personal access token or IBMid password.

-s *server*: The server name or IP address of the {{site.data.keyword.jazzhub_short}} server.    

   **Note**: Your user ID for DevOps Services can be either an IBMid or a federated ID (corporate ID). If you use federated authentication, to log in to your Bluemix Live Sync command-line client, you must use a personal access token instead of a password. If you don't use federated authentication, your IBMid and password work with all clients. For more information about creating a personal access token, see [What's federated authentication and how does it affect me?![External link icon](../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/devops-services/2016/06/23/whats-federated-authentication-and-how-does-it-affect-me/){:new_window}

**Examples**

This command prompts for both a *username* and a *password*:

```
bl login
```
{: pre}

Log in the user, `name@company.com`:

```
bl login –u name@company.com –p pa55w0rd
```
{: pre}

Log in the user, `name@company.com` with the password of *pa55 w0rd* that contains a space so it needs quotes:

```
bl login –u name@company.com –p “pa55 w0rd”
```
{: pre}

## Logout
{: bl_logout}

```
bl logout | lo
```
{: pre}

**Purpose**

Use this command to log out.

## Projects
{: bl_projects}

```
bl projects | p
```
{: pre}

**Purpose**

Use this command to list all the projects that are available for synchronization by the logged in user.

## Sync
{: bl_sync}

```
bl sync | s projectName -d localDirectory [ &ndash&ndashoverwritelocal ] [ &ndash&ndashoverwriteremote ] [ &ndash&ndashverbose ]
```
{: pre}

**Purpose**

Use this command to start the synchronization of the contents of a project with your local directory. This command runs until a <code>q</code> is entered. This command can optionally show a log of all file and application state changes.

**Argument**

*projectName*: The project name in the form *“alias | mproject”* or just *myproject* if the project is owned by the logged in user.

**Options**

-d *localDirectory*: Local directory path. Defaults to the current folder ".".

*&ndash&ndashoverwritelocal*: Overwrite the local directory with contents of the project workspace.

*&ndash&ndashoverwriteremote*: Overwrite the project workspace with the contents of the local directory.

*&ndash&ndashverbose*: Display verbose logging.

**Examples**

This command begins synchronization with the associated project if the current directory is an existing sync target. If the current directory is empty and is not an existing sync target, the command prompts for a *projectName*. If the current directory is not empty and not an existing sync target, an overwrite option is required.

```
bl sync
```
{: pre}

This command begins synchronization and is equivalent to `bl sync “alias | myproject”` if the project is owned by the logged in user.

```
bl sync  myproject
```
{: pre}

This command begins synchronization with the project `my pro ject` whose name contains spaces so it is enclosed in quotes:

```
bl sync “my pro ject”
```
{: pre}

This command begins synchronization of the project `myproject` with the directory `myfolder`:

```
bl sync myproject –d  myfolder
```
{: pre}

## Create
{: bl_create}

```
bl create | c [ -n PROJECT_NAME ] [ -r REGION ] [ -o ORG ] [ -s SPACE ] [ -g GIT_REPO ] [-e GIT_EXE ] [ &ndash&ndashcreds ] [ &ndash&ndashfork ] [ &ndash&ndashpublic ] [ &ndash&ndashprompt ]
```
{: pre}

**Purpose**

Use this command from a directory that contains code to create a private project, link it to a Git repo, and deploy the contents of the repo to {{site.data.keyword.Bluemix_notm}}.

**Options**

-n *PROJECT_NAME*: A name for your project. Default: current dir name.

-r *REGION*: A {{site.data.keyword.Bluemix_notm}} region. Default: US South.

-o *ORG*: A {{site.data.keyword.Bluemix_notm}} org. Default: First org found.

-s *SPACE*: A {{site.data.keyword.Bluemix_notm}} space. Default: First space found.

-g *GIT_REPO*: Name of the remote repo to use for any existing Git repos. Default: origin.

-e *GIT_EXE*: Full path to a Git executable. Default: detected.

*&ndash&ndashcreds*: Prompt for your Git credentials.

*&ndash&ndashfork*: Fork this directory and create a project and repo.

*&ndash&ndashpublic*: Make the new project public.

*&ndash&ndashprompt*: Prompt for all required options with available choices.

**Examples**

This command begins the process to create a private project and prompts for a project name to use.

```
bl create
```
{: pre}

This command creates a public project that is named `myNewProject`.

```
bl create -n myNewProject &ndash&ndashpublic
```
{: pre}

## Status
{: bl_status}

```
bl status | ss [ projectName ]
```
{: pre}

**Purpose**

Use this command to list the status of the applications that are associated with the launch configurations in the `./launchConfigurations` directory.

**Argument**

*projectName*: The project name in the form `“alias | myproject”` or just `myproject` if the project is owned by the logged in user.

**Examples**

This example displays the status of the running applications. If the current directory is an existing sync target, it uses the associated project. If the current directory is not an existing sync target, the command prompts for the `projectName`.

```
bl status
```
{: pre}

This example displays the status of the project *myproject* that is equivalent to `bl status “alias | myproject”` if the project is owned by the logged in user.

```
bl status myproject
```
{: pre}

This example displays the status of the running application that is associated with the project `my pro ject` whose name contains spaces so it is enclosed in quotes:

```
bl status “my pro ject”
```
{: pre}

## Start
{: bl_start}

```
bl start | st projectName [ -l launchConfigPath ] -m manifestPath ] [ &ndash&ndashliveedit ] [&ndash&ndashnoliveedit ] [ &ndash&ndashrestart ]
```
{: pre}

**Purpose**

Use this command to start the application instance that is described by the launch or manifest file. The application is launched in live edit mode by default if the application’s buildpack supports live edit. Once started, the URLs for the application, the debug tools, and the {{site.data.keyword.Bluemix_notm}} dashboard are displayed.

**Argument**

*projectName*: The project name in the form *“alias | myproject”* or just *myproject* if the project is owned by the logged in user.

**Options**

-l *launchConfiguration*: The launch configuration name (for example, `mylaunchconfig`), file name (for example, `mylaunchconfig.launch`, or a project-relative path to the launch configuration file (for example, `launchConfigurations/mylaunchconf.launch`).

-m *manifestPath*: The project-relative path to the manifest file (for example, `manifest.yml`).

*&ndash&ndashliveedit*: Start the associated application in live edit mode or exits with an error if the buildpack does not support live edit mode.

*&ndash&ndashnoliveedit*: Start the associated application in normal mode.

*&ndash&ndashview*: Open a browser of the running application.

*&ndash&ndashrestart*: Restart an application already running in live edit mode without redeploying it.

**Examples**

This command starts an application instance of `myproject` associated with the launch file `launchConfigurations/my.launch`.

```
bl start myproject –l “launchConfigurations/my.launch”
```
{: pre}

This command starts an application instance of the project that is associated with the current directory with the launch file `launchConfigurations/my.launch`. If the current directory is not a sync target, an error is displayed.

```
bl start –l “launchConfigurations/my.launch”
```
{: pre}

This command starts an application instance of the project that is associated with the current directory with the manifest file `manifest.yml`. The information specified in the manifest is used to create a new launch configuration file. The command prompts you for the remaining required information, and then starts the application described by the launch configuration:

```
bl start –m “mymanifest.yml”
```
{: pre}

This command starts an application instance of the project that is associated with the current directory with the manifest file `manifest.yml` and is equivalent to `bl start –m manifest.yml`.

```
bl start
```
{: pre}

## Stop
{: bl_stop}

```
bl stop | sp projectName [ -l launchConfiguration ]
```
{: pre}

**Purpose**

Use this command to stop the application instance that is associated with the launch file.

**Argument**

*projectName*: The project name in the form *“alias | mproject”* or just *mproject* if the project is owned by the logged in user.

**Options**

-l *launchConfiguration*: The launch configuration name (for example, `mylaunchconfig`), file name (for example, `mylaunchconfig.launch`, or a project-relative path to the launch configuration file (for example, `launchConfigurations/mylaunchconf.launch`).

**Examples**

This command stops the application if the current directory is a sync target; otherwise, it exits with an error. If there are no launch configurations, then this command exits with an error. If there are more than one launch configurations, then the command prompts you for the one to stop.

```
bl stop
```
{: pre}

This command stops an application instance of the project that is running with the launch file `mylaunchConfig`.

```
bl stop myproject –l “mylaunchConfig”
```
{: pre}

This command stops the application if the current directory is a sync target of the associated project that was started with the launch file `launchConfigurations/mylaunchconfig.launch`; otherwise, it exits with an error:

```
bl stop –l “launchConfigurations/mylaunchconfig.launch”
```
{: pre}
-->

# Liens connexes
{: #rellinks}

<!--
## Tutorials and Samples
{: #samples}

* [Test and debug a Node.js app with Bluemix Live Sync![External link icon](../icons/launch-glyph.svg "External link icon")](https://hub.jazz.net/tutorials/livesync){:new_window}
-->


## Liens connexes
{: #general}

* [Eclipse tools for Bluemix![](../icons/launch-glyph.svg "")](https://www.ng.bluemix.net/docs/manageapps/eclipsetools/eclipsetools.html){:new_window}
