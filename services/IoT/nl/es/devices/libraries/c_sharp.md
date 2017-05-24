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


# ﻿C# for device developers
{: #c_sharp}

Puede utilizar C# para crear y personalizar dispositivos que interactúan con su organización en {{site.data.keyword.iot_full}}. Utilice la información y los ejemplos que se proporcionan para empezar a desarrollar los dispositivos mediante C#.
{:shortdesc}

## Descarga del cliente y los recursos de C#
{: #csharp_client_download}

Para acceder al cliente y a los recursos de C# para {{site.data.keyword.iot_short_notm}}, vaya al repositorio [iot-csharp ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ibm-watson-iot/iot-csharp){: new_window} en GitHub y complete las instrucciones de instalación.


## Constructor
{: #constructor}

El constructor compila la instancia del cliente y acepta los argumentos que contienen las siguientes definiciones:

|Definición |Descripción |
|:---|:---|
|`orgId`|El ID de la organización.|
|`deviceType`|El tipo del dispositivo.|
|`deviceId` |El ID del dispositivo.|
|`auth-method`   |El método de autenticación que debe utilizarse. El único valor al que se da soporte actualmente es `token`.|
|`auth-token`   |Una señal de autenticación para conectar de forma segura el dispositivo a Watson IoT Platform.|


Si `deviceId` y `deviceType` son los únicos argumentos proporcionados, el cliente se conecta al servicio Inicio rápido de {{site.data.keyword.iot_short_notm}} como un dispositivo no registrado. La lista de argumentos define cómo se conecta el cliente al módulo de {{site.data.keyword.iot_short_notm}}.


```
namespace com.ibm.iotf.client

public DeviceClient(string orgId, string deviceType, string deviceID, string auth-method, string auth-token)
        : base(orgId, "d" + CLIENT_ID_DELIMITER + orgId + CLIENT_ID_DELIMITER + deviceType + CLIENT_ID_DELIMITER + deviceID, "use-token-auth", auth-token)
    {

    }
```

## Publicación de sucesos
{: #publishing-events}

Los sucesos de uso de dispositivos para publicar datos en la instancia de {{site.data.keyword.iot_short_notm}}. El dispositivo controla el contenido del suceso y asigna un nombre a cada suceso que envía.

Cuando una instancia de {{site.data.keyword.iot_short_notm}} recibe un suceso, las credenciales del suceso entrante identifican el dispositivo de envío, lo que significa que un dispositivo no puede suplantar a otro dispositivo.

Los sucesos se pueden publicar en cualquiera de los tres [niveles de calidad de servicio (QoS)](../mqtt.html#managed-devices), definidos por el protocolo MQTT. De forma predeterminada, los sucesos se publican en QoS 0.


## Publicación de un suceso utilizando la calidad predeterminada del nivel de servicio
{: #publish_event_default_qos}

```
deviceClient.connect();
deviceClient.publishEvent("event", "json", "{temp:23}");
```


## Publicación de un suceso utilizando una calidad definida por el usuario del nivel de servicio
{: #publish_event_user_qos}

Los sucesos que se publican en un nivel MQTT QoS que sean mayores que `0` incluyen información de confirmación de recepción adicional y puede que tarden un poco más en publicarse que los sucesos que tengan un nivel de QoS de `0`.


```
deviceClient.connect();
deviceClient.publishEvent("event", "json", "{temp:23}", 2);
```

## Manejo de mandatos
{: #handling_commands}

Cuando se conecta un cliente de dispositivo, se suscribe automáticamente a todos los mandatos para este dispositivo. Para procesar mandatos específicos, debe registrar un método callback de mandatos tal como se muestra en el ejemplo siguiente:

```
public static void processCommand(string cmdName, string cmdFormat, string cmdData) {
...
 }
```

```
deviceClient.connect();
deviceClient.commandCallback += processCommand;
```
La tabla siguiente describe los parámetros del método commandCallback:

|Parámetro|Tipos de datos|Descripción|
|:---|:---|
|`cmdName`|Serie|Identifica el mandato. |
|`cmdFormat`|Serie|El formato puede ser una serie, como por ejemplo JSON.|
|`cmdData`|Diccionario|Los datos para la carga útil. La longitud máxima es 131072 bytes.|
