---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# userId によるデバイスの登録
{: #register_device_with_userId}
最終更新日: 2017 年 2 月 6 日
{: .last-updated}

userId ベースの通知への登録を行うには、以下の手順を実行します。

## Android
{: android-register}

{{site.data.keyword.mobilepushshort}}サービスの `AppGUID` および `clientSecret` キーを使用して MFPPush クラスを初期化します。
```
// Initialize the Push Notifications service
push = MFPPush.getInstance();
push.initialize(getApplicationContext(),"AppGUID", "clientSecret");
```
	{: codeblock}


- **AppGUID**: これは、{{site.data.keyword.mobilepushshort}} サービスの AppGUID キーです。
- **clientSecret**: これは、{{site.data.keyword.mobilepushshort}} サービスの clientSecret キーです。

  **registerDeviceWithUserId** API を使用して、デバイスを{{site.data.keyword.mobilepushshort}}に登録します。

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

- **userId**: {{site.data.keyword.mobilepushshort}} への登録を行うための固有の userId 値を渡します。

**注:** UserId によってターゲット指定される{{site.data.keyword.mobilepushshort}}を有効にするには、必ず、UserId を指定してデバイスを登録し、{{site.data.keyword.mobilepushshort}}サービスのプロビジョン時に割り振られる「clientSecret」も渡してください。有効な clientSecret がないと、デバイス登録は失敗します。

## Cordova
{: cordova}

以下の API を使用して、UserId ベースの{{site.data.keyword.mobilepushshort}}への登録を行います。

```
// Register device for Push Notification with UserId
var options = {"userId": "Your User Id value"};
BMSPush.registerDevice(options,success, failure);
```
	{: codeblock}


- **userId**: {{site.data.keyword.mobilepushshort}} への登録を行うための固有の userId 値を渡します。


## Swift
{: swift-register}

```
// Initialize the BMSPushClient
let push =  BMSPushClient.sharedInstance
push.initializeWithAppGUID("appGUID", clientSecret:"clientSecret")
```
	{: codeblock}


- **AppGUID**: これは、{{site.data.keyword.mobilepushshort}} サービスの AppGUID キーです。
- **clientSecret**: これは、{{site.data.keyword.mobilepushshort}} サービスの clientSecret キーです。

**registerWithUserId** API を使用して、デバイスを{{site.data.keyword.mobilepushshort}}に登録します。

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

- **userId**: {{site.data.keyword.mobilepushshort}} への登録を行うための固有の userId 値を渡します。

## Google Chrome、Safari、および Mozilla Firefox
{: web-register}

以下の API を使用して、userId ベースの通知への登録を行います。`app GUID`、`app Region`、および `Client Secret` を使用して SDK を初期化します。

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
  
初期化が正常に完了したら、userId を指定して Web アプリケーションを登録します。

```
bmsPush.registerWithUserId("UserId", function(response) {
 alert(response.response)
  })
```
	{: codeblock}

## Google Chrome アプリケーションおよびエクステンション
{: web-register-new}

以下の API を使用して、userId ベースの通知への登録を行います。`app GUID`、`app Region`、および `Client Secret` を使用して SDK を初期化します。

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
  
正常に初期化された後、userId を使用して Web アプリケーションを登録する必要があります。

```
bmsPush.registerWithUserId("UserId", function(response) {
 alert(response.response)
  })
```
	{: codeblock}

# userId ベースの通知の使用
{: #using_userid}

userId ベースの通知は、特定のユーザーをターゲットとする通知メッセージです。1 つのユーザーで複数のデバイスを登録できます。以下の手順では、ユーザー ID ベースの通知の送信方法を説明します。

1. **「プッシュ通知」**ダッシュボードで、**「通知の送信 (Send Notifications)」**オプションを選択します。
1. **「送信先 (Send to)」**リストのオプションで**「UserId」**を選択します。
1. **「ユーザー ID」**フィールドで、使用するユーザー ID を検索し、**「+ 追加 (+Add)」**をクリックします。![「通知」画面](images/user_notification.jpg)
1. **「メッセージ」**フィールドに、通知で送信するテキストを入力します。
1. **「送信」**をクリックします。
