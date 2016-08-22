---

copyright:
 years: 2015, 2016

---


# 사용자 ID를 사용하여 디바이스 등록
{: #register_device_with_userId}
*마지막 업데이트 날짜: 2016년 7월 20일*
{: .last-updated}

사용자 ID 기반 알림을 등록하려면, 다음 단계를 완료하십시오. 

## Android
 
푸시 알림 서비스의 `pushTenantId` 및 `clientSecret` 키를 사용하여 IMFPush 클래스를 초기화하십시오. 

```
// Initialize the MFPPush
push = MFPPush.getInstance();
push.initializeBluemixPushWithClientSecret(getApplicationContext(),"clientSecret");
```

**clientSecret** 

푸시 알림 서비스의 clientSecret 키입니다. 


**registerWithUserId** API를 사용하여 푸시 알림에 디바이스를 등록하십시오. 

```
// Register the device to push notifications service.
push.registerWithUserId("userId",new MFPPushResponseListener<String>() {
    @Override
	    public void onSuccess(String deviceId) {
	           updateTextView("Device is registered with Push Service.");
        displayTags();
    }

    @Override
    public void onFailure(MFPPushException ex) {
         updateTextView("Error registering with Push Service...\n"
        + "Push notifications will not be received.");
    }
});
```

**userId** 

푸시 알림에 등록하기 위한 고유 사용자 ID 값을 전달합니다. 

>**참고:** UserID로 대상이 지정되는 푸시 알림을 사용하려면, UserId를 사용하여 디바이스를 등록하고 푸시 알림 서비스가 프로비저닝될 때 할당되는 'clientSecret'을 전달해야 합니다. 올바른 clientSecret을 전달하지 않는 경우 디바이스 등록은 실패합니다.


## Cordova

다음 코드 스니펫을 모바일 애플리케이션에 복사하여 사용자 ID 기반 알림에 등록하십시오. 

`clientsecret`을 사용하여 `MFPPush`를 초기화하십시오.  

```
MFPPush.initializeBluemixPushWithClientSecret("clientSecret");
```

**clientSecret** 

푸시 알림 서비스의 clientSecret 키입니다. 

```
//Register for Push notification with userId
var userId = "userId";
MFPPush.registerWithUserId(userId,success,failure);
```
**userId** 

푸시 알림 서비스에 등록하기 위한 고유 사용자 ID 값을 전달합니다. 


## Objective-C


다음 API를 사용하여 사용자 ID 기반 푸시 알림에 등록하십시오. 


```
// Initialize the MFPPush
IMFPushClient* push = [IMFPushClient sharedInstance];
[push initializeBluemixPushWithClientSecret:@"clientSecret"];
```

**clientSecret** 

푸시 알림 서비스의 clientSecret 키입니다. 


**registerWithUserId** API를 사용하여 푸시 알림에 디바이스를 등록하십시오. 


```
// Register the device to push notifications service.
[push registerDeviceToken:deviceToken WithUserId:@"userId" completionHandler:^(IMFResponse *response, NSError *error) {
    NSString *message=@"";
    
	if (error){
        message = [NSString stringWithFormat:@"Error registering for push notifications: %@", error.description];
        NSLog(@"%@",message);
    } else {
        message=@"Successfully registered for push notifications";
        NSLog(@"%@",message);
    }
}];
```


**userId** 

푸시 알림에 등록하기 위한 고유 사용자 ID 값을 전달합니다. 

## Swift

```
// Initialize the BMSPushCliet
let push =  BMSPushClient.sharedInstance
push.initializeBluemixPushWithClientSecret("clientSecret")
```

**clientSecret** 

푸시 알림 서비스의 clientSecret 키입니다. 

**registerWithUserId** API를 사용하여 푸시 알림에 디바이스를 등록하십시오. 

```
// Register the device to Push Notifications service.
push.registerDeviceToken("deviceToken", WithUserId: "userId")  { (response, statusCode, error) -> Void in
if error.isEmpty {

    print( "Response during device registration : \(response)")

        print( "status code during device registration : \(statusCode)")

    } else {

        print( "Error during device registration \(error) ")
    }
}
```

**userId** 

푸시 알림에 등록하기 위한 고유 사용자 ID 값을 전달합니다. 


# 사용자 ID 기반 알림 사용
{: #using_userid}


사용자 ID 기반 알림은 특정 사용자로 대상이 지정되는 알림 메시지입니다. 하나의 사용자에 여러 디바이스를 등록할 수 있습니다. 다음 단계는 사용자 ID 기반 알림을 전송하는 방법에 대해 설명합니다.  

1. **푸시 알림** 대시보드에서 **알림** 탭을 클릭하십시오. 
1. 사용자 ID 기반 알림을 전송하려면 **UserId** 옵션을 선택하십시오. 
1. UserID **검색** 필드에서 사용하려는 사용자 ID를 검색한 다음 **+추가** 단추를 클릭하십시오. ![알림 화면](images/tag_notification.jpg)
1. **메시지 텍스트** 필드에 알림으로 전송할 텍스트를 입력하십시오. 
1. **전송** 단추를 클릭하십시오. 
