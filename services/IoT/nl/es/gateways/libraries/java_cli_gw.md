---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-30"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

#Desarrollo de pasarelas en {{site.data.keyword.iot_short_notm}} mediante Java
{: #java_cli_gw}

Si los dispositivos no puede conectarse directamente a la organización en {{site.data.keyword.iot_full}}, puede crear y personalizar pasarelas utilizando Java™. Se proporciona una biblioteca de cliente de Java para {{site.data.keyword.iot_short_notm}}, documentación y ejemplos para ayudarle a comenzar con el desarrollo de pasarelas.
{:shortdesc}

## Descarga del cliente y los recursos de Java
{: #java_client_download}

Para acceder a las bibliotecas y a los ejemplos de cliente Java para {{site.data.keyword.iot_short_notm}}, vaya al repositorio [iot-java](https://github.com/ibm-watson-iot/iot-java) en GitHub y complete las instrucciones de instalación.

## Constructor
{: #constructor}

El constructor compila la instancia del cliente de pasarela y acepta el objeto `Properties`, que contiene las siguientes definiciones:

|Definición |Descripción |
|:----|:----|
|`org`|Un valor necesario que debe establecerse en el ID de la organización. Si está utilizando un flujo de Quickstart, especifique `quickstart`.|
|`domain`|El URL de punto final de mensajería, que es opcional. Si no especifica un valor para un dominio, el URL adopta como valor predeterminado `internetofthings.ibmcloud.com`, que es el servidor de producción de {{site.data.keyword.iot_short_notm}}.|
|`type`|Un valor obligatorio que especifica el tipo de pasarela.|
|`id` |Un valor obligatorio que especifica el ID exclusivo de la pasarela.|
|`auth-method`|El método de autenticación que debe utilizarse. El único método al que se da soporte es `token`.|
|`auth-token`|Una señal de autenticación de clave de API para conectar de forma segura la pasarela a {{site.data.keyword.iot_short_notm}}.|
|`clean-session`|Un valor true o false que sólo es necesario si desea conectar la pasarela en modalidad de suscripción duradera. De forma predeterminada, `clean-session` se establece en true.|
|`WebSocket`|Un valor true o false que sólo es necesario si desea conectar la pasarela mediante websockets.|
|`Port`|El número de puerto al que conectarse. Especifique 8883 o 443. Si no especifica un número de puerto, el cliente se conectará a {{site.data.keyword.iot_short_notm}} en el número de puerto 8883 de forma predeterminada.|
|`MaxInflightMessages`|Establece el número máximo de mensajes en vuelo para la conexión. El valor predeterminado es 100.|
|`Automatic-Reconnect`|Un valor true o false que es necesario cuando desea que la pasarela se conecte automáticamente a {{site.data.keyword.iot_short_notm}} mientras se encuentra en un estado desconectado. El valor predeterminado es false.|
|`Disconnected-Buffer-Size`|El número máximo de mensajes que se pueden almacenar en memoria mientras el cliente está desconectado. El valor predeterminado es 5000.|

**Nota:** Para conectar la pasarela en modalidad de suscripción duradera, establezca `clean-session` en `false`. Para obtener más información sobre la sesión limpia, consulte la sección 'Almacenamientos intermedios de suscripción y sesión limpia' de la [documentación de MQTT](../../reference/mqtt/index.html#subscription-buffers-and-clean-session).

El objeto `Propiedades` crea definiciones que se utilizan para interactuar con el módulo de {{site.data.keyword.iot_short_notm}}.

El ejemplo de código siguiente muestra cómo crear una instancia de cliente de pasarela:

```java
Properties options = new Properties();
options.setProperty("org", "<Your organization ID>");
options.setProperty("type", "<The gateway device type>");
options.setProperty("id", "The gateway device ID");
options.setProperty("auth-method", "token");
options.setProperty("auth-token", "API token");
GatewayClient gwClient = new GatewayClient(options);

```


### Utilización de un archivo de configuración

En lugar de utilizar el objeto `Properties` directamente para crear una instancia de pasarela, puede utilizar un archivo de configuración que contenga los pares nombre-valor para las propiedades de la pasarela. Para utilizar un archivo de configuración para crear el objeto `Properties` para la pasarela, utilice el siguiente formato de código:

```Java
Properties props = GatewayClient.parsePropertiesFile(new File("C:\\temp\\device.prop"));
GatewayClient gwClient = new GatewayClient(props);
...
```

El contenido del archivo de configuración debe estar en el formato siguiente:

```java
[Gateway]
org=$orgId
domain=$domain
typ=$myGatewayDeviceType
id=$myGatewayDeviceId
auth-method=token
auth-token=$token

```

## Conexión con {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

Para conectarse a {{site.data.keyword.iot_short_notm}}, utilice la función `connect()`. La función `connect()` incluye un parámetro booleano opcional denominado `autoRetry`, que determina si la biblioteca intenta volver a conectarse cuando haya un fallo de conexión con una excepción de MQTT (MqttException). De forma predeterminada, `autoRetry` se establece en true. Si falla una conexión MqttSecurityException porque se pasan detalles de registro de dispositivos incorrectos, la biblioteca no intentará volver a conectarse, incluso aunque `autoRetry` esté establecido en true.

Para establecer el intervalo keep alive para MQTT, puede utilizar opcionalmente el método `setKeepAliveInterval(int)` antes de llamar a la función `connect()`. El valor `setKeepAliveInterval(int)` se mide en segundos y define el intervalo de tiempo máximo entre mensajes que se han enviado o recibido. Cuando se especifica un valor `setKeepAliveInterval(int)`, el cliente puede detectar cuándo ya no está disponible el servidor sin esperar a que finalice el periodo de tiempo de espera de TCP/IP. El cliente garantiza que al menos un mensaje viaja por la red dentro de cada periodo de intervalo de keep alive. Si se reciben mensajes relacionados con datos cero durante el periodo de tiempo de espera, el cliente envía un mensaje `ping` pequeño, el cual reconoce el servidor. El `setKeepAliveInterval(int)` se establece en 60 segundos de forma predeterminada. Para inhabilitar la característica de proceso keep alive en el cliente, establezca el valor `setKeepAliveInterval(int)` en 0.

```java
Properties props = GatewayClient.parsePropertiesFile(new File("C:\\temp\\device.prop"));
GatewayClient gwClient = new GatewayClient(props);
gwClient.setKeepAliveInterval(80);
gwClient.connect();
```

Para controlar el número de reintentos que se producen cuando hay una anomalía de conexión, utilice la función overloaded connect(int numberOfTimesToRetry).

```java
GatewayClient gwClient = new GatewayClient(props);
gwClient.setKeepAliveInterval(80);
gwClient .connect(10);
```

Después de que el cliente de pasarela se conecta correctamente a {{site.data.keyword.iot_short_notm}}, la pasarela puede publicar sucesos y suscribirse a mandatos para sí misma y también en nombre de los dispositivos conectados a la pasarela.

## Registro de dispositivos que están detrás de la pasarela
{: #register_device_gateway}

Puede registrar dispositivos que están detrás de la pasarela conectada a la instancia de {{site.data.keyword.iot_short_notm}} de forma automática o mediante el desarrollo de código utilizando la API.

### Registro automático de dispositivos
Puede registrar sus dispositivos en {{site.data.keyword.iot_short_notm}} automáticamente siempre que la pasarela publica cualquier suceso o se suscribe a cualquier mandato para los dispositivos conectados a la misma.

### Registro de dispositivos mediante API
También puede utilizar la API de {{site.data.keyword.iot_short_notm}} para registrar dispositivos que están detrás de una pasarela en su instancia {{site.data.keyword.iot_short_notm}}.

Para simplificar el desarrollo con la API de {{site.data.keyword.iot_short_notm}}, inicie una instancia de cliente de API invocando al método api(), tal como se muestra en el ejemplo de código siguiente:

```java
import com.ibm.iotf.client.api.APIClient;
....

GatewayClient gwClient = new GatewayClient(props);
gwClient.connect();

APIClient api = gwClient.api();
```
Cuando reciba el manejador del cliente de API, puede empezar a registrar dispositivos en una pasarela, tal como se muestra en el ejemplo de código siguiente:

```java
gwClient.connect();

  String deviceToBeAdded = "{\"deviceId\": \"" + DEVICE_ID +
					"\",\"authToken\": \"qwer123\"}";

    JsonParser parser = new JsonParser();
    JsonElement input = parser.parse(deviceToBeAdded);
    JsonObject response = this.gwClient.api().registerDeviceUnderGateway(DEVICE_TYPE, gwDeviceId, gwDeviceType, input);

```

Cuando se registra un dispositivo que está detrás de una pasarela, el dispositivo se asocia a la pasarela mediante los valores de los atributos `gwDeviceId` y `gwDeviceType`.

## Publicación de sucesos
{: #publish_events}

Los sucesos son el mecanismo por el que las pasarelas y los dispositivos publican datos en {{site.data.keyword.iot_short_notm}}. La pasarela o el dispositivo controla el contenido del suceso y asigna un nombre a cada suceso que envía. Una pasarela puede publicar sucesos de sí misma y en nombre de cualquier dispositivo que esté conectado a través de la pasarela.

Cuando una instancia de {{site.data.keyword.iot_short_notm}} recibe un suceso, las credenciales del suceso recibido identifican la pasarela de envío, lo que significa que una pasarela no puede suplantar a otro dispositivo.

Los sucesos se pueden publicar en cualquiera de los tres [niveles de calidad de servicio (QoS)](../../reference/mqtt/index.html#qos-levels) definidos por el protocolo MQTT.  De forma predeterminada, los sucesos se publican en QoS=0.

### Código para publicar sucesos de pasarela de nivel de QoS predeterminado

```java
gwClient.connect();
  JsonObject event = new JsonObject();
  event.addProperty("name", "foo");
  event.addProperty("cpu",  90);
  event.addProperty("mem",  70);

gwClient.publishGatewayEvent("status", event);
```

### Código para aumentar el nivel de QoS predeterminado para un suceso

Puede aumentar los [niveles de QoS](../../reference/mqtt/index.html#qos-levels) para los sucesos de pasarela que se publican. Los sucesos que tienen un nivel de QoS mayor que cero pueden tardar un poco más en publicarse, debido a la información de recepción de confirmación adicional que se incluye.


```java
gwClient.connect();
  JsonObject event = new JsonObject();
  event.addProperty("name", "foo");
  event.addProperty("cpu",  90);
  event.addProperty("mem",  70);

gwClient.publishGatewayEvent("status", event, 2);
```

### Código para publicar sucesos en formatos personalizados

Los sucesos se pueden publicar en distintos formatos, por ejemplo, JSON, serie, binario, etc. De forma predeterminada, la biblioteca publica sucesos en formato JSON, pero puede especificar los datos en distintos formatos si lo prefiere. Por ejemplo, para publicar datos en el formato de serie de caracteres, utilice el siguiente fragmento de código:

```java
gwClient.connect();
String data = "cpu:80";
boolean status = gwClient.publishGatewayEvent("load", data, "text", 2);
```

**Nota:** En el ejemplo de código anterior, la carga útil del suceso debe estar en formato de serie.

Los datos XML se pueden convertir a formato de serie y publicarse tal como se indica en el siguiente ejemplo de código:

```java
status = gwClient.publishGatewayEvent("load", xmlConvertedString, "xml", 2);
```

De forma similar, para publicar sucesos en formato binario, utilice la matriz de bytes que se describe en el ejemplo siguiente:

```java
gwClient.connect();
byte[] cpuLoad = new byte[] {30, 35, 30, 25};
status = gwClient.publishGatewayEvent("blink", cpuLoad , "binary", 1);
```

### Código para publicar sucesos procedentes de dispositivos
{: #publishing_events_devices}

Una pasarela puede publicar sucesos en nombre de cualquier dispositivo que esté conectado a través de la pasarela transfiriendo los valores adecuados de ID de tipo e ID de dispositivo del suceso original, tal como se muestra en el siguiente ejemplo:

```java

gwClient.connect()

//Generar el suceso a ser publicado
    JsonObject event = new JsonObject();
    event.addProperty("name", "foo");
    event.addProperty("cpu",  60);
    event.addProperty("mem",  40);

// publicar el suceso en nombre del dispositivo
gwClient.publishDeviceEvent(deviceType, deviceId, eventName, event);
```

Utilice el método `publishDeviceEvent()` sobrecargado para publicar el suceso en el nivel de calidad de servicio que desee. Para obtener más información sobre la estructura de temas que se utiliza, consulte [Conectividad MQTT para pasarelas](../mqtt.html).

### Código para publicar sucesos de dispositivo en formato personalizado

AL igual que sucede con los sucesos de pasarela, los sucesos de dispositivo también se puede publicar en distintos formatos. De forma predeterminada, la biblioteca publica los sucesos de dispositivo en formato JSON, pero puede especificar los datos en distintos formatos si lo prefiere. Por ejemplo, para publicar datos en el formato de serie de caracteres, utilice el siguiente ejemplo de código:

```java
gwClient.connect();
String data = "cpu:80";
boolean status = gwClient.publishDeviceEvent(deviceType, deviceId, "load", data, "text", 2);
```

**Nota:** la carga útil del suceso debe estar en formato de serie.

Los datos XML se pueden convertir a formato de serie y publicarse tal como se muestra en el siguiente ejemplo:

```java
status = gwClient.publishDeviceEvent(deviceType, deviceId, "load", xmlConvertedString, "xml", 2);
```

De forma similar, para publicar sucesos de dispositivo en formato binario, utilice la matriz de bytes que se describe en el ejemplo siguiente:
```java
gwClient.connect();
byte[] cpuLoad = new byte[] {30, 35, 30, 25};
status = gwClient.publishDeviceEvent(deviceType, deviceId, "blink", cpuLoad , "binary", 1);
```

## Manejo de mandatos
{: #handling_commands}

La pasarela puede suscribirse a los mandatos que se direccionan a la propia pasarela y a cualquier dispositivo conectado detrás de la pasarela. Cuando el cliente de pasarela se conecta, se suscribe automáticamente a todos los mandatos para esta pasarela. Pero, para suscribirse a cualquier mandato para los dispositivos conectados a través de la pasarela, utilice el método sobrecargado `subscribeToDeviceCommands()` tal como se muestra en el ejemplo siguiente:

```java
gwClient.connect()

// suscribirse a mandatos en nombre del dispositivo
gwClient.subscribeToDeviceCommands(DEVICE_TYPE, DEVICE_ID);
```

Para procesar mandatos específicos, necesita registrar un método callback `Command`. Los mensajes se devuelven como una instancia de la clase `Command` y contienen las siguientes propiedades:


| Propiedad     |Tipos de datos     | Descripción|
|----------------|----------------|---------------
|`deviceType`|Serie| El tipo de dispositivo para el que se recibe el mandato.|
|`deviceId`|Serie| El ID de dispositivo para el que se recibe el mandato, que puede ser la pasarela o un dispositivo que está conectado a través de la pasarela.|
|`data`|Objeto| La carga útil de mandatos.|
|`format`|Serie| El formato de la carga útil de mandatos, que puede ser cualquier serie, como por ejemplo JSON. binary, texto y otros.|
|`command`|Serie|El nombre del mandato.|
|`timestamp`|org.joda.time.DateTime|La fecha y hora en que se envió el mandato.|

En el ejemplo de código siguiente se describe cómo puede implementar el método de devolución de llamada `Command`:

```java
import com.ibm.iotf.client.gateway.Command;
import com.ibm.iotf.client.gateway.GatewayCallback;

public class GatewayCommandCallback implements GatewayCallback, Runnable {
	// Una cola para albergar y procesar los mandatos
	private BlockingQueue<Command> queue = new LinkedBlockingQueue<Command>();

	public void processCommand(Command cmd) {
  	    queue.put(cmd);
  	}

  	public void run() {
  	    while(true) {
  	        Command cmd = queue.take();
  	        System.out.println("Command " + cmd.getData());

  	        // código para procesar el mandato
  	    }
  	}

  	/**
	 * Si una pasarela se suscribe a un tema de un dispositivo o envía datos en nombre de un dispositivo al
	 * que dicha pasarela no tiene permiso para conectarse, el mensaje o la suscripción se pasan por alto.
	 * Este comportamiento es distinto del comportamiento de las aplicaciones, en las que la conexión finaliza.
	 * Se notifica a la pasarela en el siguiente tema de notificación:
	 */
  	@Override
public void processNotification(Notification notification) {

}
  }

```
Cuando se añade la devolución de llamada `Command` al cliente de pasarela, se invoca el método `processCommand()` siempre que se publica un mandato que tiene los criterios suscritos.

En el ejemplo de código siguiente se describe cómo añadir la devolución de llamada `Command` a la instancia de cliente de pasarela.

```java
gwClient.connect()
GatewayCommandCallback callback = new GatewayCommandCallback();
gwClient.setGatewayCallback(callback);
//Suscripción a un dispositivo conectado a la pasarela
gwClient.subscribeToDeviceCommands(DEVICE_TYPE, DEVICE_ID);
```

Hay disponibles métodos sobrecargados para controlar la suscripción de mandatos.

### Listado de los dispositivos conectados a través de una pasarela
{: #list_devices_gw}


Para recuperar todos los dispositivos que están conectados a través de la pasarela especificada (typeId, deviceId) a {{site.data.keyword.iot_short_notm}}, invoque el método `getDevicesConnectedThroughGateway()`.

```java
gwClient.connect()
gwClient.api().getDevicesConnectedThroughGateway(gatewayType, gatewayId);
```

## Ejemplos
{: #samples}

Dispone de varios ejemplos para ayudarle a conectar pasarelas y dispositivos situados detrás de pasarelas a su instancia de {{site.data.keyword.iot_short_notm}}. En los ejemplos se utiliza la biblioteca cliente Java de {{site.data.keyword.iot_short_notm}} y se encuentran en el [Repositorio GitHub de ejemplos de pasarela](https://github.com/ibm-messaging/iot-gateway-samples/tree/master/java/gateway-samples).

## Recetas
{: #recipes}

| Receta     | Descripción|
|----------------|----------------
|[Conexión de un dispositivo como pasarela a {{site.data.keyword.iot_short_notm}}](https://developer.ibm.com/recipes/tutorials/connect-raspberry-pi-as-gateway-to-watson-iot-platform/)| Un proyecto GitHub e instrucciones detalladas que indican cómo conectar una pasarela Raspberry Pi y dispositivos Arduino Uno tras la pasarela a {{site.data.keyword.iot_short_notm}}.
|[Raspberry Pi como pasarela gestionada en {{site.data.keyword.iot_short_notm}} ](https://developer.ibm.com/recipes/tutorials/raspberry-pi-as-managed-gateway-in-watson-iot-platform-part-1/)|Una extensión de la receta de pasarela anterior que explica cómo conectar la pasarela Raspberry Pi como dispositivos gestionado en {{site.data.keyword.iot_short_notm}} y cómo realizar operaciones de gestión de dispositivos.
