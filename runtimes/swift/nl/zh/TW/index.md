{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .pre}


# IBM Bluemix Runtime for Swift
{: #swift_runtime}
前次更新：2016 年 9 月 19 日
{: .last-updated}

{{site.data.keyword.Bluemix}} 上的 Runtime for Swift 是採用 [IBM Bluemix Buildpack for Swift](https://github.com/IBM-Swift/swift-buildpack)（亦即 swift_buildpack）的技術。
此建置套件為 Swift 應用程式提供完整的運行環境。
{: shortdesc}

## 入門範本應用程式
{: #starter_application}

{{site.data.keyword.Bluemix}} 提供以 Kitura 為基礎的 Swift [入門範本應用程式](https://github.com/IBM-Swift/Kitura-Starter-Bluemix)。Kitura
入門範本應用程式是簡單的 Swift 應用程式，您可以用來瞭解可以使用 Swift 程式設計開發的伺服器應用程式類型。這個範例應用程式會建立基本的
Kitura HTTP 伺服器，將 HTML 內容傳回給用戶端。

**附註：**Kitura 入門範本應用程式是要用於教育用途。您可以使用入門範本應用程式進行實驗－進行加強，然後將變更推送到 {{site.data.keyword.Bluemix}} 環境。請參閱[使用入門範本應用程式](../../cfapps/starter_app_usage.html)以取得使用入門範本應用程式的說明。

## 重新命名應用程式
{: #renaming_your_app}

如果您想要重新命名應用程式，無論是從 Kitura 入門範本，或是更一般性的方式，有一些變更需要注意。這樣可以避免混淆，同時確保部署不會發生錯誤。

- 重新命名應用程式的專案資料夾，以符合您的應用程式名稱。
- `Package.swift` - 變更下列項目：
    - `name` - 應該符合應用程式的名稱
    - `targets[Target(name:)]` - 應該符合應用程式的名稱
- `manifest.yml` - 變更下列項目：
    - `name` - 應該符合應用程式的名稱
    - `host` - 代表應用程式 URL 的主要主機區段
- `Procfile` - `web` 的值應該符合應用程式的目錄名稱。這是在編譯之後執行的指令，用來啟動 Web 應用程式。


## 運行環境版本
{: #runtime_versions}

根據預設值，{{site.data.keyword.Bluemix}} 上管理的 Runtime for Swift (swift_buildpack) 會使用最新 GA 版本的 Swift 二進位檔。這是 IBM 唯一直接支援的 Swift 版本，也是建議用於您應用程式中的版本。您可以檢查 swift_buildpack 的[最新版本資訊](https://github.com/IBM-Swift/swift-buildpack/releases)，確認此支援版本。建置套件可能列出其他 Swift 版本，如同其 [manifest.yml](https://github.com/IBM-Swift/swift-buildpack/blob/master/manifest.yml) 檔案中所示。這些常見但不受支援的 Swift 版本已預先快取在建置套件內，如此可縮短佈建時間。

如果您想要在 {{site.data.keyword.Bluemix}} 上為您的應用程式使用不同的 Swift 版本，可以在儲存庫的根目錄使用 `.swift-version` 檔指定版本。這個 `.swift-version` 檔案定義 swift_buildpack 要使用哪個 Swift 版本。

```
$ cat .swift-version
3.0
```
{: pre}

由於經常會有 Swift 語言更新，您應該隨時包含 `.swift-version` 檔，以便您的應用程式「固定」在應用程式已知能夠使用的 Swift 版本。

請注意，您可以在 `.swift-version` 檔案中指定任何有效的 Swift 版本。這些替代版本必須符合命名，且直接從 [Swift.org](https://swift.org/download/) 取回。使用非快取的版本會使得佈建時間略長一些，不過對於您的 Swift 應用程式而言沒有運行環境效能差異。

如果您的應用程式根目錄包含 `Package.swift` 檔，則會使用 {{site.data.keyword.Bluemix}} 中的預設 swift_buildpack。如果您想要使用替代建置套件，則必須新增 `buildpack: {buildpackUrl}` 項目到您應用程式的 manifest.yml 檔以進行指定。或者，您可以在部署時定義，方法是使用 `cf push -b {buildpackUrl}` 指令引數。


## 開發人員環境

開發人員在使用 Swift 建立伺服器端應用程式時有數個選項。使用 Apple MacOS 裝置的人可能偏好使用 Xcode IDE，不過這不是必要。將在 {{site.data.keyword.Bluemix}} 上部署與執行的 Swift 應用程式可以使用任何程式設計編輯器或 IDE。許多熱門編輯器都有 Swift 的語法強調顯示及程式碼分析。Swift REPL 指令行工具（包含在來自 [Swift.org](https://swift.org/) 的二進位檔）允許先進行本端編譯與測試，然後才部署到 {{site.data.keyword.Bluemix}}。

若為 MaxOS 使用者，您可以使用 [IBM Cloud Tools for Swift](http://cloudtools.bluemix.net/)，它會簡化對於在 {{site.data.keyword.Bluemix}} 上執行之伺服器端 Swift 應用程式的建立、部署、管理和控制。  


## 加強整合

使用 [Kitura Web 架構](http://ibm-swift.github.io/Kitura/)能夠提供許多功能。Kitura 在本質上是模組化的，您會很快就想要以套裝 SDK 來延伸它的功能，以提供例如鑑別、Watson 服務存取和各種資料庫等特性。Kitura 提供對許多資料庫的直接支援，其他開放程式碼專案也提供許多資料庫平台的 SDK。以下是 Kitura 所提供 SDK 的不完整清單，這些 SDK 可用來搭配外部資源。

- [IBM Watson](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/swift-watson-sdk)
- [IBM DB2 及 DashDB](https://swiftpkgs.ng.bluemix.net/package/IBM-DTeam/swift-for-db2)
- [IBM Cloudant 及 Couchbase](https://swiftpkgs.ng.bluemix.net/package/cloudant/swift-cloudant)
- [IBM ObjectStorage](https://swiftpkgs.ng.bluemix.net/package/ibm-bluemix-mobile-services/bluemix-objectstorage-serversdk-swift)
- [Apache Cassandra](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Kassandra)
- [Aphid MQTT](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Aphid)

若要找到更多 Swift 套件以便包含在您的應用程式中，請移至 [IBM Swift Package Catalog](https://swiftpkgs.ng.bluemix.net/) 並提供目標服務或資料庫的搜尋。Package Catalog 讓您能輕鬆找到可以包含在 Swift 應用程式中的套件。套件可以藉由將套件的 Git URL 和版本詳細資料包含在應用程式 `Package.swift` 檔案中，而新增至 Swift 應用程式。如需套件管理的詳細資料，請參閱 [Swift.org 的 Package Manager 區段](https://swift.org/package-manager/)。


## 相關資訊

IBM 也提供了其他線上工具給 Swift 開發人員使用。
- [IBM Swift DevCenter](https://developer.ibm.com/swift/) - 所有 IBM Swift 資訊的主要到達網站。您可以找到關於我們的產品與服務、部落格、社交活動、文件等等的相關資訊。
- [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/) - 這個網站提供環境讓您快速且輕鬆地針對各種 Swift 版本測試 Swift 程式碼片段，甚至是在不同的 Swift 運行環境平台上測試。您也可以儲存程式碼範例並與其他人共用，並且探索其他人所提供的熱門範例。


# 相關鏈結
{: #rellinks}
## 一般
{: #general}
* [IBM Swift DevCenter](https://developer.ibm.com/swift/)
* [IBM Cloud Tools for Swift](http://cloudtools.bluemix.net/)
* [IBM Swift Package Catalog](https://swiftpkgs.ng.bluemix.net/)
* [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/)
* [Kitura Documentation and APIs](http://ibm-swift.github.io/Kitura/)
* [Kitura Starter app for Bluemix](https://github.com/IBM-Swift/Kitura-Starter-Bluemix)
* [IBM Bluemix buildpack for Swift](https://github.com/IBM-Swift/swift-buildpack)
* [IBM Bluemix buildpack for Swift release notes](https://github.com/IBM-Swift/swift-buildpack/releases)
* [Swift.org](https://swift.org/)
* [Swift language documentation](https://swift.org/documentation)
