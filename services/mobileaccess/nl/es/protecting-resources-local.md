---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-08"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Uso de {{site.data.keyword.amashort}} con un entorno de desarrollo local
{: #protecting-local}

Puede configurar su desarrollo local para que utilice el servicio de {{site.data.keyword.amafull}} que se ejecuta en {{site.data.keyword.Bluemix}}. Específicamente, puede desarrollar código de forma local utilizando el SDK del servidor de {{site.data.keyword.amashort}} y enviar solicitudes de {{site.data.keyword.amashort}} al servidor de desarrollo. Estas solicitudes las protegerá el servicio de {{site.data.keyword.amashort}} que se ejecuta en {{site.data.keyword.Bluemix}}.

## Antes de empezar
{: #before-you-begin}

Debe tener lo siguiente:

* Una instancia de una aplicación {{site.data.keyword.Bluemix_notm}} que esté protegida por el servicio {{site.data.keyword.amashort}}. Para obtener más información sobre la creación de una aplicación de fondo {{site.data.keyword.Bluemix_notm}}, consulte [Cómo empezar](index.html).
* Su **TenantID**. Abra el servicio en el panel de control de {{site.data.keyword.amafull}}. Pulse el botón **Opciones móviles**. Los valores `tenantId` (también conocidos como `appGUID`) se muestran en el campo **GUID de app / TenantId**. Necesitará este valor para inicializar el gestor de autorización.
* Su **Ruta de aplicación**. Es el URL de la aplicación de programa de fondo. Necesita este valor para enviar solicitudes a sus puntos finales protegidos.
* Su {{site.data.keyword.Bluemix_notm}} **Región**.  Encontrará su región de {{site.data.keyword.Bluemix_notm}} actual en la cabecera, junto al icono **Avatar** ![icono Avatar](images/face.jpg "icono Avatar"). El valor de la región que aparece debe ser uno de los siguientes: `EE.UU. Sur`, `Sídney` o `Reino Unido`. Para ver la sintaxis exacta requerida por el SDK, consulte los comentarios de los ejemplos de código. Necesitará este valor para inicializar el cliente {{site.data.keyword.amashort}}.
* Un proyecto de Android Studio, configurado para funcionar con Gradle. Para obtener más información sobre la configuración del entorno de desarrollo de Android, consulte las [Herramientas del desarrollador de Google ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://developer.android.com/sdk/index.html "Icono de enlace externo"){: new_window}.

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
	{: codeblock}

1. Pulse el separador **Mostrar credenciales** en el panel de control de {{site.data.keyword.amashort}}. Se muestra un objeto JSON con las credenciales de acceso que proporciona {{site.data.keyword.amashort}} a la aplicación de fondo móvil.

1. En el entorno de desarrollo local, defina la variable de entorno `VCAP_SERVICES`. El valor de esta variable debe ser un objeto JSON en serie que contenga las credenciales de {{site.data.keyword.amashort}}.  Consulte el ejemplo siguiente para obtener más información.

## Código del servidor de ejemplo
{: #local-dev-sample}

Para utilizar el servicio de {{site.data.keyword.amashort}} en un entorno de desarrollo Node.js local, añada el código siguiente.  

```JavaScript
var vcapApplication = {
	application_id:"tenantID"
};

var vcapServices = {
	"AdvancedMobileAccess": [
		{
			"credentials": {
				"admin_url": "https://mobile.ng.bluemix.net/imfmobileplatformdashboard/?appGuid=appGUID",
				"clientId": "tenantID",
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
{: codeblock}

Para obtener información sobre cómo buscar el valor *tenantID*, consulte [Antes de empezar](#before-you-begin).


## Configuración de aplicaciones de {{site.data.keyword.amashort}} para que funcionen con un servidor de desarrollo local
{: #configuring-local}

Inicialice los SDK del cliente de {{site.data.keyword.amashort}} con el URL real de la aplicación de {{site.data.keyword.Bluemix_notm}} y utilice el localhost (o dirección IP) en cada solicitud. Vea los ejemplos siguientes.

Sustituya la región por la región adecuada. Consulte los ejemplos de código para obtener la sintaxis correcta.

Sustituya los valores *appGUID* y *bluemixAppRoute*. Para obtener información sobre cómo obtener estos valores, consulte [Antes de empezar](#before-you-begin).

Es posible que tenga que cambiar `localhost` por una dirección IP real del servidor de desarrollo en los ejemplos siguientes.

### Android
{: #android}

```Java
String baseRequestUrl = "http://localhost:3000";
String bluemixAppRoute = "http://myapp.mybluemix.net";
String bluemixAppGUID = "your-bluemix-app-guid";
String tenantId = "your-MCA-service-tenantID";


BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_UK);

//  establezca la región de la aplicación MCA aquí. En este momento, los valores posibles son BMSClient.REGION_US_SOUTH, BMSClient.REGION_SYDNEY, o BMSClient.REGION_UK

BMSClient.getInstance().setAuthorizationManager(
					MCAAuthorizationManager.createInstance(this, "<MCAServiceTenantId>"));

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
{: codeblock}


### iOS - Swift
{: #swift}

```Swift

 let baseRequestUrl = "http://localhost:3000";
 let tenantId = "<serviceTenantID>"
 let regionName = <applicationBluemixRegion>
 //possible values: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, or BMSClient.Region.sydney
 let mcaAuthManager = MCAAuthorizationManager.sharedInstance
 mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
 BMSClient.sharedInstance.authorizationManager = mcaAuthManager
        
        
 let requestPath = baseRequestUrl + "/protectedResource"
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
{: codeblock}


### Cordova
{: #cordova}

```JavaScript
var baseRequestUrl = "http://localhost:3000";
var bluemixAppRoute = "http://myapp.mybluemix.net";
var bluemixAppGUID = "your-bluemix-app-guid";
Var tenantId = "your-MCA-service-tenantID";

BMSClient.initialize(<applicationBluemixRegion>);

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
{: codeblock}
