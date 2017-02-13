---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock: .codeblock}

# 取得程式碼
{: #Get_Code}

當您使用選取的功能完成配置及設定行動專案時，即可下載讓您採用 Xcode 或 Android Studio 執行程式碼的程式碼。您的已下載專案已預先配置您所配置的每一個功能的必要 SDK 相依關係及認證。

您需要完成無法在已下載專案中配置之服務的認證。入門範本專案的 `README.md` 檔案包含這些指示。請使用 Markdown 檢視器檢視 `README.md` 檔案，以完成設定。

### 必備開發人員工具
{: #prereq-dev-tools}

當您從 {{site.data.keyword.Bluemix_notm}} 行動儀表板使用產生的程式碼時，需要下列開發人員工具：

#### Android
* [Android Studio 2.2 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.android.com/studio "外部鏈結圖示")
	* 安裝最新的 [Android 7.0 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://www.android.com/versions/nougat-7-0/ "外部鏈結圖示") 運行環境。

#### iOS
* [Xcode 8.0 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.apple.com/xcode/ "外部鏈結圖示")（建議）
	* 安裝最新的 [iOS 10 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](http://www.apple.com/ios/ios-10/ "外部鏈結圖示") 運行環境。
* [Homebrew ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](http://brew.sh/ "外部鏈結圖示")
	* 協助 Apple 開發人員安裝其他工具及運行環境（例如 CocoaPods 及 Carthage）的指令行工具。
* [CocoaPods ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://cocoapods.org/ "外部鏈結圖示") 相依關係管理程式，用於安裝 iOS SDK 相依關係。請使用最新版本：

	```
	$ sudo gem install cocoapods --pre
	```
* [Carthage ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/Carthage/Carthage "外部鏈結圖示") 相依關係管理程式，用於安裝 Watson Developer Cloud SDK。

	```
	$ brew install carthage
	```

#### {{site.data.keyword.Bluemix_notm}}
* 協助執行 API Connect Loopback 及其他 Bluemix Productivity 工具的 NodeJS（Node 及 NPM 運行環境）。

	若要在本端執行 API Connect 工具，請使用 Node 5.x：
	```
	$ brew install Node5
	```

* [Bluemix CLI 工具 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](http://clis.ng.bluemix.net/ui/home.html "外部鏈結圖示")。
使用 Bluemix 從指令行介面輕鬆地部署 Cloud Foundry 運行環境的指令行工具。  
