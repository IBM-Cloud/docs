{:new_window: target="_blank"}

# {{site.data.keyword.objectstorageshort}} 疑難排解
{: #troubleshooting}

*前次更新：2016 年 8 月 17 日*
{: .last-updated}

以下是關於使用 {{site.data.keyword.objectstoragefull}} 的一般疑難排解問題的回答。

## 使用 openstack4J 搭配 Liberty 設定檔時傳回無法辨識的記號內容套件
{: #unrecognized_token}

### 症狀

使用 openstack4j 搭配 Liberity 設定檔時可能發生下列堆疊追蹤：

    Exception thrown by application class 'org.openstack4j.connectors.okhttp.HttpResponseImpl.readEntity:124'
    org.openstack4j.api.exceptions.ClientResponseException: Unrecognized token 'contentpack': was expecting ('true', 'false' or 'null') at [Source: contentpack ; line: 1, column: 12]
    at org.openstack4j.connectors.okhttp.HttpResponseImpl.readEntity(HttpResponseImpl.java:124)
    at org.openstack4j.core.transport.HttpEntityHandler.handle(HttpEntityHandler.java:56)
    at org.openstack4j.connectors.okhttp.HttpResponseImpl.getEntity(HttpResponseImpl.java:68)
    at org.openstack4j.openstack.internal.BaseOpenStackService$Invocation.execute(BaseOpenStackService.java:169)
    at org.openstack4j.openstack.internal.BaseOpenStackService$Invocation.execute(BaseOpenStackService.java:163)
    at org.openstack4j.openstack.storage.object.internal.ObjectStorageContainerServiceImpl.list(ObjectStorageContainerServiceImpl.java:41)
    at com.mimotic.SecureMessageApp.HelloResource.getInformation(HelloResource.java:47)
    at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
    at sun.reflect.NativeMethodAccessorImpl.invoke(Unknown Source)
    at sun.reflect.DelegatingMethodAccessorImpl.invoke(Unknown Source)
    at java.lang.reflect.Method.invoke(Unknown Source)

### 解決方案

此問題起因為類別載入問題，其中 openstack4j 程式庫包含 Liberty 設定檔所提供的部分相同套件。例如，OpenStack4j 使用 JERSEY，這可能會與 Wink 程式庫衝突。

若要解決此問題，請遵循下列步驟：

1. 使用反向類別載入 (parentLast)。
2. 從已啟用的特性排除 jaxrs。

## 取得 {{site.data.keyword.objectstorageshort}} 的協助及支援
{: #gettinghelp}

如果您在使用 {{site.data.keyword.objectstoragefull}} 時有任何問題，則可以搜尋資訊或透過討論區提出問題來取得協助。您也可以開啟支援問題單。

使用討論區提出問題時，請標記您的問題，讓 {{site.data.keyword.Bluemix_notm}} 開發團隊可以看到它。

* 如果您有關於 {{site.data.keyword.objectstorageshort}} 的技術問題，請在 [Stack Overflow](http://stackoverflow.com/search?q=object-storage+ibm-bluemix){:new_window} 上張貼您的問題，並使用 "ibm-bluemix" 及 "object-storage" 來標記您的問題。
<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->
* 若為關於服務及開始使用指示的問題，請使用 [IBM developerWorks dW Answers](https://developer.ibm.com/answers/topics/object-storage/?smartspace=bluemix){:new_window} 討論區。請包括 "object-storage" 及 "bluemix" 標籤。

如需使用討論區的詳細資料，請參閱[取得協助](https://console.ng.bluemix.net/docs/support/index.html#getting-help)。

如需開啟 IBM 支援問題單的相關資訊，或支援層次與問題單嚴重性的相關資訊，請參閱[聯絡支援中心](https://console.ng.bluemix.net/docs/support/index.html#contacting-support)。
