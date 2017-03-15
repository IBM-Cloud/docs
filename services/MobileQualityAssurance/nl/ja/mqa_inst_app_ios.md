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

# iOS アプリでの MQA の装備 (非推奨)
{: #instrumentios}

iOS アプリで {{site.data.keyword.mqafull}} を使用するには、SDK をダウンロードし、Xcode 開発環境を使用していくつかの変更を行って装備する必要があります。
{: shortdesc}

アプリに {{site.data.keyword.mqa}} を装備するには、事前に {{site.data.keyword.Bluemix}} アカウントを取得し、装備するアプリのプラットフォームに対応するバージョンの開発環境を正しくインストールしておく必要があります。

Objective-C アプリまたは Swift アプリと連携するように {{site.data.keyword.mqa}} を装備するには、以下のタスクを実行します。

1. 必要な許可、およびダウンロードした SDK を iOS プロジェクトに追加します。

	1. Xcode でプロジェクトを作成するか、開きます。

	2. Xcode プロジェクトの「*General*」タブの「*Linked Frameworks and Libraries*」セクションで`「+」`を選択して、以下の依存関係ライブラリーを追加します。

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

	3. 「{{site.data.keyword.mqa}} SDK for iOS `Q4M.framework`」フォルダーをナビゲーター・ツリーの **「Frameworks」**グループ内にドラッグします。「Choose options」ウィンドウで、「*Copy items if needed*」、**「Create groups」** を選択し、ターゲットとしてプロジェクト名のボックスにチェック・マークを付けます。

	4. 「*Build Settings*」タブの「Linking」セクションで、デバッグおよびリリース用の「*Other Linker flags*」を**「-ObjC」**に設定します。重要: 「*All*」タブが選択されていて、「Other Linker flags」がリストに含まれていることを確認してください。

	5. *Objective-C の場合のみ:* `AppDelegate.m` ファイルと `ViewController.m` ファイルに、次の import ステートメントを追加します。

		```
		#import <Q4M/MQALogger.h>
		```
		{: codeblock}

	6. *Swift の場合のみ:* 以下の手順を実行して、{{site.data.keyword.mqa}} SDK for iOS の Objective-C ブリッジング・ヘッダーを追加します。

		1. プロジェクトのルート・ノードを右クリックして、**「New File」**を選択します。

		2. iOS 下の「Choose Template」ウィンドウで、「Source」セクションの「Header File template」をクリックします。

		3. ファイルに `MyProject-Bridging-Header.h` という名前を付けます。ここで、*MyProject* は Swift プロジェクトの名前です。ターゲットとして対象プロジェクトの名前を選択します。例えば、ファイル名を `MyProject-Bridging-Header.h` とします。

		4. **「Create」**をクリックして、ファイルをプロジェクトのルートに保存します。

		5. 新規ブリッジング・ヘッダー・ファイルに、次のブリッジング・ヘッダー・ファイルの import ステートメントを追加します。

			```
			#import <Q4M/MQALogger.h>
			```
			{: codeblock}

		6. Xcode プロジェクト・ナビゲーター内でプロジェクトを選択した状態で、**「Build Settings」**をクリックして、`Objective-C Bridging Header` を検索します。

		7. **「Swift Compiler - General」**の下で、**「Objective-C Bridging Header」**の値をブリッジング・ヘッダーのパスに設定します。このパスは、プロジェクトのルートからの相対パスです。例えば、プロジェクト MQASampleApp が `/user/example/MQASampleApp` にある場合、パスは `/user/example/MQASampleApp/MQASampleApp-Bridging-Header.h` となります。ファイルをプロジェクトのルートに保存した場合は、`${SRCROOT}/${PROJECT}-Bridging-Header.h` を入力することにより、環境変数を使用してパスを設定できます。

		8. アプリを保存してビルドし、パスが正しいことを確認します。

	7. `info.plist` ファイルで、プロジェクト情報内の以下の設定を確認します。

		* 「Bundle version」- {{site.data.keyword.mqa}} はこのフィールドの値を使用して、テスターに新規ビルド通知を送信するタイミングを決定します。{{site.data.keyword.mqa}} に新規ビルドをアップロードする際には、必ずこの数値を増分してください。「Bundle version」フィールドのストリングは、数字とピリオド (.) 文字に制限されています。この制限は Xcode の要件であるため、ほとんどのアプリケーションがこの規則に従っており、変更する必要はありません。
		* 「Bundle versions string」- このフィールドには、ストリング表記のバージョン番号が入ります。このストリングには、「Bundle version」フィールドと同じ制限は適用されません。

2. ログインごとに新規セッションを開始するように構成します。

    1. `AppDelegate` ファイルで `didFinishLaunchingWithOptions` メソッドを見つけます。

        * Objective-C: `AppDelegate.m` ファイル
        * Swift: `AppDelegate.swift` ファイル

	2. {{site.data.keyword.mqa}} セッションを開始します。

		* Objective-C

			1. `applicationDelegate` メソッド内のメソッド (例えば、`didFinishLaunchingWithOptions` メソッド) で新規セッションを開始します。プロジェクト・ナビゲーター内のプロジェクトと同じ名前のフォルダーを開くと、デリゲートが見つかります。`projectDelegate.m` ファイルを探してください。

			2. `didFinishLaunchingWithOptions` メソッド内の `return YES;` という行の前に、以下のコードを追加します。

				```
				// Starts a quality assurance session using a
				    placeholder key and QA mode
				[MQALogger startNewSessionWithApplicationKey:@"Your_Application_Key"];
				```
				{: codeblock}

			3. *Your_Application_Key* 変数を {{site.data.keyword.mqa}} のアプリケーション・キーに置き換えます。ヒント: {{site.data.keyword.mqa}} Web ペインの「アプリの設定 (App Settings)」下でアプリケーション・キーを見つけることができます。

		* Swift

			1. `AppDelegate.swift` ファイルで `didFinishLaunchingWithOptions` メソッドを見つけます。

			2. このメソッド内の `return true` という行の前に以下のコードを追加します。ここで、*Your_Application_Key* は、アプリの有効なキーです。

				```
				// Set the application key
				MQALogger.startNewSession(withApplicationKey: "Your_Application_Key")
				```
				{: codeblock}

	3. 実動前モードを使用するか、実動モードを使用するかを定義します。実動前モードと実動モードの相違については、IBM Knowledge Center の [Differences between preproduction and production modes ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/cPreprodvsProd.html){: new_window}を参照してください。

		* Objective-C

			1. `didFinishLaunchingWithOptions` メソッドを見つけます。

			2. didFinishLaunchingWithOptions メソッド内の `return YES;` という行の前に、以下のいずれかのコード行を追加します。

			実動前モードを使用する場合は、次のコード行を追加します。

				```
				[[MQALogger settings] setMode:MQAModeQA];
				```
				{: codeblock}

			実動モードを使用する場合は、次のコード行を追加します。

				```
				[[MQALogger settings] setMode:MQAModeMarket];
				```
				{: codeblock}

				**Objective-C の完全な例**
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

			1. AppDelegate.swift ファイルで、`didFinishLaunchingWithOptions` メソッドを検索します。

			2. `didFinishLaunchingWithOptions` メソッドの `return true` という行の前に、以下の行を追加します。

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

			コードの例を以下に示します。

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

				**Swift の完全な例**
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

3. アプリを実行して、アプリの始動時に {{site.data.keyword.mqa}} が開始することを確認します。

4. [{{site.data.keyword.mqa}} の開始](index.html)ページのステップを続けます。

# 関連リンク
{: #rellinks notoc}

## 関連リンク
{: #general notoc}
* [{{site.data.keyword.mqa}} の開始](index.html){:new_window}
