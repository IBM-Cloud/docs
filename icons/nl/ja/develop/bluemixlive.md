---



copyright:
  years: 2015，2017
lastupdated: "2017-3-10"

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}

#{{site.data.keyword.Bluemix_notm}} Live Sync 
{: #live-sync}

 
Node.js アプリケーションを作成する場合、{{site.data.keyword.Bluemix}} Live Sync を使用すると、{{site.data.keyword.Bluemix_notm}} 上のアプリケーション・インスタンスを素早く更新して開発することができ、手動で再デプロイする必要がありません。   
{: shortdesc}

変更を行うと、実行中の {{site.data.keyword.Bluemix_notm}} アプリケーションでその変更を即時に確認できます。
{{site.data.keyword.Bluemix_notm}} Live Sync は<!--from both the command line and --> Eclipse Orion Web IDE (Web IDE) で動作します。Node.js で書かれたアプリケーションを {{site.data.keyword.Bluemix_notm}} Live Sync を使用してデバッグできます。  

{{site.data.keyword.Bluemix_notm}} Live Sync は、2 つのフィーチャーで構成されています。
<!--three -->

<!--
**Desktop Sync**  

You can synchronize any desktop directory tree with a cloud-based project workspace similar to the way Dropbox works. The Web IDE directly edits the same cloud-based workspace, so both stay in sync. Desktop Sync works for any kind of application. To use Desktop Sync, you need to download and install the BL command line interface.  
-->

**Live Edit**

{{site.data.keyword.Bluemix_notm}} で実行中の Node.js アプリケーションに変更を加え、その変更をブラウザーで直ちにテストすることができます。Web IDE 内で加えた変更はすべて、直ちに当該アプリケーションのファイル・システムに伝搬されます。  

**Debug**  

Node.js アプリケーションが Live Edit モードになっている間は、そのアプリケーションにシェルを作成してデバッグできます。Node Inspector というデバッガーを使用して、コードの動的な編集、ブレークポイントの挿入、コードのステップスルー、ランタイムの再始動などを行うことができます。  

<!-- You can use Desktop Sync to keep your desktop workspace in sync with the cloud-based project workspace that you edit directly with the Web IDE. -->

Live Edit を使用して、クラウド・ベースのプロジェクト・ワークスペース内の変更内容を、実行中のアプリケーションに伝搬させることができます。 
<!-- You can use one or both of these features. And if you use Desktop Sync or -->
Live Edit を使用してアプリケーションを Live Edit モードにすると、実行中のアプリケーションをデバッグできます。


Bluemix Live Sync プロセスを以下の図に示します。    

図 1. Bluemix Live Sync プロセス
    

![Bluemix Live Sync プロセスのイメージ](images/bluemix-live-sync.png)

Liberty で実行される Java アプリケーションを開発している場合、[Eclipse Tools for Bluemix](/docs/manageapps/eclipsetools/eclipsetools.html#eclipsetools) を使用してリモートでデバッグすることができます。

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

Node.js アプリケーションをビルドしている場合、Web IDE を使用してプロジェクトに変更を加えると、{{site.data.keyword.Bluemix_notm}} Live Sync の Live Edit フィーチャーによって、{{site.data.keyword.Bluemix_notm}} で実行中のアプリケーションを素早く更新できます。Live Edit を使用すれば、デスクトップにある場合と同じように再デプロイせずに開発することができます。

Live Edit がサポートされるのは Node.js アプリケーションのみです。

Eclipse Orion Web IDE (Web IDE) の実行バーで、**「Live Edit」**をクリックします。

![Live Edit のある実行バーのイメージ](images/bluemix-live-sync-light.png)

Live Edit を使用すれば、{{site.data.keyword.Bluemix_notm}} で実行中の Node.js アプリケーションに対する変更を迅速にプレビューできます。Live Edit をオンにしてコードを更新すると、変更を加えてからほんの数秒で、Web アプリケーションのブラウザー・ウィンドウを最新表示して変更が反映されたことを確認できます。

<!--
For a tutorial on using the Live Edit feature of {{site.data.keyword.Bluemix_notm}} Live Sync, see the tutorial [Test and debug a Node.js app with Bluemix Live Sync![External link icon](../icons/launch-glyph.svg "External link icon")](https://hub.jazz.net/tutorials/livesync){:new_window}.
-->

Web IDE 内でファイルを変更すると、それらのファイルは {{site.data.keyword.Bluemix_notm}} で実行中のアプリケーションに自動的に再デプロイされます。Node アプリケーションの再始動が必要な場合、実行バーにある **「再始動」**ボタンを使用できます。

**注:** {{site.data.keyword.Bluemix_notm}} Live Sync の Live Edit フィーチャーの使用時に、より一貫性のある動作をさせるためには、256MB の追加メモリーが必要であり、メモリーが追加されます。

##{{site.data.keyword.Bluemix_notm}} Live Debug {: #live-debug}

{{site.data.keyword.Bluemix_notm}} Live Sync が Node.js アプリに対して使用可能になっている場合、{{site.data.keyword.Bluemix_notm}} Live Sync Debug フィーチャーにアクセスできます。

Debug を使用すると、アプリが {{site.data.keyword.Bluemix_notm}} で実行されている間に、コードの動的な編集、ブレークポイントの挿入、コードのステップスルー、ランタイムの再始動などを行うことができます。{{site.data.keyword.Bluemix_notm}} の多数のサービスのリストから選択しながら、アプリを段階的に素早く開発できます。

{{site.data.keyword.Bluemix_notm}} Live Debug には、以下のフィーチャーが含まれています。

* アプリケーション・ランタイム制御
* [node-inspector![「外部リンク」アイコン](../icons/launch-glyph.svg "「外部リンク」アイコン")](https://github.com/node-inspector/node-inspector){:new_window} を使用したデバッグ
* シェル・アクセス

###アプリケーション・ランタイム制御 {: #app-runtime}

アプリケーション・ランタイム制御により、Debug を使用してアプリの開始時の状態を検査することができます。この機能は、始動時に異常終了するアプリをトラブルシューティングする際に役立ちます。

アプリの開発中、次のアクションから選択できます。

* アプリの素早い再始動を実行する。
* アプリのコードが実行される前にアプリを一時停止する。

###Debug {: #debug}

Debug には、以下の機能が含まれています。

**制限:** Google Chrome が必要です。

* アプリ・コードにブレークポイントを設定して、特定の行で実行を一時停止する。
* ブレークポイントの条件を編集して、特定の条件が満たされた場合にのみ実行を一時停止する。
* ローカル変数やフィールドの状態を検査する。
* `console.log()` 呼び出しからのデバッグ出力を即座に表示する。cf ログをモニターするより、このアクションの方がより迅速です。
* 組み込みソース・コード・エディターを使用して、実行中のアプリ・コードに即時 (ただし一時的な) 変更を行う。

###シェル {: #shell}

このツールは、アプリが実行されているコンテナーへのシェル・アクセスを提供します。この端末を使用することにより、診断シェル・コマンドをリモート側で実行してアプリを管理することができます。

標準的な Linux コマンド (**top**、**ps**、および **kill** など) を使用するインスタンス内でメモリーおよび CPU の使用量をモニターします。

###{{site.data.keyword.Bluemix_notm}} Live Debug を使用可能にするためのアプリの構成 {: #configure_app_debug}

アプリは、IBM SDK for Node.js ビルドパックを使用する必要があります。カスタム・ビルドパックはサポートされていません。

1. ビルドパックがアプリの start コマンドを検出できるようにします。start コマンドは、`manifest.yml` ファイル内に設定されるのではなく、ビルドパックによって自動検出される必要があります。  

    a. `package.json` ファイルに、アプリの start コマンドを含む開始スクリプトを含めるようにします。  
    b. アプリの `manifest.yml` ファイルにコマンドが含まれている場合は、それをヌルに設定します。  

2. 環境変数を設定します。  

    a. `manifest.yml` ファイルに次の変数を追加します。
	
	```
	env:
      ENABLE_BLUEMIX_DEV_MODE: "true" 
	```

3. メモリーを増やします。  

    a. アプリの `manifest.yml` ファイルで、メモリー属性に指定されている値に 128M 以上を追加します。

{{site.data.keyword.Bluemix_notm}} Live Debug がインストールされたら、デバッグ・ツールを使用することができます。

アプリをプッシュし、次に `https://app-host.mybluemix.net/bluemix-debug/manage` を参照して、{{site.data.keyword.Bluemix_notm}} デバッグ・ユーザー・インターフェースにアクセスします。認証を求めるプロンプトが出されたら、ユーザー ID と、パーソナル・アクセス・トークンまたは IBM ID のパスワードを入力します。    

<!--
   **Note**: Your user ID for DevOps Services can be either an IBMid or a federated ID (corporate ID). If you use federated authentication, to log in to your Bluemix Live Sync command-line client, you must use a personal access token instead of a password. If you don't use federated authentication, your IBMid and password work with all clients. For more information about creating a personal access token, see [What's federated authentication and how does it affect me?![External link icon](../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/devops-services/2016/06/23/whats-federated-authentication-and-how-does-it-affect-me/){:new_window}
   -->

###アプリ構成の復元および Bluemix Live Debug の使用不可化 {: #restore_live_debug}

1. アプリの `manifest.yml` ファイルから ENABLE_BLUEMIX_DEV_MODE 環境変数を削除します。

2. アプリの、元の start コマンドとメモリー値を復元します。

3. アプリをプッシュします。

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

# 関連リンク
{: #rellinks}

<!--
## Tutorials and Samples
{: #samples}

* [Test and debug a Node.js app with Bluemix Live Sync![External link icon](../icons/launch-glyph.svg "External link icon")](https://hub.jazz.net/tutorials/livesync){:new_window}
-->


## 関連リンク
{: #general}

* [Eclipse tools for Bluemix![「外部リンク」アイコン](../icons/launch-glyph.svg "「外部リンク」アイコン")](https://www.ng.bluemix.net/docs/manageapps/eclipsetools/eclipsetools.html){:new_window}
