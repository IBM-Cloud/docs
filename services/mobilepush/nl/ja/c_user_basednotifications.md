---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# ユーザー・ベースの通知の使用可能化
{: #user_based_notifications}
最終更新日: 2017 年 2 月 28 日
{: .last-updated}

ユーザー ID ベースの{{site.data.keyword.mobilepushshort}}は、カスタマイズしたメッセージを使用し、モバイル・アプリ・ユーザーをターゲットとします。ユーザー・ベースの通知では、通知設定に基づいて特定の個人に通知するように選択できます。

## ユーザー ID を使用したデバイスの登録
{: #register_device_wh_userid}

ユーザー ID によってターゲット指定されるプッシュ通知を有効にするには、必ず、「ユーザー ID」フィールドを設定した状態でデバイスを登録してください。     

ユーザー ID には、アプリケーションがデバイス登録 API に提供する任意のストリングが可能です。通常、モバイル・アプリケーションはまず、[{{site.data.keyword.amafull}} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/docs/services/mobileaccess/index.html){: new_window}などの認証サービスに対してモバイル・アプリ・ユーザーを認証する認証サイクルを実行します。認証に成功すると、認証済みユーザー ID がプッシュ・デバイス登録 API に渡されます。 

userId ベースの通知への登録を行うには、以下の手順を実行します。

### Android
{: #android-register}

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

### Cordova
{: #cordova_register}

以下の API を使用して、UserId ベースの{{site.data.keyword.mobilepushshort}}への登録を行います。

```
// Register device for Push Notification with UserId
var options = {"userId": "Your User Id value"};
BMSPush.registerDevice(options,success, failure);
```
	{: codeblock}


- **userId**: {{site.data.keyword.mobilepushshort}} への登録を行うための固有の userId 値を渡します。


### Swift
{: #swift-register}

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

### Google Chrome、Safari、および Mozilla Firefox
{: #web-register}

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

### Google Chrome アプリケーションおよびエクステンション
{: #web-register-new}

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

## userId ベースの通知の使用
{: #using_userid}

userId ベースの通知は、特定のユーザーをターゲットとする通知メッセージです。1 つのユーザーで複数のデバイスを登録できます。以下の手順では、ユーザー ID ベースの通知の送信方法を説明します。

1. **「プッシュ通知」**ダッシュボードで、**「通知の送信 (Send Notifications)」**オプションを選択します。
1. **「送信先 (Send to)」**リストのオプションで**「UserId」**を選択します。
1. **「ユーザー ID」**フィールドで、使用するユーザー ID を検索し、**「+ 追加 (+Add)」**をクリックします。![「通知」画面](images/user_notification.jpg)
1. **「メッセージ」**フィールドに、通知で送信するテキストを入力します。
1. **「送信」**をクリックします。


## ユーザーのログインおよびログアウトの同期化 
{: #sync_login_logout}

ユーザーがログインしている場合にのみ通知を送信するようにすることができます。 

例えば、デバイスが家族や職場のチームのメンバーによって共有されているときに、特定ユーザーに対応する必要がある場合を考えてください。そのようなユース・ケースでは、ユーザー・ログイン/ログアウト・シーケンスを使用できます。この認証メカニズムを使用すると、アプリケーションが、アプリケーションの現在のユーザーの ID を追跡できるようになります。これにより、特定のユーザーをターゲットとした通知は、常にそのユーザーのみが受信するようにできます。正常なログインの後、ログイン・ユーザーのユーザー ID を渡すデバイス登録 API を呼び出します。ログアウトの前にも同様に、デバイス登録抹消 API を呼び出します。これらのプッシュ API を、ログインおよびログアウトと共にシーケンスにすると、特定のユーザー向けの通知がそのユーザーだけに送信されるようになります。
