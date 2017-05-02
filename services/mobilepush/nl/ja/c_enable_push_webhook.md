---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Web フックの使用可能化 
{: #tag_based_notifications}
最終更新日: 2017 年 3 月 1 日
{: .last-updated}


{{site.data.keyword.mobilepushshort}} サービスを使用して、変更された情報に関するアラートを受け取ることを選択できます。エンタープライズ情報に対する変更があると、イベントが作成されます。これらのイベントを Web フック・イベントとして登録することによって、通知を受け取ることができます。これらの Web フック・イベントは、アラートをトリガーします。 

Web フックは、デバイスの登録やタグへのサブスクライブなどのイベントによってトリガーされる、ユーザー定義のコールバックです。{{site.data.keyword.mobilepushshort}} サービス上で、以下の Web フック・イベントを登録できます。 

- **onDeviceRegister**: プッシュ用にデバイスが登録された場合に、Web フック・イベントがトリガーされます。
- **onDeviceUpdate**: 登録デバイスに関する情報が更新されたときに、Web フック・イベントがトリガーされます。
- **onDeviceUnregister**: デバイスが登録抹消されたときに、Web フック・イベントがトリガーされます。 
- **onSubscribe**: ユーザーがタグをサブスクライブしたときに、Web フック・イベントがトリガーされます。
- **onUnsubscribe**: ユーザーがタグをアンサブスクライブしたときに、Web フック・イベントがトリガーされます。
- **onNotificationSend**: 通知がディスパッチされた場合に、Web フック・イベントがトリガーされます。
- **onNotificationFailure**: 通知が失敗した場合に、Web フック・イベントがトリガーされます。


**注**: 通知のディスパッチはバッチ単位で行われます。1 回のメッセージのディスパッチに複数の Web フック・イベントが含まれることがあります。また、これには失敗と成功の両方が含まれている可能性があります。
Web フック・イベントは、ディスパッチされたメッセージと同じ messageID を持ちます。 

Web フックについて詳しくは、[IBM Push Notifications REST API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://mobile.{DomainName}/imfpush/#/webhooks){: new_window}を参照してください。

## Web フック・イベントに関するアラートの受信
{: #webhook_alert_event}

サブスクライバーは、Web フック・イベントに関するアラートを JSON ファイルとして受け取ることを選択できます。イベント構造体とサンプル・ペイロードは以下のとおりです。

- デバイスの登録
	```
		{ type: 'onDeviceRegister',
		entity:
		{ id: 1,
		deviceId: 'device1',
		applicationId: 'app1',
		userId: 'user1',
		token: 'token1',
		platform: 'G' },
		applicationId: 'app1',
		eventTimeStamp: 1487523766958 }
	```
		{: codeblock}

- デバイスの登録抹消
	```
		{ type: 'onDeviceUnregister',
		entity:
		{ id: 1,
		deviceId: 'device1',
		applicationId: 'app1',
		userId: 'user1',
		token: 'token1',
		platform: 'G' },
		applicationId: 'app1',
		eventTimeStamp: 1487523841874 }
	```
		{: codeblock}

- タグへのサブスクライブ
	```
		{ type: 'onSubscribe',
		entity:
		{ device:
		{ id: 18,
		deviceId: 'device1',
		applicationId: 'app1',
		userId: 'user1',
		token: 'token1',
		platform: 'G' },
		tagName: 'tag1',
		deviceId: 'device1',
		subscriptionId: 'b0246677bfa655385fbc2b5532f6443f' },
		applicationId: 'app1',
		eventTimeStamp: 1487755527470 }
	```
		{: codeblock}

- タグのアンサブスクライブ
	```
		{ type: 'onUnsubscribe',
		entity:
		{ device:
		{ id: 18,
		deviceId: 'device1',
		applicationId: 'app1',
		userId: 'user1',
		token: 'token1',
		platform: 'G' },
		tagName: 'tag1',
		deviceId: 'device1',
		subscriptionId: 'b0246677bfa655385fbc2b5532f6443f' },
		applicationId: 'app1',
		eventTimeStamp: 1487755581059 }
	```
		{: codeblock}

- 通知の送信
	```
		{ type: 'onNotificationSent',
		entity:
		{ applicationId: 'app1',
		deviceIds:
		[ 'device1',
		'device2'],
		platform: 'A',
		msgStatus: 'dispatched',
		messageId: '55cb688' },
		applicationId: 'app1',
		eventTimeStamp: 1487524517353 }
	```
		{: codeblock}

- 通知失敗
	```
		{ type: 'onNotificationFailure',
		entity:
		{ applicationId: 'app1',
		deviceIds: [ 'device1' ],
		platform: 'G',
		msgStatus: 'failure',
		failureReason: 'InvalidRegistration',
		messageId: '55cb688' },
		applicationId: 'app1',
		eventTimeStamp: 1487524519453 }
	```
		{: codeblock}

