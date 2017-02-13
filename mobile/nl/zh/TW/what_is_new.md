---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}

# 行動儀表板的新增功能
{: #what_is_new}

### 文件日期：2016 年 12 月
{: #dec-2016}

{{site.data.keyword.Bluemix}} 行動儀表板的 2016 年 12  月更新引進了下列變更：

   * 您可以從專案中移除已連接的服務，以便可以刪除它，或搭配另一個專案重複使用它。 
   * 您可以將現有服務新增至專案。
   * 當使用程式碼入門範本時，您可以建立或連接現有的 CloudantNoSQL 服務，作為資料來源。
   * 一旦支援，您就可以建立或連接現有的「物件儲存空間」服務，作為您專案的資料來源。
   * 您可以自訂您將利用使用者介面入門範本建立之應用程式的導覽設計。 
   

### 文件日期：2016 年 11 月
{: #nov-2016}

{{site.data.keyword.Bluemix}} 行動儀表板的十一月更新引進了下列變更：

   * 您現在可以從**程式碼**頁面產生專案的 SDK 構件。
   * Basic Code Starter 現在支援 Cordova。
   * 您現在可以在「{{site.data.keyword.mobileanalytics_short}} 主控台」的**網路要求**頁面中[報告網路事件 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](/docs/services/mobileanalytics/sdk.html#network-requests "外部鏈結圖示"){: new_window} 及[監視網路要求 ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](/docs/services/mobileanalytics/app-monitoring.html#monitor-network-requests "外部鏈結圖示"){: new_window}。
   * 您現在可以在「{{site.data.keyword.mobileanalytics_short}} 主控台」中[將資料匯出至 dashDB ![外部鏈結圖示](../icons/launch-glyph.svg "外部鏈結圖示")](/docs/services/mobileanalytics/app-monitoring.html#dashdb "外部鏈結圖示"){: new_window}。


### 文件日期：2016 年 10 月
{: #oct-2016}

{{site.data.keyword.Bluemix_notm}} 行動儀表板的 2016 年十月更新引進了下列變更：

   * 您現在可以直接從儀表板中將 {{site.data.keyword.mobilepushshort}} 及 Analytics 功能新增至專案。
   * 現在已提供[程式碼入門範本](starters.html#Code_Starter)。
   * 您可以將「鑑別」新增至從「程式碼入門範本」建立的專案。
   * 現在支援 Swift。


#### Analytics
{: #analytics}

   * 當您新增 Analytics 功能時，預設會啟用展示模式。在您執行應用程式之後，即可關閉展示模式來檢視分析。


#### 使用者介面建置器
{: #ui_builder}

   * 現在可以從專案存取 **{{site.data.keyword.mobilepushshort}}** 功能。
   * **專案設定**標籤已重新命名為**設定**標籤。
   * **鑑別**標籤已重新命名為**使用者存取**標籤。


#### 程式碼
{: #code}

   * 針對 iOS 產生的 Objective-C 及 Swift 程式碼現在使用 CocoaPods 來管理相依關係。這表示您需要安裝 CocoaPods。若要安裝它，請執行 `sudo gem install cocoapods`。安裝 CocoaPods 之後，請執行 `pod setup` 來進行配置（如果尚未配置）。最後，執行 `pod install` 來下載及安裝必要的專案相依關係，之後再於 Xcode 中開啟 `.xcworkspace` 檔案。在所下載程式碼保存檔的 `README.md` 檔案中提供其他詳細資料。如需相關資訊，請閱讀[必備開發人員工具](get_code.html#prereq-dev-tools)。

請經常檢查，以保有最新的更新項目。
