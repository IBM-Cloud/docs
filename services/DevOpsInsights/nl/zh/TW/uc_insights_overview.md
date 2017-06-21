---

copyright:
  years: 2017
lastupdated: "2017-03-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# 將 DevOps Insights 與 IBM UrbanCode Deploy 整合 - 概觀
{: #uc_insights_overview}

Delivery Insights 是 {{site.data.keyword.DRA_short}} 的一部分，它會顯示 IBM UrbanCode Deploy 安裝的部署統計資料、度量值及其他相關資訊。例如，它會顯示部署持續時間、成功及失敗等圖表，全部依邏輯分組環境排序。
{:shortdesc}

如果您沒有工具鏈或 {{site.data.keyword.DRA_short}}，則必須先設定 {{site.data.keyword.DRA_short}}：
1. 從 {{site.data.keyword.Bluemix}} 型錄中按一下 **{{site.data.keyword.DRA_short}}**、選取定價方案，然後按一下**建立**。
1. 按一下**管理**標籤，然後在**開始使用 Delivery Insights for UrbanCode** 下，按一下**從這裡開始**。Delivery Insights 會在背景中建立組織的工具鏈。開放式工具鏈是工具整合的集合，在此情況下，IBM UrbanCode Deploy 和 {{site.data.keyword.DRA_short}} 是工具鏈的一部分。如需工具鏈的相關資訊，請參閱[使用工具鏈](../ContinuousDelivery/toolchains_working.html)。
1. 在 **Delivery Insights 設定**頁面中，遵循步驟來設定 DevOps Connect，並連接您的 IBM UrbanCode Deploy 伺服器。
<!--  1. Set up a system to run DevOps Connect. See [prerequisites](uc_insights_prereqs.html).
  1. Download DevOps Connect, which is provided in a runnable JAR file.
  1. Copy the script from the **Delivery Insights Setup** page and run it. This command starts DevOps Connect with a token that allows it to connect to your organization on {{site.data.keyword.Bluemix}}.
  1. Connect your IBM UrbanCode Deploy servers to DevOps connect. See [Connecting IBM UrbanCode Deploy servers to Delivery Insights](uc_insights_connect_ucd.html). -->


如果您已經有工具鏈，請遵循下列步驟來新增 Delivery Insights：
1. 如果您還沒有 {{site.data.keyword.DRA_short}} 工具，請將它新增至工具鏈。
1. 在工具鏈上，按一下 {{site.data.keyword.DRA_short}} 工具。
1. 在 **Delivery Insights 設定**頁面中，遵循步驟來設定 DevOps Connect，並連接您的 IBM UrbanCode Deploy 伺服器。

設定 Delivery Insights 和 DevOps Connect 之後，即可在 Delivery Insights 中顯示 IBM UrbanCode Deploy 伺服器中的資料。請參閱[將 IBM UrbanCode Deploy 伺服器連接至 Delivery Insights](uc_insights_connect_ucd.html)。

<!-- 
For questions or issues, see the [questions forum](https://developer.ibm.com/answers/?community=urbancode).
--> 

![根據 UrbanCode Insights 示範資料的兩個圖表](images/uc_insights_demo_data.gif)

您可以在 Delivery Insights 上看到的部分資訊包括：

- 部署的相關統計資料，包括部署持續時間，以及一段時間的部署量。
- 部署失敗率的相關統計資料（依應用程式及環境分類）。
- 元件部署的相關統計資料，包括失敗率、部署時間及持續時間。

## 系統概觀

Delivery Insights 的拓蹼包括 IBM UrbanCode Deploy <!-- (and optionally IBM UrbanCode Release) --> 的一個以上內部部署安裝，以及 DevOps Connect 公用程式。

下圖顯示這些系統的一般安裝。

![UrbanCode Insights（包括客戶內部部署系統及 IBM Cloud Services）的拓蹼概觀](images/uc_insights_overview_topology_multi_ucd.png)

- **IBM UrbanCode Deploy** 的安裝會提供部署成功和失敗的相關資訊給度量值。IBM UrbanCode Deploy 需要修補程式，才能與 IBM Bluemix DevOps Connect 通訊。

<!--
- **IBM UrbanCode Release** is an optional part of the topology. You can use the environment mappings in IBM UrbanCode Release to set logical environments for reports.

-->

- **IBM Bluemix DevOps Connect**（舊稱 IBM UrbanCode Sync Utility）會協調 IBM UrbanCode Deploy <!-- and IBM UrbanCode Release --> 內部部署安裝與 IBM 管理服務（例如 UrbanCode Insights）之間的通訊。DevOps Connect 使用與內部部署伺服器的安全 HTTPS 通訊以及記號鑑別，來提供資料給 UrbanCode Insights。

  DevOps Connect 需要外掛程式，才能連接至拓蹼中的其他系統。

- **Delivery Insights** 是 {{site.data.keyword.DRA_short}} 的一部分，它會提供 IBM UrbanCode Deploy 上部署活動的相關度量值，包括部署時間和根據環境群組的失敗率。授權是由 {{site.data.keyword.Bluemix}} 帳戶控制。
