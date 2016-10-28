---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Java para desarrolladores de aplicaciones
{: #java}

Última actualización: 07 de septiembre de 2016
{: .last-updated}

Puede utilizar Java para crear y personalizar aplicaciones que interactúan con su organización en {{site.data.keyword.iot_full}}. Utilice la información y los ejemplos que se proporcionan para empezar a desarrollar las aplicaciones mediante Java.
{:shortdesc}

## Descarga del cliente y los recursos de Java
{: #java_client_download}

Para acceder a las bibliotecas y a los ejemplos de cliente Java para {{site.data.keyword.iot_short_notm}}, vaya al repositorio [iot-java](https://github.com/ibm-watson-iot/iot-java) en GitHub y complete las instrucciones de instalación.


## Constructor
{: #constructor}

El constructor compila la instancia del cliente y acepta un objeto `Propiedades` que contiene las siguientes definiciones:

| Definición     |Descripción     |
|----------------|----------------|
|`org` |El ID de la organización. Se trata de un valor obligatorio. Si está utilizando un flujo de Quickstart, especifique `quickstart`.|
|`id` |El ID exclusivo de la aplicación en su organización.|
|`auth-method`  |El método de autenticación, para el que el único valor al que se da soporte actualmente es `apikey`.|
|`auth-key`   |Una clave API opcional, que es obligatoria cuando auth-method está establecido en `apikey`.  |
|`auth-token`   |Una señal de clave API, que es obligatoria cuando auth-method está establecido en `apikey`. |
|`clean-session`|Un valor true o false que sólo es necesario si desea conectar la aplicación en modalidad de suscripción duradera. De forma predeterminada, `clean-session` se establece en `true`.|
|`shared-subscription`|Un valor booleano. Establézcalo en `true` si desea construir aplicaciones escalables que equilibren la carga de mensajes en varias instancias de la aplicación. Para obtener más información, consulte [Aplicaciones escalables](mqtt.html#/scalable-applications#scalable-applications).

El objeto `Propiedades` crea definiciones que se utilizan para interactuar con el módulo de {{site.data.keyword.iot_short_notm}}. Si no especifica las propiedades para este objeto, o si especifica `quickstart`, el cliente se conecta al servicio de Inicio rápido de {{site.data.keyword.iot_short_notm}} como un dispositivo no registrado.

El ejemplo de código siguiente muestra cómo puede construir la instancia de ApplicationClient en modalidad `quickstart`:

```
    import com.ibm.iotf.client.app.ApplicationClient;
    import java.util.Properties;

    Properties options = new Properties();
    options.put("org", "quickstart");

    ApplicationClient myClient = new ApplicationClient(options);
```

El ejemplo de código siguiente muestra cómo puede construir la instancia de ApplicationClient en la modalidad de flujo registrada:

```
    Properties options = new Properties();
    options.put("org", "uguhsp");
    options.put("id", "app" + (Math.random() * 10000));
    options.put("Authentication-Method","apikey");
    options.put("API-Key", "<API-Key>");
    options.put("Authentication-Token", "<Authentication-Token>");

    ApplicationClient myClient = new ApplicationClient(options);
```

### Utilización de un archivo de configuración

En lugar de incluir un objeto `Propiedades` directamente, puede utilizar un archivo de configuración que contenga los pares nombre-valor para el objeto `Propiedades` en el formato siguiente:

```
    Properties props = ApplicationClient.parsePropertiesFile(new File("C:\\temp\\application.prop"));
    ApplicationClient myClient = new ApplicationClient(props);
    ...
```
El archivo de configuración de aplicación debe estar en el formato siguiente:

```
    [application]
    org=$orgId
    id=$myApplication
    auth-method=apikey
    auth-key=$key
    auth-token=$token
    enable-shared-subscription=true|false
```

## Conexión con {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

Para conectarse a {{site.data.keyword.iot_short_notm}}, utilice la función `connect()`. La función `connect()` incluye un parámetro booleano opcional que se llama `autoRetry` que determina si la biblioteca intenta volver a conectarse en el caso de un fallo de conexión a MqttException. De forma predeterminada, `autoRetry` se establece en true. Si falla una conexión MqttSecurityException porque se pasan detalles de registro de dispositivos incorrectos, la biblioteca no intentará volver a conectarse, incluso si `autoRetry` se establece en `true`.

```
    Properties props = ApplicationClient.parsePropertiesFile(new File("C:\\temp\\application.prop"));
    ApplicationClient myClient = new ApplicationClient(props);

    myClient.connect();
```

Tras la conexión correcta al servicio de {{site.data.keyword.iot_short_notm}}, los clientes de la aplicación pueden suscribirse a los sucesos del dispositivo, suscribirse a los estados del dispositivo y publicar los sucesos y los mandatos del dispositivo.

## Suscripción a sucesos de dispositivos
{: #subscribing_device_events}

Los sucesos son el mecanismo por el que los dispositivos publican datos a {{site.data.keyword.iot_short_notm}}. El dispositivo controla el contenido del suceso y asigna un nombre a cada suceso que envía.

Cuando una instancia de {{site.data.keyword.iot_short_notm}} recibe un suceso, las credenciales del suceso recibido identifican el dispositivo de envío, lo que significa que un dispositivo no puede suplantar a otro dispositivo.


De forma predeterminada, las aplicaciones se suscriben a todos los sucesos desde todos los dispositivos conectados. Utilice los parámetros device type, device ID, event y message format para controlar el ámbito de la suscripción. Los siguientes ejemplos de código muestran cómo puede utilizar estos parámetros para definir el ámbito de una suscripción:

### Suscripción a todos los sucesos de todos los dispositivos


```
    myClient.connect();
    myClient.subscribeToDeviceEvents();
```
### Suscripción a todos los sucesos de todos los dispositivos de un tipo específico


```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino");
```

### Suscripción a todos los sucesos de un dispositivo específico


```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino", "00aabbccddee");
```
### Suscripción a un suceso específico de dos o más dispositivos distintos

```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino", "00aabbccddee", "myEvent");
    myClient.subscribeToDeviceEvents("iotsample-arduino", "10aabbccddee", "myEvent");
```
### Suscripción a sucesos que se publican en formato JSON


```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino", "00aabbccddee", "myEvent", "json", 0);
```

**Nota**: Un cliente individual puede admitir varias suscripciones.

## Manejo de sucesos desde dispositivos
{: #handling_device_events}

Para procesar los sucesos que han recibido las suscripciones, registre un método callback de sucesos. Los mensajes se devuelven como una instancia de la clase de sucesos, que tiene los parámetros siguientes:

|Parámetro|Tipos de datos|Descripción|
|:---|:---|
|`event.device`|Serie|Identifica de forma exclusiva el dispositivo a través de todos los tipos de dispositivos de la organización.|
|`event.deviceType`|Serie|Identifica el tipo de dispositivo. Normalmente, el deviceType es una agrupación para los dispositivos que realizan una tarea específica, como por ejemplo "weatherballoon".|
|`event.deviceId`|Serie|Representa el ID del dispositivo. Normalmente, para un determinado tipo de dispositivo, el deviceId es un identificador exclusivo de dicho dispositivo, por ejemplo un número de serie o una dirección MAC.|
|`event.event`|Serie|Normalmente se utiliza para agrupar sucesos específicos, como por ejemplo "status", "warning" y "data".|
|`event.format`|Serie|El formato puede ser una serie, como por ejemplo JSON.  |
|`event.data`|Diccionario|Los datos para la carga útil de mensaje. La longitud máxima es 131072 bytes.|
|`event.timestamp`|Fecha y hora|La fecha y hora del suceso|


El código siguiente proporciona una implementación de ejemplo de callback de sucesos:

```
  import com.ibm.iotf.client.app.Event;
  import com.ibm.iotf.client.app.EventCallback;
  import com.ibm.iotf.client.app.Command;

  import java.util.concurrent.BlockingQueue;
  import java.util.concurrent.LinkedBlockingQueue;

  /**
    * Una clase de devolución de llamadas de sucesos de ejemplo que procesa los sucesos del dispositivo en una hebra independiente.
    *
    */
   class MyEventCallback implements EventCallback, Runnable {

	// Una cola para retener y procesar los sucesos para un manejo sencillo de mensajes MQTT
	private BlockingQueue<Event> evtQueue = new LinkedBlockingQueue<Event>();

	public void processEvent(Event e) {
		try {
			evtQueue.put(e);
		} catch (InterruptedException e1) {
			e1.printStackTrace();
		}
	}

	@Override
	public void processCommand(Command cmd) {
		System.out.println("Command received:: " + cmd);
	}

	@Override
	public void run() {
		while(true) {
			Event e = null;
			try {
				e = evtQueue.take();
				// En este ejemplo, la única salida es el suceso
				System.out.println("Event:: " + e.getDeviceId() + ":" + e.getEvent() + ":" + e.getPayload());
			} catch (InterruptedException e1) {
				// Omita la excepción Interuppted, vuelva a intentarlo
				continue;
			}
		}
	}
    }
```

Cuando se añade callback de sucesos al ApplicationClient, se invoca el método `processEvent()` siempre que se publique un suceso que coincida con la suscripción. El fragmento de código siguiente muestra cómo añadir el suceso en la instancia de ApplicationClient:



```
    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToDeviceEvents();
```

De forma parecida a la suscripción a sucesos de dispositivo, la aplicación puede suscribirse a mandatos que se envían a los dispositivos. El siguiente ejemplo de código muestra cómo suscribirse a todos los mandatos para todos los dispositivos de la organización:

```

    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToDeviceCommands();
```

Hay disponibles métodos sobrecargados para controlar la suscripción de mandatos. El método `processCommand()` se invoca cuando se envía un mandato al dispositivo que coincide con la suscripción de mandato.


## Suscripción a estado de dispositivos
{: #subscribing_device_status}

De forma parecida a la suscripción a sucesos de dispositivos, las aplicaciones pueden suscribirse al estado del dispositivo, como por ejemplo la conexión y desconexión del dispositivo a {{site.data.keyword.iot_short_notm}}. De forma predeterminada, esta suscripción se suscribe a las actualizaciones de estado para todos los dispositivos conectados. Utilice los parámetros device type y device id para controlar el ámbito de la suscripción. Los siguientes ejemplos de código muestran cómo puede utilizar estos parámetros para definir el ámbito de una suscripción:

### Suscribirse a actualizaciones de estado para todos los dispositivos

```
    myClient.connect();
    myClient.subscribeToDeviceStatus();
```

### Suscribirse a actualizaciones de estado para todos los dispositivos de un tipo específico


```

    myClient.connect();
    myClient.subscribeToDeviceStatus("iotsample-arduino");
```

### Suscribirse a actualizaciones de estado para dos dispositivos diferentes


```

    myClient.connect();
    myClient.subscribeToDeviceStatus("iotsample-arduino", "00aabbccddee");
    myClient.subscribeToDeviceStatus("iotsample-arduino", "10aabbccddee");
```

**Nota**: Un cliente individual puede admitir varias suscripciones.

## Manejo de actualizaciones de estado desde dispositivos
{: #handling_device_status_updates}

Para procesar las actualizaciones de estado que han recibido las suscripciones, necesita registrar un método callback de sucesos de estado. Para los sucesos de estado `Conectar` y `Desconectar`, los mensajes se devuelven como una instancia de la clase Estado, que contiene los parámetros siguientes:


| Parámetro     |Tipos de datos     |
|----------------|----------------|
|`status.clientAddr` |serie|
|`status.protocol`  |serie|
|`status.clientId`   |serie|
|`status.user`   |serie|
|`status.time`   |java.util.Date|
|`status.action` |serie|
|`status.connectTime`   |java.util.Date|
|`status.port`|entero|

Las siguientes propiedades sólo se establecen cuando el suceso de estado es `Desconectar`:

| Propiedad     |Tipos de datos     |
|----------------|----------------|
|`status.writeMsg` |entero|
|`status.readMsg`  |entero|
|`status.reason`   |serie|
|`status.readBytes`   |entero|
|`status.writeBytes`   |entero|


El ejemplo de código siguiente proporciona una implementación de ejemplo del callback de estado:

```

  private static class MyStatusCallback implements StatusCallback {

      public void processApplicationStatus(ApplicationStatus status) {
          System.out.println("Application Status = " + status.getPayload());
      }

      public void processDeviceStatus(DeviceStatus status) {
          if(status.getAction() == "Disconnect") {
              System.out.println("device: "+status.getDeviceId()
                                  + "  time: "+ status.getTime()
                                  + "  action: " + status.getAction()
                                  + "  reason: " + status.getReason());
          } else {
              System.out.println("device: "+status.getDeviceId()
                                  + "  time: "+ status.getTime()
                                  + "  action: " + status.getAction());
          }
      }
  }
```

Cuando se añade el callback de estado al ApplicationClient, se invocará el método `processDeviceStatus()` siempre que un dispositivo que coincida con los criterios se conecte o se desconecte del {{site.data.keyword.iot_short_notm}}. El ejemplo de código siguiente muestra cómo se puede añadir la instancia de callback de estado al ApplicationClient:

```

    myClient.connect()
    myClient.setStatusCallback(new MyStatusCallback());
    myClient.subscribeToDeviceStatus();
```
Las aplicaciones pueden suscribirse a cualquier otro estado de aplicación, como la conexión y desconexión de la aplicación a Watson IoT Platform. El siguiente fragmento de código muestra cómo suscribirse al estado de la aplicación de la organización:

```
    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToApplicationStatus();
```
El método sobrecargado está disponible para controlar la suscripción de estado a una aplicación particular. El método processApplicationStatus() se invoca siempre que se conecta o se desconecta una aplicación que coincide con los criterios del {{site.data.keyword.iot_short_notm}}.

## Publicación de sucesos desde dispositivos
{: #publishing_events_devices}

El ejemplo de código siguiente muestra cómo pueden publicar sucesos las aplicaciones como si se hubieran originado desde un dispositivo.

```

    myClient.connect()

    //Generar el suceso a ser publicado
    JsonObject event = new JsonObject();
    event.addProperty("name", "foo");
    event.addProperty("cpu",  60);
    event.addProperty("mem",  40);

    // publicar el suceso en nombre del dispositivo
    myClient.publishEvent(deviceType, deviceId, "blink", event);
```

### Publicar sucesos utilizando HTTP
{: #publishing_events_http}

Además de MQTT, puede configurar las aplicaciones para publicar sucesos de dispositivos en {{site.data.keyword.iot_short_notm}} utilizando HTTP llevando a cabo los pasos siguientes:

* Construir la instancia de ApplicationClient mediante el archivo de propiedades
* Construir el suceso que debe publicarse
* Especificar el nombre de suceso, el tipo de dispositivo y el ID de dispositivo
* Publicar el suceso utilizando el método `publishEventOverHTTP`(), tal como se muestra en el código siguiente:

```

    	ApplicationClient myClient = new ApplicationClient(props);

    	JsonObject event = new JsonObject();
    	event.addProperty("name", "foo");
    	event.addProperty("cpu",  90);
    	event.addProperty("mem",  70);

    	code = myClient.publishEventOverHTTP(deviceType, deviceId, "blink", event);
```

Para obtener el ejemplo de código completo, consulte el siguiente ejemplo de aplicación:

[HttpApplicationDeviceEventPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/HttpApplicationDeviceEventPublish.java)

En función de los valores del archivo de propiedades, el método `publishEventOverHTTP()` publica el suceso en Inicio rápido o en el flujo registrado. Cuando `quickstart` es el ID de organización que se especifica en el archivo de propiedades, el método `publishEventOverHTTP()` publica el suceso en el servicio Inicio rápido de {{site.data.keyword.iot_short_notm}} en formato HTTP plano. Cuando se especifica una organización registrada válida en el archivo de propiedades, el suceso siempre se publicará utilizando HTTPS, de forma que toda la comunicación esté protegida.

El protocolo HTTP proporciona una entrega 'at most once', que es similar al nivel de calidad de servicio 'at most once' (QoS 0) del protocolo MQTT. Al utilizar la entrega 'at most once' para publicar sucesos, la aplicación debe implementar la lógica de reintento cuando se produce un error.


## Publicación de mandatos en dispositivos
{: #publishing_commands_devices}

Las aplicaciones pueden publicar mandatos a los dispositivos conectados, como se muestra en el ejemplo siguiente:

```

    myClient.connect()

    //Generar el suceso a publicar
    JsonObject data = new JsonObject();
    data.addProperty("name", "stop-rotation");
    data.addProperty("delay",  0);

    //El flujo registrado permite QoS 0, 1 y 2
    myAppClient.publishCommand(deviceType, deviceId, "stop", data);
```


## Ejemplos
{: #examples}


-  [MQTTApplicationDeviceEventPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/MQTTApplicationDeviceEventPublish.java): Una aplicación de ejemplo que muestra cómo puede publicar sucesos de dispositivos.
-   [RegisteredApplicationCommandPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/RegisteredApplicationCommandPublish.java): Una aplicación de ejemplo que muestra cómo se puede publicar un mandato a un dispositivo.
-  [RegisteredApplicationSubscribeSample](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/RegisteredApplicationSubscribeSample.java): Una aplicación de ejemplo que muestra cómo puede suscribirse a distintos sucesos como por ejemplo sucesos de dispositivos, mandatos de dispositivos, estado de dispositivos y estado de aplicaciones.
-   [SharedSubscriptionSample](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/SharedSubscriptionSample.java): Una aplicación de ejemplo que muestra cómo se puede construir una aplicación escalable que equilibra la carga de mensajes entre varias instancias de la aplicación.
-  [Ejemplo de copia de seguridad y restauración](https://github.com/ibm-messaging/iot-backup-restore-sample): Un ejemplo que muestra cómo puede realizar una copia de seguridad y restaurar la configuración de dispositivos en una base de datos Cloudant NoSQL.
