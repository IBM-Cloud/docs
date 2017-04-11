---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-10-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Java para desarrolladores de dispositivos
{: #java}

Puede crear y personalizar dispositivos que interactúan con su organización en {{site.data.keyword.iot_full}} utilizando Java™. Se proporciona una biblioteca de cliente de Java para {{site.data.keyword.iot_short_notm}}, documentación y ejemplos para ayudarle a comenzar con el desarrollo de dispositivos.
{:shortdesc}

## Descarga del cliente y los recursos de Java
{: #java_client_download}

Para acceder a las bibliotecas y a los ejemplos de cliente Java para {{site.data.keyword.iot_short_notm}}, vaya al repositorio [iot-java](https://github.com/ibm-watson-iot/iot-java) en GitHub y complete las instrucciones de instalación.

## Constructor
{: #constructor}

El constructor compila la instancia del cliente y acepta el objeto `Properties`, que contiene las siguientes definiciones:

|Definición |Descripción |
|:----|:----|
|`org` |Un valor necesario que debe establecerse en el ID de la organización. Si está utilizando un flujo de Quickstart, especifique `quickstart`.|
|`type`  |Un valor obligatorio que especifica el tipo de dispositivo.|
|`id`  |Un valor obligatorio que especifica el ID exclusivo del dispositivo.|
|`auth-method`  |El método de autenticación que debe utilizarse. El único método al que se da soporte es `token`.|
|`auth-token`   |Una señal de autenticación para conectar de forma segura el dispositivo a {{site.data.keyword.iot_short_notm}}.|
|`clean-session`|Un valor true o false que sólo es necesario si desea conectar la aplicación en modalidad de suscripción duradera. De forma predeterminada, `clean-session` se establece en true.|
|`Port`|El número de puerto al que conectarse. Especifique 8883 o 443. Si no especifica un número de puerto, el cliente se conectará a {{site.data.keyword.iot_short_notm}} en el número de puerto 8883 de forma predeterminada.|
|`MaxInflightMessages`  |Establece el número máximo de mensajes en vuelo para la conexión. El valor predeterminado es 100.|
|`Automatic-Reconnect`  |Un valor true o false que es necesario cuando desea que el dispositivo se conecte automáticamente a {{site.data.keyword.iot_short_notm}} mientras se encuentra en un estado desconectado. El valor predeterminado es false.|
|`Disconnected-Buffer-Size`|El número máximo de mensajes que se pueden almacenar en memoria mientras el cliente está desconectado. El valor predeterminado es 5000.|
|`WebSocket`|Un valor true o false que es necesario si desea utilizar conexiones websockets con {{site.data.keyword.iot_short_notm}}. El valor predeterminado es false.|

**Nota:** Para conectar el dispositivo en modalidad de suscripción duradera, establezca `clean-session` en `false`. Para obtener más información sobre la sesión limpia, consulte la sección 'Almacenamientos intermedios de suscripción y sesión limpia' de la [documentación de MQTT](../../reference/mqtt/index.html#subscription-buffers-and-clean-session).

El objeto `Propiedades` crea definiciones que se utilizan para interactuar con el módulo de {{site.data.keyword.iot_short_notm}}.

El ejemplo de código siguiente muestra cómo pueden publicar los dispositivos sucesos en la modalidad de Inicio rápido.

```
package com.ibm.iotf.sample.client.device;

import java.util.Properties;

import com.google.gson.JsonObject;
import com.ibm.iotf.client.device.DeviceClient;

public class QuickstartDeviceEventPublish {

    public static void main(String[] args) {

        //Proporcionar los datos específicos del dispositivo utilizando la clase Properties
        Properties options = new Properties();
        options.setProperty("org", "quickstart");
        options.setProperty("type", "iotsample-arduino");
        options.setProperty("id", "00aabbccde03");

        DeviceClient myClient = null;
        try {
            //Instanciar la clase pasando el archivo de propiedades
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Conectar al {{site.data.keyword.iot_short_notm}}
        myClient.connect();

        //Generar un objeto JSON del suceso que se va a publicar
        JsonObject event = new JsonObject();
        event.addProperty("name", "foo");
        event.addProperty("cpu",  90);
        event.addProperty("mem",  70);

        //El flujo de Inicio rápido permite sólo QoS = 0
        myClient.publishEvent("status", event, 0);
        System.out.println("SUCCESSFULLY POSTED......");

  ...
```

El ejemplo de código siguiente muestra cómo pueden publicar los dispositivos sucesos en un flujo registrado.


```
package com.ibm.iotf.sample.client.device;

import java.util.Properties;

import com.google.gson.JsonObject;
import com.ibm.iotf.client.device.DeviceClient;

public class RegisteredDeviceEventPublish {

    public static void main(String[] args) {

        //Proporcionar los datos específicos del dispositivo, así como Auth-key y token utilizando la clase Properties
        Properties options = new Properties();

        options.setProperty("org", "uguhsp");
        options.setProperty("type", "iotsample-arduino");
        options.setProperty("id", "00aabbccde03");
        options.setProperty("auth-method", "token");
        options.setProperty("auth-token", "AUTH TOKEN FOR DEVICE");

        DeviceClient myClient = null;
        try {
            //Instanciar la clase pasando el archivo de propiedades
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Conectar al {{site.data.keyword.iot_short_notm}}
        myClient.connect();

        //Generar un objeto JSON del suceso que se va a publicar
        JsonObject event = new JsonObject();
        event.addProperty("name", "foo");
        event.addProperty("cpu",  90);
        event.addProperty("mem",  70);

        //El flujo registrado permite 0, 1 y 2 QoS
        myClient.publishEvent("status", event);
        System.out.println("SUCCESSFULLY POSTED......");

  ...
```

### Utilización de un archivo de configuración

En lugar de utilizar el objeto `Propiedades` directamente, puede utilizar un archivo de configuración que contenga los pares name-value para las propiedades. Si está utilizando un archivo de configuración que contiene el objeto `Propiedades`, utilice el siguiente formato de código:

```
package com.ibm.iotf.sample.client.device;

import java.io.File;
import java.util.Properties;

import com.google.gson.JsonObject;
import com.ibm.iotf.client.device.DeviceClient;

public class RegisteredDeviceEventPublishPropertiesFile {

    public static void main(String[] args) {
        //Proporcionar los datos específicos del dispositivo, así como Auth-key y token utilizando la clase Properties
        Properties options = DeviceClient.parsePropertiesFile(new File("C:\\temp\\device.prop"));

        DeviceClient myClient = null;
        try {
            //Instanciar la clase pasando el archivo de propiedades
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Conectar al {{site.data.keyword.iot_short_notm}}
        myClient.connect();

        //Generar un objeto JSON del suceso que se va a publicar
        JsonObject event = new JsonObject();
        event.addProperty("name", "foo");
        event.addProperty("cpu",  90);
        event.addProperty("mem",  70);

        //El flujo registrado permite 0, 1 y 2 QoS
        myClient.publishEvent("status", event, 1);
        System.out.println("SUCCESSFULLY POSTED......");

  ...
```

El contenido del archivo de configuración debe estar en el formato siguiente:

```
    [device]
    org=$orgId
    typ=$myDeviceType
    id=$myDeviceId
    auth-method=token
    auth-token=$token
```

## Conexión con {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}


Para conectarse a {{site.data.keyword.iot_short_notm}}, utilice la función `connect()`. La función `connect()` incluye un parámetro booleano opcional que se llama `autoRetry`, que determina si la biblioteca intenta volver a conectarse cuando haya un fallo de conexión a MqttException. De forma predeterminada, `autoRetry` se establece en true. Si falla una conexión MqttSecurityException porque se pasan detalles de registro de dispositivos incorrectos, la biblioteca no intentará volver a conectarse, incluso aunque `autoRetry` esté establecido en true.

Para establecer el intervalo 'keep alive' para MQTT, puede utilizar opcionalmente el método `setKeepAliveInterval(int)` antes de llamar a la función `connect()`. El valor `setKeepAliveInterval(int)` se mide en segundos, y define el intervalo de tiempo máximo entre mensajes que se han enviado o recibido. Cuando se utiliza, el cliente puede detectar cuándo ya no está disponible el servidor sin esperar a que finalice el periodo de tiempo de espera de TCP/IP. El cliente garantiza que al menos un mensaje viaja por la red dentro de cada periodo de intervalo de 'keep alive'. Si se reciben mensajes relacionados con datos cero durante el periodo de tiempo de espera, el cliente envía un mensaje `ping` pequeño, el cual reconoce el servidor. El `setKeepAliveInterval(int)` se establece en 60 segundos de forma predeterminada. Para inhabilitar la característica de proceso 'keep alive' en el cliente, establezca el valor `setKeepAliveInterval(int)` en 0.


```
DeviceClient myClient = new DeviceClient(options);
myClient.setKeepAliveInterval(120);
myClient.connect(true);
```

Para controlar el número de reintentos que se producen cuando hay una anomalía de conexión, utilice la función overloaded connect(int numberOfTimesToRetry).


```
DeviceClient myClient = new DeviceClient(options);
myClient.setKeepAliveInterval(120);
myClient.connect(10);
```

Una vez que los dispositivos se hayan conectado correctamente a {{site.data.keyword.iot_short_notm}}, pueden publicar sucesos y suscribirse a mandatos de dispositivos desde una aplicación.


## Publicación de sucesos
{: #publishing_events}

Los sucesos son el mecanismo por el que los dispositivos publican datos en el {{site.data.keyword.iot_short_notm}}. El dispositivo controla el contenido del suceso y asigna un nombre a cada suceso que envía.

Cuando una instancia de {{site.data.keyword.iot_short_notm}} recibe un suceso, las credenciales del suceso recibido identifican el dispositivo de envío, lo que significa que un dispositivo no puede suplantar a otro dispositivo.

Los sucesos se pueden publicar en cualquiera de los tres [niveles de calidad de servicio (QoS)](../../reference/mqtt/index.html#qos-levels) definidos por el protocolo MQTT.  De forma predeterminada, los sucesos se publican en QoS=0.

### Sucesos de publicación en el nivel QoS predeterminado

```
myClient.connect();

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

myClient.publishEvent("status", event);
```


### Aumentar el nivel de QoS para un suceso

Puede aumentar los [niveles de QoS](../../reference/mqtt/index.html#qos-levels) para los sucesos que se publican. Los sucesos con un nivel de QoS mayor que cero pueden tardar un poco más en publicarse, debido a la información de recepción de confirmación adicional que se incluye.

```
myClient.connect();

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

//El flujo registrado permite 0, 1 y 2 QoS
myClient.publishEvent("status", event, 2);
```

### Publicación de sucesos en formatos personalizados

Los sucesos se pueden publicar en distintos formatos, por ejemplo, JSON, serie, binario, etc. De forma predeterminada, la biblioteca publica sucesos en formato JSON, pero puede especificar los datos en distintos formatos si lo prefiere. Por ejemplo, para publicar datos en el formato de serie, utilice el siguiente fragmento de código.

```
myClient.connect();

String data = "cpu:"+getProcessCpuLoad();
status = myClient.publishEvent("load", data, "text", 2);
```

**Nota:** En el ejemplo de código anterior, la carga útil del suceso debe estar en formato de serie.

Cualquier dato XML se puede convertir a formato serie y publicarse como se indica a continuación:

```
status = myClient.publishEvent("load", xmlConvertedString, "xml", 2);
```

De forma similar, para publicar sucesos en formato binario, utilice la matriz de bytes que se describe en el ejemplo siguiente:

```
myClient.connect();

byte[] cpuLoad = new byte[] {30, 35, 30, 25};
status = myClient.publishEvent("blink", cpuLoad , "binary", 1);
```

### Publicar sucesos utilizando HTTP
{: #publishing_events_http}


Además de utilizar MQTT, también puede configurar los dispositivos para publicar sucesos en {{site.data.keyword.iot_short_notm}} mediante HTTP. En los pasos siguientes se describe la secuencia para publicar sucesos a través de HTTP:

1. Construir una instancia de `DeviceClient` utilizando el archivo de propiedades.
2. Construir un suceso que debe publicarse.
3. Especificar el nombre de archivo y, a continuación, publicar el suceso utilizando el método `publishEventOverHTTP()`, como se muestra en el ejemplo de código siguiente:

``` sourceCode
DeviceClient myClient = new DeviceClient(deviceProps);

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

boolean response  = myClient.api().publishDeviceEventOverHTTP("blink", event, ContentType.json);
```

Para ver todo el código, consulte el ejemplo de dispositivo [HttpDeviceEventPublish].

En función de los valores del archivo de propiedades, el método `publishEventOverHTTP()` publica el suceso en modalidad de Inicio rápido o en modalidad de flujo registrado. Cuando el ID de organización en el archivo de propiedades se establece en `quickstart`, el método `publishEventOverHTTP()` publica el suceso en el servicio de inicio rápido de ejemplo del dispositivo y publica el suceso en formato HTTP sin formato. Cuando se especifica una organización registrada válida en el archivo de propiedades, los sucesos se publicarán de forma segura mediante HTTPS.

El protocolo HTTP proporciona una entrega 'at most once', que es similar al nivel de calidad de servicio 'at most once' (QoS 0) del protocolo MQTT. Al utilizar la entrega 'at most once' para publicar sucesos, la aplicación debe implementar la lógica de reintento siempre que haya un error.

[HttpDeviceEventPublish]: https://github.com/ibm-messaging/iot-device-samples/blob/master/java/device-samples/src/main/java/com/ibm/iotf/sample/client/device/HttpDeviceEventPublish.java

## Manejo de mandatos
{: #handling_commands}

Cuando el cliente de dispositivo se conecta, se suscribe automáticamente a todos los mandatos para este dispositivo. Para procesar mandatos específicos, necesita registrar un método callback de mandatos.
Los mensajes se devuelven como una instancia de la clase `Command`, que contiene las siguientes propiedades:

| Propiedad     |Tipos de datos     | Descripción|
|----------------|----------------|
|`payload` |java.lang.String| Los datos para la carga útil de mensaje.|
|`format`  |java.lang.String| El formato puede ser una serie, como por ejemplo JSON.|
|`command`   |java.lang.String|Identifica el mandato.|
|`timestamp`   |org.joda.time.DateTime|La fecha y hora del suceso.|


``` sourceCode
package com.ibm.iotf.sample.client.device;

import java.util.Properties;
import java.util.concurrent.BlockingQueue;
import java.util.concurrent.LinkedBlockingQueue;


import com.ibm.iotf.client.device.Command;
import com.ibm.iotf.client.device.CommandCallback;
import com.ibm.iotf.client.device.DeviceClient;


//Implemente la clase CommandCallback para proporcionar la forma en que desea que se maneje el mandato
class MyNewCommandCallback implements CommandCallback, Runnable {

    // Una cola para retener & procesar los mandatos para el manejo sencillo de mensajes MQTT
    private BlockingQueue<Command> queue = new LinkedBlockingQueue<Command>();

    /**
    * Este método lo invoca la biblioteca siempre que haya un mandato que coincida con los criterios de suscripción
    */
    @Override
    public void processCommand(Command cmd) {
        try {
            queue.put(cmd);
            } catch (InterruptedException e) {
        }
    }

    @Override
    public void run() {
        while(true) {
            Command cmd = null;
            try {
                //En este ejemplo, se muestra el mandato
                cmd = queue.take();
                System.out.println("COMMAND RECEIVED = '" + cmd.getCommand() + "'\twith Payload = '" + cmd.getPayload() + "'");
            } catch (InterruptedException e) {}
        }
    }
}

public class RegisteredDeviceCommandSubscribe {


    public static void main(String[] args) {

        //Proporcionar los datos específicos del dispositivo, así como Auth-key y token utilizando la clase Properties
        Properties options = new Properties();

        options.setProperty("org", "uguhsp");
        options.setProperty("type", "iotsample-arduino");
        options.setProperty("id", "00aabbccde03");
        options.setProperty("auth-method", "token");
        options.setProperty("auth-token", "AUTH TOKEN FOR DEVICE");

        DeviceClient myClient = null;
        try {
            //Instanciar la clase pasando el archivo de propiedades
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Pase el CommandCallback implementado anteriormente como un argumento a este cliente de dispositivo
        myClient.setCommandCallback(new MyNewCommandCallback());

        //Conéctese al {{site.data.keyword.iot_short_notm}}
        myClient.connect();
    }
}
```

## Ejemplos
{: #samples}

Para obtener una lista de dispositivos y de ejemplos de gestión de dispositivos desarrollados utilizando la biblioteca de clientes Java de {{site.data.keyword.iot_short_notm}}, consulte el [repositorio de GitHub iot-device-samples](https://github.com/ibm-messaging/iot-device-samples/tree/master/java).
