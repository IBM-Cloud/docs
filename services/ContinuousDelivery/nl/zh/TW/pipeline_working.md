---



copyright:

  years: 2015, 2016



---


{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}

# 使用 {{site.data.keyword.deliverypipeline}} {: #pipeline-working}  

前次更新：2016 年 11 月 18 日
{: .last-updated}

若要自動建置及部署至 {{site.data.keyword.Bluemix}}，請使用 {{site.data.keyword.deliverypipeline}} for {{site.data.keyword.Bluemix_notm}}。
{: shortdesc}

使用 {{site.data.keyword.deliverypipeline}}，有數種建置類型可供您選擇。您提供建置 Script，{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}} 便會執行它，不需要設定建置系統。接著只要按一下，您便可將應用程式自動部署至一個或許多個 {{site.data.keyword.Bluemix_notm}} 空間、公用 Cloud Foundry 伺服器，或 IBM Containers for {{site.data.keyword.Bluemix_notm}} 上的 Docker 容器。  

建置工作會從 Git 儲存庫編譯及包裝您的應用程式原始碼。建置工作會產生可部署的構件，例如 WAR 檔或 IBM Containers 的 Docker 容器。此外，您可以在建置內自動執行單元測試。您可以設定建置工作，以在每次推送確定時觸發建置。

部署工作會取得建置工作的輸出，並將它部署至 IBM Containers 或 Cloud Foundry 伺服器，例如 {{site.data.keyword.Bluemix_notm}}。  

您可以部署至一或多個地區及服務。例如，您可以設定 {{site.data.keyword.deliverypipeline}} 使用一個以上的服務、在一個地區中測試，以及部署至多個地區進行正式作業。如需相關資訊，請參閱[地區](/docs/overview/whatisbluemix.html#ov_intro_reg)。

有數種方式可建立管線，包括將管線新增至現有應用程式，以及在沒有現有應用程式的情況下建立管線。如果您的組織中還沒有 {{site.data.keyword.deliverypipeline}} 服務，則可以前往型錄、按一下 {{site.data.keyword.deliverypipeline}}，然後按一下「建立」。

請完成下列步驟，以設定現有應用程式的 {{site.data.keyword.deliverypipeline}}：    

1. 在 {{site.data.keyword.Bluemix_notm}} 應用程式「儀表板」上，按一下您的應用程式。
1. 從 {{site.data.keyword.Bluemix_notm}} 功能表列的漢堡式功能表中，按一下**服務**，然後按一下 **DevOps**。
1. 按一下**管線**，然後按一下**建立管線**。

若要[建立管線（在新視窗中開啟鏈結）](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window}，而管線配置成部署 Cloud Foundry 應用程式，請遵循下列步驟：    

1. 按一下 **Cloud Foundry**。  
1. 如果您要使用不同的管線名稱，請變更其預設名稱。 
1. 如果您要使用不同的應用程式名稱，請變更其預設名稱。此名稱是將管線部署至其中的應用程式。 
1. 如果您沒有工具鏈，則系統會為您建立含有預設名稱的工具鏈。如果您要使用不同的工具鏈名稱，請變更其名稱。使用工具鏈時，只要與其他工具及服務整合，即可延伸管線的功能。

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
1. 如果您要使用不同的管線名稱，請變更其預設名稱。 
1. 如果您沒有工具鏈，則系統會為您建立含有預設名稱的工具鏈。如果您要使用不同的工具鏈名稱，請變更其名稱。使用工具鏈時，只要與其他工具及服務整合，即可延伸管線的功能。
1. 選取您要使用的工具鏈，或鍵入您要建立的新工具鏈的名稱。
1. 按一下**建立**。即會建立空管線，並在工具鏈的「概觀」頁面上呈現為磚。

從 {{site.data.keyword.deliverypipeline}} 磚中變更配置；檢查建置的狀態、已部署的應用程式及最近的部署；查看最新日誌及部署詳細資料，或者刪除管線。  

<article class="topic reference nested1" aria-labelledby="d68e338" lang="en-us" id="rellinks" role="article">
<h2 class="topictitle2" id="d68e338">相關鏈結</h2>
<aside role="complementary" aria-labelledby="related_links">
<div class="linklist" id="general"><h3 class="linklistlabel" id="related_links">相關鏈結</h3>
<ul>
<li><img src="./sout.gif" alt=""><a href="https://developer.ibm.com/bluemix/support/#prereqs" rel="external" title="（在新分頁或視窗中開啟）">{{site.data.keyword.Bluemix_notm}} 必要條件</a></li>
<li><img src="./sout.gif" alt=""><a href="https://www.ibm.com/devops/method/content/deliver/practice_delivery_pipeline/" rel="external" title="（在新分頁或視窗中開啟）">IBM Bluemix Garage Method：Delivery Pipeline</a></li>
</ul>
</div>

<div class="linklist" id="samples">
<h3 class="linklistlabel">指導教學和範例</h3>
<ul>

<!--
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/devopsweb/" rel="external" title="(Opens in a new tab or window)">Clone, edit, and deploy an app</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditor" rel="external" title="(Opens in a new tab or window)">Develop and deploy a Node.js app</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditorjava" rel="external" title="(Opens in a new tab or window)">Develop and deploy a Java app</a></li>
-->

<li><img src="./sout.gif" alt=""><a href="http://www.ibm.com/developerworks/topics/delivery%20pipeline%20service" rel="external" title="（在新分頁或視窗中開啟）">developerWorks：{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.deliverypipeline}} service</a></li>
</ul>
</div>
</aside>
</article>
