---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 跨地區管理 {{site.data.keyword.objectstorageshort}} {: #multi-regions}
*前次更新：2016 年 10 月 19 日*
{: .last-updated}

{{site.data.keyword.objectstorageshort}} 服務支援達拉斯及倫敦儲存空間地區。這些儲存空間地區與在其中建立 {{site.data.keyword.objectstorageshort}} 服務實例的 {{site.data.keyword.Bluemix_notm}} 地區（例如美國南部及英國）無關。如果您在美國南部的 {{site.data.keyword.Bluemix_notm}} 地區建立實例，則可以在達拉斯或倫敦儲存空間地區讀取及寫入資料。
{: shortdesc}

對於美國南部的 {{site.data.keyword.Bluemix_notm}} 地區，達拉斯儲存空間地區是預設值。對於英國的 {{site.data.keyword.Bluemix_notm}} 地區，倫敦儲存空間地區是預設值。{{site.data.keyword.objectstorageshort}} 使用者介面一律會啟動至 {{site.data.keyword.Bluemix_notm}} 地區的預設儲存空間地區。若要切換地區，請按一下「{{site.data.keyword.objectstorageshort}} 地區」下拉清單，然後選擇其他地區。

**附註：**{{site.data.keyword.objectstorageshort}} 服務不支援跨儲存空間地區抄寫。

### 多個地區存取

若要使用 {{site.data.keyword.objectstorageshort}} 服務，您必須[鑑別 OpenStack Keystone](../ObjectStorage/os_security.html#keystone-authentication){: new_window}。順利鑑別之後，即會在回應中提供 `X-Subject-Token` 及 {{site.data.keyword.objectstorageshort}} 端點。每一個儲存空間地區都會有不同的[存取點](../ObjectStorage/os_api.html#access-points)。


例如，若要在達拉斯儲存空間地區建立名為 `my_container` 的容器，請在 curl 指令中指定達拉斯存取點，如下所示：

  ```
  curl -i https://dal.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAABAABWlw4mwttbb_6G3LnTiGusyoOSEFMG7oTnDYWN1vBZB6XAxUEhe4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5L7lEZyyKQlsgmQWcrch9VOO_OiSKKToORZR7luI-2TrR_JIVZm-8AAS7hLhl9"
  ```
  {: pre}
您將會收到下列輸出：

  ```
  HTTP/1.1 201 Created
  Content-Length: 0
  Content-Type: text/html; charset=UTF-8
  X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
  Date: Thu, 14 Jan 2016 03:16:13 GMT
  ```
  {: screen}

若要在倫敦儲存空間地區建立名為 `my_container` 的容器，請在 curl 指令中指定倫敦存取點，如下所示：

  ```
  curl -i https://lon.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAABAABWlw4mwttbb_6G3LnTiGusyoOSEFMG7oTnDYWN1vBZB6XAxUEhe4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5L7lEZyyKQlsgmQWcrch9VOO_OiSKKToORZR7luI-2TrR_JIVZm-8AAS7hLhl9"
  ```
  {: pre}
您將會收到下列輸出：

  ```
  HTTP/1.1 201 Created
  Content-Length: 0
  Content-Type: text/html; charset=UTF-8
  X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
  Date: Thu, 14 Jan 2016 03:16:13 GMT
  ```
  {: screen}

**附註：**從 Keystone 獲得的 `X-Subject-Token`（在範例中標示為 `X-Trans-ID`）可以跨儲存空間地區運作。
