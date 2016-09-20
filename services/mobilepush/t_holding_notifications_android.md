---

copyright:
 years: 2015, 2016

---

# Holding notifications for Android
{: #hold-notifications-android}
Last updated: 17 September 2016
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