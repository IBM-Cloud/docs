---

copyright:
  years: 2016

---
<!-- Copyright info at top of file: REQUIRED
    The copyright info is YAML content that must occur at the top of the MD file, before attributes are listed.
    It must be surrounded by 3 dashes.
    The value "years" can contain just one year or a two years separated by a comma. (years: 2014, 2016)
    Indentation as per the previous template must be preserved.
-->

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 從管線建置及部署
{: #deliverypipeline_build_deploy}
前次更新：2016 年 8 月 29 日
{: .last-updated}

IBM&reg; Bluemix&reg; {{site.data.keyword.deliverypipeline}} 服務可讓您實作可重複的持續整合及持續交付程序。
{:shortdesc}

請完成下列作業來建立及配置管線。

## 新增階段
{: #deliverypipeline_add_stage}

1. 在「管線：所有階段」頁面上，按一下**新增階段**。即會開啟「階段配置」頁面。
2. 配置階段。
  1. 在**輸入**標籤上，選取階段的輸入。
  2. 在**工作**標籤上，新增及配置至少一個工作。第一個階段通常至少會有一個建置工作。
3. 按一下**儲存**。

## 將工作新增至階段
{: #deliverypipeline_add_job}

1. 在階段上，按一下**階段配置**圖示，然後按一下**配置階段**。
2. 按一下**工作**標籤。
3. 按一下**新增工作**。選取要新增的工作類型。
4. 配置工作。
5. 按一下**儲存**。

![將工作新增至階段](./images/AddJob.png)

## 執行階段
{: #deliverypipeline_run_stage}

按一下「管線：所有階段」頁面上的**執行階段**圖示，即可手動執行階段。

![按一下階段上的「執行階段」圖示](./images/RunStage.png)

您也可以使用下列兩種方法的其中一種，從建置歷程頁面中要求依需求建置及部署：
* 將建置拖曳至所配置階段下的方框。
* 在建置旁邊，按一下**傳送至**圖示，然後選取要部署至的空間。
  ![具有此建置圖示的「執行」階段](./images/deploy_to.png)

若要取消執行中階段，請按一下階段上的**檢視日誌及歷程**。在工作清單中，按一下執行中工作的號碼，然後按一下**取消**。按一下工作，然後按一下**取消**，或者按一下其階段上工作旁邊的**停止**圖示，也可以個別取消工作。

## 部署應用程式
{: #deliverypipeline_deploy}

只要執行工作，適當配置的部署工作就會將應用程式部署至目標。若要手動執行部署工作，請按一下工作所在階段的**執行階段**圖示。

###輸入修訂
當您手動執行階段時，或者它是在階段完成之前執行，則執行中階段會選取其輸入修訂。輸入修訂通常是建置號碼。若要選取輸入修訂，則階段會遵循此程序：

1. 如果選取特定修訂，即使用它。
2. 如果未指定特定修訂，請在找到使用相同輸入的階段之前搜尋先前的階段。請尋找並使用該輸入的最後成功執行修訂。
3. 如果未指定特定修訂，而且沒有其他階段使用所指定的來源作為輸入，則請使用輸入的最新修訂。

**提示：**您可以部署前一個建置。在包含建置的階段上，按一下**檢視日誌及歷程**。在開啟的頁面上，按一下以展開執行號碼，然後按一下建置工作。按一下**傳送至**，然後選取目標。

###將服務新增至應用程式
您可以將服務新增至您的應用程式，以及從「Bluemix 儀表板」或 Cloud Foundry 指令行介面 (CLI) 來管理這些服務。您也可以在 DevOps Services 管線工作的 Script 中發出 Cloud Foundry CLI 指令。例如，您可以在部署工作的 Script 中將服務新增至應用程式。如需新增服務的相關資訊，請參閱[將服務新增至應用程式](https://www.ng.bluemix.net/docs/services/reqnsi.html#add_service)。

## 檢視日誌
{: #deliverypipeline_view_logs}

您可以在「階段歷程」頁面上檢視工作的日誌，以及檢視其執行的階段。

若要檢視工作的日誌，請按一下工作。或者，按一下階段上的**檢視日誌及歷程**。

若要檢視所部署應用程式的運行環境日誌，請按一下**檢視運行環境日誌**。

![階段磚中可按一下以開啟相關日誌的區域](./images/view_logs_and_history.png)

除了工作日誌之外，您還可以檢視任何建置工作的單元測試結果、所產生的構件，以及程式碼變更。

您也可以從「階段歷程」頁面執行、取消或配置階段。在頁面頂端，按一下**執行**來執行階段，或按一下**配置**來配置階段。在階段執行時，按一下執行號碼，然後按一下「取消」，即可予以取消。

![在「階段歷程」頁面上按一下階段執行號碼來選取階段](./images/click_stage_run_number.png)

<!--
[1]: https://www.ng.bluemix.net/docs/manageapps/deployingapps.html#appmanifest
[2]: https://www.ng.bluemix.net/docs/#services/DeliveryPipeline/index.html#getstartwithCD
[3]: http://docs.cloudfoundry.org/devguide/installcf/whats-new-v6.html#push
[4]: https://console.ng.bluemix.net/?ace_base=true/#/pricing/cloudOEPaneId=pricing
[5]: ./images/open_logs.png
[6]: #manifests
[7]: ./images/runbar-annotated-dark.png
[8]: ./images/input_tab_only_execute.png
[9]: ./images/deploy_to.png
[10]: ./images/view_logs_and_history.png
[11]: ./images/play_button.png
[12]: ./images/basicAnimate.gif
[13]: ./images/AddStage.png
[14]: ./images/AddJob.png
[15]: ./images/jobs.png
[16]: ./images/RunStage.png
[17]: https://www.ng.bluemix.net/docs/starters/container_pipeline.html#container_pipeline
[18]: ../../../tutorials/basicbuild
[19]: #add_stage
[20]: #add_job
[21]: ../deploy_ext
[22]: ./images/pipeline_settings_icon.png
[23]: https://www.ng.bluemix.net/docs/services/reqnsi.html#add_service
[24]: ../deploy_var
[25]: ./images/click_stage_run_number.png
[26]: ./images/diagram.jpg

-->
