---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-10"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 配置行動連線功能及安全
{: #iot4e_configureMCA}

配置 {{site.data.keyword.amafull}}，以啟用行動通訊及安全。此作業是使用範例行動應用程式的必要項目，而且只需要執行一次。
{:shortdesc}

開始之前，您必須在 {{site.data.keyword.Bluemix_notm}} 組織中部署 {{site.data.keyword.iotelectronics}} 入門範本實例。部署入門範本實例，會自動部署元件應用程式及服務（包括 {{site.data.keyword.amafull}}）。

1. 在 {{site.data.keyword.Bluemix_notm}} 儀表板中，開啟 {{site.data.keyword.iotelectronics}} 應用程式。

   **提示：**應用程式位於 {{site.data.keyword.Bluemix_notm}} 儀表板的「應用程式」區段。請務必按一下名稱，而不是路徑。

    ![儀表板中的 {{site.data.keyword.iotelectronics}}](images/IoT4E_bm_dashboard.svg "儀表板中的 {{site.data.keyword.iotelectronics}}")

2. 在**檢視應用程式**上按一下滑鼠右鍵，然後選取**複製鏈結位置**，以複製 {{site.data.keyword.iotelectronics}} Web 應用程式的 URL。

3. 在**連線**標籤上，按一下 {{site.data.keyword.amashort}} 服務予以開啟。

3. 在「{{site.data.keyword.amashort}} 鑑別」頁面上，按一下**開啟**以啟用鑑別。

4. 在**自訂**區段中，輸入下列鑑別認證：

    - **領域名稱**：`myRealm`

    - **自訂身分提供者 URL**：貼上已在第一個步驟中複製的 API 應用程式 URL，格式如下：**https://<*myIoT4eStarterApp*>.mybluemix.net**。

    **重要事項：**請確定 URL 使用安全通訊協定 `https`，即使您複製的值使用 `http` 也是一樣。

    - **您的 Web 應用程式重新導向 URI**：將此欄位空白。

   ![配置 {{site.data.keyword.amashort}}。](images/MCA_config_pg.svg "「{{site.data.keyword.amashort}} 鑑別」頁面")

5. 儲存設定。您現在可以回到 {{site.data.keyword.iotelectronics}} 服務主控台或 {{site.data.keyword.Bluemix_notm}} 主控台。
