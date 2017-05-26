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

# Java para desarrolladores de aplicaciones
{: #java}


Puede crear y personalizar aplicaciones que interactúan con su organización en {{site.data.keyword.iot_full}} utilizando Java™. Se proporciona una biblioteca de cliente Java para {{site.data.keyword.iot_short_notm}}, documentación y ejemplos para ayudarle a iniciarse con el desarrollo de aplicaciones.

{:shortdesc}

## Descarga del cliente y los recursos de Java
{: #java_client_download}

Última actualización: 25 de octubre de 2016
{: .last-updated}

Para acceder a las bibliotecas y ejemplos de cliente de Java para {{site.data.keyword.iot_short_notm}}, vaya al repositorio [iot-java ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ibm-watson-iot/iot-java){: new_window} en GitHub y complete las instrucciones de instalación.


## Constructor
{: #constructor}

El constructor compila la instancia del cliente y acepta el objeto `Properties`, que contiene las siguientes definiciones:

| Definición     |Descripción     |
|----------------|----------------|
|`org` |Un valor necesario que debe establecerse en el ID de la organización. Si está utilizando un flujo de Quickstart, especifique `quickstart`.|
|`id` |El ID exclusivo de la aplicación en su organización.|
|`auth-method`  |El método de autenticación. El único método al que se da soporte es `apikey`.|
|`auth-key`   |Una clave de API opcional, que debe especificar al establecer el valor de auth-method en `apikey`.|
|`auth-token`   |Una señal de clave API, que también es obligatoria al establecer el valor de auth-method en `apikey`. |
|`clean-session`|Un valor true o false que sólo es necesario si desea conectar la aplicación en modalidad de suscripción duradera. De forma predeterminada, `clean-session` se establece en `true`.|
|`Port`|El número de puerto al que conectarse. Especifique 8883 o 443. Si no especifica un número de puerto, el cliente se conectará a {{site.data.keyword.iot_short_notm}} en el número de puerto 8883 de forma predeterminada.|
|`MaxInflightMessages`  |Establece el número máximo de mensajes en vuelo para la conexión. El valor predeterminado es 100.|
|`Automatic-Reconnect`  |Un valor true o false que es necesario cuando desea que el dispositivo se conecte automáticamente a {{site.data.keyword.iot_short_notm}} mientras se encuentra en un estado desconectado. El valor predeterminado es false.|
|`Disconnected-Buffer-Size`|El número máximo de mensajes que se pueden almacenar en memoria mientras el cliente está desconectado. El valor predeterminado es 5000.|
|`shared-subscription`|Un valor booleano que se debe establecer en true si desea compilar aplicaciones escalables que equilibran la carga de mensajes en varias instancias de la aplicación. Para obtener más información, consulte [Aplicaciones escalables](../mqtt.html#scalable_apps).

El objeto `Propiedades` crea definiciones que se utilizan para interactuar con el módulo de {{site.data.keyword.iot_short_notm}}. Si no especifica las propiedades para este objeto, o si especifica `quickstart`, el cliente se conecta al servicio de Inicio rápido de {{site.data.keyword.iot_short_notm}} como un dispositivo no registrado.

El ejemplo de código siguiente muestra cómo puede construir la instancia del cliente de aplicaciones (`ApplicationClient`) en modalidad `quickstart`:

```
    import com.ibm.iotf.client.app.ApplicationClient;
    import java.util.Properties;

    Properties options = new Properties();
    options.put("org", "quickstart");

    ApplicationClient myClient = new ApplicationClient(options);
```

El ejemplo de código siguiente muestra cómo puede construir la instancia del cliente de aplicaciones (`ApplicationClient`) en modalidad de flujo registrada:

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

En lugar de incluir el objeto `Propiedades` directamente, puede utilizar un archivo de configuración que contenga los pares nombre-valor para el objeto `Propiedades`, como se resalta en el siguiente ejemplo de código:

```
    Properties props = ApplicationClient.parsePropertiesFile(new File("C:\\temp\\application.prop"));
    ApplicationClient myClient = new ApplicationClient(props);
    ...
```
El archivo de configuración de aplicación especificado debe estar en el formato siguiente:

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

Para conectarse a {{site.data.keyword.iot_short_notm}}, utilice la función `connect()`. La función `connect()` incluye un parámetro booleano opcional que se llama `autoRetry`, que determina si la biblioteca intenta volver a conectarse cuando haya un fallo de conexión a MqttException. De forma predeterminada, `autoRetry` se establece en true. Si falla una conexión MqttSecurityException porque se pasan detalles de registro de dispositivos incorrectos, la biblioteca no intentará volver a conectarse, incluso aunque `autoRetry` esté establecido en true.

Para establecer el intervalo 'keep alive' para MQTT, puede utilizar opcionalmente el método `setKeepAliveInterval(int)` antes de llamar a la función `connect()`. El valor `setKeepAliveInterval(int)` se mide en segundos, y define el intervalo de tiempo máximo entre mensajes que se han enviado o recibido. Cuando se utiliza, el cliente puede detectar cuándo ya no está disponible el servidor sin esperar a que finalice el periodo de tiempo de espera de TCP/IP. El cliente garantiza que al menos un mensaje viaja por la red dentro de cada periodo de intervalo de 'keep alive'. Si se reciben mensajes relacionados con datos cero durante el periodo de tiempo de espera, el cliente envía un mensaje `ping` pequeño, el cual reconoce el servidor. El `setKeepAliveInterval(int)` se establece en 60 segundos de forma predeterminada. Para inhabilitar la característica de proceso 'keep alive' en el cliente, establezca el valor `setKeepAliveInterval(int)` en 0.

```
    Properties props = ApplicationClient.parsePropertiesFile(new File("C:\\temp\\application.prop"));
    ApplicationClient myClient = new ApplicationClient(props);
    myClient.setKeepAliveInterval(120);
    myClient.connect();
```

Para controlar el número de reintentos que se producen cuando hay una anomalía de conexión, especifique un entero en la función myClient.connect(), tal como se describe en el siguiente fragmento de código:

```
    DeviceClient myClient = new DeviceClient(options);
    myClient.setKeepAliveInterval(120);
    myClient.connect(10);
```

Una vez que los clientes de la aplicación se hayan conectado correctamente al servicio de {{site.data.keyword.iot_short_notm}}, pueden suscribirse a los sucesos y estados de dispositivos, y también pueden publicar los sucesos y mandatos del dispositivo.

## Suscripción a sucesos de dispositivos
{: #subscribing_device_events}

Los sucesos son el mecanismo por el que los dispositivos publican datos en {{site.data.keyword.iot_short_notm}}. El dispositivo controla el contenido del suceso y asigna un nombre a cada suceso que envía.

Cuando una instancia de {{site.data.keyword.iot_short_notm}} recibe un suceso, las credenciales del suceso recibido identifican el dispositivo de envío, lo que significa que un dispositivo no puede suplantar a otro dispositivo.


De forma predeterminada, las aplicaciones se suscriben a todos los sucesos desde todos los dispositivos conectados. Utilice los parámetros device type, device ID, event y message-format para controlar el ámbito de la suscripción. Los siguientes ejemplos de código muestran cómo puede utilizar estos parámetros para definir el ámbito de una suscripción:

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
|`event.deviceType`|Serie|Identifica el tipo de dispositivo. Normalmente, el deviceType es una agrupación para los dispositivos que realizan una tarea específica, como por ejemplo "weatherballoon" podría ser un tipo de dispositivo.|
|`event.deviceId`|Serie|Representa el ID del dispositivo. Normalmente, para un tipo de dispositivo específico, el deviceId es un identificador exclusivo de dicho dispositivo, por ejemplo un número de serie o una dirección MAC.|
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

De forma parecida a la suscripción a sucesos de dispositivos, las aplicaciones pueden suscribirse al estado del dispositivo, como por ejemplo la conexión y desconexión del dispositivo a {{site.data.keyword.iot_short_notm}}. De forma predeterminada, esta suscripción se suscribe a las actualizaciones de estado para todos los dispositivos conectados. Utilice los parámetros device type y device ID para controlar el ámbito de la suscripción. Los siguientes ejemplos de código muestran cómo puede utilizar estos parámetros para definir el ámbito de una suscripción:

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

Cuando se añade el callback de estado al cliente de la aplicación, se invocará el método `processDeviceStatus()` siempre que un dispositivo que coincida con los criterios se conecte o se desconecte del {{site.data.keyword.iot_short_notm}}. El ejemplo de código siguiente muestra cómo se puede añadir la instancia de callback de estado al cliente de la aplicación:

```

    myClient.connect()
    myClient.setStatusCallback(new MyStatusCallback());
    myClient.subscribeToDeviceStatus();
```
Las aplicaciones pueden suscribirse a cualquier otro estado de aplicación, como la conexión y desconexión de la aplicación a {{site.data.keyword.iot_short_notm}}. El siguiente fragmento de código muestra cómo suscribirse al estado de la aplicación de una organización de {{site.data.keyword.iot_short_notm}}:

```
    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToApplicationStatus();
```
El método sobrecargado está disponible para controlar la suscripción de estado a una aplicación particular. El método `processApplicationStatus()` se invoca siempre que se conecta o se desconecta una aplicación que coincide con los criterios del {{site.data.keyword.iot_short_notm}}.


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


Los sucesos se pueden publicar en distintos formatos, por ejemplo, JSON, serie, binario, etc. De forma predeterminada, la biblioteca publica sucesos en formato JSON, pero puede especificar los datos en distintos formatos si lo prefiere. Por ejemplo, para publicar datos en el formato de serie, utilice el siguiente fragmento de código.

```
    myClient.connect();
    String data = "cpu:"+60;
    status = myClient.publishEvent("load", data, "text", 2);
```
**Nota:** En el ejemplo de código anterior, la carga útil del suceso debe estar en formato de serie.

Cualquier dato XML se puede convertir a serie y publicarse como se indica a continuación:

```
    status = myClient.publishEvent("load", xmlConvertedString, "xml", 2);
```

De forma similar, para publicar sucesos en formato binario, utilice la matriz de bytes, tal como se describe en el ejemplo siguiente:

```
    myClient.connect();
    byte[] cpuLoad = new byte[] {60, 35, 30, 25};
    status = myClient.publishEvent("blink", cpuLoad , "binary", 1);
```

### Publicar sucesos utilizando HTTP
{: #publishing_events_http}

Además de utilizar MQTT, también puede configurar las aplicaciones para publicar sucesos de dispositivos en {{site.data.keyword.iot_short_notm}} mediante HTTP. En los pasos siguientes se describe la secuencia para publicar sucesos de dispositivos a través de HTTP:

1. Construir la instancia de ApplicationClient mediante el archivo de propiedades.
2. Construir el suceso que debe publicarse.
3. Especificar el nombre de suceso, el tipo de dispositivo y el ID de dispositivo.
4. Publicar el suceso utilizando el método `publishEventOverHTTP`(), tal como se muestra en el ejemplo de código siguiente:

```
    	ApplicationClient myClient = new ApplicationClient(props);

    	JsonObject event = new JsonObject();
    	event.addProperty("name", "foo");
    	event.addProperty("cpu",  90);
    	event.addProperty("mem",  70);

    	boolean status = myClient.publishApplicationEventforDeviceOverHTTP(deviceId, deviceType, "blink", event, ContentType.json);
```

Para obtener el ejemplo de código completo, consulte el ejemplo de aplicación de [HttpApplicationDeviceEventPublish ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/HttpApplicationDeviceEventPublish.java){: new_window}.

En función de los valores del archivo de propiedades, el método `publishEventOverHTTP()` publica el suceso en Inicio rápido o en el flujo registrado. Cuando se especifica `quickstart` como el ID de organización en el archivo de propiedades, el método `publishEventOverHTTP()` publica el suceso en el servicio Inicio rápido de {{site.data.keyword.iot_short_notm}} en formato HTTP sin formato. Cuando se especifica una organización registrada válida en el archivo de propiedades, el suceso siempre se publicará utilizando HTTPS, de forma que toda la comunicación esté protegida.

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

### Publicar mandatos utilizando HTTP
{: #publishing_commands_http}

Además de utilizar MQTT, también puede configurar las aplicaciones para publicar mandatos en el dispositivo conectado mediante HTTP. En los pasos siguientes se describe la secuencia para publicar sucesos de dispositivos mediante HTTP:

1. Construir la instancia de ApplicationClient mediante el archivo de propiedades
2. Construir el mandato que debe publicarse
3. Especificar el nombre de mandato, el tipo de dispositivo y el ID de dispositivo
4. Publicar el mandato utilizando el método `publishCommandOverHTTP`(), tal como se muestra en el código siguiente:

```

    	ApplicationClient myClient = new ApplicationClient(props);

    	// Generar un objeto JSON del suceso que se va a publicar
	JsonObject event = new JsonObject();
	event.addProperty("reboot", 5);

	boolean response = myClient.publishCommandOverHTTP("execute", event);
```

Para ver el ejemplo de código completo, consulte el ejemplo de aplicación de [HttpCommandPublish ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/HttpCommandPublish.java){: new_window}.

El protocolo HTTP proporciona una entrega 'at most once', que es similar al nivel de calidad de servicio 'at most once' (QoS 0) del protocolo MQTT. Al utilizar la entrega 'at most once' para publicar mandatos, la aplicación debe implementar la lógica de reintento cuando se produce un error. Para obtener más información, consulte [API REST HTTP para aplicaciones](../api.html).


## Ejemplos
{: #samples}

-  [MQTTApplicationDeviceEventPublish ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/MQTTApplicationDeviceEventPublish.java){: new_window}: Una aplicación de ejemplo que muestra cómo puede publicar sucesos de dispositivo.
-   [RegisteredApplicationCommandPublish ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/RegisteredApplicationCommandPublish.java){: new_window}: Una aplicación de ejemplo que muestra cómo puede publicar un mandato en un dispositivo.
-  [RegisteredApplicationSubscribeSample ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/RegisteredApplicationSubscribeSample.java){: new_window}: Una aplicación de ejemplo que muestra cómo puede suscribirse a distintos sucesos como por ejemplo sucesos de dispositivos, mandatos de dispositivos, estado de dispositivos y estado de aplicaciones.
-   [SharedSubscriptionSample ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/SharedSubscriptionSample.java){: new_window}: Una aplicación de ejemplo que muestra cómo se puede construir una aplicación escalable que equilibra la carga de mensajes entre varias instancias de la aplicación.
-  [Backup-restore-sample ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ibm-messaging/iot-backup-restore-sample){: new_window}: Un ejemplo que muestra cómo puede realizar una copia de seguridad y restaurar la configuración de dispositivos en {{site.data.keyword.cloudant}}.
