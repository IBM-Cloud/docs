---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Realización de una solicitud de red
{: #sdk-network-request}

También puede utilizar el SDK `BMSCore` para realizar solicitudes de red a cualquier recurso.

## Android
{: #request-android}

1. Asegúrese de haber [importado e inicializado el SDK del cliente](/docs/mobile/sdk_BMSClient.html#init-BMSClient-android) en la aplicación Android. 
	
2. Realice una solicitud de red.

	```
	public void makeGetCall() {
		Thread thread = new Thread(new Runnable() {
			@Override
			public void run() {
				try  {
					Request request = new Request("http://httpbin.org/get", "GET");
					request.send(null, null);
				} catch (Exception e) {
					// Manejar aquí los errores.
				}
			}
		});
		thread.start();
	}
	```
	{: codeblock}

## iOS
{: #request-ios}

1. Asegúrese de haber [importado e inicializado el SDK de cliente](/docs/mobile/sdk_BMSClient.html#init-BMSClient-ios) en la aplicación iOS.

2. Cree una solicitud de red.

	### Swift 3.0
	{: #ios-swift3 notoc}
	
	```Swift
	 	// Realizar una solicitud de red
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
	 	// Realizar una solicitud de red
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

La clase `Request` ofrece un método sencillo para realizar una solicitud HTTP y obtener la respuesta una vez completada la solicitud. Si desea más flexibilidad y control del que puede obtener de la clase `Request`, puede utilizar la clase `BMSURLSession`. Algunas de las características de la clase `BMSURLSession` incluyen el progreso de supervisión de las cargas y la colocación en pausa o cancelación de solicitudes. Para obtener las respuestas, puede elegir manejadores de terminación o delegados.

La clase `BMSURLSession` solo está disponible para iOS. Para obtener más información sobre `BMSURLSession`, consulte los archivos [README](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core) del SDK de `BMSCore`.


## Cordova
{: #request-cordova}

1. Asegúrese de haber [importado e inicializado el SDK del cliente](/docs/mobile/sdk_BMSClient.html#init-BMSClient-cordova) en la aplicación Cordova.

2. Cree una solicitud de red.

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


# Enlaces relacionados
{: #rellinks notoc}

## Enlaces relacionados
{: #general notoc}

* [SDK de Android de BMSCore](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}
* [SDK de iOS de BMSCore](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window}
* [SDK de Cordova de BMSCore](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}
