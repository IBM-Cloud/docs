---

copyright:
  años: 2015, 2016

---

# Uso de {{site.data.keyword.amashort}} con un entorno de desarrollo local
{: #protecting-local}

Puede configurar su entorno de desarrollo local para que utilice el servicio de {{site.data.keyword.amashort}} que se ejecuta en {{site.data.keyword.Bluemix}}. Específicamente, puede utilizar el SDK del servidor de {{site.data.keyword.amashort}} cuando desarrolle código del lado del servidor con un servidor de desarrollo local, como Node.js.

El SDK del servidor de {{site.data.keyword.amashort}} necesita que se definan dos variables de entorno. Cuando desarrolle código del lado del servidor en {{site.data.keyword.Bluemix_notm}}, la infraestructura de {{site.data.keyword.Bluemix_notm}} proporciona estas variables.

* `VCAP_SERVICES`: contiene información sobre servicios que están enlazados a la aplicación de fondo móvil.
* `VCAP_APPLICATION`: contiene información sobre la aplicación de fondo móvil.

Para utilizar {{site.data.keyword.amashort}} con un servidor de desarrollo local, debe añadir estas variables manualmente.

1. Abra el panel de control de {{site.data.keyword.Bluemix_notm}} del programa de fondo móvil que está protegido con el servicio de {{site.data.keyword.amashort}}.

1. Pulse **Opciones móviles** y copie el valor de **AppGUID**.

1. En el entorno de desarrollo local, defina la variable de entorno *VCAP_APPLICATION*. La variable debe contener un objeto JSON en serie con una sola propiedad.
```JavaScript
{
    application_id: "appGUID"
}
```
Sustituya la variable *appGUID* con el valor del campo **Opciones móviles**.

1. Haga clic en **Mostrar credenciales** en el mosaico de servicios de {{site.data.keyword.amashort}} en la aplicación de fondo móvil en el panel de control de {{site.data.keyword.Bluemix_notm}}. Se muestra un objeto JSON con las credenciales de acceso que proporciona {{site.data.keyword.amashort}} a la aplicación de fondo móvil.

1. En el entorno de desarrollo local, defina la variable de entorno `VCAP_SERVICES`. El valor de esta variable debe ser un objeto JSON en serie que contenga las credenciales de {{site.data.keyword.amashort}}.  Consulte el ejemplo siguiente para obtener más información.

## Código de ejemplo
{: #local-dev-sample}

Para utilizar el servicio de {{site.data.keyword.amashort}} en un entorno de desarrollo Node.js local, añada el código siguiente antes del módulo require `bms-mca-token-validation-strategy`.

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

var MCABackendStrategy =
	require('bms-mca-token-validation-strategy').MCABackendStrategy;

// Resto del código
```
Sustituya las apariciones del valor *appGUID* en el código con el valor *appGUID* del programa de fondo móvil.


## Configuración de aplicaciones móviles para que funcionen con un servidor de desarrollo local
{: #configuring-local}

Inicialice los SDK del cliente de {{site.data.keyword.amashort}} con un URL real de la aplicación de {{site.data.keyword.Bluemix_notm}} y utilice el localhost (o dirección IP) en cada solicitud. Vea los ejemplos siguientes.

Es posible que tenga que cambiar `localhost` por una dirección IP real del servidor de desarrollo en los ejemplos siguientes.

### Android

```Java
String baseRequestUrl = "http://localhost:3000";
String bluemixAppRoute = "http://myapp.mybluemix.net";
String bluemixAppGUID = "your-bluemix-app-guid";

BMSClient.getInstance().initialize(bluemixAppRoute, bluemixAppGUID);

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
### Cordova

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

### iOS - Objective C

```Objective-C
NSString *baseRequestUrl = @"http://localhost:3000";
NSString *bluemixAppRoute = @"http://myapp.mybluemix.net";
NSString *bluemixAppGUID = @"your-bluemix-app-guid";

[[IMFClient sharedInstance]
			initializeWithBackendRoute:bluemixAppRoute
			backendGUID:bluemixAppGUID];

NSString *requestPath = [NSString stringWithFormat:@"%@/resource/path",
								baseRequestUrl];

IMFResourceRequest* request = [IMFResourceRequest
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
