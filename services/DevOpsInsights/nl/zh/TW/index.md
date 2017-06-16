---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 開始使用 DevOps Insights（測試版）
{: #gettingstarted}

{{site.data.keyword.DRA_full}} 將開發人員、團隊和部署分析套用至您最忙碌的 DevOps 專案。您可以用它來瞭解團隊符合 DevOps 和開發人員作法的程度、管理程式碼庫中的風險，以及在持續交付專案中自動強制執行品質標準。
{:shortdesc}

{{site.data.keyword.DRA_short}} 包含數組功能：

   * Developer Insights 提供綜合性的方法來探索專案的開發成熟度。您可以識別具有高度錯誤傾向的檔案，並對照開發人員作法獲得專案相符性觀點。

   * Team Dynamics 使用社交編碼分析來幫助您瞭解團隊協同作業的情況，並瞭解如何可以做得更好。

   * Deployment Risk 像是持續交付安全網。它會在部署程序中的指定閘道上，分析單元測試、功能測試、應用程式掃描及程式碼涵蓋面工具的結果，並防止釋出有風險的變更。

   * Delivery Insights 會顯示 IBM UrbanCode Deploy 安裝的部署統計資料、度量值及其他相關資訊。例如，它會顯示部署持續時間、成功及失敗等圖表，全部依邏輯分組環境排序。請參閱[將 DevOps Insights 與 IBM UrbanCode Deploy 整合](/docs/services/DevOpsInsights/uc_insights_overview.html)。

{{site.data.keyword.DRA_short}} 是 Bluemix 開放式工具鏈型錄中的一項整合。如需工具鏈的相關資訊，請參閱[使用工具鏈](/docs/services/ContinuousDelivery/toolchains_working.html)。

若要使用 {{site.data.keyword.DRA_short}}，您必須將它新增至工具鏈。許多工具鏈範本都已包括 {{site.data.keyword.DRA_short}}。此外，也務必[將它新增至 {{site.data.keyword.Bluemix_notm}} 組織作為服務](/docs/services/reqnsi.html)，讓您能夠查看 {{site.data.keyword.DRA_short}} 的相關資訊，以及從 {{site.data.keyword.Bluemix_notm}} 儀表板存取包括它的一些工具鏈範本。  

## 將 DevOps Insights 新增至工具鏈
{: #catalog}

{{site.data.keyword.DRA_short}} 是 {{site.data.keyword.contdelivery_short}} 的一部分。您可以從工具整合型錄中選取 {{site.data.keyword.DRA_short}}，以將它新增至任何工具鏈。

{{site.data.keyword.DRA_short}} 也是許多工具鏈範本的一部分。如果您要從包括 {{site.data.keyword.DRA_short}} 的範本建立工具鏈，請確定 {{site.data.keyword.DRA_short}} 設為**進階**。然後，建立工具鏈，並跳至[使用 Insights](/docs/services/DevOpsInsights/index.html#using)。

若要將 {{site.data.keyword.DRA_short}} 新增至工具鏈，請執行下列動作：

1. 按一下**新增工具**。

2. 按一下 **{{site.data.keyword.DRA_short}}**。

3. 按一下**建立整合**。

現在即可在工具鏈的「概觀」頁面上使用 {{site.data.keyword.DRA_short}}。會自動掃描您的儲存庫和問題追蹤系統是否有資料。 

## 使用 DevOps Insights
{: #using}

如果您的工具鏈包括 GitHub、GitLab 或 JIRA，{{site.data.keyword.DRA_short}} 會在進行一些起始資料收集及分析之後，自動提供程式碼庫和團隊的相關資訊給您。如果工具鏈不包括上述任何整合，請新增其中一項，然後遵循下列步驟：

1. 從工具鏈的「概觀」頁面中，按一下 **{{site.data.keyword.DRA_short}}**。

2. 按一下 **Team Dynamics** 或 **Developer Insights**，然後選擇一個資料種類。 

3. 檢視該資料種類中的儀表板，以探索專案的資料。如果您要進一步瞭解某個圖形，或是瞭解可以使用其資訊做什麼，請按一下**資訊**或**指引**。

探索 Team Dynamics 和 Developer Insights 之後，請[配置 Deployment Risk](/docs/services/DevOpsInsights/insights_risk.html)，以協助您強制執行程式碼品質。Deployment Risk 與 {{site.data.keyword.contdelivery_short}} 管線和 Jenkins 都相容。   
