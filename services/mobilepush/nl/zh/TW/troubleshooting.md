---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 疑難排解
{: #errors}
前次更新：2017 年 4 月 12 日
{: .last-updated}

本主題會引導您識別及解決在使用 Push Notifications Service 時可能發生的可能錯誤情境。

## 解決常見推送通知問題
{: #troubleshooting_notification_errors}

### 發生內部伺服器錯誤。請與管理者聯絡。（內部錯誤碼：PUSHD102E）
{: #troubleshooting_notification_internal}

**說明**：如果您在 2015 年 11 月之前已建立 Push 實例，則可能發生此錯誤。  

**使用者回應**：若要解決此問題，請刪除 Push 實例然後建立一個新的。請注意，當您刪除 Push 實例時，不會保留您的標籤。


### UnauthorizedRegistration
{: #troubleshooting_notification_unauth}

**說明**：Chrome Web Push 無法與 Firebase Cloud Messaging (FCM) 金鑰搭配使用。如果您從 GCM 移至 FCM 之後無法在 Chrome 上接收 Web Push 通知，這是因為網站先前配置為與 GCM 專案搭配使用，但新的專案是採用 FCM 建立的。用於識別瀏覽器的產生記號是由 Chrome 瀏覽器快取。

**使用者回應**：您可以透過移除 Cookie 並重設瀏覽器的許可權來解決此問題。這將要求許可權以啟用 Push Notifications。 


### 在此瀏覽器中不支援服務工作程式
{: #troubleshooting_notification_service_workers}

**說明**：無法使用以服務工作程式包含為 `BMSPushSDK.js` 一部分的 SDK。 

**使用者回應**：建議您切換為支援服務工作程式的瀏覽器。支援的瀏覽器版本為 Firefox 第 49 版或更新版本，以及 Chrome 第 53 版（64 位元）或更新版本。


### SecurityError：作業不安全
{: #troubleshooting_notification_insecure}

**說明**：在 Firefox 中啟用 Web 主控台時，您可能會看到錯誤。在 Push Notification Service 中的 Web 推送支援需要以 `https` 通訊協定，而非 `http` 通訊協定進行網站存取。

**使用者回應**：建議您從瀏覽器嘗試使用 `https` 連接至網站。


## 解析 Web 推送配置錯誤
{: #troubleshooting_configuration_errors}

您可以瀏覽 `BMSPushSDK.js` 檔案，以診斷 Web 推送配置相關錯誤。此檔案包含失敗資訊。 

若要剖析在回呼時傳回的錯誤，請考量下列範例程式碼：

```
function showStatus(response) {
 if(response.statusCode == 200 || response.statusCode == 201) {
   		document.getElementById("status").innerHTML = "Response is " + response.response;
   	}
   	else if(response.statusCode == 0) {
  		if(response.response) {
  			document.getElementById("status").innerHTML = response.response;	
    		}
    		else {
    			document.getElementById("status").innerHTML = "There is a possible CORS or access issue while attempting the request.";	
   		}   		
   	}
   	else {
   		document.getElementById("status").innerHTML = "Response is " + response.response + " with the error " 
		+ response.error + " and the status code " + response.statusCode;
   	}
 	}
```
	{: codeblock}


- 如果未正確配置 `applicationId`，{{site.data.keyword.mobilepushshort}} 服務的起始要求將會失敗，因此 statusCode 將設為零 (0)。
- 狀態碼 200 或 201 表示順利回應。
- 案例 `clientSecret` 無效，將在 statusCode 上設定 401 回應。`response.reponse` 元件將包含錯誤說明。


## 解決 Push Notifications Service 錯誤訊息
{: #troubleshooting_service_errors}

傳回下列 {{site.data.keyword.mobilepushshort}} 錯誤訊息，以回應 REST API 要求。

錯誤回應範例：
```
	{
		"message": "Missing APNs credentials",
     "docUrl": "https://www.ng.bluemix.net/docs/troubleshoot/errors/mobilepush/index.html#FPWSE0003E",
     "code":   "FPWSE0003E"

}
```
		    {: codeblock}

若要取得錯誤的其他相關資訊，請搜尋相關錯誤碼的文件。

### FPWSE0001E
{: #error_fpwse0001e}

**說明**：伺服器上沒有您嘗試查詢的資源（例如標籤或訂閱）。

**使用者回應**：請建立訊息中所報告的資源。或者，提供正確的 ID 來查詢資源。


### FPWSE0002E
{: #error_fpwse0002e}

**說明**：伺服器上已有您嘗試建立的資源。此資源可以是標籤、訂閱等等。

**使用者回應**：請使用不同的 ID 建立資源。


### FPWSE0003E
{: #error_fpwse0003e}

**說明**：{{site.data.keyword.mobilepushshort}} Service 的必要配置未完成。在配置之前，請嘗試取得 Apple Push Notification Service (APNs) 認證。

**使用者回應**：請確定已使用 APNs 的有效安全憑證配置 {{site.data.keyword.mobilepushshort}} Service。如需相關資訊，請參閱[配置通知提供者的認證 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](t__main_push_config_provider.html){: new_window}。


### FPWSE0004E
{: #error_fpwse0004e}

**說明**：要求中內含的 JSON 主體無效。


**使用者回應**：請確定您在要求使用的是有效的 JSON 語法。



### FPWSE0005E
{: #error_fpwse0005e}

**說明**：向 {{site.data.keyword.mobilepushshort}} 伺服器提出的要求不正確或不完整，因為 JSON 主體未包含完成 API 要求所需的內容值。例如，密碼無效或裝置記號遺漏。


**使用者回應**：請檢閱訊息以瞭解遺漏或無效的內容值，然後提供必要資訊。



### FPWSE0006E
{: #error_fpwse0006e}

**說明**：要求的 JSON 主體具有 {{site.data.keyword.mobilepushshort}} 伺服器不瞭解的參數。


**使用者回應**：請確認要求中的 JSON 主體遵循 {{site.data.keyword.mobilepushshort}} 伺服器所預期要求的格式。如需相關資訊，請參閱 [REST API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://mobile.{DomainName}/imfpush/){: new_window}。



### FPWSE0007E 
{: #error_fpwse0007e}

**說明**：要求 URL 的查詢字串含有無法辨識的參數。例如，如果刪除訂閱的要求中含有 deviceId 及 tagName 以外的參數，則可能發生此錯誤。


**使用者回應**：請確認要求中的 JSON 主體遵循 {{site.data.keyword.mobilepushshort}} 伺服器所預期要求的格式。如需相關資訊，請參閱 [REST API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://mobile.{DomainName}/imfpush/){: new_window}。



### FPWSE0008E
{: #error_fpwse0008e}

**說明**：要求 URL 的查詢字串遺漏必要的參數。例如，刪除訂閱的要求中遺漏 deviceId 及 tagName 參數。


**使用者回應**：請確認要求中的 JSON 主體遵循 {{site.data.keyword.mobilepushshort}} 伺服器所預期要求的格式。如需相關資訊，請參閱 [REST API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://mobile.{DomainName}/imfpush/){: new_window}。



### FPWSE0009E
{: #error_fpwse0009e}

**說明**：嘗試傳送通知，但沒有任何裝置已向應用程式進行登錄。

**使用者回應**：嘗試傳送通知之前，請確定裝置已向應用程式進行登錄。



### FPWSE0010E
{: #error_fpwse0010e}

**說明**：提交至伺服器的要求導致異常狀況。下列其中一種狀況可能造成此錯誤：

- {{site.data.keyword.mobilepushshort}} 使用的某個內部子系統未回應。
- 導致錯誤狀況的要求可能不是由 {{site.data.keyword.mobilepushshort}} 處理。
- {{site.data.keyword.mobilepushshort}} Service 需要管理者的注意。

**使用者回應**：請重試要求。如果問題持續發生，請聯絡 IBM 軟體支援中心。



### FPWSE0011E
{: #error_fpwse0011e}

**說明**：伺服器上已存在訂閱的標籤。例如，若您建立已存在的訂閱時。

**使用者回應**：請使用唯一標籤名稱來建立訂閱。



### FPWSE0012E
{: #error_fpwse0012e}

**說明**：伺服器上不存在訂閱的標籤。提交要擷取或刪除不存在的訂閱的要求時，會發生此錯誤。


**使用者回應**：請在要求中使用正確的標籤名稱及裝置 ID。



### FPWSE0013E
{: #error_fpwse0013e}

**說明**：要求中的 JSON 有效負載無效。


**使用者回應**：請確定 JSON 有效負載是有效的。


### FPWSE0025E
{: #error_fpwse0025e}

**說明**：伺服器目前無法處理要求。

**使用者回應**：請稍後再重新提交要求。


### FPWSE1007E 
{: #error_fpwse1007e}

**說明**：此應用程式的 {{site.data.keyword.mobilepushshort}} Service 已停用。這可能是因為管理者已停用計費或應用程式。


**使用者回應**：請參閱「Bluemix 文件」中的「疑難排解」主題，以檢查服務狀態、檢閱疑難排解資訊或取得協助的相關資訊。



### FPWSE1079E
{: #error_fpwse1079e}

**說明**：針對查詢作業所提供的偏移值無效。

**使用者回應**：請確定偏移值大於或等於零。



### FPWSE1080E 
{: #error_fpwse1080e}

**說明**：針對查詢作業所提供的大小值無效。

**使用者回應**：請確定大小值大於或等於零。


