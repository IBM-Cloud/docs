---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 管理 Trajectory Pattern Analysis
{: #tp_iotdriverinsights_admin}

前次更新：2016 年 7 月 22 日
{: .last-updated}

若要管理 Trajectory Pattern Analysis 服務，請使用 {{site.data.keyword.Bluemix_notm}} 儀表板上的管理主控台。從管理主控台中，您可以配置 Trajectory Pattern Analysis 的參數，以及管理服務中所儲存的資料。您也可以檢視承租戶資訊，以及重設承租戶密碼。

{:shortdesc}

## 啟動管理主控台
{: #start-admin-console}

若要存取 {{site.data.keyword.iotdriverinsights_full}} 之 Trajectory Pattern Analysis 服務的管理主控台，請執行下列動作：

1. 在 {{site.data.keyword.Bluemix_notm}} 儀表板上，按一下 {{site.data.keyword.iotdriverinsights_short}} 服務磚。
2. 選取服務實例的**管理**視圖。請記下使用者名稱和密碼認證，因為您稍後需要它們。若要存取管理主控台，則需要您的 IBM ID，這可能與 {{site.data.keyword.Bluemix_notm}} 認證不同。
3. 按一下**啟動**，然後在系統提示時輸入 IBM ID 認證。
4. 按一下**登入**。即會開啟**管理主控台**視窗。


## 管理承租戶資訊
{: #viewtenantinfo}

若要檢視承租戶資訊，請按一下**承租戶資訊**。

### 重設承租戶密碼
{: #resettenantpassword}

若要重設承租戶密碼，請執行下列動作：

1. 從**承租戶資訊**視窗中，按一下**重設**。
2. 在確認對話框上，按一下**確定**。即會產生新的密碼，並將其顯示在**承租戶資訊**視圖中。**重要事項：**請確定您在所有存取 {{site.data.keyword.iotdriverinsights_short}} API 的應用程式中更新密碼。

## 配置服務參數
{: #configureparameters}

服務參數可控制行程資料的分析方式。若要修改 Trajectory Pattern Analysis 服務參數，請執行下列動作：

1. 開啟**參數**視圖。
2. 按一下**行程型樣的參數**標籤，然後更新[行程型樣分析參數](#tp_parameters)，以符合您的需求。
3. 按一下**儲存**。
4. 按一下**確定**。

已更新的參數值會套用至提交的下一個工作。

### 支援臨界值參數

下表說明您可在**行程型樣的參數**標籤上配置的支援臨界值參數。

|參數名稱|說明|預設值|
|:--------|:--------|:-------|
|O/D 的最小行程號碼支援|O/D（原點/目的地）型樣所需的最小絕對支援行程號碼|4（必須大於零）|
|路徑的最小行程號碼支援|路徑型樣所需的最小絕對支援行程號碼|2（必須大於零）|

## 管理結果資料
{: #managedata}

Trajectory Pattern Analysis 服務分析所產生的結果資料除非遭到刪除，否則會儲存在系統中。

若要刪除結果資料，請執行下列動作：

1. 按一下**資料管理** > **行程型樣結果**。即會顯示結果資料。
2. 選取記錄，然後按一下**刪除**。
