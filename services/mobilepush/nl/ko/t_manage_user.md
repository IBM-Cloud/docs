---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 사용자 ID를 사용하여 디바이스 등록
{: #register_device_with_userId}
마지막 업데이트 날짜: 2017년 2월 06일
{: .last-updated}

사용자 ID 기반 알림에 등록하려면 다음 단계를 완료하십시오. 

## Android
{: android-register}

{{site.data.keyword.mobilepushshort}} 서비스의 `AppGUID`와 `clientSecret` 키를 사용하여 MFPPush 클래스를 초기화하십시오. 
```
// Initialize the Push Notifications service
push = MFPPush.getInstance();
push.initialize(getApplicationContext(),"AppGUID", "clientSecret");
```
	{: codeblock}


- **AppGUID**: {{site.data.keyword.mobilepushshort}} 서비스의 AppGUID입니다. 
- **clientSecret**: {{site.data.keyword.mobilepushshort}} 서비스의 clientSecret 키입니다. 

  **registerDeviceWithUserId** API를 사용하여 {{site.data.keyword.mobilepushshort}}를 받을 디바이스를 등록하십시오. 

```
// Register the device to Push Notifications
push.registerDeviceWithUserId("userId",new MFPPushResponseListener<String>() {
		@Override
		public void onSuccess(String response) {
		Log.d("Device is registered with Push Service.");}
		@Override
		public void onFailure(MFPPushException ex) {
		  Log.d("Error registering with Push Service...\n"
   		  + "Push notifications will not be received.");
		}
		});
```
	{: codeblock}

- **사용자 ID**: {{site.data.keyword.mobilepushshort}}에 등록하기 위한 고유 사용자 ID 값을 전달하십시오.

**참고:** UserId로 대상이 지정되는 {{site.data.keyword.mobilepushshort}}를 사용하려면 UserId를 사용하여 디바이스를 등록하고 {{site.data.keyword.mobilepushshort}} 서비스가 프로비저닝될 때 할당되는 'clientSecret'을 전달해야 합니다. 올바른 clientSecret이 없으면 디바이스 등록에 실패합니다. 

## Cordova
{: cordova}

다음 API를 사용하여 UserId 기반 {{site.data.keyword.mobilepushshort}}를 받도록 등록하십시오. 

```
// Register device for Push Notification with UserId
var options = {"userId": "Your User Id value"};
BMSPush.registerDevice(options,success, failure);
```
	{: codeblock}


- **사용자 ID**: {{site.data.keyword.mobilepushshort}}에 등록하기 위한 고유 사용자 ID 값을 전달하십시오.


## Swift
{: swift-register}

```
// Initialize the BMSPushClient
let push =  BMSPushClient.sharedInstance
push.initializeWithAppGUID("appGUID", clientSecret:"clientSecret")
```
	{: codeblock}


- **AppGUID**: {{site.data.keyword.mobilepushshort}} 서비스의 AppGUID입니다. 
- **clientSecret**: {{site.data.keyword.mobilepushshort}} 서비스의 clientSecret 키입니다. 

**registerWithUserId** API를 사용하여 {{site.data.keyword.mobilepushshort}}를 받을 디바이스를 등록하십시오. 

```
// Register the device to Push Notifications service
push.registerWithDeviceToken("deviceToken", WithUserId: "userId")  { (response, statusCode, error) -> Void in
if error.isEmpty {
  print( "Response during device registration : \(response)")
  print( "status code during device registration : \(statusCode)")
  } else {
  print( "Error during device registration \(error) ")
  }
  }
```
	{: codeblock}

- **사용자 ID**: {{site.data.keyword.mobilepushshort}}에 등록하기 위한 고유 사용자 ID 값을 전달하십시오.

## Google Chrome, Safari 및 Mozilla Firefox
{: web-register}

사용자 ID 기반 알림에 등록하려면 다음 API를 사용하십시오. `app GUID`, `app Region` 및 `Client Secret`을 사용하여 SDK를 초기화하십시오.

```
var bmsPush = new BMSPush();
var params = {
    "appGUID":"push app GUID",
    "appRegion":"App Region",
    "clientSecret":"Push Client Secret" 
    }
  bmsPush.initialize(params, function(response){
          alert(response.response)
      })
```
	{: codeblock}
  
초기화가 완료되면 사용자 ID를 사용하여 웹 애플리케이션을 등록하십시오.

```
    bmsPush.registerWithUserId("UserId", function(response) {
      alert(response.response)
  })
```
	{: codeblock}

## Google Chrome 앱 및 확장 프로그램
{: web-register-new}

사용자 ID 기반 알림에 등록하려면 다음 API를 사용하십시오. `app GUID`, `app Region` 및 `Client Secret`을 사용하여 SDK를 초기화하십시오.

```
var bmsPush = new BMSPush();
var params = {
    "appGUID":"push app GUID",
    "appRegion":"App Region",
    "clientSecret":"Push Client Secret" 
    }
  bmsPush.initialize(params, function(response){
          alert(response.response)
      })
```
	{: codeblock}
  
초기화가 완료되면 사용자 ID로 웹 애플리케이션을 등록해야 합니다. 

```
    bmsPush.registerWithUserId("UserId", function(response) {
      alert(response.response)
  })
```
	{: codeblock}

# 사용자 ID 기반 알림 사용
{: #using_userid}

사용자 ID 기반 알림은 특정 사용자를 대상으로 하는 알림 메시지입니다. 하나의 사용자에 여러 디바이스를 등록할 수 있습니다. 다음 단계는 사용자 ID 기반 알림을 전송하는 방법에 대해 설명합니다. 

1. **Push Notification** 대시보드에서 **알림 전송** 옵션을 선택하십시오. 
1. **받는 사람** 옵션 목록에서 **사용자 ID**를 선택하십시오. 
1. **사용자 ID** 필드에서 사용하려는 사용자 ID를 검색한 후 **+추가**를 클릭하십시오. ![알림 화면](images/user_notification.jpg)
1. **메시지** 필드에 알림에서 전송할 텍스트를 입력하십시오. 
1. **전송**을 클릭하십시오. 
