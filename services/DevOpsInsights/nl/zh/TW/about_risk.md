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

# 關於 Deployment Risk

{{site.data.keyword.DRA_short}} 針對部署提供豐富的相關資訊，尤其是風險。您可以利用它，透過原則和閘道將 Delivery Pipeline 中的品質保護作業自動化。
{:shortdesc}

從工具鏈開啟 {{site.data.keyword.DRA_short}} 之後，按一下 **Deployment Risk**。您可以從這裡取得編譯打包和正式作業環境中的應用程式概觀，並往下探查，以瞭解程式碼涵蓋面、測試效能和安全報告。儀表板會自動移入管線的 {{site.data.keyword.DRA_short}} 測試中的最新資訊。

Deployment Risk 可讓您透過原則和閘道，在工具鏈中強制執行品質標準。原則包含規則集；閘道可強制執行原則。例如，您可以建立「單元測試和測試涵蓋面」原則，要求建置需符合單元測試和測試涵蓋面標準。然後，將參照該原則的閘道新增至持續交付程序。不符合原則的建置會在該閘道被阻擋下來。 

## 整合資訊

Deployment Risk 會與 {{site.data.keyword.deliverypipeline}}（隸屬於 {{site.data.keyword.contdelivery_full}}）和 Jenkins 專案整合。使用其中任一項的方法大致都相同。  

如果是使用 {{site.data.keyword.deliverypipeline}}，請遵循下列步驟：

1. [建立原則和規則](risk_policies.html)，以供 {{site.data.keyword.DRA_short}} 管理。
2. [準備管線的階段](risk_cd.html)，以與 {{site.data.keyword.DRA_short}} 整合。
3. 在管線中[建立或編輯測試工作](risk_cd.html)，以將結果上傳至 {{site.data.keyword.DRA_short}}。
4. [新增閘道](risk_cd.html)至管線，以根據那些結果和您的原則來制定升級決策。
5. 執行管線並[檢視結果](results.html)。

如果是使用 Jenkins，請遵循下列步驟：

1. [建立原則和規則](risk_policies.html)，以供 {{site.data.keyword.DRA_short}} 管理。
2. [安裝並配置 Jenkins 外掛程式](risk_jenkins.html)。
3. [依照外掛程式指示的說明來建立測試工作和閘道](risk_jenkins.html)。測試會將結果上傳至 {{site.data.keyword.DRA_short}} 以進行分析，而閘道會使用那些結果來制定升級決策。
4. 執行專案並[檢視結果](results.html)。 

無論您如何建置及部署程式碼，結果皆相同：符合標準的建置將會通過 Deployment Risk 閘道，而不符合標準的建置就會被阻擋下來。 

## 必要條件
{: #prerequisites}

除了[開始使用 {{site.data.keyword.DRA_short}}](/docs/services/DevOpsInsights/index.html) 中所說明的內容，Deployment Risk 還需要一些配置。

若要使用 Deployment Risk，您需要以下兩項：

* {{site.data.keyword.deliverypipeline}} 實例或 Jenkins 專案
* 您要用來評估專案的測試
