---

copyright:
 years: 2015, 2016

---

# 대화식 알림
{: #interactive-notifications}

대화식 알림을 사용자여 사용자는 알림이 도착했을 때 애플리케이션을 열지 않고 조치를 취할 수 있습니다. 대화식 알림이 도착하면 디바이스에 알림 메시지와 함께 조치 단추가 표시됩니다. 대화식 알림은 iOS 버전 8 이상이 설치된 디바이스에서
지원됩니다. iOS 버전 8 미만이 설치된 디바이스에 대화식 알림이 전송되는 경우에는 알림 조치가 표시되지 않습니다.  

##대화식 푸시 알림 전송


대화식 알림은 푸시 대시보드 또는 REST API를 사용하여 전송할 수 있습니다(REST API 문서 참조).

푸시 콘솔에서: 

푸시 대시보드의 알림 탭 아래에서 알림 전송을 클릭하십시오. 알림 수신인을 선택하고 다음을 클릭하십시오. 알림 작성 페이지에서 대화식 푸시는 유형을 기본 또는 혼합으로 설정하고 고급 옵션 탭 아래에서 카테고리 값을 지정하여 전송할 수 있습니다. 클라이언트에서 카테고리 값을 구성하려면 기본 iOS 애플리케이션 섹션에서 대화식 푸시 알림 처리를 선택하십시오. 

## iOS 애플리케이션에서 대화식 푸시 알림 처리

대화식 알림을 받으려면 다음 단계를 따라야 합니다. 

1. 애플리케이션이 원격 알림 수신에 대한 백그라운드 태스크를 수행하는 기능을 사용으로 설정하십시오. 이 단계는 일부 조치가 백그라운드를 사용할 경우에 필요합니다. 
1. `AppDelegate (application: didRegisterForRemoteNotificationsWithDeviceTokenapplication:)`에서
`WLPush Object`에 `deviceToken`을 설정하기 전에 카테고리를 설정하십시오. 

```
	if([application respondsToSelector:@selector(registerUserNotificationSettings:)]){
	 UIUserNotificationType userNotificationTypes = UIUserNotificationTypeNone | UIUserNotificationTypeSound | UIUserNotificationTypeAlert | UIUserNotificationTypeBadge;
	      
	 UIMutableUserNotificationAction *acceptAction = [[UIMutableUserNotificationAction alloc] init];
	 acceptAction.identifier = @"OK";
	 acceptAction.title = @"OK";
	      
	 UIMutableUserNotificationAction *rejetAction = [[UIMutableUserNotificationAction alloc] init];
	 rejetAction.identifier = @"NOK";
	 rejetAction.title = @"NOK";
	      
	 UIMutableUserNotificationCategory *cateogory = [[UIMutableUserNotificationCategory alloc] init];
	 cateogory.identifier = @"poll";
	 [cateogory setActions:@[acceptAction,rejetAction] forContext:UIUserNotificationActionContextDefault];
	 [cateogory setActions:@[acceptAction,rejetAction] forContext:UIUserNotificationActionContextMinimal];
	      
	 NSSet *catgories = [NSSet setWithObject:cateogory];
	 [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:userNotificationTypes categories:catgories]];
}
```

1. AppDelegate에 새로운 콜백 메소드 구현:

```
	-(void)application:(UIApplication *)application handleActionWithIdentifier:(NSString *)identifier forRemoteNotification:(NSDictionary *)userInfo completionHandler:(void (ˆ)())completionHandler
``` 

5. 이 새로운 콜백 메소드는 사용자가 조치 단추를 클릭할 때 호출됩니다. 이 메소드를 구현하기 위해서는 지정된 ID와 연관된 작업을 수행하고 `completionHandler` 매개변수의 블록을 실행해야 합니다. 
