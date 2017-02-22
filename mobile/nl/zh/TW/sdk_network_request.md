---

copyright:
  years: 2016, 2017
lastupdated: "2016-11-30"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 提出網路要求
{: #sdk-network-request}

您也可以使用 `BMSCore` SDK 對任何資源提出網路要求。

## Android
{: #request-android}

1. 確定您已在 Android 應用程式中[匯入用戶端 SDK 並起始設定它](/docs/mobile/sdk_BMSClient.html#init-BMSClient-android)。 
	
2. 提出網路要求。

	```
	public void makeGetCall() {
		Thread thread = new Thread(new Runnable() {
			@Override
			public void run() {
				try  {
					Request request = new Request("http://httpbin.org/get", "GET");
					request.send(null, null);
				} catch (Exception e) {
					// Handle failure here.
				}
			}
		});
		thread.start();
	}
	```
	{: codeblock}

## iOS
{: #request-ios}

1. 確定您已在 iOS 應用程式中[匯入用戶端 SDK 並起始設定它](/docs/mobile/sdk_BMSClient.html#init-BMSClient-ios)。

2. 建立網路要求。

	#### Swift 3.0
	{: #ios-swift3}
	
	```Swift
	 	// Make a network request
		let customResourceURL = "<your resource URL>"
		let request = Request(url: customResourceURL, method: HttpMethod.GET)
	
		let callBack:BMSCompletionHandler = {(response: Response?, error: Error?) in
	   	if error == nil {
	       	    print ("response:\(response?.responseText), no error")
	    	  } else {
	       	    print ("error: \(error)")
	    	}
		}
		request.send(completionHandler: callBack)
	```
	{: codeblock}
 
	#### Swift 2.2
	{: #ios-swift22}
	
	```Swift
	 	// Make a network request
		let customResourceURL = "<your resource URL>"
		let request = Request(url: customResourceURL, method: HttpMethod.GET)
	
		let callBack:BMSCompletionHandler = {(response: Response?, error: NSError?) in
	   	if error == nil {
	       	    print ("response:\(response?.responseText), no error")
	    	  } else {
	       	    print ("error: \(error)")
	    	}
		}
		request.send(completionHandler: callBack)
	```
	{: codeblock}

`Request` 類別是提出 HTTP 要求並在要求完成後取得回應的簡單方法。如果您想要得到比 `Request` 類別更多的彈性與控制，可以使用 `BMSURLSession` 類別。`BMSURLSession` 類別部分特性包括監視上傳的進度，以及暫停或取消要求。若要取得回應，您可以選擇完成處理程式或委派。

`BMSURLSession` 類別僅適用於 iOS。如需 `BMSURLSession` 的相關資訊，請參閱 `BMSCore` SDK [README](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core)。


## Cordova
{: #request-cordova}

1. 確定您已在 Cordova 應用程式中[匯入用戶端 SDK 並起始設定它](/docs/mobile/sdk_BMSClient.html#init-BMSClient-cordova)。

2. 建立網路要求。

	```
	var success = function(data) {
		console.log("success", data);
	}
	var failure = function(error)
		{console.log("failure", error);
	}
	var request = new BMSRequest("<your application route>", BMSRequest.GET);
	request.send(success, failure);
	```
	{: codeblock}


# 相關鏈結
{: #rellinks}

## 相關鏈結
{: #general}

* [BMSCore Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}
* [BMSCore iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window}
* [BMSCore Cordova 外掛程式](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}
