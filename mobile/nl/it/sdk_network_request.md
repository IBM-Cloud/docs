---

copyright:
  years: 2016, 2017
lastupdated: "2016-11-30"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Effettuazione di una richiesta di rete
{: #sdk-network-request}

Puoi utilizzare l'SDK `BMSCore` per effettuare richieste di rete a qualsiasi risorsa.

## Android
{: #request-android}

1. Assicurati di aver [importato e inizializzato l'SDK Client](/docs/mobile/sdk_BMSClient.html#init-BMSClient-android) nella tua applicazione Android. 
	
2. Effettua una richiesta di rete.

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

1. Assicurati di aver [importato e inizializzato l'SDK Client](/docs/mobile/sdk_BMSClient.html#init-BMSClient-ios) nella tua applicazione iOS.

2. Crea una richiesta di rete.

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

La classe `Request` rappresenta un metodo semplice per effettuare una richiesta HTTP e ottenere la risposta al completamento della richiesta. Se vuoi più flessibilità e controllo rispetto a quello ottenuto con `Request`, puoi utilizzare la classe `BMSURLSession`. Alcune funzioni della classe `BMSURLSession` comprendono il monitoraggio dell'avanzamento dei caricamenti e la messa in pausa o l'annullamento delle richieste. Per ottenere le risposte, hai la possibilità di scegliere i gestori o i delegati di completamento.

La classe `BMSURLSession` è disponibile solo per iOS. Per ulteriori informazioni su `BMSURLSession`, consulta il [README](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core) dell'SDK `BMSCore`.


## Cordova
{: #request-cordova}

1. Assicurati di aver [importato e inizializzato l'SDK Client](/docs/mobile/sdk_BMSClient.html#init-BMSClient-cordova) nella tua applicazione Cordova.

2. Crea una richiesta di rete.

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


# Link correlati
{: #rellinks}

## Link correlati
{: #general}

* [BMSCore Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}
* [BMSCore iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window}
* [BMSCore Cordova Plugin](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}
