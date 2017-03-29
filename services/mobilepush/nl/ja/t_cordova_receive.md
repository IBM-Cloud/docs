---

copyright:
 years: 2015, 2016

---

# デバイスでのプッシュ通知の受け取り
{: #cordova_receive}

デバイスでプッシュ通知を受け取るには、以下のコード・スニペットをコピーして貼り付けます。


##JavaScript

以下の JavaScript コード・スニペットを Cordova アプリケーションの Web パーツに追加します。



```
var notification = function(notification){
    // notification is a JSON object.
    alert(notification.message);
};
MFPPush.registerNotificationsCallback(notification);
```

##Android 通知プロパティー

次のセクションに、Android の通知プロパティーをリストします。

* message - プッシュ通知メッセージ
* payload - 通知ペイロードを含む JSON オブジェクト


##iOS 通知プロパティー

次のセクションに、iOS の通知プロパティーをリストします。

* message - プッシュ通知メッセージ
* payload - 通知ペイロードを含む JSON オブジェクト。
action-loc-key - このストリングは、現行ローカリゼーションにおいて、「View」の代わりに右ボタンのタイトルに使用されるローカライズされたストリングを取得するためのキーとして使用されます。
* badge - アプリ・アイコンのバッジとして表示する数。このプロパティーがないと、バッジは変更されません。バッジを削除するには、このプロパティーの値を 0 に設定します。
* sound - アプリ・バンドル内、またはアプリ・データ・コンテナーの Library/Sounds フォルダー内にある音声ファイルの名前。


##Objective-C

アプリケーション代行クラスに次の Objective-C コード・スニペットを追加します。

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

アプリケーション代行クラスに次の Swift コード・スニペットを追加します。

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
次のステップ。[基本プッシュ通知の送信](t_send_push_notifications.html)を行います。
