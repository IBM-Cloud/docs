---

copyright:
 years: 2015, 2016

---

# 対話式通知
{: #interactive-notifications}

対話式通知を使用すると、ユーザーは通知が到着したときにアプリケーションを開かずにアクションを取ることができます。対話式通知が到着すると、デバイスは通知メッセージとともにアクション・ボタンを表示します。対話式通知は、バージョン 8 以降の iOS デバイスでサポートされています。対話式通知が iOS 8 より低いバージョンの iOS デバイスに送信された場合、通知アクションは表示されません。

##対話式プッシュ通知の送信


対話式通知は、Push ダッシュボードを使用するか、REST API を使用して (REST API documentationREST API 資料を参照) 送信できます。

Push コンソールから、以下のようにします。 

Push ダッシュボードの通知タブの下で、「通知の送信 (Send Notification)」をクリックします。通知の受信側を選択して、「次へ」をクリックします。「通知の作成 (compose notification)」ページで、「タイプ」を「デフォルト」または「混合」のいずれかに設定し、「詳細オプション」タブの下で「カテゴリー」値を指定して、対話式プッシュを送信できます。クライアント上でカテゴリー値を構成するには、ネイティブ iOS アプリケーション・セクションで「対話式プッシュ通知の処理」を確認します。

## iOS アプリケーションでの対話式プッシュ通知の処理

対話式通知を受け取るには、以下のステップに従う必要があります。

1. リモート通知の受信時にバックグラウンド・タスクを実行するアプリケーション機能を使用可能にします。このステップは、アクションの一部がバックグラウンド対応の場合に必要です。
1. `AppDelegate (application: didRegisterForRemoteNotificationsWithDeviceTokenapplication:)` で、`WLPush Object` 上の `deviceToken` を設定する前に、カテゴリーを設定します。

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

1. AppDelegate に、新規コールバック・メソッドを実装します。

```
	-(void)application:(UIApplication *)application handleActionWithIdentifier:(NSString *)identifier forRemoteNotification:(NSDictionary *)userInfo completionHandler:(void (ˆ)())completionHandler
``` 

5. ユーザーがアクション・ボタンをクリックすると、この新しいコールバック・メソッドが呼び出されます。このメソッドの実装では、指定の識別子に関連付けられたアクションを実行し、`completionHandler` パラメーター内のブロックを実行する必要があります。
