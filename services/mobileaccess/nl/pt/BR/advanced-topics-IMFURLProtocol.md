---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-27"  

---
# Enviando solicitações com IMFURLProtocol
{: #imfurl}

Em alguns casos, talvez você não consiga usar a classe
`IMFResourceRequest` para enviar solicitações a recursos protegidos pelo
{{site.data.keyword.amafull}}, como quando uma solicitação para um recurso
protegido é enviada por algum código de terceiros. Uma solução possível é usar a API `IMFURLProtocol`, junto com a chamada `NSURLRequest (NSMutableURLRequest)` padrão.

**Nota:** a API `IMFURLProtocol` está disponível somente a partir do {{site.data.keyword.amashort}} Objective-C SDK.

## Instalando a impressão on demand `IMFURLProtocol`
{: #imfurl-pod}

Use o CocoaPods para instalar o pod `IMFURLProtocol`. 

Edite o arquivo Podfile e inclua a linha a seguir e execute:
```Bash
pod 'IMFURLProtocol'
```

Em seguida, faça referência a `IMFURLProtocol.h` a partir de seu projeto iOS.

## Enviando solicitações com a API `IMFURLProtocol`
{: #imfurl-send}

1. Importe o arquivo `IMFURLProtocol.h` na classe que está sendo usada para enviar a solicitação.
2. Implemente a API `NSURLConnectionDataDelegate` em uma classe que é passada como um delegado para a classe `NSURLConnection`.
3. Registre uma instância de `IMFURLProtocol` com o método `IMFURLProtocol:registerIMFURLProtocol`.
4. Registre o caminho de recurso protegido com o método `IMFURLProtocol:registerProtectedResourceWithPath`.
5. Crie uma `NSMutableURLRequest` e configure suas propriedades conforme necessário para uma solicitação regular para um recurso.
6. Configure `NSURLConnection` com a solicitação e o delegado que foram criados nas etapas anteriores e envie-o usando `NSURLConnection:start`.
7. A resposta é processada por um `NSURLConnectionDataDelegate`.

## Código de Amostra
{: #imfurl-sample}

Este exemplo mostra como registrar `IMFURLProtocol` e enviar uma solicitação padrão para recurso protegido.

### Etapa 1: Inclua a implementação do protocolo e processe a resposta
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

### Etapa 2: Registre a classe IMFURLProtocol e defina um caminho para o recurso protegido
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
