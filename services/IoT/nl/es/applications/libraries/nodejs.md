---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}



# Node.js para desarrolladores de aplicaciones
{: #nodejs}

Última actualización: 29 de julio de 2016
{: .last-updated}

Puede adaptar las bibliotecas y los ejemplos del cliente en Node.js para crear y personalizar aplicaciones que interactúan con su organización en {{site.data.keyword.iot_full}}.
{:shortdesc}

Utilice la información y los ejemplos que se proporcionan para empezar a desarrollar las aplicaciones mediante Node.js.

## Descarga del cliente y los recursos de Node.js
{: #nodejs_client_download}

Para acceder a las bibliotecas de cliente de Node.js para {{site.data.keyword.iot_short_notm}} y otros recursos disponibles, vaya al repositorio [iot-nodejs ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ibm-watson-iot/iot-nodejs){: new_window} en GitHub y complete las instrucciones de instalación.


Para más información, consulte los siguientes recursos:
- [Ejemplos de aplicación ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ibm-watson-iot/iot-nodejs/tree/master/samples){: new_window} en GitHub.
- [ibmiotf ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.npmjs.com/package/ibmiotf){: new_window} en NPM.
- Sección [Referencia](#reference_nodejs) de este documento.


## Constructor
{: #constructor}

El constructor compila la instancia del cliente de aplicaciones y acepta un archivo de configuración de JSON que contiene las siguientes propiedades:

| Propiedad     |Descripción     |
|----------------|----------------|
|`org` |El ID de la organización. Se trata de un valor obligatorio.|
|`id`  |El ID exclusivo de la aplicación dentro de su organización.|
|`auth-key`   |Una clave API para conectar de forma segura la aplicación a Watson IoT Platform.|
|`auth-token`   |Una señal de clave API para conectar de forma segura el dispositivo a Watson IoT Platform.|
|`type`  |El tipo de suscripción. Especifique `shared` para habilitar la suscripción compartida.|


Para utilizar Quickstart, sólo son necesarias las dos primeras propiedades.

```
  var Client = require("ibmiotf");
	var appClientConfig = {
		"org" : orgId,
		"id" : appId,
		"auth-key" : apiKey,
		"auth-token" : apiToken
	}

	var appClient = new Client.IotfApplication(appClientConfig);
```


### Utilización de un archivo de configuración


En lugar de pasar las propiedades JSON directamente, también puede utilizar un archivo de configuración resaltado en el siguiente ejemplo de código:

```

  var Client = require("ibmiotf");
	var appClientConfig = require("./application.json");
	var appClient = new Client.IotfApplication(appClientConfig);
```

Asegúrese de que el archivo de configuración JSON se encuentre en el siguiente formato:

```
    {
	  "org": 'xxxxx',
	  "id": 'myapp',
	  "auth-key": 'a-xxxxxxx-zenkqyfiea',
	  "auth-token": 'xxxxxxxxxx'
    }
```


## Conexión con {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

Para conectarse a {{site.data.keyword.iot_short_notm}}, envíe una solicitud *connect*, tal como se indica a continuación:

```
  var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

	//Añada su código aquí
	});
```

Tras conectarse satisfactoriamente al servicio de {{site.data.keyword.iot_short_notm}}, el cliente de la aplicación enviará un suceso `connect`, de forma que cualquier lógica se pueda implementar dentro de esta función callback.



El cliente de aplicaciones intenta automáticamente volver a conectarse cuando pierde la conexión. Cuando la reconexión se realiza correctamente, el cliente enviará un suceso `reconnect`.



## Registro
{: #logging}

De forma predeterminada, sólo se registran los sucesos de registro de tipo `warn`. Si desea aumentar o disminuir el nivel de registro, utilice la función `log.setLevel`. Están soportados los siguientes niveles de registro:
- trace
- debug
- info
- warn
- error

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();
	//establecimiento del nivel de registro a 'trace'
	appClient.log.setLevel('trace');
	appClient.on("connect", function () {

	//Añada su código aquí
	});
```

## Suscripciones compartidas
{: #shared_subscriptions}

Utilice la función de suscripción compartida para crear aplicaciones escalables que equilibren la carga de mensajes de varias instancias de la aplicación. Para habilitar el equilibrio de carga, establezca el campo `type` en `shared`, lo que se muestra en el ejemplo siguiente:

```

	var appClientConfig = {
	  org: 'xxxxx',
	  id: 'myapp',
	  "auth-key": 'a-xxxxxx-xxxxxxxxx',
	  "auth-token": 'xxxxx!xxxxxxxx',
	  "type" : "shared" // realice esta conexión como suscripción compartida
	};
	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();
	//establecimiento del nivel de registro a 'trace'
	appClient.log.setLevel('trace');
	appClient.on("connect", function () {

	//Añada su código aquí
	});
```

## Manejo de errores
{: #handling_errors}

Cuando el cliente de aplicaciones detecta un error, se generará un suceso `error`.

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();
	//establecimiento del nivel de registro a 'trace'
	appClient.log.setLevel('trace');
	appClient.on("connect", function () {

	//Añada su código aquí
	});
	appClient.on("error", function (err) {
		console.log("Error : "+err);
	});
```

## Suscripción a sucesos de dispositivos
{: #subscribing_device_events}

Los sucesos son el mecanismo por el que los dispositivos publican datos en la instancia de {{site.data.keyword.iot_short_notm}}. El dispositivo controla el contenido del suceso y asigna un nombre a cada suceso que envía.

Cuando una instancia de {{site.data.keyword.iot_short_notm}} recibe un suceso, las credenciales del suceso recibido identifican el dispositivo de envío, lo que significa que un dispositivo no puede suplantar a otro dispositivo.


De forma predeterminada, las aplicaciones se suscriben a todos los sucesos desde todos los dispositivos conectados. Utilice los parámetros device type, device ID, event y message format para controlar el ámbito de la suscripción. Los siguientes ejemplos de código muestran cómo puede utilizar estos parámetros para definir el ámbito de una suscripción:

### Suscripción a todos los sucesos de todos los dispositivos


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents();
	});
```

### Suscripción a todos los sucesos de todos los dispositivos de un tipo específico

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("mydeviceType");
	});
```

### Suscripción a un suceso específico de todos los dispositivos


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("+","+","myevent");
	});
```

### Suscripción a un suceso específico de dos o más dispositivos distintos

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("myDeviceType","device01","myevent");
		appClient.subscribeToDeviceEvents("myOtherDeviceType","device02","myevent");
	});
```

### Suscripción a todos los sucesos que se publican en formato JSON


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("myDeviceType","device01","+","json");

	});
