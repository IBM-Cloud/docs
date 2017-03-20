---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-11"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 管理 Liberty 和 Node.js 应用程序
{: #app_management}


应用程序管理实用程序是一组开发和调试实用程序，可以对 {{site.data.keyword.Bluemix}} 上的 Liberty 和 Node.js 应用程序启用这些实用程序。
{:shortdesc}

## 应用程序管理实用程序
{: #Utilities}

### 以下实用程序支持 Liberty 和 Node.js
{: #liberty_and_node_utilities}

#### proxy
{: #proxy}

*proxy* 在应用程序和 {{site.data.keyword.Bluemix_notm}} 之间提供最少的应用程序管理。

启用该项时，buildpack 会启动位于应用程序的运行时与容器之间的代理。*proxy* 实用程序会处理应用程序接收到的所有请求。它会执行应用程序管理操作或将请求转发给应用程序，具体取决于请求的类型。通过 *proxy*，可以启用大多数其他应用程序管理实用程序。启用 *proxy* 后，即使应用程序崩溃，应用程序容器也会继续保持活动。此 proxy 代理还允许增量文件更新，这使您能够使用 Node.js 应用程序的“实时编辑”方式。

#### noproxy
{: #noproxy}

*noproxy* 实用程序将禁用其他某个实用程序本来会自动启动的 *proxy* 实用程序。使用 Diego 后，代理不再是必需的，因为 Diego 直接向应用程序提供了 *ssh* 的功能，并将设置端口转发。

*noproxy* 实用程序仅适用于在 Diego 单元中运行的应用程序。



#### devconsole
{: #devconsole}

使用 (*devconsole*) 开发控制台，用户可以重新启动、停止或暂挂自己的应用程序。用户还可以启用或访问 shell 和 inspector 实用程序。这可通过以下 URL 进行访问：
```
  https://<yourappname>.mybluemix.net/bluemix-debug/manage
```

对于 Node V6.3.0 或更高版本，开发控制台可为应用程序提供重新启动按钮，并提供 shell 实用程序的访问权。有关更多信息，请参阅 *inspector* 讨论。

*devconsole* 实用程序还会启动 *proxy*。

#### hc
{: #hc}

(*hc*) Health Center 代理程序支持通过 Health Center 客户机来监视应用程序。

Health Center 支持使用 IBM Monitoring and Diagnostic Tools 分析 Liberty 和 Node.js 应用程序的性能。有关更多信息，请参阅 [How to analyze the performance of Liberty Java or Node.js apps in {{site.data.keyword.Bluemix_notm}} ![外部链接图标](../icons/launch-glyph.svg)](https://developer.ibm.com/bluemix/2015/07/03/how-to-analyze-performance-in-bluemix/){: new_window}。</p></li>

*hc* 实用程序还会启动 *proxy*。

*hc* 实用程序可以与 *noproxy* 一起使用。要将 Health Center 与 *noproxy* 一起使用，请首先使用 `cf ssh` 命令建立端口转发。例如：

```
$ cf ssh -N -T -L 1883:127.0.0.1:1883 <appName>
```

接着，要与 Health Center 客户机连接，请使用 [MQTT 连接 ![外部链接图标](../icons/launch-glyph.svg)](http://www.ibm.com/support/knowledgecenter/SS3KLZ/com.ibm.java.diagnostics.healthcenter.doc/topics/connectingtojvm.html){: new_window}，并将主机指定为 `127.0.0.1`，将端口指定为 `1883`。

#### shell
{: #shell}

*shell* 实用程序可启用基于 Web 的 shell。通过 *devconsole* 实用程序或通过访问以下 URL 可访问该实用程序：

```
  https://<yourappname>.mybluemix.net/bluemix-debug/shell
```

访问 *shell* 实用程序后，将显示一个终端窗口，允许通过 shell 访问您的应用程序。您可以执行常规 shell 中支持的所有操作，例如编辑文件、检查内存使用量或运行诊断命令。

*shell* 实用程序还会启动 *proxy*。

Diego 通过 `cf ssh` 命令提供交互式 shell，因此 *shell* 实用程序只适用于在 DEA 上运行的应用程序。

### 以下实用程序仅支持 Liberty
{: #liberty_utilities}

#### debug
{: #debug}

*debug* 实用程序将 Liberty 应用程序置于调试方式，并支持客户机（例如，IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}）建立与应用程序的[远程调试](/docs/manageapps/eclipsetools/eclipsetools.html#remotedebug)会话。

*debug* 实用程序还会启动 *proxy*。

*debug* 实用程序可以与 *noproxy* 一起使用。要将调试器与 *noproxy* 一起使用，请首先使用 `cf ssh` 命令建立端口转发。例如：

```
$ cf ssh -N -T -L 7777:127.0.0.1:7777 <appName>
```

接着，要在 Eclipse 中建立连接，请使用“远程 Java 配置”，并将主机指定为 `127.0.0.1`，将端口指定为 `7777`。

#### jmx
{: #jmx}

*jmx* 实用程序启用 JMX REST Connector 以允许远程 JMX 客户机使用 {{site.data.keyword.Bluemix_notm}} 用户凭证来管理应用程序。

有关配置 JMX Connector 的更多信息，请参阅 [Configuring secure JMX connection to Liberty profile ![外部链接图标](../icons/launch-glyph.svg)](https://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/twlp_admin_restconnector.html){:new_window}。

*jmx* 实用程序不会启动 proxy。

#### localjmx
{: #localjmx}

*localjmx* 实用程序将启用 [localConnector-1.0 ![外部链接图标](../icons/launch-glyph.svg)](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_feature_localConnector-1.0.html){:new_window} Liberty 功能。此功能与本地端口转发组合使用可支持另一种方法来允许远程 JMX 客户机管理应用程序。

*localjmx* 实用程序仅适用于在 Diego 单元中运行的应用程序。要使用 *localjmx*，请首先使用 `cf ssh` 命令建立端口转发。例如：

```
$ cf ssh -N -T -L 5000:127.0.0.1:5000 <appName>
```

接着，要与 JConsole 连接，请选择“远程进程”，指定 `127.0.0.1:5000`，并使用不安全连接。


### 以下实用程序仅支持 Node.js
{: #node_utilities}

#### inspector
{: #inspector}

对于 6.3.0 之前的 Node.js 版本，*inspector* 会启用 Node Inspector 调试器接口。*inspector* 进程在应用程序容器中运行。使用此实用程序可创建 CPU 使用情况概要文件，添加断点和调试代码，所有这些操作都可在应用程序在 {{site.data.keyword.Bluemix_notm}} 上运行的同时执行。有关 Node Inspector 模块的更多信息，请参阅 [node-inspector on GitHub ![外部链接图标](../icons/launch-glyph.svg)](https://github.com/node-inspector/node-inspector){:new_window}。

对于 Node.js V6.3.0 和更高版本，*inspector* 会利用 [V8 Inspector Integration for Node.js ![外部链接图标](../icons/launch-glyph.svg)](https://nodejs.org/dist/latest-v6.x/docs/api/debugger.html#debugger_v8_inspector_integration_for_node_js){:new_window}。

缺省情况下，inspector 实用程序会启动 *proxy*，但远程调试方式取决于 Node.js 版本以及使用的是 *proxy* 还是 *noproxy*。下表显示了如何在各种场景中访问远程调试。

| | proxy | noproxy |
|---|---|---|
| < &nbsp; 6.3.0 | devconsole 实用程序*：*<br/> https://myApp.mybluemix.net/bluemix-debug/inspector | http://127.0.0.1:8790
| >= 6.3.0 | chrome-devtools URL | chrome-devtools URL

对于 *noproxy* 以及 6.3.0 之前的 Node.js 版本，通过本地端口转发启用对 URL 的访问。例如：

```
$ cf ssh -N -T -L <localPort>:127.0.0.1:8790 <appName>
```

然后，在 Chrome Web 浏览器中浏览到 http://127.0.0.1:8790。通过设置 BLUEMIX_APP_MGMT_INSPECTOR 环境变量更改该端口：

```
$ cf set-env <appName> BLUEMIX_APP_MGMT_INSPECTOR='{port: 9790}'
```

对于 Node.js V6.3.0 或更高版本，您将找到一条日志消息，其中包含可用于将 Chrome DevTools 附加到应用程序的 URL。日志消息类似以下内容：

```
  2016-11-30T16:40:56.03-0500 [APP/0]      OUT Starting app with 'node --inspect=9229  app.js '
  2016-11-30T16:40:56.17-0500 [APP/0]      ERR Debugger listening on port 9229.
  2016-11-30T16:40:56.17-0500 [APP/0]      ERR To start debugging, open the following URL in Chrome:
  2016-11-30T16:40:56.17-0500 [APP/0]      ERR     chrome-devtools://devtools/remote/serve_file...
```

通过本地端口转发启用对 URL 的访问。例如：

```
$ cf ssh -N -T -L 9229:127.0.0.1:9229 <appName>
```

您将需要最新版本的 Chrome Web 浏览器才可浏览到此 URL。在此场景中，proxy 不会将流量路由到 inspector。

#### trace
{: #trace}

*trace* 轨迹允许您动态设置跟踪级别（如果应用程序使用的是 *log4js*、*ibmbluemix* 或 *bunyan* 日志记录模块）。

**注：**支持的依赖关系版本：
* log4js：(0.6.0 - 0.6.24)
* bunyan：(1.0.0, 1.0.1, 1.1.0 - 1.1.3, 1.2.0 - 1.2.3, 1.3.0 - 1.3.5)
* ibmbluemix：(1.0.0-20140707-1250)-(1.0.0-20150409-1328)

转至 {{site.data.keyword.Bluemix_notm}} Web 控制台的“实例详细信息”页面，然后选择**操作**以查看 UI。

如果是使用“-b buildpack”选项启动的应用程序，那么 *trace* 实用程序不可用。

*trace* 实用程序不会启动 *proxy*。

##  如何配置应用程序管理
{: #configure}

要启用应用程序管理实用程序，请设置 *BLUEMIX_APP_MGMT_ENABLE* 环境变量，并重新编译打包应用程序。通过以“+”分隔实用程序，可以启用多个实用程序。

例如，要启用 *devconsole* 和 *shell* 实用程序，请运行以下命令：

```
$ cf set-env myApp BLUEMIX_APP_MGMT_ENABLE devconsole+shell
```

在设置环境变量后重新编译打包应用程序：

```
$ cf restage myApp
```

如果不希望应用程序管理实用程序随应用程序一起安装，请将 *BLUEMIX_APP_MGMT_INSTALL* 环境变量设置为“false”并重新编译打包应用程序。

例如：

```
$ cf set-env myApp BLUEMIX_APP_MGMT_INSTALL false
$ cf restage myApp
```

## 限制
{: #restrictions}

* 对于在 DEA 节点上运行的应用程序，应用程序管理实用程序仅支持单实例应用程序。
* 使用应用程序管理实用程序对应用程序进行的更改是瞬态的，退出此方式后就没有了。此方式仅用于临时开发，由于存在性能问题，因此不应用作生产环境。
* 如果在 `manifest.yml` 文件（命令）或 CF CLI (-c) 中设置启动命令，那么大多数应用程序管理实用程序都不会工作。这些方法是 buildpack 覆盖，也是用于启动 Node.js 应用程序的反模式。为了获得最佳结果，请在 `package.json` 文件或 `Procfile` 中设置启动命令。

## Eclipse Tools 的开发方式
{: #devmode}

开发方式是 [Eclipse Tools for {{site.data.keyword.Bluemix_notm}}](/docs/manageapps/eclipsetools/eclipsetools.html#eclipsetools) 的一种功能，该功能使开发者能够在应用程序在云中运行的同时处理应用程序。

在 {{site.data.keyword.Bluemix_notm}} 上处理应用程序时，开发者可能会觉得，他们不能像在本地环境中那样正常执行开发活动。为了解决此问题，通过 Eclipse Tools 的开发方式提供了一种在云中工作的方法，即在一个临时的安全工作空间中工作。

Liberty 和 Node.js 应用程序都支持开发方式。Liberty 或 Node.js 应用程序启用开发方式后，您可以通过递增方式更新应用程序文件，不需要推送应用程序。您还可以使用应用程序建立调试会话。Liberty 应用程序的开发方式相当于启用了调试和 jmx 应用程序管理实用程序。Node.js 应用程序的开发方式相当于启用了 *devconsole*、*inspector* 和 *shell* 实用程序。
