---

copyright:
 years: 2015, 2016

---

# Holding notifications for Android
{: #hold-notifications-android}
Last updated: 14 June 2016
{: .last-updated}

When your application goes into background, you might want the Push notification service to retain the notifications that are sent to your application. To hold notifications, call the hold() method in the onPause() method of the activity that is handling push notifications.

```
@Override
protected void onPause() {
    super.onPause();

    if (push != null) {
        push.hold();
    }
} 
```