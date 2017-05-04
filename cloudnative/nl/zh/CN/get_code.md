---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-18"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock: .codeblock}

# 获取代码
{: #Get_Code}

当您使用所选功能完成项目的配置和设置时，您可以下载支持运行应用程序的代码。您所下载的项目已使用您所配置的每一个功能所需的 SDK 依赖关系和凭证进行了预配置。

对于无法在已下载项目中配置的服务，您需要完成凭证。入门模板项目的 `README.md` 文件包含指示信息。请在 Markdown 查看器中查看 `README.md` 文件，以完成设置。

## 必备开发者工具
{: #prereq-dev-tools}

当您从 {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} 使用生成的代码时，需要下列开发者工具：


### 常规
{: #general notoc}

* [Homebrew ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](http://brew.sh/)
	* 命令行工具，用于帮助安装其他工具和运行时，如 CocoaPods 和 Carthage（对于 Apple 开发者）。

* [Docker ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.docker.com/get-docker)
	* 开放式源代码项目，用于帮助运行和调试容器中的应用程序。只有非移动项目需要它。

### {{site.data.keyword.Bluemix_notm}}
{: #bluemix notoc}

* Node.js（Node 和 npm 运行时），用于帮助运行 {{site.data.keyword.apiconnect_short}} Lopback 和其他 {{site.data.keyword.Bluemix_notm}} Productivity 工具。

	要在本地运行 {{site.data.keyword.apiconnect_short}} 工具，请使用 Node 5.x：
	
	```
	$ brew install Node5
	```

* [Bluemix CLI 工具 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](http://clis.ng.bluemix.net/ui/home.html)

   命令行工具，用于使用 {{site.data.keyword.Bluemix_notm}} 从命令行界面部署 Cloud Foundry 运行时。  

* [{{site.data.keyword.dev_cli_notm}} ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](dev_cli.html)

	{{site.data.keyword.Bluemix_notm}} CLI 插件，用于创建、运行、测试和部署 Web 和移动项目。
	
* [SDK Generator 插件 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](sdk_cli.html)

	{{site.data.keyword.Bluemix_notm}} CLI 插件，用于从符合[开放 API 规范 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.openapis.org/) 的 REST API 定义中生成 SDK。

### Android
{: #android notoc}

* [Android Studio 2.2 或更高版本 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://developer.android.com/studio)
	* 安装最新的 [Android 7.0 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.android.com/versions/nougat-7-0/) 运行时。

### iOS
{: #ios notoc}

* [Xcode 8 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://developer.apple.com/xcode/)（建议）

<!-- * Install the latest [iOS 10 ![External link icon](../icons/launch-glyph.svg "External link icon")](http://www.apple.com/ios/ios-10/) runtime.
-->
* [CocoaPods ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://cocoapods.org/) 依赖关系管理器，用于安装 iOS SDK 依赖关系。请使用最新的版本：

	```
	$ sudo gem install cocoapods --pre
	```
* [Carthage ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://github.com/Carthage/Carthage) 依赖关系管理器，用于安装 {{site.data.keyword.watson}} Developer Cloud SDK。

	```
	$ brew install carthage
	```
