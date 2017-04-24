---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-24"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Making a network request
{: #sdk-network-request}

You can also use the `BMSCore` SDK to make network requests to any resource.

## Android
{: #request-android}

1. Make sure you have [imported the Client SDK and initialized it](/docs/mobile/sdk_BMSClient.html#init-BMSClient-android) in your Android application. 
	
2. Make a network request.

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

1. Make sure you have [imported the Client SDK and initialized it](/docs/mobile/sdk_BMSClient.html#init-BMSClient-ios) in your iOS application.

2. Create a network request.

	### Swift 3.0
	{: #ios-swift3 notoc}
	
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
 
	### Swift 2.2
	{: #ios-swift22 notoc}
	
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

The `Request` class is a simple way to make an HTTP request and get the response after the request is completed. If you want more flexibility and control than what you can get from the `Request` class, you can use the `BMSURLSession` class. Some features of the `BMSURLSession` class include monitoring progress of uploads, and pausing or canceling requests. To get the responses, you have the option to choose either completion handlers or delegates.

The `BMSURLSession` class is available for iOS only.

For complete usage examples, see the `BMSCore` GitHub [README](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core).


## Cordova
{: #request-cordova}

1. Make sure you have [imported the Client SDK and initialized it](/docs/mobile/sdk_BMSClient.html#init-BMSClient-cordova) in your Cordova application.

2. Create a network request.

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

