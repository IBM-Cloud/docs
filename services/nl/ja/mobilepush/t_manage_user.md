---

copyright:
 years: 2015, 2016

---


# UserId を使用したデバイスの登録
{: #register_device_with_userId}
*最終更新日: 2016 年 7 月 20 日*
{: .last-updated}

ユーザー ID ベースの通知への登録を行うには、以下の手順を実行します。

## Android
 
プッシュ通知サービスの `pushTenantId` と `clientSecret` 鍵を使用して、IMFPush クラスを初期化します。

```
// Initialize the MFPPush
push = MFPPush.getInstance();
push.initializeBluemixPushWithClientSecret(getApplicationContext(),"clientSecret");
```

**clientSecret** 

これは、プッシュ通知サービスのクライアント秘密鍵です。


**registerWithUserId** API を使用して、デバイスをプッシュ通知に登録します。

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

プッシュ通知への登録を行うための固有のユーザー ID 値を渡します。

>**注:** UserId によってターゲット指定されるプッシュ通知を有効にするには、必ず、UserId を使用してデバイスを登録し、プッシュ通知サービスのプロビジョン時に割り振られる「クライアント秘密鍵」も渡してください。有効なクライアント秘密鍵を渡さないと、デバイスの登録は失敗します。


## Cordova

ユーザー ID ベースの通知への登録を行うには、次のコード・スニペットをモバイル・アプリケーションにコピーします。

`clientsecret` を使用して `MFPPush` を初期化します。 

```
MFPPush.initializeBluemixPushWithClientSecret("clientSecret");
```

**clientSecret** 

これは、プッシュ通知サービスのクライアント秘密鍵です。

```
//Register for Push notification with userId
var userId = "userId";
MFPPush.registerWithUserId(userId,success,failure);
```
**userId**

プッシュ通知サービスへの登録を行うための固有のユーザー ID 値を渡します。


## Objective-C


以下の API を使用して、ユーザー ID ベースのプッシュ通知への登録を行います。


```
// Initialize the MFPPush
IMFPushClient* push = [IMFPushClient sharedInstance];
[push initializeBluemixPushWithClientSecret:@"clientSecret"];
```

**clientSecret** 

これは、プッシュ通知サービスのクライアント秘密鍵です。


**registerWithUserId** API を使用して、デバイスをプッシュ通知に登録します。


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

プッシュ通知への登録を行うための固有のユーザー ID 値を渡します。

## Swift

```
// Initialize the BMSPushCliet
let push =  BMSPushClient.sharedInstance
push.initializeBluemixPushWithClientSecret("clientSecret")
```

**clientSecret** 

これは、プッシュ通知サービスのクライアント秘密鍵です。

**registerWithUserId** API を使用して、デバイスをプッシュ通知に登録します。

```
// Register the device to Push Notifications service.
push.registerDeviceToken("deviceToken", WithUserId: "userId")  { (response, statusCode, error) -> Void in
if error.isEmpty {

    print( "Response during device registration : \(response)")

        print( "status code during device registration : \(statusCode)")

    }  else {
print( "Error during device registration \(error) ")
    }
}
```

**userId** 

プッシュ通知への登録を行うための固有のユーザー ID 値を渡します。


# ユーザー ID ベースの通知の使用
{: #using_userid}


ユーザー ID ベースの通知は、特定のユーザーをターゲットとする通知メッセージです。1 つのユーザーで複数のデバイスを登録できます。以下の手順では、ユーザー ID ベースの通知の送信方法を説明します。 

1. **「Push Notification」**ダッシュボードで、**「通知」**タブをクリックします。
1. ユーザー ID ベースの通知を送信するために、**「UserId」**オプションを選択します。
1. **「ユーザー ID の検索 (Search UserId)」**フィールドで、使用するユーザー ID を検索し、**「+ 追加 (+Add)」**ボタンをクリックします。![通知画面](images/tag_notification.jpg)
1. **「メッセージ・テキスト (Message Text)」**フィールドに、通知で送信するテキストを入力します。
1. **「送信」**ボタンをクリックします。
