---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 保存 Android 的通知
{: #hold-notifications-android}
前次更新：2017 年 1 月 11 日
{: .last-updated}

在應用程式進入背景時，您可能會想要 {{site.data.keyword.mobilepushshort}} Service 保留傳送給應用程式的通知。若要保留通知，請在處理 {{site.data.keyword.mobilepushshort}} 之活動的 onPause() 方法中呼叫 hold() 方法。

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
