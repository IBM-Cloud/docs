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

 
Node.js 애플리케이션을 빌드하는 경우 {{site.data.keyword.Bluemix}} Live Sync를 사용하여 수동 재배치 없이 {{site.data.keyword.Bluemix_notm}}에서 애플리케이션 인스턴스를 신속하게 업데이트하고 개발할 수 있습니다.   
{: shortdesc}

변경할 경우 실행 중인 {{site.data.keyword.Bluemix_notm}} 애플리케이션에서 변경사항을 즉시 확인할 수 있습니다. {{site.data.keyword.Bluemix_notm}} Live Sync는
<!--from both the command line and -->
Eclipse Orion Web IDE(Web IDE)에서 작동합니다. {{site.data.keyword.Bluemix_notm}} Live Sync를 사용하여 Node.js로 작성된 애플리케이션을 디버그할 수 있습니다.  

{{site.data.keyword.Bluemix_notm}} Live Sync는 두 가지 기능으로 구성됩니다.
<!--three -->

<!--
**Desktop Sync**  

You can synchronize any desktop directory tree with a cloud-based project workspace similar to the way Dropbox works. The Web IDE directly edits the same cloud-based workspace, so both stay in sync. Desktop Sync works for any kind of application. To use Desktop Sync, you need to download and install the BL command line interface.  
-->

**Live Edit**

{{site.data.keyword.Bluemix_notm}}에서 실행 중인 Node.js 애플리케이션을 변경하고 브라우저에서 즉시 테스트할 수 있습니다. Web IDE 에서 변경한 사항은 애플리케이션의 파일 시스템으로 즉시 전파됩니다.  

**Debug**  

Node.js 애플리케이션이 Live Edit 모드일 경우 이를 쉘로 전환하여 디버그할 수 있습니다. 노드 검사기 디버거를 사용하여 동적으로 코드 편집, 중단점 삽입, 코드 스텝 스루, 런타임 다시 시작 등을 수행할 수 있습니다.  

<!-- You can use Desktop Sync to keep your desktop workspace in sync with the cloud-based project workspace that you edit directly with the Web IDE. -->

Live Edit를 사용하면 클라우드 기반 프로젝트 작업공간의 변경사항을 실행 중인 애플리케이션으로 전파할 수 있습니다.  
<!-- You can use one or both of these features. And if you use Desktop Sync or -->
Live Edit를 사용하여 애플리케이션을 Live Edit 모드로 전환할 경우 실행 중인 애플리케이션을 디버그할 수 있습니다.


Bluemix Live Sync 프로세스는 다음 그림에 표시되어 있습니다.    

그림 1. Bluemix Live Sync 프로세스
    

![Bluemix Live Sync 프로세스의 이미지](images/bluemix-live-sync.png)

