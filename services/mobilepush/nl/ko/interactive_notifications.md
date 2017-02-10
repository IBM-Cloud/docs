ka---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 대화식 알림
{: #interactive-notifications}
마지막 업데이트 날짜: 2017년 1월 18일
{: .last-updated}

대화식 알림을 사용하면 애플리케이션을 열지 않고 알림에 응답할 수 있습니다. 대화식 알림이 도착하면 디바이스에 알림 메시지와 함께 조치 단추가 표시됩니다. 대화식 알림은 iOS 버전 8 이상이 설치된 디바이스에서 지원됩니다. 버전 8 미만의 iOS 디바이스에 보낸 대화식 알림의 경우 알림 조치가 표시되지 않습니다.

##대화식 {{site.data.keyword.mobilepushshort}} 전송


푸시 대시보드 또는 [REST API 문서](t_restapi.html)를 사용하여 대화식 알림을 전송할 수 있습니다. 

{{site.data.keyword.mobilepushshort}} 콘솔에서 다음을 수행하십시오. 

1. 푸시 대시보드의 알림 탭에서 **알림 전송**을 클릭하십시오.  
2. 알림 수신인을 선택하고 **다음**을 클릭하십시오.  
3. 알림 작성 페이지에서 유형을 기본 또는 혼합으로 설정하고 고급 옵션 탭에서 카테고리 값을 지정하여 대화식 푸시를 전송할 수 있습니다. 클라이언트에서 카테고리 값을 구성하려면 기본 iOS 애플리케이션 섹션에서 **대화식 {{site.data.keyword.mobilepushshort}} 처리**를 선택하십시오. 

## iOS 애플리케이션에서 대화식 {{site.data.keyword.mobilepushshort}} 처리


### Swift

대화식 알림을 받으려면 다음 단계를 완료하십시오. 

1. 애플리케이션이 원격 알림 수신에 대한 백그라운드 태스크를 수행하는 기능을 사용으로 설정하십시오.  
1. 조치 카테고리로 `BMSPush` SDK를 초기화하십시오.
	```
	let myBMSClient = BMSClient.sharedInstance
	myBMSClient.initialize(bluemixRegion: BMSClient.Region.usSouth)
	let push =  BMSPushClient.sharedInstance
    let actionOne = BMSPushNotificationAction(identifierName: "FIRST", buttonTitle: "Accept", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
   	let actionTwo = BMSPushNotificationAction(identifierName: "SECOND", buttonTitle: "Reject", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
   	let category = BMSPushNotificationActionCategory(identifierName: "category", buttonActions: [actionOne, actionTwo])
   	let notifOptions = BMSPushClientOptions(categoryName: [category])
	push.initializeWithAppGUID(appGUID: "YOUR_APP_GUID", clientSecret:"YOUR_APP_CLIENT_SECRET", options: notifOptions)
	```
		{: codeblock}

1. AppDelegate에서 다음과 같이 새 콜백 메소드를 구현하십시오.
	```
	 func userNotificationCenter(_ center: UNUserNotificationCenter,
       didReceive response: UNNotificationResponse,
       withCompletionHandler completionHandler: @escaping () -> Void) {
            switch response.actionIdentifier {
		    case "FIRST":
		      print("FIRST")
		    case "SECOND":
		      print("SECOND")  
		    default:
		      print("Unknown action")
		    }
		completionHandler
	}
	```
	{: codeblock} 
5. 이 새로운 콜백 메소드는 사용자가 조치 단추를 클릭할 때 호출됩니다. 이 메소드를 구현하기 위해서는 지정된 ID와 연관된 태스크를 수행하고 `completionHandler` 매개변수에서 블록을 실행해야 합니다. 


### Cordova

Cordova iOS 애플리케이션에서 조치 가능 알림을 받으려면 다음 단계를 완료하십시오.

1. `BMSPush.initialize` 메소드에 카테고리 필드를 추가합니다.
   ```
	var category =  {"Category_Name":[{"IdentifierName_1":"actionName_1"},{"IdentifierName_2":"actionName_2"}]}
       BMSPush.initialize(appGUID,clientSecret,category);
    ```
	{: codeblock} 
2. AppDelegate에서 새 콜백 메소드를 구현합니다.
3. 이 새로운 콜백 메소드는 사용자가 조치 단추를 클릭할 때 호출됩니다. 이 메소드를 구현하기 위해서는 지정된 ID와 연관된 태스크를 수행하고 completionHandler 매개변수에서 블록을 실행해야 합니다. 
