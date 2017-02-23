---

copyright:
  years: 2016, 2017
lastupdated: "2016-09-14"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 应用程序连接

要将应用程序连接到 {{site.data.keyword.iot_full}}，必须通过使用 API 密钥和令牌或在 {{site.data.keyword.Bluemix_notm}} 中将应用程序直接绑定到 {{site.data.keyword.iot_short_notm}} 进行连接。使用访问仪表板授予访问权。
{:shortdesc}

## API 密钥连接
{: #api-key}
将应用程序连接到 {{site.data.keyword.iot_short_notm}} 组织时，会使用 API 密钥。应用程序需要用于连接到组织的 API 密钥以及必须与该 API 密钥配合使用的唯一认证令牌。  

有关应用程序连接的更多信息，请参阅开发者文档中的[应用程序的 MQTT 连接](https://docs.internetofthings.ibmcloud.com/applications/mqtt.html)。


要创建新的 API 密钥和认证令牌对，请执行以下操作：  
1.	在 {{site.data.keyword.iot_short_notm}} 仪表板中，转至**应用程序 > API 密钥**。  
2.	单击**生成 API 密钥**。
  
**重要信息：**记录 API 密钥和令牌对。认证令牌是不可恢复的。如果丢失或忘记此令牌，需要重新注册 API 密钥以生成新的认证令牌。
 - API 密钥示例为 `a-organization_id-a84ps90Ajs`  
 - 令牌示例为 `MP$08VKz!8rXwnR-Q*`  
3.	添加注释以在仪表板中标识 API 密钥，例如：用于连接我的应用程序的密钥。
4.	单击**完成**。



## Bluemix 绑定连接
{: #bluemix-binding}
可以从 {{site.data.keyword.Bluemix_notm}} 将应用程序绑定到 {{site.data.keyword.iot_short_notm}} 组织。应用程序在绑定后，仅可与相同空间或组织中的服务实例通信。您可以在 VCAP_SERVICES 环境变量中找到应用程序与服务实例进行通信时所需的所有数据。如果应用程序与多个服务绑定，那么 VCAP_SERVICES 变量会包含每个服务实例的连接信息。  

不过，也可以按照与外部应用程序相同的方式使用其他空间或组织中的服务实例。不要创建绑定，请改用凭证来直接配置应用程序实例。有关更多信息，请参阅 {{site.data.keyword.Bluemix_notm}} 文档中的[请求新服务实例](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)。

要查看绑定到您组织所关联的 Bluemix 服务实例的 Bluemix 应用程序的详细信息，请转至**应用程序 > Bluemix 应用程序**。  
