---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-10"
---
{:shortdesc: .shortdesc} 

# Uso de {{site.data.keyword.amashort}} con un entorno de desarrollo local
{: #protecting-local}

Puede configurar su desarrollo local para que utilice el servicio de {{site.data.keyword.amafull}} que se ejecuta en {{site.data.keyword.Bluemix}}. Específicamente, puede desarrollar código de forma local utilizando el SDK del servidor de {{site.data.keyword.amashort}} y enviar solicitudes de {{site.data.keyword.amashort}} al servidor de desarrollo. Estas solicitudes las protegerá el servicio de {{site.data.keyword.amashort}} que se ejecuta en {{site.data.keyword.Bluemix}}.

## Antes de empezar
{: #before-you-begin}
Debe tener lo siguiente:

* Una instancia de una aplicación {{site.data.keyword.Bluemix_notm}} que esté protegida por el servicio {{site.data.keyword.amashort}}. Para obtener más información sobre la creación de una aplicación de fondo {{site.data.keyword.Bluemix_notm}}, consulte [Cómo empezar](index.html).
* Los valores del parámetro de servicio. Abra el servicio en el panel de control de {{site.data.keyword.Bluemix_notm}}. Pulse **Opciones móviles**. Los valores `applicationRoute` y `appGUID` (también conocidos como `tenantId`) se muestran en los campos **Ruta** y **GUID de app / TenantId**. Necesitará estos valores para inicializar el SDK y para enviar solicitudes a la aplicación de fondo.
*  Busque la región en la que se aloja su aplicación {{site.data.keyword.Bluemix_notm}}. Para ver la región de {{site.data.keyword.Bluemix_notm}}, pulse el icono de **Avatar** ![Icono de Avatar](images/face.jpg "Icono de Avatar") de la barra de menús para abrir el widget **Cuenta y soporte**. El valor de región debe ser uno de los siguientes: **EE.UU. sur**, **Sídney** o **Reino Unido**. Los valores constantes de SDK exactos que se corresponden con estos nombres se indican en los ejemplos de código. 

## Configuración del SDK del servidor
{: #serversetup}

El SDK del servidor de {{site.data.keyword.amashort}} necesita que se definan dos variables de entorno. Cuando desarrolle código del lado del servidor en {{site.data.keyword.Bluemix_notm}}, la infraestructura de {{site.data.keyword.Bluemix_notm}} proporciona estas variables.

* `VCAP_SERVICES`: contiene información sobre servicios que están enlazados a la aplicación de fondo móvil.
* `VCAP_APPLICATION`: contiene información sobre la aplicación de fondo móvil.

Para utilizar {{site.data.keyword.amashort}} con un servidor de desarrollo local, debe añadir estas variables manualmente.

1. Abra el panel de control de {{site.data.keyword.Bluemix_notm}} de la aplicación de programa de fondo móvil protegida con el servicio de {{site.data.keyword.amashort}}.

1. En el entorno de desarrollo local, defina la variable de entorno *VCAP_APPLICATION*. La variable debe contener un objeto JSON en serie con una sola propiedad.
```JavaScript
{
    application_id: "appGUID"
}
```

Sustituya el valor *appGUID* por el valor `appGUID` obtenido en [Antes de empezar](#before-you-begin). 

1. Pulse **Mostrar credenciales** en el icono de servicios de {{site.data.keyword.amashort}} en la aplicación de fondo móvil en el panel de control de {{site.data.keyword.Bluemix_notm}}. Se muestra un objeto JSON con las credenciales de acceso que proporciona {{site.data.keyword.amashort}} a la aplicación de fondo móvil.

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
				"tenantId": "tenantId"
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

Sustituya el valor *appGUID* por el valor `appGUID` obtenido en [Antes de empezar](#before-you-begin). 


## Configuración de aplicaciones de {{site.data.keyword.amashort}} para que funcionen con un servidor de desarrollo local
{: #configuring-local}

Inicialice los SDK del cliente de {{site.data.keyword.amashort}} con el URL real de la aplicación de {{site.data.keyword.Bluemix_notm}} y utilice el localhost (o dirección IP) en cada solicitud. Vea los ejemplos siguientes.

Sustituya la región por la región adecuada.

Sustituya los valores *appGUID* y *bluemixAppRoute* por los valores obtenidos en [Antes de comenzar](#before-you-begin). 

Es posible que tenga que cambiar `localhost` por una dirección IP real del servidor de desarrollo en los ejemplos siguientes.

### Android
{: #android}
```Java
String baseRequestUrl = "http://localhost:3000";
String bluemixAppRoute = "http://myapp.mybluemix.net";
String bluemixAppGUID = "your-bluemix-app-guid";
String tenantId = "your-MCA-service-tenantID";

BMSClient.getInstance().initialize(bluemixAppRoute, bluemixAppGUID, BMSClient.REGION_UK);
// establezca la región de la aplicación MCA aquí. En este momento, los valores posibles son BMSClient.REGION_US_SOUTH, BMSClient.REGION_SYDNEY, o BMSClient.REGION_UK BMSClient.getInstance().setAuthorizationManager(
                 MCAAuthorizationManager.createInstance(this, tenantId));

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
NSString *tenantId = "your-MCA-service-tenantID";

[[IMFClient sharedInstance]
			initializeWithBackendRoute:bluemixAppRoute
			backendGUID:bluemixAppGUID];
			
[[IMFAuthorizationManager sharedInstance]  initializeWithTenantId: tenantId];


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

let baseRequestUrl = "http://localhost:3000"
let bluemixAppRoute = "http://myapp.mybluemix.net"
let tenantId = "your-MCA-service-tenantID"
let regionName = BMSClient.Region.usSouth
// establezca la región de la aplicación MCA aquí. En este momento, puede ser BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, BMSClient.Region.sydney
BMSClient.sharedInstance.initialize(bluemixAppRoute: bluemixAppRoute, bluemixAppGUID: tenantId, bluemixRegion: regionName)

BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance
           
let requestPath = baseRequestUrl + "/resource/path"               
let request = Request(url: requestPath, method: HttpMethod.GET)
            
request.send { (response, error) in
	if let error = error {
    			print("Connection failure")
     		print("Error :: \(error)");
     		print("Status :: \(response?.statusCode)");
    	} else {
           print("Connection success")
           print("Response :: \(response?.responseText)")
    }                
}



```


### Cordova
{: #cordova}

```JavaScript
var baseRequestUrl = "http://localhost:3000";
var bluemixAppRoute = "http://myapp.mybluemix.net";
var bluemixAppGUID = "your-bluemix-app-guid";
Var tenantId = "your-MCA-service-tenantID";

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

