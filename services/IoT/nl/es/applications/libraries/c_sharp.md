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


# ﻿C# for application developers
{: #c_sharp}


Puede utilizar C# para crear y personalizar aplicaciones que interactúan con su organización en {{site.data.keyword.iot_full}}. Utilice la información y los ejemplos que se proporcionan para empezar a desarrollar las aplicaciones mediante C#.
{:shortdesc}

## Descarga del cliente y los recursos de C#
{: #csharp_client_download}

Para acceder a las bibliotecas y ejemplos de cliente C# para {{site.data.keyword.iot_short_notm}}, vaya al repositorio [iot-csharp ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ibm-watson-iot/iot-csharp){: new_window} en GitHub y complete las instrucciones de instalación.


## Constructor
{: #constructor}

El constructor compila la instancia del cliente y acepta los argumentos que contienen las siguientes definiciones:

|Definición |Descripción |
|:---|:---|
|`orgId`   |El ID de la organización.|
|`appId`   |El ID exclusivo de una aplicación en su organización.|
|`auth-key`   |Una clave API para conectar de forma segura la aplicación a Watson IoT Platform|
|`auth-token`   |Una señal de clave API para conectar de forma segura la aplicación a Watson IoT Platform.|

Si `appId` es el único argumento que se proporciona, el cliente se conecta al servicio de Inicio rápido de {{site.data.keyword.iot_short_notm}} como un dispositivo no registrado. La lista de argumentos define cómo se conecta el cliente al módulo de {{site.data.keyword.iot_short_notm}}.

```
ApplicationClient applicationClient = new ApplicationClient(orgId, appId, apiKey, authToken);  
applicationClient.connect();
```


## Suscripción a sucesos de dispositivos
{: #subscribe_device_events}

Los sucesos de uso de dispositivos para publicar datos en la instancia de {{site.data.keyword.iot_short_notm}}. El dispositivo controla el contenido del suceso y asigna un nombre a cada suceso que envía.

Cuando una instancia de {{site.data.keyword.iot_short_notm}} recibe un suceso, las credenciales del suceso recibido identifican el dispositivo de envío, lo que significa que un dispositivo no puede suplantar a otro dispositivo.

De forma predeterminada, las aplicaciones se suscriben a todos los sucesos desde todos los dispositivos conectados. Utilice los parámetros device type, device ID, event y message format para controlar el ámbito de la suscripción. En los siguientes ejemplos de código se muestra cómo se puede definir el ámbito de una suscripción utilizando estos parámetros:

### Suscripción a todos los sucesos de todos los dispositivos

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents();
```

### Suscripción a todos los sucesos de todos los dispositivos de un tipo específico

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(deviceType);
```

### Suscripción a un suceso específico de todos los dispositivos

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(evt);
```

###  Suscripción a un suceso específico de dos o más dispositivos distintos:

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(deviceType, deviceId, evt);
```

### Suscripción a todos los sucesos que se publican en formato JSON

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(deviceType, deviceId, evt, "json", 0);
```

**Nota**: Una instancia de cliente individual puede admitir varias suscripciones.

### Manejo de sucesos desde dispositivos

Para procesar sucesos que se han recibido por las suscripciones, registre un método callback de sucesos como se muestra en el ejemplo siguiente:

```
public static void processEvent(String eventName, string eventFormat, string eventData) {
// Do something
}
applicationClient.connect();
applicationClient.eventCallback += processEvent;
applicationClient.subscribeToDeviceEvents();
```
La tabla siguiente describe los parámetros del método callback de sucesos:

|Parámetro|Tipos de datos|Descripción|
|:---|:---|
|`eventName`|Serie|Identifica el suceso. |
|`eventFormat`|Serie| El formato puede ser una serie, como por ejemplo JSON.|
|`eventData`|Diccionario| Los datos para la carga útil de mensaje. La longitud máxima es 131072 bytes.|


## Suscripción a estado de dispositivos
{: #subscribe_device_status}

De forma predeterminada, la suscripción se establece en recibir actualizaciones de estado para todos los dispositivos conectados. Utilice los parámetros device type y device ID para controlar el ámbito de la suscripción. En los siguientes ejemplos de código se muestra cómo se puede definir el ámbito de una suscripción utilizando estos parámetros:

### Suscripción a actualizaciones de estado para todos los dispositivos

```
applicationClient.connect();
applicationClient.subscribeToDeviceStatus += processDeviceStatus;
applicationClient.subscribeToDeviceStatus();
```

### Suscripción a actualizaciones de estado para dos dispositivos distintos

```
applicationClient.connect();
applicationClient.subscribeToDeviceStatus += processDeviceStatus;
applicationClient.subscribeToDeviceStatus(deviceType, deviceId);
```

**Nota**: Una instancia de cliente individual puede admitir varias suscripciones.

### Manejo de actualizaciones de estado desde dispositivos

Para procesar las actualizaciones de estado recibidas por las suscripciones, registre un método callback de sucesos tal como se muestra en el ejemplo siguiente:

```
public static void processDeviceStatus(String deviceType, string deviceId, string data)
        {
           //
        }
applicationClient.connect();
applicationClient.appStatusCallback += processAppStatus;
applicationClient.subscribeToApplicationStatus();
```

## Publicación de sucesos desde dispositivos
{: #publish_events_devices}

Las aplicaciones pueden publicar sucesos como si se originaran a partir de un dispositivo.

```
applicationClient.connect();
applicationClient.publishEvent(deviceType, deviceId, evt, data, 0);

```

La tabla siguiente describe los parámetros que se especifican en el método `publishEvent()`:

|Parámetro|Tipos de datos|Descripción|
|:---|:---|
|`deviceType`|Serie| El tipo de dispositivo. Normalmente, el deviceType es una agrupación para los dispositivos que realizan una tarea específica, como por ejemplo "weatherballoon".|
|`deviceId`|Serie| El ID del dispositivo. Normalmente, para un determinado tipo de dispositivo, el deviceId es un identificador exclusivo de dicho dispositivo, por ejemplo un número de serie o una dirección MAC.|
|`evt`|Serie| El nombre del suceso.|
|`format`|Serie| El formato puede ser una serie, como por ejemplo JSON.|
|`data`|Diccionario| Los datos para la carga útil de mensaje. La longitud máxima es 131072 bytes.|
|`QoS`|Entero| La Calidad de servicio. Los valores válidos son `0`, `1`, `2`. |


## Publicación de mandatos en dispositivos
{: #publish_commands_devices}

Las aplicaciones pueden publicar mandatos en dispositivos conectados.

```
applicationClient.connect();
applicationClient.publishCommand(deviceType, deviceId, "testcmd", "json", data, 0);
```
La tabla siguiente describe los parámetros que se especifican en el método `publishCommand()`:

|Parámetro|Tipos de datos|Descripción|
|:---|:---|
|`deviceType`|Serie| El tipo de dispositivo. Normalmente, el deviceType es una agrupación para los dispositivos que realizan una tarea específica, como por ejemplo "weatherballoon".|
|`deviceId`|Serie| El ID del dispositivo. Normalmente, para un determinado tipo de dispositivo, el deviceId es un identificador exclusivo de dicho dispositivo, por ejemplo un número de serie o una dirección MAC.|
|`command`|Serie| El nombre del mandato.|
|`format`|Serie| El formato puede ser una serie, como por ejemplo JSON.|
|`data`|Diccionario| Los datos para la carga útil de mensaje. La longitud máxima es 131072 bytes.|
|`QoS`|Entero| La Calidad de servicio. Los valores válidos son `0`, `1`, `2`. |
