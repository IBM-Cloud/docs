---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
# Configure badge, sound, and payload and iOS badge

{: #badge-sound-payload}

Configure an iOS badge, sound and additional JSON payload.

1. On the Push Notifications dashboard, go to the **Notifications** tab.
2. Go to the **Optional Fields** section to configure the following push notification features. ios badge, sound, and additonal payload.
       
	a. **iOS Badge** - For iOS devices, the number to display as the badge of the app icon. If this property is absent, the badge is not changed. To remove the badge, set the value of this property to 0.
       
	b. **Sound File** - Enter a string to point to the sound file in your mobile app. In the payload, specify the string name of the sound file to use.
	
	
	Android
	
	```
	"settings":{
	     "gcm":{ 
	     "sound":"tt.wav", 
	  }
	 }  
	```
	
	iOS
		
	```
	"settings": {
	     "apns" : { 
	      "badge": 10,
	      "sound": "tt.wav", 
	  }
	} 
	``` 		
**Additional Payload** - This payload can be any key-value pair and must be a JSON object that you want to send with the push notification.
	
	```
	{"key":"value", "key2":"value2"}
	```

	