```

**Nota**: Un cliente individual puede admitir varias suscripciones.

### Manejo de sucesos desde dispositivos


Para procesar los sucesos recibidos por las suscripciones, implemente un método callback de sucesos de dispositivos. El cliente de aplicaciones de {{site.data.keyword.iot_short_notm}} envía el suceso `deviceEvent`. Esta función tiene las propiedades siguientes:

- deviceType
- deviceId
- eventType
- format
- payload
- topic

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("myDeviceType","device01","+","json");

	});
	appClient.on("deviceEvent", function (deviceType, deviceId, eventType, format, payload) {

		console.log("Device Event from :: "+deviceType+" : "+deviceId+" of event "+eventType+" with payload : "+payload);

	});
```


## Suscripción a estado de dispositivos
{: #subscribing_device_status}

De forma predeterminada, al suscribirse al estado del dispositivo, se recibirán actualizaciones de estado para todos los dispositivos conectados. Utilice los parámetros type e ID para controlar el ámbito de la suscripción. Un cliente individual puede admitir varias suscripciones.

### Suscripción a actualizaciones de estado para todos los dispositivos

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus();

	});
```

### Suscripción a actualizaciones de estado para todos los dispositivos de un tipo específico


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus("myDeviceType");

	});
```

### Suscripción a actualizaciones de estado para dos dispositivos distintos

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus("myDeviceType","device01");
		appClient.subscribeToDeviceStatus("myOtherDeviceType","device02");

	});
