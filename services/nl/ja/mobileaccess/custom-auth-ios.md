---

copyright:
  years: 2015, 2016

---

# iOS 用の {{site.data.keyword.amashort}} Client SDK の構成
{: #custom-ios}

{{site.data.keyword.amashort}} Client SDK の使用および {{site.data.keyword.Bluemix}} へのアプリケーションの接続のためにカスタム認証を使用する iOS アプリケーションを構成します。

**ヒント:** iOS アプリを Swift で作成している場合は、{{site.data.keyword.amashort}} Client Swift SDK を使用することを検討してください。このページの手順は、{{site.data.keyword.amashort}} Client Objective-C SDK に適用されます。Swift SDK を使用する手順については、[iOS用の {{site.data.keyword.amashort}} Client SDK の構成 (Swift SDK)](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-ios-swift-sdk.html) を参照してください。

## 開始する前に
{: #before-you-begin}
カスタム ID プロバイダーを使用するように構成済みの{{site.data.keyword.amashort}} サービスのインスタンスにより保護されているリソースを持っている必要があります。また、モバイル・アプリに {{site.data.keyword.amashort}} Client SDK が装備されている必要があります。詳しくは、以下の情報を参照してください。

 * [{{site.data.keyword.amashort}} 入門](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [iOS Objective-C SDK のセットアップ](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios.html)
 * [カスタム ID プロバイダーの使用](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [カスタム ID プロバイダーの作成](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [カスタム認証用の {{site.data.keyword.amashort}} の構成 ](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)



## CocoaPods を使用した Client SDK のインストール
{: #custom-ios-sdk-cocoapods}
CocoaPods 依存関係マネージャーを使用して {{site.data.keyword.amashort}} Client SDK をインストールします。

1. 端末を開いて、iOS プロジェクトのルート・ディレクトリーに移動します。

1. `Podfile` を編集して以下の行を追加します。

	```
	pod 'IMFCore'
	```

1. コマンド・ラインで `pod install` を実行します。
追加された依存関係が CocoaPods によってインストールされます。進行状況および追加されたコンポーネントが表示されます。

**重要**: この時点で、CocoaPods によって生成された xcworkspace ファイルを使用してプロジェクトを開く必要があります。通常、名前は `{your-project-name}.xcworkspace` です。

1. コマンド・ラインから `open {your-project-name}.xcworkspace` を実行して、iOS プロジェクトのワークスペースを開きます。



### Client SDK の初期化 
{: #custom-ios-sdk-initialize}

アプリケーションの経路 (`applicationRoute`) および GUID (`applicationGUID`) のパラメーターを渡すことによって、SDK を初期化します。初期化コードを入れる場所は一般的に (必須ではありませんが)、アプリケーション代行の `application:didFinishLaunchingWithOptions` メソッドの中です。

1. アプリケーション・パラメーター値を取得します。{{site.data.keyword.Bluemix_notm}}ダッシュボードでアプリを開きます。**「モバイル・オプション」**をクリックし、**「経路」** (`applicationRoute`) と **「アプリ GUID」** (`applicationGUID`) の値を確認します。

1. Client SDK を使用したいクラスに `IMFCore` フレームワークをインポートします。

	Objective-C:
                    


	```Objective-C
	#import <IMFCore/IMFCore.h>
	```

	Swift:


	{{site.data.keyword.amashort}} Client SDK は Objective-C によって実装されます。この SDK を使用するために、Swift プロジェクトへのブリッジング・ヘッダーを追加する必要がある場合があります。

	* Xcode でプロジェクトを右クリックし、**「新規ファイル... (New File...)」**を選択します。
	* **「iOS ソース」**カテゴリーから**「ヘッダー・ファイル」**を選出します。このファイルに `BridgingHeader.h` という名前を付けます。
	* ブリッジング・ヘッダーに `#import <IMFCore/IMFCore.h>` を追加します。
	* Xcode でプロジェクトをクリックし、**「ビルド設定 (Build Settings)」**タブを選択します。
	* `Objective-C Bridging Header` を探します。
	* `BridgingHeader.h` ファイルの場所に値を設定します。例: `$(SRCROOT)/MyApp/BridgingHeader.h`
	* プロジェクトをビルドすることによって、Xcode によってブリッジング・ヘッダーが選出されることを検証します。

1. Client SDK を初期化します。applicationRoute および applicationGUID を、**「モバイル・オプション」**で取得した**「経路」** (`applicationRoute`) と **「アプリ GUID」** (`applicationGUID`) の値に置き換えます。

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


## IMFAuthenticationHandler 代行
{: #custom-ios-sdk-authhandler}


{{site.data.keyword.amashort}} Client SDK は、カスタム認証フローを実装するための `IMFAuthenticationHandler` インターフェースを提供します。`IMFAuthenticationHandler` は、認証プロセスの異なるフェーズで呼び出される 3 つのメソッドを公開します。

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
 						didReceiveAuthenticationChallenge:(NSDictionary*)challenge;
```

このメソッドは、{{site.data.keyword.amashort}} サービスからカスタム認証チャレンジを受け取ったときに呼び出されます。引数は次のとおりです。

* `IMFAuthenticationContext` プロトコルは、開発者が認証チャレンジ応答、または資格情報収集中の失敗 (例: ユーザーによる取り消し) を返すことができるように、{{site.data.keyword.amashort}} Client SDK によって提供されます。
* `NSDictionary` は、カスタム ID プロバイダーによって返されるカスタム認証チャレンジを含みます。

`authenticationContext:didReceiveAuthenticationChallenge` メソッドを呼び出すことによって、{{site.data.keyword.amashort}} Client SDK は制御を開発者に委任し、資格情報待ちモードに入ります。`IMFAuthenticationContext` プロトコル・メソッド (下記参照) のいずれかを使用して、資格情報を収集して {{site.data.keyword.amashort}} Client SDK に返すのは、開発者の責任です。

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
						didReceiveAuthenticationSuccess:(NSDictionary *)userInfo;
```

このメソッドは認証が成功した後で呼び出されます。引数は、IMFAuthenticationContext と、認証の成功についての詳しい情報を含む NSDictionary (オプション) です。

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
						didReceiveAuthenticationFailure:(NSDictionary*)userInfo;
```

このメソッドは認証が失敗した後で呼び出されます。引数は、IMFAuthenticationContext と、認証の失敗についての詳しい情報を含む NSDictionary (オプション) です。

## IMFAuthenticationContext プロトコル
{: #custom-ios-sdk-authcontext}


`IMFAuthenticationContext` は、カスタム `IMFAuthenticationHandler` の `authenticationContext:didReceiveAuthenticationChallenge` メソッドへの引数として提供されます。資格情報を収集すること、および、`IMFAuthenticationContext` メソッドを使用して資格情報を {{site.data.keyword.amashort}} Client SDK に返すか、または、失敗を報告することは、開発者の責任です。以下の方法の 1 つを使用します。


```
-(void) submitAuthenticationChallengeAnswer:(NSDictionary*) answer;

-(void) submitAuthenticationFailure:(NSDictionary*) userInfo;
```

## カスタム IMFAuthenticationDelegate の実装例
{: #custom-ios-sdk-sample}


IMFAuthenticationDelegate サンプルは、カスタム ID プロバイダーのサンプルと連携するよう設計されています。このサンプルは [Github リポジトリー](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)からダウンロードできます。

Objective-C:
                    


``` Objective-C
CustomAuthenticationDelegate.h
-----------------------------------
#import <Foundation/Foundation.h>

@import IMFCore;
@interface CustomAuthenticationDelegate : NSObject <IMFAuthenticationDelegate>
@end


CustomAuthenticationDelegate.m
-----------------------------------
#import "CustomAuthenticationDelegate.h"

@implementation CustomAuthenticationDelegate

-(void)authenticationContext:(id<IMFAuthenticationContext>)context
					didReceiveAuthenticationChallenge:(NSDictionary *)challenge{

	NSLog(@"didReceiveAuthenticationChallenge :: %@", challenge);

	// In this sample the IMFAuthenticationDelegate immediately returns a hardcoded
	// set of credentials. In a real life scenario this is where developer would
	// show a login screen, collect credentials and invoke
	// [context submitAuthenticationChallengeAnswer:] API

	NSDictionary *challengeAnswer = [NSDictionary dictionaryWithObjectsAndKeys:
									 @"john.lennon", @"username",
									 @"12345", @"password", nil];

	[context submitAuthenticationChallengeAnswer:challengeAnswer];

	// In case there was a failure collecting credentials you need to report
	// it back to the IMFAuthenticationContext. Otherwise Mobile Client
	// Access Client SDK will remain in a waiting-for-credentials state
	// forever
}

-(void)authenticationContext:(id<IMFAuthenticationContext>)context
					didReceiveAuthenticationSuccess:(NSDictionary *)userInfo{
	NSLog(@"didReceiveAuthenticationSuccess");


}

-(void)authenticationContext:(id<IMFAuthenticationContext>)context
					didReceiveAuthenticationFailure:(NSDictionary *)userInfo{
	NSLog(@"didReceiveAuthenticationFailure");

}

@end
```

Swift 実装:

```Swift
import Foundation

class CustomAuthenticationDelegate : NSObject, IMFAuthenticationDelegate{

	func authenticationContext(context: IMFAuthenticationContext!, didReceiveAuthenticationChallenge challenge: [NSObject : AnyObject]!) {

		NSLog("didReceiveAuthenticationChallenge :: %@", challenge)

		// In this sample the IMFAuthenticationDelegate immediately returns a hardcoded
		// set of credentials. In a real life scenario this is where developer would
		// show a login screen, collect credentials and invoke
		// context.submitAuthenticationChallengeAnswer() API

		let challengeAnswer: [String:String] = [
			"username":"john.lennon",
			"password":"12345"
		]

		context.submitAuthenticationChallengeAnswer(challengeAnswer)

		// In case there was a failure collecting credentials you need to report
		// it back to the IMFAuthenticationContext. Otherwise Mobile Client
		// Access Client SDK will remain in a waiting-for-credentials state
		// forever
	}


	func authenticationContext(context: IMFAuthenticationContext!, didReceiveAuthenticationSuccess userInfo: [NSObject : AnyObject]!) {
		NSLog("didReceiveAuthenticationSuccess")
	}

	func authenticationContext(context: IMFAuthenticationContext!, didReceiveAuthenticationFailure userInfo: [NSObject : AnyObject]!) {
		NSLog("didReceiveAuthenticationFailure")
	}
}
```

## カスタム IMFAuthenticationDelegate の登録

カスタム IMFAuthenticationDelegate を作成した後に、`IMFClient` に登録します。アプリケーション内で、保護リソースに要求を送信する前に、以下のコードを呼び出します。realmName には {{site.data.keyword.amashort}} ダッシュボードで指定したものを使用してください。

Objective-C アプリケーション:

```Objective-C
[[IMFClient sharedInstance]
				registerAuthenticationDelegate:[CustomAuthenticationDelegate new]
										forRealm:realmName];
```

Swift アプリケーション:
```Swift
IMFClient.sharedInstance().registerAuthenticationDelegate(CustomAuthenticationDelegate(),
									forRealm: realmName)
```




## 認証のテスト
{: #custom-ios-testing}
Client SDK を初期化し、カスタム `IMFAuthenticationDelegate` を登録した後、モバイル・バックエンドに要求を出すことを開始できます。

### 開始する前に
{: #custom-ios-testing-before}
{{site.data.keyword.mobilefirstbp}} ボイラープレートを使用して作成されたアプリケーションと、 `/protected` エンドポイントで{{site.data.keyword.amashort}} により保護されているリソースを持っている必要があります。

1. ブラウザーで `{applicationRoute}/protected` (例えば `http://my-mobile-backend.mybluemix.net/protected`) を開いて、モバイル・バックエンドの保護エンドポイントに要求を送信します。{{site.data.keyword.mobilefirstbp}} ボイラープレートを使用して作成されたモバイル・バックエンドの`/protected` エンドポイントは、{{site.data.keyword.amashort}} で保護されています。このエンドポイントは {{site.data.keyword.amashort}} Client SDK により装備されたモバイル・アプリケーションからのみアクセス可能です。
その結果、`承認されていない`というメッセージがブラウザーに表示されます。
1. iOS アプリケーションを使用して、同じエンドポイントへの要求を実行します。`BMSClient` を初期化し、カスタム `IMFAuthenticationDelegate` を登録した後に、以下のコードを追加します。

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
1. 	要求が成功したら、Xcode コンソールに次のような出力が表示されます。

	![image](images/ios-custom-login-success.png)
	
	
	
	次のコードを追加してログアウト機能を追加することもできます。

	Objective C: 

	```Objective-C
	[[IMFAuthorizationManager sharedInstance] logout : callBack]
	```
	Swift:
 

	```Swift
	IMFAuthorizationManager.sharedInstance().logout(callBack)
	```

ユーザーのログイン後に、このコードを呼び出すと、そのユーザーはログアウトされます。そのユーザーが再度ログインしようとする場合は、サーバーから受信した要求に再度応じる必要があります。ログアウト機能へ `callBack` を渡すことは、オプションです。`nil` を渡すこともできます。

