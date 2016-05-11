<!-- Attribute definitions -->
{:codeblock: .codeblock}
{:screen: .screen}

# 開始使用 HelloWorld 範例
{: #gettingstarted-ios}
*前次更新：2016 年 1 月 28 日*
如果您要開始使用新的 iOS 應用程式，可以使用 HelloWorld 應用程式。這個應用程式會示範如何從行動式應用程式連接到
{{site.data.keyword.Bluemix}} 後端而不需鑑別。
應用程式已安裝 SDK。當您準備好時，便可以取得想要在應用程式中使用的特定程式庫。

1. 在 {{site.data.keyword.Bluemix_notm}} 中建立行動式後端。
<ol>
	<li>在 {{site.data.keyword.Bluemix_notm}} 型錄的「樣板」區段中，按一下 **MobileFirst Services Starter**。</li>
    <li>輸入您應用程式的名稱及主機，然後按一下**建立**。</li>
    <li>按一下**完成**。</li>
</ol>
2. 從 GitHub 取得專案。從您的電腦中，開啟終端機，然後輸入下列指令：```
git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloworld```

3. 起始設定專案。若要起始設定 SDK，請在「應用程式委派」中將下列程式碼複製到 `didFinishLaunchingWithOptions` 方法。
   * Objective-C：

```
// initialize SDK with IBM Bluemix application ID and route
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:@"<insert route>" backendGUID:@"<insertGUID>"];
return YES;
```{: codeblock}
   * Swift：
```
// initialize SDK with IBM Bluemix application ID and route
IMFClient.sharedInstance().initializeWithBackendRoute("<insert route>", backendGUID: "<insertGUID>")
return true
```{: codeblock}

4. 在開發環境中執行範例。在 Xcode 中，按一下**產品&gt;執行**。隨即啟動 iOS 模擬器。在模擬器中，按一下 **Ping
                {{site.data.keyword.Bluemix_notm}}**。範例應用程式會從 Mobile Client Access 服務取得授權標頭。如果連線測試成功，模擬器中的文字會更新。
<br/>順利在 Xcode 中從行動式應用程式連接 {{site.data.keyword.Bluemix_notm}} 時，即會顯示訊息「耶！您連上了」：<br/>
![Hello World 應用程式順利連接 {{site.data.keyword.Bluemix_notm}}](images/yayconnected.jpg "圖 1. Hello World 應用程式順利連接 {{site.data.keyword.Bluemix_notm}}")
<br/>
如果您順利連接，Xcode 中的除錯日誌會包含下列訊息：
`您已順利連接 {{site.data.keyword.Bluemix_notm}}`
5. 解決任何問題。連線失敗時，會顯示訊息「糟糕，出問題了」。已包含錯誤的相關資訊。<br/>
![Hello World 應用程式未連接 {{site.data.keyword.Bluemix_notm}}](images/bummer_android.jpg "圖 2. Hello World 應用程式未連接 Bluemix")
<br/>驗證您已正確地貼上路徑及 GUID 值：
   * Objective-C：

```
  [imfClient initializeWithBackendRoute:@"https://hellotest.mybluemix.net"
  backendGUID:@"9d48d73a-0878-4254-test-bdcbe6c79c31"];
  ``` {: codeblock}
   * Swift：
```
  IMFClient.sharedInstance().initializeWithBackendRoute("https://hellotest.mybluemix.net", backendGUID: "9d48d73a-0878-4254-test-bdcbe6c79c31")```{: codeblock}


如需相關資訊，您也可以檢查除錯日誌。

## 後續步驟：
{: #next}
如需如何取得 SDK 並整合到您的行動式應用程式的相關資訊，請參閱有關設定 {{site.data.keyword.Bluemix}} 服務的資訊。
   * [Mobile Client Access](../../services/mobileaccess/index.html)
   * [Push](../../services/mobilepush/index.html)

# 相關鏈結

## 範例
   * [HelloWorld 範例](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloworld)

## SDK
   * [Core SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-ios-core)

## API
*
[核心 API](https://classicdocs.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)
