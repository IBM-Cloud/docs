---

copyright:
  years: 2015, 2017
lastupdated: "2016-07-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 在 {{site.data.keyword.GlobalizationPipeline_short}} 以外使用 {{site.data.keyword.Bluemix_notm}}
{: #globalizationpipeline_external}


许多 {{site.data.keyword.Bluemix_notm}} 服务（包括 {{site.data.keyword.GlobalizationPipeline_short}}）都可从内部部署应用程序托管环境使用，甚至可从其他云平台使用，而无需在 {{site.data.keyword.Bluemix_notm}} 上托管应用程序。
{:shortdesc}

要在 {{site.data.keyword.Bluemix_notm}} 以外使用 {{site.data.keyword.GlobalizationPipeline_short}}，请完成以下步骤：

1. 浏览至 {{site.data.keyword.Bluemix_notm}} 目录并从 **DevOps** 类别中选择 **{{site.data.keyword.GlobalizationPipeline_short}}** 服务。

2. 从 {{site.data.keyword.GlobalizationPipeline_short}} 服务目录页面中，填写必要信息。对于**连接至**字段，选择**保持未绑定**选项。

3. 单击**创建**，以向 {{site.data.keyword.Bluemix_notm}} 组织添加服务。系统会将您带到 {{site.data.keyword.GlobalizationPipeline_short}} 仪表板。

4. 从该仪表板中，单击**服务凭证**选项卡。  

**服务凭证**选项卡显示可用于该服务特定实例的所有凭证。使用这些凭证和所提供的服务 URL，您可以访问 {{site.data.keyword.GlobalizationPipeline_short}} API，并通过您的应用程序在任何托管环境中使用其功能。

要了解 {{site.data.keyword.GlobalizationPipeline_short}} RESTful API，请参阅 [API 参考](https://gp-rest.ng.bluemix.net/translate/swagger/index.html){: new_window}。
