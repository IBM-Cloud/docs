---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock: .codeblock}

# 获取代码
{: #Get_Code}

当您使用所选功能完成移动项目的配置和设置时，您可以下载支持在 Xcode 或 Android Studio 中运行的代码。您所下载的项目已使用您所配置的每一个功能所需的 SDK 依赖关系和凭证进行了预配置。

对于无法在已下载项目中配置的服务，您需要完成凭证。入门模板项目的 `README.md` 文件包含指示信息。请在 Markdown 查看器中查看 `README.md` 文件，以完成设置。

### 必备开发者工具
{: #prereq-dev-tools}

当您从 {{site.data.keyword.Bluemix_notm}} Mobile 仪表板使用生成的代码时，需要下列开发者工具：

#### Android
* [Android Studio 2.2 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://developer.android.com/studio "外部链接图标")
	* 安装最新的 [Android 7.0 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://www.android.com/versions/nougat-7-0/ "外部链接图标") 运行时。

#### iOS
* [Xcode 8.0 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://developer.apple.com/xcode/ "外部链接图标")（建议）
	* 安装最新的 [iOS 10 ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](http://www.apple.com/ios/ios-10/ "外部链接图标") 运行时。
* [Homebrew ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](http://brew.sh/ "外部链接图标")
	* 命令行工具，用于帮助安装其他工具和运行时，如 CocoaPods 和 Carthage（对于 Apple 开发者）。
* [CocoaPods ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://cocoapods.org/ "外部链接图标") 依赖关系管理器，用于安装 iOS SDK 依赖关系。请使用最新的版本：

	```
	$ sudo gem install cocoapods --pre
	```
* [Carthage ![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](https://github.com/Carthage/Carthage "外部链接图标") 依赖关系管理器，用于安装 Watson Developer Cloud SDK。

	```
	$ brew install carthage
	```

#### {{site.data.keyword.Bluemix_notm}}
* NodeJS（Node 和 NPM 运行时），以帮助运行 API Connect Loopback 和其他 Bluemix Productivity 工具。

	要在本地运行 API Connect 工具，请使用 Node 5.x：
	```
	$ brew install Node5
	```

* [Bluemix CLI 工具![外部链接图标](../icons/launch-glyph.svg "外部链接图标")](http://clis.ng.bluemix.net/ui/home.html "外部链接图标")命令行工具可使用 Bluemix 从命令行界面轻松地部署 Cloud Foundry 运行时。  
