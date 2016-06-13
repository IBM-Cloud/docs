---

copyright:
 years: 2015, 2016

---

# 使用 REST API
{: #push-api-rest}

您可對推送通知使用 REST（具象狀態傳輸）API（應用程式介面）。也可以使用 SDK 及 [Push API](https://mobile.{DomainName}/imfpushrestapidocs/) 來進一步開發用戶端應用程式。

運用 Push REST API，後端伺服器應用程式及用戶端可以存取 Push 功能。

- 裝置登錄
- 登錄
- 訊息
- 訂閱
- 標籤

若要取得 REST API 的基本 URL，請執行下列動作：

1. 在 Bluemix® 型錄的「樣板」區段中建立後端應用程式，以自動將 Push 服務連結至此應用程式。如果您已建立後端應用程式，請確定將應用程式連結至 Push Notification Service。 

1. 在 Bluemix 儀表板的主頁面中，移至**應用程式**區域，然後按一下您的應用程式。

3. 按一下「行動式選項」。路徑及應用程式 GUID 值會顯示在應用程式的詳細資料頁面頂端。



## Accept-Language（接受語言）標頭
{: #push-api-rest-accept}

"Accept-Language" 標頭指定 [Push REST API](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window} 所輸出之錯誤訊息要使用的語言。以下是錯誤訊息支援的語言：簡體中文、繁體中文、美式英文、德文、法文、義大利文、日文、韓文、葡萄牙文及西班牙文。

## appSecret
{: #push-api-rest-secret}

應用程式連結至 Push Notifications 時，服務會產生 appSecret（唯一金鑰）並透過回應標頭進行傳遞。如果您使用的是 IBM® Push Notifications for Bluemix Rest API，請使用 REST API 參考資料來取得所需保護之 API 的資訊。如需 REST API 的相關資訊，請參閱「REST API 參考資料」。

要求標頭必須包含 appSecret。如果沒有，則伺服器會傳回「401 未獲授權」的錯誤碼。將 Push Notifications 新增至應用程式時，會建立特定的 AppID。在回應中有一個稱為 appSecret 的標頭，它用來建立「標籤」或傳送訊息。作業是透過型錄或樣板中的服務進行。

若要取得 appSecret 值，請執行下列動作：

1. 按一下連結至 Push 服務的 *app-name*。
2. 按一下**顯示認證**鏈結，以顯示 appSecret (AppID)。

**顯示認證**畫面會顯示 AppSecret 的相關資訊：

```
{
 "imfpush_Dev": [
   {
     "name": "testapp1",
     "label": "imfpush_Dev",
     "plan": "Basic",
     "credentials": {
       "url": "http://imfpush.ng.bluemix.net/imfpush/v1/apps/b615b280-b37e-4042-8815-38a758f234e2",
       "admin_url": "//mobile.ng.bluemix.net/imfpushdashboard/?appGuid=b615b280-b37e-4042-8815-38a758f234e2",
       "appSecret": "8dac71a5-2219-42b3-a9f3-dbb828ba1f04"  
       }
   }
 ]
}
``` 

##Push REST API 過濾器
{: #push-api-rest-filters}

過濾器會定義一個搜尋準則，以限制從 Push 的 GET API 傳回的資料。請將過濾器套用至您要過濾的 Get 作業結果。過濾器會限制結果中包括的項目數。例如，您可以使用過濾器來搜尋開頭為 "test" 的標籤。您可以使用下列語法來產生過濾器。

**name**
要套用過濾器的欄位名稱。

**operator**
說明要使用的過濾器相符項目的 ==（完全相符）或 =@（包含子字串）。

**expression**
要併入結果中的值。

在表示式中顯示逗點及反斜線時，必須使用反斜線跳出。

當您使用多個過濾器時，可以使用 AND 及 OR 邏輯進行結合。

- 對於 AND 邏輯，請在查詢中使用多個過濾器。
- 對於 OR 邏輯，請在過濾器表示式內使用逗點 (,)。
- 對於 AND 及 OR 邏輯：單一查詢可以同時包含 AND 及 OR 邏輯。會先個別評估每一個過濾器，再使用 AND 表示式結合過濾器。

若為裝置 GET API，支援下列組合：
- 名稱為 platform 欄位。
- 除了 platform 之外，運算子可以是 == 或 =@。
- 若為 platform，運算子必須是 ==。如果使用運算子 =@，則值可以是子字串。
- 如果使用 ==，則值必須是完全相符的字串。

若為訂閱 GET API，支援下列組合：

- 名稱可以是下列其中一個欄位：tagName 或 deviceId。
- 除了 platform 之外，運算子可以是 == 或 =@。
- 若為 platform，運算子必須是 ==。
- 如果使用 =@ 運算子，則值可以是子字串。如果使用 == 運算子，則值必須是完全相符的字串。
- 若為標籤 GET API，支援下列組合：
- 名稱可以是下列其中一個欄位：name 或 description。
- 如果使用運算子 =@，則值可以是子字串。
- 如果使用 ==，則值必須是完全相符的字串。
