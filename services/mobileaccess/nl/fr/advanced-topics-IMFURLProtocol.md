---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-27"  

---
# Envoi de demandes avec IMFURLProtocol
{: #imfurl}

Dans certains cas, il peut être impossible d'utiliser la classe `IMFResourceRequest` pour envoyer des demandes à des ressources protégées par {{site.data.keyword.amafull}}, quand la demande est envoyée, par exemple, par un code provenant d'un éditeur tiers. Une solution consiste à utiliser l'API `IMFURLProtocol` avec l'appel standard `NSURLRequest (NSMutableURLRequest)`.

**Remarque :** L'API `IMFURLProtocol` n'est disponible que dans le SDK {{site.data.keyword.amashort}} Objective-C.

## Installation de la capsule `IMFURLProtocol`
{: #imfurl-pod}

Utilisez CocoaPods pour installer la nacelle `IMFURLProtocol`. 

Editez le fichier Podfile en lui ajoutant la ligne suivante et exécutez :
```Bash
pod 'IMFURLProtocol'
```

Référencez ensuite `IMFURLProtocol.h` depuis votre projet iOS.

## Envoi de demandes avec l'API `IMFURLProtocol`
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
