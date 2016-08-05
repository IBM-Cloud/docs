{:new_window: target="_blank"}

# {{site.data.keyword.objectstorageshort}} 疑難排解
{: #troubleshooting}

*前次更新：2016 年 6 月 24 日*
{: .last-updated}

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
