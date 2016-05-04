{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .pre}


# Swift 執行時期
{: #swift_runtime}
*前次更新：2016 年 2 月 19 日*

{{site.data.keyword.Bluemix}} 上的 Swift 執行時期是採用 swift_buildpack 技術。
swift_buildpack 為 Swift 應用程式提供完整的執行時期環境。
{: shortdesc}

如果您應用程式的根目錄包含 Package.swift 檔案，將使用 swift_buildpack。

## 入門範本應用程式
{: #starter_application}

{{site.data.keyword.Bluemix}} 提供 Swift 入門範本應用程式。Swift 入門範本應用程式是簡單的 Swift 應用程式，您可以利用它來瞭解可使用 Swift 程式設計語言開發的伺服器應用程式類型。此範例應用程式會建立基本伺服器，以將 HTML 問候語傳回用戶端。  

**附註：**此入門範本應用程式不是可用於正式作業的應用程式。相反地，它是要作為教學用途。您可以用入門範本應用程式進行實驗，並進行及推送對 {{site.data.keyword.Bluemix}} 環境的變更。如需關於使用入門範本應用程式的協助，請參閱[使用入門範本應用程式](../../cfapps/starter_app_usage.html)。

## 執行時期版本
{: #runtime_versions}

您可以使用儲存庫根目錄中的 `.swift-version` 檔案，指定應用程式要使用的 Swift 版本：

```
cat .swift-version
swift-DEVELOPMENT-SNAPSHOT-2016-02-03-a
```
{: pre}

如需 Swift 所支援版本的完整清單，請參閱建置套件的 [manifest.yml](https://github.com/cloudfoundry-community/swift-buildpack/blob/master/manifest.yml) 檔案。

如需已安裝在 {{site.data.keyword.Bluemix}} 中的 Swift 建置套件的現行版本詳細資料，請參閱該建置套件的[版本資訊](https://github.com/cloudfoundry-community/swift-buildpack/releases/tag/v1.0.3)。

因為 Swift 語言經常變更，您應該包含 .swift-version 檔案，使您的應用程式「固定」為已知該應用程式可以運作的 Swift 版本。

# 相關鏈結
## 一般
* [Cloud Foundry buildpack for Swift](https://github.com/cloudfoundry-community/swift-buildpack)
* [Swift 語言文件](https://swift.org/)
