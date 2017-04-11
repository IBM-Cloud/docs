---

copyright:

years: 2017
lastupdated: "2017-03-16"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# API
{: #api_overview}

數個 API 適用於開發連接至 {{site.data.keyword.iot_full}} 的裝置、閘道及應用程式的程式碼。

HTTP API 是以 HTTP 基本鑑別來進行保護。當您使用儀表板來產生 API 金鑰時，會出現金鑰及鑑別記號。如需 API 金鑰及記號的相關資訊，請參閱 [API 金鑰連線](../platform_authorization.html#api-key)。


## 關於 HTTP API
{: #api_about}

登錄您自己的組織之後，系統會提供您 6 個字元的組織 ID，在用於任何 HTTP API 呼叫的主機名稱中，都需要此 ID。您可以在下列位址存取您組織的基本 URL：

https://<**orgId**>.internetofthings.ibmcloud.com/api/v0002

若要向應用程式 API 鑑別要求，請將使用者名稱設為 API 金鑰，將密碼設為鑑別記號。

如需「傳訊 API」，請使用下列位址：

https://<**orgId**>.messaging.internetofthings.ibmcloud.com/api/v0002

## HTTP API
{: #api_http}

API                     | 用來...       
------------- | -------------
[組織管理 ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/orgAdmin.html){: new_window} | 配置組織（包括建立及刪除裝置），檢查用法、服務狀態，以及診斷裝置連線問題。[安全 ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/security.html){: new_window} | 管理使用者邀請與鑑別，以及使用者、API 金鑰和裝置的授權。[資訊管理 ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/info-mgmt.html){: new_window} |  存取裝置事件資料、取得和更新裝置位置，以及取得該位置的天氣資訊。[裝置管理 ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/deviceMgmt.html){: new_window} | 使用裝置管理通訊協定來與受管理裝置互動。[傳訊 ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/http-messaging.html){: new_window}   | 使用 HTTP 來發佈事件及傳送指令。**附註：**如需「傳訊 API」，請使用下列位址：*https://<**orgId**>.messaging.internetofthings.ibmcloud.com/api/v0002*



## 延伸規格 HTTP API
{: #api_extension}

API                     | 用來...       
------------- | -------------
[AT&T 延伸規格 ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/ext-atnt.html){: new_window} | 管理 AT&T 裝置。
[Jasper 延伸規格 ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/ext-jasper.html){: new_window} | 管理 Jasper 裝置。
[Orange 延伸規格 ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/ext-orange.html){: new_window} | 從連接至 {{site.data.keyword.iot_short_notm}} 組織的裝置檢視 SIM 卡資料，以及安裝 Orange SIM 卡。

## 測試版 HTTP API
{: #api_beta}

API                     | 用來...       
------------- | -------------
[閘道安全 ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html){: new_window}   | 檢查及指派閘道裝置的角色。
[裝置安全 ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-devices-beta.html){: new_window} | 檢查及指派裝置的角色。
[介面對映 ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html){: new_window}   |   使用介面來對映及存取裝置資料。
