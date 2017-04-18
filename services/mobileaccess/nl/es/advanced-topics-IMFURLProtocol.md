---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-27"  

---
# Envío de solicitudes con IMFURLProtocol
{: #imfurl}

En algunas situaciones, es posible que no pueda utilizar la clase `IMFResourceRequest` para el envío de solicitudes a recursos protegidos por {{site.data.keyword.amafull}}, como por ejemplo cuando algún código de terceros envía una solicitud a un recurso protegido. Una posible solución es utilizar la API `IMFURLProtocol`, junto con la llamada estándar `NSURLRequest (NSMutableURLRequest)`.

**Nota:** La API `IMFURLProtocol` solo está disponible desde el SDK Objective-C de {{site.data.keyword.amashort}}.

## Instalación de pod `IMFURLProtocol`
{: #imfurl-pod}

Utilice CocoaPods para instalar pod `IMFURLProtocol`. 

Edite el archivo Podfile y añada la siguiente línea y ejecute:
```Bash
pod 'IMFURLProtocol'
```

Después, haga referencia a `IMFURLProtocol.h` desde el proyecto de iOS.

## Envío de solicitudes con la API `IMFURLProtocol`
{: #imfurl-send}

1. Importe el archivo `IMFURLProtocol.h` a la clase que esté utilizando para enviar la solicitud.
2. Implemente la API `NSURLConnectionDataDelegate` en una clase que se haya pasado como delegada de una clase `NSURLConnection`.
3. Registre una instancia de `IMFURLProtocol` con el método `IMFURLProtocol:registerIMFURLProtocol`.
4. Registre la vía de acceso al recurso protegido con el método `IMFURLProtocol:registerProtectedResourceWithPath`.
5. Cree una solicitud `NSMutableURLRequest` y defina las propiedades como necesarias para una solicitud estándar a un recurso.
6. Configure `NSURLConnection` con la solicitud y el delegado que se creó en los pasos anteriores y envíelos utilizando `NSURLConnection:start`.
7. La respuesta se procesa mediante un `NSURLConnectionDataDelegate`.

## Código de ejemplo
{: #imfurl-sample}

Este ejemplo muestra cómo registrar `IMFURLProtocol` y cómo enviar una solicitud estándar a un recurso protegido.

### Paso 1: añada la implementación del protocolo y procese la respuesta.
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

### Paso 2: registre la clase IMFURLProtocol y defina una vía de acceso al recurso protegido.
{: #imfurl-sample2}

```Swift
let URL_RESOURCE = "http://myapp.mybluemix.net/protectedResource"

@IBAction func onSendURLProtocol(sender: AnyObject) {

	IMFURLProtocol.sharedInstance().registerIMFURLProtocol()
	IMFURLProtocol.sharedInstance().registerProtectedResourceWithPath(URL_RESOURCE)

	// Envía una solicitud estándar
	var postRequest: NSMutableURLRequest = NSMutableURLRequest(URL: NSURL(string: URL_RESOURCE)!)
	postRequest.HTTPMethod = "GET"
	var theConnection: NSURLConnection = NSURLConnection(request: postRequest, delegate: self)!
	theConnection.start()
}
```
