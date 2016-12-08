---

copyright:
  years: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 開始使用 {{site.data.keyword.contdelivery_short}}
{: #cd_getting_started}

前次更新：2016 年 11 月 18 日
{: .last-updated}  

使用 {{site.data.keyword.contdelivery_full}} 來採用 DevOps 方式，包括自動化應用程式建置及部署的工具鏈。您可以從建立支援開發、部署及操作作業的簡式部署工具鏈開始。
{: shortdesc}

在您從 {{site.data.keyword.Bluemix_notm}} 型錄選取服務磚來建立 {{site.data.keyword.contdelivery_short}} 實例之後，可以選擇要如何開始使用服務。
 ![「持續交付」歡迎使用頁面](images/cd_landing_page.png)

 * 若要使用自動化管線來快速開始使用及部署應用程式，請在「開始使用管線」區段中，按一下**[從這裡開始](#starting_with_a_pipeline)**。您稍後可以再新增其他工具。 
 * 若要從範本來建立及配置持續交付工具鏈，請在「從工具鏈範本開始」區段中，按一下**[從這裡開始](#starting_from_a_toolchain_template)**。工具鏈會整合用於規劃、開發、部署管線以及管理應用程式的工具。您一律可以從工具鏈新增或移除工具。
 * 如果您已有工具鏈，請在「從工具鏈範本開始」區段中，按一下**檢視工具鏈**。如需使用工具鏈的相關資訊，請參閱[在 Bluemix 公用上使用工具鏈](/docs/services/ContinuousDelivery/toolchains_using.html){: new_window}。

##開始使用管線
{: #starting_with_a_pipeline}

管線會自動化建置、部署及其他作業。若要開始使用自動化管線，請選取範本，並提供 GitHub 儲存庫的位置。

若要[建立管線（在新視窗中開啟鏈結）](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window}，而管線配置成部署 Cloud Foundry 應用程式，請遵循下列步驟：

1. 按一下 **Cloud Foundry**。
1. 如果您要使用不同的管線名稱，請變更其預設名稱。在 {{site.data.keyword.Bluemix_notm}} 中，可透過管線名稱來識別管線。 
1. 如果您要使用不同的應用程式名稱，請變更其預設名稱。在 {{site.data.keyword.Bluemix_notm}} 中，可透過應用程式名稱來識別應用程式。此名稱是將管線部署至其中的應用程式。 
1. 如果您沒有工具鏈，則系統會為您建立含有預設名稱的工具鏈。如果您要使用不同的工具鏈名稱，請變更其名稱。管線是透過工具鏈所管理。使用工具鏈時，只要與其他工具及服務整合，即可延伸管線的功能。 

 **提示**：管線及工具鏈屬於組織。如果您隸屬於包含工具鏈的組織，則可以使用這些工具鏈，即使您並未建立它們。
 
1. 選取您要使用的工具鏈，或鍵入您要建立的新工具鏈的名稱。
1. 提供 GitHub 儲存庫的位置。

 **提示**：如果您未授權 {{site.data.keyword.Bluemix_notm}} 存取 GitHub，則系統會提示您按一下**授權**來移至 GitHub 網站。如果您沒有作用中的 GitHub 階段作業，則系統會提示您登入。按一下**授權應用程式**，以容許 {{site.data.keyword.Bluemix_notm}} 存取 GitHub 帳戶。如果您有作用中的 GitHub 階段作業，但最近未輸入過密碼，則系統可能會提示您輸入 GitHub 密碼進行確認。

   * 如果您有 GitHub 儲存庫並且想要使用它，請針對儲存庫類型選取**鏈結**。請搜尋儲存庫的位置，或從可用儲存庫清單中選取儲存庫。
   
   * 如果您要建立空的 GitHub 儲存庫，請針對儲存庫類型選取**新建**。鍵入儲存庫的名稱。
   
   * 如果您要建立 GitHub 儲存庫的複製品，請針對儲存庫類型選取**複製**。請搜尋儲存庫的位置，或從可用儲存庫清單中選取儲存庫。
   
   * 如果您要分出 GitHub 儲存庫，以透過取回要求來提出變更，請選取**分出**。請搜尋儲存庫的位置，或從可用儲存庫清單中選取儲存庫。
 
1. 按一下**建立**。即會在工具鏈的「概觀」頁面上建立、配置及顯示管線。
 ![「管線」磚](images/cd_pipeline.png)
 
若要建立沒有任何預先配置階段的[空管線（在新視窗中開啟鏈結）](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window}，請執行下列動作：

1. 按一下**自訂**。
1. 如果您要使用不同的管線名稱，請變更其預設名稱。在 {{site.data.keyword.Bluemix_notm}} 中，可透過管線名稱來識別管線。 
1. 如果您沒有工具鏈，則系統會為您建立含有預設名稱的工具鏈。如果您要使用不同的工具鏈名稱，請變更其名稱。管線是透過工具鏈所管理。使用工具鏈時，只要與其他工具及服務整合，即可延伸管線的功能。
1. 選取您要使用的工具鏈，或鍵入您要建立的新工具鏈的名稱。
1. 按一下**建立**。即會建立空管線，並在工具鏈的「概觀」頁面上呈現為磚。

##從工具鏈範本開始
{: #starting_from_a_toolchain_template}

若要從[範本（在新視窗中開啟鏈結）](https://console.ng.bluemix.net/devops/create){: new_window}來建立及配置持續交付工具鏈，請執行下列動作：

1. 在**建立工具鏈**頁面上，按一下工具鏈範本。  
1. 檢閱即將建立之工具鏈的圖表。此圖會顯示每個工具整合在工具鏈中的生命週期階段。下列影像中的圖表是範例。當您建立工具鏈時，圖表會顯示每一個屬於工具鏈一部分的工具整合。
![「工具鏈」圖表](images/toolchain_diagram.png)
1. 檢閱工具鏈設定的預設資訊。在 {{site.data.keyword.Bluemix_notm}} 中，可透過工具鏈名稱來識別工具鏈。如果您要使用不同的名稱，請變更工具鏈的名稱。
1. 在「可配置的整合」區段中，選取您要配置給工具鏈的每一個工具整合。有些工具整合不需要進行配置。如需配置工具整合的相關資訊，請參閱[配置工具整合](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}。
1. 按一下**建立**。會自動執行數個步驟來設定工具鏈：

 * 建立工具鏈。
 * 如果您已配置 Delivery Pipeline 工具整合，則會建立及觸發管線。
 * 如果您已配置 Sauce Labs 工具整合，則 Sauce Labs 設定成將工作新增至管線，然後執行測試。
 * 如果您已配置 PagerDuty 工具整合，則 PagerDuty 設定成將警示通知傳送至您所指定的服務。 
 * 如果您已配置 Slack 工具整合，則 Slack 設定成將部署狀態通知傳送至您所指定的通道。 
 * 如果您已配置 GitHub 工具整合，則會將範例 GitHub 儲存庫複製到 GitHub 帳戶。 

# 相關鏈結
{: #rellinks}

## 指導教學及範例
{: #samples}

* [建立及使用第一個工具鏈（在新視窗中開啟鏈結）](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_flow){:new_window}
* [建立自訂工具鏈（在新視窗中開啟鏈結）](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_custom){:new_window}
* [建立具有三個微服務的應用程式（在新視窗中開啟鏈結）](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_microservices){:new_window}

## 相關鏈結
{: #general}

* [微服務工具鏈（在新視窗中開啟鏈結）](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [簡式工具鏈（在新視窗中開啟鏈結）](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM Bluemix Garage Method（在新視窗中開啟鏈結）](https://www.ibm.com/devops/method){:new_window}
