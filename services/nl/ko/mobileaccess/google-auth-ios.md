---

copyright:
  years: 2015, 2016

---

# iOS 앱에서 Google 인증 사용
{: #google-auth-ios}

**팁:** Swift로 iOS 앱을 개발하는 경우 {{site.data.keyword.amashort}} 클라이언트 Swift SDK 사용을 고려하십시오. 이 페이지의 지시사항은 {{site.data.keyword.amashort}} 클라이언트 Objective-C SDK에 적용됩니다. Swift SDK 사용에 대한 지시사항은 [iOS 앱(Swift SDK)에서 Google 인증 사용](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html)을 참조하십시오.

## 시작하기 전에
{: #google-auth-ios-before}
* {{site.data.keyword.amashort}}에서 보호하는 자원 및 {{site.data.keyword.amashort}} 클라이언트 SDK로 계측되는 iOS 프로젝트가 있어야 합니다. 자세한 정보는 [{{site.data.keyword.amashort}} 시작하기](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) 및 [iOS Objective-C SDK 설정](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios.html)을 참조하십시오.  
* {{site.data.keyword.amashort}} 서버 SDK를 사용하여 백엔드 애플리케이션을 수동으로 보호하십시오. 자세한 정보는 [자원 보호](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)를 참조하십시오. 


## iOS 플랫폼에 대한 Google 프로젝트 구성
{: #google-auth-ios-project}
ID 제공자로 Google 사용을 시작하려면 Google 클라이언트 ID를 확보하기 위해 Google 개발자 콘솔에서 프로젝트를 작성하십시오. 이 클라이언트 ID는 연결하려고 시도하는 애플리케이션을 Google에서 인지할 수 있게 하는 고유 ID입니다. 이미 Google 프로젝트가 있는 경우 프로젝트 작성에 대해 설명하는 단계를 건너뛰고 신임 정보 추가를 시작할 수 있습니다. 



1. [Google 개발자 콘솔](https://console.developers.google.com)에서 프로젝트를 작성하십시오.
이미 프로젝트가 있는 경우 프로젝트 작성에 대해 설명하는 단계를 건너뛰고 신임 정보 추가를 시작할 수 있습니다. 
   1.    새 프로젝트 메뉴를 여십시오.  
         
         ![이미지](images/FindProject.jpg)

   2.    **프로젝트 작성**을 클릭하십시오. 
   
         ![이미지](images/CreateAProject.jpg)


1. **소셜 API** 목록에서 **Google+ API**를 선택하십시오. 

     ![이미지](images/chooseGooglePlus.jpg)

1. 다음 화면에서 **사용**을 클릭하십시오. 

1. **동의 화면** 탭을 선택하고 사용자에게 표시된 제품 이름을 제공하십시오. 기타 값은 선택사항입니다. **저장**을 클릭하십시오.

    ![이미지](images/consentScreen.png)
    
1. **신임 정보** 목록에서 OAuth 클라이언트 ID를 선택하십시오. 

     ![이미지](images/chooseCredentials.png)
     


1. 이 시점에 애플리케이션 유형 선택사항이 표시됩니다. **iOS**를 선택하십시오. 

1. iOS 클라이언트에 대한 의미있는 이름을 지정하십시오. iOS 애플리케이션의 번들 ID를 지정하십시오. iOS 애플리케이션의 번들 ID를 찾으려면 `info.plist` 파일 또는 Xcode 프로젝트 **일반** 탭에서 **번들 ID**를 검색하십시오.

1. 새 iOS 클라이언트 ID를 기록해 놓으십시오. {{site.data.keyword.Bluemix}}에서 애플리케이션을 설정할 때 값이 필요합니다. 


## Google 인증을 위해 {{site.data.keyword.amashort}} 구성
{: #google-auth-ios-config}

iOS 클라이언트 ID가 있으므로 {{site.data.keyword.Bluemix_notm}} 대시보드에서 Google 인증을 사용하도록 설정할 수 있습니다. 

1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 앱을 여십시오. 

1. **모바일 옵션**을 클릭하고 **라우트**(`applicationRoute`) 및 **앱 GUID**(`applicationGUID`)를 기록해 두십시오. SDK를 초기화하는 경우 이 값이 필요합니다. 

1. {{site.data.keyword.amashort}} 타일을 클릭하십시오. {{site.data.keyword.amashort}} 대시보드가 로드됩니다. 

1. **Google** 타일을 클릭하십시오.

1. **iOS용 애플리케이션 ID**에서 Android용 iOS 클라이언트 ID를 지정하고 **저장**을 클릭하십시오.

	참고: Google 클라이언트 id와 함께, 클라이언트 구성에 대해 반대 값도 필요합니다(아래 참조). 
두 값에 모두 액세스하려면 연필 아이콘을 사용하여 예제 plist를 다운로드하십시오.
![info.plist 파일 다운로드](images/download_plist.png)

## iOS용 {{site.data.keyword.amashort}} 클라이언트 SDK 구성
{: #google-auth-ios-sdk}

### CocoaPods를 사용하여 {{site.data.keyword.amashort}} 클라이언트 SDK 설치
{: #google-auth-ios-sdk-cocoapods}

1. iOS 프로젝트로 이동하십시오.

1. `Podfile`을 편집하여 다음 행을 추가하십시오.

	```
	pod 'IMFGoogleAuthentication'
	```

1. `Podfile`을 저장하고 명령행에서 `pod install`을 실행하십시오. CocoaPods가 종속 항목을 설치합니다. 진행상태 및 추가된 컴포넌트를 확인할 수 있습니다. 

  **중요**: 이제 CocoaPods에서 생성한 `xcworkspace` 파일을 사용하여 프로젝트를 열어야 합니다. 일반적으로 이름은 `{your-project-name}.xcworkspace`입니다.   

1. 명령행에서 `open {your-project-name}.xcworkspace`를 실행하여 iOS 프로젝트 작업공간을 여십시오.

### Google 인증을 위해 iOS 프로젝트 구성
{: #google-auth-ios-googleauth}
`info.plist` 파일을 업데이트하여 Google 통합을 구성하십시오. `info.plist` 파일은 보통 Xcode 프로젝트의 `지원 파일` 폴더에 있습니다. 
특성 목록 편집기에서 또는 문서 편집기를 사용하여 해당 파일을 편집할 수 있습니다. 

* 다음 URL 스키마를 `info.plist` 파일에 추가하여 Google 통합을 구성하십시오.
	![info.plist 파일](images/ios-google-infoplist-settings.png)

	첫 번째 URL 스키마는 Google 개발자 콘솔에서 가져온 클라이언트 ID의 역방향 버전입니다. 예를 들어, 클라이언트 ID가 `123123-abcabc.apps.googleusercontent.com`이면 URL 스키마는 `com.googleusercontent.apps.123123-abcabc`입니다. 

	두 번째 URL 스키마는 애플리케이션의 번들 ID입니다.

* 문서 편집기를 사용하십시오. `info.plist`를 마우스 오른쪽 단추로 클릭하고 **다른 이름으로 열기 > 소스 코드**를 선택하십시오. 다음 XML을 파일에 추가하십시오.

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
	두 URL 스키마를 모두 업데이트하십시오.

	**중요**: `info.plist` 파일의 기존 특성을 대체하지 마십시오. 중첩된 특성이 있는 경우 특성을 수동으로 병합해야 합니다. 자세한 정보는 [Try Sign-In for iOS](https://developers.google.com/identity/sign-in/ios/start)를 참조하십시오.

## {{site.data.keyword.amashort}} 클라이언트 SDK 초기화
{: #google-auth-ios-initialize}

{{site.data.keyword.amashort}} 클라이언트 SDK를 사용하려면 applicationGUID 및 applicationRoute 매개변수를 전달하여 해당 클라이언트 SDK를 초기화하십시오.

필수는 아니지만 일반적으로 초기화 코드를 넣는 위치는 애플리케이션 위임자의 `application:didFinishLaunchingWithOptions` 메소드입니다. 

1. applicationGUID 및 applicationRoute 값을 가져오십시오. {{site.data.keyword.Bluemix_notm}} 대시보드에서 사용자 앱을 클릭하십시오. **모바일 옵션**을 클릭하십시오. 애플리케이션 라우트 및
애플리케이션 GUID 값이 표시됩니다.

1. {{site.data.keyword.amashort}} 클라이언트 SDK를 사용하려는 클래스에 필수 프레임워크를 가져오십시오. 다음 헤더를 추가하십시오.

	Objective-C:
                    


	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>
	```

	Swift:


	{{site.data.keyword.amashort}} 클라이언트 SDK는 Objective-C로 구현됩니다. SDK를 사용하려면 브리징 헤더를 사용자의 Swift 프로젝트에 추가해야
할 수도 있습니다. 

	1. Xcode에서 마우스 오른쪽 단추로 프로젝트를 클릭하고 **새 파일...**을 선택하십시오. 
	2. **iOS 소스** 카테고리에서 **헤더 파일**을 선택하십시오. 
	3. `BridgingHeader.h`로 이름을 지정하십시오. 
	4. 다음 가져오기를 브리징 헤더에 추가하십시오.

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>
	```
	5. Xcode에서 프로젝트를 클릭하고 **빌드 설정** 탭을 선택하십시오.
	6. `Objective-C Bridging Header`를 검색하십시오. 
	7. 값을 `BridgingHeader.h` 파일의 위치로 설정하십시오(예: `$(SRCROOT)/MyApp/BridgingHeader.h`).
	8. 프로젝트를 빌드하여 Xcode가 브리징 헤더를 선택 중인지 확인하십시오. 

3. 다음 코드를 사용하여 클라이언트 SDK를 초기화하십시오. *applicationRoute* 및 *applicationGUID*를 **모바일 옵션**에서 얻은 **라우트** 및 **앱 GUID** 값으로 바꾸십시오.

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



1. 앱 위임자의 `application:didFinishLaunchingWithOptions` 메소드에 다음 코드를 추가하여 Google 인증 핸들러를 등록하십시오. 
IMFClient를 초기화한 이후 즉시 이 코드를 추가하십시오. 

	Objective-C:
                    


	```Objective-C
	[[IMFGoogleAuthenticationHandler sharedInstance] registerWithDefaultDelegate];
	```

	Swift:


	```Swift
	IMFGoogleAuthenticationHandler.sharedInstance().registerWithDefaultDelegate()
	```

1. 다음 코드를 앱 위임자에 추가하십시오. 

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

## 인증 테스트
{: #google-auth-ios-testing}
클라이언트 SDK가 초기화되면 모바일 백엔드에 대한 요청 작성을 시작할 수 있습니다. 

### 시작하기 전에
{: #google-auth-ios-testing-before}
{{site.data.keyword.mobilefirstbp}} 표준 유형을 사용해야 하며 이미 `/protected` 엔드포인트에 {{site.data.keyword.amashort}}가 보호하는 자원이 있어야 합니다. `/protected` 엔드포인트를 설정해야 하는 경우
[자원 보호](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html)를 참조하십시오. 


1. `{applicationRoute}/protected`(예: `http://my-mobile-backend.mybluemix.net/protected`)를 열어 데스크탑 브라우저에서 모바일 백엔드의 보호 엔드포인트로 요청을 전송하십시오.

1. MobileFirst 서비스 표준 유형으로 작성된 모바일 백엔드의 `/protected` 엔드포인트는 {{site.data.keyword.amashort}}로 보호되므로 {{site.data.keyword.amashort}} 클라이언트 SDK를 사용하여 계측된 모바일 애플리케이션만 액세스할 수 있습니다. 결과적으로 데스크탑 브라우저에 `권한 없음`이 표시됩니다. 

1. iOS 애플리케이션을 사용하여 동일한 엔드포인트에 대해 요청을 작성하십시오. 

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

1. 애플리케이션을 실행하십시오. Google 로그인 화면이 팝업으로 표시됩니다. 

	![이미지](images/ios-google-login.png)

	이 화면은 사용자 디바이스에 Facebook 앱이 설치되어 있지 않거나 현재 Facebook에 로그인되어 있지 않은 경우 약간 다르게 보일 수 있습니다. 

1. **확인**을 클릭하면 인증을 위해 Google 사용자 ID를 사용하도록 {{site.data.keyword.amashort}}에 권한을 부여합니다. 

1. 	요청이 성공적으로 처리되어야 합니다. LogCat에 다음 출력이 표시되어야 합니다. 

	![이미지](images/ios-google-login-success.png)
	
	
	다음 코드를 추가하여 로그아웃 기능을 추가할 수도 있습니다. 
	
	Objective C:
	
	```Objective-C
	[[IMFGoogleAuthenticationHandler sharedInstance] logout : callBack]
	```

	Swift:


	```Swift
	IMFGoogleAuthenticationHandler.sharedInstance().logout(callBack)
	```


	Google에서 사용자가 로그인한 이후 이 코드를 호출하며 사용자가 다시 로그인을 시도하는 경우,
사용자에게는 인증 용도로 Google을 사용하도록 Mobile Client Access 권한 부여 프롬프트가 제시됩니다. 
이 시점에, 사용자는 화면 상단 오른쪽 모서리에서 사용자 이름을 클릭하여 다른 사용자를 선택하고 이를 사용하여 로그인할 수 있습니다. 

	로그아웃 기능에 `callBack` 전달은 선택사항입니다. `nil`을 전달할 수도 있습니다. 
