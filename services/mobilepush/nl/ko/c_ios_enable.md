---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

#{{site.data.keyword.mobilepushshort}}를 전송하도록 iOS 애플리케이션 설정
{: #enable-push-ios-notifications}
마지막 업데이트 날짜: 2017년 1월 16일
{: .last-updated}

iOS 애플리케이션이 {{site.data.keyword.mobilepushshort}}를 사용자 디바이스에 전송하도록 설정할 수 있습니다.


##CocoaPods 설치
{: #enable-push-ios-notifications-install}

기존 Xcode 프로젝트의 경우 CocoaPods 종속 항목 관리 도구를 사용하여 Bluemix Mobile Services Client SDK를 설정할 수 있습니다. 또는 SDK를 수동으로 설치할 수 있습니다. 

Swift 푸시 readme 파일을 보려면 [Readme ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master "외부 링크 아이콘"){: new_window}으로 이동하십시오.



1. Mac 터미널에서 다음 명령을 사용하여 CocoaPods를 설치하십시오.
```$ sudo gem install cocoapods
```
	{: codeblock}
2. 터미널에 `pod init` 명령을 입력하여 CocoaPods를 초기화하십시오. Xcode 프로젝트가 있는 디렉토리에서 명령을 실행하십시오. `pod init` 명령에서 Podfile을 작성합니다.  
3. 생성된 Podfile에 필요한 SDK 종속 항목을 추가하십시오. 다음 Podfile을 복사하십시오.
   
	```
	source 'https://github.com/CocoaPods/Specs.git'
	// Copy the following list as is and remove the dependencies you do not need.
	use_frameworks!
	target 'MyApp' do
	platform :ios, '8.0'
	pod 'BMSCore'
	pod 'BMSPush'
	pod 'BMSAnalyticsAPI'
	end
	```
		{: codeblock}

3. 터미널에서 프로젝트 폴더로 이동한 후 `pod update` 명령을 사용하여 종속 항목을 설치하십시오. 

이 명령은 종속 항목을 설치하고 새 Xcode 작업공간을 작성합니다.   
**참고**: 원래 Xcode 프로젝트 파일 대신, 반드시 항상 새 Xcode 작업공간을 여십시오. 
```
$ open App.xcworkspace
	```
	{: codeblock}

작업공간에는 원래 프로젝트 및 종속 항목이 포함된 Pods 프로젝트가 있습니다. Bluemix Mobile Services 소스 폴더를 수정하려는 경우 Pods 프로젝트의 `Pods/yourImportedSourceFolder`에서 이 폴더를 찾을 수 있습니다(예: `Pods/BMSPush`).

##Carthage를 사용하여 프레임워크 추가
{: #carthage}

[Carthage ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos "외부 링크 아이콘"){: new_window}을 사용하여 프로젝트에 프레임워크를 추가하십시오. Xcode8의 Carthage는 지원되지 않습니다. 

1. `BMSPush` 프레임워크를 Cartfile에 추가하십시오. 
```
github "github "ibm-bluemix-mobile-services/bms-clientsdk-swift-push" ~> 1.0"
```
	{: codeblock}
2. `carthage update` 명령을 실행하십시오. 빌드가 완료되면 `BMSPush.framework`, `BMSCore.framework`, `BMSAnalyticsAPI.framework`를 Xcode 프로젝트로 끌어오십시오. 
3. [Carthage ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos "외부 링크 아이콘"){: new_window} 사이트의 지시사항을 따라 통합을 완료하십시오.

##iOS SDK 설정
{: ios-sdk}

iOS SDK를 설치하고 다음 코드를 애플리케이션의 **AppDelegate.swift** 파일에 추가하십시오. 이 코드도 APNs에 등록됩니다.  
```
func application(_ application: UIApplication,
didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool
  {
  BMSPushClient.sharedInstance.initializeWithAppGUID(appGUID: "APP-GUID-HERE", clientSecret:"CLIENT-SECRET-HERE")
  }
```
    {: codeblock}

##가져온 프레임워크 및 소스 폴더 사용
{: using-imported-frameworks}

코드에서 SDK를 참조하십시오. 다음 전제조건이 충족되는지 확인하십시오.
	- iOS 8.0 이상	
	- Xcode 7

관련 헤더에 대해 `#import` 지시문을 작성합니다. 예: 
	```
	//swift
	import BMSCore
	import BMSPush
	```
		{: codeblock}

Swift 푸시 readme 파일을 읽으려면 [Readme ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master "외부 링크 아이콘"){: new_window}을 참조하십시오.

**참고**: CocoaPods 명령 `pod install` 또는 `pod update`를 사용하여 Pods 프로젝트를 업데이트하면 Bluemix Mobile Services 소스 폴더가 대체될 수 있습니다. 원래 파일의 사용자 정의한 버전을 유지하려면, 이러한 명령을 실행하기 전에 해당 버전을 백업해야 합니다. 


##빌드 설정
{: build-settings}

**Xcode > 빌드 설정 > 빌드 옵션 및 Bitcode 사용 설정**으로 이동하여 **No**로 설정하십시오.

**주의**: iOS 9의 경우, ATS(App Transport Security) 기능을 변경하면 인증 프로세스의 처리 방식에 영향이 미칠 수 있습니다. 다음 블로그 게시물은 변경사항에 대한 자세한 정보를 설명합니다. [ATS and Bitcode in iOS 9 ![외부 링크 아이콘](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/){: new_window} 및 [Connect your iOS 9 app to Bluemix today ![외부 링크 아이콘](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/){: new_window}.

## iOS 앱을 위한 푸시 SDK 초기화
{: #enable-push-ios-notifications-initialize}

초기화 코드를 배치하는 공통 위치는 iOS 애플리케이션에 대한 애플리케이션 위임자입니다. 푸시 대시보드의 **모바일 옵션** 링크를 클릭하여 애플리케이션 라우트와 GUID를 가져오십시오. 

###Core SDK 초기화
{: Initializing-the-core-sdk}


```
// Initialize the Core SDK for Swift with IBM Bluemix GUID, route, and region
let myBMSClient = BMSClient.sharedInstance
myBMSClient.initialize(bluemixRegion: "Location where your app is hosted.") 
```
	{: codeblock}

### 라우트, GUID 및 Bluemix 리젼
{: route-guid-bluemix-region}

####appRoute
{: ios-approute}

Bluemix에서 생성한 서버 애플리케이션에 지정된 라우트를 지정합니다.

####GUID
{: ios-guid}

Bluemix에서 생성한 애플리케이션에 지정된 고유 키를 지정합니다. 이 값은 대소문자를 구분합니다. 

####bluemixRegionSuffix
{: ios-bluemixRegionSuffix}

앱이 호스트된 위치를 지정합니다. `bluemixRegion` 매개변수는 사용 중인 Bluemix 배치를 지정합니다. 이 값을 `BMSClient.REGION` 정적 특성으로 설정하고 세 값 중 하나를 사용할 수 있습니다. 

- BMSClient.Region.usSouth 
- BMSClient.Region.unitedKingdom
- BMSClient.Region.sydney

####AppGUID
{: ios-AppGUID}

Bluemix에서 작성한 {{site.data.keyword.mobilepushshort}} 서비스에 지정되는 고유 AppGUID 키를 지정합니다.

###클라이언트 푸시 SDK 초기화
{: initializing-the-client-Push-SDK}

```
//Initialize client Push SDK for Swift
let push = BMSPushClient.sharedInstance
push.initializeWithAppGUID("appGUID", clientSecret:"clientSecret")
```
	{: codeblock}


## iOS 애플리케이션 및 디바이스 등록
{: #enable-push-ios-notifications-register}


디바이스에 애플리케이션을 설치한 후 원격 알림을 수신하려면 애플리케이션을 APNs에 등록해야 합니다. APNs에서 생성한 디바이스 토큰을 앱에서 수신한 후에는 {{site.data.keyword.mobilepushshort}} 서비스에 이를 되돌려 보내야 합니다. 

iOS 애플리케이션과 디바이스를 등록하려면 다음을 수행해야 합니다. 

1. 백엔드 애플리케이션을 작성하십시오. 
2. 토큰을 {{site.data.keyword.mobilepushshort}}에 전달하십시오. 


###백엔드 애플리케이션 작성
{: create-a-backend-app}

Boilerplates 섹션 Bluemix® 카탈로그에서 {{site.data.keyword.mobilepushshort}} 서비스를 이 애플리케이션에 자동으로 바인드하는 백엔드 애플리케이션을 작성하십시오. 백엔드 앱을 이미 작성한 경우에는 앱을 {{site.data.keyword.mobilepushshort}} 서비스에 바인드했는지 확인하십시오. 


###{{site.data.keyword.mobilepushshort}}에 토큰 전달
{: pass-token-push-notifications}

APNs에서 토큰이 수신되면 `registerWithDeviceToken` 메소드의 일부로 {{site.data.keyword.mobilepushshort}}에 토큰을 전달하십시오. 

APNs로부터 토큰이 수신되면 이 토큰을 `didRegisterForRemoteNotificationsWithDeviceToken` 메소드의 일부로 푸시 알림에 전달하십시오. 

```
func application (_application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data){
   let push =  BMSPushClient.sharedInstance
   push.registerWithDeviceToken(deviceToken) { (response, statusCode, error) -> Void in
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
	{: codeblock}


## iOS 디바이스에서 푸시 알림 수신
{: #enable-push-ios-notifications-receiving}


iOS 디바이스에서 푸시 알림을 수신하려면 애플리케이션의 위임자에 다음 Swift 메소드를 추가하십시오.

```
// For Swift
func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) 
{ //UserInfo dictionary will contain data sent from the server }
```
	{: codeblock}

## iOS 디바이스에서 푸시 알림 모니터링
{: ios-monitoring}

알림의 현재 상태를 모니터하려면 다음 Swift 메소드를 애플리케이션의 애플리케이션 위임자에 추가하십시오.

```
// Send notification status when app is opened by clicking the notifications
func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any]) {
 let push =  BMSPushClient.sharedInstance
 let respJson = (userInfo as NSDictionary).value(forKey: "payload") as! String
 let data = respJson.data(using: String.Encoding.utf8)
 let jsonResponse:NSDictionary = try! JSONSerialization.jsonObject(with: data! , options: JSONSerialization.ReadingOptions.allowFragments) as! NSDictionary
 let messageId:String = jsonResponse.value(forKey: "nid") as! String
    push.sendMessageDeliveryStatus(messageId: messageId) { (res, ss, ee) in
      print("Send message status to the Push server")
     }
}
```
	{: codeblock}

```
// Send notification status when the app is in background mode.
func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
 let payLoad = ((((userInfo as NSDictionary).value(forKey: "aps") as! NSDictionary).value(forKey: "alert") as! NSDictionary).value(forKey: "body") as! NSString)
 self.showAlert(title: "Recieved Push notifications", message: payLoad)
 let push =  BMSPushClient.sharedInstance
 let respJson = (userInfo as NSDictionary).value(forKey: "payload") as! String
 let data = respJson.data(using: String.Encoding.utf8)
 let jsonResponse:NSDictionary = try! JSONSerialization.jsonObject(with: data! , options: JSONSerialization.ReadingOptions.allowFragments) as! NSDictionary
 let messageId:String = jsonResponse.value(forKey: "nid") as! String
 push.sendMessageDeliveryStatus(messageId: messageId) { (res, ss, ee) in
       completionHandler(UIBackgroundFetchResult.newData)
   }
}
```
	{: codeblock}


## 기본 푸시 알림 전송
{: #send}

애플리케이션을 개발한 후에는 기본 푸시 알림을 전송할 수 있습니다. 

기본 푸시 알림을 전송하려면 다음 단계를 완료하십시오. 

1. **알림 전송**을 선택하고 **받는 사람** 옵션을 선택하여 메시지를 작성하십시오. 지원되는 옵션은 **태그별 디바이스**, **디바이스 ID**, **사용자 ID**, **Android 디바이스**, **iOS 디바이스**, **웹 알림** 및 **모든 디바이스**입니다.
  
**참고**: **모든 디바이스** 옵션을 선택하는 경우 {{site.data.keyword.mobilepushshort}}를 구독하는 모든 디바이스가 알림을 수신합니다.
![알림 화면](images/tag_notification.jpg)

2. **메시지** 필드에 메시지를 작성하십시오. 필요에 따라 선택적 옵션을 구성하도록 선택하십시오.
3. **전송**을 클릭하십시오. 
3. 디바이스가 알림을 수신했는지 확인하십시오. 

다음 이미지는 iOS 디바이스에서 {{site.data.keyword.mobilepushshort}}를 처리하는 경보 상자를 표시합니다.

![iOS의 포그라운드 푸시 알림](images/iOS_Screenshot.jpg) 

### 알림 전송을 위한 선택적 설정
{: #send_ios_otpional_setting}

iOS 디바이스에 알림을 전송하기 위해 {{site.data.keyword.mobilepushshort}} 설정을 추가로 사용자 정의할 수 있습니다. 다음과 같은 선택적 사용자 정의 옵션이 지원됩니다.

- **배지**: 애플리케이션 배지에 표시되는 숫자를 나타냅니다. 기본값은 영(0)이며, 이 값은 배지를 표시하지 않습니다. 
- **사운드**: 알림을 수신할 때 재생되는 사운드 클립을 표시합니다. 기본값 또는 앱에 번들링된 사운드 리소스의 이름을 지원합니다.
- **추가 페이로드**: 알림에 대한 사용자 정의 페이로드 값을 지정합니다.

##대화식 알림 사용

대화식 알림을 설정하여 이미지, 맵 또는 응답 단추 추가와 같은 추가 세부사항으로 iOS 알림을 보강할 수 있습니다. 이를 통해 현재 컨텍스트를 종료하지 않고도 즉시 조치를 수행할 수 있는 기능과 추가 컨텍스트를 제공할 수 있습니다.   

대화식 알림을 설정하려면 다음 코드를 사용하십시오. 

```
// This defines the button action.
let actionOne = BMSPushNotificationAction(identifierName: "ACCEPT", buttonTitle: "Accept", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
 let actionTwo = BMSPushNotificationAction(identifierName: "DECLINE", buttonTitle: "Decline", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
```
	{: codeblock}
```
// This defines category for the buttons
let category = BMSPushNotificationActionCategory(identifierName: "category", buttonActions: [actionOne, actionTwo])
```
	{: codeblock}
```
// This updates the registration to include the buttonsPass the defined category into iOS BMSPushClientOptions
let notificationOptions = BMSPushClientOptions(categoryName: [category])
let push = BMSPushClient.sharedInstance
push.initializeWithAppGUID(appGUID: "APP-GUID-HERE", clientSecret:"CLIENT-SECRET-HERE", options: notificationOptions)
```
	{: codeblock}

대화식 알림을 보내려면 다음 단계를 완료하십시오. 

1. 작성 섹션의 받는 사람 드롭 다운 목록에서 **iOS 디바이스**를 선택합니다. 
2. 보내려는 알림 메시지를 입력합니다. 
3. 선택적 설정 섹션에서 **모바일**을 선택하고 **iOS**를 클릭합니다.
4. 유형 드롭 다운 목록에서 **혼합**을 선택합니다.
5. 카테고리 필드에서 앱에서 정의한 알림 유형을 지정합니다.  

![iOS용 대화식 알림](images/push_ios_notification_interactive.jpg) 

## 다음 단계
{: #next_steps_tags}

정상적으로 기본 알림을 설정한 후 태그 기반 알림 및 고급 옵션을 구성할 수 있습니다. 

이러한 푸시 알림 서비스 기능을 앱에 추가하십시오.
태그 기반 알림을 사용하려면 [태그 기반 알림](c_tag_basednotifications.html)을 참조하십시오.
고급 알림 옵션을 사용하려면 [고급 푸시 알림 사용](t_advance_badge_sound_payload.html)의 내용을 참조하십시오. 
