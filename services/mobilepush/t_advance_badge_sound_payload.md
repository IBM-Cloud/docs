---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

#Enabling advanced push notifications
Last updated: 28 February 2017
{: .last-updated}

Configure an iOS badge, sound, additional JSON payload, actionable notifications, and holding notifications.

## Configure sound, and payload and iOS badge
{: #badge-sound-payload}

Configure an iOS badge, sound, and additional JSON payload.

1. On the {{site.data.keyword.mobilepushshort}} dashboard, go to the **Notifications** tab.
2. Go to the **Optional Fields** section to configure the {{site.data.keyword.mobilepushshort}} features. 
	- **Sound File** - Enter a string to point to the sound file in your mobile app. In the payload, specify the string name of the sound file to use.
	- **iOS Badge** - For iOS devices, the number to display as the badge of the app icon. If this property is absent, the badge is not changed. To remove the badge, set the value of this property to 0.
	
### Android
{: #badge-sound-payload_android}

Add your sound file in `res/raw` directory of your android application. While sending notification, add the sound file name in the sound field of {{site.data.keyword.mobilepushshort}}.

```
"settings":{
     "gcm":{
     "sound":"tt.wav",
  }
 }  
```
    {: codeblock}	
	
### iOS
{: #badge-sound-payload_ios}

```
"settings": {
     "apns" : {
      "badge": 10,
      "sound": "tt.wav",
  }
}
``` 
	{: codeblock}
		
**Additional Payload** - This payload can be any key-value pair and must be a JSON object that you want to send with the {{site.data.keyword.mobilepushshort}}.

```
{"key":"value", "key2":"value2"}
```
	{: codeblock}

## Holding Android notifications 
{: #hold-notifications-android}

When your application goes into background, you might want {{site.data.keyword.mobilepushshort}} to hold back notifications sent to your application. To hold notifications, call the hold() method in the onPause() method of the activity that is handling {{site.data.keyword.mobilepushshort}}.

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

    
