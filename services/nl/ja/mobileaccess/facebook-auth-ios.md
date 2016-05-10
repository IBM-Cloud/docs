---

copyright:
  years: 2015, 2016

---

# iOS アプリで Facebook 認証を使用可能にする (Objective-C SDK)
{: #facebook-auth-ios}

iOS アプリケーションで Facebook をID プロバイダーとして使用するには、iOS プラットフォームを追加して Facebook アプリケーション用に構成する必要があります。

**ヒント:** iOS アプリを Swift で作成している場合は、{{site.data.keyword.amashort}} Client Swift SDK を使用することを検討してください。このページの手順は、{{site.data.keyword.amashort}} Client Objective-C SDK に適用されます。Swift SDK を使用する手順については、 [iOS アプリで Facebook 認証を使用可能にする (Swift SDK)](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios-swift-sdk.html) を参照してください。

## 開始する前に
{: #facebook-auth-ios-before}
* {{site.data.keyword.amashort}} により保護されたリソース、および {{site.data.keyword.amashort}} Client SDK が装備された iOS プロジェクトが必要です。詳しくは、[{{site.data.keyword.amashort}} 入門](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)および [iOS Objective-C SDK のセットアップ](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios.html)を参照してください。  
* {{site.data.keyword.amashort}}  Server SDK を使用して手作業でバックエンド・アプリケーションを保護します。詳しくは、[リソースの保護](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)を参照してください。
* Facebook Application ID を作成します。詳しくは、[Facebook Developer Portal から Facebook アプリケーション ID を取得する](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID)を参照してください。

## iOS プラットフォーム用の Facebook アプリケーションの構成
{: #facebook-auth-ios-config}


1. Facebook Developer Portal の Facebook アプリケーションで、**「設定 (Settings)」>「プラットフォームの追加 (Add Platform)」>「iOS」**とクリックします。

1. iOS アプリケーションの *bundleId* を指定します。ご使用の iOS アプリケーションの *bundleId* を調べるには、`info.plist` ファイル内または Xcode プロジェクトの**「一般 (General)」**タブ内で**「バンドル ID (Bundle Identifier)」**を探します。
**ヒント**: これらの機能を使用する予定がある場合は、URL スキーム・サフィックスまたはシングル・サインオンを使用可能にすることを検討してください。

1. **「設定の保存」**をクリックします。

## Facebook 認証用の {{site.data.keyword.amashort}} の構成
{: #facebook-auth-ios-configmca}

Facebook Application ID および Facebook アプリケーションを iOS クライアントに対して機能するよう構成したら、{{site.data.keyword.amashort}} で Facebook 認証を使用可能にすることができます。

1. {{site.data.keyword.Bluemix}}ダッシュボードでアプリを開きます。

1. **「モバイル・オプション」**をクリックし、**「経路」** (`applicationRoute`) と **「アプリ GUID」** (`applicationGUID`) のメモを取ります。SDK を初期化する際に、これらの値が必要になります。

1. {{site.data.keyword.amashort}} タイルをクリックします。{{site.data.keyword.amashort}} ダッシュボードがロードされます。

1. **「Facebook」**タイルをクリックします。

1. Facebook Application ID を指定して**「保存」**をクリックします。

## iOS 用の {{site.data.keyword.amashort}} Client SDK の構成
{: #facebook-auth-ios-sdk}

### CocoaPods のインストール
{: #facebook-auth-cocoapods}

{{site.data.keyword.amashort}} Client SDK は、iOS プロジェクト用の依存関係マネージャーである CocoaPods を使用して配布されます。CocoaPods は、自動的にリポジトリーから成果物をダウンロードし、iOS アプリケーションで使用できるようにします。

1. 端末エミュレーターを開いて `pod --version` コマンドを実行します。既に CocoaPods をインストール済みの場合は、バージョン番号が表示されます。この場合、このチュートリアルの次のセクションはスキップすることができます。

1. `sudo gem install cocoapods` を実行して CocoaPods をインストールします。更にガイダンスが必要な場合は、[CocoaPods の Web サイト](https://cocoapods.org/)を参照してください。

### CocoaPods を使用した {{site.data.keyword.amashort}} Client SDK のインストール
{: #facebook-auth-install-cocoapods}

1. ご使用の iOS プロジェクトで、`Podfile` および以下の行を編集してください。

	```
	pod 'IMFFacebookAuthentication'
	```

1. `Podfile` を保存して、コマンド・ラインから `pod install` コマンドを実行します。CocoaPods は依存関係をインストールします。進行状況および追加されたコンポーネントが表示されます。**重要**: この時点で、CocoaPods によって生成された `xcworkspace` ファイルを使用してプロジェクトを開く必要があります。通常、名前は `{your-project-name}.xcworkspace` です。  

1. コマンド・ラインから `open {your-project-name}.xcworkspace` を実行して、iOS プロジェクトのワークスペースを開きます。

### Facebook 認証用の iOS プロジェクトの構成
{: #facebook-auth-ios-configproject}

1. `info.plist` ファイルを見つけます。このファイルは、通常、Xcode プロジェクトの `Supporting files` フォルダーにあります。

1. `info.plist` ファイルに以下のプロパティーを追加して、Facebook 統合を構成します。

	![image](images/ios-facebook-infoplist-settings.png)

	Facebook Application ID を使用して URL スキームおよび FacebookappID プロパティーを更新します

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
Facebook Application ID を使用して URL スキームおよび FacebookappID プロパティーを更新します。 **重要**: `info.plist` ファイル内の既存のプロパティーをオーバーライドすることのないようにしてください。重複するプロパティーがある場合は、手動でマージする必要があります。詳しくは、[Xcode プロジェクトの構成 (Configure Xcode Project) ](https://developers.facebook.com/docs/ios/getting-started/)および [iOS9 用のアプリの準備 (Preparing Your Apps for iOS9) ](https://developers.facebook.com/docs/ios/ios9)を参照してください。

## {{site.data.keyword.amashort}} Client SDK の初期化
{: #facebook-auth-ios-initalize}

アプリの経路 (`applicationRoute`) および GUID (`applicationGUID`) を渡すことによって、Client SDK を初期化します。

初期化コードを入れる場所は一般的に (必須ではありませんが)、アプリケーション代行の `application:didFinishLaunchingWithOptions` メソッドの中です。

1. {{site.data.keyword.Bluemix_notm}} ダッシュボードのメインページを開いて、アプリをクリックします。**「モバイル・オプション」**をクリックし、**「経路」** (`applicationRoute`) と **「アプリ GUID」** (`applicationGUID`) のメモを取ります。

1. 以下のヘッダーを追加することで、{{site.data.keyword.amashort}} Client SDK を使用するクラスで必要なフレームワークをインポートします。

	**Objective-C**

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFFacebookAuthentication/IMFFacebookAuthenticationHandler.h>
	#import <FacebookSDK/FacebookSDK.h>
```

	**Swift**

	{{site.data.keyword.amashort}} Client SDK は Objective-C を使用して実装されているため、swift プロジェクトへのブリッジング・ヘッダーを追加する必要がある場合があります。 

	1. Xcode でプロジェクトを右クリックし、**「新規ファイル... (New File...)」**を選択します。
	* **「iOS ソース (iOS Source)」**カテゴリーで、`「ヘッダー・ファイル (Header file)」`を選択します。
	* それに「`BridgingHeader.h`」という名前を付けます。
	* ブリッジング・ヘッダーにインポートを追加します。

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFFacebookAuthentication/IMFFacebookAuthenticationHandler.h>
	#import <FacebookSDK/FacebookSDK.h>
```
	* Xcode でプロジェクトをクリックし、**「ビルド設定 (Build Settings)」**タブを選択します。
	* **Objective-C ブリッジング・ヘッダー**を検索します。
	* `BridgingHeader.h` ファイルの場所に値を設定します。例: `$(SRCROOT)/MyApp/BridgingHeader.h`
	* プロジェクトをビルドすることで、Xcode によってご使用のブリッジング・ヘッダーが選択されることを確認してください。失敗メッセージは無いはずです。

3. Client SDK を初期化します。*applicationRoute* および *applicationGUID* を、{{site.data.keyword.Bluemix_notm}} ダッシュボード内の**「モバイル・オプション」**から取得した**「経路」**および**「アプリ GUID」**の値に置き換えます。

	**Objective-C**

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	**Swift**

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",
	 							backendGUID: "applicationGUID")
	```

1. アプリ代行の `application:didFinishLaunchingWithOptions` メソッドに以下のコードを追加することで、Facebook SDK にアプリのアクティベーションについて通知し、Facebook Authentication Handler を登録します。このコードは IMFClient インスタンスを初期化した直後に追加してください。

	**Objective-C**

	```Objective-C
		[FBAppEvents activateApp];
		[[IMFFacebookAuthenticationHandler sharedInstance] registerWithDefaultDelegate];
```

	**Swift**

	```Swift
		FBAppEvents.activateApp()
		IMFFacebookAuthenticationHandler.sharedInstance().registerWithDefaultDelegate()
```

1. アプリ代行に以下のコードを追加します。

	**Objective-C**

	```Objective-C
	- (BOOL)application:(UIApplication *)application openURL:(NSURL *)url
			sourceApplication:(NSString *)sourceApplication annotation:(id)annotation {

		return [FBAppCall handleOpenURL:url sourceApplication:sourceApplication];


	}
```

	**Swift**

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

1. ブラウザーで、新しく作成されたモバイル・バックエンドの保護エンドポイントに要求を送信してみてください。次の URL を開きます。`{applicationRoute}/protected` (たとえば、 `http://my-mobile-backend.mybluemix.net/protected`)
<br/>MobileFirst Services Starter ボイラープレートを使用して作成されたモバイル・バックエンドの`/protected` エンドポイントは、{{site.data.keyword.amashort}}で保護されています。 `認証されていない`というメッセージがブラウザーに戻されます。このエンドポイントは {{site.data.keyword.amashort}} Client SDK により装備されたモバイル・アプリケーションからのみアクセス可能であるため、このメッセージが戻されます。
1. iOS アプリケーションを使用して同じエンドポイントに対する要求を作成します。

	**Objective-C**

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

	**Swift**

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

	この画面は、デバイスに Facebook アプリをインストールしていない場合、または現在 Facebook に ログインしていない場合は少し違って見えるかも知れません。 

1. 「**OK**」をクリックし、{{site.data.keyword.amashort}} が認証を目的として Facebook のユーザー ID を使用することを承認します。

1. 	要求が成功すると、以下の出力が Xcode コンソールに表示されます。
	![image](images/ios-facebook-login-success.png)



	次のコードを追加してログアウト機能を追加することもできます。


	**Objective-C**

	```Objective-C
	[[IMFFacebookAuthenticationHandler sharedInstance] logout : callBack]
	```

	**Swift**

	```Swift
	IMFFacebookAuthenticationHandler.sharedInstance().logout(callBack)
	```

	ユーザーが Facebook にログインした後でこのコードを呼び出し、そのユーザーが再度ログインしようとする場合、Mobile Client Access が認証を目的として Facebook を使用することについての許可を求めるプロンプトが出されます。

	ユーザーを切り替えるには、このコードを呼び出す必要があり、ユーザーはブラウザーで Facebook からログアウトしなければなりません。ログアウト機能へ `callBack` を渡すことは、オプションです。`nil` を渡すこともできます。

