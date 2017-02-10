---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Web フックのイベント・ベースの通知の使用可能化
{: #tag_based_notifications}
最終更新日: 2017 年 1 月 16 日
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

Web フックについて詳しくは、[IBM Push Notifications REST API ![外部リンク・アイコン](../../icons/launch-glyph.svg "External link icon")](https://mobile.{DomainName}/imfpush/#/webhooks "External link icon"){: new_window}を参照してください。
