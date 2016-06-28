{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .pre}


# Swift 运行时
{: #swift_runtime}
*上次更新时间：2016 年 6 月 10 日*
{: .last-updated}

{{site.data.keyword.Bluemix}} 上的 Swift 运行时由 Bluemix 的 Swift buildpack（例如，swift_buildpack）提供技术支持。swift_buildpack 为 Swift 应用程序提供了完整的运行时环境。
{: shortdesc}

如果应用程序的根目录中包含 Package.swift 文件，那么将使用 swift_buildpack。

## 入门模板应用程序
{: #starter_application}

{{site.data.keyword.Bluemix}} 提供了 Swift 入门模板应用程序。Swift 入门模板应用程序是一个简单的 Swift 应用程序，可以用于了解可使用 Swift 编程语言开发的服务器应用程序的类型。此样本应用程序会创建向客户机返回 HTML 内容的基本 HTTP 服务器。

**注：**此入门模板应用程序不是用于生产的应用程序，而是旨在用于培训。您可以尝试使用该入门模板应用程序来进行更改并将更改推送到 {{site.data.keyword.Bluemix}} 环境。有关使用入门模板应用程序的帮助，请参阅[使用入门模板应用程序](../../cfapps/starter_app_usage.html)。

## 运行时版本
{: #runtime_versions}

Bluemix 上安装的 swift_buildpack 支持 Swift 二进制的 `DEVELOPMENT-SNAPSHOT-2016-05-03-a` 版本。如果希望您的应用程序在 Bluemix 上使用其他 Swift 版本，您可以在存储库根目录中的 `.swift-version` 文件中指定版本。

```
cat .swift-version
swift-DEVELOPMENT-SNAPSHOT-2016-04-25-a
```
{: pre}

除了包含 `.swift-version` 文件以外，您还需要将 `-b https://github.com/IBM-Swift/swift-buildpack` 参数添加到 `cf push` 命令中，如下所示：

```
cf push -b https://github.com/IBM-Swift/swift-buildpack
```

有关 Swift 支持的版本的完整列表，请参阅该 buildpack 的 [manifest.yml](https://github.com/IBM-Swift/swift-buildpack/blob/bluemix-buildpack/manifest.yml) 文件。

有关在 {{site.data.keyword.Bluemix}} 中安装的 Swift buildpack 的当前版本，请参阅该 buildpack 的[发行版信息](https://github.com/IBM-Swift/swift-buildpack/releases/tag/1.1.1)。

由于 Swift 语言更改频繁，因此应该包含 `.swift-version` 文件，以便应用程序“锁定”到应用程序已知使用的 Swift 版本。另请记住，如果使用 `DEVELOPMENT-SNAPSHOT-2016-05-03-a` 以外的 Swift 版本，您之后在推送应用程序时应指定 `-b https://github.com/IBM-Swift/swift-buildpack` 参数（如上所示）。

# 相关链接
{: #rellinks}
## 常规
{: #general}
* [Bluemix 的 Swift buildpack](https://github.com/IBM-Swift/swift-buildpack)
* [Swift 语言文档](https://swift.org/)
