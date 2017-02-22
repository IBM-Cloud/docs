---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

#고급 푸시 알림 사용
마지막 업데이트 날짜: 2017년 1월 11일
{: .last-updated}

iOS 배지, 사운드, 추가 JSON 페이로드, 조치 가능 알림, 보류 알림을 구성합니다. 

## 사운드, 페이로드 및 iOS 배지 구성
{: #badge-sound-payload}

iOS 배지, 사운드 및 추가적인 JSON 페이로드를 구성합니다. 

1. {{site.data.keyword.mobilepushshort}} 대시보드에서 **알림** 탭으로 이동하십시오. 
2. **선택적 필드** 섹션으로 이동하여 다음과 같이 {{site.data.keyword.mobilepushshort}} 기능을 구성하십시오.  
	- **사운드 파일** - 모바일 앱의 사운드 파일을 가리키는 문자열을 입력하십시오. 페이로드에서 사용할 사운드 파일의 문자열 이름을 지정하십시오. 
	- **iOS 배지** - iOS 디바이스의 경우 앱 아이콘의 배지로 표시할 숫자입니다. 이 특성을 비워두면 배지가 변경되지 않습니다. 배지를 제거하려면 이 특성의 값을 0으로 설정하십시오. 
	
###Android

Android 애플리케이션의 `res/raw` 디렉토리에 사운드 파일을 추가하십시오. 알림을 전송하는 동안 {{site.data.keyword.mobilepushshort}}의 사운드 필드에 사운드 파일 이름을 추가하십시오. 

```
"settings":{
     "gcm":{
     "sound":"tt.wav",
	 }
 }  
```
    {: codeblock}	
	
###iOS

```
"settings": {
     "apns" : {
      "badge": 10,
	     "sound": "tt.wav",
	 }
	}
``` 
	{: codeblock}
		
**추가 페이로드** - 이 페이로드는 키-값 쌍이며 {{site.data.keyword.mobilepushshort}}를 사용하여 전송하려는 JSON 오브젝트여야 합니다.

```
{"key":"value", "key2":"value2"}
```
	{: codeblock}

## Android 알림 보류 
{: #hold-notifications-android}

애플리케이션이 백그라운드로 전환되는 경우 {{site.data.keyword.mobilepushshort}}에서 애플리케이션에 전송되는 알림을 보류할 수 있습니다. 알림을 보류하려면 {{site.data.keyword.mobilepushshort}}를 처리하는 활동의 onPause() 메소드에서 hold() 메소드를 호출하십시오. 

```
@Override
protected void onPause() {
super.onPause();
    if (push != null) {
                push.hold();
    }
} 
```
	{: codeblock}
## iOS 조치 가능 알림 사용  
{: #enable-actionable-notifications-ios}

일반적인 {{site.data.keyword.mobilepushshort}}와 달리 조치 가능 알림은 사용자가 알림 경보 수신 시 앱을 열지 않고 조치를 선택할 수 있는 프롬프트를 표시합니다.  

애플리케이션에서 조치 가능 {{site.data.keyword.mobilepushshort}}를 사용하려면 다음 단계를 완료하십시오. 

1. 사용자 응답 조치를 작성하십시오. 
```
//For Swift
	let acceptAction = UIMutableUserNotificationAction()
	acceptAction.identifier = "ACCEPT_ACTION"
	acceptAction.title = "Accept"
	acceptAction.destructive = false
	acceptAction.authenticationRequired = false
	acceptAction.activationMode = UIUserNotificationActivationMode.Foreground
```
	{: codeblock}
```
//For Swift
	let declineAction = UIMutableUserNotificationAction()
	declineAction.identifier = "DECLINE_ACTION"
	declineAction.title = "Decline"
	declineAction.destructive = true
	declineAction.authenticationRequired = false
	declineAction.activationMode = UIUserNotificationActivationMode.Background
```
	{: codeblock}

2. 알림 카테고리를 작성하고 조치를 설정하십시오. **UIUserNotificationActionContextDefault** 또는 **UIUserNotificationActionContextMinimal**이 올바른 컨텍스트입니다.
```
// For Swift
	let pushCategory = UIMutableUserNotificationCategory()
	pushCategory.identifier = "TODO_CATEGORY"
	pushCategory.setActions([acceptAction, declineAction], forContext: UIUserNotificationActionContext.Default)
```
	{: codeblock}

1. 알림 설정을 작성하고 이전 단계에서 작성한 카테고리를 지정하십시오. 
```
// For Swift
	let categories = NSSet(array:[pushCategory]);
```
	{: codeblock}

1. 로컬 또는 원격 알림을 작성하고 카테고리 ID를 지정하십시오. 
```
//For Swift
	let settings = UIUserNotificationSettings(forTypes: [.Alert, .Badge, .Sound], categories: categories as? Set<UIUserNotificationCategory>)
    UIApplication.sharedApplication().registerUserNotificationSettings(settings)
    UIApplication.sharedApplication().registerForRemoteNotifications()
```
	{: codeblock}
	
## 조치 가능 iOS 알림 처리  
{: #actionable-notifications}

조치 가능 알림이 수신되면 선택한 ID를 기반으로 다음 메소드에 제어가 전달됩니다.

 
```
func application(application: UIApplication, handleActionWithIdentifier identifier: String?, forRemoteNotification userInfo: [NSObject : AnyObject], completionHandler: () -> Void) {
      //must call completion handler when finished
      completionHandler()
  }
```    
	{: codeblock}
    
