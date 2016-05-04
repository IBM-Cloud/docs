---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# buildpack 缺省值
{: #buildpack_defauts}

*上次更新时间：2016 年 3 月 23 日*

Liberty buildpack 在 Bluemix 中会频繁更新。每个发行版都可能包含安全修订或增强功能。

对于 WAR 或 EAR 应用程序的 Java 版本或 Liberty 功能集等设置，buildpack 具有缺省值。其中一些缺省值可能会在不同 buildpack 发行版中有所更改，这可能会对应用程序产生不利影响。要阻止应用程序受 buildpack 缺省值更改的影响，请执行步骤来配置应用程序，以避免应用程序依赖 buildpack 缺省值。

## Liberty 功能
{: #liberty_features}

部署 WAR 或 EAR 文件时，buildpack 会为具有缺省 Liberty 功能集的应用程序提供配置。缺省 Liberty 功能集可能会在不同 buildpack 发行版中有所更改，尽管此情况很少发生。缺省功能集的更改可能会对应用程序产生不利影响。有一些选项可确保应用程序不受功能缺省值更改的影响。

* 设置 JBP_CONFIG_LIBERTY 环境变量以显式指定对应用程序启用的功能的列表。有关更多信息，请参阅[独立应用程序](optionsForPushing.html#stand_alone_apps)。
* 将应用程序部署为[服务器目录](optionsForPushing.html#server_directory)或[打包服务器](optionsForPushing.html#packaged_server)。提供定制 server.xml 文件，以指定应用程序需要的准确功能集。

部署为服务器目录或打包服务器的应用程序不受 Liberty 功能缺省值更改的影响。

## Java 版本
{: #java_version}

buildpack 为应用程序提供了缺省 JRE。JRE 的主版本或次版本可能会在不同 buildpack 发行版中有所更改。JRE 次版本可能会频繁更新，而主版本很少更新。JRE 主版本的更改可能会对应用程序产生不利影响。

要确保应用程序不受主版本更改的影响，请如[定制 JRE](customizingJRE.html) 中所述，使用相应的 JRE 版本设置环境变量。为了获得最佳结果，请对应用程序采用 Java 8。

# 相关链接
## 常规
* [Liberty 运行时](index.html)
* [Liberty 概要文件概述](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
