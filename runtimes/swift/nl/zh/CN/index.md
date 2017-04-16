{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .pre}


# IBM Bluemix Runtime for Swift
{: #swift_runtime}
上次更新时间：2016 年 9 月 19 日
{: .last-updated}

Runtime for Swift on {{site.data.keyword.Bluemix}} 由 [IBM Bluemix buildpack for Swift](https://github.com/IBM-Swift/swift-buildpack)（即 swift_buildpack）提供支持。
此 buildpack 为 Swift 应用程序提供完整的运行时环境。
{: shortdesc}

## 入门模板应用程序
{: #starter_application}

{{site.data.keyword.Bluemix}} 提供基于 Kitura 的 Swift [入门模板应用程序](https://github.com/IBM-Swift/Kitura-Starter-Bluemix)。Kitura 入门模板应用程序是简单的 Swift 应用程序，您可用于了解可使用 Swift 编程语言部署的服务器应用程序的类型。此样本应用程序可创建基本 Kitura HTTP 服务器，将 HTML 内容返回给客户端。

**注：**Kitura 入门模板应用程序旨在用于教育目的。您可以通过执行增强功能，来尝试使用该入门模板应用程序，并将这些更改推送至 {{site.data.keyword.Bluemix}} 环境。请参阅[使用入门模板应用程序](../../cfapps/starter_app_usage.html)，以获取使用入门模板应用程序的帮助。

## 重命名应用程序
{: #renaming_your_app}

如果您想要重命名应用程序，那么可以通过 Kitura Starter，或者一般来说，需要进行几处更改。这两种作法都可避免产生混淆，并确保无错部署。

- 重命名应用程序的项目文件夹以与应用程序的名称相匹配。
- `Package.swift` - 更改以下条目：
    - `name` - 应该与应用程序的名称相匹配
    - `targets[Target(name:)]` - 应该与应用程序的名称相匹配
- `manifest.yml` - 更改以下条目：
    - `name` - 应该与应用程序的名称相匹配
    - `host` - 代表应用程序 URL 的主要主机分段
- `Procfile` - `web` 的值应该与应用程序的目录名称相匹配。这是在编译之后运行的命令，以启动 Web 应用程序。


## 运行时版本
{: #runtime_versions}

缺省情况下，在 {{site.data.keyword.Bluemix}} 上托管的 Runtime for Swift (swift_buildpack) 会使用 Swift 二进制的最新 GA 版本。这是 IBM 直接支持的唯一 Swift 版本，建议在应用程序中使用此版本。您可以通过检查 swift_buildpack 的 [最新发行版信息](https://github.com/IBM-Swift/swift-buildpack/releases)，来确定此受支持的版本。buildpack 可能会列出 [manifest.yml](https://github.com/IBM-Swift/swift-buildpack/blob/master/manifest.yml) 文件中所示的其他 Swift 版本。这些常见的不受支持的 Swift 版本预先缓存在 buildpack 中，其可缩短供应时间。

如果您要在 {{site.data.keyword.Bluemix}} 上为应用程序使用不同的 Swift 版本，那么您可以使用存储库根目录下的 `.swift-version` 文件来指定版本。此 `.swift-version` 文件可定义要由 swift_buildpack 使用的 Swift 版本。

```
$ cat .swift-version
3.0
```
{: pre}

因为 Swift 语言经常更新，所以您应该始终包括 `.swift-version` 文件，以便您的应用程序“锁定”到已知应用程序要使用的 Swift 版本。

请注意，您可以在 `.swift-version` 文件中指定任何有效的 Swift 版本。这些替代版本必须匹配命名，且直接从 [Swift.org](https://swift.org/download/) 拉出。虽然使用非缓存版本会花费较长的时间才能供应，但是您的 Swift 应用程序没有任何运行时性能差异。

如果应用程序的根目录包含 `Package.swift` 文件，那么会使用 {{site.data.keyword.Bluemix}} 中的缺省 swift_buildpack。如果您要使用替代 buildpack，那么您必须通过将 `buildpack: {buildpackUrl}` 条目添加到应用程序的 manifest.yml 文件，来指定此项。或者，您可以使用 `cf push -b {buildpackUrl}` 命令自变量，在部署时定义此项。


## 开发者环境

开发者在使用 Swift 创建服务器端应用程序时，有几个选择。那些使用 Apple MacOS 设备的开发者可能更愿意使用 Xcode IDE，尽管这并不是必需的。要在 {{site.data.keyword.Bluemix}} 上部署和运行的基于 Swift 的应用程序可以使用任何编程编辑器或 IDE。针对 Swift 的语法突出显示和代码自动检查功能可用于许多常用编辑器。包含在 [Swift.org](https://swift.org/) 二进制文件中的 Swift REPL 命令行工具允许在部署至 {{site.data.keyword.Bluemix}} 之前，先进行本地编译和测试。

对于 MaxOS 用户，您可以使用 [IBM Cloud Tools for Swift](http://cloudtools.bluemix.net/)，其可简化 {{site.data.keyword.Bluemix}} 上运行的服务器端 Swift 应用程序的创建、部署、管理和控制。  


## 增强的集成

使用 [Kitura Web 框架](http://ibm-swift.github.io/Kitura/)可提供许多功能。Kitura 在本质上是模块化的，您很快就会想要使用已包装的 SDK，来扩展其功能，以提供各种特性，如认证、访问基于 Watson 的服务和广泛的数据库。Kitura 可直接提供对许多数据库的支持，而其他开放式源代码项目也会为许多数据库平台提供 SDK。以下是 Kitura 所提供的可使用外部资源的 SDK 非详尽列表。

- [IBM Watson](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/swift-watson-sdk)
- [IBM DB2 和 DashDB](https://swiftpkgs.ng.bluemix.net/package/IBM-DTeam/swift-for-db2)
- [IBM Cloudant 和 Couchbase](https://swiftpkgs.ng.bluemix.net/package/cloudant/swift-cloudant)
- [IBM ObjectStorage](https://swiftpkgs.ng.bluemix.net/package/ibm-bluemix-mobile-services/bluemix-objectstorage-serversdk-swift)
- [Apache Cassandra](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Kassandra)
- [Aphid MQTT](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Aphid)

要查找更多 Swift 软件包以包含在您的应用程序中，请转至 [IBM Swift 软件包目录](https://swiftpkgs.ng.bluemix.net/)，并对目标服务或数据库执行搜索。“软件包目录”提供一种轻松的方法，可查找可包含在 Swift 应用程序中的软件包。通过将软件包的 Git URL 和版本详细信息添加到应用程序的 `Package.swift` 文件中，可将软件包添加到 Swift 应用程序。有关软件包管理的详细信息，请参阅 [Swift.org 的软件包管理器部分](https://swift.org/package-manager/)。


## 相关信息

IBM 还提供其他在线工具，可供 Swift 开发者使用。
- [IBM Swift DevCenter](https://developer.ibm.com/swift/) - 所有 IBM Swift 信息的主要登录站点。您可以查找有关我们的产品、博客、社交活动、文档等信息。
- [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/) - 通过此站点为您提供的环境，可以快速而轻松地针对 Swift 各种版本，测试 Swift 代码片段，甚至在不同的 Swift 运行时平台上也是如此。您还可以保存代码样本并与其他人共享，也可以浏览其他人提供的流行示例。


# 相关链接
{: #rellinks}
## 一般
{: #general}
* [IBM Swift DevCenter](https://developer.ibm.com/swift/)
* [IBM Cloud Tools for Swift](http://cloudtools.bluemix.net/)
* [IBM Swift 软件包目录](https://swiftpkgs.ng.bluemix.net/)
* [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/)
* [Kitura 文档和 API](http://ibm-swift.github.io/Kitura/)
* [Bluemix 的 Kitura Starter 应用程序](https://github.com/IBM-Swift/Kitura-Starter-Bluemix)
* [IBM Bluemix buildpack for Swift](https://github.com/IBM-Swift/swift-buildpack)
* [IBM Bluemix buildpack for Swift 发行说明](https://github.com/IBM-Swift/swift-buildpack/releases)
* [Swift.org](https://swift.org/)
* [Swift 语言文档](https://swift.org/documentation)
