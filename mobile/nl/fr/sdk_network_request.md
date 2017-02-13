---

copyright:
  years: 2016, 2017
lastupdated: "2016-11-30"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Soumission d'une demande réseau
{: #sdk-network-request}

Vous pouvez également utiliser le SDK `BMSCore` pour effectuer des demandes réseau à n'importe quelle ressource.

## Android
{: #request-android}

1. Vérifiez que vous avez bien [importé et initialisé le SDK client](/docs/mobile/sdk_BMSClient.html#init-BMSClient-android) dans votre application Android. 
	
2. Effectuez une demande réseau.

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

1. Vérifiez que vous avez bien [importé et initialisé le SDK client](/docs/mobile/sdk_BMSClient.html#init-BMSClient-ios) dans votre
application iOS.

2. Créez une demande réseau.

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

La classe `Request` est un moyen simple d'effectuer une demande HTTP et d'obtenir une réponse une fois la demande effectuée. Si vous avez
besoin de plus de souplesse et de contrôle que ceux offerts par la classe `Request`, vous pouvez utiliser la classe `BMSURLSession`. Parmi
les fonctionnalités de la classe `BMSURLSession`, on dénote le suivi de la progression des téléchargements et la mise en pause ou l'annulation des
demandes. Pour obtenir les réponses, vous pouvez choisir des gestionnaires d'exécution ou des délégués.

La classe `BMSURLSession` n'est disponible que pour iOS. Pour plus d'informations
sur `BMSURLSession`, reportez-vous au fichier [README](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core) du
SDK `BMSCore`.


## Cordova
{: #request-cordova}

1. Vérifiez que vous avez bien [importé et initialisé le SDK client](/docs/mobile/sdk_BMSClient.html#init-BMSClient-cordova) dans votre
application Cordova.

2. Créez une demande réseau.

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


# Liens connexes
{: #rellinks}

## Liens connexes
{: #general}

* [BMSCore Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}
* [BMSCore iOS SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window}
* [BMSCore Cordova Plugin](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}
