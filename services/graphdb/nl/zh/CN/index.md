---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.graphfull}} 入门
{: #gettingstartedtemplate}
上次更新时间： 2016年7月27日
{: .last-updated}

{{site.data.keyword.graphfull}} 是完全受管的图形数据库服务，可通过基于 REST 的 HTTP API 界面进行访问。使用它来构建需要图形数据库功能的移动和 Web 应用程序。
{:shortdesc}

{{site.data.keyword.graphfull}} 基于 [Apache TinkerPop](http://tinkerpop.incubator.apache.org/)&trade;
堆栈，用于构建使用可兼容 V3 的 API 的高性能图形应用程序。利用该堆栈，您可以在熟悉的环境中拥有更高的灵活性和更多功能。使用 {{site.data.keyword.Bluemix}} 仪表板，可以轻松将 {{site.data.keyword.graphfull}} 服务与 {{site.data.keyword.Bluemix_short}} 应用程序集成。

使用 {{site.data.keyword.graphfull}} 的方式有两种：

*	使用 {{site.data.keyword.graphfull}} 简化的 API 命令。
*	使用完整的 Apache TinkerPop V3 查询语言 (Gremlin)。

{{site.data.keyword.graphfull}} 功能使用 HTTP REST 端点以 API 形式提供。这些端点使用 HTTP 来生成 API 请求并获取结果，从而为应用程序提供了连接和使用 {{site.data.keyword.graphfull}} 服务的便捷方式。使用由所选应用程序编程语言提供的 HTTP 功能来访问端点。此外，还可以使用命令接口或 `curl` 脚本达到相同的效果。API 参考描述了 {{site.data.keyword.graphfull}} 服务所提供的各种功能，以及如何使用这些功能的示例。

您的应用程序还可以使用 Apache TinkerPop 查询语言（名为 Gremlin）来执行使用 {{site.data.keyword.graphfull}} 服务的任务。在 JSON 文档中包含 Gremlin 查询，然后将该文档传递到 `/gremlin` 服务端点。在完整文档中提供了关于如何将 Gremlin 用于 {{site.data.keyword.graphfull}} 的示例。

完成下列步骤以开始使用 {{site.data.keyword.graphfull}} 服务：

1.	为 {{site.data.keyword.graphfull}} 服务[创建实例](https://www.ng.bluemix.net/docs/services/reqnsi.html#req_instance)。
2.	记录在创建实例时生成的三个必要值。单击服务磁贴后，会在`服务凭证`选项卡上显示这些值。
	*	IBM Graph 端点：`apiURL`。
	*	服务实例用户名 `username`。
	*	服务实例密码 `password`。
3.	在应用程序或脚本中使用这三个必要值以执行 {{site.data.keyword.graphfull}} 任务。在完整文档中提供了示例。

# 相关链接
{: #rellinks}

## 教程和样本
{: #samples}

* [示例](https://ibm-graph-docs.ng.bluemix.net/examples.html){:new_window}

## API 参考
{: #api}

* [用于 IBM Graph 的 REST API](https://ibm-graph-docs.ng.bluemix.net/api.html){:new_window}
* [将 Gremlin 用于 IBM Graph](https://ibm-graph-docs.ng.bluemix.net/api.html#gremlin-apis){:new_window}

## 相关链接
{: #general}

* [完整文档](https://ibm-graph-docs.ng.bluemix.net/){:new_window}
* [Stack Overflow](http://stackoverflow.com/questions/tagged/ibm-graph){:new_window}
* [Apache Tinkerpop](http://tinkerpop.incubator.apache.org/){:new_window}
