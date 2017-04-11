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


# mBed C++ para desarrolladores de dispositivos
{: #mbedcpp}

Utilice la [biblioteca de cliente mBed C++ ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/){: new_window} para conectar fácilmente [dispositivos mBed ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.mbed.com/en/){: new_window}, como [LPC1768](https://developer.mbed.org/platforms/mbed-LPC1768/) o [FRDM-K64F ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.mbed.org/platforms/FRDM-K64F/){: new_window}, al servicio {{site.data.keyword.iot_full}}.
{:shortdesc}

Para obtener más información, consulte [ibmiotf ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/){: new_window} en [developer.mbed.org ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.mbed.org/){: new_window}.

Aunque la biblioteca utiliza C++, evita las ubicaciones de memoria dinámicas y el uso de funciones STL, porque los dispositivos mBed a veces cuentan con modelos de memoria idiosincráticos que hacen que la importación sea difícil. En cualquier caso, la biblioteca le permite realizar el uso de memoria de forma tan predecible como sea posible.

## Dependencias
{: #dependencies}

|Dependencia |Descripción|
|:---|:---|
|[Biblioteca de Eclipse Paho MQTT ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.mbed.org/teams/mqtt/code/MQTT/){: new_window}|Proporciona una biblioteca de cliente MQTT para dispositivos mBed. Para obtener más información, consulte [Bibliotecas de cliente Embedded MQTT C/C++ ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.eclipse.org/paho/clients/c/embedded/){: new_window}|
|[Biblioteca EthernetInterface ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.mbed.org/users/mbed_official/code/EthernetInterface/){: new_window}|Una biblioteca mBed IP en Ethernet.|

## Cómo utilizar la biblioteca
{: #library_use}

Utilice el [compilador mBed ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.mbed.org/compiler/){: new_window} para crear las aplicaciones cuando se utiliza la biblioteca de cliente mBed C++ IBMIoTF. El compilador mBed proporciona un C/C++ IDE en línea ligero configurado para grabar, compilar y descargar programas que se ejecuten en el microcontrolador mBed.

**Nota:** No tiene que instalar o configurar nada para utilizar mBed.

Para obtener información sobre cómo conectar un microcontrolador ARM mBed NXP LPC 1768 a {{site.data.keyword.iot_short_notm}}, consulte la receta [Biblioteca de cliente mBed C++ para IBM Watson IoT Platform ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/recipes/tutorials/mbed-c-client-library-for-ibm-iot-foundation/){: new_window}.

## Constructor
{: #constructor}

El constructor crea la instancia de cliente y acepta los siguientes parámetros:

|Parámetro |Descripción |
|:---|:---|
|`org` |El ID de la organización. Este valor es obligatorio. Si está utilizando un flujo de Quickstart, especifique `quickstart`.|
|`type`   |El tipo del dispositivo. Este campo es obligatorio.|
|`id`   |El ID del dispositivo. Este campo es obligatorio.|
|`auth-method`   |El método de autenticación, que es un campo opcional que sólo es necesario para un flujo registrado. El único valor al que se da soporte actualmente es `token`.|
|`auth-token`   |Una señal de autenticación para conectar de forma segura el dispositivo a Watson IoT Platform. Este es un campo opcional que sólo es necesario para un flujo registrado.|

Estos parámetros crean definiciones que se utilizan para interactuar con el servicio de {{site.data.keyword.iot_short_notm}}.

El ejemplo de código siguiente describe cómo puede interactuar una instancia de DeviceClient con el servicio de Inicio rápido de {{site.data.keyword.iot_short_notm}}:

```
  #include "DeviceClient.h"
  ....
  ....

  // Establezca los parámetros de conexión {{site.data.keyword.iot_short_notm}}
  char organization[11] = "quickstart";     // Para una conexión registrada, sustituya por su org
  char deviceType[8] = "LPC1768";           // Para una conexión registrada, sustituya por su device type
  char deviceId[3] = "01";                  // Para una conexión registrada, sustituya por su device id

  // Crear DeviceClient
  IoTF::DeviceClient client(organization, deviceType, deviceId);

  // Obtener el DeviceID(MAC Address) si se está en una modalidad de inicio rápido y el ID de dispositivo no se ha especificado
  if((strcmp(organization, QUICKSTART) == 0) && (strcmp("", deviceId) == 0))
  {
  	char tmpBuf[50];
  	client.getDeviceId(tmpBuf, sizeof(tmpBuf));
  }
  ....
```

Como se muestra en el ejemplo de código anterior, si no se especifica el ID de dispositivo, el DeviceClient utiliza la dirección MAC del dispositivo como ID de dispositivo para conectarse con la {{site.data.keyword.iot_short_notm}}. El código de dispositivo puede utilizar el método `getDeviceId()` para recuperar el ID de dispositivo de la instancia de DeviceClient.

El siguiente bloque de código muestra cómo crear una instancia de DeviceClient para interactuar con la organización Registrada de {{site.data.keyword.iot_short_notm}}.

```
  #include "DeviceClient.h"
  ....
  ....

  // Establecer los parámetros de conexión {{site.data.keyword.iot_short_notm}}
  char organization[11] = "hrcl78";
  char deviceType[8] = "LPC1768";
  char deviceId[3] = "LPC176801";
  char method[6] = "token";
  char token[9] = "password";

  // Crear DeviceClient
  IoTF::DeviceClient client(organization, deviceType, deviceId, method, token);
  ....
```

## Conexión con {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

El dispositivo puede conectarse a la {{site.data.keyword.iot_short_notm}} invocando la función connect en la instancia de DeviceClient.

```
  #include "DeviceClient.h"
  ....
  ....

  // Crear DeviceClient
  IoTF::DeviceClient client(organization, deviceType, deviceId, method, token);

  bool status = client.connect();

```
Tras la correcta conexión, el dispositivo puede publicar sucesos en la {{site.data.keyword.iot_short_notm}} y puede escuchar mandatos.

Además, el dispositivo puede consultar el estado de la conexión utilizando el método `isConnected()`, que se muestra en el ejemplo siguiente:

```
  #include "DeviceClient.h"
  ....
  ....

  client.isConnected();

```


## Publicación de sucesos
{: #publishing_events}

Los sucesos son el mecanismo por el que los dispositivos publican datos en el {{site.data.keyword.iot_short_notm}}. El dispositivo controla el contenido del suceso y asigna un nombre a cada suceso que envía.

Cuando una instancia de {{site.data.keyword.iot_short_notm}} recibe un suceso, las credenciales del suceso recibido identifican el dispositivo de envío, lo que significa que un dispositivo no puede suplantar a otro dispositivo.

Los sucesos se pueden publicar en cualquiera de los tres [niveles de calidad de servicio (QoS)](../../reference/mqtt/index.html#qos-levels) definidos por el protocolo MQTT. De forma predeterminada, los sucesos se publican en QoS 0.

### Publicación de sucesos utilizando la calidad de servicio predeterminada

En el ejemplo siguiente se muestra cómo publicar los siguientes puntos de datos en {{site.data.keyword.iot_short_notm}} en formato JSON:

- LPC1768, como por ejemplo los ejes x, y y z
- Posición del joystick
- Lectura de temperatura actual

```
	boolean status = client.connect();

	// Crear almacenamiento intermedio para albergar el suceso
	char buf[250];

	// Construir un mensaje de sucesos con los puntos de datos deseados en formato JSON
	sprintf(buf,
            "{\"d\":{\"myName\":\"IoT mbed\",\"accelX\":%0.4f,\"accelY\":%0.4f,\"accelZ\":%0.4f,
            \"temp\":%0.4f,\"joystick\":\"%s\",\"potentiometer1\":%0.4f,\"potentiometer2\":%0.4f}}",
            MMA.x(), MMA.y(), MMA.z(), sensor.temp(), joystickPos, ain1.read(), ain2.read());

        status = client.publishEvent("blink", buf);
	....
```
Para obtener el ejemplo completo, consulte [ IBMIoTClientLibrarySample ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTClientLibrarySample/file/e58533b6bc6b/src/Main.cpp){: new_window}.

### Aumentar el nivel de QoS para un suceso

Puede aumentar los [niveles de QoS](../../reference/mqtt/index.html#qos-levels) para los sucesos que se publican. Los sucesos que tienen un nivel de QoS mayor que `0` pueden tardar más tiempo en publicarse debido a la información de recepción de confirmación adicional que se incluye.

**Nota:** La modalidad de flujo de Inicio rápido sólo da soporte a QoS 0.

```
	#include "MQTTClient.h"

	boolean status = client.connect();

	// Crear almacenamiento intermedio para albergar el suceso
	char buf[250];

	// Construir un mensaje de sucesos con los puntos de datos deseados en formato JSON
	sprintf(buf,
            "{\"d\":{\"myName\":\"IoT mbed\",\"accelX\":%0.4f,\"accelY\":%0.4f,\"accelZ\":%0.4f,
            \"temp\":%0.4f,\"joystick\":\"%s\",\"potentiometer1\":%0.4f,\"potentiometer2\":%0.4f}}",
            MMA.x(), MMA.y(), MMA.z(), sensor.temp(), joystickPos, ain1.read(), ain2.read());

        status = client.publishEvent("blink", buf, MQTT::QOS2);
	....
```

### Gestión del error de pérdida de la conexión durante la publicación de un suceso


Cuando el método `publishEvent()` devuelve el valor false, puede comprobar el estado de la conexión e invocar `reConnect()` si se pierde la conexión.

```
	#include "MQTTClient.h"

	status = client.publishEvent("blink", buf, MQTT::QOS2);

	if(status == false) {
	    // Comprobar si la conexión se ha perdido y volver a intentar
	    while(!client.isConnected())
	    {
	        client.reConnect();
	        wait(5.0);
	    }
	}
	....
```
La biblioteca no almacena los sucesos que se publican durante el estado desconectado, por lo que el dispositivo necesita invocar el método `publishEvent()` de nuevo para poder enviar dichos sucesos cuando se restablezca la conexión.


## Manejo de mandatos
{: #handling_commands}

Cuando el cliente de dispositivo se conecta, se suscribe automáticamente a todos los mandatos para este dispositivo. Para procesar mandatos específicos, necesita registrar un método de devolución de llamada de mandato.
Los mensajes se devuelven como una instancia de la clase Command, que tiene las siguientes propiedades:

|Propiedad |Descripción|
|:---|:---|
|`command` | El nombre del mandato que se ha invocado.|  
|`format`  |El formato del suceso. El formato puede ser una serie, como por ejemplo JSON. |
|`payload`  |Los datos para la carga útil de mandatos. La longitud máxima es 131072 bytes. |


El código siguiente define una función de devolución de llamada de mandatos de ejemplo que procesa el mandato de intervalo de parpadeo LED desde la aplicación y establece el manejador de funciones en la instancia de DeviceClient para que el método callback se ejecute siempre que el dispositivo reciba el mandato de parpadeo.

```
    #include "DeviceClient.h"
    #include "Command.h"

    // Procesar el mandato y establecer el intervalo de parpadeo LED
    void processCommand(IoTF::Command &cmd)
    {
        if (strcmp(cmd.getCommand(), "blink") == 0)
    	{
    	    char *payload = cmd.getPayload();
    	    char* pos = strchr(payload, '}');
    	    if (pos != NULL) {
    	        *pos = '\0';
    	        char* ratepos = strstr(payload, "rate");
    	        if(ratepos == NULL)
    	            return;
    	        if ((pos = strchr(ratepos, ':')) != NULL)
    	        {
    	            int blink_rate = atoi(pos + 1);
    	            blink_interval = (blink_rate <= 0) ? 0 : (blink_rate > 50 ? 1 : 50/blink_rate);
    	        }
    	    }
    	} else {
            WARN("Unsupported command: %s\n", cmd.getCommand());
        }
    }

    client.setCommandCallback(processCommand);

    client.yield(1000);  // permitir al cliente MQTT recibir mensajes
    ....
```
Para obtener el ejemplo completo, consulte [ IBMIoTClientLibrarySample ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTClientLibrarySample/file/e58533b6bc6b/src/Main.cpp){: new_window}.

**Nota:** La función `client.yield()` debe invocarse periódicamente para que reciba mandatos.
La función `client.yield()` permite al dispositivo recibir mandatos desde Watson IoT Platform y mantiene la conexión activa. Si la función `client.yield()` no se invoca dentro del intervalo de tiempo especificado por el intervalo de keepAlive, el dispositivo no recibirá los mandatos que se envíen desde la plataforma. El valor que se asigna a la función `client.yield()` especifica la longitud de tiempo (en milisegundos) que se pueden leer los datos desde el socket antes de que se devuelva el control a la aplicación.

## Desconexión del cliente
{: #disconnect_client}

Para desconectar el cliente y lanzar las conexiones, ejecute el siguiente fragmento de código:

```
	...
	client.disconnect();
	....
```
## Ejemplos
{: #samples}

[IBMIoTClientLibrarySample ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTClientLibrarySample/){: new_window} es un ejemplo de código que muestra cómo utilizar la biblioteca de cliente de {{site.data.keyword.iot_short_notm}} para conectar los dispositivos mbed LPC1768 o FRDM-K64F a la instancia de servicio.
