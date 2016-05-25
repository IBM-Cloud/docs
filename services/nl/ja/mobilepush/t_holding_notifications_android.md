---

copyright:
 years: 2015, 2016

---

# Android の通知の保留
{: #hold-notifications-android}

アプリケーションがバックグラウンドになる場合、恐らく、アプリケーションに送信された通知を Push が保留するようにする必要があります。通知を保留するには、プッシュ通知を処理しているアクティビティーの onPause() メソッドで hold() メソッドを呼び出します。

```
@Override
protected void onPause() {
    super.onPause();


    if (push != null) {
push.hold();
    }
} 
```
