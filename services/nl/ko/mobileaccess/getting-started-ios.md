---

copyright:
  years: 2015, 2016

---

# iOS Objective-C SDK 설정
{: #getting-started-ios}

{{site.data.keyword.amashort}} SDK를 사용하여 iOS 애플리케이션을 계측하십시오. SDK를 초기화하고 보호 및 비보호 자원에 대한 요청을 작성하십시오. 

**팁:** Swift로 iOS 앱을 개발하는 경우, {{site.data.keyword.amashort}} 클라이언트 Swift SDK 사용을 고려하십시오. 세부사항은 [iOS Swift SDK 설정](getting-started-ios-swift-sdk.html)을 참조하십시오.

## 시작하기 전에
{: #before-you-begin}
* {{site.data.keyword.amashort}} 서비스에서 보호하는 모바일 백엔드의 인스턴스가 있어야 합니다. 모바일 백엔드 작성 방법에 대한 자세한 정보는 [시작하기](getting-started.html)를 참조하십시오. 
* 올바르게 Xcode를 설정했는지 확인하십시오. iOS 개발 환경을 설정하는 방법에 대한 자세한 정보는 [Apple 개발자 웹 사이트](https://developer.apple.com/support/xcode/)를 참조하십시오. 


## {{site.data.keyword.amashort}} 클라이언트 SDK 설치
{: #install-mca-sdk-ios}
{{site.data.keyword.amashort}} SDK는 iOS 프로젝트에 대한 종속 항목 관리자인 CocoaPods를 사용하여 분배됩니다. CocoaPods는 저장소에서 아티팩트를 자동으로 다운로드하고 iOS 애플리케이션에서 아티팩트를 사용할 수 있게 합니다. 


### CocoaPods 설치
{: #install-cocoapods}
1. 터미널을 열고 **pod --version** 명령을 실행하십시오. 이미 CocoaPods가 설치되어 있는 경우 버전 번호가 표시됩니다. SDK를 설치하기 위해 다음 섹션으로 건너뛸 수 있습니다. 

1. CocoaPods가 설치되어 있지 않은 경우에는 다음을 실행하십시오.
```
sudo gem install cocoapods```
자세한 정보는 [CocoaPods 웹 사이트](https://cocoapods.org/)를 참조하십시오.

### CocoaPods로 {{site.data.keyword.amashort}} 클라이언트 SDK 설치
{: #install-sdk-cocoapods}

1. 터미널에서 iOS 프로젝트의 루트 디렉토리로 이동하십시오. 

1. 이미 CocoaPods에 대한 작업공간을 초기화하지 않은 경우 `pod init` 명령을 실행하십시오. <br/>
CocoaPods가 `Podfile` 파일을 작성하고 이 파일에서 사용자는 iOS 프로젝트에 대한 종속 항목을 정의합니다. 

1. `Podfile` 파일을 편집하고 필요한 대상에 다음 행을 추가하십시오. 

	```
	pod 'IMFCore'
	```

1. `Podfile` 파일을 저장하고 명령행에서 `pod install`을 실행하십시오. <br/>Cocoapods는 추가된 종속 항목을 설치합니다. 진행상태 및 추가된 컴포넌트를 확인할 수 있습니다. <br/>
**중요**: CocoaPods는 `xcworkspace` 파일을 생성합니다. 앞으로 프로젝트에 대해 작업하려면 이 파일을 열어야 합니다. 

1. iOS 프로젝트 작업공간을 여십시오. CocoaPods에서 생성한 `xcworkspace` 파일을 여십시오. 예: `{your-project-name}.xcworkspace`. `open {your-project-name}.xcworkspace`를 실행하십시오. 

## {{site.data.keyword.amashort}} 클라이언트 SDK 초기화
{: #init-mca-sdk-ios}

{{site.data.keyword.amashort}} 클라이언트 SDK를 사용하려면 **라우트**(`applicationRoute`) 및 **앱 GUID**(`applicationGUID`) 매개변수를 전달하여 SDK를 초기화해야 합니다.


1. {{site.data.keyword.Bluemix_notm}} 대시보드의 기본 페이지에서 사용자 앱을 클릭하십시오. **모바일 옵션**을 클릭하십시오. SDK를 초기화하려면 **라우트** 및 **앱 GUID** 값이 필요합니다.

1. 다음 헤더를 추가하여 {{site.data.keyword.amashort}} 클라이언트 SDK를 사용하려는 클래스에 `IMFCore` 프레임워크를 가져오십시오.

	**Objective-C:**
	 ```Objective-C
	#import <IMFCore/IMFCore.h>
	```

	**Swift:
**

	{{site.data.keyword.amashort}} 클라이언트 SDK는 Objective-C로 구현됩니다. 브리징 헤더를 Swift 프로젝트에 추가해야 할 수 있습니다. 

	1. Xcode에서 마우스 오른쪽 단추로 프로젝트를 클릭하고 **새 파일..**을 선택하십시오. 
	1. **iOS 소스** 카테고리에서 **헤더 파일**을 클릭하십시오. 파일 이름을 `BridgingHeader.h`로 지정하십시오. 
	1. 브리징 헤더에 다음 행을 추가하십시오. `#import <IMFCore/IMFCore.h>`
	1. Xcode에서 프로젝트를 클릭하고 **빌드 설정** 탭을 선택하십시오. 
	1. `Objective-C Bridging Header`를 검색하십시오. 
	1. 값을 `BridgingHeader.h` 파일의 위치로 설정하십시오(예: `$(SRCROOT)/MyApp/BridgingHeader.h`). 
	1. 프로젝트를 빌드하여 Xcode가 브리징 헤더를 선택 중인지 확인하십시오. 실패 메시지가 표시되지 않아야 합니다. 

1. 다음 코드를 사용하여 {{site.data.keyword.amashort}} 클라이언트 SDK를 초기화하십시오. 필수는 아니지만 일반적으로 초기화 코드를 넣는 위치는 애플리케이션 위임자의 `application:didFinishLaunchingWithOptions` 메소드입니다. <br/>
*applicationRoute* 및 *applicationGUID*를 {{site.data.keyword.Bluemix_notm}} 대시보드의 **모바일 옵션** 값으로 대체하십시오.


	**Objective-C:**

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	**Swift:
**

	```Swift
IMFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",backendGUID: "applicationGUID")
	```

## 모바일 백엔드에 대한 요청 작성
{: #request}

{{site.data.keyword.amashort}} 클라이언트 SDK가 초기화되면 모바일 백엔드에 대한 요청 작성을 시작할 수 있습니다. 

1. 브라우저에서 모바일 백엔드의 보호 엔드포인트에 요청을 전송하십시오. URL `{applicationRoute}/protected`를 여십시오. (예: `http://my-mobile-backend.mybluemix.net/protected`)
<br/>MobileFirst Services Starter 표준 유형으로 작성된 모바일 백엔드의 `/protected` 엔드포인트는 {{site.data.keyword.amashort}}를 사용하여 보호됩니다. 이 엔드포인트는 {{site.data.keyword.amashort}} 클라이언트 SDK를 사용하여 계측되는 모바일 애플리케이션에서만 액세스할 수 있기 때문에 브라우저에 `권한 없음` 메시지가 리턴됩니다.

1. iOS 애플리케이션을 사용하여 동일한 엔드포인트에 대해 요청을 작성하십시오. `IMFClient`를 초기화한 후에 다음 코드를 추가하십시오. 

	**Objective-C:**

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

	**Swift:
**

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

1.  요청에 성공하는 경우 Xcode 콘솔에 다음 출력이 표시됩니다. 

	![이미지](images/getting-started-ios-success.png)

## 다음 단계
{: #next-steps}
보호 엔드포인트에 연결된 경우 신임 정보는 필요하지 않습니다. 사용자가 애플리케이션에 로그인하게 하려면 Facebook, Google 또는 사용자 정의 인증을 구성해야 합니다. 
  * [Facebook](facebook-auth-ios.html)
  * [Google](google-auth-ios.html)
  * [사용자 정의 ](custom-auth-ios.html)
