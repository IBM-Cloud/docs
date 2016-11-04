---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 跨区域管理 {{site.data.keyword.objectstorageshort}} {: #multi-regions}
*上次更新时间：2016 年 10 月 19 日*
{: .last-updated}

{{site.data.keyword.objectstorageshort}} 服务支持达拉斯和伦敦存储区域。这两个存储区域独立于 {{site.data.keyword.Bluemix_notm}} 区域（例如，美国南部区域和英国），而 {{site.data.keyword.objectstorageshort}} 服务实例创建于该区域。如果在美国南部的 {{site.data.keyword.Bluemix_notm}} 区域中创建实例，那么可以读写达拉斯或伦敦存储区域的数据。
{: shortdesc}

对于美国南部的 {{site.data.keyword.Bluemix_notm}} 区域，“达拉斯”存储区域是缺省值。对于英国的 {{site.data.keyword.Bluemix_notm}} 区域，“伦敦”存储区域是缺省值。{{site.data.keyword.objectstorageshort}} 用户界面启动后始终会进入 {{site.data.keyword.Bluemix_notm}} 区域的缺省存储区域。要切换区域，请单击“{{site.data.keyword.objectstorageshort}} 区域”下拉列表，然后选择其他区域。

**注：**{{site.data.keyword.objectstorageshort}} 服务不支持跨存储区域复制。

### 多区域访问

要使用 {{site.data.keyword.objectstorageshort}} 服务，必须[向 OpenStack Keystone 认证](../ObjectStorage/os_security.html#keystone-authentication){: new_window}。认证成功后，响应中将可以使用 `X-Subject-Token` 和 {{site.data.keyword.objectstorageshort}} 端点。每个存储区域都有不同的[访问点](../ObjectStorage/os_api.html#access-points)。


例如，要在达拉斯存储区域中创建名为 `my_container` 的容器，请在 curl 命令中指定达拉斯访问点，如下所示：

  ```
  curl -i https://dal.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAABAABWlw4mwttbb_6G3LnTiGusyoOSEFMG7oTnDYWN1vBZB6XAxUEhe4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5L7lEZyyKQlsgmQWcrch9VOO_OiSKKToORZR7luI-2TrR_JIVZm-8AAS7hLhl9"
  ```
  {: pre}
您将收到以下输出内容：

  ```
  HTTP/1.1 201 Created
  Content-Length: 0
  Content-Type: text/html; charset=UTF-8
  X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
  Date: Thu, 14 Jan 2016 03:16:13 GMT
  ```
  {: screen}

要在“伦敦”存储区域中创建名为 `my_container` 的容器，请在 curl 命令中指定伦敦访问点，如下所示：

  ```
  curl -i https://lon.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAABAABWlw4mwttbb_6G3LnTiGusyoOSEFMG7oTnDYWN1vBZB6XAxUEhe4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5L7lEZyyKQlsgmQWcrch9VOO_OiSKKToORZR7luI-2TrR_JIVZm-8AAS7hLhl9"
  ```
  {: pre}
您将收到以下输出内容：

  ```
  HTTP/1.1 201 Created
  Content-Length: 0
  Content-Type: text/html; charset=UTF-8
  X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
  Date: Thu, 14 Jan 2016 03:16:13 GMT
  ```
  {: screen}

**注：**从 Keystone 获取的 `X-Subject-Token`（在示例中标注为 `X-Trans-ID`）在各存储区域中都有效。
