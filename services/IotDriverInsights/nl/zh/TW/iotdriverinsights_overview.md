---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 關於 {{site.data.keyword.iotdriverinsights_short}}
{: #iotdriverinsights_overview}

您可以使用 {{site.data.keyword.iotdriverinsights_full}}，從汽車探測資料及環境定義資料分析駕駛人的行為。
{:shortdesc}

## 駕駛人行為分析
{: #driver_behavior_analysis}
您可以從汽車探測資料及環境定義資料分析駕駛人行為，例如急劇加速或緊急剎車、頻繁剎車、超速行駛、急轉彎及其他動作。

包含下列活動及環境定義：
 - 駕駛行為 
    - 速度相關項目
       - 急劇加速
       - 緊急剎車
       - 超速行駛
       - 頻繁停車
       - 頻繁加速
       - 頻繁剎車
    - 轉彎相關項目
       - 急轉彎（高速轉彎）
       - 轉彎前加速
       - 轉彎時剎車過度
    - 其他
       - 疲勞駕駛
 - 駕駛環境定義
    - 時間範圍
       - 早上尖峰時間
       - 晚上尖峰時間
       - 日間
       - 夜間
    - 道路類型
       - 高速公路
       - 市區快速道路
       - 市區主要道路
       - 市區道路
       - 其他
    - 根據道路類型的速度模式
       - 順暢的車流量
       - 穩定的車流量
       - 擁塞
       - 嚴重擁塞
       - 混合狀況

## 海量資料分析基礎架構
{: #big_data_analysis_infrastructure}
{{site.data.keyword.iotdriverinsights_short}} 使用 Hadoop 作為後端基礎架構。Hadoop 可讓 {{site.data.keyword.iotdriverinsights_short}} 實現高度可調整性，用來從汽車探測資料及環境定義資料分析海量資料。

## REST API
{: #rest_api}
開發人員可以透過 REST API 擷取分析結果，並在 {{site.data.keyword.Bluemix_notm}} 應用程式中使用它們。
 1. 車輛資料
   - `sendCarProbeData` 可傳送要分析的汽車探測資料。
   - `getCarProbeDataListAsDate` 可傳回按日期排列的汽車探測資料清單。
   - `deleteCarProbeDataListByDate` 可刪除汽車探測資料。
 2. 分析工作
   - `sendJobRequest` 可傳送駕駛行為分析工作要求。
   - `getJobInfo` 可傳回所指定工作的資訊。
   - `getJobInfoList` 可傳回工作資訊的清單。
 3. 分析結果 
   - `getAnalyzedTripSummaryList` 可傳回已分析的行程摘要資訊清單。
   - `getAnalyzedTripInfo` 可傳回指定的已分析行程的資訊。
   - `deleteJobResult` 可刪除與某個工作相關的所有已分析結果。

## 可配置性
{: #configurability}
部分分析臨界值參數（例如每個道路類型的速度範圍、轉彎角度範圍等等）可以從使用者介面 (UI) 進行配置。
