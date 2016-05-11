---

copyright:
  years: 2015, 2016

---

# 配置 {{site.data.keyword.amashort}} Client SDK for iOS
{: #custom-ios}

配置 iOS 應用程式，這個應用程式利用自訂鑑別來使用 {{site.data.keyword.amashort}} Client SDK，並將您的應用程式連接至 {{site.data.keyword.Bluemix}}。

**提示：**如果您是以 Swift 開發 iOS 應用程式，請考量使用 {{site.data.keyword.amashort}} Client Swift SDK。此頁面上的指示適用於 {{site.data.keyword.amashort}} Client Objective-C SDK。如需使用 Swift SDK 的相關指示，請參閱[配置 {{site.data.keyword.amashort}} Client SDK for iOS (Swift SDK)](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-ios-swift-sdk.html)

## 開始之前
{: #before-you-begin}
您必須具有配置成使用自訂身分提供者的 {{site.data.keyword.amashort}} 服務實例所保護的資源。您的行動式應用程式也必須使用 {{site.data.keyword.amashort}} Client SDK 進行檢測。如需相關資訊，請參閱下列資訊：
 * [開始使用 {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [設定 iOS Objective-C SDK](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios.html)
 * [使用自訂身分提供者](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [建立自訂身分提供者](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [配置 {{site.data.keyword.amashort}} 進行自訂鑑別](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)



## 使用 CocoaPods 安裝 Client SDK
{: #custom-ios-sdk-cocoapods}
使用 CocoaPods 相依關係管理程式來安裝 {{site.data.keyword.amashort}} Client SDK。

1. 開啟「終端機」，並導覽至您 iOS 專案的根目錄。

1. 編輯 `Podfile`，並新增下行。

	```
	pod 'IMFCore'
	```

1. 從指令行執行 `pod install`。
CocoaPods 將安裝新增的相依關係。即會顯示進度及新增的元件。

**重要事項**：您現在必須使用 CocoaPods 所產生的 xcworkspace 檔案來開啟專案。名稱通常為 `{your-project-name}.xcworkspace`。

1. 從指令行執行 `open {your-project-name}.xcworkspace`，以開啟您的 iOS 專案工作區。



### 起始設定 Client SDK
{: #custom-ios-sdk-initialize}

透過傳遞應用程式路徑 (`applicationRoute`) 及 GUID (`applicationGUID`) 參數來起始設定 SDK。放置起始設定碼的一般（但非強制）位置是在應用程式委派的 `application:didFinishLaunchingWithOptions` 方法。

1. 取得應用程式參數值。在 {{site.data.keyword.Bluemix_notm}} 儀表板中開啟應用程式。按一下**行動式選項**，以查看**路徑** (`applicationRoute`) 及 **應用程式 GUID**(`applicationGUID`) 值。

1. 在您要使用 Client SDK 的類別中，匯入 `IMFCore` 架構。

	Objective-C：

	```Objective-C
	#import <IMFCore/IMFCore.h>
	```

	Swift：

	{{site.data.keyword.amashort}} Client SDK 是使用 Objective-C 進行實作。您可能需要將橋接標頭新增至 Swift 專案，才能使用 SDK。

	* 在 Xcode 中的專案上按一下滑鼠右鍵，然後選取**新建檔案...**。
	* 在 **iOS 來源**種類中，挑選**標頭檔**。將檔案命名為 `BridgingHeader.h`。
	* 將 `#import <IMFCore/IMFCore.h>` 新增至橋接標頭。
	* 在 Xcode 中按一下您的專案，然後選取**建置設定**標籤。
	* 搜尋 `Objective-C Bridging Header`。
	* 將值設為 `BridgingHeader.h` 檔案的位置（例如：`$(SRCROOT)/MyApp/BridgingHeader.h`）。
	* 建置專案，以驗證 Xcode 取得橋接標頭。

1. 起始設定 Client SDK。將 applicationRoute 及 applicationGUID 取代為您取自**行動式選項**的**路徑** (`applicationRoute`) 及**應用程式 GUID** (`applicationGUID`) 值。

	Objective-C：

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	Swift：

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",
	 							backendGUID: "applicationGUID")
	```


## IMFAuthenticationHandler 委派
{: #custom-ios-sdk-authhandler}


{{site.data.keyword.amashort}} Client SDK 提供 `IMFAuthenticationHandler` 介面，以實作自訂鑑別流程。`IMFAuthenticationHandler` 公開在鑑別處理程序的不同階段所呼叫的三種方法。

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
 						didReceiveAuthenticationChallenge:(NSDictionary*)challenge;
```

從「{{site.data.keyword.amashort}} 服務」接收自訂鑑別盤查時，會呼叫此方法。引數包括：

* `IMFAuthenticationContext` 通訊協定是由 {{site.data.keyword.amashort}} Client SDK 所提供，讓開發人員可以在認證收集期間回報鑑別盤查回答或失敗（例如：使用者已取消）。
* `NSDictionary` 包含「自訂身分提供者」所傳回的自訂鑑別盤查。

透過呼叫 `authenticationContext:didReceiveAuthenticationChallenge` 方法，{{site.data.keyword.amashort}} Client SDK 會將控制權委派給開發人員，並讓它自行進入等待認證模式。開發人員負責收集認證，並使用其中一種 `IMFAuthenticationContext` 通訊協定方法將它們回報給 {{site.data.keyword.amashort}} Client SDK（將在下面說明）。

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
						didReceiveAuthenticationSuccess:(NSDictionary *)userInfo;
```

在成功鑑別之後，會呼叫此方法。引數包括 IMFAuthenticationContext 以及內含鑑別成功延伸資訊的選用 NSDictionary。

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
						didReceiveAuthenticationFailure:(NSDictionary*)userInfo;
```

在鑑別失敗之後，會呼叫此方法。引數包括 IMFAuthenticationContext 以及內含鑑別失敗延伸資訊的選用 NSDictionary。

## IMFAuthenticationContext 通訊協定
{: #custom-ios-sdk-authcontext}


`IMFAuthenticationContext` 提供作為自訂 `IMFAuthenticationHandler` 的 `authenticationContext:didReceiveAuthenticationChallenge` 方法的引數。開發人員負責收集認證，然後使用 `IMFAuthenticationContext` 方法將認證傳回給 {{site.data.keyword.amashort}} Client SDK 或報告失敗。請使用下列其中一種方法。

```
-(void) submitAuthenticationChallengeAnswer:(NSDictionary*) answer;

-(void) submitAuthenticationFailure:(NSDictionary*) userInfo;
```

## 自訂 IMFAuthenticationDelegate 範例實作
{: #custom-ios-sdk-sample}


IMFAuthenticationDelegate 範例設計成使用自訂身分提供者範例。您可以從 [Github 儲存庫](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)下載範例。

Objective-C：

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

Swift 實作：

```Swift
import Foundation

class CustomAuthenticationDelegate : NSObject, IMFAuthenticationDelegate{

	func authenticationContext(context: IMFAuthenticationContext!,
					didReceiveAuthenticationChallenge challenge: [NSObject : AnyObject]!) {

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

## 登錄自訂 IMFAuthenticationDelegate

建立自訂 IMFAuthenticationDelegate 之後，會向 `IMFClient` 登錄。先在應用程式中呼叫下列程式碼，再將任何要求傳送至受保護資源。使用 {{site.data.keyword.amashort}} 儀表板中所指定的 realmName。

Objective-C 應用程式：

```Objective-C
[[IMFClient sharedInstance]
				registerAuthenticationDelegate:[CustomAuthenticationDelegate new]
										forRealm:realmName];
```

Swift 應用程式：
```Swift
IMFClient.sharedInstance().registerAuthenticationDelegate(CustomAuthenticationDelegate(),
									forRealm: realmName)
```




## 測試鑑別
{: #custom-ios-testing}
起始設定 Client SDK 並登錄自訂 `IMFAuthenticationDelegate` 之後，即可開始對行動式後端提出要求。

### 開始之前
{: #custom-ios-testing-before}
您必須具有使用 {{site.data.keyword.mobilefirstbp}} 樣板所建立的應用程式，並在 `/protected` 端點具有 {{site.data.keyword.amashort}} 所保護的資源。

1. 開啟 `{applicationRoute}/protected`（例如 `http://my-mobile-backend.mybluemix.net/protected`），以在瀏覽器中將要求傳送給行動式後端的受保護端點。使用 {{site.data.keyword.mobilefirstbp}} 樣板所建立之行動式後端的 `/protected` 端點是透過 {{site.data.keyword.amashort}} 進行保護。只有使用 {{site.data.keyword.amashort}} Client SDK 所檢測的行動式應用程式才能存取這個端點。因此，會在瀏覽器中顯示 `Unauthorized` 訊息。
1. 使用 iOS 應用程式以對相同的端點提出要求。起始設定 `BMSClient` 並登錄自訂 `IMFAuthenticationDelegate` 之後，請新增下列程式碼：

	Objective-C：

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

	Swift：

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
1. 	當要求成功時，您會在 Xcode 主控台中看到下列輸出：

	![影像](images/ios-custom-login-success.png)
	
	
	
	您也可以新增下列程式碼，來新增登出功能：

	Objective C: 

	```Objective-C
	[[IMFAuthorizationManager sharedInstance] logout : callBack]
	```
	Swift： 

	```Swift
	IMFAuthorizationManager.sharedInstance().logout(callBack)
	```

如果您在使用者登入之後呼叫此程式碼，則會將使用者登出。使用者嘗試再次登入時，必須再次回答接收自伺服器的盤查。
將 `callBack` 傳遞給 logout 函數是選用的。您也可以傳遞 `nil`。

