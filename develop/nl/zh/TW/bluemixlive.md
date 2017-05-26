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

 
如果您要建置 Node.js 應用程式，可以使用 {{site.data.keyword.Bluemix}} Live Sync 快速更新 {{site.data.keyword.Bluemix_notm}} 上的應用程式實例，而且不需手動重新部署即可開發。   
{: shortdesc}

當您進行變更時，可以立即在執行中的 {{site.data.keyword.Bluemix_notm}} 應用程式看到該變更。{{site.data.keyword.Bluemix_notm}} Live Sync 會 
<!--from both the command line and -->
在 Eclipse Orion Web IDE (Web IDE) 中運作。您可以使用 {{site.data.keyword.Bluemix_notm}} Live Sync，針對以 Node.js 撰寫的應用程式進行除錯。  

{{site.data.keyword.Bluemix_notm}} Live Sync 包含兩個特性。
<!--three -->

<!--
**Desktop Sync**  

You can synchronize any desktop directory tree with a cloud-based project workspace similar to the way Dropbox works. The Web IDE directly edits the same cloud-based workspace, so both stay in sync. Desktop Sync works for any kind of application. To use Desktop Sync, you need to download and install the BL command line interface.  
-->

**即時編輯**

您可以對在 {{site.data.keyword.Bluemix_notm}} 中執行的 Node.js 應用程式進行變更，並立刻在瀏覽器中加以測試。您在 Web IDE 中進行的任何變更，都會立即傳播到應用程式的檔案系統。  

**除錯**  

當 Node.js 應用程式處於「即時編輯」模式時，您可以使用 Shell 方式連入並進行除錯。您可以使用 Node Inspector 除錯器，以動態編輯程式碼、插入岔斷點、逐步執行程式碼、重新啟動運行環境等等。  

<!-- You can use Desktop Sync to keep your desktop workspace in sync with the cloud-based project workspace that you edit directly with the Web IDE. -->

您可以使用「即時編輯」，將雲端型專案工作區中的變更傳播到執行中的應用程式。 
<!-- You can use one or both of these features. And if you use Desktop Sync or -->
如果您使用「即時編輯」將應用程式置於「即時編輯」模式，就可以對執行中的應用程式進行除錯。下圖說明 Bluemix Live Sync 處理程序。    

圖 1. Bluemix Live Sync 處理程序
    

![Bluemix Live Sync 處理程序的影像](images/bluemix-live-sync.png)

