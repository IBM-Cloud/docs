---
copyright:
  years: 2015, 2016
---
# IMFURLProtocol in iOS-Anwendungen verwenden
{: #imfurl}
In erweiterten Szenarios ist es vielleicht nicht möglich, die Klasse `IMFResourceRequest` zum Senden von Anforderungen an geschützte Ressourcen zu senden. Dies ist zum Beispiel der Fall, wenn eine Anforderung an eine geschützte Ressource durch einen Code eines Drittanbieters gesendet wird. Eine mögliche Lösung besteht in der Verwendung der API `IMFURLProtocol` in Kombination mit dem Standardaufruf `NSURLRequest (NSMutableURLRequest)`.

## Pod `IMFURLProtocol` installieren
{: #imfurl-pod}

Mithilfe von CocoaPods können Sie den Pod `IMFURLProtocol` installieren. Anschließend können Sie `IMFURLProtocol.h` in Ihrem iOS-Projekt referenzieren.

## Anforderungen mit der API IMFURLProtocol senden
{: #imfurl-send}

1. Importieren Sie die Datei `IMFURLProtocol.h` in die Klasse, die zum Senden der Anforderung verwendet wird.
2. Implementieren Sie die API `NSURLConnectionDataDelegate` in einer Klasse, die als Delegat an die Klasse `NSURLConnection` übergeben wird.
3. Registrieren Sie eine Instanz von `IMFURLProtocol` mit der Methode `IMFURLProtocol:registerIMFURLProtocol`.
4. Registrieren Sie den Pfad der geschützten Ressourcen mit der Methode `IMFURLProtocol:registerProtectedResourceWithPath`.
5. Erstellen Sie eine Anforderung `NSMutableURLRequest` und legen Sie die zugehörigen Eigenschaften wie für eine reguläre Anforderung an eine Ressource erforderlich fest.
6. Richten Sie die Klasse `NSURLConnection` mit der Anforderung und dem Delegat ein, die in den vorherigen Schritten erstellt wurden, und senden Sie sie mit `NSURLConnection:start`.
7. Die Antwort wird durch ein Delegat `NSURLConnectionDataDelegate` verarbeitet.

## Beispielcode
{: #imfurl-sample}

Dieses Beispiel zeigt, wie `IMFURLProtocol` registriert und eine Standardanforderung an eine geschützte Ressource gesendet wird.

### Schritt 1: Protokollimplementierung hinzufügen und Antwort verarbeiten
{: #imfurl-sample1}
```Swift
import Foundation

class ViewController : UIViewController, NSURLConnectionDataDelegate {

	func connection(connection: NSURLConnection, didReceiveResponse response: NSURLResponse) {

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

### Schritt 2: Klasse IMFURLProtocol registrieren und Pfad zu geschützter Ressource definieren
{: #imfurl-sample2}

```Swift
let URL_RESOURCE = "http://myapp.mybluemix.net/protectedResource"

@IBAction func onSendURLProtocol(sender: AnyObject) {

	IMFURLProtocol.sharedInstance().registerIMFURLProtocol()
	IMFURLProtocol.sharedInstance().registerProtectedResourceWithPath(URL_RESOURCE)

	// Standardanforderung senden
	var postRequest: NSMutableURLRequest = NSMutableURLRequest(URL: NSURL(string: URL_RESOURCE)!)
	postRequest.HTTPMethod = "GET"
	var theConnection: NSURLConnection = NSURLConnection(request: postRequest, delegate: self)!
	theConnection.start()
}
```
