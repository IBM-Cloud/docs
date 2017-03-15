---

copyright:
  years: 2012, 2017
  
lastupdated: "2017-01-25"  

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 



# {{site.data.keyword.mqa}} 疑難排解 
{: #tsmqa}
以下是使用 {{site.data.keyword.mqa}} 時的數個常見問題的答案。
{:shortdesc}

## JavaScript 混合式建置失敗
{: #ts_js_build_fail}

您的 JavaScript 混合式 {{site.data.keyword.mqa}} 應用程式建置失敗，雖然 IBM MobileFirst Platform Foundation 的 JavaScript&tm; 混合式 SDK 元件在應用程式中，且已新增必要的程式碼。


當您嘗試執行 {{site.data.keyword.mqa}} 應用程式建置時，建置失敗。
{: tsSymptoms notoc} 


1. Android 及 iOS 平台專用混合式 SDK 元件未安裝在專案中。
2. 已安裝的 Android 及 iOS 平台專用混合式 SDK 元件與已安裝的 JavaScript SDK 元件不相容。
3. 已安裝原生 Android SDK 及/或原生 iOS SDK，但未安裝 Android 及 iOS 平台專用混合式 SDK 元件。
{: tsCauses notoc} 
 

解決此問題的部分建議包含下列步驟：
{: tsResolve notoc}
  1.  確定您已安裝所有必要的 Android 及 iOS 平台專用混合式 SDK 元件，以及您的應用程式支援之平台的所有必要原生 Android SDK 或原生 iOS SDK。 
  2. 確定您的 Android 及 iOS 平台專用混合式 SDK 元件的主要版本號碼與 JavaScript 元件相同或更高，最高可達下個主要版本。下表包含範例：
  
| JavaScript 元件版本 | 平台專用元件版本 | 是否相容？ |
|---------: |------------: |------------: |
| 1.2.3 | 1.2.3 | 是 |
| 1.2.3 | 1.2.1 | 否 |
| 1.2.3 | 1.3.2 | 是 |
| 1.2.3 | 2.0.0 | 否 |

  3. 確定您已安裝 Android 及 iOS 平台專用混合式 SDK 元件。如果您的應用程式在那些平台上執行，則需要原生 Android SDK 和原生 iOS SDK，不過混合式應用程式也必須安裝每個平台的 Android 及 iOS 平台專用混合式 SDK 元件。

  
## 無法開啟觀感分析或配送測試應用程式
{: #ts_sent_fail}

您無法開啟觀感分析或配送測試應用程式。

您無法開啟觀感分析或配送測試應用程式，因為您的瀏覽器已封鎖蹦現視窗。
{: tsSymptoms notoc} 

Mobile Quality Assurance 使用蹦現視窗及 Cookie 來與 Mobile Quality Assurance 伺服器進行通訊。
{: tsCauses notoc}


若要建立 Mobile Quality Assurance 與 Mobile Quality Assurance 伺服器之間的通訊，您可能需要配置瀏覽器設定，允許蹦現視窗和 Cookie。例如，當您從使用者介面按一下選項（例如 Sentiment Score）時，Mobile Quality Assurance 可能會遭到阻止，無法與伺服器進行通訊。如果蹦現視窗及 Cookie 遭到封鎖，便無法顯示觀感分析。如需如何配置瀏覽器設定的相關資訊，請參閱特定瀏覽器的文件。
{: tsResolve notoc}


## 無法執行過期的應用程式
{: #ts_app_expired}

您無法執行 Mobile Quality Assurance 應用程式。

當您嘗試執行 Mobile Quality Assurance 應用程式時，看到下列訊息：「您的應用程式已過期，目前無法執行。」
{: tsSymptoms notoc} 

您的應用程式已在 Mobile Quality Assurance 的 Builds 頁面中標示為停用。
{: tsCauses notoc}


請檢查 Mobile Quality Assurance 的 Builds 頁面，以確定應用程式都未標示為停用。通常應用程式會標示為停用，以通知使用者（透過應用程式本身）不要使用特定版本的建置。如需 Mobile Quality Assurance Builds 頁面中之設定的相關資訊，請參閱 IBM Knowledge Center 中的 Managing builds。
{: tsResolve notoc}

