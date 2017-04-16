---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-03"

---
{:shortdesc: .shortdesc}

# iOS アプリ用の Facebook 認証の使用可能化 (Objective-C SDK)
{: #facebook-auth-ios}

{{site.data.keyword.amafull}} iOS アプリケーションで Facebook を ID プロバイダーとして使用するには、iOS プラットフォームを追加して Facebook アプリケーション用に構成します。


{:shortdesc}

**注:** Objective-C SDK は現在も完全にサポートされており、{{site.data.keyword.Bluemix}} モバイル・サービス用の主要 SDK とされていますが、今年後半には廃止され、新しい Swift SDK が後継になる予定です ([iOS Swift SDK のセットアップ](facebook-auth-ios-swift-sdk.html)を参照してください)。

## 開始する前に
{: #before-you-begin}

以下が必要です。
* CocoaPods と連動して機能するようにセットアップされた iOS プロジェクト。詳しくは、[iOS SDK のセットアップ](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios.html)の **CocoaPods のインストール**を参照してください。
   **注:** 先に進む前にコア {{site.data.keyword.amashort}} Client SDK をインストールする必要はありません。
* {{site.data.keyword.amashort}} サービスによって保護された {{site.data.keyword.Bluemix_notm}} アプリケーションのインスタンス。{{site.data.keyword.Bluemix_notm}} バックエンドの作成方法について詳しくは、[概説](index.html)を参照してください。
* **AppGUID** 値。{{site.data.keyword.amashort}} ダッシュボードでサービスを開きます。**「モバイル・オプション」**ボタンをクリックします。`appGUID` (`tenantId` とも呼ばれる) の値が、**「アプリ GUID」/「TenantId」**フィールドに表示されます。許可マネージャーを初期化するためにこの値が必要になります。
* Facebook アプリケーションとアプリケーション ID。詳しくは、[Facebook for Developers Web サイトでのアプリケーションの作成](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID)を参照してください。

## iOS プラットフォーム用の Facebook アプリケーションの構成
{: #facebook-auth-ios-config}
Facebook for Developers サイトで以下を行います。

1. [Facebook for Developers](https://developers.facebook.com) で自分のアカウントにログインします。 

1. iOS プラットフォームがアプリに追加済みであることを確認します。iOS プラットフォームを追加または構成する場合、iOS アプリケーションの **bundleId** を提供する必要があります。ご使用の iOS アプリケーションの **bundleId** を調べるには、`info.plist` ファイル内または Xcode プロジェクトの**「一般 (General)」**タブ内で**「バンドル ID (Bundle Identifier)」**を探します。

1. **「設定の保存」**をクリックします。

	**ヒント**: これらの機能を使用する予定がある場合は、URL スキーム・サフィックスまたはシングル・サインオンを使用可能にすることを検討してください。

1. **「設定の保存」**をクリックします。

## Facebook 認証用の {{site.data.keyword.amashort}} の構成
{: #facebook-auth-ios-configmca}

Facebook Application ID および Facebook アプリケーションを iOS クライアントに対して機能するよう構成したら、{{site.data.keyword.amashort}} で Facebook 認証を使用可能にすることができます。

1. {{site.data.keyword.amashort}} ダッシュボードでサービスを開きます。
1. **「管理」**タブで、**「許可」**をオンに切り替えます。
	1. **「Facebook」**セクションを展開します。
	1. **Facebook Application ID** を追加して**「保存」**をクリックします。

## iOS 用の {{site.data.keyword.amashort}} Facebook Client SDK の構成
{: #facebook-auth-ios-sdk}

### CocoaPods のインストール
{: #facebook-auth-cocoapods}

{{site.data.keyword.amashort}} Client SDK は、iOS プロジェクト用の依存関係マネージャーである CocoaPods を使用して配布されます。CocoaPods は、自動的にリポジトリーから成果物をダウンロードし、iOS アプリケーションで使用できるようにします。

1. 端末を開き、`pod --version` コマンドを実行します。既に CocoaPods をインストール済みの場合は、バージョン番号が表示されます。この場合、このチュートリアルの次のセクションはスキップすることができます。

1. `sudo gem install cocoapods` を実行して CocoaPods をインストールします。更にガイダンスが必要な場合は、[CocoaPods の Web サイト](https://cocoapods.org/)を参照してください。

### CocoaPods を使用した {{site.data.keyword.amashort}} Facebook Client SDK のインストール
{: #facebook-auth-install-cocoapods}

1. ご使用の iOS プロジェクトで、`Podfile` および以下の行を編集してください。

	```
	pod 'IMFFacebookAuthentication'
	```
{: codeblock}

1. `Podfile` を保存して、コマンド・ラインから `pod install` コマンドを実行します。CocoaPods は依存関係をインストールします。進行状況および追加されたコンポーネントが表示されます。**重要**: この時点で、CocoaPods によって生成された `xcworkspace` ファイルを使用してプロジェクトを開く必要があります。通常、名前は `{your-project-name}.xcworkspace` です。  

1. コマンド・ラインから `open {your-project-name}.xcworkspace` を実行して、iOS プロジェクトのワークスペースを開きます。

### Facebook 認証用の iOS プロジェクトの構成
{: #facebook-auth-ios-configproject}

1. `info.plist` ファイルを見つけます。このファイルは、通常、Xcode プロジェクトの `Supporting files` フォルダーにあります。

1. `info.plist` ファイルに以下のプロパティーを追加して、Facebook 統合を構成します。

	![image](images/ios-facebook-infoplist-settings.png)

`info.plist` ファイルの更新は、このファイルを右クリックし、**「指定して開く」>「ソース・コード」**を選択して以下の XML を追加することでも行えます。

```XML
<key>CFBundleURLTypes</key>
<array>
	<dict>
		<key>CFBundleURLSchemes</key>
		<array>
			<string>fb{your-facebook-application-id}</string>
		</array>
	</dict>
</array>
<key>FacebookAppID</key>
<string>{your-facebook-application-id}</string>
<key>FacebookDisplayName</key>
<string>MyApp</string>
<key>LSApplicationQueriesSchemes</key>
<array>
	<string>fbauth</string>
	<string>fbauth2</string>
</array>
<key>NSAppTransportSecurity</key>
<dict>
    <key>NSExceptionDomains</key>
    <dict>
        <key>facebook.com</key>
        <dict>
            <key>NSIncludesSubdomains</key>
            <true/>
            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
            <false/>
        </dict>
        <key>fbcdn.net</key>
        <dict>
            <key>NSIncludesSubdomains</key>
            <true/>
            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
            <false/>
        </dict>
        <key>akamaihd.net</key>
        <dict>
            <key>NSIncludesSubdomains</key>
            <true/>
            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
            <false/>
        </dict>
    </dict>
</dict>
```
{: codeblock}

**Facebook Application ID** を使用して URL スキームおよび `FacebookappID` プロパティーを更新します。

 **重要**: `info.plist` ファイル内の既存のプロパティーをオーバーライドすることのないようにしてください。重複するプロパティーがある場合は、手動でマージする必要があります。詳しくは、[Xcode プロジェクトの構成 (Configure Xcode Project) ](https://developers.facebook.com/docs/ios/getting-started/)および [iOS9 用のアプリの準備 (Preparing Your Apps for iOS9) ](https://developers.facebook.com/docs/ios/ios9)を参照してください。


## {{site.data.keyword.amashort}} Client SDK の初期化
{: #facebook-auth-ios-initalize}

アプリの経路 (`applicationRoute`) および GUID (`applicationGUID`) を渡すことによって、Client SDK を初期化します。

初期化コードを入れる場所は一般的に (必須ではありませんが)、アプリケーション代行の `application:didFinishLaunchingWithOptions` メソッドの中です。


1. 以下のヘッダーを追加することによって、{{site.data.keyword.amashort}} Client SDK を使用したいクラスに、必要なフレームワークをインポートします。

	####Objective-C
	{: #framework-objc}

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFFacebookAuthentication/IMFFacebookAuthenticationHandler.h>
	#import <FacebookSDK/FacebookSDK.h>
```	

	####Swift
	{: #bridgingheader-swift}

	{{site.data.keyword.amashort}} Client SDK は Objective-C を使用して実装されているため、swift プロジェクトへのブリッジング・ヘッダーを追加する必要がある場合があります。

	1. Xcode でプロジェクトを右クリックし、**「新規ファイル... (New File...)」**を選択します。
		1. **「iOS ソース」**カテゴリーから`「ヘッダー・ファイル」`を選出します。
		1. これに `BridgingHeader.h` という名前を付けます。
		1. ブリッジング・ヘッダーにインポートを追加します。

			```Objective-C
			#import <IMFCore/IMFCore.h>
			#import <IMFFacebookAuthentication/IMFFacebookAuthenticationHandler.h>
			#import <FacebookSDK/FacebookSDK.h>
			```

	1. Xcode でプロジェクトをクリックし、**「ビルド設定 (Build Settings)」**タブを選択します。
		1. **Objective-C Bridging Header** を探します。
		1. 値を `BridgingHeader.h` ファイルの場所に設定します (例: `$(SRCROOT)/MyApp/BridgingHeader.h`)。 
		1. プロジェクトをビルドすることで、Xcode によってご使用のブリッジング・ヘッダーが選択されることを確認してください。失敗メッセージは無いはずです。

2. Client SDK を初期化します。`applicationRoute` と `applicationGUID` の取得について詳しくは、[開始する前に](#before-you-begin)を参照してください。

	####Objective-C
	{: #approute-objc}

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	####Swift
	{: #approute-swift}

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",
	 							backendGUID: "applicationGUID")
	```

1. {{site.data.keyword.amashort}} サービスの `tenantId` パラメーターを渡すことによって、`AuthorizationManager` を初期化します。[開始する前に](#before-you-begin)を参照してください。

	####Objective-C
	{: #authman-objc}

	```Objective-C
     [[IMFAuthorizationManager sharedInstance]  initializeWithTenantId: @"tenantId"];
  ```

	####Swift
	{: #authman-swift}

	```Swift
  IMFAuthorizationManager.sharedInstance().initializeWithTenantId("tenantId")
 ```

1. アプリ代行の `application:didFinishLaunchingWithOptions` メソッドに以下のコードを追加することによって、Facebook SDK にアプリのアクティベーションについて通知し、Facebook Authentication Handler を登録します。このコードは IMFClient インスタンスの初期化の後に追加します。

	####Objective-C
	{: #activate-objc}

	```Objective-C
		[FBAppEvents activateApp];
		[[IMFFacebookAuthenticationHandler sharedInstance] registerWithDefaultDelegate];
```

	####Swift
	{: #activate-swift}

	```Swift
		FBAppEvents.activateApp()
		IMFFacebookAuthenticationHandler.sharedInstance().registerWithDefaultDelegate()
```

1. アプリ代行に以下のコードを追加します。

	####Objective-C
	{: #appdelegate-objc}

	```Objective-C
	- (BOOL)application:(UIApplication *)application openURL:(NSURL *)url
			sourceApplication:(NSString *)sourceApplication annotation:(id)annotation {

		return [FBAppCall handleOpenURL:url sourceApplication:sourceApplication];
	}
	```

	####Swift
	{: #appdelegate-swift}

	```Swift
	func application(application: UIApplication, openURL url: NSURL,
					sourceApplication: String?, annotation: AnyObject) -> Bool {

		return FBAppCall.handleOpenURL(url, sourceApplication: sourceApplication)

	}
```


## 認証のテスト
{: #facebook-auth-ios-testing}
Client SDK が初期化され、Facebook 認証マネージャーの登録が完了すると、モバイル・バックエンドに要求を出すことができるようになります。

### 開始する前に
{: #facebook-auth-ios-testing-before}
{{site.data.keyword.mobilefirstbp}} ボイラープレートを使用していて、{{site.data.keyword.amashort}}により`/protected` エンドポイントで保護されているリソースを既に持っている必要があります。`/protected` エンドポイントをセットアップする必要がある場合、[リソースの保護 ](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)を参照してください。

1. ブラウザーで、新しく作成されたモバイル・バックエンドの保護エンドポイントへの要求の送信を試行します。次の URL を開きます。
`{applicationRoute}/protected` (たとえば、 `http://my-mobile-backend.mybluemix.net/protected`)
<br/>MobileFirst Services Starter ボイラープレートを使用して作成されたモバイル・バックエンドの`/protected` エンドポイントは、{{site.data.keyword.amashort}}で保護されています。 `認証されていない`というメッセージがブラウザーに戻されます。このエンドポイントは {{site.data.keyword.amashort}} Client SDK により装備されたモバイル・アプリケーションからのみアクセス可能であるため、このメッセージが戻されます。

1. iOS アプリケーションを使用して、同じエンドポイントへ要求を出します。

	####Objective-C
	{: #requestpath-objc}

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

	####Swift
	{: #requestpath-swift}

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

1. アプリケーションを実行します。Facebook のログイン画面が表示されます。

	![image](images/ios-facebook-login.png)

	この画面は、デバイスに Facebook アプリをインストールしていない場合、または現在 Facebook に ログインしていない場合は少し違って見えるかもしれません。 

1. 「**OK**」をクリックし、{{site.data.keyword.amashort}} が認証を目的として Facebook のユーザー ID を使用することを承認します。

1. 	要求が成功すると、以下の出力が Xcode コンソールに表示されます。
	![image](images/ios-facebook-login-success.png)

	次のコードを追加してログアウト機能を追加することもできます。

	####Objective-C
	{: #logout-objc}

	```Objective-C
	[[IMFFacebookAuthenticationHandler sharedInstance] logout : callBack]
	```
{: codeblock}

	####Swift
	{: #logout-swift}

	```Swift
	IMFFacebookAuthenticationHandler.sharedInstance().logout(callBack)
	```
{: codeblock}

	ユーザーが Facebook にログインした後でこのコードを呼び出し、そのユーザーが再度ログインしようとする場合、{{site.data.keyword.amashort}} が認証を目的として Facebook を使用することについての許可を求めるプロンプトが出されます。

	ユーザーを切り替えるには、このコードを呼び出す必要があり、ユーザーはブラウザーで Facebook からログアウトしなければなりません。

  ログアウト機能へ `callBack` を渡すことは、オプションです。`nil` を渡すこともできます。
