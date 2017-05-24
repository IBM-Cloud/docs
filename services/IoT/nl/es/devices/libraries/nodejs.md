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


# Node.js para desarrolladores de dispositivos
{: #nodejs}

Puede adaptar las bibliotecas de cliente y los ejemplos de Node.js para crear y desarrollar código de dispositivo que interactúa con su organización en {{site.data.keyword.iot_full}}.
{:shortdesc}

Utilice la información y los ejemplos proporcionados para empezar a desarrollar los dispositivos utilizando Node.js.

## Descarga del cliente y los recursos de Node.js
{: #node.js_client_downloads}

Para acceder a las bibliotecas de cliente de Node.js para {{site.data.keyword.iot_short_notm}} y otros recursos disponibles, vaya al repositorio [iot-nodejs ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ibm-watson-iot/iot-nodejs){: new_window} en GitHub y complete las instrucciones de instalación.


Para más información, consulte los siguientes recursos:

- [Ejemplos para dispositivos ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ibm-watson-iot/iot-nodejs/tree/master/samples){: new_window} en Github
- El repositorio [ibmiotf ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.npmjs.com/package/ibmiotf){: new_window} en NPM

## Constructor
{: #constructor}

El constructor crea la instancia del cliente de dispositivo. Acepta un JSON de configuración que contiene las siguientes definiciones:

|Definición |Descripción |
|:---|:---|
|`org` |El ID de la organización.|
|`type`  |El tipo del dispositivo. Normalmente, el deviceType es una agrupación para los dispositivos que realizan una tarea específica, como por ejemplo "weatherballoon".|
|`id`  |El ID del dispositivo. Normalmente, para un determinado tipo de dispositivo, el deviceId es un identificador exclusivo de dicho dispositivo, por ejemplo un número de serie o una dirección MAC.|
|`auth-method`   |El método de autenticación que debe utilizarse. El único valor al que se da soporte actualmente es `token`.|
|`auth-token`   |Una señal de autenticación para conectar de forma segura el dispositivo a Watson IoT Platform. Este campo es obligatorio si `auth-method` es `token`.|

**Nota:** Si desea utilizar el servicio de Inicio rápido, tendrá que enviar sólo las tres primeras propiedades.

```
    var iotf = require("ibmiotf");
    var config = {
		"org" : "organization",
		"id" : "deviceId",
		"type" : "deviceType",
		"auth-method" : "token",
		"auth-token" : "authToken"
    };


    var deviceClient = new iotf.IotfDevice(config);
```

### Utilización de un archivo de configuración

En lugar de pasar la configuración directamente, puede utilizar un archivo de configuración JSON para proporcionar las propiedades de configuración necesarias, como se muestra en el ejemplo siguiente:


```  
    var iotf = require("ibmiotf");
    var config = require("./device.json");
    var deviceClient = new iotf.IotfDevice(config);  
```
El archivo de configuración `device.json` debe estar en el formato siguiente:

```
	{
	  "org": "xxxxx",
	  "type": "raspi",
	  "id": "pi1",
	  "auth-method" : "token",
	  "auth-token" : "xxxxxxxxxxxxxxxx"
	}

```  

## Conexión con {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

Puede conectarse al {{site.data.keyword.iot_short_notm}} invocando la función `connect`.

```
	var iotf = require("ibmiotf");
	var config = require("./device.json");

	var deviceClient = new iotf.IotfDevice(config);

	//establecimiento del nivel de registro a depurar. De forma predeterminada, es 'warn'
	deviceClient.log.setLevel('debug');

	deviceClient.connect();

	deviceClient.on('connect', function(){
		var i=0;
		console.log("connected");
		setInterval(function function_name () {
			i++;
			deviceClient.publish('myevt', 'json', '{"value":'+i+'}', 2);
		},2000);
	});

```

Tras la correcta conexión con el servicio {{site.data.keyword.iot_short_notm}}, el cliente de dispositivo envía un suceso `connect`. Este proceso significa que toda la lógica de dispositivos se puede implementar dentro de esta función de devolución de llamada.

El cliente de dispositivo intenta automáticamente volver a conectarse cuando pierde la conexión. Cuando la reconexión se realiza correctamente, el cliente enviará un suceso `reconnect`.

## Registro
{: #logging}

De forma predeterminada, sólo se registran los sucesos de registro de tipo *warn*. Si desea aumentar o disminuir el nivel de registro, utilice la función log.setLevel. Están soportados los siguientes niveles de registro:
- trace
- debug
- info
- warn
- error

```
	var iotf = require("ibmiotf");
	var config = require("./device.json");

	var deviceClient = new iotf.IotfDevice(config);

	//establecimiento del nivel de registro a depurar. De forma predeterminada, es 'warn'
	deviceClient.log.setLevel('debug');

```


## Publicación de sucesos
{: #publishing_events}

Los sucesos son el mecanismo por el que los dispositivos publican datos en el {{site.data.keyword.iot_short_notm}}. El dispositivo controla el contenido del suceso y asigna un nombre a cada suceso que envía.

Cuando una instancia de {{site.data.keyword.iot_short_notm}} recibe un suceso, las credenciales del suceso recibido identifican el dispositivo de envío, lo que significa que un dispositivo no puede suplantar a otro dispositivo.

Puede aumentar el nivel de calidad de servicio (QoS) para los sucesos que se publican. Los sucesos con un nivel de QoS superior a `0` pueden tardar más tiempo en publicarse debido a la información de recepción de confirmación adicional que se incluye.

**Nota:** La modalidad de flujo de Inicio rápido sólo da soporte a un nivel de QoS de `0`.


Los sucesos se pueden publicar con las siguientes propiedades:

|Propiedad |Descripción|
|:---|:---|
|`eventType`  | El tipo de suceso que se publicará, como por ejemplo estado o GPS. |  
|`eventFormat`  |El formato del suceso, por ejemplo, JSON. |
|`data`  | La carga útil del suceso, que debe ser una serie de almacenamiento intermedio. |
|`QoS`  | La calidad de servicio de MQTT para el suceso publicado. Los valores soportados son 0, 1 y 2.|


```
    var deviceClient = new Client.IotfDevice(config);

    deviceClient.connect();

    deviceClient.on("connect", function () {
       //publicar un suceso en la calidad de servicio predeterminada
       deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

       //publicar un suceso en la calidad de servicio definida por el usuario
       var myQosLevel=2
       deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}', myQosLevel);
  });

```

## Manejo de mandatos
{: #handling_commands}

Cuando el cliente de dispositivo se conecta, se suscribe automáticamente a cualquier mandato para este dispositivo. Para procesar mandatos específicos, debe registrar una función de devolución de llamada de mandatos. El cliente de dispositivo invoca la función de devolución de llamada de mandatos cuando se reciba un mandato. La función de devolución de llamada tiene las siguientes propiedades:

|Propiedad |Descripción|
|:---|:---|
|`commandName`  | Una serie, que especifica el nombre del mandato que se ha invocado. |  
|`format`  | Una serie, que especifica el formato del suceso, por ejemplo, JSON. |
|`payload`  | Una serie, que especifica los datos para la carga útil de mandatos.  |
|`topic`  | Cuando se publica como un dispositivo, la serie de temas no incluye el tipo de dispositivo ni el ID de dispositivo; estos se toman del ID de cliente.  Por ejemplo, `iot-2/evt/event_id/fmt/format_string`.  Al publicar como una aplicación o pasarela en nombre de un dispositivo, el tema debe incluir el tipo de dispositivo y el ID de dispositivo.  Por ejemplo `iot-2/type/device_type/id/device_id/evt/event_id/fmt/format_string`.|


```
	var deviceClient = new Client.IotfDevice(config);

	deviceClient.connect();

	deviceClient.on("connect", function () {
		//publicar un suceso en la calidad de servicio predeterminada
		deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

	});

	deviceClient.on("command", function (commandName,format,payload,topic) {
		if(commandName === "blink") {
			console.log(blink);
			//función que se realizará para este mandato
			blink(payload);
		} else {
			console.log("Command not supported.. " + commandName);
		}
	});

```

## Manejo de errores
{: #handling_errors}

Cuando el cliente de dispositivo ha detectado un error, envía un suceso *error*.

```
	var deviceClient = new Client.IotfDevice(config);

	deviceClient.connect();

	deviceClient.on("connect", function () {
		//publicar un suceso en la calidad de servicio predeterminada
		deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

	});

	deviceClient.on("error", function (err) {
		console.log("Error : "+err);
	});
	....

```

## Desconexión del cliente
{: #disconnecting_client}

En el ejemplo siguiente se muestra cómo puede desconectar el cliente y lanzar la conexión:

```
	var deviceClient = new Client.IotfDevice(config);

	deviceClient.connect();

	client.on("connect", function () {
		//publicar un suceso en la calidad de servicio predeterminada
		client.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

		//publicar el suceso en la calidad de servicio definida por el usuario
		var myQosLevel=2
		client.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}', myQosLevel);

		//desconectar el cliente
		client.disconnect();
	});

	....
```
