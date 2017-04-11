---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 使用 iOS 應用程式檢測 MQA（已淘汰）
{: #instrumentios}

用於{{site.data.keyword.mqafull}} 檢測 iOS 應用程式，您必須下載 SDK，它可以使用 Xcode 開發環境做部分變更。
{: shortdesc}

使用 {{site.data.keyword.mqa}} 檢測應用程式之前，您必須有 {{site.data.keyword.Bluemix}} 帳戶，以及適合要檢測之應用程式平台的正確安裝開發環境版本。

若要檢測 {{site.data.keyword.mqa}} 以便搭配 Objective-C 或 Swift 應用程式使用，請完成下列作業：

1. 將必要的許可權和已下載的 SDK 新增至您的 iOS 專案。

	1. 在 Xcode 中建立或開啟您的專案。

	2. 新增下列相依關係檔案庫，方法是在 Xcode 專案 *General* 標籤的 *Linked Frameworks and Libraries* 區段中選取 `+`。

		* AssetsLibrary.framework
		* AudioToolbox.framework
		* AVFoundation.framework
		* CoreData.framework
		* CoreLocation.framework
		* CoreMedia.framework
		* CoreMotion.framework
		* CoreTelephony.framework
		* CoreText.framework
		* CoreVideo.framework
		* MediaPlayer.framework
		* QuartzCore.framework
		* Security.framework
		* SystemConfiguration.framework

	3. 將 {{site.data.keyword.mqa}} SDK for iOS `Q4M.framework` 資料夾拖曳到導覽器樹狀結構中的 **Frameworks** 群組。在 Choose options 視窗中，選取 *Copy items if needed*、**Create groups**，然後勾選以您的專案名稱為目標的方框。

	4. 在 *Build Settings* 標籤的 Linking 區段，將 Debug and Release 的 *Other Linker flags* 設為 **-ObjC**。重要事項：請確定已選取 *All* 標籤，以便將 Other Linker flags 包含在清單中。

	5. *僅限 Objective-C：*請將下列 import 陳述式新增到 `AppDelegate.m` 和 `ViewController.m` 檔案：

		```
		#import <Q4M/MQALogger.h>
		```
		{: codeblock}

	6. *僅限 Swift：*完成下列步驟，新增 {{site.data.keyword.mqa}} SDK for iOS 的 Objective-C 橋接標頭：

		1. 在專案根節點按一下滑鼠右鍵，然後選取 **New File**。

		2. 在 iOS 下的 Choose Template 視窗，按一下 Source 區段中的 Header File 範本。

		3. 將檔案命名為 `MyProject-Bridging-Header.h`，其中 *MyProject* 是您的 Swift 專案名稱，然後選取專案的名稱作為目標。例如，將檔案命名為 `MyProject-Bridging-Header.h`。

		4. 按一下 **Create** 將檔案儲存在專案的根目錄。

		5. 在新的橋接標頭檔中，為橋接標頭檔新增下列 import 陳述式：

			```
			#import <Q4M/MQALogger.h>
			```
			{: codeblock}

		6. 在 Xcode Project Navigator 選取專案之後，按一下 **Build Settings**，然後搜尋 `Objective-C Bridging Header`。

		7. 在 **Swift Compiler - General** 下，將 **Objective-C Bridging Header** 的值設為橋接標頭的路徑。路徑相對於您專案的根目錄。例如，如果專案 MQASampleApp 是位於 `/user/example/MQASampleApp`，則路徑是 `/user/example/MQASampleApp/MQASampleApp-Bridging-Header.h`。如果您將檔案儲存在檔案的根目錄，則可以輸入 `${SRCROOT}/${PROJECT}-Bridging-Header.h` 使用環境變數設定路徑。

		8. 儲存並建置應用程式，以驗證路徑是否正確。

	7. 在 `info.plist` 檔案中，驗證專案資訊中的下列設定：

		* 軟體組版本 -{{site.data.keyword.mqa}} 使用此欄位的值來決定何時傳送新的建置通知給測試人員。上傳新的建置給 {{site.data.keyword.mqa}} 時，請確定您遞增此號碼。軟體組版本欄位中的字串以數字和句點 (.) 字元為限。由於這項限制是 Xcode 需求，大部分應用程式都會遵循此慣例，不需要變更。
		* 軟體組版本字串 - 這個欄欄位包含版本號碼的字串表示法。字串沒有和軟體組版本欄位相同的限制。

2. 配置新的階段作業，以開始進行每個登入。

    1. 在 `AppDelegate` 檔案中找到 `didFinishLaunchingWithOptions` 方法：

        * Objective-C：`AppDelegate.m` 檔案
        * Swift：`AppDelegate.swift` 檔案

	2. 啟動 {{site.data.keyword.mqa}} 階段作業。

		* Objective-C

			1. 在 `applicationDelegate` 方法內的方法啟動新階段作業，例如 `didFinishLaunchingWithOptions` 方法。您可以在 Project Navigator 中開啟與您專案同名的資料夾，找到您的委派。尋找 `projectDelegate.m` 檔案。

			2. 將下列程式碼新增到 `didFinishLaunchingWithOptions` 方法內，`return YES;` 這行之前：

				```
				// Starts a quality assurance session using a
				    placeholder key and QA mode
				[MQALogger startNewSessionWithApplicationKey:@"Your_Application_Key"];
				```
				{: codeblock}

			3. 將 *Your_Application_Key* 變數取代為來自 {{site.data.keyword.mqa}} 的應用程式索引鍵。
               提示：您可以 {{site.data.keyword.mqa}} Web 窗格的 App Settings 下找到應用程式索引鍵。

		* Swift

			1. 在 `AppDelegate.swift` 檔案中找到 `didFinishLaunchingWithOptions` 方法。

			2. 將下列程式碼新增到方法內，`return YES;` 這行之前，其中 *Your_Application_Key* 是您的應用程式的有效索引鍵：

				```
				// Set the application key
				MQALogger.startNewSession(withApplicationKey: "Your_Application_Key")
				```
				{: codeblock}

	3. 定義要使用正式作業前模式還是正式作業模式。如需正式作業前與正式作業模式之間差異的相關資訊，請參閱 IBM Knowledge Center 中的 [Differences between preproduction and production modes ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/cPreprodvsProd.html){: new_window}。

		* Objective-C

			1. 找到 `didFinishLaunchingWithOptions` 方法。

			2. 將下列程式碼行的其中之一新增到 didFinishLaunchingWithOptions 方法內，`return YES;` 這行之前：

			若要使用正式作業前模式，請新增下列這行程式碼：

				```
				[[MQALogger settings] setMode:MQAModeQA];
				```
				{: codeblock}

			若要使用正式作業模式，請新增下列這行程式碼：

				```
				[[MQALogger settings] setMode:MQAModeMarket];
				```
				{: codeblock}

				**Objective-C 完整範例**
				<pre><code>
					- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
						{
					   // Override point for customization after application launch.
					   if ([[UIDevice currentDevice] userInterfaceIdiom] == UIUserInterfaceIdiomPad) {
					      UISplitViewController *splitViewController = (UISplitViewController*)self.window.rootViewController;
					      UINavigationController *navigationController = [splitViewController.viewControllers lastObject];
					      splitViewController.delegate = (id)navigationController.topViewController;
						}
					     #ifdef Debug
					   [[MQALogger settings] setMode:MQAModeQA];
					   #else
					   [[MQALogger settings] setMode:MQAModeMarket];
					   #endif
					      // Starts a quality assurance session using a placeholder key
					      [MQALogger startNewSessionWithApplicationKey:@"Your-Application-Key"];
					      // Enables the quality assurance application crash reporting
					      NSSetUncaughtExceptionHandler(&MQAUncaughtExceptionHandler);
					      return YES; }
				</code></pre>
				{: codeblock}

        * Swift

			1. 在 AppDelegate.swift 檔案中，搜尋 `didFinishLaunchingWithOptions` 方法。

			2. 將下列行新增到 `didFinishLaunchingWithOptions` 方法，`return true` 這行之前：

				```
				//Set the SDK mode Market vs QA for Production
				   and Pre-Production
				#if Debug
				  MQALogger.settings().mode = MQAMode.QA
				#elseif Release
				  MQALogger.settings().mode = MQAMode.Market
				#endif
				```
				{: codeblock}

			程式碼的範例：

				```
				func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

				//Set the SDK mode Market vs QA for Production
				   and Pre-Production
				#if Debug
					MQALogger.settings().mode = MQAMode.QA
				#elseif Release
					MQALogger.settings().mode = MQAMode.Market
				#endif

				// Set the application key
				MQALogger.startNewSession(withApplicationKey: "Your_Application_Key")

				// Override point for customization after
				   application launch.
				return true
				```
				{: codeblock}

				**Swift 完整範例**
				<pre><code>				
				func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions:[NSObject: AnyObject]?) -> Bool {
					// Override point for customization after application launch.
					//Set the Shake Device option to true or false. If this is not explicitly set, the Shake Device is enabled by default.
					MQALogger.settings().reportOnShakeEnabled = true
					//Set the SDK mode Market vs QA for Production and Pre-Production
					#if Debug
					MQALogger.settings().mode = MQAMode.QA
					#elseif Release
					MQALogger.settings().mode = MQAMode.Market
					#endif

				//Start the MQA session with the specified app key
					   MQALogger.startNewSession(withApplicationKey: "Your_Application_Key")
				// Enables MQA crash reporting to catch uncaught exceptions
					   NSSetUncaughtExceptionHandler(exceptionHandlerPointer);

					   return true
					}
				</code></pre>
				{: codeblock}

3. 執行應用程式，以確定在應用程式啟動時，{{site.data.keyword.mqa}} 會啟動。

4. 繼續執行[開始使用 {{site.data.keyword.mqa}}](index.html) 頁面上的步驟。

# 相關鏈結
{: #rellinks notoc}

## 相關鏈結
{: #general notoc}
* [開始使用 {{site.data.keyword.mqa}}](index.html){:new_window}
