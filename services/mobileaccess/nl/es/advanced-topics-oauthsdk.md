---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-15"

---

{:codeblock:.codeblock}

El servicio {{site.data.keyword.amafull}} se sustituye por el servicio {{site.data.keyword.appid_full}}.

# Comunicación entre servicios y aplicaciones de fondo
{: #backend-comm}

En algunas situaciones, es posible que tenga que enviar solicitudes desde la aplicación de fondo que se esté ejecutando en {{site.data.keyword.Bluemix}} a otro servicio de fondo que esté protegido por el servicio de {{site.data.keyword.amafull}} (por ejemplo, el servicio de {{site.data.keyword.cloudant}}). En estos casos, debe añadir una señal OAuth a la solicitud.

Utilice el módulo `bms-mca-oauth-sdk npmjs` para obtener e inyectar elementos OAuth en las solicitudes.

## Instalación del módulo bms-mca-oauth-sdk
{: #sdk}

En una línea de mandatos, abra el directorio de la aplicación Node.js y ejecute el mandato siguiente:

```Bash
npm install -save bms-mca-oauth-sdk
```
{: codeblock}

## Utilización del módulo bms-mca-oauth-sdk
{: #using-sdk}

El código siguiente muestra cómo utilizar el módulo `bms-mca-oauth-sdk`.


``` JavaScript
var oauthSDK = require('bms-mca-oauth-sdk');

var options = {

	// Puede almacenar las señales en memoria caché para evitar recorridos de ida y vuelta adicionales en cada solicitud
	// Esta propiedad define el número de señales que se van a almacenar en la memoria caché

	cacheSize: 100,

	// Las propiedades siguientes se recuperan automáticamente cuando el archivo Node.js
	// se ejecuta en {{site.data.keyword.Bluemix_notm}} y se enlaza a una instancia del servicio de {{site.data.keyword.amashort}}.
	// Como alternativa, puede obtener los valores de estas propiedades pulsando Mostrar credenciales
	// en el icono del servicio {{site.data.keyword.amashort}} del panel de control de la aplicación de {{site.data.keyword.Bluemix_notm}}

	appId: "tenantID",				// a.k.a. Bluemix applicationGUID
	clientId: "clientId",			
	secret: "secret",
	serverUrl: "serverUrl"
};

oauthSDK.getAuthorizationHeader(options).then(function(authHeader){

	// En la solicitud que desea enviar al recurso protegido,
	// añada el valor authHeader.

	request.headers.Authorization = authHeader;

	// Envíe la solicitud

});

```
{: codeblock}
