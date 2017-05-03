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

{{site.data.keyword.Bluemix}} 上的 Runtime for Swift 是採用 [IBM Bluemix buildpack for Swift](https://github.com/IBM-Swift/swift-buildpack) 技術（即 swift_buildpack）。
此建置套件為 Swift 應用程式提供完整的運行環境。
{: shortdesc}

## 入門範本應用程式
{: #starter_application}

{{site.data.keyword.Bluemix}} 提供 Kitura 型 Swift [入門範本應用程式](https://github.com/IBM-Bluemix/Kitura-Starter)。Kitura 入門範本應用程式是簡單的 Swift 應用程式，您可以利用它來瞭解可使用 Swift 程式設計語言開發的伺服器應用程式類型。此範例應用程式會建立基本 Kitura HTTP 伺服器，以將 HTML 內容傳回給用戶端。

**附註：**Kitura 入門範本應用程式是要作為教學用途。您可以利用入門範本應用程式進行實驗，並將那些變更推送至 {{site.data.keyword.Bluemix}} 環境。如需關於使用入門範本應用程式的協助，請參閱[使用入門範本應用程式](../../cfapps/starter_app_usage.html)。

## 重新命名您的應用程式
{: #renaming_your_app}

如果您要從 Kitura 入門範本或以一般方式重新命名應用程式，有許多需要處理的變更。這會避免混淆，並確保無錯誤的部署。

- 重新命名應用程式的專案資料夾，以符合您應用程式的名稱。
- `Package.swift` - 變更下列項目：
    - `name` - 應該符合應用程式的名稱。
    - `targets[Target(name:)]` - 應該符合應用程式的名稱。
- `manifest.yml` - 變更下列項目：
    - `name` - 應該符合應用程式的名稱。
    - `command` - 用來啟動應用程式的執行檔名稱（應該符合 Package.swift 檔案中所指定的名稱）。

## 運行環境版本
{: #runtime_versions}

依預設，{{site.data.keyword.Bluemix}} 上管理的 Runtime for Swift (swift_buildpack) 會使用 Swift 二進位檔的最新 GA 版本。這是 IBM 直接支援的唯一 Swift 版本，而且是要在您應用程式中使用的建議版本。您可以檢查 swift_buildpack 的[最新版本資訊](https://github.com/IBM-Swift/swift-buildpack/releases)，來判定此支援的版本。建置套件可能列出其 [manifest.yml](https://github.com/IBM-Swift/swift-buildpack/blob/master/manifest.yml) 檔案內顯示的其他 Swift 版本。在建置套件內會預先快取這些常用但不受支援的 Swift 版本，因而縮短佈建時間。

如果想要對您的應用程式使用 {{site.data.keyword.Bluemix}} 上不同版本的 Swift，則您可以利用儲存庫的根目錄中的 `.swift-version` 檔案指定版本。此 `.swift-version` 檔案定義 swift_buildpack 將使用的 Swift 版本。

```
$ cat .swift-version
3.0
```
{: pre}

因為 Swift 語言經常更新，所以您應該一律包括 `.swift-version` 檔案，使您的應用程式「固定」使用該應用程式已知可以搭配運作的 Swift 版本。

請注意，您可以在 `.swift-version` 檔案中指定任何有效的 Swift 版本。這些替代版本必須符合命名，而且直接從 [Swift.org ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://swift.org/download/) 取回。儘管使用非快取版本將需要有點長的時間來佈建，但您的 Swift 應用程式沒有運行環境效能差異。

如果您應用程式的根目錄包含 `Package.swift` 檔案，則會使用 {{site.data.keyword.Bluemix}} 中的預設 swift_buildpack。如果您喜歡使用替代建置套件，則必須將 `buildpack: {buildpackUrl}` 項目新增至應用程式的 manifest.yml 檔案來指定此建置套件。或者，您可以在部署時使用 `cf push -b {buildpackUrl}` 指令引數，來定義此建置套件。


## 開發人員環境

使用 Swift 建立伺服器端應用程式時，開發人員有數個選項。雖然使用 Xcode IDE 不是需求，但是使用 Apple 的 MacOS 裝置的開發人員可能喜好使用 Xcode IDE。將在 {{site.data.keyword.Bluemix}} 上部署並執行的 Swift 型應用程式可以使用任何程式設計編輯器或 IDE。許多著名的編輯器可以使用 Swift 的語法強調顯示及標示。來自 [Swift.org ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://swift.org/) 的二進位檔中內含的 Swift REPL 指令行工具，容許在部署至 {{site.data.keyword.Bluemix}} 之前進行本端編譯及測試。

若為 MaxOS 使用者，您可以使用 [IBM Cloud Tools for Swift](http://cloudtools.bluemix.net/)，簡化在 {{site.data.keyword.Bluemix}} 上執行之伺服器端 Swift 應用程式的建立、部署、管理及控制。  


## 加強的整合

使用 [Kitura Web 架構](http://ibm-swift.github.io/Kitura/)可提供相當多的功能。Kitura 的本質是模組化，而且您很快就會想要使用套裝的 SDK 擴充其功能，以提供如下功能：鑑別、存取 Watson 型服務，以及廣泛的各種資料庫。Kitura 可直接支援許多資料庫，而其他開放程式碼專案也會針對許多資料庫平台提供 SDK。下列是 Kitura 所提供以使用外部資源之 SDK 的非完整清單。

- [IBM Watson](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/swift-watson-sdk)
- [IBM DB2 及 DashDB](https://swiftpkgs.ng.bluemix.net/package/IBM-DTeam/swift-for-db2)
- [IBM Cloudant 及 CouchDB](https://swiftpkgs.ng.bluemix.net/package/cloudant/swift-cloudant)
- [IBM ObjectStorage](https://swiftpkgs.ng.bluemix.net/package/ibm-bluemix-mobile-services/bluemix-objectstorage-serversdk-swift)
- [Apache Cassandra](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Kassandra)
- [Aphid MQTT](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Aphid)

若要尋找要包含在您應用程式中的其他 Swift 套件，請移至 [IBM Swift 套件型錄](https://swiftpkgs.ng.bluemix.net/)，並在您的目標服務或資料庫上執行搜尋。「套件型錄」提供一種簡易方法，以找出您可以包含在 Swift 應用程式中的套件，套件可以新增至 Swift 應用程式，方法為將套件的 Git URL 及版本詳細資料包含在應用程式的 `Package.swift` 檔案中。如需套件管理的其他詳細資料，請參閱 [Swift.org 的套件管理小節](https://swift.org/package-manager/)，


## 相關資訊

IBM 也提供可供 Swift 開發人員使用的其他線上工具。
- [IBM Swift DevCenter](https://developer.ibm.com/swift/) - 所有 IBM Swift 資訊的主要登入網站。您可以尋找有關我們的供應項目、部落格、社交活動、文件，以及其他項目的資訊。
- [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/) - 此網站提供一種環境，可讓您針對各種 Swift 版本快速且輕易地測試 Swift 程式碼片段，而且甚至在不同的 Swift 運行環境平台上也可以這樣做。您也可以儲存程式碼範例並與其他人共用，也可以瀏覽其他人所提供的著名範例。


# 相關鏈結
{: #rellinks notoc}
## 一般
{: #general notoc}
* [IBM Swift DevCenter](https://developer.ibm.com/swift/)
* [IBM Cloud Tools for Swift](http://cloudtools.bluemix.net/)
* [IBM Swift 套件型錄](https://swiftpkgs.ng.bluemix.net/)
* [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/)
* [Kitura 文件及 API](http://ibm-swift.github.io/Kitura/)
* [適用於 Bluemix 的 Kitura 入門範本應用程式](https://github.com/IBM-Bluemix/Kitura-Starter)
* [IBM Bluemix buildpack for Swift](https://github.com/IBM-Swift/swift-buildpack)
* [IBM Bluemix buildpack for Swift 版本注意事項](https://github.com/IBM-Swift/swift-buildpack/releases)
* [Swift.org ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://swift.org/)
* [Swift 語言文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://swift.org/documentation)
