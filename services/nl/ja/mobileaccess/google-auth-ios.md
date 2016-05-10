---

copyright:
  years: 2015, 2016

---

# iOS アプリでの Google 認証の使用可能化
{: #google-auth-ios}

**ヒント:** iOS アプリを Swift で作成している場合は、{{site.data.keyword.amashort}} Client Swift SDK を使用することを検討してください。このページの手順は、{{site.data.keyword.amashort}} Client Objective-C SDK に適用されます。Swift SDK を使用する手順については、 [iOS アプリで Google 認証を使用可能にする (Swift SDK)](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html) を参照してください。

## 開始する前に
{: #google-auth-ios-before}
* {{site.data.keyword.amashort}} によって保護されたリソースと、{{site.data.keyword.amashort}} Client SDK が装備された iOS プロジェクトが必要です。詳しくは、[{{site.data.keyword.amashort}} 入門](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)および [iOS Objective-C SDK のセットアップ](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios.html)を参照してください。  
* {{site.data.keyword.amashort}}  Server SDK を使用して手作業でバックエンド・アプリケーションを保護します。詳しくは、[リソースの保護](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)を参照してください。


## iOS プラットフォーム用の Google プロジェクトの構成
{: #google-auth-ios-project}
Google を ID プロバイダーとして使用することを開始するには、Google Developer Console にプロジェクトを作成して、Google クライアント ID を取得します。このクライアント ID は、どのアプリケーションが接続を試行しているかを Google に知らせるための固有 ID です。既に Google プロジェクトがある場合は、プロジェクトの作成について説明している手順をスキップし、資格情報の追加を開始できます。



1. [Google Developer Console](https://console.developers.google.com)にプロジェクトを作成します。既にプロジェクトがある場合は、プロジェクト作成について説明している手順をスキップし、資格情報の追加を開始してください。
   1.    新規プロジェクトのメニューを開きます。 
         
         ![image](images/FindProject.jpg)

   2.    **「プロジェクトの作成 (Create a project)」**をクリックします。
   
         ![image](images/CreateAProject.jpg)


1. **「Social API」**リストから、**「Google+ API」**を選択します。

     ![image](images/chooseGooglePlus.jpg)

1. 次の画面から、**「使用可能 (Enable)」**をクリックします。

1. **「同意取得」**タブを選択し、ユーザーに表示する製品名を指定します。その他の値はオプションです。**「保存」**をクリックします。

    ![image](images/consentScreen.png)
    
1. **「資格情報」**リストから、「OAuth クライアント ID」を選択します。

     ![image](images/chooseCredentials.png)
     


1. この時点で、アプリケーション・タイプの選択が表示されます。**「iOS」**を選択します。

1. iOS クライアントに、意味のある名前を指定します。iOS アプリケーションのバンドル ID を指定します。iOS アプリケーションのバンドル ID を見つけるには、`info.plist` ファイル内、または Xcode プロジェクトの**「General (一般)」**タブで**「Bundle Identifier (バンドル ID)」**を探してください。

1. 新しい iOS のクライアント ID をメモします。この値は、{{site.data.keyword.Bluemix}} にアプリケーションをセットアップする時に必要です。


## Google 認証用の {{site.data.keyword.amashort}} の構成
{: #google-auth-ios-config}

これで iOS のクライアント ID を取得したので、{{site.data.keyword.Bluemix_notm}} ダッシュボードで Google 認証を使用可能にすることができます。

1. {{site.data.keyword.Bluemix_notm}}ダッシュボードでアプリを開きます。

1. **「モバイル・オプション」**をクリックし、**「経路」** (`applicationRoute`) と **「アプリ GUID」** (`applicationGUID`) のメモを取ります。SDK を初期化する際に、これらの値が必要になります。

1. {{site.data.keyword.amashort}} タイルをクリックします。{{site.data.keyword.amashort}} ダッシュボードがロードされます。

1. **「Google」**タイルをクリックします。

1. **「iOS のアプリケーション ID (Application ID for iOS)」**で、Android の iOS クライアント ID を指定し、**「保存」**をクリックします。

	注: Google クライアント ID に加えて、クライアント構成にはリバース値も必要です (下記を参照)。両方の値にアクセスするには、鉛筆のアイコンを使用してサンプルの plist をダウンロードします。![info.plist file download](images/download_plist.png)

## iOS 用の {{site.data.keyword.amashort}} Client SDK の構成
{: #google-auth-ios-sdk}

### CocoaPods を使用した {{site.data.keyword.amashort}} Client SDK のインストール
{: #google-auth-ios-sdk-cocoapods}

1. iOS プロジェクトにナビゲートします。

1. `Podfile` を編集して以下の行を追加します。

	```
	pod 'IMFGoogleAuthentication'
	```

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
	両方の URL スキーマを更新します。

	**重要**: `info.plist` ファイル内の既存のプロパティーをオーバーライドしないでください。オーバーラップするプロパティーがある場合は、それらのプロパティーを手動でマージする必要があります。詳細については、[Try Sign-In for iOS](https://developers.google.com/identity/sign-in/ios/start) を参照してください。

## {{site.data.keyword.amashort}} Client SDK の初期化
{: #google-auth-ios-initialize}

{{site.data.keyword.amashort}} Client SDK を使用するには、applicationGUID パラメーターと applicationRoute パラメーターを渡して初期化します。

初期化コードを入れる場所は一般的に (必須ではありませんが)、アプリケーション代行の `application:didFinishLaunchingWithOptions` メソッドの中です。

1. applicationGUID と applicationRoute の値を取得します。{{site.data.keyword.Bluemix_notm}} ダッシュボードからアプリをクリックします。「**Mobile オプション**」をクリックします。アプリケーション経路とアプリケーション GUID の値が表示されます。

1. {{site.data.keyword.amashort}} Client SDK を使用したいクラス内で必要なフレームワークをインポートします。以下のヘッダーを追加します。

	Objective-C:
                    


	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>
	```

	Swift:

	{{site.data.keyword.amashort}} Client SDK は Objective-C によって実装されます。この SDK を使用するために、Swift プロジェクトへのブリッジング・ヘッダーを追加する必要がある場合があります。

	1. Xcode でプロジェクトを右クリックし、**「新規ファイル... (New File...)」**を選択します。
	2. **「iOS ソース」**カテゴリーから**「ヘッダー・ファイル」**を選出します。
	3. それに「`BridgingHeader.h`」という名前を付けます。
	4. ブリッジング・ヘッダーに以下のインポートを追加します。

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>
	```
	5. Xcode でプロジェクトをクリックし、**「ビルド設定 (Build Settings)」**タブを選択します。
	6. `Objective-C Bridging Header` を探します。
	7. 値を、`BridgingHeader.h` ファイルのロケーション (例えば、`$(SRCROOT)/MyApp/BridgingHeader.h`) に設定します。
	8. プロジェクトをビルドすることで、Xcode によってご使用のブリッジング・ヘッダーが選択されることを確認してください。

3. 以下のコードを使用して、Client SDK を初期化します。*applicationRoute* および *applicationGUID* を、**「モバイル・オプション」**から取得した**「経路」**および**「アプリ GUID」**の値に置き換えます。

	Objective-C:
                    


	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	Swift:

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",
	 							backendGUID: "applicationGUID")
	```



1. アプリ代行内の `application:didFinishLaunchingWithOptions` メソッドに以下のコードを追加して、Google 認証ハンドラーを登録します。このコードは、IMFClient の初期化の直後に追加してください。

	Objective-C:
                    


	```Objective-C
	[[IMFGoogleAuthenticationHandler sharedInstance] registerWithDefaultDelegate];
	```

	Swift:

	```Swift
	IMFGoogleAuthenticationHandler.sharedInstance().registerWithDefaultDelegate()
	```

1. アプリ代行に以下のコードを追加します。

	Objective-C:
                    


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

	Swift:

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
{{site.data.keyword.mobilefirstbp}} ボイラープレートを使用していて、{{site.data.keyword.amashort}}により`/protected` エンドポイントで保護されているリソースを既に持っている必要があります。`/protected` エンドポイントをセットアップする必要がある場合、[リソースの保護 ](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)を参照してください。


1. `{applicationRoute}/protected` (例えば、`http://my-mobile-backend.mybluemix.net/protected`) を開いて、デスクトップ・ブラウザーで、モバイル・バックエンドの保護エンドポイントに要求を送信してみてください。

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
			NSLog(@"%@", [[IMFAuthorizationManager sharedInstance] userIdentity]);
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
	
	
	次のコードを追加してログアウト機能を追加することもできます。
	
	Objective C:
	
	```Objective-C
	[[IMFGoogleAuthenticationHandler sharedInstance] logout : callBack]
	```

	Swift:

	```Swift
	IMFGoogleAuthenticationHandler.sharedInstance().logout(callBack)
	```


	ユーザーが Google にログインした後でこのコードを呼び出し、そのユーザーが再度ログインしようとする場合、Mobile Client Access が認証を目的として Google を使用することについての許可を求めるプロンプトが出されます。その時点で、画面の右上隅にあるユーザー名をクリックすると、別のユーザーを選択してログインすることができます。

	ログアウト機能へ `callBack` を渡すことは、オプションです。`nil` を渡すこともできます。
