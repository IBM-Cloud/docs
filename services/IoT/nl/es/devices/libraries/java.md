---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Java para desarrolladores de dispositivos
{: #java}

Última actualización: 02 de agosto de 2016
{: .last-updated}


Puede utilizar Java para crear y personalizar dispositivos que interactúan con su organización en {{site.data.keyword.iot_full}}. Utilice la información y los ejemplos que se proporcionan para empezar a desarrollar los dispositivos mediante Java.
{:shortdesc}

## Descarga del cliente y los recursos de Java
{: #java_client_download}

Para acceder a las bibliotecas y a los ejemplos de cliente Java para {{site.data.keyword.iot_short_notm}}, vaya al repositorio [iot-java](https://github.com/ibm-watson-iot/iot-java) en GitHub y complete las instrucciones de instalación.


## Constructor
{: #constructor}

El constructor compila la instancia del cliente y acepta un objeto de propiedades que contiene las siguientes definiciones:

|Definición |Descripción |
|:---|:---|
|`org` |El ID de la organización. Este campo es obligatorio. Si está utilizando un flujo de Quickstart, especifique `quickstart`.|
|`type`  |El tipo del dispositivo. Este campo es obligatorio.|
|`id`  |El ID del dispositivo. Este campo es obligatorio.|
|`auth-method`   |El método de autenticación que debe utilizarse. El único valor al que se da soporte actualmente es `token`.|
|`auth-token`   |Una señal de autenticación para conectar de forma segura el dispositivo a Watson IoT Platform.|
|`clean-session`|Un valor true o false que sólo es necesario si desea conectar la aplicación en modalidad de suscripción duradera. De forma predeterminada, `clean-session` se establece en `true`.|

**Nota:** Para conectar el dispositivo en modalidad de suscripción duradera, establezca `clean-session` en `false`. Para obtener más información sobre la sesión limpia, consulte la sección 'Almacenamientos intermedios de suscripción y sesión limpia' de la [documentación de MQTT](../../reference/mqtt/index.html#subscription-buffers-and-clean-session).

El objeto de propiedades crea definiciones utilizadas para interactuar con el módulo de {{site.data.keyword.iot_short_notm}}.

El código siguiente muestra sucesos de publicación de dispositivos en modalidad de Inicio rápido.

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

En lugar de utilizar un objeto de propiedades directamente, puede utilizar un archivo de configuración que contenga los pares name-value para las propiedades. Si está utilizando un archivo de configuración que contiene un objeto de propiedades, utilice el siguiente formato de código:

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

Conéctese a la {{site.data.keyword.iot_short_notm}} invocando la función de conexión. La función de conexión toma un parámetro booleano opcional `autoRetry`, que es `true` de forma predeterminada. El parámetro `autoRetry` permite que la biblioteca vuelva a conectarse cuando se produzca un error MqttException. Tenga en cuenta que la biblioteca no intenta volver a conectarse cuando se produce un error de MqttSecurityException porque se han utilizado detalles de registro de dispositivos incorrectos, incluso si el parámetro `autoRetry` se establece en `true`.

```
DeviceClient myClient = new DeviceClient(options);

myClient.connect(true);
```

Tras la correcta conexión con el servicio de {{site.data.keyword.iot_short_notm}}, el cliente del dispositivo puede realizar operaciones como, por ejemplo, publicar sucesos y suscribirse a los mandatos de dispositivos desde una aplicación.


## Publicación de sucesos
{: #publishing_events}

Los sucesos son el mecanismo por el que los dispositivos publican datos en el {{site.data.keyword.iot_short_notm}}. El dispositivo controla el contenido del suceso y asigna un nombre a cada suceso que envía.

Cuando una instancia de {{site.data.keyword.iot_short_notm}} recibe un suceso, las credenciales del suceso recibido identifican el dispositivo de envío, lo que significa que un dispositivo no puede suplantar a otro dispositivo.

Los sucesos se pueden publicar en cualquiera de los tres [niveles de calidad de servicio (QoS)](../../reference/mqtt/index.html#qos-levels) definidos por el protocolo MQTT. De forma predeterminada, los sucesos se publican en QoS=0.

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

Puede aumentar los [niveles de QoS](../../reference/mqtt/index.html#qos-levels) para los sucesos que se publican. Los sucesos que tienen un nivel de QoS mayor que cero pueden tardar un poco más en publicarse, debido a la información de recepción de confirmación adicional que se incluye.

```
myClient.connect();

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

//El flujo registrado permite 0, 1 y 2 QoS
myClient.publishEvent("status", event, 2);
```

### Publicar sucesos utilizando HTTP

Además de MQTT, los dispositivos pueden publicar sucesos en la {{site.data.keyword.iot_short_notm}} utilizando HTTP y utilizando los pasos siguientes:

* Construir una instancia de DeviceClient utilizando el archivo de propiedades.
* Construir un suceso que debe publicarse.
* Especificar el nombre del suceso y publicarlo mediante el método `publishEventOverHTTP()`, como se muestra en el código siguiente:

``` sourceCode
DeviceClient myClient = new DeviceClient(deviceProps);

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

int httpCode = myClient.publishEventOverHTTP("blink", event);
```

Puede encontrar todo el código en el ejemplo de dispositivo [HttpDeviceEventPublish].

En función de los valores del archivo de propiedades, el método `publishEventOverHTTP()` publica el suceso en modalidad de Inicio rápido o en modalidad de flujo registrado. Cuando el ID de organización en el archivo de propiedades es `quickstart`, el método `publishEventOverHTTP()` publica el suceso en el servicio de inicio rápido de ejemplo del dispositivo y publica el suceso en formato HTTP sin formato. Cuando se utiliza una organización registrada válida en el archivo de propiedades, este método siempre publica el suceso en HTTPS, que es HTTP a través de SSL, de forma que toda la comunicación está protegida.

El protocolo HTTP proporciona una entrega 'at most once', que es similar al nivel de calidad de servicio 'at most once' (QoS 0) del protocolo MQTT. Al utilizar la entrega 'at most once' para publicar sucesos, la aplicación debe implementar la lógica de reintento cuando se produce un error.

[HttpDeviceEventPublish]: https://github.com/ibm-messaging/iot-device-samples/blob/master/java/device-samples/src/main/java/com/ibm/iotf/sample/client/device/HttpDeviceEventPublish.java

## Manejo de mandatos
{: #handling_commands}

Cuando el cliente de dispositivo se conecta, se suscribe automáticamente a todos los mandatos para este dispositivo. Para procesar mandatos específicos, necesita registrar un método callback de mandatos.
Los mensajes se devuelven como una instancia de la clase Command, que tiene las siguientes propiedades:

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

Para obtener una lista de dispositivos y de ejemplos de gestión de dispositivos desarrollados utilizando la biblioteca de clientes Java de {{site.data.keyword.iot_short_notm}}, consulte el [repositorio de GitHub](https://github.com/ibm-messaging/iot-device-samples/tree/master/java).
