{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .pre}


# Swift 运行时
{: #swift_runtime}
*上次更新时间：2016 年 2 月 19 日*

{{site.data.keyword.Bluemix}} 上的 Swift 运行时由 swift_buildpack 提供技术支持。swift_buildpack 为 Swift 应用程序提供了完整的运行时环境。
{: shortdesc}

如果应用程序的根目录中包含 Package.swift 文件，那么将使用 swift_buildpack。

## 入门模板应用程序
{: #starter_application}

{{site.data.keyword.Bluemix}} 提供了 Swift 入门模板应用程序。Swift 入门模板应用程序是一个简单的 Swift 应用程序，可以用于了解可使用 Swift 编程语言开发的服务器应用程序的类型。此样本应用程序会创建向客户机返回 HTML 问候的基本服务器。  

**注：**此入门模板应用程序不是用于生产的应用程序，而是旨在用于培训。您可以尝试使用该入门模板应用程序来进行更改并将更改推送到 {{site.data.keyword.Bluemix}} 环境。有关使用入门模板应用程序的帮助，请参阅[使用入门模板应用程序](../../cfapps/starter_app_usage.html)。

## 运行时版本
{: #runtime_versions}

您可以使用存储库根目录下的 `.swift`-version 文件来指定您的应用程序要使用的 Swift 版本。

```
cat .swift-version
swift-DEVELOPMENT-SNAPSHOT-2016-02-03-a
```
{: pre}

有关 Swift 支持的版本的完整列表，请参阅该 buildpack 的 [manifest.yml](https://github.com/cloudfoundry-community/swift-buildpack/blob/master/manifest.yml) 文件。

有关在 {{site.data.keyword.Bluemix}} 中安装的 Swift buildpack 的当前版本，请参阅该 buildpack 的[发行版信息](https://github.com/cloudfoundry-community/swift-buildpack/releases/tag/v1.0.3)。

由于 Swift 语言更改频繁，因此应该包含 .swift-version 文件，以便应用程序“锁定”到应用程序已知使用的 Swift 版本。

# 相关链接
## 常规
* [用于 Swift 的 Cloud Foundry buildpack](https://github.com/cloudfoundry-community/swift-buildpack)
* [Swift 语言文档](https://swift.org/)
