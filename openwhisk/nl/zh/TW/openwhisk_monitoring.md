---

copyright:
  years: 2016
lastupdated: "2016-08-02"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 使用 {{site.data.keyword.openwhisk_short}} 儀表板監視 {{site.data.keyword.openwhisk_short}} 活動

[{{site.data.keyword.openwhisk}} 儀表板](https://{DomainName}/whisk/dashboard/)提供活動的圖形摘要。使用儀表板，以判定 {{site.data.keyword.openwhisk_short}} 動作的效能及性能。
{:shortdesc}

隨時按一下**重新載入**，以使用最新啟動日誌資料來更新儀表板。

## 活動摘要
{: #summary}

此視圖提供 {{site.data.keyword.openwhisk_short}} 環境的高階摘要。使用**活動摘要**視圖，以監視啟用 {{site.data.keyword.openwhisk_short}} 功能的服務的整體性能及效能。從此視圖中的度量值，您可以執行下列動作：
* 判定服務之啟用 {{site.data.keyword.openwhisk_short}} 功能的動作的使用率，方法是檢視呼叫這些動作的次數。
* 判定所有動作的整體失敗率。如果您發現錯誤，則可以檢視**活動直方圖**視圖，來找出發生錯誤的服務或動作。檢視**活動日誌**，以找出錯誤本身。
* 檢視與每一個動作相關聯的平均完成時間，以判定動作的效能。

<!-- For tips on improving performance, see troubleshooting? -->

## 活動時間表
{: #timeline}

**活動時間表**視圖會顯示垂直線圖形，以檢視過去及現在動作的活動。紅色指出特定動作內發生錯誤。請產生此視圖與**活動日誌**的關聯，以尋找錯誤的其他詳細資料。

## 活動直方圖
{: #histogram}

**活動直方圖**視圖會顯示水平軸圖形，以檢視過去及現在動作的活動。紅色指出特定動作內發生錯誤。請產生此視圖與**活動日誌**的關聯，以尋找錯誤的其他詳細資料。

## 活動日誌
{: #log}

此視圖顯示啟動日誌的格式化版本。它會顯示每次啟動的詳細資料，但是一分鐘會輪詢一次來尋找新的啟動。按一下動作來顯示詳細日誌。
**附註：**若要使用 CLI 來取得「活動日誌」中顯示的輸出，請使用下列指令：

  ```
wsk activation poll
  ```
  {: pre}

## 過濾選項
{: #filtering}

選取您要檢視的動作日誌，以及選取所記載活動的時間範圍。

**附註：**這些過濾器會套用至儀表板上的所有視圖。
