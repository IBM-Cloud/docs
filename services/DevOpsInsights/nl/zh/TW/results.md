---

copyright:
  years: 2016, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 檢視結果

## Deployment Risk 評估

管線執行之後，{{site.data.keyword.DRA_short}} 會開始收集並分析其測試結果，以建立基準線。收集每個後續執行的資料，並將其與先前的結果進行比較。決策閘道使用此資料來判斷何時停止部署。 

您可以從 Deployment Risk 儀表板查看部署和閘道評估資料。若要開啟儀表板，請開啟 {{site.data.keyword.DRA_short}}，然後從側邊功能表中按一下 **Deployment Risk**。

如果您是使用 {{site.data.keyword.contdelivery_short}} 管線，則可從管線本身檢視個別閘道執行報告。若要從管線檢視閘道的決策報告，請完成下列步驟：

1. 在包含要檢查之閘道的階段上，按一下 **View logs and history**。

2. 從包含閘道的工作中，按一下閘道的名稱。

3. 在日誌視圖中，尋找 `Check {{site.data.keyword.DRA_short}} report here` 訊息，然後按一下鏈結來開啟報告。

## Developer Insights 和 Team Dynamics 報告

您可以在起始資料採礦期間過後，檢視團隊和程式碼的相關儀表板。在服務導覽功能表中，按一下 **Developer Insights** 或 **Team Dynamics**，然後選取資料種類來檢視此資訊。
