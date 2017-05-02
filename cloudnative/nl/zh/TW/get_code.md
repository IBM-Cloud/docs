---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-18"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock: .codeblock}

# 取得程式碼
{: #Get_Code}

當您使用選取的功能完成配置及設定專案時，即可下載可讓您執行應用程式的程式碼。您的已下載專案已預先配置您所配置的每一個功能的必要 SDK 相依關係及認證。

您需要完成無法在已下載專案中配置之服務的認證。入門範本專案的 `README.md` 檔案包含這些指示。請使用 Markdown 檢視器檢視 `README.md` 檔案，以完成設定。

## 必備開發人員工具
{: #prereq-dev-tools}

當您從 {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} 使用產生的程式碼時，需要下列開發人員工具：


### 一般
{: #general notoc}

* [Homebrew ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](http://brew.sh/)
	* 協助 Apple 開發人員安裝其他工具及運行環境（例如 CocoaPods 及 Carthage）的指令行工具。

* [Docker ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://www.docker.com/get-docker)
	* 開放程式碼專案，協助在容器中執行及除錯應用程式。只有針對非行動專案，這才是必要項目。

### {{site.data.keyword.Bluemix_notm}}
{: #bluemix notoc}

* Node.js（Node 及 npm 運行環境），協助執行 {{site.data.keyword.apiconnect_short}} Loopback 及其他 {{site.data.keyword.Bluemix_notm}} Productivity 工具。

	若要在本端執行 {{site.data.keyword.apiconnect_short}} 工具，請使用 Node 5.x：
	
	```
	$ brew install Node5
	```

* [Bluemix CLI 工具 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](http://clis.ng.bluemix.net/ui/home.html)

   使用 {{site.data.keyword.Bluemix_notm}}，從指令行介面部署 Cloud Foundry 運行環境的指令行工具。  

* [{{site.data.keyword.dev_cli_notm}} ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](dev_cli.html)

	建立、執行、測試與部署 Web 及行動專案的 {{site.data.keyword.Bluemix_notm}} CLI 外掛程式。
	
* [SDK 產生器外掛程式 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](sdk_cli.html)

	從 [Open API 規格 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://www.openapis.org/) 相容的 REST API 定義產生 SDK 的 {{site.data.keyword.Bluemix_notm}} CLI 外掛程式。

### Android
{: #android notoc}

* [Android Studio 2.2 或更新版本![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.android.com/studio)
	* 安裝最新的 [Android 7.0 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://www.android.com/versions/nougat-7-0/) 運行環境。

### iOS
{: #ios notoc}

* [Xcode 8 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.apple.com/xcode/)（建議）

<!-- * Install the latest [iOS 10 ![External link icon](../icons/launch-glyph.svg "External link icon")](http://www.apple.com/ios/ios-10/) runtime.
-->
* [CocoaPods ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://cocoapods.org/) 相依關係管理程式，用於安裝 iOS SDK 相依關係。請使用最新版本：

	```
	$ sudo gem install cocoapods --pre
	```
* 安裝 {{site.data.keyword.watson}} Developer Cloud SDK 的 [Carthage ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/Carthage/Carthage) 相依關係管理員。

	```
	$ brew install carthage
	```
