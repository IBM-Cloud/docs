# iOS アプリでの Google 認証の使用可能化
{: #google-auth-ios}

## 開始する前に
{: #google-auth-ios-before}
* {{site.data.keyword.amashort}} によって保護されたリソースと、{{site.data.keyword.amashort}} Client SDK が装備された iOS プロジェクトが必要です。詳しくは、[{{site.data.keyword.amashort}} 入門) ](getting-started.html)および [iOS SDK のセットアップ](getting-started-ios.html)を参照してください。  
* {{site.data.keyword.amashort}}  Server SDK を使用して手作業でバックエンド・アプリケーションを保護します。詳しくは、[リソースの保護](protecting-resources.html)を参照してください。


## iOS プラットフォーム用の Google プロジェクトの構成
{: #google-auth-ios-project}
Google を ID プロバイダーとして使用することを開始するには、Google Developer Console にプロジェクトを作成して、Google クライアント ID を取得します。このクライアント ID は、どのアプリケーションが接続を試行しているかを Google に知らせるための固有 ID です。既に Google プロジェクトがある場合は、プロジェクトの作成について説明している手順をスキップし、資格情報の追加を開始できます。

1. [Google Developer Console](https://console.developers.google.com) を開きます。

1. プロジェクトを作成します。**「Create project (プロジェクトの作成)」**をクリックします。

1. プロジェクトを選択し、**「Use Google APIs (Google API の使用)」**をクリックします。さらに、**「Enable APIs and get credentials like keys (API の使用可能化および鍵などの資格情報の取得)」**をクリックすることもできます。

1. API リストから Google+ API を選択し、**「Enable API (API の使用可能化)」**をクリックします。

1. **「資格情報 (Credentials)」>「Add credentials (資格情報の追加)」**をクリックし、**「OAuth 2.0 client ID (OAuth 2.0 クライアント ID)」**を選択します。

1. 同意コンソールで製品名を設定するよう要求される可能性があります。その場合は、設定してください。

1. この時点で、アプリケーション・タイプの選択が表示されます。**「iOS」**を選択します。

1. iOS クライアントに、意味のある名前を指定します。iOS アプリケーションの bundleID を指定します。iOS アプリケーションの bundleId を見つけるには、`info.plist` ファイル内、または Xcode プロジェクトの**「General (一般)」**タブで**「Bundle Identifier (バンドル ID)」**を探してください。

1. 新しい iOS のクライアント ID をメモします。この値は、{{site.data.keyword.Bluemix_notm}} にアプリケーションをセットアップする時に必要です。


## Google 認証用の {{site.data.keyword.amashort}} の構成
{: #google-auth-ios-config}

これで iOS のクライアント ID を取得したので、{{site.data.keyword.Bluemix_notm}} ダッシュボードで Google 認証を使用可能にすることができます。

1. {{site.data.keyword.Bluemix}} ダッシュボードを開き、{{site.data.keyword.Bluemix_notm}} アプリケーションをクリックします。

1. **「モバイル・オプション」**をクリックし、*applicationRoute* と *applicationGUID* の値をメモします。これらの値は、SDK を初期化するために必要です。

1. {{site.data.keyword.amashort}} タイルをクリックします。

1. {{site.data.keyword.amashort}} ダッシュボードが表示されます。

1. **「認証のセットアップ」**をクリックします。

1. **「Google」**をクリックします。

1. 前の手順で取得した iOS のクライアント ID を指定し、**「保存」**をクリックします。

## iOS 用の {{site.data.keyword.amashort}} Client SDK の構成
{: #google-auth-ios-sdk}

### Cocoapods を使用した {{site.data.keyword.amashort}} Client SDK のインストール
{: #google-auth-ios-sdk-cocoapods}

1. iOS プロジェクトにナビゲートします。

1. `Podfile` を編集し、必要なターゲットに以下の行を追加します。

	```
	pod 'IMFGoogleAuthentication'
	```

1. `Podfile` を保存し、コマンド・ラインから `pod install` を実行します。

1. Cocoapods が追加の依存関係をインストールします。進行状況と、どのコンポーネントが追加されたかが表示されます。

	> この時点から、Cocoapods によって生成された xcworkspace ファイルを常に使用してプロジェクトを開く必要があります。通常、このファイルの名前は {your-project-name}.xcworkspace となります。  

1. コマンド・ラインから `open {your-project-name}.xcworkspace` を実行して、iOS プロジェクト・ワークスペースを開きます。

### Google 認証用の iOS プロジェクトの構成
{: #google-auth-ios-googleauth}

1. `info.plist` ファイルを見つけます。このファイルは、通常、Xcode プロジェクトの `Supporting files` フォルダーにあります。

1. 以下の 2 つの URL スキームを `info.plist` ファイルに追加して、Google 統合を構成します。

	![image](images/ios-google-infoplist-settings.png)

	> 最初の URL スキーマは、Google Developer Console から取得した、リバースされたクライアント ID です。例えば、ユーザーのクライアント ID が `123123-abcabc.apps.googleusercontent.com` の場合、URL スキーマは `com.googleusercontent.apps.123123-abcabc` となります。
	> 2 番目の URL スキーマは、アプリケーションのバンドル ID です。

1. 代わりに、`info.plist` ファイルを右クリックし、「`Open as`」->「`Source code`」を選択し、以下の XML を追加することにより、info.plist ファイルを更新することができます。

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
	> 以下の説明に従って両方の URL スキーマを更新します。

	> `info.plist` 内の既存のプロパティーはオーバーライドしないようにしてください。オーバーラップするプロパティーがある場合は、手動でマージする必要があります。追加情報については、Google 資料の [Try Sign-In for iOS](https://developers.google.com/identity/sign-in/ios/start) セクションを参照してください。
## {{site.data.keyword.amashort}} Client SDK の初期化
{: #google-auth-ios-initialize}

{{site.data.keyword.amashort}} Client SDK を使用できるようにするには、applicationGUID パラメーターと applicationRoute パラメーターを渡して初期化する必要があります。

> 初期化コードを入れる場所は一般的に (必須ではありませんが)、アプリケーション代行の `application:didFinishLaunchingWithOptions` メソッドの中です。1. {{site.data.keyword.Bluemix_notm}} ダッシュボードのメインページを開き、以前に作成したアプリをクリックします。これにより、モバイル・バックエンド・アプリのダッシュボードが開きます。

2. ダッシュボードの右上部にある`「モバイル・オプション」`をクリックします。「アプリケーション経路 (Application Route)」と「アプリケーション GUID (Application GUID)」の値が表示されます。

1. 以下のヘッダーを追加して、{{site.data.keyword.amashort}} Client SDK を使用するクラス内に必要なフレームワークをインポートします。

	Objective-C アプリケーション:

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>
	```

	Swift アプリケーション:

	{{site.data.keyword.amashort}} Client SDK は、Objective-C を使用して実装されます。したがって、それを使用するためには、ブリッジング・ヘッダーを Swift プロジェクトに追加する必要がある場合があります。

	* Xcode 内のプロジェクトを右クリックし、「`New File...`」を選択します。
	* 「`iOS Source`」カテゴリーから「`Header file`」を選択します。
	* それに「`BridgingHeader.h`」という名前を付けます。
	* 以下の import をブリッジング・ヘッダーに追加します。

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>
	```
	* Xcode でプロジェクトをクリックし、`「ビルド設定 (Build Settings)」`タブを選択します。
	* `Objective-C Bridging Header` を探します。
	* この値を、`BridgingHeader.h` ファイルのロケーション (例えば、`$(SRCROOT)/MyApp/BridgingHeader.h`) に設定します。
	* プロジェクトをビルドして、ブリッジング・ヘッダーが Xcode によって取得されることを確認します。失敗メッセージは表示されないはずです。

3. 以下のコードを使用して Client SDK を初期化します。

	Objective-C アプリケーション:

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	Swift アプリケーション:

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",
	 							backendGUID: "applicationGUID")
	```

	> applicationRoute および applicationGUID は、「モバイル・オプション」から取得した値に置換します。

1. アプリ代行内の `application:didFinishLaunchingWithOptions` メソッドに以下のコードを追加して、Google 認証ハンドラーを登録します。この作業は、IMFClient の初期化直後に行うことを推奨します。

	Objective-C アプリケーション:

	```Objective-C
	[[IMFGoogleAuthenticationHandler sharedInstance] registerWithDefaultDelegate];
	```

	Swift アプリケーション:

	```Swift
	IMFGoogleAuthenticationHandler.sharedInstance().registerWithDefaultDelegate()
	```

1. 以下のコードをアプリ代行に追加します。

	Objective-C アプリケーション:

	```Objective-C
	- (void)applicationDidBecomeActive:(UIApplication *)application {
		[[IMFGoogleAuthenticationHandler sharedInstance] handleDidBecomeActive];
	}

	- (BOOL)application: (UIApplication *)application openURL: (NSURL *)url
					sourceApplication: (NSString *)sourceApplication annotation: (id)annotation {

		BOOL shouldHandleGoogleURL = [GPPURLHandler handleURL:url sourceApplication:sourceApplication annotation:annotation];


		[[IMFGoogleAuthenticationHandler sharedInstance] handleOpenURL:shouldHandleGoogleURL];
		return  shouldHandleGoogleURL;
	}
	```

	Swift アプリケーション:

	```Swift
	func application(application: UIApplication, openURL url: NSURL,
					sourceApplication: String?, annotation: AnyObject) -> Bool {

		let shouldHandleGoogleURL = GPPURLHandler.handleURL(url,
				sourceApplication: sourceApplication, annotation: annotation)

		IMFGoogleAuthenticationHandler.sharedInstance().handleOpenURL(shouldHandleGoogleURL)


		return shouldHandleGoogleURL;
	}
```

## 認証のテスト
{: #google-auth-ios-testing}
Client SDK が初期化されたら、モバイル・バックエンドへの要求の実行を開始できます。

### 開始する前に
{: #google-auth-ios-testing-before}
{{site.data.keyword.mobilefirstbp}} ボイラープレートを使用していて、{{site.data.keyword.amashort}}により`/protected` エンドポイントで保護されているリソースを既に持っている必要があります。`/protected` エンドポイントをセットアップする必要がある場合、[リソースの保護 ](protecting-resources.html)を参照してください。


1. デスクトップ・ブラウザーで、`http://{appRoute}/protected` を開いて、モバイル・バックエンドの保護エンドポイント (例: `http://my-mobile-backend.mybluemix.net/protected`) に要求を送信することを試みます。
1. MobileFirst Services ボイラープレートを使用して作成されたモバイル・バックエンドの `/protected` エンドポイントは、{{site.data.keyword.amashort}} によって保護されています。したがって、このエンドポイントにアクセスできるのは、{{site.data.keyword.amashort}} Client SDK の装備されたモバイル・アプリケーションのみとなります。結果的に、デスクトップ・ブラウザーに `Unauthorized` が表示されます。

1. iOS アプリケーションを使用して、同じエンドポイントへの要求を実行します。

	Objective-C:
                    


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
			NSLog("%@", IMFAuthorizationManager.sharedInstance().userIdentity)
		}
	}];
	```

	Swift:

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

1. アプリケーションを実行します。Google のログイン画面のポップアップが表示されます。

	![image](images/ios-google-login.png)

	この画面は、デバイスに Facebook アプリをインストールしていない場合、または現在 Facebook に ログインしていない場合は少し違って見えるかも知れません。 

1. **「OK」**をクリックして、{{site.data.keyword.amashort}} が Google ユーザー ID を認証目的に使用することを許可します。

1. 	ユーザーの要求は正常に処理されます。LogCat に以下の出力が表示されます。

	![image](images/ios-google-login-success.png)
