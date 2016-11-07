---

copyright:
 years: 2015, 2016

---

# 対話式通知
{: #interactive-notifications}
最終更新日: 2016 年 10 月 17 日
{: .last-updated}

対話式通知を使用すると、ユーザーは通知が到着したときにアプリケーションを開かずにアクションを取ることができます。対話式通知が到着すると、デバイスは通知メッセージとともにアクション・ボタンを表示します。対話式通知は、バージョン 8 以降の iOS デバイスでサポートされています。対話式通知が iOS 8 より低いバージョンの iOS デバイスに送信された場合、通知アクションは表示されません。

##対話式{{site.data.keyword.mobilepushshort}}の送信


対話式通知は、Push ダッシュボードを使用するか、[REST API 資料](t_restapi.html)を参照して、送信できます。

Push コンソールから、以下のようにします。 

1. Push ダッシュボードの通知タブの下で、**「通知の送信」**をクリックします。 
2. 通知の受信側を選択して、**「次へ」**をクリックします。 
3. 「通知の作成」ページで、「タイプ」を「デフォルト」または「混合」のいずれかに設定し、「詳細オプション」タブの下で「カテゴリー」値を指定することで、対話式プッシュを送信できます。クライアント上でカテゴリー値を構成するには、ネイティブ iOS アプリケーション・セクションで**「対話式{{site.data.keyword.mobilepushshort}}の処理 (Handling interactive {{site.data.keyword.mobilepushshort}})」**にチェック・マークを付けます。

## iOS アプリケーションでの対話式{{site.data.keyword.mobilepushshort}}の処理

対話式通知を受け取るには、以下の手順を行います。

1. リモート通知の受信時にバックグラウンド・タスクを実行するアプリケーション機能を使用可能にします。このステップは、アクションの一部がバックグラウンド対応の場合に必要です。
1. AppDelegate (アプリケーション: didRegisterForRemoteNotificationsWithDeviceTokenapplication:) で、`WLPush Object` 上の `deviceToken` を設定する前に、カテゴリーを設定します。
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
	{: codeblock}

1. AppDelegate に、新規コールバック・メソッドを実装します。
	```
	 -(void)application:(UIApplication *)application handleActionWithIdentifier:(NSString *)identifier forRemoteNotification:(NSDictionary *)userInfo completionHandler:(void (ˆ)())completionHandler
```
	{: codeblock} 
5. ユーザーがアクション・ボタンをクリックすると、この新しいコールバック・メソッドが呼び出されます。このメソッドの実装では、指定の ID に関連付けられたタスクを行い、`completionHandler` パラメーター内のブロックを実行する必要があります。
