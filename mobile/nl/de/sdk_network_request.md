---

copyright:
  years: 2016, 2017
lastupdated: "2016-11-30"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Netzanforderung erstellen
{: #sdk-network-request}

Sie können auch das `BMSCore`-SDK zum Erstellen von Netzanforderungen an beliebige Ressourcen verwenden.

## Android
{: #request-android}

1. Stellen Sie sicher, dass Sie in Ihrer Android-Anwendung [das Client-SDK importiert und initialisiert haben](/docs/mobile/sdk_BMSClient.html#init-BMSClient-android). 
	
2. Erstellen Sie eine Netzanforderung.

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

1. Stellen Sie sicher, dass Sie in Ihrer iOS-Anwendung [das Client-SDK importiert und initialisiert haben](/docs/mobile/sdk_BMSClient.html#init-BMSClient-ios).

2. Erstellen Sie eine Netzanforderung.

	#### Swift 3.0
	{: #ios-swift3}
	
	```Swift
	 	// Make a network request
		let customResourceURL = "<Ihre_ressourcen-URL>"
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
		let customResourceURL = "<Ihre_ressourcen-URL>"
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

Die Klasse `Request` ist eine einfache Möglichkeit zum Erstellen einer HTTP-Anforderung und zum Erhalten der Antwort nach der Durchführung der Anforderung. Wenn Sie größere Flexibilität und mehr Steuerungsmöglichkeiten wünschen als mit der Klasse `Request`, können Sie die Klasse `BMSURLSession` verwenden. Funktionen der Klasse `BMSURLSession` sind unter anderem das Überwachen des Verarbeitungsfortschritts beim Hochladen und das Anhalten oder Abbrechen von Anforderungen. Um die Antworten zu erhalten, können Sie entweder Completion-Handler oder Delegierte (Delegates) auswählen.

Die Klasse `BMSURLSession` ist nur für iOS verfügbar. Weitere Informationen zu `BMSURLSession` finden Sie in der `BMSCore`-SDK-[README](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core).


## Cordova
{: #request-cordova}

1. Stellen Sie sicher, dass Sie in Ihrer Cordova-Anwendung [das Client-SDK importiert und initialisiert haben](/docs/mobile/sdk_BMSClient.html#init-BMSClient-cordova).

2. Erstellen Sie eine Netzanforderung.

	```
	var success = function(data) {
		console.log("success", data);
	}
	var failure = function(error)
		{console.log("failure", error);
	}
	var request = new BMSRequest("<Ihre_anwendungsroute>", BMSRequest.GET);
	request.send(success, failure);
	```
	{: codeblock}


# Zugehörige Links
{: #rellinks}

## Zugehörige Links
{: #general}

* [BMSCore-Android-SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}
* [BMSCore-iOS-SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window}
* [BMSCore-Cordova-Plug-in](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}