如果您要開發在 Liberty 上執行的 Java 應用程式，可以使用 [Eclipse Tools for Bluemix](/docs/manageapps/eclipsetools/eclipsetools.html#eclipsetools) 進行遠端除錯。

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

##即時編輯 {: #live-edit}

如果您要建置 Node.js 應用程式，則使用 Web IDE 來變更專案時，{{site.data.keyword.Bluemix_notm}} Live Sync 的「即時編輯」特性能夠快速更新在 {{site.data.keyword.Bluemix_notm}} 上執行的應用程式實例。「即時編輯」可讓您就像在桌面上開發一樣，而無需重新部署。

「即時編輯」支援僅適用於 Node.js 應用程式。

在 Eclipse Orion Web IDE (Web IDE) 的執行列中，按一下**即時編輯**。

![含有即時編輯之執行列的影像](images/bluemix-live-sync-light.png)

「即時編輯」可讓您快速預覽在 {{site.data.keyword.Bluemix_notm}} 上執行之 Node.js 應用程式的變更。當您開啟「即時編輯」來更新程式碼時，可以重新整理 Web 應用程式的瀏覽器視窗，就能看到在進行變更幾秒後所反映的變更。

<!--
For a tutorial on using the Live Edit feature of {{site.data.keyword.Bluemix_notm}} Live Sync, see the tutorial [Test and debug a Node.js app with Bluemix Live Sync![External link icon](../icons/launch-glyph.svg "External link icon")](https://hub.jazz.net/tutorials/livesync){:new_window}.
-->

當您變更 Web IDE 中的檔案時，會自動將其重新部署至在 {{site.data.keyword.Bluemix_notm}} 上執行的應用程式。如果您需要重新啟動 Node 應用程式，可以使用執行列中的**重新啟動**按鈕。

**附註：**為達到使用 {{site.data.keyword.Bluemix_notm}} Live Sync 的「即時編輯」特性時更一致的體驗，需要且將會新增 256MB 的額外記憶體。

##{{site.data.keyword.Bluemix_notm}} 即時除錯 {: #live-debug}

如果已針對 Node.js 應用程式啟用 {{site.data.keyword.Bluemix_notm}} Live Sync，則您可以存取 {{site.data.keyword.Bluemix_notm}} Live Sync 的「除錯」特性。

您可以使用除錯來動態編輯程式碼、插入岔斷點、逐步執行程式碼、重新啟動運行環境等等，這些全都可以在由 {{site.data.keyword.Bluemix_notm}} 為您的應用程式提供服務時執行。您可以靈活地以漸進方式開發應用程式，同時從龐大的 {{site.data.keyword.Bluemix_notm}} 服務清單進行選擇。

「{{site.data.keyword.Bluemix_notm}} 即時除錯」包含下列特性：

* 應用程式運行環境控制
* 使用 [node-inspector ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/node-inspector/node-inspector){:new_window} 進行除錯
* Shell 存取

###應用程式運行環境控制 {: #app-runtime}

使用應用程式運行環境控制，您可以用「除錯」來檢查應用程式在啟動時的狀態。當您對於在啟動時當機的應用程式進行疑難排解時，此功能很有用。

開發應用程式時，可以從下列動作選取：

* 執行應用程式的快速重新啟動
* 在任何應用程式程式碼執行之前先暫停應用程式

###除錯 {: #debug}

「除錯」包含下列功能：

**限制：**需要使用 Google Chrome。

* 在應用程式碼中設定岔斷點，以在特定行暫停執行。
* 編輯岔斷點條件，只在符合特定準則時暫停執行。
* 檢查區域變數及欄位的狀態。
* 立即檢視來自 `console.log()` 呼叫的除錯輸出。此動作的速度比監視 cf logs 還要快。
* 使用內建原始碼編輯器，對執行中的應用程式碼進行立即但暫時的變更。

###Shell {: #shell}

此工具可讓您對應用程式執行所在的容器進行 Shell 存取。您可以使用此終端機，在遠端執行診斷 Shell 指令來管理應用程式。

監視使用標準 Linux 指令（例如 **top**、**ps** 及 **kill**）之實例內的記憶體及 CPU 用量。

###配置應用程式，以啟用 {{site.data.keyword.Bluemix_notm}} 即時除錯 {: #configure_app_debug}

應用程式必須使用 IBM SDK for Node.js 建置套件。不支援自訂建置套件。

1. 容許建置套件偵測應用程式啟動指令。啟動指令必須由建置套件自動偵測，而不是設定在 `manifest.yml` 檔案中。  

    a. 確保 `package.json` 檔案包含一個包括應用程式啟動指令的啟動 Script。  
    b. 如果應用程式 `manifest.yml` 檔案包含指令，請將它設為 null。  

2. 設定環境變數。  

    a. 在 `manifest.yml` 檔案中，新增下列變數：
	
	```
	env:
      ENABLE_BLUEMIX_DEV_MODE: "true" 
	```

3. 增加記憶體。  

    a. 在應用程式 `manifest.yml` 檔案中，在為記憶體屬性指定的值加上 128M 以上。

安裝「{{site.data.keyword.Bluemix_notm}} 即時除錯」之後，您可以使用除錯工具。

推送應用程式，然後瀏覽至 `https://app-host.mybluemix.net/bluemix-debug/manage`，以存取 {{site.data.keyword.Bluemix_notm}} 除錯使用者介面。當系統提示您進行鑑別時，請輸入您的使用者 ID 及個人存取記號或 IBM ID 密碼。    

<!--
   **Note**: Your user ID for DevOps Services can be either an IBMid or a federated ID (corporate ID). If you use federated authentication, to log in to your Bluemix Live Sync command-line client, you must use a personal access token instead of a password. If you don't use federated authentication, your IBMid and password work with all clients. For more information about creating a personal access token, see [What's federated authentication and how does it affect me?![External link icon](../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/devops-services/2016/06/23/whats-federated-authentication-and-how-does-it-affect-me/){:new_window}
   -->

###還原應用程式配置並停用 Bluemix 即時除錯 {: #restore_live_debug}

1. 從應用程式 `manifest.yml` 檔案移除 ENABLE_BLUEMIX_DEV_MODE 環境變數。

2. 還原應用程式的原始啟動指令及記憶體值。

3. 推送應用程式。

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

# 相關鏈結
{: #rellinks}

<!--
## Tutorials and Samples
{: #samples}

* [Test and debug a Node.js app with Bluemix Live Sync![External link icon](../icons/launch-glyph.svg "External link icon")](https://hub.jazz.net/tutorials/livesync){:new_window}
-->


## 相關鏈結
{: #general}

* [Eclipse Tools for Bluemix ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ng.bluemix.net/docs/manageapps/eclipsetools/eclipsetools.html){:new_window}
