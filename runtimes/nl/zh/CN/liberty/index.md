---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Liberty for Java
{: #liberty_runtime}

*上次更新时间：2016 年 3 月 23 日*

{{site.data.keyword.Bluemix}} 上的 Liberty for Java 应用程序由 liberty-for-java buildpack 提供技术支持。liberty-for-java buildpack 为基于 Liberty 概要文件运行 Java EE 7 和 OSGi 应用程序提供了完整的运行时环境。它支持 Spring 等流行框架，并包含 IBM JRE。WebSphere Liberty 支持非常适合云的快速应用程序开发。
{: shortdesc}

## 检测
{: #detection}
部署以下类型的应用程序时，将使用 Liberty buildpack：
* [WAR 文件](optionsForPushing.html#stand_alone_apps)
* [EAR 文件](optionsForPushing.html#stand_alone_apps)
* [Liberty 服务器目录](optionsForPushing.html#server_directory)
* [Liberty 打包服务器](optionsForPushing.html#packaged_server)
* Java main
* [Distzip](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/container-distZip.md)

## 入门模板应用程序
{: #starter_application}
{{site.data.keyword.Bluemix}} 提供了几种 Liberty 入门模板应用程序。Liberty 入门模板应用程序是为您提供可使用模板的简单 Liberty 应用程序。您可以体验该入门模板应用程序，对其进行更改并将更改推送到 Bluemix 环境。有关使用入门模板应用程序的帮助，请参阅[使用入门模板应用程序](../../cfapps/starter_app_usage.html)。

# 相关链接
## 常规
* [Liberty 概要文件概述](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
* [管理 Liberty 应用程序](../../manageapps/app_mng.html#Utilities)
* [使用 IBM Eclipse Tools for Bluemix 部署应用程序](../../manageapps/eclipsetools/eclipsetools.html#eclipsetools)
* [IBM Monitoring and Analytics for Bluemix 服务入门](../../services/monana/index.html#monana_oview)
## 样本
* [Cloud Foundry Architecture Labs](https://developer.ibm.com/bluemix/docs/category/cloud-foundry-docs/)
