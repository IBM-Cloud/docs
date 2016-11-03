---



copyright:

  years: 2015, 2016



---


{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}

# 開始使用 {{site.data.keyword.deliverypipeline}} {: #delivery-pipeline}  

前次更新：2016 年 9 月 15 日
{: .last-updated}

若要自動建置並部署至 {{site.data.keyword.Bluemix}}，請使用 IBM Continuous {{site.data.keyword.deliverypipeline}} for {{site.data.keyword.Bluemix_notm}}。
{: shortdesc}

此資訊同時適用於 {{site.data.keyword.deliverypipeline}} 及 {{site.data.keyword.deliverypipeline}} Next。

運用 {{site.data.keyword.deliverypipeline}} 服務，有數種建置類型可供您選擇。您提供建置 Script，{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}} 便會執行它，不需要設定建置系統。接著只要按一下，您便可將應用程式自動部署至一個或許多個 {{site.data.keyword.Bluemix_notm}} 空間、公用 Cloud Foundry 伺服器，或 IBM Containers for {{site.data.keyword.Bluemix_notm}} 上的 Docker 容器。  

建置工作會從 Git 或 Jazz 來源控制管理 (SCM) 儲存庫編譯及包裝您的應用程式原始碼。建置工作會產生可部署的構件，例如 WAR 檔或 IBM Containers 的 Docker 容器。此外，您可以在建置內自動執行單元測試。原始碼每次變更時，都會觸發建置。

部署工作會取得建置工作的輸出，並將它部署至 IBM Containers 或 Cloud Foundry 伺服器，例如 {{site.data.keyword.Bluemix_notm}}。  

您可以部署至一或多個地區及服務。例如，您可以設定 {{site.data.keyword.deliverypipeline}} 服務，讓開發構件使用 IBM Containers、在一個地區中測試，並部署至多個地區進行正式作業。如需相關資訊，請參閱[地區](../../overview/index.html#ov_intro__reg)。

有數種方式可建立管線，包括將管線新增至現有應用程式，以及在沒有現有應用程式的情況下建立管線。如果您的組織中尚無 {{site.data.keyword.deliverypipeline}} 服務，可以前往型錄、按一下 {{site.data.keyword.deliverypipeline}} 或 {{site.data.keyword.deliverypipeline}} Next，然後按一下「建立」。

請完成下列步驟，以設定現有應用程式的 {{site.data.keyword.deliverypipeline}}：    

1. 在 {{site.data.keyword.Bluemix_notm}} 應用程式「儀表板」的「概觀」標籤上，於**持續交付**下，按一下**新增 Git 儲存庫及管線**或**新增 Git**（視環境定義而定）來建立應用程式的 Git 受管理專案。
1. 確定已選取**將入門範本應用程式套件移入儲存庫，並啟用「建置並部署」管線**勾選框，然後按一下**繼續**。您可能需要驗證電子郵件位址才能繼續。  
1. 建立 Git 儲存庫之後，按一下**關閉**。「新增 Git」按鈕會取代為「編輯程式碼」按鈕及 Git URL。  
1. 若要開啟管線，請按一下**編輯程式碼**，然後按一下**建置並部署**。若要第一次執行管線，請將變更推送至 Git 儲存庫。

新增此服務之後，您可以配置並執行包含建置、測試及部署工作的階段，以在 {{site.data.keyword.Bluemix_notm}} 空間中建立多階段的部署管線。在 {{site.data.keyword.deliverypipeline}}「儀表板」上，您可以查看 {{site.data.keyword.jazzhub_short}} 專案，並且它們所在的狀態。您可以檢查建置的狀態、已部署的應用程式及最近的部署，或者查看最新的日誌及部署詳細資料。  

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
<h3 class="linklistlabel">指導教學及範例</h3>
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
