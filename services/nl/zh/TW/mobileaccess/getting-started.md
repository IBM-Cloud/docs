---

copyright:
  years: 2015, 2016

---

# 開始使用
{: #getting-started}
若要開始使用 {{site.data.keyword.amashort}}，您可以將 {{site.data.keyword.amashort}} 服務新增至現有 {{site.data.keyword.Bluemix}} 應用程式，也可以使用樣板來建立新的應用程式。  

## 建立 {{site.data.keyword.amashort}} 服務的實例
{: #service-instance}

您可以從 {{site.data.keyword.Bluemix}} 型錄建立新的 {{site.data.keyword.amashort}} 服務實例。如果您未使用樣板來建立新的行動式後端，則必須在現有後端上配置 Server SDK。


  * **新的應用程式**：下列各節中的指示說明如何建立新應用程式，來建立行動式後端並使用 {{site.data.keyword.amashort}} Server SDK 進行保護。按一下 **MobileFirst Services Starter** 樣板，以使用 {{site.data.keyword.amashort}} 服務來建立新的應用程式。
  * **現有應用程式**：按一下 {{site.data.keyword.amashort}} 圖示，並建立連結至現有應用程式的新服務實例。若要在現有應用程式上配置 Server SDK，請參閱[保護雲端資源](protecting-resources.html)。


## 使用 MobileFirst Services Starter 樣板建立行動式後端
{: #create-backend}
當您使用 MobileFirst Services Starter 時，會取得 IBM {{site.data.keyword.Bluemix_notm}} 上執行的 Node.js 執行時期實例，用來實作自訂後端邏輯。會將一組提供安全、資料、推送及監視功能的核心行動式服務連結至該 Node.js 應用程式。建立 {{site.data.keyword.Bluemix_notm}} Node.js 應用程式之後，即可設定開發環境，並開始使用 {{site.data.keyword.Bluemix_notm}} Mobile Services SDK。您可以使用 SDK，透過簡式 API 呼叫來存取連結至雲端應用程式的服務。

1. 從 {{site.data.keyword.Bluemix_notm}} 型錄中，移至**樣板**區段，然後按一下 **MobileFirst Services Starter**。
1. 新增行動式後端的相關資訊（包括空間、名稱、主機及服務方案）。
1. 按一下**建立**。



## 後續步驟
{: #next-steps}
使用樣板所建立的 Node.js 應用程式的數個端點是使用 {{site.data.keyword.amashort}} 進行保護。若要進一步瞭解預設行動式後端應用程式，請參閱 [bms-hellotodo-strongloop](https://github.com/ibm-bluemix-mobile-services/bms-hellotodo-strongloop)。

您可以設定行動式應用程式來使用 {{site.data.keyword.amashort}} SDK。設定 SDK 之後，即可開始設定應用程式中的鑑別及監視。請遵循行動式開發平台的指示：

* [Android](getting-started-android.html)
* [iOS (Swift SDK)](getting-started-ios.html)
* [iOS (Objective-C SDK)](getting-started-ios.html)
* [Cordova](getting-started-cordova.html)
