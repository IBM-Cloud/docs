---

copyright:
 years: 2015, 2016

---

# 针对 Android 的暂停通知
{: #hold-notifications-android}
*上次更新时间：2016 年 6 月 14 日*
{: .last-updated}

应用程序转入后台运行时，您可能希望 Push Notifications 服务暂停发送给应用程序的通知。要暂停通知，请调用处理推送通知的活动的 onPause() 方法中的 hold() 方法。

```
@Override
protected void onPause() {super.onPause();
if (push != null) {
push.hold();
    }
} 
```
