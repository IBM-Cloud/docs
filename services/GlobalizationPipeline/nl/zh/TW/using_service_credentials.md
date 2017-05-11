---

copyright:
  years: 2015, 2017
lastupdated: "2016-07-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 在 {{site.data.keyword.Bluemix_notm}} 外部使用 {{site.data.keyword.GlobalizationPipeline_short}}
{: #globalizationpipeline_external}


許多 {{site.data.keyword.Bluemix_notm}} 服務（包括 {{site.data.keyword.GlobalizationPipeline_short}}）都可以從內部部署應用程式管理環境或甚至從另一個雲端平台使用，而不需要管理 {{site.data.keyword.Bluemix_notm}} 上的應用程式。
{:shortdesc}

若要在 {{site.data.keyword.Bluemix_notm}} 外部使用 {{site.data.keyword.GlobalizationPipeline_short}}，請完成下列步驟：

1. 導覽至 {{site.data.keyword.Bluemix_notm}} 型錄，然後從 **DevOps** 種類中選取 **{{site.data.keyword.GlobalizationPipeline_short}}** 服務。

2. 從 {{site.data.keyword.GlobalizationPipeline_short}} 服務型錄頁面中，填入必要資訊。在**連接至**欄位中，選擇**維持不連結**的選項。

3. 按一下**建立**，以將服務新增至 {{site.data.keyword.Bluemix_notm}} 組織。即會將您帶到 {{site.data.keyword.GlobalizationPipeline_short}} 儀表板。

4. 從儀表板中，按一下**服務認證**標籤。  

**服務認證**標籤會顯示所有可用於服務之該特定實例的認證。使用這些認證以及所提供的服務 URL，即可存取 {{site.data.keyword.GlobalizationPipeline_short}} API，而且可以從任何管理環境的應用程式中利用其特性。

若要瞭解 {{site.data.keyword.GlobalizationPipeline_short}} RESTful API，請參閱 [API 參考資料](https://gp-rest.ng.bluemix.net/translate/swagger/index.html){: new_window}。
