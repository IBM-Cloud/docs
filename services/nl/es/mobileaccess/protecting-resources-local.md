---

copyright:
  years: 2015, 2016

---

# Uso de {{site.data.keyword.amashort}} con un entorno de desarrollo local
{: #protecting-local}

*Última actualización: 17 de julio de 2016*
{: .last-updated}

Puede configurar su desarrollo local para que utilice el servicio de {{site.data.keyword.amashort}} que se ejecuta en {{site.data.keyword.Bluemix}}. Específicamente, puede desarrollar código de forma local utilizando el SDK del servidor de {{site.data.keyword.amashort}} y enviar solicitudes de {{site.data.keyword.amashort}} al servidor de desarrollo. Estas solicitudes las protegerá el servicio de {{site.data.keyword.amashort}} que se ejecuta en {{site.data.keyword.Bluemix}}.

## Configuración del SDK del servidor
{: #serversetup}

El SDK del servidor de {{site.data.keyword.amashort}} necesita que se definan dos variables de entorno. Cuando desarrolle código del lado del servidor en {{site.data.keyword.Bluemix_notm}}, la infraestructura de {{site.data.keyword.Bluemix_notm}} proporciona estas variables.

* `VCAP_SERVICES`: contiene información sobre servicios que están enlazados a la aplicación de fondo móvil.
* `VCAP_APPLICATION`: contiene información sobre la aplicación de fondo móvil.

Para utilizar {{site.data.keyword.amashort}} con un servidor de desarrollo local, debe añadir estas variables manualmente.

1. Abra el panel de control de {{site.data.keyword.Bluemix_notm}} de la aplicación de programa de fondo móvil protegida con el servicio de {{site.data.keyword.amashort}}.

1. Pulse **Opciones móviles** y copie el valor de **AppGUID**.

1. En el entorno de desarrollo local, defina la variable de entorno *VCAP_APPLICATION*. La variable debe contener un objeto JSON en serie con una sola propiedad.
```JavaScript
{
    application_id: "appGUID"
}
```
Sustituya la variable *appGUID* con el valor del campo **Opciones móviles** **AppGUID**.

1. Pulse **Mostrar credenciales** en el mosaico de servicios de {{site.data.keyword.amashort}} en la aplicación de fondo móvil en el panel de control de {{site.data.keyword.Bluemix_notm}}. Se muestra un objeto JSON con las credenciales de acceso que proporciona {{site.data.keyword.amashort}} a la aplicación de fondo móvil.

1. En el entorno de desarrollo local, defina la variable de entorno `VCAP_SERVICES`. El valor de esta variable debe ser un objeto JSON en serie que contenga las credenciales de {{site.data.keyword.amashort}}.  Consulte el ejemplo siguiente para obtener más información.

## Código del servidor de ejemplo
{: #local-dev-sample}

Para utilizar el servicio de {{site.data.keyword.amashort}} en un entorno de desarrollo Node.js local, añada el código siguiente.  

```JavaScript
var vcapApplication = {
	application_id:"appGUID"
};

var vcapServices = {
	"AdvancedMobileAccess": [
		{
			"credentials": {
				"admin_url": "https://mobile.ng.bluemix.net/imfmobileplatformdashboard/?appGuid=appGUID",
				"clientId": "appGUID",
				"secret": "secret",
				"serverUrl": "https://imf-authserver.ng.bluemix.net/imf-authserver",
				"tenantId": "appGUID"
			}
		}
	]
};

process.env["VCAP_APPLICATION"] = JSON.stringify(vcapApplication);
process.env["VCAP_SERVICES"] = JSON.stringify(vcapServices);

// Ahora puede que necesite el módulo bms-mca-token-validation-strategy:
var MCABackendStrategy =
	require('bms-mca-token-validation-strategy').MCABackendStrategy;

// Resto del código
```
Sustituya las apariciones del valor *appGUID* en el código con el valor *appGUID* del programa de fondo móvil.


## Configuración de aplicaciones de {{site.data.keyword.amashort}} para que funcionen con un servidor de desarrollo local
{: #configuring-local}

Inicialice los SDK del cliente de {{site.data.keyword.amashort}} con el URL real de la aplicación de {{site.data.keyword.Bluemix_notm}} y utilice el localhost (o dirección IP) en cada solicitud. Vea los ejemplos siguientes.

Sustituya el `BMSClient.REGION_UK` con la región adecuada.

Es posible que tenga que cambiar `localhost` por una dirección IP real del servidor de desarrollo en los ejemplos siguientes.

### Android
{: #android}
```Java
String baseRequestUrl = "http://localhost:3000";
String bluemixAppRoute = "http://myapp.mybluemix.net";
String bluemixAppGUID = "your-bluemix-app-guid";

BMSClient.getInstance().initialize(bluemixAppRoute, bluemixAppGUID, BMSClient.REGION_UK);

Request request =
			new Request(baseRequestUrl + "/resource/path", Request.GET);

request.send(this, new ResponseListener() {
	@Override
	public void onSuccess (Response response) {
		Log.d("Myapp", "onSuccess :: " + response.getResponseText());
	}
	@Override
	public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
		if (null != t) {
			Log.d("Myapp", "onFailure :: " + t.getMessage());
		} else if (null != extendedInfo) {
			Log.d("Myapp", "onFailure :: " + extendedInfo.toString());
		} else {
			Log.d("Myapp", "onFailure :: " + response.getResponseText());
		}
	}
});
```


### iOS - Objective C
{: #objc}

```Objective-C
NSString *baseRequestUrl = @"http://localhost:3000";
NSString *bluemixAppRoute = @"http://myapp.mybluemix.net";
NSString *bluemixAppGUID = @"your-bluemix-app-guid";

[[IMFClient sharedInstance]
			initializeWithBackendRoute:bluemixAppRoute
			backendGUID:bluemixAppGUID];

NSString *requestPath = [NSString stringWithFormat:@"%@/resource/path",
								baseRequestUrl];

IMFResourceRequest *request =  [IMFResourceRequest
				requestWithPath:requestPath
				method:@"GET"];

[request sendWithCompletionHandler:^(IMFResponse *response, NSError *error) {
	if (error){
		NSLog(@"Error :: %@", [error description]);
	} else {
		NSLog(@"Response :: %@", [response responseText]);
	}
}];
```

### iOS - Swift
{: #swift}

```Swift
let baseRequestUrl = "http://localhost:3000";
let bluemixAppRoute = "http://myapp.mybluemix.net";
let bluemixAppGUID = "your-bluemix-app-guid";

IMFClient.sharedInstance().initializeWithBackendRoute(bluemixAppRoute,
	 							backendGUID: bluemixAppGuid)

let requestPath = baseRequestUrl + "/resource/path"

let request = IMFResourceRequest(path: requestPath, method: "GET");

request.sendWithCompletionHandler { (response, error) -> Void in
	if (nil != error){
		NSLog("Error :: %@", error.description)
	} else {
		NSLog("Response :: %@", response.responseText)
	}
};

```

### Cordova
{: #cordova}

```JavaScript
var baseRequestUrl = "http://localhost:3000";
var bluemixAppRoute = "http://myapp.mybluemix.net";
var bluemixAppGUID = "your-bluemix-app-guid";

BMSClient.initialize(bluemixAppRoute, bluemixAppGUID);

var success = function(data){
   	console.log("success", data);
}

var failure = function(error){
	console.log("failure", error);
}

var request = new MFPRequest(baseRequestUrl +
							"/resource/path", MFPRequest.GET);

request.send(success, failure);
```
