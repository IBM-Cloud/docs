---

copyright:
 years: 2015, 2016

---

# 디바이스에서 푸시 알림 수신
{: #cordova_receive}

디바이스에서 푸시 알림을 수신하려면 다음 코드 스니펫을 복사하여 붙여넣으십시오. 

##JavaScript

다음의 JavaScript 코드 스니펫을 Cordova 애플리케이션의 웹 파트에 추가하십시오. 


```
var notification = function(notification){
    // notification is a JSON object.
    alert(notification.message);
};
MFPPush.registerNotificationsCallback(notification);
```

##Android 알림 특성

다음 섹션에는 Android 알림 특성이 나열되어 있습니다. 

* 메시지 - 푸시 알림 메시지
* 페이로드 - 알림 페이로드를 포함하는 JSON 오브젝트


##iOS 알림 특성

다음 섹션에는 iOS 알림 특성이 나열되어 있습니다. 

* 메시지 - 푸시 알림 메시지
* 페이로드 - 알림 페이로드를 포함한 JSON 오브젝트
action-loc-key - 문자열은 "보기" 대신 오른쪽 단추의 제목에 사용할 현재 로컬라이제이션의 현지화된 문자열을 가져오기 위한 키로 사용됩니다. 
* 배지 - 앱 아이콘의 배지로 표시할 숫자입니다. 이 특성을 비워두면 배지가 변경되지 않습니다. 배지를 제거하려면 이 특성의 값을 0으로 설정하십시오. 
* 사운드 - 앱 번들 또는 앱 데이터 컨테이너의 라이브러리/사운드 폴더에 있는 사운드 파일의 이름입니다. 

##Objective-C

다음의 Objective-C 코드 스니펫을 애플리케이션 위임 클래스에 추가하십시오. 

```
// Handle receiving a remote notification
-(void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo fetchCompletionHandler:(void (^)(UIBackgroundFetchResult))completionHandler {

 [[CDVMFPPush sharedInstance] didReceiveRemoteNotification:userInfo];
}
```

```
// Handle receiving a remote notification on launch
- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions

    [[CDVMFPPush sharedInstance] didReceiveRemoteNotificationOnLaunch:launchOptions];
}
```

##Swift

다음의 Swift 코드 스니펫을 애플리케이션 위임 클래스에 추가하십시오. 

```
// Handle receiving a remote notification
funcapplication(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: ){

    CDVMFPPush.sharedInstance().didReceiveRemoteNotification(userInfo)
}
```

```
// Handle receiving a remote notification on launch
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {


    CDVMFPPush.sharedInstance().didReceiveRemoteNotificationOnLaunch(launchOptions)
}

```
다음 단계. [기본 푸시 알림 전송](t_send_push_notifications.html).
