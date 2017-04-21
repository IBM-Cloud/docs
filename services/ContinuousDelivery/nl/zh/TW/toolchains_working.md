---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-7"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 建立工具鏈
{: #toolchains_getting_started}

*工具鏈* 是一組可支援開發、部署及操作作業的工具整合。工具鏈的集體力量大於其個別工具整合的總和。
{: shortdesc}

開放式工具鏈適用於 {{site.data.keyword.Bluemix}} 的「公用」及「專用」環境。您可以使用兩種方式來建立工具鏈：使用範本來建立工具鏈，或從應用程式建立工具鏈。在「{{site.data.keyword.Bluemix_notm}} 公用」上，工具鏈只適用於美國南部地區。


每一個工具鏈都會與特定組織相關聯，而且任何屬於該組織成員的使用者都可以新增至其任何關聯工具鏈的存取控制清單。如需工具鏈存取控制的相關資訊，請參閱[管理存取權](/docs/services/ContinuousDelivery/toolchains_using.html#managing_access){: new_window}。建立工具鏈之前，請確定您是在要建立工具鏈的組織中工作。您在其中工作的組織會顯示在功能表列上。若要切換至另一個組織，請按一下功能表列中的該組織，然後選取您要切換至的組識。


##從範本建立工具鏈   
{: #creating_a_toolchain_from_a_template}

您可以使用範本作為起點來[建立工具鏈 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/devops/create){: new_window}，而此工具鏈包括一組特定的工具整合。進一步瞭解如何使用 [IBM Cloud Garage Method ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/devops/method/category/tools){:new_window} 中的範本。

1. 如果您使用「{{site.data.keyword.Bluemix_notm}} 公用」，請登入 [{{site.data.keyword.Bluemix_notm}} ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://console.ng.bluemix.net){:new_window}。
1. 如果您使用「{{site.data.keyword.Bluemix_notm}} 專用」，請登入 {{site.data.keyword.Bluemix_notm}} 的「專用」環境。
1. 從漢堡式功能表中，按一下**服務**，然後按一下 **DevOps**。
1. 在 DevOps 儀表板的**工具鏈**頁面上，按一下**建立工具鏈**。
1. 在**建立工具鏈**頁面上，按一下工具鏈範本。
1. 檢閱即將建立之工具鏈的圖表。此圖會顯示每個工具整合在工具鏈中的生命週期階段。

 **提示**：有一些工具鏈範本會有多個工具整合實例。例如，「{{site.data.keyword.Bluemix_notm}} 公用」上的「微服務」工具鏈範本包含三個 GitHub 實例及三個 Delivery Pipeline 實例，三個微服務各有一個。

 下列影像中的圖表是範例。當您建立工具鏈時，圖表會顯示每一個屬於工具鏈一部分的工具整合。
![工具鏈圖表](images/toolchain_diagram.png)

1. 檢閱工具鏈設定的預設資訊。在 {{site.data.keyword.Bluemix_notm}} 中，可透過工具鏈名稱來識別工具鏈。如果您要使用不同的名稱，請變更工具鏈的名稱。  
1. 在「工具整合」區段中，選取您要配置給工具鏈的每一個工具整合。有些工具整合不需要進行配置。如需配置工具整合的相關資訊，請參閱[配置工具整合](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}。
1. 按一下**建立**。會自動執行數個步驟來設定工具鏈。根據您選取的工具鏈範本以及使用的是「{{site.data.keyword.Bluemix_notm}} 公用」還是「{{site.data.keyword.Bluemix_notm}} 專用」，設定的工具整合會有所不同。例如，當您在「{{site.data.keyword.Bluemix_notm}} 公用」上建立「微服務」工具鏈時，會執行下列步驟：

 * 建立工具鏈。
 * 如果您已配置 Delivery Pipeline，則會建立及觸發管線。
 * 如果您已配置 Sauce Labs，則會設定工具鏈將 Sauce Labs 測試工作新增至管線。
 * 如果您已配置 PagerDuty，則會設定工具鏈將警示通知傳送至所指定的 PagerDuty 服務。
 * 如果您已配置 Slack，則會設定工具鏈將部署狀態通知傳送至所指定的 Slack 頻道。
 * 如果您已配置原始碼工具整合（例如 GitHub），則會將範例 GitHub 儲存庫複製到 GitHub 帳戶。


##從應用程式建立工具鏈
{: #creating_a_toolchain_from_an_app}

您可以從應用程式建立工具鏈。工具鏈可支援持續開發、部署、監視及其他作業，且其與應用程式相關聯。每一個應用程式都可能與工具鏈相關聯。將變更推送至工具鏈的 GitHub 或 {{site.data.keyword.ghe_short}} 儲存庫時，管線會自動建置及部署應用程式。  

1. 在應用程式之「概觀」頁面的「持續交付」卡上，按一下**啟用**。如果您使用「{{site.data.keyword.Bluemix_notm}} 公用」，應用程式會配置成從已移入應用程式入門範本程式碼的新 GitHub 儲存庫進行持續交付。如果您使用「{{site.data.keyword.Bluemix_notm}} 專用」，應用程式會配置成從已移入應用程式入門範本程式碼的新 GitHub 或 {{site.data.keyword.ghe_short}} 儲存庫進行持續交付。
1. 在工具鏈建立頁面上，檢閱即將建立之工具鏈的圖表。此圖會顯示每個工具整合在工具鏈中的生命週期階段。
1. 檢閱工具鏈設定的預設資訊。在 {{site.data.keyword.Bluemix_notm}} 中，可透過工具鏈名稱來識別工具鏈。如果您要使用不同的名稱，請變更工具鏈的名稱。
1. 在「工具整合」區段中，選取您要配置給工具鏈的每一個工具整合。有些工具整合不需要進行配置。如需配置工具整合的相關資訊，請參閱[配置工具整合](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}。
1. 按一下**建立**。會自動執行數個步驟來設定工具鏈。根據您是在「{{site.data.keyword.Bluemix_notm}} 公用」還是「{{site.data.keyword.Bluemix_notm}} 專用」上使用工具鏈，設定的工具整合會有所不同。例如，當您從「{{site.data.keyword.Bluemix_notm}} 公用」的應用程式建立工具鏈時，會執行下列步驟：

 * 建立工具鏈。
 * 如果您已配置 Delivery Pipeline，則會建立及觸發管線。
 * 如果您已配置 GitHub，則會將範例 GitHub 儲存庫複製到 GitHub 帳戶。


##檢視工具鏈
{: #viewing_a_toolchain}

在您配置工具鏈及其工具整合之後，即可檢視工具鏈的視覺化呈現。

1. 在 DevOps 儀表板的**工具鏈**頁面上，按一下工具鏈來開啟其「概觀」頁面。或者，在應用程式之「概觀」頁面的「持續交付」卡上，按一下**檢視工具鏈**。然後，按一下**概觀**。
2. 若要存取工具鏈中的工具整合，請按一下工具。

 **提示**：如果您有多個 GitHub、{{site.data.keyword.ghe_short}} 或 Git 儲存庫，則相同的工具整合可能會有多個卡片，因為每一個儲存庫都會以它自己的卡片來呈現。如果您有多個管線，則相同的工具整合可能會有多個卡片，因為每一個管線都會以它自己的卡片來呈現。例如，當您建立「微服務」工具鏈時，三個微服務各有其專屬 GitHub、{{site.data.keyword.ghe_short}} 或 Git 儲存庫，以及其專屬管線。
