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

# {{site.data.keyword.objectstorageshort}} 故障诊断
{: #troubleshooting}


下面是有关使用 {{site.data.keyword.objectstoragefull}} 的常见故障诊断问题的答案。
{: shortdesc}

## 使用 openstack4J 与 Liberty 概要文件时返回无法识别的令牌内容套件
{: #unrecognized_token}


使用 openstack4j 与 Liberty 概要文件时可能会发生以下堆栈跟踪：
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


此问题源自类装入问题，openstack4j 库包含 Liberty 概要文件提供的一些相同的软件包。例如，OpenStack4j 使用 JERSEY，其可能与 Wink 库发生冲突。
{: tsCauses}


可以通过以下方式解决此问题：
{: tsResolve}
  * 使用反向类装入 (parentLast)。
  * 从已启用的功能中排除 jaxrs。


## 获取 {{site.data.keyword.objectstorageshort}} 的帮助和支持
{: #gettinghelp}

如果您在使用 {{site.data.keyword.objectstoragefull}} 时有任何疑问或遇到任何问题，您可以在论坛中搜索相关信息或进行提问来获取帮助。还可以提交支持凭单。

使用论坛进行提问时，请使用适当的标记来标注您的问题，以方便 {{site.data.keyword.Bluemix_notm}} 开发团队识别。

* 如果您有关于 {{site.data.keyword.objectstorageshort}} 的技术问题，请将问题发布到 <a href="http://stackoverflow.com/search?q=object-storage+ibm-bluemix" target="_blank">Stack Overflow <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>，并用“ibm-bluemix”和“object-storage”标记您的问题。
* 有关服务的问题和入门指示信息，请使用 <a href="https://developer.ibm.com/answers/topics/objectstorage/?smartspace=bluemix" target="_blank">IBM developerWorks dW Answers <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a> 论坛。请加上“objectstorage”和“bluemix”标记。

有关使用论坛的更多详细信息，请参阅[获取帮助](/docs/support/index.html#getting-help)。

有关提交 IBM 支持凭单或支持级别和凭单严重性的信息，请参阅[联系支持人员](/docs/support/index.html#contacting-support)。
