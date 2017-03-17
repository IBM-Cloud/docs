---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.mobilepushshort}} Service 錯誤訊息
{: #errors}
前次更新：2017 年 2 月 13 日
{: .last-updated}


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

## FPWSE0001E
{: #error_fpwse0001e}

**說明**：伺服器上沒有您嘗試查詢的資源（例如標籤或訂閱）。

**使用者回應**：請建立訊息中所報告的資源。或者，提供正確的 ID 來查詢資源。


## FPWSE0002E
{: #error_fpwse0002e}

**說明**：伺服器上已有您嘗試建立的資源。此資源可以是標籤、訂閱等等。

**使用者回應**：請使用不同的 ID 建立資源。


## FPWSE0003E
{: #error_fpwse0003e}

**說明**：{{site.data.keyword.mobilepushshort}} Service 的必要配置未完成。在配置之前，請嘗試取得 Apple Push Notification Service (APNs) 認證。

**使用者回應**：請確定已使用 APNs 的有效安全憑證配置 {{site.data.keyword.mobilepushshort}} Service。如需相關資訊，請參閱 [配置 APNs 的認證 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](t_push_provider_ios.html){: new_window}。


## FPWSE0004E
{: #error_fpwse0004e}

**說明**：要求中內含的 JSON 主體無效。


**使用者回應**：請確定您在要求使用的是有效的 JSON 語法。



## FPWSE0005E
{: #error_fpwse0005e}

**說明**：向 {{site.data.keyword.mobilepushshort}} 伺服器提出的要求不正確或不完整，因為 JSON 主體未包含完成 API 要求所需的內容值。例如，密碼無效或裝置記號遺漏。


**使用者回應**：請檢閱訊息以瞭解遺漏或無效的內容值，然後提供必要資訊。



## FPWSE0006E
{: #error_fpwse0006e}

**說明**：要求的 JSON 主體具有 {{site.data.keyword.mobilepushshort}} 伺服器不瞭解的參數。


**使用者回應**：請確認要求中的 JSON 主體遵循 {{site.data.keyword.mobilepushshort}} 伺服器所預期要求的格式。如需相關資訊，請參閱 [REST API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://mobile.{DomainName}/imfpush/){: new_window}。



## FPWSE0007E 
{: #error_fpwse0007e}

**說明**：要求 URL 的查詢字串含有無法辨識的參數。例如，如果刪除訂閱的要求中含有 deviceId 及 tagName 以外的參數，則可能發生此錯誤。


**使用者回應**：請確認要求中的 JSON 主體遵循 {{site.data.keyword.mobilepushshort}} 伺服器所預期要求的格式。如需相關資訊，請參閱 [REST API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://mobile.{DomainName}/imfpush/){: new_window}。



## FPWSE0008E
{: #error_fpwse0008e}

**說明**：要求 URL 的查詢字串遺漏必要的參數。例如，刪除訂閱的要求中遺漏 deviceId 及 tagName 參數。


**使用者回應**：請確認要求中的 JSON 主體遵循 {{site.data.keyword.mobilepushshort}} 伺服器所預期要求的格式。如需相關資訊，請參閱 [REST API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://mobile.{DomainName}/imfpush/){: new_window}。



## FPWSE0009E
{: #error_fpwse0009e}

**說明**：嘗試傳送通知，但沒有任何裝置已向應用程式進行登錄。

**使用者回應**：嘗試傳送通知之前，請確定裝置已向應用程式進行登錄。



## FPWSE0010E
{: #error_fpwse0010e}

**說明**：提交至伺服器的要求導致異常狀況。下列其中一種狀況可能造成此錯誤：

- {{site.data.keyword.mobilepushshort}} 使用的某個內部子系統未回應。
- 導致錯誤狀況的要求可能不是由 {{site.data.keyword.mobilepushshort}} 處理。
- {{site.data.keyword.mobilepushshort}} Service 需要管理者的注意。

**使用者回應**：請重試要求。如果問題持續發生，請聯絡 IBM 軟體支援中心。



## FPWSE0011E
{: #error_fpwse0011e}

**說明**：伺服器上已存在訂閱的標籤。例如，若您建立已存在的訂閱時。

**使用者回應**：請使用唯一標籤名稱來建立訂閱。



## FPWSE0012E
{: #error_fpwse0012e}

**說明**：伺服器上不存在訂閱的標籤。提交要擷取或刪除不存在的訂閱的要求時，會發生此錯誤。


**使用者回應**：請在要求中使用正確的標籤名稱及裝置 ID。



## FPWSE0013E
{: #error_fpwse0013e}

**說明**：要求中的 JSON 有效負載無效。


**使用者回應**：請確定 JSON 有效負載是有效的。


## FPWSE0025E
{: #error_fpwse0025e}

**說明**：伺服器目前無法處理要求。

**使用者回應**：請稍後再重新提交要求。


## FPWSE1007E 
{: #error_fpwse1007e}

**說明**：此應用程式的 {{site.data.keyword.mobilepushshort}} Service 已停用。這可能是因為管理者已停用計費或應用程式。


**使用者回應**：請參閱「Bluemix 文件」中的「疑難排解」主題，以檢查服務狀態、檢閱疑難排解資訊或取得協助的相關資訊。



## FPWSE1079E
{: #error_fpwse1079e}

**說明**：針對查詢作業所提供的偏移值無效。

**使用者回應**：請確定偏移值大於或等於零。



## FPWSE1080E 
{: #error_fpwse1080e}

**說明**：針對查詢作業所提供的大小值無效。

**使用者回應**：請確定大小值大於或等於零。



