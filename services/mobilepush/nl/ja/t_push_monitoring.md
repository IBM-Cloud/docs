---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# プッシュ通知のモニター 
{: #monitor-notifications}
最終更新日: 2017 年 4 月 12 日
{: .last-updated}


IBM {{site.data.keyword.mobilepushshort}} サービスの機能が拡張され、ユーザー・データからグラフを生成することにより、プッシュのパフォーマンスをモニターできるようになりました。ユーティリティーを使用して、すべての送信プッシュ通知をリストするか、すべての登録デバイスをリストして、日次、週次、または月次ベースで情報を分析できます。

すべての送信通知のレポートを生成するには、[REST API](https://mobile.{DomainName}/imfpush/){: new_window} で Push Messages GET レポート・メソッドを使用します。 

![送信通知レポート](images/monitoring_messages.jpg)


すべての登録デバイスのレポートを生成するには、[REST API](https://mobile.{DomainName}/imfpush/){: new_window} で Push Device Registrations GET レポート・メソッドを使用します。

![登録デバイス・レポート](images/monitoring_devices.jpg)

Android SDK を更新して通知情報をモニターする方法については、[モバイル・デバイス用の通知の使用可能化](c_enable_push.html)にある『Android デバイスでのプッシュ通知のモニター』トピックを参照してください。


 
