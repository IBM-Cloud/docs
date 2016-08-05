{:new_window: target="_blank"}

# {{site.data.keyword.objectstorageshort}} 故障诊断
{: #troubleshooting}

*上次更新时间：2016 年 6 月 24 日*
{: .last-updated}

## 使用 openstack4J 与 Liberty 概要文件时返回无法识别的令牌内容套件
{: #unrecognized_token}

### 故障现象

使用 openstack4j 与 Liberity 概要文件时可能会发生以下堆栈跟踪：

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

### 解决方案

此问题源自类装入问题，openstack4j 库包含 Liberty 概要文件提供的一些相同的软件包。例如，OpenStack4j 使用 JERSEY，其可能与 Wink 库发生冲突。

要解决此问题，请执行以下步骤：

1. 使用反向类装入 (parentLast)。
2. 从启用的功能中排除 jaxrs。
