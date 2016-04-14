---

copyright:
  years: 2015, 2016
  
---

# 使用 Google 來鑑別使用者
{: #google-auth}
您可以配置 {{site.data.keyword.amashort}} 服務以使用 Google 作為身分提供者來保護資源。行動式應用程式使用者接著可以使用其 Google 認證進行鑑別。

**重要事項：**您不需要個別安裝 Google SDK。當您配置 {{site.data.keyword.amashort}} Client SDK 時，相依關係管理程式會自動安裝 Google SDK。

## {{site.data.keyword.amashort}} 流程
{: #google-auth-overview}

請參閱下列簡化圖表，以瞭解 {{site.data.keyword.amashort}} 如何與 Google 整合來進行鑑別。

![影像](images/mca-sequence-google.jpg)

1. 使用 {{site.data.keyword.amashort}} SDK，對使用 {{site.data.keyword.amashort}} Server SDK 所保護的後端資源提出要求。
* {{site.data.keyword.amashort}} Server SDK 會偵測未獲授權的要求，並傳回 HTTP 401 代碼及授權範圍。
* {{site.data.keyword.amashort}} Client SDK 會自動偵測 HTTP 401 代碼，並啟動鑑別處理程序。
* {{site.data.keyword.amashort}} Client SDK 會聯絡 {{site.data.keyword.amashort}} 服務，並要求發出授權標頭。
* {{site.data.keyword.amashort}} 服務會提供鑑別盤查，以要求先向 Google 鑑別用戶端。
* {{site.data.keyword.amashort}} Client SDK 會使用 Google SDK 來啟動鑑別處理程序。成功鑑別之後，Google SDK 會傳回 Google 存取記號。
* Google 存取記號視為鑑別盤查回答。記號會傳送至 {{site.data.keyword.amashort}} 服務。
* 服務會向 Google 伺服器驗證鑑別盤查回答。
* 如果驗證成功，則 {{site.data.keyword.amashort}} 服務會產生授權標頭，並將它傳回給 {{site.data.keyword.amashort}} Client SDK。授權標頭包含兩個記號：包含存取權資訊的存取記號，以及包含現行使用者、裝置及應用程式相關資訊的 ID 記號。
* 從此時起，透過 {{site.data.keyword.amashort}} Client SDK 所提出的所有要求都會有新取得的授權標頭。
* {{site.data.keyword.amashort}} Client SDK 會自動重新傳送已觸發授權流程的原始要求。
* {{site.data.keyword.amashort}} Server SDK 會從要求中擷取授權標頭、向 {{site.data.keyword.amashort}} 服務驗證授權標頭，以及授與對後端資源的存取權。

## 後續步驟
{: #google-auth-nextsteps}

* [在 Android 應用程式中啟用 Google 鑑別](google-auth-android.html)
* [在 iOS 應用程式中啟用 Google 鑑別](google-auth-ios.html)
* [在 Cordova 應用程式中啟用 Google 鑑別](google-auth-cordova.html)
