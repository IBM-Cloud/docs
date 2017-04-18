---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Fazendo uma solicitação de rede
{: #sdk-network-request}

Também é possível usar o kit de desenvolvimento de software (SDK) `BMSCore` para fazer
solicitações de rede para qualquer recurso.

## Android
{: #request-android}

1. Certifique-se de ter [importado o SDK do Cliente e de tê-lo inicializado](/docs/mobile/sdk_BMSClient.html#init-BMSClient-android) em seu aplicativo Android. 
	
2. Faça uma solicitação de rede.

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

1. Certifique-se de ter [importado o SDK do Cliente e de tê-lo inicializado](/docs/mobile/sdk_BMSClient.html#init-BMSClient-ios) em seu aplicativo iOS.

2. Crie uma solicitação de rede.

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

A classe `Request` é uma maneira simples de fazer uma solicitação de HTTP e
de obter a resposta após a solicitação ser concluída. Se deseja mais flexibilidade e controle do que é
possível obter com a classe `Request`, a classe `BMSURLSession`
pode ser usada. Alguns recursos da classe `BMSURLSession` incluem monitoramento do
progresso de uploads e pausa ou cancelamento de solicitações. Para obter as respostas, há a opção de
escolher manipuladores ou delegados de conclusão.

A classe `BMSURLSession` está disponível somente para iOS. Para obter mais informações
sobre `BMSURLSession`, consulte o
[LEIA-ME](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core) do SDK
`BMSCore`.


## Cordova
{: #request-cordova}

1. Certifique-se de ter [importado o SDK do Cliente e de tê-lo inicializado](/docs/mobile/sdk_BMSClient.html#init-BMSClient-cordova) em seu aplicativo Cordova.

2. Crie uma solicitação de rede.

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


# Links relacionados
{: #rellinks notoc}

## Links relacionados
{: #general notoc}

* [SDK Android BMSCore](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}
* [SDK iOS BMSCore](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window}
* [Plug-in do Cordova BMSCore](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}
