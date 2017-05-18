---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-13"

---

<!-- Attribute definitions -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 开发针对 {{site.data.keyword.streaminganalyticsshort}} 的 Python 应用程序
{: #t_develop_apps_python}

现在可以在 IBM Data Science Experience (DSX) 或在本地 Python 开发环境中开发 Python 应用程序，并在 {{site.data.keyword.streaminganalyticsshort}} 中部署这些应用程序。
{:shortdesc}

开发 Python 应用程序，并通过 {{site.data.keyword.streaminganalyticsshort}} 服务使用以下某种方法将其部署到 {{site.data.keyword.Bluemix_short}} 云：


## 在 DSX 中开发 Streams Python 应用程序
{: #t_develop_python_dsx}

如果没有 Python 开发环境，那么最简单的入门方法是使用 DSX 中的配置页，针对 {{site.data.keyword.streaminganalyticsshort}} 服务创建样本 Python 应用程序。这些配置页中提供了步骤和代码样本，可用于在 DSX Python 环境中针对 {{site.data.keyword.streaminganalyticsshort}} 服务创建和部署简单的 Python 应用程序：

* [Hello World!](https://apsportal.ibm.com/exchange/public/entry/view/9fc33ce7301f10e21a9f92039ca9c6e8)：创建简单的 Hello World! 应用程序以便于入门，然后将应用程序部署到 {{site.data.keyword.streaminganalyticsshort}} 服务的实例。

* [Healthcare Demo](https://apsportal.ibm.com/exchange/public/entry/view/9fc33ce7301f10e21a9f92039cad29a6)：创建可摄入并分析来自订阅源的流式数据的应用程序，然后在配置页中实现这些数据的可视化。最终将此应用程序提交给 {{site.data.keyword.streaminganalyticsshort}} 服务实例。

* [Neural Net Demo](https://apsportal.ibm.com/exchange/public/entry/view/9fc33ce7301f10e21a9f92039ca60bb7)：创建样本数据集，创建样本数据的模型，在流式应用程序中使用该模型，实现流式数据的可视化，最终将该流式应用程序提交给 {{site.data.keyword.streaminganalyticsshort}} 服务。

## 在本地 Python 环境中开发应用程序
 {: #t_develop_python_api}

 streamsx 程序包中随附的 [{{site.data.keyword.streamsshort}} Python 应用程序 API](http://ibmstreams.github.io/streamsx.documentation/docs/python/python-appapi-devguide/#50-api-features) 支持使用 Python 可调用类或函数来创建流处理应用程序。然后使用 Python 应用程序 API 来定义应用程序并将应用程序提交给服务。

按照[针对 {{site.data.keyword.streaminganalyticsshort}} 服务进行开发](http://ibmstreams.github.io/streamsx.documentation/docs/python/1.6/python-appapi-devguide-2a/index.html)教程中的步骤开始在本地 Python 环境中创建样本应用程序，并将其部署到 {{site.data.keyword.streaminganalyticsshort}} 服务。
