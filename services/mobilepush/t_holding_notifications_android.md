---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Holding notifications for Android
{: #hold-notifications-android}
Last updated: 06 December 2016
{: .last-updated}

When your application goes into background, you might want {{site.data.keyword.mobilepushshort}} service to retain the notifications that are sent to your application. To hold notifications, call the hold() method in the onPause() method of the activity that is handling {{site.data.keyword.mobilepushshort}}.

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