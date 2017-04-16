---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-02"

---
{:shortdesc: .shortdesc}

# iOS Objective-C SDK のセットアップ
{: #getting-started-ios}

iOS アプリケーションに {{site.data.keyword.amafull}} SDK を装備し、SDK を初期化し、保護されたリソースまたは無保護のリソースへの要求を実行します。


{:shortdesc}

**重要:** Objective-C SDK は現在も完全にサポートされており、{{site.data.keyword.Bluemix_notm}} モバイル・サービス用の主要 SDK とされていますが、この SDK は今年後半には廃止され、新しい Swift SDK が後継になる予定です。新規アプリケーションには Swift SDK を使用することを強くお勧めします ([iOS Swift SDK のセットアップ](getting-started-ios-swift-sdk.html)を参照してください)。

## 開始する前に
{: #before-you-begin}
以下が必要です。
* {{site.data.keyword.amashort}} サービスによって保護された {{site.data.keyword.Bluemix_notm}} アプリケーションのインスタンス。{{site.data.keyword.Bluemix_notm}} バックエンド・アプリケーションの作成方法について詳しくは、[概説](index.html)を参照してください。




* **「TenantID」**。{{site.data.keyword.amashort}} ダッシュボードでサービスを開きます。**「モバイル・オプション」**をクリックします。`tenantId` (`appGUID` とも呼ばれる) の値が、**「アプリ GUID」/「TenantId」**フィールドに表示されます。{{site.data.keyword.amashort}} 許可マネージャーを初期化するためにこの値が必要になります。
* **「アプリケーションの経路 (Application Route)」**。これは、バックエンド・アプリケーションの URL です。保護されているエンドポイントに要求を送信するためにこの値が必要になります。
* Xcode プロジェクト。  


## {{site.data.keyword.amashort}} Client SDK のインストール
{: #install-mca-sdk-ios}
{{site.data.keyword.amashort}} SDK は、iOS プロジェクト用の依存関係マネージャーである CocoaPods とともに配布されています。CocoaPods は、自動的にリポジトリーから成果物をダウンロードし、iOS アプリケーションで使用できるようにします。


### CocoaPods のインストール
{: #install-cocoapods}

1. 端末を開き、**pod --version** コマンドを実行します。既に CocoaPods がインストールされている場合は、バージョン番号が表示されます。次のセクションにスキップして SDK をインストールします。

1. CocoaPods をインストールしていない場合は、以下を実行します。

```
sudo gem install cocoapods
```

詳細については、[CocoaPods の Web サイト](https://cocoapods.org/)を参照してください。

### CocoaPods を使用した {{site.data.keyword.amashort}} Client SDK のインストール
{: #install-sdk-cocoapods}

1. 端末で、iOS プロジェクトのルート・ディレクトリーにナビゲートします。

1. まだ CocoaPods 用にワークスペースを初期化していない場合は、`pod init` コマンドを実行します。<br/> CocoaPods が、iOS プロジェクトの依存関係を定義する `Podfile` ファイルを作成します。

1. `Podfile` ファイルを編集し、必要なターゲットに以下の行を追加します。


	`pod 'IMFCore'`

1. `Podfile` ファイルを保存し、コマンド・ラインから `pod install` を実行します。<br/>Cocoapods が追加の依存関係をインストールし、追加されたコンポーネントを表示します。<br/>

	**重要**: CocoaPods は `xcworkspace` ファイルを生成します。プロジェクトの開発を進めるためには、このファイルを開く必要があります。

1. iOS プロジェクト・ワークスペースを開きます。CocoaPods によって生成された `xcworkspace` ファイルを開きます。例えば、`{your-project-name}.xcworkspace` などです。`open {your-project-name}.xcworkspace` を実行します。

## {{site.data.keyword.amashort}} Client SDK の初期化
{: #init-mca-sdk-ios}

1. 以下のヘッダーを追加することで、{{site.data.keyword.amashort}} Client SDK を使用するクラスに `IMFCore` フレームワークをインポートします。

	####Objective-C
	{: #imfcore-objc}

	```Objective-C
	  #import <IMFCore/IMFCore.h>
	```

	####Swift
	{: #sdk-swift}

	{{site.data.keyword.amashort}} Client SDK は Objective-C によって実装されます。以下の手順に従って、Swift プロジェクトにブリッジング・ヘッダーを追加する必要がある場合があります。
	1. Xcode でプロジェクトを右クリックし、**「新規ファイル (New File)」**を選択します。
	1. 「**iOS Source**」カテゴリーから「**Header file**」をクリックします。このファイルに `BridgingHeader.h` という名前を付けます。
	1. ブリッジング・ヘッダーに次の行を追加します。`#import <IMFCore/IMFCore.h>`。
	1. Xcode でプロジェクトをクリックし、**「ビルド設定 (Build Settings)」**タブを選択します。
	1. `Objective-C Bridging Header` を探します。
	1. 値を、`BridgingHeader.h` ファイルのロケーション (例えば、`$(SRCROOT)/MyApp/BridgingHeader.h`) に設定します。
	1. プロジェクトをビルドすることで、Xcode によってご使用のブリッジング・ヘッダーが選択されることを確認してください。失敗メッセージは表示されないはずです。

1. 以下のコードを使用して、{{site.data.keyword.amashort}} Client SDK を初期化します。初期化コードを入れる場所は一般的に (必須ではありませんが)、アプリケーション代行の `application:didFinishLaunchingWithOptions` メソッドの中です。<br/>
`applicationRoute` および `applicationGUID` の取得については、[開始する前に](#before-you-begin)を参照してください。 

	####Objective-C
	{: #sharedinstance-objc}

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	####Swift
	{: #sharedinstance-swift}
	```Swift
 		MFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",backendGUID: "applicationGUID")
	```

## AuthorizationManager の初期化
{{site.data.keyword.amashort}} サービスの `tenantId` パラメーターを渡すことによって、`AuthorizationManager` を初期化します。これらの値の取得については、[開始する前に](#before-you-begin)を参照してください。 

####Objective-C

```Objective-C
[[IMFAuthorizationManager sharedInstance]  initializeWithTenantId: @"<tenantId>"];
```

####Swift

```Swift
IMFAuthorizationManager.sharedInstance().initializeWithTenantId("<tenantId>")
```

	
## モバイル・バックエンド・アプリケーションへの要求の実行
{: #request}

{{site.data.keyword.amashort}} Client SDK が初期化された後、モバイル・バックエンド・アプリケーションに要求を出すことができるようになります。

1. ブラウザーで、モバイル・バックエンド・アプリケーション上の保護されたエンドポイントへの要求の送信を試行します。次の URL を開きます。`{applicationRoute}/protected` (たとえば、 `http://my-mobile-backend.mybluemix.net/protected`)
<br/>MobileFirst Services Starter ボイラープレートを使用して作成されたモバイル・バックエンド・アプリケーションの `/protected` エンドポイントは、{{site.data.keyword.amashort}} で保護されています。このエンドポイントにアクセスできるのは、{{site.data.keyword.amashort}} Client SDK が装備されたモバイル・アプリケーションのみであるため、ブラウザーに `Unauthorized` メッセージが返されます。

1. iOS アプリケーションを使用して、同じエンドポイントへ要求を出します。`IMFClient` を初期化した後に、以下のコードを追加します。

	####Objective-C
	{: #nsstring-objc}

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
		}
	}];
	```

	####Swift
	{: #imfclientrequestpath-swift}

	```Swift
	let requestPath = IMFClient.sharedInstance().backendRoute + "/protected"

	let request = IMFResourceRequest(path: requestPath, method: "GET");
	request.sendWithCompletionHandler { (response, error) -> Void in
		if (nil != error){
			NSLog("Error :: %@", error.description)
		} else {
			NSLog("Response :: %@", response.responseText)
		}
	};

	```

1.  要求が正常に実行されると、Xcode コンソールに以下の出力が表示されます。

	![image](images/getting-started-ios-success.png)

## 次のステップ
{: #next-steps}
保護されているエンドポイントに接続する場合、資格情報は必要ありませんでした。アプリケーションにユーザーのログインを要求する場合、Facebook、Google またはカスタム認証を構成する必要があります。
  * [Facebook](facebook-auth-ios.html)
  * [Google](google-auth-ios.html)
  * [カスタム](custom-auth-ios.html)
