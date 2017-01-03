---

copyright:
  years: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 使用工具鏈
{: #toolchains_getting_started}

前次更新：2016 年 11 月 17 日
{: .last-updated}  

*工具鏈* 是一組可支援開發、部署及操作作業的工具整合。工具鏈的集體力量大於其個別工具整合的總和。
{: shortdesc}

工具鏈適用於 {{site.data.keyword.Bluemix}} 的「公用」及「專用」環境。您可以透過兩種方法建立工具鏈：使用範本來建立工具鏈，或從應用程式中建立工具鏈。在「{{site.data.keyword.Bluemix_notm}} 公用」上，工具鏈只適用於美國南部地區。


##開始使用工具鏈：公用
{: #getting_started_public}

每一個工具鏈都會與特定組織相關聯，而且任何屬於該組織成員的使用者都可以存取其相關聯的工具鏈。建立工具鏈之前，請確定您是在要建立工具鏈的組織中工作。您目前在其中工作的組織顯示在功能表列中。若要切換至另一個組織，請按一下功能表列中的該組織，然後選取您要切換至的組識。

###從範本建立工具鏈   
{: #creating_a_toolchain_from_a_template}

您可以使用範本作為起點來[建立工具鏈（在新視窗中開啟鏈結）](https://console.ng.bluemix.net/devops/create){: new_window}，而此工具鏈包括一組特定工具整合。進一步瞭解如何使用 [IBM Bluemix Garage Method（在新視窗中開啟鏈結）](https://www.ibm.com/devops/method/category/tools){:new_window}中的範本。

1. 登入 [{{site.data.keyword.Bluemix_notm}}（在新視窗中開啟鏈結）](http://console.ng.bluemix.net){:new_window}。{{site.data.keyword.Bluemix_notm}}「儀表板」即會開啟並顯示組織的作用中 {{site.data.keyword.Bluemix_notm}} 空間的概觀。
1. 從漢堡式功能表中，按一下**服務**，然後按一下 **DevOps**。
1. 在 DevOps 儀表板的**工具鏈**頁面上，按一下**建立工具鏈**。
1. 在**建立工具鏈**頁面上，按一下工具鏈範本。
1. 檢閱即將建立之工具鏈的圖表。此圖會顯示每個工具整合在工具鏈中的生命週期階段。下列影像中的圖表是範例。當您建立工具鏈時，圖表會顯示每一個屬於工具鏈一部分的工具整合。
![工具鏈圖表](images/toolchain_diagram.png)

1. 檢閱工具鏈設定的預設資訊。在 {{site.data.keyword.Bluemix_notm}} 中，可透過工具鏈名稱來識別工具鏈。如果您要使用不同的名稱，請變更工具鏈的名稱。  
1. 在「可配置的整合」區段中，選取您要配置給工具鏈的每一個工具整合。有些工具整合不需要進行配置。如需配置工具整合的相關資訊，請參閱[配置工具整合](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}。
1. 按一下**建立**。會自動執行數個步驟來設定工具鏈：

 * 建立工具鏈。
 * 如果您已配置 Delivery Pipeline 工具整合，則會建立及觸發管線。
 * 如果您已配置 Sauce Labs 工具整合，則 Sauce Labs 設定成將工作新增至管線，然後執行測試。
 * 如果您已配置 PagerDuty 工具整合，則 PagerDuty 設定成將警示通知傳送至您所指定的服務。
 * 如果您已配置 Slack 工具整合，則 Slack 設定成將部署狀態通知傳送至您所指定的通道。
 * 如果您已配置 GitHub 工具整合，則會將範例 GitHub 儲存庫複製到 GitHub 帳戶。


###從應用程式建立工具鏈
{: #creating_a_toolchain_from_an_app}

您可以從應用程式建立工具鏈。工具鏈可支援持續開發、部署、監視及其他作業，且其與應用程式相關聯。每一個應用程式都可能與工具鏈相關聯。將變更推送至工具鏈的 GitHub 儲存庫時，管線會自動建置及部署應用程式。  

1. 在應用程式之「概觀」頁面的「持續交付」磚上，按一下**啟用**。您的應用程式會配置成從移入應用程式入門範本程式碼的新 GitHub 儲存庫進行持續交付。
1. 在工具鏈建立頁面上，檢閱即將建立之工具鏈的圖表。此圖會顯示每個工具整合在工具鏈中的生命週期階段。
1. 檢閱工具鏈設定的預設資訊。在 {{site.data.keyword.Bluemix_notm}} 中，可透過工具鏈名稱來識別工具鏈。如果您要使用不同的名稱，請變更工具鏈的名稱。
1. 在「可配置的整合」區段中，選取您要配置給工具鏈的每一個工具整合。有些工具整合不需要進行配置。如需配置工具整合的相關資訊，請參閱[配置工具整合](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}。
1. 按一下**建立**。會自動執行數個步驟來設定工具鏈：

 * 建立工具鏈。
 * 如果您已配置 Delivery Pipeline 工具整合，則會建立及觸發管線。
 * 如果您已配置 Sauce Labs 工具整合，則 Sauce Labs 設定成將工作新增至管線，然後執行測試。
 * 如果您已配置 PagerDuty 工具整合，則 PagerDuty 設定成將警示通知傳送至您所指定的服務。
 * 如果您已配置 Slack 工具整合，則 Slack 設定成將部署狀態通知傳送至您所指定的通道。
 * 如果您已配置 GitHub 工具整合，則會將範例 GitHub 儲存庫複製到 GitHub 帳戶。


##開始使用工具鏈：專用
{: #getting_started_dedicated}

每一個工具鏈都會與特定組織相關聯，而且任何屬於該組織成員的使用者都可以存取其相關聯的工具鏈。建立工具鏈之前，請按一下功能表列中的**{{site.data.keyword.avatar}}**圖示來開啟「帳戶及支援」小組件，以及檢視您在其中工作的組織。如果該組織不是您要建立工具鏈的組織，請切換至另一個組織。

###從範本建立工具鏈   
{: #creating_a_toolchain_from_a_template_dedicated}

您可以使用範本作為起點來建立包括一組特定工具整合的工具鏈。

1. 在「{{site.data.keyword.Bluemix_notm}} 儀表板」的 **DevOps** 標籤上，按一下新增按鈕 (+) 來建立工具鏈。
1. 在**建立工具鏈**頁面上，按一下工具鏈範本。 
1. 檢閱即將建立之工具鏈的圖表。此圖會顯示每個工具整合在工具鏈中的生命週期階段。下列影像中的圖表是範例。當您建立工具鏈時，圖表會顯示每一個屬於工具鏈一部分的工具整合。
![專用工具鏈圖表](images/toolchain_dedicated_diagram.png)

1. 檢閱工具鏈設定的預設資訊。在 {{site.data.keyword.Bluemix_notm}} 中，可透過工具鏈名稱來識別工具鏈。如果您已有該名稱的工具鏈，或要使用不同的名稱，請變更工具鏈的名稱。  
1. 在「可配置的整合」區段中，選取您要配置給工具鏈的每一個工具整合。有些工具整合不需要進行配置。如需配置工具整合的相關資訊，請參閱[配置工具整合](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}。
1. 按一下**建立**。會自動執行數個步驟來設定工具鏈：

 * 建立工具鏈。
 * 如果您已配置 Delivery Pipeline 工具整合，則會建立及觸發管線。
 * 如果您已配置 PagerDuty 工具整合，則 PagerDuty 設定成將警示通知傳送至您所指定的服務。
 * 如果您已配置 Slack 工具整合，則 Slack 設定成將部署狀態通知傳送至您所指定的通道。
 * 如果您已配置 GitHub Enterprise 工具整合，則會將範例 GitHub Enterprise 儲存庫複製到 GitHub Enterprise 帳戶。


###從應用程式建立工具鏈
{: #creating_a_toolchain_from_an_app_dedicated}

您可以從應用程式建立工具鏈。工具鏈可支援持續開發、部署、監視及其他作業，且其與應用程式相關聯。每一個應用程式都可能與工具鏈相關聯。將變更推送至工具鏈的 GitHub Enterprise 儲存庫時，管線會自動建置及部署應用程式。  

1. 在應用程式之「概觀」頁面的右上角，按一下**新增工具鏈**。您的應用程式會配置成從移入應用程式入門範本程式碼的新 GitHub Enterprise 儲存庫進行持續交付。
1. 在工具鏈建立頁面上，檢閱即將建立之工具鏈的圖表。此圖會顯示每個工具整合在工具鏈中的生命週期階段。
1. 檢閱工具鏈設定的預設資訊。在 {{site.data.keyword.Bluemix_notm}} 中，可透過工具鏈名稱來識別工具鏈。如果您已有該名稱的工具鏈，或要使用不同的名稱，請變更工具鏈的名稱。
1. 在「可配置的整合」區段中，選取您要配置給工具鏈的每一個工具整合。有些工具整合不需要進行配置。如需配置工具整合的相關資訊，請參閱[配置工具整合](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}。
1. 按一下**建立**。會自動執行數個步驟來設定工具鏈：

 * 建立工具鏈。
 * 如果您已配置 Delivery Pipeline 工具整合，則會建立及觸發管線。
 * 如果您已配置 PagerDuty 工具整合，則 PagerDuty 設定成將警示通知傳送至您所指定的服務。
 * 如果您已配置 Slack 工具整合，則 Slack 設定成將部署狀態通知傳送至您所指定的通道。
 * 如果您已配置 GitHub Enterprise 工具整合，則會將範例 GitHub Enterprise 儲存庫複製到 GitHub Enterprise 帳戶。


##檢視工具鏈
{: #viewing_a_toolchain}

在您配置工具鏈及其工具整合之後，即可檢視工具鏈的視覺化呈現。

* 如果您使用「{{site.data.keyword.Bluemix_notm}} 公用」，請在 DevOps 儀表板的**工具鏈**頁面上，按一下工具鏈來開啟其「概觀」頁面。或者，在應用程式之「概觀」頁面的「持續交付」磚上，按一下**檢視工具鏈**。然後，按一下**概觀**。 
   
* 如果您使用「{{site.data.keyword.Bluemix_notm}} 專用」，請在「儀表板」的 **DevOps** 標籤上，按一下工具鏈來開啟它的「工具整合」頁面。或者，在應用程式之「概觀」頁面的右上角，按一下**檢視工具鏈**。

* 若要存取工具鏈中的工具整合，請按一下工具的磚。 
 
 **提示**：如果您有多個 GitHub 或 GitHub Enterprise 儲存庫，則相同的工具整合可能會有多個磚，因為每一個儲存庫都會以它自己的磚來呈現。


# 相關鏈結
{: #rellinks}

## 指導教學和範例
{: #samples}

* [建立及使用第一個工具鏈（在新視窗中開啟鏈結）](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_flow){:new_window}
* [建立自訂工具鏈（在新視窗中開啟鏈結）](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_custom){:new_window}
* [建立具有三個微服務的應用程式（在新視窗中開啟鏈結）](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_microservices){:new_window}
* [從 {{site.data.keyword.Bluemix_notm}} 專用的範本建立工具鏈（測試版）（在新視窗中開啟鏈結）](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_template_flow){:new_window}
* [從 {{site.data.keyword.Bluemix_notm}} 專用的應用程式建立工具鏈（測試版）（在新視窗中開啟鏈結）](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_app_flow){:new_window}

## 相關鏈結
{: #general}

* [微服務工具鏈（在新視窗中開啟鏈結）](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [簡式工具鏈（在新視窗中開啟鏈結）](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM Bluemix Garage Method（在新視窗中開啟鏈結）](https://www.ibm.com/devops/method){:new_window}
