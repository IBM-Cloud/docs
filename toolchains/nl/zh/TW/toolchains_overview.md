---

copyright:
  years: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 開始使用工具鏈（實驗性）
{: #toolchains_getting_started}

*前次更新：2016 年 6 月 8 日*
{: .last-updated}  

工具鏈是一組可支援開發、部署及操作作業的工具整合。工具鏈的集體力量大於其個別工具整合的總和。
{: shortdesc}

您可以透過兩種方法建立工具鏈：使用範本來建立工具鏈，或從應用程式中建立工具鏈。根據您使用的範本或工具鏈，工具鏈可能包括已移入應用程式入門範本程式碼和預先配置交付管線的 GitHub 儲存庫。將變更推送至工具鏈的 GitHub 儲存庫時，交付管線會自動建置應用程式，並將它部署至 {{site.data.keyword.Bluemix}}。

作為起點，您可以使用工具鏈範本來建立具有一組特定工具整合的工具鏈，或是建立可在其中新增工具整合的空白工具鏈。

**重要事項**：這是實驗性功能。工具鏈可能不穩定，與舊版本不相容的部分也可能會變更。建議不要將它們用於正式作業環境。若要使用工具鏈，您必須進行一次性的[存取要求](https://new-console.ng.bluemix.net/devops?cm_mmc=IBMBluemixGarageMethod-_-MethodSite-_-10-19-15::12-31-18-_-toolchains-welcome-page){: new_window}。工具鏈只適用於美國南部地區。


##從範本建立工具鏈   
{: #creating_a_toolchain_from_a_template}

核准工具鏈存取要求之後，即可使用範本作為起點來建立包含一組特定工具整合的工具鏈。

1. 在 DevOps 儀表板的**工具鏈**標籤上，按一下**建立工具鏈**來建立第一個工具鏈。如果您已有工具鏈，請按一下新增按鈕 (+) 來建立另一個工具鏈。
1. 按一下工具鏈範本。例如，若要使用線上商店範例來建立工具鏈，請按一下**微服務工具鏈**。 
1. 在工具鏈建立頁面上，檢閱即將建立之工具鏈的圖表。此圖會顯示每個工具整合在工具鏈中的生命週期階段。下列影像中的圖表是範例。當您建立工具鏈時，圖表會顯示每一個屬於工具鏈一部分的工具整合。
![工具鏈圖表](images/toolchain_diagram.png)

1. 檢閱工具鏈設定的預設資訊。在 {{site.data.keyword.Bluemix}} 中，可透過工具鏈名稱來識別工具鏈。如果您已有該名稱的工具鏈，或要使用不同的名稱，請變更工具鏈的名稱。  
1. 在「可配置的整合」區段中，選取您要配置給工具鏈的每一個工具整合。如需配置工具整合的相關資訊，請參閱[配置工具整合](../toolchains/toolchains_integrations.html){: new_window}。
1. 按一下**建立**。會自動執行數個步驟來設定工具鏈：

 * 建立工具鏈。
 * 如果您已配置 Delivery Pipeline 工具整合，則會觸發管線。
 * 如果您已配置 Sauce Labs 工具整合，則 Sauce Labs 整合會配置成將工作新增至管線，然後執行測試。
 * 如果您已配置 PagerDuty 工具整合，則 PagerDuty 整合會配置成將通知傳送給您在 Slack 中所配置的通道。這些通知會指出何時發生問題。
 * 如果您已配置 Slack 工具整合，則 Slack 整合會配置成將通知傳送給您在 Slack 中所配置的通道。這些通知會指出部署進度；例如，`Connected with Project XYZ`、`Pipeline Configured` 及 `Stage 'build' started`。
 * 如果您已配置 GitHub 工具整合，則會將範例 GitHub 儲存庫複製到 GitHub 帳戶。


##從應用程式建立工具鏈
{: #creating_a_toolchain_from_an_app}

核准工具鏈存取要求之後，即可從應用程式建立工具鏈。工具鏈可支援持續開發、部署、監視及其他作業，且其與應用程式相關聯。每一個應用程式都可能與工具鏈相關聯。將變更推送至工具鏈的 GitHub 儲存庫時，管線會自動建置及部署應用程式。  

1. 在應用程式之「概觀」頁面的「持續交付」磚上，按一下**新增工具鏈**。或者，在「Bluemix 一般經驗」中，按一下**新增 Git**。您的應用程式會配置成從移入應用程式入門範本程式碼的新 GitHub 儲存庫進行持續交付。
1. 在工具鏈建立頁面上，檢閱即將建立之工具鏈的圖表。此圖會顯示每個工具整合在工具鏈中的生命週期階段。
1. 檢閱工具鏈設定的預設資訊。在 {{site.data.keyword.Bluemix}} 中，可透過工具鏈名稱來識別工具鏈。如果您已有該名稱的工具鏈，或要使用不同的名稱，請變更工具鏈的名稱。
1. 在「可配置的整合」區段中，選取您要配置給工具鏈的每一個工具整合。如需配置工具整合的相關資訊，請參閱[配置工具整合](../toolchains/toolchains_integrations.html){: new_window}。
1. 按一下**建立**。會自動執行數個步驟來設定工具鏈：

 * 建立工具鏈。
 * 如果您已配置 Delivery Pipeline 工具整合，則會觸發管線。
 * 如果您已配置 Sauce Labs 工具整合，則 Sauce Labs 整合會配置成將工作新增至管線，然後執行測試。
 * 如果您已配置 PagerDuty 工具整合，則 PagerDuty 整合會配置成將通知傳送給您在 Slack 中所配置的通道。這些通知會指出何時發生問題。
 * 如果您已配置 Slack 工具整合，則 Slack 整合會配置成將通知傳送給您在 Slack 中所配置的通道。這些通知會指出部署進度；例如，`Connected with Project XYZ`、`Pipeline Configured` 及 `Stage 'build' started`。
 * 如果您已配置 GitHub 工具整合，則會將範例 GitHub 儲存庫複製到 GitHub 帳戶。

 
##檢視工具鏈
{: #viewing_a_toolchain}

配置工具鏈和所有工具整合之後，即可在「工具整合」頁面中檢視工具鏈的視覺化呈現。

1. 在「DevOps 儀表板」的**工具鏈**標籤上，按一下工具鏈來開啟它的「工具整合」頁面。或者，在應用程式之「概觀」頁面的「持續交付」磚上，按一下**檢視工具鏈**，然後按一下**工具整合**。
1. 檢閱頁面來查看工具鏈的視覺化呈現。
1. 若要存取工具鏈中的工具整合，請按一下工具磚。 
 
 **提示**：如果您有多個 GitHub 儲存庫，則相同的工具整合可能會有多個磚，因為每一個儲存庫都需要有它自己的管線。


 <!-- The toolchain in the following image is an example. When you create your own toolchain, the visual representation of the toolchain shows the tool integrations that you configure.
![Sample toolchain](images/toolchain.png) -->


# 相關鏈結
{: #rellinks}

## 指導教學和範例
{: #samples}

* [建立具有三個微服務的應用程式](https://www.ibm.com/devops/method/tutorials/tutorial_microservices_part1){:new_window}

## 相關鏈結
{: #general}

* [Microservices toolchain (Experimental)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Simple toolchain (Experimental)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM&reg; Bluemix&reg; Garage Method](https://www.ibm.com/devops/method){:new_window}
