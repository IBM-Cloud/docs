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


# Python para desarrolladores de dispositivos
{: #python}

Puede utilizar Python para crear y desarrollar código de dispositivo para interactuar con su organización en {{site.data.keyword.iot_full}}. El cliente Python para {{site.data.keyword.iot_short_notm}} proporciona una API para facilitar la interacción simple con las características de {{site.data.keyword.iot_short_notm}} abstrayendo los protocolos subyacentes como MQTT y HTTP.
{:shortdesc}

Utilice la información y los ejemplos que se proporcionan para empezar a desarrollar los dispositivos utilizando Python.

## Descarga del cliente y los recursos de Python
{: #python_client_download}

Para acceder al cliente Python para {{site.data.keyword.iot_short_notm}} a y otros recursos disponibles, vaya al repositorio [iot-python ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ibm-watson-iot/iot-python){: new_window} en GitHub y complete las instrucciones de instalación.

## Constructor
{: #constructor}

El diccionario de opciones crea definiciones que se utilizan para interactuar con el módulo de {{site.data.keyword.iot_short_notm}}. El constructor compila la instancia de cliente y acepta un diccionario de opciones que contiene las siguientes definiciones:

|Definición|Descripción |
|:---|:---|
|`orgId`|El ID de la organización.|
|`type`|El tipo del dispositivo. El tipo de dispositivo es una agrupación para los dispositivos que realizan una tarea específica, como por ejemplo "weatherballoon".|
|`id`|Identificador exclusivo de un dispositivo. Normalmente, para un determinado tipo de dispositivo, el ID de dispositivo es un identificador exclusivo de dicho dispositivo, por ejemplo un número de serie o una dirección MAC.|
|`auth-method`|El método de autenticación. El único método al que se da soporte es `apikey`.|
|`auth-token`|Una señal de clave API, que también es obligatoria al establecer el valor de auth-method en `apikey`.|
|`clean-session`|Un valor true o false que sólo es necesario si desea conectar la aplicación en modalidad de suscripción duradera. De forma predeterminada, `clean-session` se establece en true.|

Si no se proporciona el diccionario de opciones, el cliente se conecta al servicio Inicio rápido de {{site.data.keyword.iot_short_notm}} como un dispositivo no registrado.

```python

import ibmiotf.device
try:
  options = {
    "org": orgId,
    "type": deviceType,
    "id": deviceId,
    "auth-method": authMethod,
    "auth-token": authToken,
    "clean-session": true
  }
  client = ibmiotf.device.Client(options)
except ibmiotf.ConnectionException  as e:
...
```

### Utilización de un archivo de configuración

En lugar de definir un diccionario de opciones directamente, también puede definir un diccionario de opciones por separado en un archivo de configuración, tal como se describe en el siguiente ejemplo de código:

```python

import ibmiotf.device
try:
  options = ibmiotf.device.ParseConfigFile(configFilePath)
  client = ibmiotf.device.Client(options)
except ibmiotf.ConnectionException  as e:
...
```

El archivo de configuración que contiene el diccionario de opciones debe estar en el formato siguiente:

```python

[device]
org=orgID
type=deviceType
id=deviceId
auth-method=token
auth-token=token
clean-session=true/false
```

## Publicación de sucesos
{: #publishing_events}

Los sucesos son el mecanismo por el que los dispositivos publican datos en el {{site.data.keyword.iot_short_notm}}. El dispositivo controla el contenido del suceso y asigna un nombre a cada suceso que envía.

Cuando una instancia de {{site.data.keyword.iot_short_notm}} recibe un suceso, las credenciales del suceso recibido identifican el dispositivo de envío, lo que significa que un dispositivo no puede suplantar a otro dispositivo.

Los sucesos se pueden publicar con cualquiera de los tres niveles de calidad de servicio (QoS) definidos por el protocolo MQTT.  De forma predeterminada, los sucesos se publican con un nivel de QoS de `0`.

### Publicar un suceso utilizando la calidad de servicio predeterminada

```
client.connect()
myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50}
client.publishEvent("status", "json", myData)
```

### Aumentar el nivel de QoS para un suceso

Puede aumentar el [nivel de calidad de servicio (QoS)](../../reference/mqtt/index.html#qos-levels) para los sucesos que se publican. Los sucesos que tienen un nivel de QoS superior a `0` pueden tardar más tiempo en publicarse debido a la información de recepción de confirmación adicional que se incluye.

**Nota:** La modalidad de flujo de Inicio rápido sólo da soporte a un nivel de QoS de `0`.

```
client.connect()
myQosLevel=2
myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50}
client.publishEvent("status", "json", myData, myQosLevel)
```
## Manejo de mandatos
{: #handling_commands}

Cuando se conecta el cliente del dispositivo, se suscribe automáticamente a cualquier mandato especificado para este dispositivo. Para procesar mandatos específicos, necesita registrar un método callback de mandatos. Los mensajes se devuelven como una instancia de la clase Command, que contiene las siguientes propiedades:

|Propiedad|Tipos de datos|Descripción|
|:---|:---|
|`command`|Serie|Identifica el mandato.|
|`format`|Serie|El formato puede ser una serie, como por ejemplo JSON.|
|`data`|Diccionario|Los datos para la carga útil. La longitud máxima es 131072 bytes.|
|`timestamp`|Fecha y hora|La fecha y hora del suceso.|


```python

def myCommandCallback(cmd):
  print("Command received: %s" % cmd.data)
  if cmd.command == "setInterval":
    if 'interval' not in cmd.data:
      print("Error - command is missing required information: 'interval'")
    else:
      interval = cmd.data['interval']
  elif cmd.command == "print":
    if 'message' not in cmd.data:
      print("Error - command is missing required information: 'message'")
    else:
      print(cmd.data['message'])

...
client.connect()
client.commandCallback = myCommandCallback
```

## Soporte de formatos de mensajes personalizado
{: #custom_message_format}

De forma predeterminada, el formato de mensajes se establece en `json`, lo que significa que la biblioteca da soporte a la codificación y decodificación de los objetos del diccionario Python en formato JSON. Cuando el formato del mensaje se establece en `json-iotf`, el mensaje se codifica de acuerdo con la especificación de carga útil JSON de {{site.data.keyword.iot_short_notm}}. Para añadir soporte para sus propios formatos de mensaje personalizados, consulte el [ejemplo de Formato de mensaje personalizado ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ibm-watson-iot/iot-python/tree/master/samples/customMessageFormat){: new_window} en GitHub.

Cuando se crea un módulo de codificador personalizado, debe registrarlo en el cliente de dispositivo, tal como se describe en el ejemplo siguiente:

```python

import myCustomCodec

client.setMessageEncoderModule("custom", myCustomCodec)
client.publishEvent("status", "custom", myData)
```
Si se envía un suceso en un formato desconocido o si un dispositivo no reconoce el formato, la biblioteca de dispositivos devuelve una condición `MissingMessageDecoderException`.
