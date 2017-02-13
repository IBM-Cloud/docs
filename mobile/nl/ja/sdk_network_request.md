---

copyright:
  years: 2016, 2017
lastupdated: "2016-11-30"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# ネットワーク要求を行う
{: #sdk-network-request}

`BMSCore` SDK を使用して、任意のリソースにネットワーク要求を行うこともできます。

## Android
{: #request-android}

1. Android アプリケーションに [Client SDK をインポートして初期化](/docs/mobile/sdk_BMSClient.html#init-BMSClient-android)しておくようにしてください。 
	
2. ネットワーク要求を行います。

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

1. iOS アプリケーションに [Client SDK をインポートして初期化](/docs/mobile/sdk_BMSClient.html#init-BMSClient-ios)しておくようにしてください。

2. ネットワーク要求を作成します。

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

`Request` クラスは、HTTP 要求を行い、要求が完了した後に応答を取得するためのシンプルな方法です。`Request` クラスよりも高い柔軟性と制御性が必要な場合は、`BMSURLSession` クラスを使用できます。`BMSURLSession` クラスのフィーチャーとしては、アップロードの進行状態のモニター、および要求の一時停止やキャンセルなどがあります。応答を取得するには、完了ハンドラーか代行のいずれかを選択するというオプションがあります。

`BMSURLSession` クラスは iOS でのみ使用可能です。`BMSURLSession` について詳しくは、`BMSCore` SDK の [README](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core) を参照してください。


## Cordova
{: #request-cordova}

1. Cordova アプリケーションに [Client SDK をインポートして初期化](/docs/mobile/sdk_BMSClient.html#init-BMSClient-cordova)しておくようにしてください。

2. ネットワーク要求を作成します。

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


# 関連リンク
{: #rellinks}

## 関連リンク
{: #general}

* [BMSCore Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}
* [BMSCore iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window}
* [BMSCore Cordova Plugin](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}
