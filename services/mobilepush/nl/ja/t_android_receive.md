---

copyright:
 years: 2015, 2016

---

# Android デバイスでのプッシュ通知の受け取り
{: #android_receive}

notificationListener オブジェクトを Push に登録するには、**MFPPush.listen()** メソッドを呼び出します。このメソッドは通常、プッシュ通知を処理しているアクティビティーの **onResume()** メソッドから呼び出されます。

1. notificationListener オブジェクトを Push に登録するには、**listen()** メソッドを呼び出します。このメソッドは通常、プッシュ通知を処理しているアクティビティーの **onResume()** メソッドから呼び出されます。

	```
	@Override
	protected void onResume(){
	   super.onResume();
	   if(push != null) {
	       push.listen(notificationListener);
	   }
	}
```
2. プロジェクトをビルドし、デバイスまたはエミュレーター上で実行します。register() メソッド内で応答リスナーに onSuccess() メソッドを呼び出す際に、デバイスが Push Notification Service に正常に登録されていることを確認します。この時点で、『基本プッシュ通知の送信』に説明されている方法でメッセージを送信できます。
3. デバイスが通知を受信していることを確認します。アプリケーションがフォアグラウンドにある場合は、通知は **MFPPushNotificationListener** により処理されます。アプリケーションがバックグラウンドにある場合は、メッセージが通知バーに表示されます。

