{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}

#開始使用 {{site.data.keyword.deliverypipeline}} {: #delivery-pipeline}  

*前次更新：2016 年 1 月 21 日*

若要自動建置並部署至 {{site.data.keyword.Bluemix}}，請使用 IBM Continuous {{site.data.keyword.deliverypipeline}} for {{site.data.keyword.Bluemix_notm}}（{{site.data.keyword.deliverypipeline}} 服務）。
{: shortdesc} 

若要在雲端開發應用程式，有數種建置類型可供您選擇。您提供建置 Script，{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}} 便會執行它，不需要設定建置系統。接著只要按一下，您便可將應用程式自動部署到一個或許多個 {{site.data.keyword.Bluemix_notm}} 空間、公用 Cloud Foundry 伺服器，或 IBM Containers for {{site.data.keyword.Bluemix_notm}} 上的 Docker 儲存器。  

建置工作會從 Git 或 Jazz 來源控制管理 (SCM) 儲存庫編譯及包裝您的應用程式原始碼。建置工作會產生可部署的構件，例如 WAR 檔或 IBM Containers 的 Docker 儲存器。此外，您可以在建置內自動執行單元測試。原始碼每次變更時，都會觸發建置。  

部署工作會取得建置工作的輸出，並將它部署到 IBM Containers 或 Cloud Foundry 伺服器，例如 {{site.data.keyword.Bluemix_notm}}。  

您可以部署到一個或許多個區域和服務。例如，您可以設定 {{site.data.keyword.deliverypipeline}} 服務，讓開發開發構件使用 IBM Containers、在一個區域中測試，並部署到多個區域中進行正式作業。如需相關資訊，請參閱[地區](../../overview/index.html#ov_intro__reg)。

1. 登入 {{site.data.keyword.Bluemix_notm}}，並且選擇應用程式的組織及空間。
1. 在「{{site.data.keyword.Bluemix_notm}} 儀表板」上，按一下**建立應用程式**。
1. 選取 Web 或行動式應用程式範本、選取入門範本，然後按一下**繼續**。為應用程式命名，然後按一下**完成**。  
1. 在「開始編碼」頁面上，向下捲動然後按一下**檢視應用程式概觀**。  
1. 在 {{site.data.keyword.Bluemix_notm}} 應用程式「儀表板」上，按一下**新增 Git** 為應用程式建立 Git 管理的專案。請確定已選取**將入門範本應用程式套件移入儲存庫並啟用 {{site.data.keyword.deliverypipeline}}（建置並部署）**勾選框，然後按一下**繼續**。   
1. 建立 Git 儲存庫之後，按一下**關閉**。新增 Git 鏈結會取代為編輯程式碼鏈結和您的 Git URL。  
1. 將 {{site.data.keyword.deliverypipeline}} 服務新增至相關聯的一個或多個空間。新增此服務之後，您可以配置並執行包含建置、測試及部署工作的階段，以在 {{site.data.keyword.Bluemix_notm}} 空間中建立多階段的部署管線。
    1. 在 {{site.data.keyword.Bluemix_notm}} 應用程式「儀表板」上，按一下**新增服務或 API**。針對種類，選取 **DevOps** 勾選框，然後從型錄按一下 **Delivery Pipeline**。
    2. 選取方案然後按一下**建立**。{{site.data.keyword.deliverypipeline}} 儀表板會開啟，並顯示您先前建立的應用程式。     
  
在 {{site.data.keyword.deliverypipeline}}「儀表板」上，您可以查看 {{site.data.keyword.jazzhub_short}} 專案，並且它們所在的狀態。您可以檢查建置的狀態、已部署的應用程式及最近的部署，或者查看最新的日誌及部署詳細資料。  

<article class="topic reference nested1" aria-labelledby="d68e338" lang="zh-tw" id="rellinks">
<h2 class="topictitle2" id="d68e338">相關鏈結</h2>
<aside>
<div class="linklist" id="general"><h3 class="linklistlabel">相關鏈結</h3>
<ul>
<li><img src="./sout.gif" alt=""><a href="https://developer.ibm.com/bluemix/support/#prereqs" rel="external" title="（在新分頁或視窗中開啟）">{{site.data.keyword.Bluemix_notm}} 必要條件</a></li>
</ul>
</div>

<div class="linklist" id="samples">
<h3 class="linklistlabel">指導教學及範例</h3>
<ul>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/devopsweb/" rel="external" title="（在新分頁或視窗中開啟）">Clone, edit, and deploy an app</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditor" rel="external" title="（在新分頁或視窗中開啟）">Develop and deploy a Node.js app</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditorjava" rel="external" title="（在新分頁或視窗中開啟）">Develop and deploy a Java app</a></li>
<li><img src="./sout.gif" alt=""><a href="http://www.ibm.com/developerworks/topics/delivery%20pipeline%20service" rel="external" title="（在新分頁或視窗中開啟）">developerWorks：{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.deliverypipeline}} service</a></li>
</ul>
</div>
</aside>
</article>
