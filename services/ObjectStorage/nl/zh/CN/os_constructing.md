---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 构造 {{site.data.keyword.objectstorageshort}} URL 以使用 Swift REST API

您可以通过命令行客户机接口（例如，cURL）来使用 Swift REST API，也可以通过应用程序来调用该 API。
{: shortdesc}


有关 {{site.data.keyword.objectstorageshort}} REST API 选项和示例的完整列表，请参阅 [OpenStack Swift API Complete Reference](http://developer.openstack.org/api-ref-objectstorage-v1.html)。

必须先使用 Keystone [认证](/docs/services/ObjectStorage/os_authenticate.html)您的服务实例，然后才能编写 URL。请确保记下目录响应。该响应类似于以下示例。

```
{
  "id" : "4207049680fa4effbecd044c7448a8cb",
  "region" : "dallas",
  "region_id" : "dallas",
  "url" : "https://dal.objectstorage.open.softlayer.com/v1/AUTH_4abf7d7bac2c4eda89c03dd3afa7a0a3",
  "interface" : "public"
},
```
{: codeblock}


将容器和对象的名称空间添加到 {{site.data.keyword.objectstorageshort}} URL 的末尾，如下图中所示。

![示例图像中显示的 {{site.data.keyword.objectstorageshort}} URL 部分](images/Swift_URL.png)

图 1. {{site.data.keyword.objectstorageshort}} URL 示例
