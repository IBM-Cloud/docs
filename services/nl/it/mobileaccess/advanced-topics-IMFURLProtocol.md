---
copyright:
  years: 2015, 2016
---
# Utilizzo di IMFURLProtocol nelle applicazioni iOS
{: #imfurl}
Nei casi avanzati, potresti non essere in grado di utilizzare la classe `IMFResourceRequest` per inviare richieste alle risorse protette, come ad esempio quando una richiesta a una risorsa protetta viene inviata da codice di terze parti. Una possibile soluzione consiste nell'utilizzare l'API `IMFURLProtocol`, insieme alla chiamata `NSURLRequest (NSMutableURLRequest)` standard.

## Installazione del pod `IMFURLProtocol`
{: #imfurl-pod}

Puoi utilizzare CocoaPods per installare il pod `IMFURLProtocol`. Puoi quindi fare riferimento a `IMFURLProtocol.h` dal tuo progetto iOS.

## Invio di richieste con l'API IMFURLProtocol
{: #imfurl-send}

1. Importa il file `IMFURLProtocol.h` nella classe che stai utilizzando per inviare la richiesta.
2. Implementa l'API `NSURLConnectionDataDelegate` in una classe passata come un delegato alla classe `NSURLConnection`.
3. Registra un'istanza di `IMFURLProtocol` con il metodo `IMFURLProtocol:registerIMFURLProtocol`.
4. Registra il percorso risorsa protetto con il metodo `IMFURLProtocol:registerProtectedResourceWithPath`.
5. Crea un `NSMutableURLRequest` e impostane le proprietà come richiesto per una richiesta regolare a una risorsa.
6. Configura `NSURLConnection` con la richiesta e il delegato creati nei passi precedenti e invialo utilizzando `NSURLConnection:start`.
7. La risposta viene elaborata da un `NSURLConnectionDataDelegate`.

## Codice di esempio
{: #imfurl-sample}

Questo esempio mostra come registrare `IMFURLProtocol` e inviare una richiesta standard a una risorsa protetta.

### Fase 1: aggiungi l'implementazione del protocollo ed elabora la risposta
{: #imfurl-sample1}
```Swift
import Foundation

class ViewController : UIViewController, NSURLConnectionDataDelegate {

	func connection(connection: NSURLConnection,
								didReceiveResponse response: NSURLResponse) {

		println("\(response.description)")
	}

	func connection(connection: NSURLConnection, didReceiveData data: NSData) {
		var text = NSString(data: data, encoding: NSUTF8StringEncoding)
		println("\(text)")
	}

	func connection(connection: NSURLConnection, didFailWithError error: NSError) {
		println("\(error.description)")
	}
}
```

### Passo 2: registra la classe IMFURLProtocol e definisci un percorso alla risorsa protetta
{: #imfurl-sample2}

```Swift
let URL_RESOURCE = "http://myapp.mybluemix.net/protectedResource"

@IBAction func onSendURLProtocol(sender: AnyObject) {

	IMFURLProtocol.sharedInstance().registerIMFURLProtocol()
	IMFURLProtocol.sharedInstance().registerProtectedResourceWithPath(URL_RESOURCE)

	// Invia una richiesta standard
	var postRequest: NSMutableURLRequest = NSMutableURLRequest(URL: NSURL(string: URL_RESOURCE)!)
	postRequest.HTTPMethod = "GET"
	var theConnection: NSURLConnection = NSURLConnection(request: postRequest, delegate: self)!
	theConnection.start()
}
```
