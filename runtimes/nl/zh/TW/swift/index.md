{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .pre}


# Swift 運行環境
{: #swift_runtime}
*前次更新：2016 年 6 月 10 日*
{: .last-updated}

{{site.data.keyword.Bluemix}} 上的 Swift 運行環境是採用適用於 Bluemix 的 Swift 建置套件技術（亦即 swift_buildpack）。
swift_buildpack 為 Swift 應用程式提供完整的運行環境。
{: shortdesc}

如果您應用程式的根目錄包含 Package.swift 檔案，將使用 swift_buildpack。

## 入門範本應用程式
{: #starter_application}

{{site.data.keyword.Bluemix}} 提供 Swift 入門範本應用程式。Swift 入門範本應用程式是簡單的 Swift 應用程式，您可以利用它來瞭解可使用 Swift 程式設計語言開發的伺服器應用程式類型。此範例應用程式會建立基本 HTTP 伺服器，以將 HTML 內容傳回給用戶端。

**附註：**此入門範本應用程式不是可用於正式作業的應用程式。相反地，它是要作為教學用途。您可以用入門範本應用程式進行實驗，並進行及推送對 {{site.data.keyword.Bluemix}} 環境的變更。如需關於使用入門範本應用程式的協助，請參閱[使用入門範本應用程式](../../cfapps/starter_app_usage.html)。

## 運行環境版本
{: #runtime_versions}

安裝於 Bluemix 的 swift_buildpack 支援 `DEVELOPMENT-SNAPSHOT-2016-05-03-a` 版本的 Swift 二進位檔。如果您要在 Bluemix 上針對應用程式使用不同版本的 Swift，則可以使用儲存庫根目錄中的 `.swift-version` 檔案來指定版本：

```
cat .swift-version
swift-DEVELOPMENT-SNAPSHOT-2016-04-25-a
```
{: pre}

除了包括 `.swift-version` 檔案之外，您還需要將 `-b https://github.com/IBM-Swift/swift-buildpack` 參數新增至 `cf push` 指令，如下所示：

```
cf push -b https://github.com/IBM-Swift/swift-buildpack
```

如需 Swift 所支援版本的完整清單，請參閱建置套件的 [manifest.yml](https://github.com/IBM-Swift/swift-buildpack/blob/bluemix-buildpack/manifest.yml) 檔案。

如需已安裝在 {{site.data.keyword.Bluemix}} 中的 Swift 建置套件的現行版本詳細資料，請參閱該建置套件的[版本資訊](https://github.com/IBM-Swift/swift-buildpack/releases/tag/1.1.1)。

因為 Swift 語言經常變更，所以您應該包含 `.swift-version` 檔案，使您的應用程式「固定」使用該應用程式已知可以搭配運作的 Swift 版本。也請記住，如果您使用的 Swift 版本不是 `DEVELOPMENT-SNAPSHOT-2016-05-03-a`，則應該在推送應用程式時指定 `-b https://github.com/IBM-Swift/swift-buildpack` 參數（如上所述）。

# 相關鏈結
{: #rellinks}
## 一般
{: #general}
* [適用於 Bluemix 的 Swift 建置套件](https://github.com/IBM-Swift/swift-buildpack)
* [Swift 語言文件](https://swift.org/)
