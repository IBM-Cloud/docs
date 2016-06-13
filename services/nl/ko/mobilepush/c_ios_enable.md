---

copyright:
 years: 2015, 2016

---

# 푸시 알림을 수신하도록 iOS 애플리케이션 설정
{: #enable-push-ios-notifications}

iOS 애플리케이션이 푸시 알림을 수신하고 사용자 디바이스에 푸시 알림을 전송하도록 설정합니다. 


##CocoaPods 설치
{: #enable-push-ios-notifications-install}

기존 Xcode 프로젝트의 경우 CocoaPods 종속 항목 관리 도구를 사용하여 Bluemix Mobile Services Client SDK를 설정할 수 있습니다. 또는 SDK를 수동으로 설치할 수 있습니다. 

**참고**: Swift Push readme 파일을 보려면 https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master 로 이동하십시오. 



1. Mac 터미널에서 다음 명령을 사용하여 CocoaPods를 설치하십시오.
```
$ sudo gem install cocoapods
```
2. 터미널에서 다음 명령을 입력하여 CocoaPods를 초기화하십시오.
이 명령을 실행할 경우 Xcode 프로젝트가 있는 디렉토리에서 실행해야 합니다. `pod init` 명령에서 파일 제목을 작성합니다.
```
$ pod init
```
3. 생성된 Podfile에서 필요한 SDK 종속 항목을 추가하십시오.
다음 Podfile을 복사하십시오.

   Objective-C

    ```
    source 'https://github.com/CocoaPods/Specs.git'
	Copy the following list as is and remove the dependencies you do not need
	pod 'IMFCore'
	pod 'IMFPush'
	```

   Swift

	```
	source 'https://github.com/CocoaPods/Specs.git'
	// Copy the following list as is and remove the dependencies you do not need.
	use_frameworks!

	target 'MyApp' do
	    platform :ios, '8.0'
	    pod 'BMSCore'
	    pod 'BMSPush'
	end
	```
3. 터미널에서 프로젝트 폴더로 이동한 후, 다음 명령을 사용하여 종속 항목을 설치하십시오.
```
$ pod update
```
해당 명령은 종속 항목을 설치하고 새 Xcode 작업공간을 작성합니다. **참고**: 원래 Xcode 프로젝트 파일 대신, 반드시 항상 새 Xcode 작업공간을 여십시오. 

	```
	$ open App.xcworkspace
	```
작업공간에는 원래 프로젝트 및 종속 항목이 포함된 Pods 프로젝트가 있습니다. Bluemix Mobile Services 소스 폴더를 수정하려는 경우, `Pods/yourImportedSourceFolder`아래의 Pods 프로젝트에서 폴더를 찾을 수 있습니다(예: `Pods/IMFGoogleAuthentication`).

##가져온 프레임워크 및 소스 폴더 사용

코드에서 SDK를 참조하십시오. 


### Objective-C

관련 헤더에 대해 #import 지시문을 작성합니다. 예: 

```
//Objective-C

#import <IMFCore/IMFCore.h>
#import <IMFPush/IMFPush.h>
```

**참고**: CocoaPods 명령 `pod install` 또는 `pod update`를 사용하여 Pods 프로젝트를 업데이트하면 Bluemix Mobile Services 소스 폴더를 대체할 수 있습니다. 원래 파일의 사용자 정의한 버전을 유지하려면, 이러한 명령을 실행하기 전에
해당 버전을 백업해야 합니다. 

###Swift

**사전 전제조건**

- iOS 8.0 이상
- Xcode 7


관련 헤더에 대해 #import 지시문을 작성합니다. 예: 

```
//swift
import BMSCore
import BMSPush
```


##빌드 설정

**Xcode > 빌드 설정 > 빌드 옵션 및 Bitcode 사용 설정**으로 이동하여 **No**로 설정하십시오.

**주의**: iOS 9의 경우, ATS(App Transport Security) 기능을 변경하면 인증 프로세스의 처리 방식에 영향이 미칠 수 있습니다. 다음 블로그 포스팅에서 이러한 변경에 대해 자세히 설명합니다. [iOS 9의 ATS 및 Bitcode](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/) 및 [지금 Bluemix에 iOS 9 앱 연결](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/)




## iOS 앱을 위한 푸시 SDK 초기화
{: #enable-push-ios-notifications-initialize}

초기화 코드를 배치하는 공통 위치는 iOS 애플리케이션에 대한 애플리케이션 위임자입니다. Bluemix 애플리케이션 대시보드의 **모바일 옵션** 링크를 클릭하여 애플리케이션 라우트와 GUID를 확보하십시오. 

###Core SDK 초기화

####Objective-C

```
// Initialize the SDK for Object-C with IBM Bluemix GUID and route
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:"add_your_applicationRoute_here" backendGUID:"add_your_appId_here"];
```

####Swift

```
// Initialize the Core SDK for Swift with IBM Bluemix GUID, route, and region
let myBMSClient = BMSClient.sharedInstance

myBMSClient.initializeWithBluemixAppRoute("BluemixAppRoute", bluemixAppGUID: "APPGUID", bluemixRegion:"Location where your app Hosted")
myBMSClient.defaultRequestTimeout = 10.0 // Timput in seconds
```


###클라이언트 푸시 SDK 초기화

####Objective-C

```
//Initialize client Push SDK for Objective-C
IMFPushClient _pushService = [IMFPushClient sharedInstance];
```

####Swift

```
//Initialize client Push SDK for Swift
let push = BMSPushClient.sharedInstance
```

### 라우트, GUID 및 Bluemix 리젼

**appRoute**

Bluemix에서 생성한 서버 애플리케이션에 지정된 라우트를 지정합니다.

**GUID**

Bluemix에서 생성한 애플리케이션에 지정된 고유 키를 지정합니다. 이 값은 대소문자를 구분합니다. 

**bluemixRegionSuffix**

앱이 호스트된 위치를 지정합니다. ```bluemixRegion``` 매개변수는 사용 중인 Bluemix 배치를 지정합니다. 이 값을 ```BMSClient.REGION`` 정적 특성으로 설정하고 다음 값 중 하나를 사용할 수 있습니다.

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY




## iOS 애플리케이션 및 디바이스 등록
{: #enable-push-ios-notifications-register}


일반적으로 앱이 디바이스에 설치된 후에 발생하는 원격 알림을 수신하려면 APNs에 애플리케이션(앱)을 등록해야 합니다. APNs에 의해 생성된 디바이스 토큰을 애플리케이션에서 수신한 후에는 푸시 알림 서비스에 이를 되돌려 보내야 합니다. 

iOs 애플리케이션 및 디바이스를 등록하려면 다음을 수행하십시오. 

1. 백엔드 애플리케이션 작성
2. 토큰을 푸시 알림에 전달


###백엔드 애플리케이션 작성

Boilerplates 섹션 Bluemix® 카탈로그에서 푸시 서비스를 이 애플리케이션에 자동으로 바인드하는 백엔드 애플리케이션을 작성하십시오. 백엔드 앱을 이미 작성한 경우 앱을 푸시 알림 서비스에 바인드해야 합니다. 

####Objective-C

```
	//For Objective-C

	- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
	if ([[[UIDevice currentDevice] systemVersion] floatValue] >= 8.0){
     [[UIApplication sharedApplication] registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeSound | UIUserNotificationTypeAlert | UIUserNotificationTypeBadge) categories:categories]];
	    [[UIApplication sharedApplication] registerForRemoteNotifications];
	    }
	    else{
	    [[UIApplication sharedApplication] registerForRemoteNotificationTypes:
	    (UIUserNotificationTypeBadge | UIUserNotificationTypeSound | UIUserNotificationTypeAlert)];
	    }
	    return YES;
	}
