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

 
如果您要构建 Node.js 应用程序，那么可以使用 {{site.data.keyword.Bluemix}} Live Sync 快速更新 {{site.data.keyword.Bluemix_notm}} 上的应用程序实例并进行开发，而无需手动重新部署。   
{: shortdesc}

执行更改后，您可以立即在运行中的 {{site.data.keyword.Bluemix_notm}} 应用程序中看到该更改。{{site.data.keyword.Bluemix_notm}} Live Sync 会在  
<!--from both the command line and -->
Eclipse Orion Web IDE (Web IDE) 中运行。您可以使用 {{site.data.keyword.Bluemix_notm}} Live Sync 来调试以 Node.js 编写的应用程序。  

{{site.data.keyword.Bluemix_notm}} Live Sync 由两个功能部件组成。
<!-- three -->

<!--
**Desktop Sync**  

You can synchronize any desktop directory tree with a cloud-based project workspace similar to the way Dropbox works. The Web IDE directly edits the same cloud-based workspace, so both stay in sync. Desktop Sync works for any kind of application. To use Desktop Sync, you need to download and install the BL command line interface.  
-->

**实时编辑**

您可以对 {{site.data.keyword.Bluemix_notm}} 中运行的 Node.js 应用程序进行更改，然后立即在浏览器中测试这些更改。在 Web IDE 中进行的任何更改都会立即传播到应用程序的文件系统中。  

**调试**  

当 Node.js 应用程序处于“实时编辑”方式时，您可以创建 shell 并在其中进行调试。您可以使用 Node Inspector 调试器来动态编辑代码、插入断点、单步执行代码、重新启动运行时，等等。  

<!-- You can use Desktop Sync to keep your desktop workspace in sync with the cloud-based project workspace that you edit directly with the Web IDE. -->

您可以使用“实时编辑”将基于云的项目工作空间中的更改传播到运行中应用程序。 
<!-- You can use one or both of these features. And if you use Desktop Sync or -->
如果使用“实时编辑”将应用程序置于“实时编辑”方式，那么可以调试运行中应用程序。


下图说明了 Bluemix Live Sync 过程。    

图 1. Bluemix Live Sync 过程
    

![Bluemix Live Sync 过程的图像](images/bluemix-live-sync.png)

