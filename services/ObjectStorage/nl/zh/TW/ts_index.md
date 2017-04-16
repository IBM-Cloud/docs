---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}

# {{site.data.keyword.objectstorageshort}} 疑難排解
{: #troubleshooting}


以下是關於使用 {{site.data.keyword.objectstoragefull}} 的一般疑難排解問題的回答。
{: shortdesc}

## 使用 openstack4J 搭配 Liberty 設定檔時傳回無法辨識的記號內容套件
{: #unrecognized_token}


搭配使用 openstack4j 與「Liberty 設定檔」時可能發生下列堆疊追蹤：
```
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
```
{: screen}
{: tsSymptoms}


此問題起因為類別載入問題，其中 openstack4j 程式庫包含 Liberty 設定檔所提供的部分相同套件。例如，OpenStack4j 使用 JERSEY，這可能會與 Wink 程式庫衝突。
{: tsCauses}


您可以透過下列方式來修正此問題：
{: tsResolve}
  * 使用反向類別載入 (parentLast)。
  * 從已啟用的特性中排除 jaxrs。


## 取得 {{site.data.keyword.objectstorageshort}} 的協助及支援
{: #gettinghelp}

如果您使用 {{site.data.keyword.objectstoragefull}} 時有問題或疑問，可以搜尋資訊或透過討論區提問來取得協助。您也可以開啟支援問題單。

使用討論區提問時，請標記您的問題，以便 {{site.data.keyword.Bluemix_notm}} 開發團隊能看到它。

* 如果您有 {{site.data.keyword.objectstorageshort}} 的相關技術問題，請將問題張貼到 <a href="http://stackoverflow.com/search?q=object-storage+ibm-bluemix" target="_blank">Stack Overflow <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> ，並使用 "ibm-bluemix" 及 "object-storage" 來標記您的問題。
* 若是服務及開始使用指示的相關問題，請使用 <a href="https://developer.ibm.com/answers/topics/objectstorage/?smartspace=bluemix" target="_blank">IBM developerWorks dW Answers <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a> 討論區。請包含 "objectstorage" 及 "bluemix" 標籤。

如需使用討論區的詳細資料，請參閱[取得協助](/docs/support/index.html#getting-help)。

如需開啟 IBM 支援問題單的相關資訊，或支援層次與問題單嚴重性的相關資訊，請參閱[與支援中心聯絡](/docs/support/index.html#contacting-support)。
