---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 네트워크 요청 작성
{: #sdk-network-request}

또한 자원에 대한 네트워크 요청을 작성하기 위해 `BMSCore` SDK를 사용할 수도 있습니다.

## Android
{: #request-android}

1. Android 애플리케이션에서 [클라이언트 SDK를 가져오고 이를 초기화](/docs/mobile/sdk_BMSClient.html#init-BMSClient-android)했는지 확인하십시오. 
	
2. 네트워크 요청을 작성하십시오. 

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

1. iOS 애플리케이션에서 [클라이언트 SDK를 가져오고 이를 초기화](/docs/mobile/sdk_BMSClient.html#init-BMSClient-ios)했는지 확인하십시오.

2. 네트워크 요청을 작성하십시오. 

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

`Request` 클래스는 요청을 작성하고 요청이 완료된 후에 응답을 가져오는 간단한 방법입니다. `Request` 클래스보다 더 많은 유연성과 제어 기능을 원하는 경우, `BMSURLSession` 클래스를 사용할 수 있습니다. `BMSURLSession` 클래스의 일부 기능으로는 업로드 프로세스 모니터링과 요청 일시정지 또는 취소가 있습니다. 응답을 가져오는 옵션으로 완료 핸들러 또는 위임 중 하나를 선택할 수 있습니다.

`BMSURLSession` 클래스는 iOS용으로만 사용 가능합니다. `BMSURLSession`에 대한 자세한 정보는 `BMSCore` SDK [README](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core)를 참조하십시오.


## Cordova
{: #request-cordova}

1. Cordova 애플리케이션에서 [클라이언트 SDK를 가져오고 이를 초기화](/docs/mobile/sdk_BMSClient.html#init-BMSClient-cordova)했는지 확인하십시오.

2. 네트워크 요청을 작성하십시오. 

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


# 관련 링크
{: #rellinks notoc}

## 관련 링크
{: #general notoc}

* [BMSCore Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}
* [BMSCore iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window}
* [BMSCore Cordova 플러그인](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}
