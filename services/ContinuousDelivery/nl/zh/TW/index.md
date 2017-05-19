---

copyright:
  years: 2015, 2017
lastupdated: "2017-3-31"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 開始使用 Continuous Delivery
{: #cd_getting_started}

使用 {{site.data.keyword.contdelivery_full}} 來採用 DevOps 方式，它包含自動進行應用程式建置及部署的開放式工具鏈。您可以從建立支援開發、部署及操作作業的簡單部署工具鏈開始。
{: shortdesc}

從 {{site.data.keyword.Bluemix_notm}} 型錄選取 {{site.data.keyword.contdelivery_short}} 以建立其實例之後，可以選擇要如何開始使用服務。
 ![Continuous Delivery 歡迎使用頁面](images/cd_landing_page.png)

 * 若要使用自動化管線來快速開始使用及部署應用程式，請在「開始使用管線」區段中，按一下**[從這裡開始](#starting_with_a_pipeline)**。您稍後可以再新增其他工具。
 * 若要從範本來建立及配置持續交付工具鏈，請在「從工具鏈範本開始」區段中，按一下**[從這裡開始](#starting_from_a_toolchain_template)**。工具鏈會整合用於規劃、開發、部署管線以及管理應用程式的工具。您隨時可以從工具鏈新增或移除工具。
 * 如果您已有工具鏈，請在「從工具鏈範本開始」區段中，按一下**檢視工具鏈**。如需使用工具鏈的相關資訊，請參閱[使用工具鏈](/docs/services/ContinuousDelivery/toolchains_using.html){: new_window}。

**提示**：管線是透過工具鏈所管理。您可以將管線新增至現有工具鏈。如果您建立管線，但沒有任何現有工具鏈，系統會為您建立具有預設名稱的工具鏈。使用工具鏈時，只要與其他工具及服務整合，即可擴充管線的功能。

##開始使用管線
{: #starting_with_a_pipeline}

管線會自動進行建置、部署及其他作業。若要開始使用自動化管線，請選取範本，並提供 GitHub 儲存庫的位置。

若要[建立管線 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){:new_window}，且配置成部署 Cloud Foundry 應用程式，請遵循下列步驟：

1. 按一下 **Cloud Foundry**。
1. 如果您要使用不同的管線名稱，請變更其預設名稱。在 {{site.data.keyword.Bluemix_notm}} 中，可透過管線名稱來識別管線。
1. 如果您要使用不同的應用程式名稱，請變更其預設名稱。在 {{site.data.keyword.Bluemix_notm}} 中，可透過應用程式名稱來識別應用程式。此名稱是管線部署至其中的應用程式。
1. 如果您沒有工具鏈，則系統會為您建立具有預設名稱的工具鏈。如果您要使用不同的工具鏈名稱，請變更其名稱。管線是透過工具鏈所管理。使用工具鏈時，只要與其他工具及服務整合，即可延伸管線的功能。

 **提示**：管線及工具鏈屬於組織。如果您隸屬於具有工具鏈的組織，則即使您未建立這些工具鏈，也可以使用它們。

1. 選取您要使用的工具鏈，或鍵入您要建立的新工具鏈的名稱。
1. 選取 Git 提供者。

 **提示**：如果您未授權 {{site.data.keyword.Bluemix_notm}} 存取 GitHub，則系統會提示您按一下**授權**來移至 GitHub 網站。如果您沒有作用中的 GitHub 階段作業，則系統會提示您登入。按一下**授權應用程式**，以容許 {{site.data.keyword.Bluemix_notm}} 存取 GitHub 帳戶。如果您有作用中的 GitHub 階段作業，但最近未輸入過密碼，則系統可能會提示您輸入 GitHub 密碼進行確認。

 如果您未獲授權存取 {{site.data.keyword.ghe_short}} 儲存庫，則必須由具有儲存庫管理者專用權的人員來新增您。如需授權使用 {{site.data.keyword.ghe_short}} 之「{{site.data.keyword.Bluemix_notm}} 專用」的指示，請參閱[開始使用 {{site.data.keyword.ghe_short}} 的 {{site.data.keyword.Bluemix_notm}} 專用](/docs/services/ghededicated/index.html){: new_window}。如果您需要授權使用專屬受管理版本的 {{site.data.keyword.ghe_short}}，請遵循內部程序。

   * 如果您有儲存庫並且想要使用它，請針對儲存庫類型選取**鏈結**。請搜尋儲存庫的位置，或從可用儲存庫清單中選取儲存庫。

   * 如果您要建立空的儲存庫，請針對儲存庫類型選取**新建**。鍵入儲存庫的名稱。

   * 如果您要建立儲存庫的複製品，請針對儲存庫類型選取**複製**。請搜尋儲存庫的位置，或從可用儲存庫清單中選取儲存庫。

   * 如果您要分出儲存庫，以透過取回要求來提出變更，請選取**分出**。請搜尋儲存庫的位置，或從可用儲存庫清單中選取儲存庫。

1. 選取儲存庫，或輸入儲存庫 URL。
1. 按一下**建立**。即會建立、配置管線，並顯示在工具鏈的「概觀」頁面上。
 ![管線卡片](images/cd_pipeline.png)

若要建立沒有任何預先配置階段的[空管線 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window}，請執行下列動作：

1. 按一下**自訂**。
1. 如果您要使用不同的管線名稱，請變更其預設名稱。在 {{site.data.keyword.Bluemix_notm}} 中，可透過管線名稱來識別管線。
1. 如果您沒有工具鏈，則系統會為您建立具有預設名稱的工具鏈。如果您要使用不同的工具鏈名稱，請變更其名稱。管線是透過工具鏈所管理。使用工具鏈時，只要與其他工具及服務整合，即可延伸管線的功能。
1. 選取您要使用的工具鏈，或鍵入您要建立的新工具鏈的名稱。
1. 按一下**建立**。即會建立空管線，並在工具鏈的「概觀」頁面上呈現為卡片。

##從工具鏈範本開始
{: #starting_from_a_toolchain_template}

若要從[範本 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/devops/create){: new_window} 來建立及配置持續交付工具鏈，請執行下列動作：

1. 在**建立工具鏈**頁面上，按一下工具鏈範本。  
1. 檢閱即將建立之工具鏈的圖表。此圖會顯示每個工具整合在工具鏈中的生命週期階段。

 **提示**：有一些工具鏈範本會有多個工具整合實例。例如，「{{site.data.keyword.Bluemix_notm}} 公用」上的「微服務」工具鏈範本包含三個 GitHub 實例及三個 Delivery Pipeline 實例，三個微服務各有一個。

 下列影像中的圖表是範例。當您建立工具鏈時，圖表會顯示每一個屬於工具鏈一部分的工具整合。
![「工具鏈」圖表](images/toolchain_diagram.png)
1. 檢閱工具鏈設定的預設資訊。在 {{site.data.keyword.Bluemix_notm}} 中，可透過工具鏈名稱來識別工具鏈。如果您要使用不同的名稱，請變更工具鏈的名稱。
1. 在「工具整合」區段中，選取您要配置給工具鏈的每一個工具整合。有些工具整合不需要進行配置。如需配置工具整合的相關資訊，請參閱[配置工具整合](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}。
1. 按一下**建立**。會自動執行數個步驟來設定工具鏈。視您選取的工具鏈範本以及使用的是「{{site.data.keyword.Bluemix_notm}} 公用」還是「{{site.data.keyword.Bluemix_notm}} 專用」而定，設定的工具整合會有所不同。例如，當您在「{{site.data.keyword.Bluemix_notm}} 公用」上建立「微服務」工具鏈時，會執行下列步驟：

 * 建立工具鏈。
 * 如果您已配置 Delivery Pipeline，則會建立及執行管線。
 * 如果您已配置 Sauce Labs，則會設定工具鏈將 Sauce Labs 測試工作新增至管線。
 * 如果您已配置 PagerDuty，則會設定工具鏈將警示通知傳送至所指定的 PagerDuty 服務。
 * 如果您已配置 Slack，則會設定工具鏈將部署狀態通知傳送至所指定的 Slack 頻道。
 * 如果您已配置原始碼工具整合（例如 GitHub），則會將範例 GitHub 儲存庫複製到 GitHub 帳戶。
