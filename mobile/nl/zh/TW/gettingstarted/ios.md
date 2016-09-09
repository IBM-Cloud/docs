---

copyright:
  years: 2015-2016

---

<!-- Attribute definitions -->
{:codeblock: .codeblock}

# 開始使用 Hello Bluemix for iOS 範例
{: #gettingstarted-android}
前次更新：2016 年 6 月 1 日
{: .last-updated}  

如果您要開始使用新的 iOS 應用程式，可以使用 Hello Bluemix 應用程式。這個應用程式會示範如何從行動應用程式連接到 {{site.data.keyword.Bluemix}} 後端而不需鑑別。當您準備好時，便可以取得想要在應用程式中使用的特定程式庫。

1. 在 {{site.data.keyword.Bluemix_notm}} 中建立行動後端。
    1. 在 {{site.data.keyword.Bluemix_notm}} 型錄的「樣板」區段中，按一下 MobileFirst Services Starter。
    2. 輸入您應用程式的名稱及主機，然後按一下**建立**。
    3. 按一下**完成**。
2. 執行 Hello Bluemix 範例應用程式：
	1. 從 GitHub 取得專案。您可以選擇性地使用 git clone 指令來取得專案。從您的電腦中，開啟終端機，然後輸入下列指令：
    ```
    git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-hellobluemix.git
    ```
	2. 從複製專案所在的 `bms-samples-swift-hellobluemix` 目錄內執行 `pod install` 指令。如果您未安裝 Cocoapods，請從 [https://cocoapods.org](https://cocoapods.org) 取得。
	3. 利用 `open HelloBluemix.xcworkspace` 指令開啟 Xcode 工作區。
	4. 在 `AppDelegate.swift` 檔案中，將 appRoute 及 appGuid 值更新為從您先前建立的 Bluemix 後端中取得的值。

3. 在開發環境中執行範例。在 Xcode 中，按一下**產品&gt;執行**。隨即啟動 iOS 模擬器。

	**重要事項：**您的 appRoute 必須使用 `https` 通訊協定，而不是 `http`，否則可能由於應用程式傳輸安全設定而發生連線失敗。您可以在 [Connect your iOS 9 app to Bluemix today ](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/) 部落格文章中深入閱讀那些設定。
	
4. 在模擬器中，按一下 **Ping {{site.data.keyword.Bluemix_notm}}**。範例應用程式會從 Mobile Client Access 服務取得授權標頭。如果連線測試成功，模擬器中的文字會更新。

  順利從 Xcode 中的行動應用程式連接至 {{site.data.keyword.Bluemix_notm}} 時，您會看到：
  `Yay! You are connected`
  {: screen}

  <!--
  ![Hello World application successfully connected to {{site.data.keyword.Bluemix_notm}}](images/yayconnected.jpg "Figure 1. Hello World application successfully connected to Bluemix")
-->

  如果連線失敗，您會看到：
  `Bummer. Something went wrong`
  {: screen}

 <!--
  ![Hello World application not connected to Bluemix](images/bummer_android.jpg "Figure 2. Hello World application not connected to Bluemix")
  -->

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
   * [Hello Bluemix 範例 (iOS)](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-hellobluemix)

## SDK
   * [核心 SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)

## API
   * [核心 API](https://www.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)
