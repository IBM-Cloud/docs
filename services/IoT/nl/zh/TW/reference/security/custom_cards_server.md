---

copyright:
  years: 2016, 2017
lastupdated: "2016-11-29"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 保護自訂卡片伺服器安全
{: #securing_custom_cards}

自訂卡片伺服器是管理自訂卡片 JavaScript 程式碼的標準 Web 伺服器。若要確保 {{site.data.keyword.iot_short_notm}} 環境的完整性，您應該採取保護卡片來源安全的步驟，來保護自訂卡片伺服器安全，如本主題所討論。
{:shortdesc}

**重要事項：**自訂卡片目前提供為實驗性特性，並且根據瀏覽器階段作業來啟用自訂卡片延伸規格。在 {{site.data.keyword.iot_short_notm}} 組織中，不會廣域地共用自訂卡片連線配置及卡片套件。

## {{site.data.keyword.Bluemix_notm}} 角色需求
{: #roles_requirements}

您必須具有 {{site.data.keyword.iot_short_notm}} 管理者權限，才能建立自訂卡片伺服器連線。

## 自訂卡片伺服器安全考量
{: #server_requirements}

下列需求是透過 {{site.data.keyword.iot_short_notm}} 設定：
- 提供伺服器上自訂卡片內容的目錄不需要認證即可存取。  
連接時不需要提供自訂卡片伺服器的鑑別，即可存取及載入自訂卡片。
- 伺服器必須使用「HTTP 安全 (HTTPS)」通訊協定。
- 伺服器必須支援「跨原點資源共用 (CORS)」連線。  

若要保護自訂卡片程式碼及卡片伺服器本身，應該使用深度防禦來定位及保護卡片伺服器安全。這包含限制自訂卡片伺服器存取權的防火牆保護。

自訂卡片處理一律是在使用者的瀏覽器與自訂卡片伺服器之間進行。{{site.data.keyword.iot_short_notm}} 後端絕不會參與處理或調整自訂卡片資訊及程式碼。

對於您選擇部署在自訂卡片伺服器的卡片中的 JavaScript 程式碼並沒有限制。自訂卡片中的 Javascript 程式碼可以存取瀏覽器中保留的所有資訊，就像儀表板中執行的任何其他卡片一樣。請確定由正確的自訂卡片伺服器將程式碼提供給瀏覽器，以顯示及處理自訂卡片。

卡片會在 {{site.data.keyword.iot_short_notm}} 瀏覽器階段作業中如所撰寫般確切執行其程式碼。此外，在未將認證提供給自訂卡片伺服器的情況下，建立自訂卡片伺服器連線。使用者的瀏覽器可以連接至任何已配置的自訂卡片伺服器。

請務必僅配置已知且安全的自訂卡片伺服器，以將自訂卡片提供給使用者的儀表板。   
