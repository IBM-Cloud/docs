---

copyright:
  years: 2015, 2016

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#管理 Liberty 和 Node.js 应用程序
{: #app_management}

*上次更新时间：2016 年 3 月 17 日*

应用程序管理实用程序是一组开发和调试实用程序，可以对 {{site.data.keyword.Bluemix}} 上的 Liberty 和 Node.js 应用程序启用这些实用程序。
{:shortdesc}

##应用程序管理实用程序
{: #Utilities}

以下实用程序支持 Liberty 和 Node.js。

  1. *proxy*：最少应用程序管理，用作应用程序和 {{site.data.keyword.Bluemix_notm}} 之间的代理。

    启用该项时，buildpack 会启动位于应用程序的运行时与容器之间的代理。*proxy* 实用程序会处理应用程序接收到的所有请求。它会执行应用程序管理操作或将请求转发给应用程序，具体取决于请求的类型。通过 *proxy*，可以启用大多数其他应用程序管理实用程序。启用 *proxy* 后，即使应用程序崩溃，应用程序容器也会继续保持活动。此代理还允许增量文件更新，这使您能够使用 Node.js 应用程序的“实时编辑”方式。
	
  2. *devconsole*：启用开发控制台实用程序，该实用程序可通过以下 URL 进行访问：```
    http://<yourappname>.mybluemix.net/bluemix-debug/manage
    ```
	
    使用开发控制台，用户可以重新启动、停止或暂挂自己的应用程序。用户还可以启用或访问 shell 和 inspector 实用程序。

    devconsole 实用程序还会启动 *proxy*。
	
  3. *hc*：Health Center 代理程序，支持通过 Health Center 客户机来监视应用程序。

    Health Center 支持使用 IBM Monitoring and Diagnostic Tools 分析 Liberty 和 Node.js 应用程序的性能。有关更多信息，请参阅 [How to analyze the performance of Liberty Java or Node.js apps in {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/2015/07/03/how-to-analyze-performance-in-bluemix/){:new_window}。</p></li>
	
  4. *shell*：启用基于 Web 的 shell，该 shell 可通过 devconsole 实用程序或通过访问以下 URL 来进行访问：```
    http://<yourappname>.mybluemix.net/bluemix-debug/shell
    ```
	
    访问 shell 实用程序后，将显示一个终端窗口，允许通过 shell 访问您的应用程序。您可以执行常规 shell 中支持的所有操作，例如编辑文件、检查内存使用量或运行诊断命令。
	
    *shell* 实用程序还会启动 *proxy*。

以下实用程序仅支持 Liberty。

  1. *debug*：将 Liberty 应用程序转换为调试方式，并启用客户机（例如，IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}）来建立与应用程序的远程调试会话。
  
   有关更多信息，请参阅[远程调试](../manageapps/eclipsetools/eclipsetools.html#remotedebug)。
   
   *debug* 实用程序还会启动 *proxy*。
   
  2. *jmx*：启用 JMX REST Connector 以允许远程 JMX 客户机使用 {{site.data.keyword.Bluemix_notm}} 用户凭证来管理应用程序。
  
  有关配置 JMX Connector 的更多信息，请参阅 [Configuring secure JMX connection to Liberty](https://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/twlp_admin_restconnector.html){:new_window}。
  
  *jmx* 实用程序不会启动 proxy。

以下实用程序仅支持 Node.js。

  1. *inspector*：启用 Node Inspector 调试器接口，该接口可通过 *devconsole* 实用程序或在 *https://myApp.mybluemix.net/bluemix-debug/inspector* 上进行访问。
  
  inspector 进程在应用程序容器中运行。使用此实用程序可创建 CPU 使用情况概要文件，添加断点和调试代码，所有这些操作都可在应用程序在 {{site.data.keyword.Bluemix_notm}} 上运行的同时执行。有关 Node Inspector 模块的更多信息，请参阅 [node-inspector on GitHub](https://github.com/node-inspector/node-inspector){:new_window}。
  
  *inspector* 实用程序还会启动 *proxy*。
  
  2. *strongpm*：启用 [StrongLoop Arc](https://strongloop.com/node-js/arc){:new_window} 以通过 [StrongLoop Metrics、Profiling 和 Tracing](https://strongloop.com/node-js/devops-tools/){:new_window} 等实用程序来分析 Node.js 应用程序。
    
  *strongpm* 实用程序还会启动 *proxy*。
  
  要为 Node.js 应用程序配置 [StrongLoop Arc](https://strongloop.com/node-js/arc){:new_window}，请执行以下步骤：

    1. 配置 *strongpm* BlUEMIX_APP_MGMT_ENABLE 环境变量，并重新编译打包应用程序。
    
	```
    cf set-env <appname> BLUEMIX_APP_MGMT_ENABLE strongpm
    cf restage <appname>
    ```
	
    2. 在 Cloud Foundry 命令行中，向应用程序添加路径，该路径将“-pm”附加到应用程序名称，例如 <appname>-pm.mybluemix.net。
    
	```
    cf map-route <appname> ng.bluemix.net -n <appname>-pm
    ```
	
    3. 在本地工作站上，安装 [StrongLoop npm 模块](https://www.npmjs.com/package/strongloop){:new_window}。
    
	```
    npm install -g strongloop```
	
    4. 在 [StrongLoop 的 Web 站点](https://strongloop.com/register/){:new_window}上创建帐户。
    5. 在本地工作站上启动 Arc，然后使用创建的帐户登录。
    
	```
    slc arc```
	
    6. 浏览到 Arc 内的 Process Manager 视图。在 Process Manager 中，输入新创建的路径与端口 80。按“激活”按钮。有关更多详细信息，请参阅[有关使用 Arc 的完整文档](https://docs.strongloop.com/display){:new_window}。
	
  3. *trace*：动态设置跟踪级别（如果应用程序使用的是 *log4js*、*ibmbluemix* 或 *bunyan* 日志记录模块）。
  
  **注：**支持的依赖关系版本：

    * log4js：(0.6.0 - 0.6.24)
    * bunyan：(1.0.0, 1.0.1, 1.1.0 - 1.1.3, 1.2.0 - 1.2.3, 1.3.0 - 1.3.5)
    * ibmbluemix：(1.0.0-20140707-1250)-(1.0.0-20150409-1328)
  
  转至 {{site.data.keyword.Bluemix_notm}} Web 控制台的“实例详细信息”页面，然后选择**操作**以查看 UI。

  *trace* 实用程序不会启动 *proxy*。

##如何配置应用程序管理
{: #configure}

要启用应用程序管理实用程序，请设置 *BLUEMIX_APP_MGMT_ENABLE* 环境变量，并重新编译打包应用程序。通过以“+”分隔实用程序，可以启用多个实用程序。

例如，要启用 devconsole 和 *shell* 实用程序，请运行以下命令：

```
cf set-env myApp BLUEMIX_APP_MGMT_ENABLE devconsole+shell
```

请勿忘记在设置环境变量后重新编译打包应用程序：

```
cf restage myApp
```

如果不希望应用程序管理实用程序随应用程序一起安装，请将 *BLUEMIX_APP_MGMT_INSTALL* 环境变量设置为“false”并重新编译打包应用程序。

例如：

```
cf set-env myApp BLUEMIX_APP_MGMT_INSTALL false
cf restage myApp
```

##限制
{: #restrictions}

* 应用程序管理实用程序仅支持单实例应用程序。
* 使用应用程序管理实用程序对应用程序进行的更改是瞬态的，退出此方式后就没有了。此方式仅用于临时开发，由于存在性能问题，因此不应用作生产环境。
* 如果在 manifest.yml 文件（命令）或 CF CLI (-c) 中设置启动命令，那么大多数应用程序管理实用程序都不会工作。这些方法是 buildpack 覆盖，也是用于启动 Node.js 应用程序的反模式。为了获得最佳结果，请在 package.json 文件或 Procfile 中设置启动命令。

##Eclipse Tools 的开发方式
{: #devmode}

开发方式是 [Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](../manageapps/eclipsetools/eclipsetools.html#eclipsetools) 的一种功能，该功能使开发者能够在应用程序在云中运行的同时处理应用程序。

在 {{site.data.keyword.Bluemix_notm}} 上处理应用程序时，开发人员可能会觉得，他们不能像在本地环境中那样正常执行开发活动。为了解决此问题，通过 Eclipse Tools 的开发方式提供了一种在云中工作的方法，即在一个临时的安全工作空间中工作。

Liberty 和 Node.js 应用程序都支持开发方式。Liberty 或 Node.js 应用程序启用开发方式后，您可以通过递增方式更新应用程序文件，不需要推送应用程序。您还可以使用应用程序建立调试会话。Liberty 应用程序的开发方式相当于启用了调试和 jmx 应用程序管理实用程序。Node.js 应用程序的开发方式相当于启用了 *devconsole*、*inspector* 和 *shell* 实用程序。
