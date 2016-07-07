---

copyright:
  years: 2015-2016

---

<!-- Attribute definitions -->
{:codeblock: .codeblock}

# 開始使用 Hello Bluemix for Android 範例
{: #gettingstarted-android}
*前次更新：2016 年 5 月 27 日*
{: .last-updated}  

如果您要開始使用新的 Android 應用程式，可以使用 HelloWorld 應用程式。這個應用程式會示範如何從行動應用程式連接到
{{site.data.keyword.Bluemix}} 後端而不需鑑別。
應用程式已安裝 SDK。當您準備好時，便可以取得想要在應用程式中使用的特定程式庫。

1. 在 {{site.data.keyword.Bluemix_notm}} 中建立行動後端。
    1. 在 {{site.data.keyword.Bluemix_notm}} 型錄的「樣板」區段中，按一下 MobileFirst Services Starter。
    2. 輸入您應用程式的名稱及主機，然後按一下**建立**。
    3. 按一下**完成**。
2. 從 GitHub 取得專案。您可以選擇性地使用 git clone 指令來取得專案。從您的電腦中，開啟終端機，然後輸入下列指令：
```
    git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloworld.git
    ```

3. 在 `BMSClient.getInstance().initialize()` 函數內的 `try` 區塊，將 &lt;APPLICATION_ROUTE&gt; 及 &lt;APPLICATION_ID&gt; 取代為您的應用程式路徑和 GUID，以起始設定專案：
```
// initialize SDK with IBM Bluemix application ID and route
BMSClient.getInstance().initialize(this, "<APPLICATION_ROUTE>", "<APPLICATION_ID>");
```
4. 在開發環境中執行範例。從 Android Studio 工具列中，按一下**播放**按鈕，然後選取模擬器。
5. 在模擬器中，按一下 **Ping {{site.data.keyword.Bluemix_notm}}**。範例應用程式會將 Get 要求傳送給 {{site.data.keyword.Bluemix_notm}} 上的 `Node.js` 運行環境。如果要求成功，則會驗證連線，且更新模擬器中的文字。

  **附註：**`Node.js` 運行環境程式碼提供於 MobileFirst Services Starter 樣板。如果未使用 MobileFirst Services Starter 樣板來建立後端應用程式，則不會順利連接應用程式。

  當您順利在 Android Studio 中從行動應用程式連接 {{site.data.keyword.Bluemix_notm}} 時，即會顯示下列訊息：

  `Yay! You are connected`
  {: screen}

  ![Hello World 應用程式順利連接 {{site.data.keyword.Bluemix_notm}}](images/yayconnected.jpg "圖 1. Hello World 應用程式順利連接 Bluemix")

  如果連線失敗，您會看到：
  `Bummer. Something went wrong`
  {: screen}

  ![Hello World 應用程式未連接 Bluemix](images/bummer_android.jpg "圖 2. Hello World 應用程式未連接 Bluemix")

  您可以針對失敗的連線進行疑難排解，如下所示：
   * 驗證您已正確地貼上路徑及 GUID 值。
   * 如需相關資訊，請檢閱除錯日誌。


## 後續步驟：
{: #next}
如需如何取得 SDK 並整合到您的行動應用程式的相關資訊，請參閱有關設定 Bluemix 服務的資訊。
   * [Mobile Client Access](../../services/mobileaccess/index.html)
   * [Push](../../services/mobilepush/index.html)

# 相關鏈結

## 範例
   * [Hello Bluemix 範例](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloworld)

## SDK
   * [核心 SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)

## API
   * [核心 API](https://www.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)