如果您要开发在 Liberty 上运行的 Java 应用程序，那么可以使用 [Eclipse Tools for Bluemix](/docs/manageapps/eclipsetools/eclipsetools.html#eclipsetools) 进行远程调试。


##实时编辑 {: #live-edit}

如果您要构建 Node.js 应用程序，那么在使用 Web IDE 对项目进行更改后，可以使用 {{site.data.keyword.Bluemix_notm}} Live Sync 的“实时编辑”功能来快速更新 {{site.data.keyword.Bluemix_notm}} 上运行的应用程序实例。利用“实时编辑”，无需重新部署即可像在桌面上一样进行开发。

“实时编辑”仅支持用于 Node.js 应用程序。

在 Eclipse Orion Web IDE (Web IDE) 中，单击运行栏中的**实时编辑**。

![运行栏中实时编辑的图像](images/bluemix-live-sync-light.png)

使用“实时编辑”，可以快速预览对 {{site.data.keyword.Bluemix_notm}} 上运行的 Node.js 应用程序所进行的更改。如果在打开“实时编辑”的情况下更新代码，那么在执行更改之后仅需几秒钟的时间，就可以通过刷新 Web 应用程序浏览器窗口看到这些更改反映出来。

<!--
For a tutorial on using the Live Edit feature of {{site.data.keyword.Bluemix_notm}} Live Sync, see the tutorial [Test and debug a Node.js app with Bluemix Live Sync![External link icon](../icons/launch-glyph.svg "External link icon")](https://hub.jazz.net/tutorials/livesync){:new_window}.
-->

当您在 Web IDE 中更改文件时，系统会自动将它们重新部署到 {{site.data.keyword.Bluemix_notm}} 上运行的应用程序中。如果需要重新启动 Node 应用程序，那么可以使用运行栏中的**重新启动**按钮。

**注：**为了在使用 {{site.data.keyword.Bluemix_notm}} Live Sync 的“实时编辑”功能时能有更一致的体验，需要并将添加额外的 256 MB 内存。

##{{site.data.keyword.Bluemix_notm}} 实时调试 {: #live-debug}

只要为您的 Node.js 应用程序启用了 {{site.data.keyword.Bluemix_notm}} Live Sync，就可以访问 {{site.data.keyword.Bluemix_notm}} Live Sync 的“实时调试”功能。

通过调试，可以执行动态编辑代码、插入断点、单步调试代码、重新启动运行时等操作，而且所有这些操作都可在 {{site.data.keyword.Bluemix_notm}} 为应用程序提供服务期间来执行。通过从大型 {{site.data.keyword.Bluemix_notm}} 服务列表中进行选择，可以敏捷地以递增方式开发应用程序。

{{site.data.keyword.Bluemix_notm}} 实时调试包括以下功能：

* 应用程序运行时控件
* 使用 [node-inspector ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://github.com/node-inspector/node-inspector){:new_window} 调试
* shell 访问

###应用程序运行时控件 {: #app-runtime}

利用应用程序运行时控件，您可以使用“调试”在启动时检测应用程序的状态。当您对启动时崩溃的应用程序进行故障诊断时，此功能很有用。

在开发应用程序时，可以从以下操作进行选择：

* 快速重新启动应用程序
* 运行任何应用程序代码之前暂挂应用程序

###调试 {: #debug}

“调试”包括以下功能：

**限制：**Google Chrome 是必需的。

* 在应用程序代码中设置断点，以在特定行暂停执行。
* 编辑断点条件以仅在满足特定条件时暂停执行。
* 检查本地变量和字段的状态。
* 立即查看 `console.log()` 调用的调试输出。此操作比监视 cf 日志速度更快。
* 使用内置源代码编辑器对运行中应用程序代码立即执行临时更改。

###shell {: #shell}

使用此工具，可以通过 shell 访问您的应用程序运行所在的容器。通过使用此终端，您可以远程运行诊断 shell 命令以管理您的应用程序。

使用标准 Linux 命令（例如，**top**、**ps** 和 **kill**），监视实例中的内存和 CPU 使用量。

###将应用程序配置为启用 {{site.data.keyword.Bluemix_notm}} 实时调试 {: #configure_app_debug}

应用程序必须使用 IBM SDK for Node.js buildpack。不支持定制 buildpack。

1. 允许 buildpack 检测应用程序 start 命令。start 命令必须由 buildpack 自动检测，而不是在 `manifest.yml` 文件中设置。  

    a. 确保 `package.json` 文件包含启动脚本，其中含有应用程序的 start 命令。  
    b. 如果应用程序 `manifest.yml` 文件包含命令，请将其设置为 null。  

2. 设置环境变量。  

    a. 在 `manifest.yml` 文件中，添加以下变量：
	
	```
	env:
      ENABLE_BLUEMIX_DEV_MODE: "true" 
	```

3. 增大内存。  

    a. 在应用程序 `manifest.yml` 文件中，将指定给内存属性的值加上 128M 或更大的值。

在安装 {{site.data.keyword.Bluemix_notm}} 实时调试后，可以使用调试工具。

推送应用程序，然后浏览到 `https://app-host.mybluemix.net/bluemix-debug/manage`，以访问 {{site.data.keyword.Bluemix_notm}} 调试用户界面。收到认证提示时，请输入用户标识和个人访问令牌或 IBM 标识密码。    

<!--
   **Note**: Your user ID for DevOps Services can be either an IBMid or a federated ID (corporate ID). If you use federated authentication, to log in to your Bluemix Live Sync command-line client, you must use a personal access token instead of a password. If you don't use federated authentication, your IBMid and password work with all clients. For more information about creating a personal access token, see [What's federated authentication and how does it affect me?![External link icon](../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/devops-services/2016/06/23/whats-federated-authentication-and-how-does-it-affect-me/){:new_window}
   -->

###复原应用程序配置并禁用 Bluemix 实时调试 {: #restore_live_debug}

1. 从应用程序 `manifest.yml` 文件中除去 ENABLE_BLUEMIX_DEV_MODE 环境变量。

2. 复原应用程序的原始 start 命令和内存值。

3. 推送应用程序。


## 相关链接
{: #general}

* [Eclipse Tools for Bluemix ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.ng.bluemix.net/docs/manageapps/eclipsetools/eclipsetools.html){:new_window}
