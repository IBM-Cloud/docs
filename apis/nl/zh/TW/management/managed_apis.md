---

copyright:
  years: 2017
lastupdated: "2017-04-13"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 我的 API
{: #manage_api}

使用**檢視受管理 API** 標籤，以查看您所管理的 API 以及您先前管理但目前未公開的 API 的整體狀態。在**共用 API** 標籤中，您可以看到已透過 API Management 或透過 {{site.data.keyword.apiconnect_short}} 服務與 {{site.data.keyword.Bluemix_notm}} 組織共用的所有 API。

您可以使用 API 儀表板，一起檢視所有利用 API Management 管理的 API。 

## 檢視受管理 API
{: #view_api}

您可以在這裡檢視針對 {{site.data.keyword.openwhisk_short}} 動作及其他外部來源所建立的 API。

1. 從「{{site.data.keyword.Bluemix_notm}} 儀表板」中，選取**功能表**圖示 > **服務** > **API**。
2. 若要選取您的來源，請按一下**管理 API**。即會顯示目前所管理的 API 清單。API 類型包括下列類型：
    * 使用者定義的端點 - 這些項目是位於 {{site.data.keyword.Bluemix_notm}} 環境外部且透過其 URL 端點追蹤的 API。 
    * {{site.data.keyword.openwhisk_short}} 應用程式 - 這些項目是包裝在 API 內部的 {{site.data.keyword.openwhisk_short}} 動作。

選取 API 的名稱，即可檢視該 API 的其他詳細資料。

## 建立受管理 API
{: #create_mgd_api}

您可以選取**建立受管理 API**，將 API 新增至清單，而不離開受管理 API 清單。

選取是要建立 {{site.data.keyword.openwhisk_short}} 還是 API Proxy（外部）API 之後，請輸入新 API 的資訊。  

這是唯一可讓您新增 API Proxy 或外部 API 的位置。外部 API 是未在 {{site.data.keyword.Bluemix_notm}} 組織空間中建立或儲存的 API。您可以指定外部端點的 URL，來管理外部 API。當您試用 API Management 以查看是否符合您的需求時，或您已經有 API 正在搭配現有 URL 一起執行而您不想要中斷時，這十分有用。 

如需建立 API 的必要設定的相關資訊，請參閱[管理 API](manage_apis.html)。

## 使用共用 API
{: #share_api}

在**探索共用 API** 標籤中，您可以檢視其他人已建立以及與您共用的 API。您也可以針對與 {{site.data.keyword.openwhisk_short}} 動作以及 {{site.data.keyword.appconserviceshort}} 服務相關聯的 API，建立 API 金鑰。

1. 從「{{site.data.keyword.Bluemix_notm}} 儀表板」中，按一下**功能表**圖示 > **服務** > **API**。
2. 選取導覽中的**探索共用 API**。這裡會顯示所有您可使用的 API。
3. 若要使用 API，請選取它以開啟其「開發人員入口網站」，您可以在其中訂閱方案以進行使用。 
4. 在您選取要管理的 API 之後，請參閱[管理 API](manage_apis.html)，以取得如何完成下列作業的相關資訊： 
    * 檢視 API 用量
    * 建立 API 金鑰
    * 使用「API 瀏覽器」，以檢視文件與測試 API。
