---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-01"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}



<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->

# 備份資料
您可以抄寫 {{site.data.keyword.cloudantfull}} 資料庫來備份 {{site.data.keyword.iotinsurance_full}} 資料。
{:shortdesc}

下表顯示 {{site.data.keyword.iotinsurance_full}} 中所儲存的 {{site.data.keyword.iotinsurance_short}} 資料庫。

*表 1：{{site.data.keyword.iotinsurance_short}} 資料庫*

資料庫名稱| 變更頻率| 變更原因 | 需要備份 | 註解
------------- | -------------| -------------| -------------| -------------
favorites|管理|新的管理者動作|是|-
Devices|管理|已新增或移除新的裝置或使用者|是| 轉換器會於記憶體中動態產生表格，並且移入來自裝置提供者的資料。對於直接連接的閘道，此表格會儲存裝置。
hazardevents|隨機|偵測到新的防護事件|是|-
Jscode|管理|已部署防護的新 JS 程式碼|是*| 管理者可以選擇性地跳過備份及部署 JS 程式碼的新版本。
Promotions|管理|已新增新的促銷活動|是|-
shieldassociations|管理|已新增新的使用者或防護|是|-
Shields|管理|已新增新的防護|是|-
Users|管理|已新增新的使用者|是|-
aggregation|-|-|否|可以予以重建。
aggregationschedule|-|-| 否|可以予以重建。

若要備份 {{site.data.keyword.iotinsurance_short}} 資料，請執行下列步驟：

## 建立抄本 {{site.data.keyword.cloudant}} 實例
{: #createinstance}
使用 [{{site.data.keyword.cloudant}} 抄寫指示 ![外部鏈結圖示](../../icons/launch-glyph.svg)](https://docs.cloudant.com/replication.html)，以建立抄本 {{site.data.keyword.cloudant}} 實例。若要進行災難回復，請透過原始 {{site.data.keyword.iotinsurance_short}} 服務在不同的位置中建立抄本。例如，如果原始實例位在達拉斯，則抄本可能位在倫敦。

## 尋找認證及 URL
{: #locate_credentials}
尋找原始 {{site.data.keyword.cloudant}} 實例及已抄寫實例的認證及 URL。
1. 開啟 {{site.data.keyword.cloudant}} 服務。
2. 按一下位在服務名稱下方的**服務認證**標籤。
3. 按一下**檢視認證**。
4. 記下使用者名稱、密碼及 URL。

## 建立新的抄寫作業
{: #create_replication}
建立每一個必須備份之資料庫的抄寫作業。前一節的表 1 列出需要備份的資料庫。

1. 開啟 {{site.data.keyword.Bluemix_notm}} 主控台。

2. 開啟原始 {{site.data.keyword.cloudant}} 服務。

3. 按一下**啟動**，以開啟 {{site.data.keyword.cloudant}} 儀表板。

4. 在功能表上，選取**抄寫**。

5. 在「來源資料庫」區段中，輸入原始資料庫的 URL。每一個資料庫 URL 的格式都是 https://<CloudantbaseURL>/<database_name>。例如，hazardevents 資料庫 URL 是 https://<CloudantbaseURL>/hazardevents。

6. 在「目標資料庫」區段中，輸入新資料庫的 URL。

7. **重要事項：**請不要選取**將此抄寫設為持續**。持續抄寫會嚴重影響效能。

8. 按一下**抄寫資料**。  

9. （選用）因為後續的抄寫作業會改寫前一個資料，所以請考慮將資料匯出至 CSV 檔。如需指示，請參閱 [Export Cloudant JSON as CSV, RSS, or iCal ![外部鏈結圖示](../../icons/launch-glyph.svg)](https://developer.ibm.com/clouddataservices/2015/09/22/export-cloudant-json-as-csv-rss-or-ical/){: new_window}。

10. 針對每一個資料庫重複這些步驟。

## 執行備份
{: #run_backup}
建立抄寫作業之後，即可隨時重新執行備份。
1. 開啟 {{site.data.keyword.Bluemix_notm}} 主控台。
2. 開啟原始 {{site.data.keyword.cloudant}} 服務。
3. 按一下**啟動**，以開啟 {{site.data.keyword.cloudant}} 儀表板。
4. 在功能表上，按一下**抄寫**，然後選取**所有抄寫**。
5. 選取所有資料庫，然後重新執行每一個抄寫。按一下**作用中抄寫**，即可檢查進行中工作的狀態。
6. 完成所有抄寫之後，即可將資料匯出為 CSV 純文字檔。

## 還原資料
{: #restore_data}
您可以從已抄寫的資料庫或透過載入已儲存的 CSV 檔來還原資料。
1. 開啟 {{site.data.keyword.Bluemix_notm}} 主控台。
2. 停止 {{site.data.keyword.iotinsurance_short}} 服務。
3. 使用下列其中一種方式來還原資料：
  - 將 CSV 備份檔中的資料直接載入至主要 Cloudant 實例
  - 建立將已抄寫資料庫當作來源並將原始資料庫當作目標的抄寫作業。此作業會將已抄寫的資料移至原始資料庫。
4. 執行下列 Script 來重建設計文件，以及還原參照完整性。Script 位於 [{{site.data.keyword.iotinsurance_short}} API 範例 GitHub 網站 ![外部鏈結圖示](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/){: new_window}。
  - iot4i-api/wearable-framework/auto-create/create.sh - 此 Script 會在 {{site.data.keyword.cloudant}} 內重建設計文件。
  - iot4i-api/wearable-framework/health/check-relations - 此 Script 會重新建立參照完整性。例如，此 Script 會更正已刪除防護但使用者關聯仍然存在的情況。
