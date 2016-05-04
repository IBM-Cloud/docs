---

copyright:
 years: 2015, 2016

---

# Holding notifications for Android
{: #hold-notifications-android}

When your application goes into background, you probably want Push to hold back notifications that are sent to your application. To hold notifications, call the hold() method in the onPause() method of the activity that is handling push notifications.

```
@Override
protected void onPause() {
    super.onPause();

    if (push != null) {
        push.hold();
    }
} 
```