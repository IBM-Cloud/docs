---

copyright:
  years: 2016
lastupdated: "2016-11-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 開始使用 {{site.data.keyword.DRA_short}}（實驗性）
{: #gettingstarted}

使用 {{site.data.keyword.DRA_full}} 來識別建置及部署的風險。
{:shortdesc}

{{site.data.keyword.DRA_short}} 聚集及分析單元測試、功能測試及程式碼涵蓋面工具的結果，以判斷程式碼是否符合部署處理程序中所指定閘道的預先定義原則。如果您的程式碼不符合或超出原則，則會中止部署，以防止釋出有風險的變更。您可以使用 {{site.data.keyword.DRA_short}} 當作持續交付環境的安全網、實作與改善一段時間品質標準的方式，以及協助您瞭解專案性能的資料視覺化工具。

{{site.data.keyword.DRA_short}} 是實驗性供應項目，僅基於開發及實驗用途來依現狀提供。若要使用 {{site.data.keyword.DRA_short}}，請將它新增至任何使用 {{site.data.keyword.deliverypipeline}} 的工具鏈。

{: #catalog}
若要存取 {{site.data.keyword.DRA_short}} 使用者介面，請從現有工具鏈來完成下列步驟：

1. 按一下**新增工具**按鈕。

2. 按一下 **{{site.data.keyword.DRA_short}}**。

3. 按一下**建立整合**。

4. 按一下 **{{site.data.keyword.DRA_short}}** 磚。

5. 完成其餘作業的設定：

	1. [配置 {{site.data.keyword.deliverypipeline}} 整合](./pipeline_integration.html)。
	2. 執行管線，並[檢閱 {{site.data.keyword.deliverypipeline}} 儀表板](./pipeline_decision_reports.html)。
	3. [定義原則](./create_criteria.html)，以供 {{site.data.keyword.DRA_short}} 管理。
	4. 重新執行管線，以驗證您的專案通過原則。


# 相關鏈結
{: #rellinks}

## 指導教學及範例
{: #samples}

* [使用分析來建議成功部署的可能性](https://www.ibm.com/devops/method/content/deliver/tool_deployment_risk_analytics/){:new_window}

## 相關鏈結
{: #general}

* [開始使用工具鏈](https://new-console.ng.bluemix.net/docs/toolchains/toolchains_overview.html){:new_window}
* [開始使用 Delivery Pipeline](https://new-console.ng.bluemix.net/docs/services/DeliveryPipeline/index.html){:new_window}
* [IBM Bluemix 定價單](https://new-console.ng.bluemix.net/pricing/){:new_window}
* [IBM Bluemix 必要條件](https://developer.ibm.com/bluemix/support/?cm_mc_uid=96503159749414585876298&cm_mc_sid_50200000=1462802909#prereqs){:new_window}
