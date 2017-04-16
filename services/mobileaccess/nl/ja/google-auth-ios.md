---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-01"

---

{:screen: .screen}
{:shortdesc: .shortdesc}


# iOS Objective C アプリ用の Google 認証の使用可能化
{: #google-auth-ios}


Google Sign-In を使用して、{{site.data.keyword.amafull}} iOS アプリのユーザーを認証します。

**注:** Objective-C SDK は現在も完全にサポートされており、{{site.data.keyword.Bluemix_notm}} モバイル・サービス用の主要 SDK とされていますが、この SDK は今年後半には廃止され、新しい Swift SDK が後継になる予定です。新規アプリケーションには Swift SDK を使用することを強くお勧めします。このページの手順は、{{site.data.keyword.amashort}} Client Objective-C SDK に適用されます。Swift SDK を使用する手順については、[iOS アプリ用の Google 認証の使用可能化 (Swift SDK)](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html) を参照してください。

## 開始する前に
{: #before-you-begin}
以下が必要です。
* {{site.data.keyword.amafull}} サービスのインスタンスおよび {{site.data.keyword.Bluemix_notm}} アプリケーション。{{site.data.keyword.Bluemix_notm}} バックエンド・アプリケーションの作成方法について詳しくは、[概説](index.html)を参照してください。
* バックエンド・アプリケーションの URL (**「アプリの経路 (App Route)」**)。バックエンド・アプリケーションの保護されたエンドポイントに要求を送信するためにこの値が必要になります。
* **TenantID** 値。{{site.data.keyword.amashort}} ダッシュボードでサービスを開きます。**「モバイル・オプション」**ボタンをクリックします。`tenantId` (`appGUID` とも呼ばれる) の値が、**「アプリ GUID」/「TenantId」**フィールドに表示されます。許可マネージャーを初期化するためにこの値が必要になります。

## iOS プラットフォーム用の Google プロジェクトの構成
{: #google-auth-ios-project}
Google を ID プロバイダーとして使用することを開始するには、Google Developer Console にプロジェクトを作成して、Google Client ID を取得します。このクライアント ID は、どのアプリケーションが接続を試行しているかを Google に知らせるための固有 ID です。   

1. Google iOS プロジェクトがまだ作成されていない場合は、[Google Developer Console](https://console.developers.google.com) サイト上の手順に従います。

1. **「Social APIs」**リストから**「Google+ API」**を選択し、**「Enable」**をクリックします。

1. **「Credentials」**リストで**「Create credentials」**ボタンをクリックし、**「OAuth client ID」**を選択します。

1. この時点で、アプリケーション・タイプの選択が表示されます。**「iOS」**を選択します。

1. iOS クライアントに、意味のある名前を指定します。iOS アプリケーションのバンドル ID を指定します。iOS アプリケーションのバンドル ID を見つけるには、`info.plist` ファイル内、または Xcode プロジェクトの**「General (一般)」**タブで**「Bundle Identifier (バンドル ID)」**を探してください。

1. 新しい Google iOS クライアント ID をメモします。この値は、{{site.data.keyword.Bluemix}} にアプリケーションをセットアップする時に必要です。




## Google 認証用の {{site.data.keyword.amashort}} の構成
{: #google-auth-ios-config}

これで Google iOS クライアント ID を取得したので、{{site.data.keyword.Bluemix_notm}} ダッシュボードで Google 認証を使用可能にすることができます。

1. {{site.data.keyword.amashort}} ダッシュボードでサービスを開きます。
1. **「管理」**タブで、**「許可」**をオンに切り替えます。
1. **「Google」**セクションを展開します。
1. **「iOS のアプリケーション ID (Application ID for iOS)」**で、iOS の Google Client ID を指定します。
1. **「保存」**をクリックします。


## iOS 用の {{site.data.keyword.amashort}} Google Client SDK の構成
{: #google-auth-ios-sdk}

### CocoaPods を使用した {{site.data.keyword.amashort}} Client SDK のインストール
{: #google-auth-ios-sdk-cocoapods}

1. iOS プロジェクトにナビゲートします。

1. `Podfile` を編集して以下の行を追加します。

	```
	pod 'IMFGoogleAuthentication'
	```
{: codeblock}

1. `Podfile` を保存し、コマンド・ラインから `pod install` を実行します。CocoaPods は依存関係をインストールします。進行状況と、どのコンポーネントが追加されたかが表示されます。

  **重要**: この時点で、CocoaPods によって生成された `xcworkspace` ファイルを使用してプロジェクトを開く必要があります。通常、名前は `{your-project-name}.xcworkspace` です。  

1. コマンド・ラインから `open {your-project-name}.xcworkspace` を実行して、iOS プロジェクトのワークスペースを開きます。

### Google 認証用の iOS プロジェクトの構成
{: #google-auth-ios-googleauth}
`info.plist` ファイルを更新して、Google 統合を構成します。`info.plist` ファイルは、通常、Xcode プロジェクト内の `Supporting files` フォルダーにあります。このファイルを、プロパティー・リスト・エディターまたはテキスト・エディターで編集できます。

* 以下の URL スキーマを `info.plist` ファイルに追加して、Google 統合を構成します。
	![info.plist file](images/ios-google-infoplist-settings.png)

	最初の URL スキーマは、Google Developer Console からのクライアント ID を逆にしたバージョンです。ユーザーのクライアント ID が `123123-abcabc.apps.googleusercontent.com` の場合、URL スキーマは `com.googleusercontent.apps.123123-abcabc` となります。

	2 番目の URL スキーマは、アプリケーションのバンドル ID です。

* テキスト・エディターを使用します。`info.plist` を右クリックし、**「指定して開く」>「ソース・コード」**を選択します。以下の XML をファイルに追加します。

	```XML
	<key>CFBundleURLTypes</key>
	<array>
		<dict>
			<key>CFBundleTypeRole</key>
			<string>Editor</string>
			<key>CFBundleURLSchemes</key>
			<array>
				<string>com.googleusercontent.apps.123123-abcabc</string>
			</array>
		</dict>
		<dict>
			<key>CFBundleTypeRole</key>
			<string>Editor</string>
			<key>CFBundleURLSchemes</key>
			<array>
				<string>com.ibm.HelloWorld</string>
			</array>
		</dict>
	</array>

	```
{: codeblock}

	両方の URL スキーマを更新します。

	**重要**: `info.plist` ファイル内の既存のプロパティーをオーバーライドしないでください。オーバーラップするプロパティーがある場合は、それらのプロパティーを手動でマージする必要があります。詳細については、[Try Sign-In for iOS](https://developers.google.com/identity/sign-in/ios/start) を参照してください。

## {{site.data.keyword.amashort}} Client SDK の初期化
{: #google-auth-ios-initialize}

{{site.data.keyword.amashort}} Client SDK を使用するには、TenantID と「アプリの経路 (App Route)」パラメーターを渡して初期化します。

初期化コードを入れる場所は一般的に (必須ではありませんが)、アプリケーション代行の `application:didFinishLaunchingWithOptions` メソッドの中です。

1. {{site.data.keyword.amashort}} Client SDK を使用したいクラス内で必要なフレームワークをインポートします。以下のヘッダーを追加します。

	#### Objective-C:

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>
	```
{: codeblock}

	#### Swift:

	{{site.data.keyword.amashort}} Client SDK は Objective-C によって実装されます。この SDK を使用するために、Swift プロジェクトへのブリッジング・ヘッダーを追加する必要がある場合があります。

	1. Xcode でプロジェクトを右クリックし、**「新規ファイル... (New File...)」**を選択します。

	2. **「iOS ソース」**カテゴリーから**「ヘッダー・ファイル」**を選出します。

	3. これに `BridgingHeader.h` という名前を付けます。

	4. ブリッジング・ヘッダーに以下のインポートを追加します。
		
	   `#import <IMFCore/IMFCore.h>`
		
	   `#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>`
	
	5. Xcode でプロジェクトをクリックし、**「ビルド設定 (Build Settings)」**タブを選択します。

	6. `Objective-C Bridging Header` を探します。

	7. 値を、`BridgingHeader.h` ファイルのロケーション (例えば、`$(SRCROOT)/MyApp/BridgingHeader.h`) に設定します。

	8. プロジェクトをビルドすることで、Xcode によってご使用のブリッジング・ヘッダーが選択されることを確認してください。

3. 以下のコードを使用して、Client SDK を初期化します。`<applicationRoute>` と `<TenantID>` を、ご使用の**「経路」**と**「TenantID」**に置き換えます。

	#### Objective-C:

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"<applicationRoute>"
			backendGUID:@"<TenantID>"];
	```
{: codeblock}

	#### Swift:

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("<applicationRoute>",
	 							backendGUID: "<TenantID>")
	```
{: codeblock}

1. {{site.data.keyword.amashort}} サービスの `tenantId` パラメーターを渡すことによって、`AuthorizationManager` を初期化します。 
  ####Objective-C
	
  ```Objective-C

  	   [[IMFAuthorizationManager sharedInstance]  initializeWithTenantId: @"tenantId"];
  ```
 {: codeblock}

  ####Swift

  ```Swift
	   IMFAuthorizationManager.sharedInstance().initializeWithTenantId("tenantId")
  ```
 {: codeblock}

1. アプリ代行内の `application:didFinishLaunchingWithOptions` メソッドに以下のコードを追加して、Google 認証ハンドラーを登録します。このコードは、IMFClient の初期化の直後に追加してください。

	#### Objective-C:

	```Objective-C
	[[IMFGoogleAuthenticationHandler sharedInstance] registerWithDefaultDelegate];
	```
{: codeblock}

	#### Swift:

	```Swift
	IMFGoogleAuthenticationHandler.sharedInstance().registerWithDefaultDelegate()
	```
{: codeblock}

1. アプリ代行に以下のコードを追加します。

	#### Objective-C:

	```Objective-C
	- (void)applicationDidBecomeActive:(UIApplication *)application {
		[[IMFGoogleAuthenticationHandler sharedInstance] handleDidBecomeActive];
	}

	- (BOOL)application: (UIApplication *)application openURL: (NSURL *)url
					sourceApplication: (NSString *)sourceApplication annotation: (id)annotation {

		BOOL shouldHandleGoogleURL = [GPPURLHandler handleURL:url
					sourceApplication:sourceApplication annotation:annotation];

		[[IMFGoogleAuthenticationHandler sharedInstance] handleOpenURL:shouldHandleGoogleURL];
		return  shouldHandleGoogleURL;
	}
	```
{: codeblock}

	#### Swift:

	```Swift
	func application(application: UIApplication, openURL url: NSURL,
					sourceApplication: String?, annotation: AnyObject) -> Bool {

		let shouldHandleGoogleURL = GPPURLHandler.handleURL(url,
				sourceApplication: sourceApplication, annotation: annotation)

		IMFGoogleAuthenticationHandler.sharedInstance()
							.handleOpenURL(shouldHandleGoogleURL)

		return shouldHandleGoogleURL;
	}
```
{: codeblock}

## 認証のテスト
{: #google-auth-ios-testing}
Client SDK が初期化されたら、モバイル・バックエンドへの要求の実行を開始できます。



### 開始する前に
{: #google-auth-ios-testing-before}
{{site.data.keyword.mobilefirstbp}} ボイラープレートを使用していて、{{site.data.keyword.amashort}}により`/protected` エンドポイントで保護されているリソースを既に持っている必要があります。`/protected` エンドポイントをセットアップする必要がある場合、[リソースの保護 ](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)を参照してください。


1. デスクトップ・ブラウザーで、`{applicationRoute}/protected` (例えば、`http://my-mobile-backend.mybluemix.net/protected`) を開くことによって、モバイル・バックエンドの保護エンドポイントへの要求の送信を試行します。

1. MobileFirst Services ボイラープレートを使用して作成されたモバイル・バックエンドの `/protected` エンドポイントは、{{site.data.keyword.amashort}} によって保護されています。したがって、このエンドポイントにアクセスできるのは、{{site.data.keyword.amashort}} Client SDK が装備されたモバイル・アプリケーションのみです。結果的に、デスクトップ・ブラウザーに `Unauthorized` が表示されます。

1. iOS アプリケーションを使用して、同じエンドポイントへ要求を出します。

	#### Objective-C:

	```Objective-C
	NSString *requestPath = [NSString stringWithFormat:@"%@/protected",
								[[IMFClient sharedInstance] backendRoute]];

	IMFResourceRequest *request =  [IMFResourceRequest requestWithPath:requestPath
																method:@"GET"];

	[request sendWithCompletionHandler:^(IMFResponse *response, NSError *error) {
		if (error){
			NSLog(@"Error :: %@", [error description]);
		} else {
			NSLog(@"Response :: %@", [response responseText]);
			NSLog(@"%@", [[IMFAuthorizationManager sharedInstance] userIdentity]);
		}
	}];
	```
{: codeblock}

	#### Swift:

	```Swift
	let requestPath = IMFClient.sharedInstance().backendRoute + "/protected"

	let request = IMFResourceRequest(path: requestPath, method: "GET");
	request.sendWithCompletionHandler { (response, error) -> Void in
		if (nil != error){
			NSLog("Error :: %@", error.description)
		} else {
			NSLog("Response :: %@", response.responseText)
			NSLog("%@", IMFAuthorizationManager.sharedInstance().userIdentity)
		}
	};

	```
{: codeblock}

1. アプリケーションを実行します。Google のログイン画面のポップアップが表示されます。

	![image](images/ios-google-login.png)

	この画面は、デバイスに Facebook アプリをインストールしていない場合、または現在 Facebook に ログインしていない場合は少し違って見えるかもしれません。 

1. **「OK」**をクリックして、{{site.data.keyword.amashort}} が Google ユーザー ID を認証目的に使用することを許可します。

1. 	ユーザーの要求は正常に処理されます。LogCat に以下の出力が表示されます。

	![image](images/ios-google-login-success.png)
		
	次のコードを追加してログアウト機能を追加することもできます。

	#### Objective C:

	```Objective-C
	[[IMFGoogleAuthenticationHandler sharedInstance] logout : callBack]
	```
{: codeblock}

	#### Swift:

	```Swift
	IMFGoogleAuthenticationHandler.sharedInstance().logout(callBack)
	```
{: codeblock}

	ユーザーが Google にログインした後でこのコードを呼び出し、そのユーザーが再度ログインしようとする場合、{{site.data.keyword.amashort}} が認証を目的として Google を使用することについての許可を求めるプロンプトが出されます。その時点で、ユーザー名をクリックすると、別のユーザーを選択してログインすることができます。<!--in the upper-right corner of the screen-->

	ログアウト機能へ `callBack` を渡すことは、オプションです。`nil` を渡すこともできます。
