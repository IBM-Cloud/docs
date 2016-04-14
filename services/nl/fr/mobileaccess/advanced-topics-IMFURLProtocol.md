---
copyright :
  années : 2015, 2016
---
# Utilisation d'IMFURLProtocol dans les applications iOS
{: #imfurl}
Dans certains scénarios avancés, il peut être impossible d'utiliser la classe `IMFResourceRequest` pour envoyer des demandes à des ressources protégées, par exemple lorsque la demande est envoyée par un code provenant d'un autre éditeur. Une solution consiste à utiliser l'API `IMFURLProtocol` avec l'appel standard `NSURLRequest (NSMutableURLRequest)`.

## Installation de la capsule `IMFURLProtocol`
{: #imfurl-pod}

Vous pouvez utiliser CocoaPods pour installer la capsule `IMFURLProtocol`. Puis, vous pouvez référencer `IMFURLProtocol.h` depuis votre projet iOS.

## Envoi de demandes à l'aide de l'API IMFURLProtocol
{: #imfurl-send}

1. Importez le fichier `IMFURLProtocol.h` dans la classe que vous utilisez pour envoyer la demande.
2. Implémentez l'API `NSURLConnectionDataDelegate` dans une classe qui est transmise en tant que délégué à la classe `NSURLConnection`.
3. Enregistrez une instance de `IMFURLProtocol` avec la méthode `IMFURLProtocol:registerIMFURLProtocol`.
4. Enregistrez le chemin de la ressource protégée avec la méthode `IMFURLProtocol:registerProtectedResourceWithPath`.
5. Créez une demande `NSMutableURLRequest` et définissez ses propriétés en fonction des besoins pour une demande
ordinaire envoyée à une ressource.
6. Configurez l'API `NSURLConnection` avec la demande et le délégué qui ont été créées aux étapes précédentes et
envoyez la demande avec `NSURLConnection:start`.
7. La réponse est traitée par `NSURLConnectionDataDelegate`.

## Exemple de code
{: #imfurl-sample}

Cet exemple montre comment enregistrer `IMFURLProtocol` et envoyer une demande standard à une ressource protégée.

### Etape 1 : Ajoutez l'implémentation du protocole et traitez la réponse
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

### Etape 2 : Enregistrez la classe IMFURLProtocol et définissez le chemin d'accès à la ressource protégée
{: #imfurl-sample2}

```Swift
let URL_RESOURCE = "http://myapp.mybluemix.net/protectedResource"

@IBAction func onSendURLProtocol(sender: AnyObject) {

	IMFURLProtocol.sharedInstance().registerIMFURLProtocol()
	IMFURLProtocol.sharedInstance().registerProtectedResourceWithPath(URL_RESOURCE)

	// Send a standard request
	var postRequest: NSMutableURLRequest = NSMutableURLRequest(URL: NSURL(string: URL_RESOURCE)!)
	postRequest.HTTPMethod = "GET"
	var theConnection: NSURLConnection = NSURLConnection(request: postRequest, delegate: self)!
	theConnection.start()
}
```
