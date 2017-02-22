---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 针对 Android 的暂停通知
{: #hold-notifications-android}
上次更新时间：2017 年 1 月 11 日
{: .last-updated}

应用程序转入后台运行时，您可能希望 {{site.data.keyword.mobilepushshort}} 服务暂停发送给应用程序的通知。要暂停通知，请调用处理 {{site.data.keyword.mobilepushshort}} 的活动的 onPause() 方法中的 hold() 方法。

```
	@Override
protected void onPause() {super.onPause();
    if (push != null) {
        push.hold();
    }
} 
```
	{: codeblock}
