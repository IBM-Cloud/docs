---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-05"

---
{:new_window: target="blank"}
{:shortdesc: .shortdesc}



# {{site.data.keyword.objectstorageshort}} 入门  {: #getting-started-with-object-storage}


{{site.data.keyword.objectstoragefull}} 提供了非结构化云数据存储。您可以存储并访问内容，也可以通过交互方式编写内容并连接到应用程序和服务。
{: shortdesc}

{{site.data.keyword.objectstorageshort}} 服务的一些常见用例如下：

* 备份实例中的卷数据
* 传输大量数据时用作中间位置
* 在未直接连接的环境之间传输数据
* 充当中心存储库


{{site.data.keyword.Bluemix_notm}} Public {{site.data.keyword.objectstorageshort}} 为您提供了对完整供应的 Swift {{site.data.keyword.objectstorageshort}} 帐户的访问权，以用于管理您的数据。提供者端加密并未提供。


1.	从 {{site.data.keyword.Bluemix_notm}} 目录供应服务实例。配置实例并单击**创建**。如果对于**应用程序**字段，初始选择的是**保持未绑定**选项，那么以后仍可以将服务实例绑定到 {{site.data.keyword.Bluemix_notm}} 应用程序。
2. 在服务实例仪表板中，创建容器以开始存储对象。
3. 从**操作**下拉菜单中，将文件添加到容器。
4. 要测试对对象的访问权，请单击**下载**，然后查看文件。
5. 准备好将实例连接到应用程序后，设置服务凭证并[绑定服务](/docs/services/reqnsi.html#add_service)。



# 相关链接 
{: #rellinks}

## API 参考 
{: #api}
* [OpenStack {{site.data.keyword.objectstorageshort}} (Swift) API V1](http://developer.openstack.org/api-ref-objectstorage-v1.html){: new_window}
* [OpenStack Identity (Keystone) API V3.0](http://developer.openstack.org/api-ref-identity-v3.html){: new_window}

## SDK 
{: #sdk}
* [OpenStack Software Development Kits (SDK)](https://wiki.openstack.org/wiki/SDKs){: new_window}

## 教程和样本 
{: #samples}
* [使用 Java 连接到 IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/recipes/tutorials/connecting-to-ibm-object-storage-for-bluemix-with-java/){: new_window}
* [使用 Python 访问您的 {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.objectstorageshort}}](https://developer.ibm.com/recipes/tutorials/use-python-to-access-your-bluemix-object-storage/){: new_window}
* [通过 PHP 使用 {{site.data.keyword.objectstorageshort}}](https://developer.ibm.com/recipes/tutorials/use-php-to-leverage-object-storage-for-bluemix/){: new_window} 的功能

## 兼容运行时 
{: #buildpacks}
* [Liberty for Java](https://www.ng.bluemix.net/docs/runtimes/liberty/index.html){: new_window}
* [SDK for Node.js](https://www.ng.bluemix.net/docs/runtimes/nodejs/index.html){: new_window}
* [Go](https://www.ng.bluemix.net/docs/runtimes/go/index.html){: new_window}
* [PHP](https://www.ng.bluemix.net/docs/runtimes/php/index.html){: new_window}
* [Python](https://www.ng.bluemix.net/docs/runtimes/python/index.html){: new_window}
* [Ruby](https://www.ng.bluemix.net/docs/runtimes/ruby/index.html){: new_window}
* [社区 buildpack](https://www.ng.bluemix.net/docs/starters/byob.html){: new_window}


## 相关链接 
{: #general}
* [IBM {{site.data.keyword.Bluemix_notm}} 价格表](https://www.ng.bluemix.net/#/pricing){: new_window}
* [IBM {{site.data.keyword.Bluemix_notm}} 先决条件](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