```

####Swift

```
	//For Swift
	func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
  let notificationTypes: UIUserNotificationType = UIUserNotificationType.Badge | UIUserNotificationType.Alert | UIUserNotificationType.Sound
		let notificationSettings: UIUserNotificationSettings = UIUserNotificationSettings(forTypes: notificationTypes, categories: categories)
		application.registerUserNotificationSettings(notificationSettings)
		application.registerForRemoteNotifications()
	}
```

###토큰을 푸시 알림에 전달

APNs로부터 토큰이 수신되면 ```registerDevice:withDeviceToken``` 메소드의 일부로 푸시 알림에 토큰을 전달하십시오. 

####Objective-C

```
//For Objective-C
-( void) application:( UIApplication *)application didRegisterForRemoteNotificationsWithDeviceToken:( NSData *)deviceToken{

   IMFClient *client = [IMFClient sharedInstance];


 [client initializeWithBackendRoute:@"your-backend-route-here" backendGUID:@"Your-backend-GUID-here"];



 // get Push instance
IMFPushClient* push = [IMFPushClient sharedInstance];
[push registerDeviceToken:deviceToken completionHandler:^(IMFResponse *response,  NSError *error) {
   if(error){
     [ self  updateMessage:error .description];
  }  else {
    [ self updateMessage:response .responseJson .description];
}
}];
```

####Swift

APNS로부터 토큰이 수신되면 ```didRegisterForRemoteNotificationsWithDeviceToken``` 메소드의 일부로 푸시 알림에 토큰을 전달하십시오. 

```
func application (application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData){
   let push =  BMSPushClient.sharedInstance
   push.registerDeviceToken(deviceToken) { (response, statusCode, error) -> Void in
        if error.isEmpty {
            print( "Response during device registration : \(response)")
            print( "status code during device registration : \(statusCode)")
        }
        else{
            print( "Error during device registration \(error) ")
            print( "Error during device registration \n  - status code: \(statusCode) \n Error :\(error) \n")
        }
    }

}
```



## iOS 디바이스에서 푸시 알림 수신
{: #enable-push-ios-notifications-receiving}

iOS 디바이스에서 푸시 알림을 수신합니다. 

###Objective-C
iOS 디바이스에서 푸시 알림을 수신하려면 애플리케이션의 위임자에 다음 Objective-C 메소드를 추가하십시오.

```
// For Objective-C
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo {
//userInfo dictionary will contain data sent from server.
}
```

###Swift
iOS 디바이스에서 푸시 알림을 수신하려면 애플리케이션의 위임자에 다음 Swift 메소드를 추가하십시오.

```
 // For Swift
func application(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: (UIBackgroundFetchResult) -> Void) {
       //UserInfo dictionary will contain data sent from the server
   }


```



## 기본 푸시 알림 전송
{: #send}

애플리케이션이 개발된 후에는 (태그, 배지, 추가 페이로드 또는 사운드 파일을 사용하지 않아도) 기본 푸시 알림을 전송할 수 있습니다. 


기본 푸시 알림을 보내십시오. 

1. **청취자 선택**에서 다음 청취자 중 하나를 선택하십시오. **모든 디바이스** 또는 플랫폼 기준으로 **iOS 디바이스만** 또는 **Anroid 디바이스만**. 

	**참고**: **모든 디바이스** 옵션을 선택하는 경우 푸시 알림에 구독된 모든 디바이스가 알림을 수신합니다. 

	![알림 화면](images/tag_notification.jpg)

2. **알림 작성**에서 메시지를 입력하고 **보내기**를 클릭하십시오.
3. 디바이스가 알림을 수신했는지 확인하십시오. 

	다음 스크린샷은 Android와 iOS 디바이스의 포그라운드에서
푸시 알림을 처리하는 경보 상자를 보여줍니다. 

	![Android의 포그라운드 푸시 알림](images/Android_Screenshot.jpg)

	![iOS의 포그라운드 푸시 알림](images/iOS_Screenshot.jpg)

	다음 스크린샷은 Android의 백그라운드에 있는 푸시 알림을 보여줍니다.
	![Android의 백그라운드 푸시 알림](images/background.jpg)




## 다음 단계
{: #next_steps_tags}

정상적으로 기본 알림을 설정한 후 태그 기반 알림 및 고급 옵션을 구성할 수 있습니다. 

다음의 푸시 알림 서비스 기능을 사용자의 앱에 추가하십시오.
태그 기반 알림을 사용하려면 [태그 기반 알림](c_tag_basednotifications.html)을 참조하십시오.
고급 알림 옵션을 사용하려면 [고급 푸시 알림](t_advance_notifications.html)을 참조하십시오. 
