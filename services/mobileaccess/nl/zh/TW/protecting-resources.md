---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-15"

---

{:shortdesc: .shortdesc} 
{:codeblock:.codeblock}

# 使用 {{site.data.keyword.amashort}} 服務保護後端資源
{: #protecting-resources}


有了 {{site.data.keyword.amafull}} 服務，您可以利用已啟用行動功能的 OAuth 安全及監視來保護 {{site.data.keyword.Bluemix_notm}} 上執行的 Node.js 及 Java 型後端應用程式。
{:shortdesc}

## 開始之前
{: #before-you-begin}
開始之前，請確定 Node.js 服務存在於 {{site.data.keyword.Bluemix_notm}} 後端應用程式中。


## 授權過濾器
{: #auth-filter}
{{site.data.keyword.amashort}} 伺服器 SDK 具有可用來保護後端應用程式的授權過濾器。授權過濾器會截取送入的要求，並驗證授權標頭是否存在。如果授權標頭不存在或無效，則過濾器會傳回具有 HTTP 401 的回應。{{site.data.keyword.amashort}} 用戶端 SDK 知道如何截取 {{site.data.keyword.amashort}} 伺服器 SDK 所傳回的 HTTP 401 回應，並觸發鑑別流程。
## 授權標頭
{: #auth-header}
送入要求中的授權標頭由三個部分組成：Bearer、Access Token 及 ID Token，這三個部分是以空格區隔。`Access Token` 是必要元件，而 `ID Token` 是選用元件。

送入的授權標頭是由個別的授權過濾器進行處理。過濾器會驗證存取記號及 ID 記號簽章、到期日及結構完整性。通過驗證之後，會將安全環境定義物件新增至要求物件。您可以使用相關 API 來取得安全環境定義的參照。

安全環境定義包含使用下列結構儲存的主題、使用者、裝置及應用程式資訊：
```JSON
{
    "imf.sub":"myclientid",
    "imf.user": {
        "id":"user-name",
        "authBy":"myrealm",
        "displayName":"display-name"
    },
    "imf.device": {
        "id":"device-id",
        "platform":"iOSnative",
        "model":"device-model",
        "osVersion":"device-os"
    },
    "imf.application": {
        "id":"ios.bundle.id",
        "version":"1.0"
    }
}
```
{: codeblock}

* `imf.sub`：指定 ID 記號（如果沒有 ID 記號，則為用戶端的唯一 ID）的主題。
* `imf.user`：指定從 ID 記號擷取的使用者身分。如果沒有 ID 記號，此欄位會保留空物件。
* `imf.device`：指定從 ID 記號擷取的裝置身分。如果沒有 ID 記號，此欄位會保留空物件。
* `imf.application`：指定從 ID 記號擷取的應用程式身分。如果沒有 ID 記號，此欄位會保留空白物件。

## 後續步驟
{: #next-steps}
* [保護 Node.js 資源](protecting-resources-nodejs.html)
* [保護 Liberty for Java&trade; 資源](protecting-resources-java.html)
* [本端開發](protecting-resources-local.html)
