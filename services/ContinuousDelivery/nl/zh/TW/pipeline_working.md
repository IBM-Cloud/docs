---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-6"

---


{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}

# 使用 {{site.data.keyword.deliverypipeline}} {: #pipeline-working}

若要自動建置及部署至 {{site.data.keyword.Bluemix}}，請使用 {{site.data.keyword.deliverypipeline}} for {{site.data.keyword.Bluemix_notm}}。
{: shortdesc}

使用 {{site.data.keyword.deliverypipeline}}，有數種建置類型可供您選擇。您提供建置 Script，{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}} 便會執行它，不需要設定建置系統。接著只要按一下，您便可將應用程式自動部署至一個或許多個 {{site.data.keyword.Bluemix_notm}} 空間、公用 Cloud Foundry 伺服器，或 IBM Containers for {{site.data.keyword.Bluemix_notm}} 上的 Docker 容器。

建置工作會從 Git 儲存庫編譯及包裝您的應用程式原始碼。建置工作會產生可部署的構件，例如 WAR 檔或 IBM Containers 的 Docker 容器。此外，您可以在建置內自動執行單元測試。您可以設定建置工作，以在每次推送確定時觸發建置。

部署工作會取得建置工作的輸出，並將它部署至 IBM Containers 或 Cloud Foundry 伺服器，例如 {{site.data.keyword.Bluemix_notm}}。

您可以部署至一或多個地區及服務。例如，您可以設定 {{site.data.keyword.deliverypipeline}} 使用一個以上的服務、在一個地區中測試，以及部署至多個地區進行正式作業。如需相關資訊，請參閱[地區](/docs/overview/whatisbluemix.html#ov_intro_reg){: new_window}。

如果您在開放式工具鏈中使用多個管線，則可以建立複合管線，來管理如何從單一位置部署所有管線。

有數種方式可建立管線，包括將管線新增至現有應用程式，以及在沒有現有應用程式的情況下建立管線。如果您的組織中還沒有 {{site.data.keyword.deliverypipeline}} 服務，則可以前往型錄、按一下 {{site.data.keyword.deliverypipeline}}，然後按一下「建立」。

請完成下列步驟，以設定現有應用程式的 {{site.data.keyword.deliverypipeline}}：

1. 在 {{site.data.keyword.Bluemix_notm}} 應用程式「儀表板」上，按一下您的應用程式。
1. 從 {{site.data.keyword.Bluemix_notm}} 功能表列的漢堡式功能表中，按一下**服務**，然後按一下 **DevOps**。
1. 按一下**管線**，然後按一下**建立管線**。

若要[建立管線 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window}，且管線配置成部署 Cloud Foundry 應用程式，請遵循下列步驟：

1. 按一下 **Cloud Foundry**。
1. 如果您要使用不同的管線名稱，請變更其預設名稱。
1. 如果您要使用不同的應用程式名稱，請變更其預設名稱。此名稱是管線部署至其中的應用程式。
1. 如果您沒有工具鏈，則系統會為您建立具有預設名稱的工具鏈。如果您要使用不同的工具鏈名稱，請變更其名稱。使用工具鏈時，只要與其他工具及服務整合，即可延伸管線的功能。如需工具鏈的相關資訊，請參閱[使用工具鏈](/docs/services/ContinuousDelivery/toolchains_working.html){: new_window}。

 **提示**：管線及工具鏈屬於組織。如果您隸屬於具有工具鏈的組織，則可以新增至其任何關聯工具鏈的存取控制清單。將您新增至工具鏈的存取控制清單之後，您就可以使用該工具鏈及任何關聯管線，即使您未建立它們。如需工具鏈存取控制的相關資訊，請參閱[管理存取權](/docs/services/ContinuousDelivery/toolchains_using.html#managing_access){: new_window}。

1. 選取您要使用的工具鏈，或鍵入您要建立的新工具鏈的名稱。
1. 選取 Git 提供者。

 **提示**：如果您未授權 {{site.data.keyword.Bluemix_notm}} 存取 GitHub，則系統會提示您按一下**授權**來移至 GitHub 網站。如果您沒有作用中的 GitHub 階段作業，則系統會提示您登入。按一下**授權應用程式**，以容許 {{site.data.keyword.Bluemix_notm}} 存取 GitHub 帳戶。如果您有作用中的 GitHub 階段作業，但最近未輸入過密碼，則系統可能會提示您輸入 GitHub 密碼進行確認。

   * 如果您有儲存庫並且想要使用它，請針對儲存庫類型選取**鏈結**。請搜尋儲存庫的位置，或從可用儲存庫清單中選取儲存庫。

   * 如果您要建立空的儲存庫，請針對儲存庫類型選取**新建**。鍵入儲存庫的名稱。

   * 如果您要建立儲存庫的複製品，請針對儲存庫類型選取**複製**。請搜尋儲存庫的位置，或從可用儲存庫清單中選取儲存庫。

   * 如果您要分出儲存庫，以透過取回要求來提出變更，請選取**分出**。請搜尋儲存庫的位置，或從可用儲存庫清單中選取儲存庫。

1. 選取儲存庫，或輸入儲存庫 URL。
1. 按一下**建立**。即會建立、配置管線，並顯示在工具鏈的「概觀」頁面上。
 ![管線卡](images/cd_pipeline.png)
1. 如果您已在包含複合管線的工具鏈中建立管線，則會將新的管線新增至複合管線。請修改部署方案，以包括新管線的部署作業。請參閱[建立 Delivery Pipeline 作業](/docs/services/ContinuousDelivery/pipeline_deployment_plan.html#tasks_pipelineCD){: new_window}。

若要建立沒有任何預先配置階段的[空管線 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window}，請執行下列動作：

1. 按一下**自訂**。
1. 如果您要使用不同的管線名稱，請變更其預設名稱。
1. 如果您沒有工具鏈，則系統會為您建立具有預設名稱的工具鏈。如果您要使用不同的工具鏈名稱，請變更其名稱。使用工具鏈時，只要與其他工具及服務整合，即可延伸管線的功能。
1. 選取您要使用的工具鏈，或鍵入您要建立的新工具鏈的名稱。
1. 按一下**建立**。即會建立空管線，並在工具鏈的「概觀」頁面上呈現為卡片。

從 {{site.data.keyword.deliverypipeline}} 中變更配置；檢查建置的狀態、已部署的應用程式及最近的部署；查看最新日誌及部署詳細資料，或者刪除管線。
