---

copyright:
  years: 2015, 2016

---

# iOS Objective-C SDK のセットアップ
{: #getting-started-ios}

iOS アプリケーションに {{site.data.keyword.amashort}} SDK を装備し、SDK を初期化し、保護されたリソースまたは無保護のリソースへの要求を実行します。

**ヒント:** iOS アプリを Swift で作成している場合は、{{site.data.keyword.amashort}} Client Swift SDK を使用することを検討してください。詳細については、[iOS Swift SDK のセットアップ](getting-started-ios-swift-sdk.html)を参照してください。

## 開始する前に
{: #before-you-begin}
* {{site.data.keyword.amashort}} サービスによって保護されたモバイル・バックエンドのインスタンスが存在している必要があります。モバイル・バックエンドの作成方法について詳しくは、[入門](getting-started.html)を参照してください。
* Xcode が正しくセットアップされていることを確認してください。iOS 開発環境のセットアップ方法について詳しくは、[Apple 開発者の Web サイト](https://developer.apple.com/support/xcode/)を参照してください。


## {{site.data.keyword.amashort}} Client SDK のインストール
{: #install-mca-sdk-ios}
{{site.data.keyword.amashort}} SDK は、iOS プロジェクト用の依存関係マネージャーである CocoaPods とともに配布されています。CocoaPods は、自動的にリポジトリーから成果物をダウンロードし、iOS アプリケーションで使用できるようにします。


### CocoaPods のインストール
{: #install-cocoapods}
1. 端末を開き、**pod --version** コマンドを実行します。既に CocoaPods がインストールされている場合は、バージョン番号が表示されます。次のセクションにスキップして SDK をインストールできます。

1. CocoaPods をインストールしていない場合は、以下を実行します。
```
sudo gem install cocoapods```
詳細については、[CocoaPods の Web サイト](https://cocoapods.org/)を参照してください。

### CocoaPods を使用した {{site.data.keyword.amashort}} Client SDK のインストール
{: #install-sdk-cocoapods}

1. 端末で、iOS プロジェクトのルート・ディレクトリーにナビゲートします。

1. まだ CocoaPods 用にワークスペースを初期化していない場合は、`pod init` コマンドを実行します。<br/> CocoaPods が、iOS プロジェクトの依存関係を定義する `Podfile` ファイルを作成します。

1. `Podfile` ファイルを編集し、必要なターゲットに以下の行を追加します。

	```
	pod 'IMFCore'
	```

1. `Podfile` ファイルを保存し、コマンド・ラインから `pod install` を実行します。<br/>Cocoapods が、追加の依存関係をインストールします。進行状況と、どのコンポーネントが追加されたかを確認できます。<br/>
**重要**: CocoaPods は、`xcworkspace` ファイルを生成します。プロジェクトの開発を進めるためには、このファイルを開く必要があります。

1. iOS プロジェクト・ワークスペースを開きます。CocoaPods によって生成された `xcworkspace` ファイルを開きます。例えば、`{your-project-name}.xcworkspace` などです。`open {your-project-name}.xcworkspace` を実行します。

## {{site.data.keyword.amashort}} Client SDK の初期化
{: #init-mca-sdk-ios}

{{site.data.keyword.amashort}} Client SDK を使用するには、**「経路」** (`applicationRoute`) および **「アプリ GUID」** (`applicationGUID`) のパラメーターを渡すことによって、SDK を初期化する必要があります。


1. {{site.data.keyword.Bluemix_notm}} ダッシュボードのメインページからアプリをクリックします。「**Mobile オプション**」をクリックします。SDK を初期化するには、**「経路」**および**「アプリ GUID」**の値が必要です。

1. 以下のヘッダーを追加することで、{{site.data.keyword.amashort}} Client SDK を使用するクラスに `IMFCore` フレームワークをインポートします。

	**Objective-C:**
	 ```Objective-C
	#import <IMFCore/IMFCore.h>
	```

	**Swift:**

	{{site.data.keyword.amashort}} Client SDK は Objective-C によって実装されます。以下の手順に従って、Swift プロジェクトにブリッジング・ヘッダーを追加する必要がある場合があります。

	1. Xcode 内のプロジェクトを右クリックし、「**New File..**」を選択します。
	1. 「**iOS Source**」カテゴリーから「**Header file**」をクリックします。このファイルに `BridgingHeader.h` という名前を付けます。
	1. 次の行をブリッジング・ヘッダーに追加します。`#import <IMFCore/IMFCore.h>`
	1. Xcode でプロジェクトをクリックし、**「ビルド設定 (Build Settings)」**タブを選択します。
	1. `Objective-C Bridging Header` を探します。
	1. 値を、`BridgingHeader.h` ファイルのロケーション (例えば、`$(SRCROOT)/MyApp/BridgingHeader.h`) に設定します。
	1. プロジェクトをビルドすることで、Xcode によってご使用のブリッジング・ヘッダーが選択されることを確認してください。失敗メッセージは表示されないはずです。

1. 以下のコードを使用して、{{site.data.keyword.amashort}} Client SDK を初期化します。初期化コードを入れる場所は一般的に (必須ではありませんが)、アプリケーション代行の `application:didFinishLaunchingWithOptions` メソッドの中です。<br/>
*applicationRoute* および *applicationGUID* は、{{site.data.keyword.Bluemix_notm}} ダッシュボード内の**「モバイル・オプション」**の値に置換します。

	**Objective-C:
                    
**

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	**Swift:**

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",
	 							backendGUID: "applicationGUID")
	```

## モバイル・バックエンドへの要求の実行
{: #request}

{{site.data.keyword.amashort}} Client SDK が初期化された後、モバイル・バックエンドに要求を出すことができるようになります。

1. ブラウザーで、モバイル・バックエンド上の保護されたエンドポイントへの要求の送信を試行します。次の URL を開きます。`{applicationRoute}/protected` (たとえば、 `http://my-mobile-backend.mybluemix.net/protected`)
<br/>MobileFirst Services Starter ボイラープレートを使用して作成されたモバイル・バックエンドの`/protected` エンドポイントは、{{site.data.keyword.amashort}}で保護されています。このエンドポイントにアクセスできるのは、{{site.data.keyword.amashort}} Client SDK が装備されたモバイル・アプリケーションのみであるため、ブラウザーに `Unauthorized` メッセージが返されます。
1. iOS アプリケーションを使用して同じエンドポイントに対する要求を作成します。`IMFClient` を初期化した後に、以下のコードを追加します。

	**Objective-C:
                    
**

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

	**Swift:**

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
保護されているエンドポイントに繋がった場合、資格情報は必要とされません。アプリケーションにユーザーのログインを要求する場合、Facebook、Google またはカスタム認証を構成する必要があります。
  * [Facebook](facebook-auth-ios.html)
  * [Google](google-auth-ios.html)
  * [カスタム](custom-auth-ios.html)
