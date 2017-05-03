---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# IBM Bluemix Runtime for Swift
{: #swift_runtime}

{{site.data.keyword.Bluemix}} 上的 Runtime for Swift 由 [IBM Bluemix buildpack for Swift](https://github.com/IBM-Swift/swift-buildpack)（即 swift_buildpack）提供技术支持。此 buildpack 为 Swift 应用程序提供完整的运行时环境。
{: shortdesc}

## 入门模板应用程序
{: #starter_application}

{{site.data.keyword.Bluemix}} 提供了基于 Kitura 的 Swift [入门模板应用程序](https://github.com/IBM-Bluemix/Kitura-Starter)。Kitura 入门模板应用程序是一个简单的 Swift 应用程序，可以用于了解可使用 Swift 编程语言开发的服务器应用程序的类型。此样本应用程序会创建向客户机返回 HTML 内容的基本 Kitura HTTP 服务器。

**注：**Kitura 入门模板应用程序旨在用于培训。您可以尝试使用该入门模板应用程序进行改进，并将更改推送到 {{site.data.keyword.Bluemix}} 环境。有关使用入门模板应用程序的帮助，请参阅[使用入门模板应用程序](../../cfapps/starter_app_usage.html)。

## 重命名应用程序
{: #renaming_your_app}

如果想要重命名应用程序，您可以从“Kitura 入门模板”进行，或者通常需要进行一些更改。这样既可避免混淆，也可确保部署不会发生错误。

- 重命名应用程序的项目文件夹，以匹配应用程序的名称。
- `Package.swift` - 更改以下条目：
    - `name` - 应匹配应用程序的名称。
    - `targets[Target(name:)]` - 应匹配应用程序的名称。
- `manifest.yml` - 更改以下条目：
    - `name` - 应匹配应用程序的名称。
    - `command` - 用于启动应用程序的可执行文件的名称（应该与 Package.swift 文件中指定的名称相匹配）。

## 运行时版本
{: #runtime_versions}

缺省情况下，{{site.data.keyword.Bluemix}} 上托管的 Runtime for Swift (swift_buildpack) 使用 Swift 二进制的最新 GA 版本。这是 IBM 直接支持的唯一 Swift 版本，建议在您的应用程序中使用该版本。您可以通过查看 swift_buildpack 的[最新发行版信息](https://github.com/IBM-Swift/swift-buildpack/releases)来确定这个受支持的版本。buildpack 可能会在其 [manifest.yml](https://github.com/IBM-Swift/swift-buildpack/blob/master/manifest.yml) 文件中列出其他 Swift 版本。buildpack 中预先高速缓存了这些常见但不受支持的 Swift 版本，以减少供应时间。

如果希望您的应用程序在 {{site.data.keyword.Bluemix}} 上使用其他 Swift 版本，您可以在存储库根目录中的 `.swift-version` 文件中指定版本。此 `.swift-version` 文件定义 swift_buildpack 要使用的 Swift 版本。

```
$ cat .swift-version
3.0
```
{: pre}

由于 Swift 语言更新频繁，因此应该始终包含 `.swift-version` 文件，以便应用程序“锁定”到应用程序已知使用的 Swift 版本。

请注意，您可以在 `.swift-version` 文件中指定任何有效的 Swift 版本。这些备用版本必须与 [Swift.org ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://swift.org/download/) 的命名匹配，并直接从中拉出。由于使用非高速缓存版本将耗费更长时间才能供应，因此对于 Swift 应用程序而言没有任何运行时性能差异。

如果应用程序的根目录中包含 `Package.swift` 文件，那么将使用 {{site.data.keyword.Bluemix}} 中的缺省 swift_buildpack。如果希望使用备用 buildpack，那么必须将 `buildpack: {buildpackUrl}` 条目添加到应用程序的 manifest.yml 文件中，以指定此版本。或者，您可以在部署时使用 `cf push -b {buildpackUrl}` 命令自变量来定义此项。


## 开发者环境

开发者在使用 Swift 创建服务器端的应用程序时可进行几种选择。使用 Apple 的 MacOS 设备的开发者可能偏向使用 Xcode IDE，虽然并非必需。{{site.data.keyword.Bluemix}} 上将部署并运行的基于 Swift 的应用程序可以使用任何编程编辑器或 IDE。很多常见的编辑器都可以使用 Swift 的语法突出显示功能。[Swift.org ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://swift.org/) 的二进制文件中包含的 Swift REPL 命令行工具支持在部署到 {{site.data.keyword.Bluemix}} 之前进行本地编译和测试。

对于 MaxOS 用户，您可以使用 [IBM Cloud Tools for Swift](http://cloudtools.bluemix.net/)，其简化了 {{site.data.keyword.Bluemix}} 上运行的服务器端 Swift 应用程序的创建、部署、管理和控制过程。  


## 增强的集成

[Kitura Web 框架](http://ibm-swift.github.io/Kitura/)提供了很多功能。Kitura 本质上进行了模块化，您很快会想要使用打包的 SDK 扩展其功能，以提供诸如认证、访问基于 Watson 的服务以及支持各种数据库等功能。Kitura 直接提供对很多数据库的支持，而其他开放式源代码项目还会为很多数据库平台提供 SDK。下面列出了 Kitura 提供的可使用外部资源的非完全 SDK 列表。

- [IBM Watson](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/swift-watson-sdk)
- [IBM DB2 和 DashDB](https://swiftpkgs.ng.bluemix.net/package/IBM-DTeam/swift-for-db2)
- [IBM Cloudant 和 CouchDB](https://swiftpkgs.ng.bluemix.net/package/cloudant/swift-cloudant)
- [IBM ObjectStorage](https://swiftpkgs.ng.bluemix.net/package/ibm-bluemix-mobile-services/bluemix-objectstorage-serversdk-swift)
- [Apache Cassandra](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Kassandra)
- [Aphid MQTT](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Aphid)

要查找更多 Swift 软件包以包含到应用程序中，请转至 [IBM Swift 软件包目录](https://swiftpkgs.ng.bluemix.net/)，并针对您的目标服务或数据库执行搜索。使用“软件包目录”可轻松找到 Swift 应用程序中可包含的软件包。通过将软件包的 Git URL 和版本详细信息包含到应用程序的 `Package.swift` 文件中，即可将软件包添加到 Swift 应用程序中。有关管理软件包的更多详细信息，请参阅 [Swift.org 的软件包管理器部分](https://swift.org/package-manager/)。


## 相关信息

IBM 还为 Swift 开发者提供了其他在线工具。
- [IBM Swift DevCenter](https://developer.ibm.com/swift/) - 所有 IBM Swift 信息的主要登录站点。您可以找到有关我们的产品、博客、社交事件、文档等信息。
- [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/) - 此站点为您提供一个环境，用于针对多种 Swift 版本甚至不同的 Swift 运行时平台，轻松快速地测试出 Swift 代码片段。您还可以保存代码样本并与他人共享，以及浏览他人提供的常见示例。


# 相关链接
{: #rellinks notoc}
## 常规
{: #general notoc}
* [IBM Swift DevCenter](https://developer.ibm.com/swift/)
* [IBM Cloud Tools for Swift](http://cloudtools.bluemix.net/)
* [IBM Swift 软件包目录](https://swiftpkgs.ng.bluemix.net/)
* [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/)
* [Kitura 文档和 API](http://ibm-swift.github.io/Kitura/)
* [Bluemix 的 Kitura 入门模板应用程序](https://github.com/IBM-Bluemix/Kitura-Starter)
* [IBM Bluemix buildpack for Swift](https://github.com/IBM-Swift/swift-buildpack)
* [IBM Bluemix buildpack for Swift 发行说明](https://github.com/IBM-Swift/swift-buildpack/releases)
* [Swift.org ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://swift.org/)
* [Swift 语言文档 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://swift.org/documentation)
