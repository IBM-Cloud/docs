---

copyright:
 years: 2015, 2016

---

# Android の通知の保留
{: #hold-notifications-android}
最終更新日: 2016 年 10 月 17 日
{: .last-updated}

アプリケーションがバックグラウンドになる場合、アプリケーションに送信される通知を{{site.data.keyword.mobilepushshort}}サービスが保留するようにすることが必要な場合があります。通知を保留するには、{{site.data.keyword.mobilepushshort}}を処理しているアクティビティーの onPause() メソッドで hold() メソッドを呼び出します。

```
	@Override
	protected void onPause() {
    super.onPause();
    if (push != null) {
        push.hold();
    }
	} 
```
	{: codeblock}
