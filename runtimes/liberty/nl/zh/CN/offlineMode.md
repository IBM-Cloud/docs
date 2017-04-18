---

copyright:
  years: 2016
lastupdated: "2016-11-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Liberty 的脱机方式
{: #offline_mode}

将 Liberty 应用程序推送到 {{site.data.keyword.Bluemix}} 后，Liberty buildpack 就可以访问 Bluemix 外部站点来获取应用程序所需的工件。下面是 Liberty buildpack 可以访问的外部站点。在 [Bluemix Dedicated](/docs/dedicated/index.html#dedicated) 和 [Bluemix Local](/docs/local/index.html#local) 环境中，可能需要将这些站点*列入白名单*。

* https://download.run.pivotal.io 和 https://java-buildpack.cloudfoundry.org，用于访问以下产品的组件：
  * [AppDynamics 代理程序](https://www.appdynamics.com/)
  * [MariaDB JDBC 驱动程序](https://mariadb.com/)
  * [New Relic 代理程序](newRelic.html)
  * [OpenJDK](customizingJRE.html#OpenJDK)
  * [PostgreSQL JDBC 驱动程序](https://www.postgresql.org)
* https://dl.zeroturnaround.com/jrebel/，用于访问 [JRebel](https://zeroturnaround.com/software/jrebel/) 的组件。
* https://download.ruxit.com/agent/paas/cloudfoundry/java，用于访问 [Dynatrace Ruxit 代理程序](dynatrace.html)的组件。
* http://downloads.dynatracesaas.com/cloudfoundry/buildpack/java/，用于访问 [Dynatrace 代理程序](dynatrace.html)。

## 使用代理
{: #working_with_proxy}

在某些环境（如 [Bluemix Dedicated](/docs/dedicated/index.html#dedicated) 和 [Bluemix Local](/docs/local/index.html#local)）中，可以配置代理。有关更多详细信息，请参阅[使用代理](/docs/manageapps/workingWithProxy.html)。

# 相关链接
{: #rellinks}
## 常规
{: #general}
* [Liberty 运行时](index.html)
* [Liberty 概要文件概述](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
