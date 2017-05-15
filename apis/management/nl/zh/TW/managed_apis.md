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

使用**檢視受管理 API** 標籤，以查看下列 API 的整體狀態：您所管理的 API，以及先前管理過但目前未公開的 API。在**共用 API** 標籤中，您可以看到已透過 API Management 或透過 {{site.data.keyword.apiconnect_short}} 服務與 {{site.data.keyword.Bluemix_notm}} 組織共用的所有 API。

您可以使用 API 儀表板，來檢視使用 API Management 所管理的所有 API。 

## 檢視受管理 API
{: #view_api}

您可以在這裡檢視針對 {{site.data.keyword.openwhisk_short}} 動作及其他外部來源所建立的 API。

1. 從「{{site.data.keyword.Bluemix_notm}} 儀表板」中，選取**功能表**圖示 > **服務** > **API**。
2. 若要選取您的來源，請按一下**管理 API**。隨即會顯示目前所管理的 API 清單。API 類型包括下列類型：
    * 使用者定義的端點 - 這些項目是 {{site.data.keyword.Bluemix_notm}} 環境外部的 API，並透過其 URL 端點進行追蹤。 
    * {{site.data.keyword.openwhisk_short}} 應用程式 - 這些項目是包裝在 API 內的 {{site.data.keyword.openwhisk_short}} 動作。

選取 API 的名稱，以檢視該 API 的詳細資料。

## 建立受管理 API
{: #create_mgd_api}

您可以選取**建立受管理 API**，以將 API 新增至清單，而不離開受管理 API 的清單。

選取要建立 {{site.data.keyword.openwhisk_short}} 還是 API Proxy（外部）API 之後，請輸入新 API 的資訊。  

這是唯一可讓您新增 API Proxy 或外部 API 的位置。外部 API 未建立或儲存於 {{site.data.keyword.Bluemix_notm}} 組織空間中。您可以指定外部端點的 URL，來管理外部 API。這適用於下列情況：當您嘗試 API Management 以確認是否符合需求時，或現有 API 與您不想干擾的現有 URL 一起執行時。 

如需建立 API 之必要設定的相關資訊，請參閱[管理 API](manage_apis.html)。

## 使用共用的 API
{: #share_api}

在**探索共用 API** 標籤中，您可以檢視其他人已建立並與您共用的 API。您也可以針對與 {{site.data.keyword.openwhisk_short}} 動作及 {{site.data.keyword.appconserviceshort}} 服務相關聯的 API，建立 API 金鑰。

1. 從「{{site.data.keyword.Bluemix_notm}} 儀表板」中，按一下**功能表**圖示 > **服務** > **API**。
2. 在導覽中，選取**探索共用 API**。隨即在這裡顯示您可使用的所有 API。
3. 若要使用 API，請選取它以開啟其「開發人員入口網站」，而您可以在其中訂閱方案來予以使用。 
4. 選取要管理的 API 之後，請參閱[管理 API](manage_apis.html) 以取得如何完成下列作業的相關資訊： 
    * 檢視 API 用量
    * 建立 API 金鑰
    * 使用 API 瀏覽器檢視文件及測試 API。
