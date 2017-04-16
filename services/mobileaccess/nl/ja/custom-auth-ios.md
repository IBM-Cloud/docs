---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-07"

---

# iOS 用の {{site.data.keyword.amashort}} Client SDK の構成 (Objective-C)
{: #custom-ios}


{{site.data.keyword.amafull}} Client SDK の使用および {{site.data.keyword.Bluemix}} へのアプリケーションの接続のためにカスタム認証を使用する iOS アプリケーションを構成します。

**注:** iOS アプリを Swift で作成している場合は、{{site.data.keyword.amashort}} Client Swift SDK を使用することを検討してください。このページの手順は、{{site.data.keyword.amashort}} Client Objective-C SDK に適用されます。新しい Swift SDK を使用する手順については、[iOS 用の {{site.data.keyword.amashort}} Client SDK の構成 (Swift SDK)](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-ios-swift-sdk.html) を参照してください。

## 開始する前に
{: #before-you-begin}
以下が必要です。

* カスタム ID プロバイダーを使用するように構成済みの {{site.data.keyword.amashort}} サービスのインスタンスによって保護されているリソース ([カスタム認証の構成](https://console.stage1.ng.bluemix.net/docs/services/mobileaccess/custom-auth-config-mca.html)を参照してください)。  
* **TenantID** 値。{{site.data.keyword.amashort}} ダッシュボードでサービスを開きます。**「モバイル・オプション」**ボタンをクリックします。`tenantId` (`appGUID` とも呼ばれる) の値が、**「アプリ GUID」/「TenantId」**フィールドに表示されます。許可マネージャーを初期化するためにこの値が必要になります。
* **「レルム」**名。これは、{{site.data.keyword.amashort}} ダッシュボードの**「管理」**タブで、**「カスタム」**セクションの**「レルム名」**フィールドに指定した値です ([カスタム認証の構成](https://console.stage1.ng.bluemix.net/docs/services/mobileaccess/custom-auth-config-mca.html)を参照してください)。
* バックエンド・アプリケーションの URL (**「アプリの経路 (App Route)」**)。バックエンド・アプリケーションの保護されたエンドポイントに要求を送信するためにこの値が必要になります。
* {{site.data.keyword.Bluemix_notm}} **「地域」**。**「アバター」**アイコン![「アバター」アイコン](images/face.jpg "「アバター」アイコン") の横のヘッダー内に現在の {{site.data.keyword.Bluemix_notm}} 地域が表示されます。表示される地域の値は、`「米国南部」`、`「英国」`、または`「シドニー」`のいずれかでなければならず、また WebView Javascript コードで必要な SDK 値 (`BMSClient.REGION_US_SOUTH`、`BMSClient.REGION_UK`、または `BMSClient.REGION_SYDNEY`) に対応している必要があります。{{site.data.keyword.amashort}} クライアントを初期化するためにこの値が必要になります。

詳しくは、以下の情報を参照してください。

 * [{{site.data.keyword.amashort}} 概説](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
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

**「アプリの経路 (App Route)」** (`applicationRoute`) および**「TenantID」** (`tenantID`) の各パラメーターを渡して、SDK を初期化します。 

初期化コードを入れる場所は一般的に (必須ではありませんが)、アプリケーション代行の `application:didFinishLaunchingWithOptions` メソッドの中です。

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

1. Client SDK を初期化します。**「アプリの経路 (App Route)」** (`applicationRoute`) および**「TenantID」** (`tenantID`) を値に置き換えます。これらの値の取得について詳しくは、[開始する前に](##before-you-begin)を参照してください。

	Objective-C:

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"tenantID"];
	```

	Swift:

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",
	 							backendGUID: "tenantID")
	```

## AuthorizationManager の初期化
{{site.data.keyword.amashort}} サービスの `tenantId` パラメーターを渡すことによって、AuthorizationManager を初期化します。 


### Objective-C:

```Objective-
 [[IMFAuthorizationManager sharedInstance]  initializeWithTenantId: @"tenantId"];
```

### Swift:

```Swift
  IMFAuthorizationManager.sharedInstance().initializeWithTenantId("tenantId")
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

`authenticationContext:didReceiveAuthenticationChallenge` メソッドを呼び出すことによって、{{site.data.keyword.amashort}} Client SDK は制御を開発者に委任し、資格情報待ちモードに入ります。資格情報を収集し、以下の `IMFAuthenticationContext` プロトコル・メソッドのいずれかを使用して {{site.data.keyword.amashort}} Client SDK に報告を返すのは、開発者の責任です。

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
						didReceiveAuthenticationSuccess:(NSDictionary *)userInfo;
```

このメソッドは認証が成功した後で呼び出されます。引数には、`IMFAuthenticationContext` と、認証の成功に関する詳しい情報を含む `NSDictionary` (オプション) があります。

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
						didReceiveAuthenticationFailure:(NSDictionary*)userInfo;
```

このメソッドは認証が失敗した後で呼び出されます。引数には、`IMFAuthenticationContext` と、認証の失敗に関する詳しい情報を含む `NSDictionary` (オプション) があります。

## IMFAuthenticationContext プロトコル
{: #custom-ios-sdk-authcontext}


`IMFAuthenticationContext` プロトコルは、カスタム `IMFAuthenticationHandler` の `authenticationContext:didReceiveAuthenticationChallenge` メソッドへの引数として提供されます。資格情報を収集し、`IMFAuthenticationContext` メソッドを使用して資格情報を {{site.data.keyword.amashort}} Client SDK に返すか、失敗を報告することは、開発者の責任です。 
```
-(void) submitAuthenticationChallengeAnswer:(NSDictionary*) answer;

-(void) submitAuthenticationFailure:(NSDictionary*) userInfo;
```

## カスタム IMFAuthenticationDelegate の実装例
{: #custom-ios-sdk-sample}


IMFAuthenticationDelegate サンプルは、カスタム ID プロバイダーのサンプルと連携するよう設計されています。このサンプルは、[GitHub リポジトリー](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)からダウンロードできます。

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

	// In this sample, the IMFAuthenticationDelegate immediately returns a hardcoded
	// set of credentials. In a real life scenario, a developer would
	// show a login screen, collect credentials and invoke the
	// [context submitAuthenticationChallengeAnswer:] API

	NSDictionary *challengeAnswer = [NSDictionary dictionaryWithObjectsAndKeys:
									 @"john.lennon", @"username",
									 @"12345", @"password", nil];

	[context submitAuthenticationChallengeAnswer:challengeAnswer];

	// In case there is a failure collecting credentials, report
	// the failure to IMFAuthenticationContext. Otherwise, the Mobile Client
	// Access client SDK remains in a waiting-for-credentials state
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

	func authenticationContext(context: IMFAuthenticationContext!,
					didReceiveAuthenticationChallenge challenge: [NSObject : AnyObject]!) {

		NSLog("didReceiveAuthenticationChallenge :: %@", challenge)

		// In this sample, the IMFAuthenticationDelegate immediately returns a hardcoded
		// set of credentials. In a real life scenario a developer would
		// show a login screen, collect credentials and invoke the
		// context.submitAuthenticationChallengeAnswer() API

		let challengeAnswer: [String:String] = [
			"username":"john.lennon",
			"password":"12345"
		]

		context.submitAuthenticationChallengeAnswer(challengeAnswer)

		// In case there is a failure collecting credentials, report
		// it back to IMFAuthenticationContext. Otherwise, the Mobile Client
		// Access client SDK remains in a waiting-for-credentials state
		// forever
	}


	func authenticationContext(context: IMFAuthenticationContext!,
					didReceiveAuthenticationSuccess userInfo: [NSObject : AnyObject]!) {
		NSLog("didReceiveAuthenticationSuccess")
	}

	func authenticationContext(context: IMFAuthenticationContext!,
					didReceiveAuthenticationFailure userInfo: [NSObject : AnyObject]!) {
		NSLog("didReceiveAuthenticationFailure")
	}
}
```

## カスタム IMFAuthenticationDelegate の登録

カスタム `IMFAuthenticationDelegate` を作成した後に、`IMFClient` に登録します。アプリケーション内で、保護リソースに要求を送信する前に、以下のコードを呼び出します。`realmName` には {{site.data.keyword.amashort}} ダッシュボードで指定したものを使用してください。

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
Client SDK を初期化し、カスタム `IMFAuthenticationDelegate` の登録が完了すると、モバイル・バックエンド・アプリケーションに要求を出すことができるようになります。

### 開始する前に
{: #custom-ios-testing-before}
{{site.data.keyword.mobilefirstbp}} ボイラープレートを使用して作成されたアプリケーションと、 `/protected` エンドポイントで{{site.data.keyword.amashort}} により保護されているリソースを持っている必要があります。

1. ブラウザーで `{applicationRoute}/protected` (例えば `http://my-mobile-backend.mybluemix.net/protected`) を開くことによって、モバイル・バックエンド・アプリケーションの保護エンドポイントに要求を送信します。{{site.data.keyword.mobilefirstbp}} ボイラープレートを使用して作成されたモバイル・バックエンド・アプリケーションの `/protected` エンドポイントは、{{site.data.keyword.amashort}} で保護されています。このエンドポイントは {{site.data.keyword.amashort}} Client SDK により装備されたモバイル・アプリケーションからのみアクセス可能です。その結果、`承認されていない`というメッセージがブラウザーに表示されます。
1. iOS アプリケーションを使用して、同じエンドポイントへ要求を出します。`BMSClient` を初期化し、カスタム `IMFAuthenticationDelegate` を登録した後に、以下のコードを追加します。

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

 ユーザーのログイン後に、このコードを呼び出すと、そのユーザーはログアウトされます。そのユーザーが再度ログインしようとする場合は、サーバーから受信した要求に再度応じる必要があります。

 ログアウト機能へ `callBack` を渡すことは、オプションです。`nil` を渡すこともできます。
