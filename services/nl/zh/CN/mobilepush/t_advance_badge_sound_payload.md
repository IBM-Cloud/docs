---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
# 配置声音、有效内容和 iOS 角标

{: #badge-sound-payload}

配置 iOS 角标、声音和其他 JSON 有效内容。

1. 在 Push Notifications 仪表板上，转至**通知**选项卡。
2. 转至**可选字段**部分，以配置以下推送通知功能。

	a. **iOS 角标** - 对于 iOS 设备，要显示为应用程序图标角标的数字。如果缺少此属性，那么角标不会改变。要除去角标，请将此属性的值设置为 0。

	b. **声音文件** - 输入字符串，以指向移动应用程序中的声音文件。在有效内容中，指定要使用的声音文件的字符串名称。


	Android

	```
	"settings": {
"gcm" : { 
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
**其他有效内容** - 此有效内容可以是任何键/值对，但必须为要与推送通知一起发送的 JSON 对象。

	```
	{"key":"value", "key2":"value2"}```