```

### Manejo de actualizaciones de estado desde dispositivos

Para procesar las actualizaciones de estado que han recibido las suscripciones, implemente un método callback de estado de dispositivos. El cliente de la aplicación {{site.data.keyword.iot_short_notm}} envía el suceso `deviceStatus`. Esta función tiene las propiedades siguientes:

-   deviceType
-   deviceId
-   payload
-   topic

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus("myDeviceType","device01");
		appClient.subscribeToDeviceStatus("myOtherDeviceType","device02");

	});
	appClient.on("deviceStatus", function (deviceType, deviceId, payload, topic) {

		console.log("Device status from :: "+deviceType+" : "+deviceId+" with payload : "+payload);

	});
```


## Publicación de sucesos desde dispositivos
{: #publishing_device_events}


Las aplicaciones pueden publicar sucesos como si se originaran a partir de un dispositivo. La función requiere las propiedades siguientes:

-   deviceType
-   deviceId
-   eventType
-   format
-   data


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		var myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50};
		myData = JSON.stringify(myData);
		appClient.publishDeviceEvent("myDeviceType","device01", "myEvent", "json", myData);

	});
```


## Publicación de mandatos en dispositivos
{: #publishing_commands_devices}

Las aplicaciones pueden publicar mandatos en dispositivos conectados. La función requiere las propiedades siguientes:

-   deviceType
-   deviceId
-   eventType
-   format
-   data

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		var myData={'DelaySeconds' : 10};
		myData = JSON.stringify(myData);
		appClient.publishDeviceCommand("myDeviceType","device01", "reboot", "json", myData);

	});
```


## Desconexión del cliente
{: #disconnect_client}

El ejemplo siguiente desconecta el cliente y también libera las conexiones:

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		var myData={'DelaySeconds' : 10}
		appClient.publishDeviceCommand("myDeviceType","device01", "reboot", "json", myData);

		appClient.disconnect();
	});
```


## Referencia
{: #reference_nodejs}

En la tabla siguiente se describen los parámetros utilizados en las funciones descritas es esta documentación de Node.js:

|Parámetro|Tipos de datos|Descripción|
|:---|:---|
|`deviceType`|Serie|El tipo de dispositivo. Normalmente, el deviceType es una agrupación para los dispositivos que realizan una tarea específica, como por ejemplo "weatherballoon".|
|`deviceId`|Serie|El ID del dispositivo. Normalmente, para un determinado tipo de dispositivo, el deviceId es un identificador exclusivo de dicho dispositivo, por ejemplo un número de serie o una dirección MAC.|
|`eventType`|Serie|Un grupo de sucesos específicos, por ejemplo "status", "warning" y "data".|
|`format`|Serie|El formato puede ser una serie, como por ejemplo JSON.  |
|`data`|Diccionario|Los datos para la carga útil de mensaje. La longitud máxima es 131072 bytes.|
|`payload`|Serie|Los datos para la carga útil de mensaje. La longitud máxima es 131072 bytes.|
|`topic`|Serie|Cuando se publica como un dispositivo, la serie de temas no incluye el tipo de dispositivo ni el ID de dispositivo; estos se toman del ID de cliente.  Por ejemplo, `iot-2/evt/event_id/fmt/format_string`.  Al publicar como una aplicación o pasarela en nombre de un dispositivo, el tema debe incluir el tipo de dispositivo y el ID de dispositivo.  Por ejemplo `iot-2/type/device_type/id/device_id/evt/event_id/fmt/format_string`.|
