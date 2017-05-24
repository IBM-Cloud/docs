---

copyright:
  years: 2016, 2017
lastupdated: "2016-11-29"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 确保定制卡服务器的安全
{: #securing_custom_cards}

定制卡服务器是标准 Web 服务器，用于托管定制卡 JavaScript 代码。要确保 {{site.data.keyword.iot_short_notm}} 环境的完整性，您应该如本主题中所述，通过采取步骤确保卡源安全，从而确保定制卡服务器的安全。
{:shortdesc}

**重要信息：**目前，定制卡是作为试验性功能提供的，并且针对每个浏览器会话启用了定制卡扩展。定制卡连接配置和卡软件包不会在 {{site.data.keyword.iot_short_notm}} 组织中全局共享。

## {{site.data.keyword.Bluemix_notm}} 角色需求
{: #roles_requirements}

您必须具有 {{site.data.keyword.iot_short_notm}} 管理员权限才可创建定制卡服务器连接。

## 定制卡服务器安全性注意事项
{: #server_requirements}

以下需求通过 {{site.data.keyword.iot_short_notm}} 进行设置：
- 服务器上提供定制卡内容的目录必须无需凭证即可访问。  
连接以访问并装入定制卡时，不会向定制卡服务器提供任何认证。
- 服务器必须使用 HTTP 安全 (HTTPS) 协议。
- 服务器必须支持跨源资源共享 (CORS) 连接。  

要保护定制卡代码和卡服务器本身，使用深度防御来定位卡服务器并确保其安全。这包括防火墙保护，以限制对定制卡服务器的访问。

定制卡处理始终位于用户浏览器和定制卡服务器之间。{{site.data.keyword.iot_short_notm}} 后端永远不会参与处理或调整定制卡信息和代码。

对于选择在定制卡服务器上的卡中部署的 JavaScript 代码，没有任何限制。定制卡中的 JavaScript 代码有权访问浏览器中保存的所有信息，就像在仪表板中运行的其他任何卡一样。确保正确的定制卡服务器在向浏览器提供代码，以用于显示和处理定制卡。

卡在您的 {{site.data.keyword.iot_short_notm}} 浏览器会话中执行其代码，完全如编写的那样。此外，在创建定制卡服务器连接时，不会向定制卡服务器提供任何凭证。用户的浏览器可以连接到任何配置的定制卡服务器。

仅配置已知且安全的定制卡服务器来向用户仪表板提供定制卡，这一点非常重要。   
