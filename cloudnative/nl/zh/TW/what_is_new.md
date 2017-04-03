---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} 的新增功能
{: #what-is-new}


## 文件日期：2017 年 3 月
{: #mar-2017}

{{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} 的 2017 年 3 月更新引進下列變更：

   * 「{{site.data.keyword.Bluemix_notm}} 行動」儀表板現在是 {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}}。
   * 專案建立已經過重新設計，併入了支援 Node.js、Java 及 Swift 的「Web 應用程式」、BFF 及 Microservice 伺服器型樣類型。
   * 與新增及改良的 {{site.data.keyword.appid_full}} 服務的整合，可鑑別行動及 Web 專案。
   * 您現在可以使用 [SDK 產生器外掛程式](sdk_cli.html)，額外產生專案的 SDK。只有針對 Mobile 專案，才能在 {{site.data.keyword.dev_console}} 中產生 SDK。
   * 您現在可以使用 [{{site.data.keyword.dev_cli_short}}](dev_cli.html)，額外建立專案。


## 文件日期：2017 年 1 月
{: #jan-2017}

「{{site.data.keyword.Bluemix_notm}} 行動」儀表板的 2017 年 1 月更新引進下列變更：

   * 自 1 月 31 日開始，「使用者介面入門範本」已淘汰。在 2017 年 4 月 30 日之前，可以使用從「使用者介面入門範本」建立的現有專案。如需移轉步驟及移除日期的相關資訊，請參閱[淘汰公告部落格文章 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/blogs/bluemix/2017/01/bluemix-mobile-dashboard-update/)。
{: deprecated}
   * 您現在可以更新專案入門範本類型，而不是刪除專案並建立新的專案。
   * 您現在可以使用「[Watson Conversation](tutorial_conversation.html) 程式碼入門範本」建立專案。
   * 支援時，您現在可以產生專案的 SDK。
   * 您現在可以新增現有[運算](sdk_compute.html)實例，並產生要新增至專案的用戶端 SDK。


## 文件日期：2016 年 12 月
{: #dec-2016}

{{site.data.keyword.Bluemix_notm}} 行動儀表板的 2016 年 12  月更新引進了下列變更：

   * 您現在可以從專案中移除已連接的服務，以將它刪除，或搭配另一個專案重複使用。 
   * 您現在可以將現有服務新增至專案。
   * 現在，使用「程式碼入門範本」時，您可以建立或連接現有 CloudantNoSQL 服務，作為資料來源。
   * 一旦支援，您就可以建立或連接現有「物件儲存空間」服務，作為您專案的資料來源。
   * 您現在可以自訂您將利用「使用者介面入門範本」建立之應用程式的導覽設計。 
   

## 文件日期：2016 年 11 月
{: #nov-2016}

{{site.data.keyword.Bluemix_notm}} 行動儀表板的十一月更新引進了下列變更：

   * 您現在可以從**程式碼**頁面產生專案的 SDK 構件。
   * Basic Code Starter 現在支援 Cordova。
   * 您現在可以在 {{site.data.keyword.mobileanalytics_short}} 主控台的**網路要求**頁面中[報告網路事件 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](/docs/services/mobileanalytics/sdk.html#network-requests){: new_window} 及[監視網路要求 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](/docs/services/mobileanalytics/app-monitoring.html#monitor-network-requests){: new_window}。
   * 您現在可以在 {{site.data.keyword.mobileanalytics_short}} 主控台中[將資料匯出至 dashDB ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](/docs/services/mobileanalytics/app-monitoring.html#dashdb){: new_window}。


## 文件日期：2016 年 10 月
{: #oct-2016}

{{site.data.keyword.Bluemix_notm}} 行動儀表板的 2016 年十月更新引進了下列變更：

   * 您現在可以直接從儀表板中將 {{site.data.keyword.mobilepushshort}} 及分析功能新增至專案。
   * 現在已提供[程式碼入門範本](starters.html#Code_Starter)。
   * 您可以將「鑑別」新增至從「程式碼入門範本」建立的專案。
   * 現在支援 Swift。


### 分析
{: #analytics notoc}

   * 當您新增分析功能時，預設會啟用展示模式。在您執行應用程式之後，即可關閉展示模式來檢視分析。


### 使用者介面建置器
{: #ui_builder notoc}

   * 現在可以從專案存取 **{{site.data.keyword.mobilepushshort}}** 功能。
   * **專案設定**標籤已重新命名為**設定**標籤。
   * **鑑別**標籤已重新命名為**使用者存取**標籤。


### 程式碼
{: #code notoc}

   * 針對 iOS 產生的 Objective-C 及 Swift 程式碼現在使用 CocoaPods 來管理相依關係。這表示您需要安裝 CocoaPods。若要安裝它，請執行 `sudo gem install cocoapods`。安裝 CocoaPods 之後，請執行 `pod setup` 來進行配置（如果尚未配置）。最後，執行 `pod install` 來下載及安裝必要的專案相依關係，之後再於 Xcode 中開啟 `.xcworkspace` 檔案。在所下載程式碼保存檔的 `README.md` 檔案中提供其他詳細資料。如需相關資訊，請閱讀[必備開發人員工具](get_code.html#prereq-dev-tools)。

請經常檢查，以保有最新的更新項目。