Liberty에서 실행되는 Java 애플리케이션을 개발하는 경우, [Eclipse Tools for Bluemix](/docs/manageapps/eclipsetools/eclipsetools.html#eclipsetools)를 사용하여 원격으로 디버그할 수 있습니다.

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

Node.js 애플리케이션을 빌드하고 있는 경우, Web IDE를 사용하여 프로젝트를 변경할 때 {{site.data.keyword.Bluemix_notm}} Live Sync의 Live Edit 기능을 사용하면 {{site.data.keyword.Bluemix_notm}}에서 실행 중인 애플리케이션 인스턴스를 신속하게 업데이트할 수 있습니다. Live Edit를 사용하면 재배치 없이 데스크탑에서처럼 개발할 수 있습니다.

Live Edit는 Node.js 애플리케이션에서만 지원됩니다.

Eclipse Orion Web IDE(Web IDE)의 실행 표시줄에서 **Live Edit**를 클릭하십시오.

![Live Edit 기능이 있는 실행 표시줄](images/bluemix-live-sync-light.png)

Live Edit를 사용하면 {{site.data.keyword.Bluemix_notm}}에서 실행 중인 Node.js 애플리케이션에 대한 변경사항을 신속하게 미리 볼 수 있습니다. Live Edit를 켠 상태에서 코드를 업데이트할 경우 웹 애플리케이션의 브라우저 창을 새로 고치면 변경한 지 몇 초 만에 변경사항이 적용되어 표시됩니다.

<!--
For a tutorial on using the Live Edit feature of {{site.data.keyword.Bluemix_notm}} Live Sync, see the tutorial [Test and debug a Node.js app with Bluemix Live Sync![External link icon](../icons/launch-glyph.svg "External link icon")](https://hub.jazz.net/tutorials/livesync){:new_window}.
-->

Web IDE에서 변경한 파일은 {{site.data.keyword.Bluemix_notm}}에서 실행 중인 애플리케이션에 자동으로 재배치됩니다. 노드 애플리케이션을 다시 시작해야 하는 경우 실행 표시줄에 있는 **다시 시작** 단추를 사용하면 됩니다.

**참고:** {{site.data.keyword.Bluemix_notm}} Live Sync의 Live Edit 기능을 사용할 때 보다 일관된 경험을 얻으려면 256MB의 추가 메모리가 필요하며 추가될 예정입니다.

##{{site.data.keyword.Bluemix_notm}} Live Debug {: #live-debug}

{{site.data.keyword.Bluemix_notm}} Live Sync가 Node.js 앱에서 사용으로 설정된 경우, {{site.data.keyword.Bluemix_notm}} Live Sync Debug 기능에 액세스할 수 있습니다.

debug 기능을 사용할 경우, {{site.data.keyword.Bluemix_notm}}에서 앱을 제공하는 동안 코드 편집, 중단점 삽입, 코드 스텝 스루, 런타임 다시 시작 등을 모두 동적으로 수행할 수 있습니다. 또한 Agile 방식으로 앱을 증분식으로 개발하면서 대형 {{site.data.keyword.Bluemix_notm}} 서비스 목록에서 서비스를 선택할 수 있습니다.

{{site.data.keyword.Bluemix_notm}} Live Debug에는 다음과 같은 기능이 포함되어 있습니다.

* 애플리케이션 런타임 제어
* [node-inspector ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/node-inspector/node-inspector){:new_window}를 사용하여 디버깅
* 쉘 액세스

###애플리케이션 런타임 제어 {: #app-runtime}

애플리케이션 런타임 제어를 사용하면 Debug 기능을 통해 시작 시 앱의 상태를 검사할 수 있습니다. 이 기능은 시작 시 충돌하는 앱의 문제점을 해결할 때 유용합니다.

앱을 개발할 때 다음 조치 중에서 선택할 수 있습니다.

* 앱을 신속하게 다시 시작합니다.
* 앱 코드를 실행하기 전에 앱을 일시중단합니다.

###Debug {: #debug}

Debug에는 다음과 같은 기능이 포함되어 있습니다.

**제한사항:** Google Chrome이 필요합니다.

* 특정 행에서 실행을 일시정지하도록 앱 코드에 중단점 설정
* 특정 기준이 충족될 경우에만 실행을 일시정지하도록 중단점 조건 편집
* 로컬 변수 및 필드의 상태 검사
* `console.log()` 호출의 디버그 출력 즉시 표시. 이 조치는 cf 로그를 모니터링하는 것보다 빠릅니다.
* 기본 제공 소스 코드 편집기를 사용하여 실행 중인 앱 코드를 임시로 즉시 변경

###쉘 {: #shell}

이 도구는 앱이 실행 중인 컨테이너에 대한 쉘 액세스를 제공합니다. 이 터미널을 사용하면 진단 쉘 명령을 원격으로 실행하여 앱을 관리할 수 있습니다.

표준 Linux 명령(예: **top**, **ps** 및 **kill**)을 사용하여 인스턴스 내에서 메모리 및 CPU 사용량을 모니터링하십시오.

###{{site.data.keyword.Bluemix_notm}} Live Debug를 사용으로 설정하도록 앱 구성 {: #configure_app_debug}

앱은 IBM SDK for Node.js 빌드팩을 사용해야 합니다. 사용자 정의 빌드팩은 지원되지 않습니다.

1. 빌드팩에서 앱 시작 명령을 발견하도록 허용하십시오. start 명령은 `manifest.yml` 파일에 설정되는 것이 아니라 빌드팩에서 자동으로 발견되어야 합니다.  

    a. `package.json` 파일에 앱에 대한 start 명령을 포함하는 시작 스크립트가 포함되어 있는지 확인하십시오.  
    b. 앱의 `manifest.yml` 파일에 명령이 포함되어 있는 경우, null로 설정하십시오.  

2. 환경 변수를 설정하십시오.  

    a. `manifest.yml` 파일에서 다음 변수를 추가하십시오.	
	```
	env:
      ENABLE_BLUEMIX_DEV_MODE: "true"
	```

3. 메모리를 늘리십시오.  

    a. 앱의 `manifest.yml` 파일에서 메모리 속성에 대해 지정된 값에 128M 이상을 추가하십시오.

{{site.data.keyword.Bluemix_notm}} Live Debug를 설치한 후 디버그 도구를 사용할 수 있습니다.

앱을 푸시한 다음 `https://app-host.mybluemix.net/bluemix-debug/manage`로 이동하여 {{site.data.keyword.Bluemix_notm}} 디버그 사용자 인터페이스에 액세스하십시오. 인증을 요구하는 프롬프트가 표시되면 사용자 ID 및 개인 액세스 토큰 또는 IBM ID 비밀번호를 입력하십시오.    

<!--
   **Note**: Your user ID for DevOps Services can be either an IBMid or a federated ID (corporate ID). If you use federated authentication, to log in to your Bluemix Live Sync command-line client, you must use a personal access token instead of a password. If you don't use federated authentication, your IBMid and password work with all clients. For more information about creating a personal access token, see [What's federated authentication and how does it affect me?![External link icon](../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/devops-services/2016/06/23/whats-federated-authentication-and-how-does-it-affect-me/){:new_window}
   -->

###앱 구성 복원 및 Bluemix Live Debug 사용 안함 {: #restore_live_debug}

1. 앱의 `manifest.yml` 파일에서 ENABLE_BLUEMIX_DEV_MODE 환경 변수를 제거하십시오.

2. 앱의 원래 시작 명령 및 메모리 값을 복원하십시오.

3. 앱을 푸시하십시오.

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

# 관련 링크
{: #rellinks}

<!--
## Tutorials and Samples
{: #samples}

* [Test and debug a Node.js app with Bluemix Live Sync![External link icon](../icons/launch-glyph.svg "External link icon")](https://hub.jazz.net/tutorials/livesync){:new_window}
-->


## 관련 링크
{: #general}

* [Eclipse Tools for Bluemix ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.ng.bluemix.net/docs/manageapps/eclipsetools/eclipsetools.html){:new_window}
