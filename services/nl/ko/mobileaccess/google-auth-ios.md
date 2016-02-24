# iOS 앱에서 Google 인증 사용
{: #google-auth-ios}

## 시작하기 전에
{: #google-auth-ios-before}
* {{site.data.keyword.amashort}}에서 보호하는 자원 및 {{site.data.keyword.amashort}} 클라이언트 SDK로 계측되는 iOS 프로젝트가 있어야 합니다. 자세한 정보는 [{{site.data.keyword.amashort}} 시작하기](getting-started.html) 및 [iOS SDK 설정](getting-started-ios.html)을 참조하십시오.   
* {{site.data.keyword.amashort}} 서버 SDK를 사용하여 백엔드 애플리케이션을 수동으로 보호하십시오. 자세한 정보는 [자원 보호](protecting-resources.html)를 참조하십시오. 


## iOS 플랫폼에 대한 Google 프로젝트 구성
{: #google-auth-ios-project}
ID 제공자로 Google 사용을 시작하려면 Google 클라이언트 ID를 확보하기 위해 Google 개발자 콘솔에서 프로젝트를 작성하십시오. 이 클라이언트 ID는 연결하려고 시도하는 애플리케이션을 Google에서 인지할 수 있게 하는 고유 ID입니다. 이미 Google 프로젝트가 있는 경우 프로젝트 작성에 대해 설명하는 단계를 건너뛰고 신임 정보 추가를 시작할 수 있습니다. 

1. [Google 개발자 콘솔](https://console.developers.google.com)을 여십시오. 

1. 프로젝트를 작성하십시오. **프로젝트 작성**을 클릭하십시오. 

1. 프로젝트를 선택하고 **Google API 사용**을 클릭하십시오. 또한 **API 사용 및 키와 같은 신임 정보 가져오기**를 클릭할 수 있습니다. 

1. API 목록에서 Google+ API를 선택하고 **API 사용**을 클릭하십시오. 

1. **신임 정보 > 신임 정보 추가**를 클릭하고 **OAuth 2.0 클라이언트 ID**를 선택하십시오. 

1. 승인 콘솔에서 제품 이름을 설정하도록 요청받을 수 있습니다. 계속 진행하십시오. 

1. 이 시점에 애플리케이션 유형 선택사항이 표시됩니다. **iOS**를 선택하십시오. 

1. iOS 클라이언트에 대한 의미있는 이름을 지정하십시오. iOS 애플리케이션의 번들 ID를 지정하십시오. iOS 애플리케이션의 번들 ID를 찾으려면, `info.plist` 파일 또는 Xcode 프로젝트 **일반** 탭에서 **번들 ID**를 검색하십시오. 

1. 새 iOS 클라이언트 ID를 기록해 놓으십시오. {{site.data.keyword.Bluemix_notm}}에서 애플리케이션을 설정할 때 값이 필요합니다. 


## Google 인증을 위해 {{site.data.keyword.amashort}} 구성
{: #google-auth-ios-config}

iOS 클라이언트 ID가 있으므로 {{site.data.keyword.Bluemix_notm}} 대시보드에서 Google 인증을 사용하도록 설정할 수 있습니다. 

1. {{site.data.keyword.Bluemix}} 대시보드를 열고 {{site.data.keyword.Bluemix_notm}} 애플리케이션을 클릭하십시오. 

1. **모바일 옵션**을 클릭하고 *applicationRoute* 및 *applicationGUID* 값을 기록해 두십시오. SDK를 초기화하는 데 이 값이 필요합니다. 

1. {{site.data.keyword.amashort}} 타일을 클릭하십시오. 

1. {{site.data.keyword.amashort}} 대시보드로 이동됩니다. 

1. **인증 설정**을 클릭하십시오. 

1. **Google**을 클릭하십시오. 

1. 이전 단계에서 확보한 iOS용 클라이언트 ID를 지정하고 **저장**을 클릭하십시오. 

## iOS용 {{site.data.keyword.amashort}} 클라이언트 SDK 구성
{: #google-auth-ios-sdk}

### Cocoapods를 사용하여 {{site.data.keyword.amashort}} 클라이언트 SDK 설치
{: #google-auth-ios-sdk-cocoapods}

1. iOS 프로젝트로 이동하십시오. 

1. `Podfile`을 편집하고 필요한 대상에 아래 행을 추가하십시오. 

	```
	pod 'IMFGoogleAuthentication'
	```

1. `Podfile`을 저장하고 명령행에서 `pod install`을 실행하십시오. 

1. Cocoapods는 추가된 종속 항목을 설치합니다. 진행상태 및 추가된 컴포넌트를 확인할 수 있습니다. 

	> 이 시점부터 항상 CocoaPods에서 생성한 xcworkspace 파일을 사용하여 프로젝트 열어야 합니다. 일반적으로 이름은 {your-project-name}.xcworkspace입니다.   

1. iOS 프로젝트 작업공간을 열려면 명령행에서 `open {your-project-name}.xcworkspace`를 실행하십시오. 

### Google 인증을 위해 iOS 프로젝트 구성
{: #google-auth-ios-googleauth}

1. `info.plist` 파일을 찾으십시오. 이 파일은 보통 Xcode 프로젝트의 `지원 파일` 폴더에 있습니다. 

1. 아래 두 개의 URL 스킴을 `info.plist` 파일에 추가하여 Google 통합을 구성하십시오. 

	![이미지](images/ios-google-infoplist-settings.png)

	> 첫 번째 URL 스키마는 Google 개발자 콘솔에서 가져온 클라이언트 ID의 역방향입니다. 예를 들어, 클라이언트 ID가 `123123-abcabc.apps.googleusercontent.com`인 경우 URL 스키마는 `com.googleusercontent.apps.123123-abcabc`여야 합니다.

	> 두 번째 URL 스키마는 애플리케이션의 번들 ID입니다. 

1. 또는 `info.plist` 파일을 마우스 오른쪽 단추로 클릭하고 `다른 이름으로 열기` -> `소스 코드`를 선택한 다음 아래 XML을 추가하여 업데이트할 수 있습니다. 

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
	> 위에 설명된 대로 두 가지 URL 스키마를 업데이트하십시오.

	> `info.plist`의 기존 특성을 대체하고 있지 않는지 확인하십시오. 중첩된 특성이 있는 경우 수동으로 병합해야 합니다. 추가 정보는 Google 문서의 [Try Sign-In for iOS](https://developers.google.com/identity/sign-in/ios/start) 섹션을 참조하십시오.

## {{site.data.keyword.amashort}} 클라이언트 SDK 초기화
{: #google-auth-ios-initialize}

{{site.data.keyword.amashort}} 클라이언트 SDK를 사용할 수 있으려면 applicationGUID 및 applicationRoute 매개변수를 전달하여 초기화해야 합니다. 

> 필수는 아니지만 일반적으로 초기화 코드를 넣는 위치는 애플리케이션 위임자의 `application:didFinishLaunchingWithOptions` 메소드입니다.

1. {{site.data.keyword.Bluemix_notm}} 대시보드의 기본 페이지를 열고 이전에 작성된 앱을 클릭하십시오. 이 동작은 모바일 백엔드 앱 대시보드를 엽니다. 

2. 대시보드의 오른쪽 맨 위에 있는 `모바일 옵션`을 클릭하십시오. 애플리케이션 라우트 및 애플리케이션 GUID 값이 표시됩니다. 

1. 아래 헤더를 추가하여 {{site.data.keyword.amashort}} 클라이언트 SDK를 사용하려는 클래스에 필수 프레임워크를 가져오십시오. 

	Objective-C 애플리케이션:

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>
	```

	Swift 애플리케이션:

	{{site.data.keyword.amashort}} 클라이언트 SDK는 Objective-C를 사용하여 구현되므로 이를 사용하려면 Swift 프로젝트에 브리징 헤더를 추가해야 할 수 있습니다. 

	* Xcode에서 마우스 오른쪽 단추로 프로젝트를 클릭하고 `새 파일...`을 선택하십시오. 
	* `iOS 소스` 카테고리에서 `헤더 파일`을 선택하십시오. 
	* `BridgingHeader.h`로 이름을 지정하십시오. 
	* 아래 가져오기를 브리징 헤더에 추가하십시오. 

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>
	```
	* Xcode에서 프로젝트를 클릭하고 `빌드 설정` 탭을 선택하십시오. 
	* `Objective-C 브리징 헤더`를 검색하십시오. 
	* 값을 `BridgingHeader.h` 파일의 위치로 설정하십시오(예: `$(SRCROOT)/MyApp/BridgingHeader.h`). 
	* 프로젝트를 빌드하여 Xcode가 브리징 헤더를 선택 중인지 확인하십시오. 

3. 클라이언트 SDK를 초기화하려면 아래 코드를 사용하십시오. 

	Objective-C 애플리케이션:

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	Swift 애플리케이션:

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",
	 							backendGUID: "applicationGUID")
	```

	> applicationRoute 및 applicationGUID를 모바일 옵션에서 확보한 값으로 대체하십시오. 

1. 아래 코드를 앱 위임자의 `application:didFinishLaunchingWithOptions` 메소드에 추가하여 Google 인증 핸들러를 등록하십시오. IMFClient를 초기화한 후에 바로 수행하는 것이 좋습니다. 

	Objective-C 애플리케이션:

	```Objective-C
	[[IMFGoogleAuthenticationHandler sharedInstance] registerWithDefaultDelegate];
	```

	Swift 애플리케이션:

	```Swift
	IMFGoogleAuthenticationHandler.sharedInstance().registerWithDefaultDelegate()
	```

1. 아래 코드를 앱 위임자에 추가하십시오. 

	Objective-C 애플리케이션:

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

	Swift 애플리케이션:

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
{{site.data.keyword.mobilefirstbp}} 표준 유형을 사용해야 하며 이미 `/protected` 엔드포인트에 {{site.data.keyword.amashort}}가 보호하는 자원이 있어야 합니다. `/protected` 엔드포인트를 설정해야 하는 경우 [자원 보호](protecting-resources.html)를 참조하십시오. 


1. `http://{appRoute}/protected`를 열어 데스크탑 브라우저에서 모바일 백엔드의 보호 엔드포인트로 요청을 전송해 보십시오. 예: `http://my-mobile-backend.mybluemix.net/protected`

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

1. 애플리케이션을 실행하십시오. Google 로그인 화면이 팝업으로 표시됩니다. 

	![이미지](images/ios-google-login.png)

	이 화면은 사용자 디바이스에 Facebook 앱이 설치되어 있지 않거나 현재 Facebook에 로그인되어 있지 않은 경우 약간 다르게 보일 수 있습니다. 

1. **확인**을 클릭하면 인증을 위해 Google 사용자 ID를 사용하도록 {{site.data.keyword.amashort}}에 권한을 부여합니다. 

1. 	요청이 성공적으로 처리되어야 합니다. LogCat에 다음 출력이 표시되어야 합니다. 

	![이미지](images/ios-google-login-success.png)
