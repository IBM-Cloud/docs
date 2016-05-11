---

copyright:
  years: 2015, 2016

---

# iOS용 {{site.data.keyword.amashort}} 클라이언트 SDK 구성
{: #custom-ios}

사용자 정의 인증을 사용하는 iOS 애플리케이션이 {{site.data.keyword.amashort}}
클라이언트 SDK를 사용하고 애플리케이션을 {{site.data.keyword.Bluemix}}에 연결하도록 구성하십시오. 

**팁:** Swift로 iOS 앱을 개발하는 경우 {{site.data.keyword.amashort}} 클라이언트 Swift SDK 사용을 고려하십시오. 이 페이지의 지시사항은 {{site.data.keyword.amashort}} 클라이언트 Objective-C SDK에 적용됩니다. Swift SDK 사용에 대한 지시사항은 [iOS용 {{site.data.keyword.amashort}} 클라이언트 SDK(Swift SDK) 구성](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-ios-swift-sdk.html)을 참조하십시오.

## 시작하기 전에
{: #before-you-begin}
사용자 정의 ID 제공자를 사용하도록 구성된 {{site.data.keyword.amashort}} 서비스
인스턴스의 보호를 받는 자원이 있어야 합니다. 모바일 앱은 {{site.data.keyword.amashort}}
클라이언트 SDK도 갖추고 있어야 합니다. 자세한 정보는 다음 내용을 참조하십시오. 
 * [{{site.data.keyword.amashort}} 시작하기](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [iOS Objective-C SDK 설정](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios.html)
 * [사용자 정의 ID 제공자 사용](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [사용자 정의 ID 제공자 작성](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [사용자 정의 인증을 사용하도록 {{site.data.keyword.amashort}} 구성](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)



## CocoaPods로 클라이언트 SDK 설치
{: #custom-ios-sdk-cocoapods}
CocoaPods 종속성 관리자를 사용하여 {{site.data.keyword.amashort}}
클라이언트 SDK를 설치하십시오. 

1. 터미널을 열고 iOS 프로젝트의 루트 디렉토리로 이동하십시오. 

1. `Podfile`을 편집하고 다음 행을 추가하십시오. 

	```
	pod 'IMFCore'
	```

1. 명령행에서 `pod install`을 실행하십시오.
CocoaPods가 추가된 종속 항목을 설치합니다. 진행상태 및 추가된 컴포넌트가 표시됩니다. 

**중요**: 이제 CocoaPods에서 생성한 xcworkspace 파일을
사용하여 프로젝트를 열어야 합니다. 일반적으로 이름은 `{your-project-name}.xcworkspace`입니다. 

1. 명령행에서 `open {your-project-name}.xcworkspace`를 실행하여
iOS 프로젝트 작업공간을 여십시오. 



### 클라이언트 SDK 초기화
{: #custom-ios-sdk-initialize}

애플리케이션 라우트(`applicationRoute`) 및 GUID(`applicationGUID`) 매개변수를 전달하여 SDK를 초기화하십시오. 초기화 코드를 삽입하는 일반 위치(필수는 아님)는 애플리케이션 위임자의
`application:didFinishLaunchingWithOptions` 메소드에 있습니다. 

1. 애플리케이션 매개변수 값을 가져오십시오. {{site.data.keyword.Bluemix_notm}} 대시보드에서
앱을 여십시오. **모바일 옵션**을 클릭하여 **라우트**(`applicationRoute`) 및 **앱 GUID**(`applicationGUID`)의 값을 확인하십시오.

1. 클라이언트 SDK를 사용하려는 클래스에서 `IMFCore`
프레임워크를 가져오십시오. 

	Objective-C:
                    


	```Objective-C
	#import <IMFCore/IMFCore.h>
	```

	Swift:


	{{site.data.keyword.amashort}} 클라이언트 SDK는 Objective-C를 사용하여
구현됩니다. SDK를 사용하려면 브리징 헤더를 사용자의 Swift 프로젝트에 추가해야
할 수도 있습니다. 

	* Xcode에서 프로젝트를 마우스 오른쪽 단추로 클릭하고 **새 파일...**을
선택하십시오. 
	* **iOS 소스** 카테고리에서 **헤더 파일**을 선택하십시오. 파일 이름을 `BridgingHeader.h`로 지정하십시오. 
	* 브리징 헤더에 `#import <IMFCore/IMFCore.h>`를 추가하십시오. 
	* Xcode에서 프로젝트를 클릭하고 **빌드 설정** 탭을 선택하십시오. 
	* `Objective-C Bridging Header`를 검색하십시오. 
	* 값을 `BridgingHeader.h` 파일의 위치로 설정하십시오(예:
`$(SRCROOT)/MyApp/BridgingHeader.h`). 
	* 프로젝트를 빌드하여 Xcode에서 브리징 헤더를 선택했는지 확인하십시오. 

1. 클라이언트 SDK를 초기화하십시오. applicationRoute 및 applicationGUID를 **모바일 옵션**에서 얻은 **라우트**(`applicationRoute`) 및 **앱 GUID**(`applicationGUID`)의 값으로 바꾸십시오.

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


## IMFAuthenticationHandler 위임자
{: #custom-ios-sdk-authhandler}


{{site.data.keyword.amashort}} 클라이언트 SDK는 사용자 정의 인증 플로우를
구현할 수 있도록 `IMFAuthenticationHandler` 인터페이스를 제공합니다.
`IMFAuthenticationHandler`는 인증 프로세스의 서로 다른 단계에서
호출되는 세 개의 메소드를 표시합니다. 

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
 						didReceiveAuthenticationChallenge:(NSDictionary*)challenge;
```

이 메소드는 {{site.data.keyword.amashort}} 서비스에서 사용자 정의 인증 확인이
수신된 경우에 호출됩니다. 인수는 다음과 같습니다. 

* `IMFAuthenticationContext` 프로토콜은 개발자가 신임 정보 수집 중 인증 확인 응답
또는 실패를 보고할 수 있도록 {{site.data.keyword.amashort}} 클라이언트 SDK에서
제공합니다(예: 사용자가 취소한 경우). 
* `NSDictionary`는 사용자 정의 ID 제공자가 리턴하는 사용자 정의
인증 확인을 포함합니다. 

`authenticationContext:didReceiveAuthenticationChallenge` 메소드를 호출하면
{{site.data.keyword.amashort}} 클라이언트 SDK가 제어 권한을 개발자에게
위임하고 waiting-for-credentials 모드로 전환합니다. 개발자는 신임 정보를 수집하고
아래에 설명된 `IMFAuthenticationContext` 프로토콜 메소드 중 하나를 사용하여
{{site.data.keyword.amashort}} 클라이언트 SDK에 신임 정보를 보고해야 합니다. 

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
						didReceiveAuthenticationSuccess:(NSDictionary *)userInfo;
```

이 메소드는 인증 성공 후에 호출됩니다. 인수로는 IMFAuthenticationContext 및 인증 성공에 대한
확장 정보가 포함된 선택적 NSDictionary가 있습니다. 

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
						didReceiveAuthenticationFailure:(NSDictionary*)userInfo;
```

이 메소드는 인증 실패 후에 호출됩니다. 인수로는 IMFAuthenticationContext 및 인증 실패에 대한
확장 정보가 포함된 선택적 NSDictionary가 있습니다. 

## IMFAuthenticationContext 프로토콜
{: #custom-ios-sdk-authcontext}


`IMFAuthenticationContext`는 사용자 정의 `IMFAuthenticationHandler`의
`authenticationContext:didReceiveAuthenticationChallenge` 메소드에 대한 인수로 제공됩니다.
개발자는 신임 정보를 수집하고 `IMFAuthenticationContext` 메소드를
사용하여 신임 정보를 {{site.data.keyword.amashort}} 클라이언트 SDK로 리턴하거나
실패를 보고해야 합니다. 다음 메소드 중 하나를 사용하십시오. 

```
-(void) submitAuthenticationChallengeAnswer:(NSDictionary*) answer;

-(void) submitAuthenticationFailure:(NSDictionary*) userInfo;
```

## 사용자 정의 IMFAuthenticationDelegate의 샘플 구현
{: #custom-ios-sdk-sample}


IMFAuthenticationDelegate 샘플은 사용자 정의 ID 제공자 샘플과 함께 작동하도록 디자인되었습니다. 이 샘플은 [Github 저장소](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)에서 다운로드할 수 있습니다.

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

Swift 구현:

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

## 사용자 정의 IMFAuthenticationDelegate 등록

사용자 정의 IMFAuthenticationDelegate를 작성한 후 `IMFClient`에 등록하십시오. 보호된 자원에 대한 요청을 전송하기 전에 애플리케이션에서 다음 코드를
호출하십시오. {{site.data.keyword.amashort}} 대시보드에서 지정한 realmName을
사용하십시오. 

Objective-C 애플리케이션:

```Objective-C
[[IMFClient sharedInstance]
				registerAuthenticationDelegate:[CustomAuthenticationDelegate new]
										forRealm:realmName];
```

Swift 애플리케이션:
```Swift
IMFClient.sharedInstance().registerAuthenticationDelegate(CustomAuthenticationDelegate(),
									forRealm: realmName)
```




## 인증 테스트
{: #custom-ios-testing}
클라이언트 SDK를 초기화하고 사용자 정의 `IMFAuthenticationDelegate`를 등록한 후에는 모바일 백엔드에 대한 요청 작성을 시작할 수 있습니다.

### 시작하기 전에
{: #custom-ios-testing-before}
{{site.data.keyword.mobilefirstbp}} 표준 유형으로 작성된
애플리케이션과 `/protected` 엔드포인트에서 {{site.data.keyword.amashort}}의
보호를 받는 자원이 있어야 합니다. 

1. `{applicationRoute}/protected`(예: `http://my-mobile-backend.mybluemix.net/protected`)를 열어 브라우저에서 모바일 백엔드의 보호 엔드포인트로 요청을
전송하십시오. {{site.data.keyword.mobilefirstbp}} 표준 유형으로 작성된 모바일 백엔드의
`/protected` 엔드포인트는 {{site.data.keyword.amashort}}에서 보호됩니다.
엔드포인트는 {{site.data.keyword.amashort}} 클라이언트 SDK를 갖춘 모바일 애플리케이션에서만
액세스할 수 있습니다. 따라서 `Unauthorized` 메시지는 브라우저에 표시됩니다. 
1. iOS 애플리케이션을 사용하여 동일한 엔드포인트를 요청하십시오.
`BMSClient`를 초기화하고 사용자 정의 `IMFAuthenticationDelegate`를
등록한 후 다음 코드를 추가하십시오. 

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
1. 	요청이 성공하면 Xcode 콘솔에 다음과 같은 출력이 표시됩니다. 

	![이미지](images/ios-custom-login-success.png)
	
	
	
	다음 코드를 추가하여 로그아웃 기능을 추가할 수도 있습니다. 

	Objective C: 

	```Objective-C
	[[IMFAuthorizationManager sharedInstance] logout : callBack]
	```
	Swift:
 

	```Swift
	IMFAuthorizationManager.sharedInstance().logout(callBack)
	```

사용자가 로그인한 후에 이 코드를 호출하면 사용자가 로그아웃됩니다. 
사용자가 다시 로그인을 시도하는 경우, 사용자는 서버에서 수신된 인증 확인에 다시 응답해야 합니다. 로그아웃 기능에 `callBack` 전달은 선택사항입니다. `nil`을 전달할 수도 있습니다. 

