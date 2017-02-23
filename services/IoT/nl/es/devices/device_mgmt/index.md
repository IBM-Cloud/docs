---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Protocolo de gestión de dispositivo
{: #index}

## Introducción
{: #introduction}

El {{site.data.keyword.iot_full}} reconoce dos clases de dispositivos: **dispositivos gestionados** y **dispositivos no gestionados**.

**Dispositivos gestionados** se definen como dispositivos que contienen un agente de gestión de dispositivos. Un agente de gestión de dispositivos es un conjunto de lógicas que permiten al dispositivo interactuar con el servicio de Gestión de dispositivos de {{site.data.keyword.iot_short_notm}} mediante el Protocolo de gestión de dispositivos. Los dispositivos gestionados pueden realizar operaciones de gestión de dispositivos incluidas actualizaciones de ubicación, descargas y actualizaciones de firmware, rearranques y restablecimientos de fábrica.

El protocolo de gestión de dispositivos define un conjunto de operaciones admitidas. Un agente de gestión de dispositivos puede dar soporte a un subconjunto de las operaciones, pero deben estar soportadas las operaciones **dispositivos gestionados** y **dispositivos no gestionados**. Un dispositivo que da soporte a las operaciones de acción de firmware también deben dar soporte a la observación.

El Protocolo de gestión de dispositivos se crea en la parte superior del protocolo de mensajería MQTT. Para obtener más información sobre cómo interactúa el Protocolo de gestión de dispositivos con MQTT, consulte [Conectividad de MQTT para dispositivos](../mqtt.html).


### El ciclo de vida de gestión de dispositivos

1. Un dispositivo y su tipo de dispositivo asociado se crean en el {{site.data.keyword.iot_short_notm}} mediante el panel de instrumentos o la API REST.
2. Un dispositivo se conecta al {{site.data.keyword.iot_short_notm}} y utiliza la operación **dispositivos gestionados** para convertirse en un dispositivo gestionado.
3. Puede ver y manipular los metadatos para un dispositivo utilizando las operaciones de dispositivos. Estas operaciones (por ejemplo, operaciones de actualización de firmware y de reinicio de dispositivos) se describen en la documentación 'Modelo del dispositivo'. Para obtener más información sobre el modelo del dispositivo, consulte [Modelo del dispositivo](https://console.ng.bluemix.net/docs/services/IoT/reference/device_model.html).
4. Un dispositivo puede comunicar actualizaciones sobre su ubicación, información de diagnóstico y códigos de error mediante el Protocolo de gestión de dispositivos.
5. Para manejar dispositivos anómalos en grandes poblaciones de dispositivos, la solicitud de operaciones **dispositivos gestionados** incluye un parámetro lifetime opcional. El parámetro lifetime es el número de segundos en los que el dispositivo debe realizar otra solicitud **dispositivos gestionados** para evitar que se clasifique como inactivo y que se convierta en un dispositivo no gestionado.
6. Cuando un dispositivo está desactivado, puede eliminarlo del {{site.data.keyword.iot_short_notm}} utilizando el panel de instrumentos o la API REST.

Consulte la receta [Conexión de Raspberry Pi como dispositivo gestionado a IBM Watson IoT Platform](https://developer.ibm.com/recipes/tutorials/connect-raspberry-pi-as-managed-device-to-ibm-iot-foundation/).

### Resumen de código de retorno


La tabla siguiente muestra los códigos de retorno que se generan en varias etapas durante el ciclo de vida de gestión de dispositivos.

|Código de retorno |Mensaje |
|:---|:---|
|200   |Operación satisfactoria|
|202   |Aceptado (para iniciar mandatos)|
|204   |Modificado (para actualizaciones de atributos)|
|400   |Solicitud incorrecta (por ejemplo, si un dispositivo no se encuentra en el estado adecuado para este mandato)|
|404   |No se ha encontrado el atributo (también se utiliza si la operación se ha publicado en un tema no válido)|
|409   |El recurso no se ha podido actualizar debido a un conflicto (por ejemplo, el recurso lo están actualizando dos solicitudes simultáneas, para que la actualización se pueda volver a intentar más tarde)|
|500   |Error de dispositivo inesperado|
|501   |Operación no implementada|


## Solicitudes Manage Device
{: #manage_device_request}

Un dispositivo utiliza la solicitud Manage Device para convertirse en un dispositivo gestionado. La solicitud Manage Device debe ser la primera solicitud de gestión de dispositivos enviada por el dispositivo tras conectarse al {{site.data.keyword.iot_short_notm}}. Un agente de gestión de dispositivos suele enviar este tipo de solicitud siempre que se inicie o reinicie.

**Importante:** El soporte para esta operación es obligatorio para cualquier dispositivo gestionado.


### Tema para una solicitud Manage Device

Un dispositivo publica una solicitud Manage Device en el tema siguiente:

```
iotdevice-1/mgmt/manage
```

El servidor responde a una solicitud Manage Device en el tema siguiente:

```
iotdm-1/response
```




### Formato de mensajes para una solicitud Manage Device


En una solicitud Manage Device, el campo `d` y todos sus subcampos son opcionales. Los valores de campos `metadata` y `deviceInfo` sustituyen los atributos correspondientes para el dispositivo de envío si se han enviado.

El campo opcional `lifetime` especifica la longitud de tiempo en segundos en la que el dispositivo debe enviar otra solicitud Manage Device para evitar que se clasifique como inactivo y que se convierta en un dispositivo no gestionado. Si se omite el campo `lifetime` o se establece en `0`, el dispositivo gestionado no se convierte en inactivo. El valor soportado mínimo para el campo `lifetime` es `3600` segundos, que es 1 hora.

Los campos opcionales `supports.deviceActions` y `supports.firmwareActions` indican las funciones del agente de gestión de dispositivos. Si se establece `supports.deviceActions`, el agente dará soporte a las acciones de reinicio y de restablecimiento de fábrica. Para un dispositivo que no distingue entre un reinicio y un restablecimiento de fábrica, es aceptable utilizar el mismo comportamiento para las dos acciones. Si se establece `supports.firmwareActions`, el agente da soporte a las acciones de descarga y de actualización de firmware.

El ejemplo siguiente muestra el formato de la solicitud:

```
Mensaje saliente del dispositivo:

Tema: iotdevice-1/mgmt/manage
{
    "d": {
        "metadata":{},
        "lifetime": number,
        "supports": {
            "deviceActions": boolean,
            "firmwareActions": boolean
        },
        "deviceInfo": {
            "serialNumber": "string",
            "manufacturer": "string",
            "model": "string",
            "deviceClass": "string",
            "description" :"string",
            "fwVersion": "string",
            "hwVersion": "string",
            "descriptiveLocation": "string"
        }
    },
    "reqId": "string"
}
```

El ejemplo siguiente muestra el formato de la respuesta:

```
Mensaje entrante del servidor:

Tema: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```


### Códigos de respuesta para una solicitud Manage Device

|Código de respuesta |Mensaje |
|:---|:---|
|200   |La operación ha sido satisfactoria.|
|400   |El mensaje de entrada no coincide con el formato esperado, o uno de los valores está fuera del rango válido.|
|404   |El nombre del tema es incorrecto, o el dispositivo no se encuentra en la base de datos.|
|409   |Se ha producido un conflicto durante la actualización de la base de datos del dispositivo. Para resolver este conflicto, simplifique la operación si es necesario.|


## Solicitudes Unmanage Device
{: #manage-unmanage}


Un dispositivo utiliza una solicitud Unmanage Device cuando ya no necesita ser gestionado. Cuando un dispositivo se convierte en no gestionado, {{site.data.keyword.iot_short_notm}} dejará de enviar nuevas solicitudes de gestión de dispositivos al dispositivo. Los dispositivos no gestionados siguen publicando códigos de error, mensajes de registro y mensajes de ubicación.
**Importante:** El soporte para esta operación es obligatorio para cualquier dispositivo gestionado.

### Tema para una solicitud Unmanage Device


Un dispositivo publica una solicitud Unmanage Device en el tema siguiente:

```
iotdevice-1/mgmt/unmanage
```

El servidor responde a una solicitud Unmanage Device en el tema siguiente:

```
iotdm-1/response
```

### Formato de mensaje para una solicitud Unmanage Device

Formato de solicitud:

```
Mensaje saliente del dispositivo:

Tema: iotdevice-1/mgmt/unmanage
{
    "reqId": "string"
}
```

Formato de respuesta:

```
Mensaje entrante del servidor:

Tema: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### Códigos de respuesta para una solicitud Unmanage Device

|Código de respuesta |Mensaje |
|:---|:---|
|200   |La operación ha sido satisfactoria.|
|400   |El mensaje de entrada no coincide con el formato esperado, o uno de los valores está fuera del rango válido.|
|404   |El nombre del tema es incorrecto, o el dispositivo no se encuentra en la base de datos.|
|409   |Se ha producido un conflicto durante la actualización de la base de datos del dispositivo. Para resolver este conflicto, simplifique la operación si es necesario.|


## Solicitudes Update Location
{: #update-location}

Un dispositivo utiliza una solicitud Update Location para gestionar los datos de la ubicación para un dispositivo. Los metadatos de ubicación para un dispositivo pueden actualizarse en {{site.data.keyword.iot_short_notm}} de las siguientes maneras:

#### Actualizaciones automáticas de la ubicación de dispositivo
- El dispositivo notifica a {{site.data.keyword.iot_short_notm}} sobre la actualización de la ubicación. El dispositivo recupera su ubicación de un receptor GPS y envía un mensaje de gestión de dispositivos a la instancia de {{site.data.keyword.iot_short_notm}} para actualizar su ubicación. La indicación de fecha y hora captura la hora a la que se ha recuperado la ubicación desde el receptor GPS. La indicación de fecha y hora es válida aunque haya un retraso en el envío del mensaje de actualización de la ubicación. Si se omite la indicación de fecha y hora del mensaje de gestión de dispositivos, la fecha y hora de la recepción del mensaje se utiliza para actualizar los metadatos de ubicación.

#### Actualizaciones manuales de ubicación de dispositivos utilizando la API REST
- Puede establecer manualmente los metadatos de ubicación para un dispositivo estático utilizando la API REST de {{site.data.keyword.iot_short_notm}} cuando el dispositivo esté registrado. También puede modificar la ubicación más adelante. El valor de indicación de fecha y hora es opcional, pero cuando se omite, la fecha y hora actuales se establece en los metadatos de ubicación para el dispositivo.

### Actualizaciones de ubicación desencadenadas por dispositivos

Los dispositivos que pueden determinar su ubicación pueden elegir notificar al servidor de gestión de dispositivos de {{site.data.keyword.iot_short_notm}} sobre los cambios de ubicación.

### Tema para una solicitud Update Location desencadenada mediante un dispositivo:


Un dispositivo publica una solicitud Update Location en el tema siguiente:

```
iotdevice-1/device/update/location
```

El servidor responde a una solicitud Update Location en el tema siguiente:

```
iotdm-1/response
```

### Actualización de ubicación desencadenada por usuarios o aplicaciones


Cuando un usuario o aplicación actualiza la ubicación de un dispositivo gestionado activo, el dispositivo recupera un mensaje de actualización.




### Tema para una solicitud Update Location desencadenada por usuarios o aplicaciones


El servidor publica una solicitud Update Location en el tema siguiente:

```
iotdm-1/device/update
```

### Formato de mensaje para una solicitud Update location


El campo `measuredDateTime` es la fecha de medida de ubicación. El campo `updatedDateTime` es la fecha de la actualización a la información de dispositivo. Por motivos de eficiencia, {{site.data.keyword.iot_short_notm}} a veces procesa actualizaciones a la información de ubicación de modo que las actualizaciones se retrasan ligeramente. La latitud y longitud deben especificarse en grados decimales utilizando World Geodetic System 1984 (WGS84).

Siempre que se actualiza la ubicación, los valores que se proporcionan para latitud, longitud, elevación e incertidumbre se consideran una sola actualización de varios valores. La latitud y la longitud son obligatorios y ambos deben proporcionarse con cada actualización.  La elevación y la incertidumbre son opcionales y se pueden omitir.

Si se suministra un valor opcional en una actualización y posteriormente se omite en una actualización posterior, el valor más antiguo se suprime por la actualización posterior. Cada actualización se considera un conjunto de varios valores completo.

### Las actualizaciones de ubicación que están desencadenadas por el dispositivo


Formato de solicitud:

```
Mensaje saliente del dispositivo:

Topic: iotdevice-1/device/update/location
{
    "d": {
        "longitude": number,
        "latitude": number,

        "elevation": number,
        "measuredDateTime": "string in ISO8601 format",
        "updatedDateTime": "string in ISO8601 format",
        "accuracy": number
    },
    "reqId": "string"
}
```

Formato de respuesta:

```
Mensaje entrante del servidor:

Tema: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### Códigos de respuesta para una solicitud Update Location

|Código de respuesta |Mensaje |
|:---|:---|
|200   |La operación ha sido satisfactoria.|
|400   |El mensaje de entrada no coincide con el formato esperado, o uno de los valores está fuera del rango válido.|
|404   |El nombre del tema es incorrecto, o el dispositivo no se encuentra en la base de datos.|
|409   |Se ha producido un conflicto durante la actualización de la base de datos del dispositivo. Para resolver este conflicto, simplifique la operación si es necesario.|


### Actualizaciones de ubicación desencadenadas por usuarios o aplicaciones


El siguiente ejemplo describe el formato de la carga útil:

```
Mensaje entrante del servidor:

Topic: iotdm-1/device/update
{
    "d": {
        "fields": [
            {
                "field": "location",
                "value": {
                    "latitude": number,
                    "longitude": number,
                    "elevation": number,
                    "accuracy": number,
                    "measuredDateTime": "string in ISO8601 format"
                }
            }
        ]
    }
}
```

**Nota:** No se utiliza el parámetro `reqID`, porque el dispositivo no es necesario para responder.

## Solicitudes Update Device Attribute
{: #update-attributes}

Al utilizar la API REST, {{site.data.keyword.iot_short_notm}} puede enviar una solicitud a un dispositivo para actualizar el valor de uno o varios de los siguientes atributos de dispositivos:


|Atributo | Más información|
|:---|:---|
|ubicación  | Consulte [Actualizar ubicación](index.html#update-location)|
|metadatos  | Opcional|
|deviceInfo | Opcional|
|mgmt.firmware | Consulte [Proceso de actualización de firmware](requests.html#firmware-actions-update)|

### Tema para una solicitud Update Device Attributes


El servidor publica la solicitud de actualización de dispositivos en el tema siguiente:

```
iotdm-1/device/update
```


### Formato de mensajes para una solicitud Update Device Attributes


El ejemplo siguiente describe el formato de la carga útil para la solicitud:

```
Mensaje entrante del servidor:

Topic: iotdm-1/device/update
{
    "d": {
        "fields": [
            {
                "field": "location",
                "value": ""
            }
        ]
    }
}
```


## Solicitudes Add Error Codes
{: #diag-add-error-code}

Los dispositivos pueden elegir notificar al servidor de gestión de dispositivos {{site.data.keyword.iot_short_notm}} acerca de los cambios en su estado de error utilizando el tipo de solicitud Add Error Codes.

### Tema para una solicitud Add Error Codes


Un dispositivo publica una solicitud Add Error Codes en el tema siguiente:

```
iotdevice-1/add/diag/errorCodes
```

### Formato de mensaje para una solicitud Add Error Codes


El valor que está asociado con `errorCode` es el código de error de dispositivos actuales y debe añadirse a la {{site.data.keyword.iot_short_notm}}.

Formato de solicitud:

```
Mensaje saliente del dispositivo:

Topic: iotdevice-1/add/diag/errorCodes
{
    "d": {
        "errorCode": number
    },
    "reqId": "string"
}
```

Formato de respuesta:

```
Mensaje entrante del servidor:

Tema: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### Códigos de respuesta para una solicitud Add Error Codes

|Código de respuesta |Mensaje |
|:---|:---|
|200   |La operación ha sido satisfactoria.|
|400   |El mensaje de entrada no coincide con el formato esperado, o uno de los valores está fuera del rango válido.|
|404   |El nombre del tema es incorrecto, o el dispositivo no se encuentra en la base de datos.|
|409   |Se ha producido un conflicto durante la actualización de la base de datos del dispositivo. Para resolver este conflicto, simplifique la operación si es necesario.|


## Solicitudes Clear Error Codes
{: #diag-clear-error-codes}

Los dispositivos pueden solicitar que {{site.data.keyword.iot_short_notm}} borre todos los códigos de error para el dispositivo utilizando el tipo de solicitud Clear Error Codes.

### Tema para una solicitud Clear Error Codes


Un dispositivo publica esta solicitud en el tema siguiente:

```
iotdevice-1/clear/diag/errorCodes
```

### Formato de mensaje para una solicitud Clear Error Codes


Formato de solicitud:

```
Mensaje saliente del dispositivo:

Topic: iotdevice-1/clear/diag/errorCodes
{
    "reqId": "string"
}
```

Formato de respuesta:

```
Mensaje entrante del servidor:

Tema: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### Códigos de respuesta para una solicitud Clear Error Codes

|Código de respuesta |Mensaje |
|:---|:---|
|200   |La operación ha sido satisfactoria.|
|400   |El mensaje de entrada no coincide con el formato esperado, o uno de los valores está fuera del rango válido.|
|404   |El nombre del tema es incorrecto, o el dispositivo no se encuentra en la base de datos.|
|409   |Se ha producido un conflicto durante la actualización de la base de datos del dispositivo. Para resolver este conflicto, simplifique la operación si es necesario.|


## Solicitudes Add Log
{: #diag-add-log}

Los dispositivos pueden elegir si notificar al soporte de gestión de dispositivos de {{site.data.keyword.iot_short_notm}} sobre los cambios añadiendo una nueva entrada de registro. Las entradas de registro incluyen un mensaje de registro, una indicación de fecha y hora, una gravedad y datos de diagnóstico binarios codificados como base64 opcionales.

### Tema para una solicitud Add Log
Un dispositivo publica esta solicitud en el tema siguiente:

```
iotdevice-1/add/diag/log
```


### Formato de mensaje para una solicitud Add Log

La tabla siguiente describe el formato de los atributos de mensaje saliente:

|Atributo |Descripción |
|:---|:---|
|`message`|Especifica un mensaje de diagnóstico que es necesario añadir a {{site.data.keyword.iot_short_notm}}|
|`timestamp`|Especifica la fecha y hora de la entrada de registro en formato ISO8601 |
|`data`|Especifica los datos de diagnóstico codificados como base64 opcionales|
|`severity`|Especifica la gravedad del mensaje (0: informativo, 1: aviso, 2: error)|


Formato de solicitud:

```
Mensaje saliente del dispositivo:

Topic: iotdevice-1/add/diag/log
{
    "d": {
        "message": string,
        "timestamp": string,
        "data": string,
        "severity": number
    },
    "reqId": "string"
}
```

Formato de respuesta:

```
Mensaje entrante del servidor:

Tema: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```


### Códigos de respuesta para una solicitud Add Log

|Código de respuesta |Mensaje |
|:---|:---|
|200   |La operación ha sido satisfactoria.|
|400   |El mensaje de entrada no coincide con el formato esperado, o uno de los valores está fuera del rango válido.|
|404   |El nombre del tema es incorrecto, o el dispositivo no se encuentra en la base de datos.|
|409   |Se ha producido un conflicto durante la actualización de la base de datos del dispositivo. Para resolver este conflicto, simplifique la operación si es necesario.|

## Solicitudes Clear Logs
{: #diag-clear-logs}

Los dispositivos pueden solicitar que {{site.data.keyword.iot_short_notm}} borre todas las entradas del registro para el dispositivo utilizando el tipo de solicitud Clear Logs.

### Tema para una solicitud Clear Logs


Un dispositivo publica una solicitud Clear Logs en el tema siguiente:

```
iotdevice-1/clear/diag/log
```

### Formato de mensaje para una solicitud Clear Logs


Formato de solicitud:

```
Mensaje saliente del dispositivo:

Topic: iotdevice-1/clear/diag/log
{
    "reqId": "string"
}
```

Formato de respuesta:

```
Mensaje entrante del dispositivo:

Tema: iotdm-1/response
{
    "rc": 200,
    "reqId": "string"
}
```

### Códigos de respuesta para una solicitud Clear Logs

|Código de respuesta |Mensaje |
|:---|:---|
|200   |La operación ha sido satisfactoria.|
|400   |El mensaje de entrada no coincide con el formato esperado, o uno de los valores está fuera del rango válido.|
|404   |El nombre del tema es incorrecto, o el dispositivo no se encuentra en la base de datos.|
|409   |Se ha producido un conflicto durante la actualización de la base de datos del dispositivo. Para resolver este conflicto, simplifique la operación si es necesario.|

## Solicitudes Observe Attribute Changes
{: #observations-observe}

{{site.data.keyword.iot_short_notm}} puede enviar una solicitud Observe Attribute Change a un dispositivo para observar los cambios de uno o varios atributos de dispositivos utilizando el tipo de solicitud Observe Attribute Changes. Cuando el dispositivo reciba la solicitud, debe enviar una solicitud de notificación a {{site.data.keyword.iot_short_notm}} siempre que los valores de los atributos observados cambien.

**Importante:** Los dispositivos deben implementar, observar, notificar y cancelar operaciones para dar soporte a los tipos de solicitud [Firmware Actions- Update](requests.html#firmware-actions-update).

### Tema para una solicitud Observe Attribute Changes


El servidor publica una solicitud Observe Attribute Changes en el tema siguiente:

```
iotdm-1/observe
```

### Formato de mensaje para una solicitud Observe Attribute Changes


La matriz `fields` es una matriz del atributo de dispositivos del modelo de dispositivo. Si se especifica un campo complejo, como por ejemplo `mgmt.firmware`, se espera que sus campos subyacentes se actualicen al mismo tiempo para que sólo se genere un mensaje de notificación único.

El parámetro `message` que se utiliza en la respuesta puede especificarse si el valor del parámetro `rc` no es `200`. Si no se puede recuperar ningún valor de parámetro especificado, el valor del parámetro `rc` debe establecerse en `404` si no se encuentra el dispositivo, o en `500` por cualquier otro motivo. Cuando no se pueden encontrar los valores para los parámetros, la matriz `fields` debería contener elementos que tengan `field` establecido en el nombre de cada parámetro que no se podía leer. El parámetro `value` debería omitirse. Para que el parámetro response code se establezca en `200`, se deben especificar `field` y `value`, donde `value` es el valor actual de un atributo especificado por el valor del parámetro `field`.

Formato de solicitud:

```
Mensaje entrante del servidor:

Topic: iotdm-1/observe
{
    "d": {
        "fields": [
            "string"
        ]
    },
    "reqId": "string"
}
```

Formato de respuesta:

```
Mensaje saliente del dispositivo:

Tema: iotdevice-1/response
{
    "rc": number,
    "message": "string",
    "d": {
        "fields": [
            {
                "field": "field_name",
                "value": "field_value"
            }
        ]
    },
    "reqId": "string"
}
```


## Solicitudes Cancel Attribute Observation
{: #observations-cancel}

{{site.data.keyword.iot_short_notm}} puede enviar una solicitud a un dispositivo para cancelar la observación actual de uno o varios atributos de dispositivos utilizando el tipo de solicitud Cancel Attribute Observation. La parte `fields` de la solicitud es una matriz de los nombres de atributos de dispositivos del modelo de dispositivos, como por ejemplo los parámetros `location`, `mgmt.firmware` o `mgmt.firmware.state`.

El parámetro `message` debe especificarse si el valor del parámetro `rc` no es `200`.

**Importante:** Los dispositivos deben implementar, observar, notificar y cancelar operaciones para dar soporte a los tipos de solicitud [Firmware Actions- Update](requests.html#firmware-actions-update).

### Tema para una solicitud Cancel Attribute Observation


El servidor publica una solicitud Cancel Attribute Observation en el tema siguiente:

```
iotdm-1/cancel
```


### Formato de mensaje para una solicitud Cancel Attribute Observation


Formato de solicitud:

```
Mensaje entrante del servidor:

Topic: iotdm-1/cancel
{
    "d": {
        "fields": [
            "string"
        ]
    },
    "reqId": "string"
}
```

Formato de respuesta:

```
Mensaje saliente del dispositivo:

Tema: iotdevice-1/response
{
    "rc": number,
    "message": "string",
    "reqId": "string"
}
```



## Solicitudes Notify Attribute Changes
{: #observations-notify}

{{site.data.keyword.iot_short_notm}} puede solicitar una solicitud de observación para un atributo específico o un conjunto de valores utilizando el tipo de solicitud Notify Attribute Changes. Cuando el valor del atributo o atributos cambia, el dispositivo debe enviar una notificación que contenga el valor más reciente.

El valor del parámetro `field_name` es el nombre del atributo que ha cambiado, y el `field_value` es el valor actual del atributo. El atributo puede ser un campo complejo. Si se actualizan varios valores de un campo complejo como resultado de una sola operación, sólo se enviará un único mensaje de notificación.

Cuando la solicitud de notificación se haya procesado correctamente, el valor del parámetro `rc` se establece en `200`. Si la solicitud no es correcta, el valor del parámetro `rc` se establece en `400`. Si el parámetro que se especifica en la solicitud de notificación no se observa, el valor del parámetro `rc` se establece en `404`.

**Importante:** Los dispositivos deben implementar, observar, notificar y cancelar operaciones para dar soporte a los tipos de solicitud [Firmware Actions- Update](requests.html#firmware-actions-update).


### Tema para una solicitud Notify Attribute Change


Un dispositivo publica una solicitud Notify Attribute Change en el tema siguiente:

```
iotdevice-1/notify
```


### Formato de mensaje para una solicitud Notify Attribute Change


Formato de solicitud:

```
Mensaje saliente del dispositivo:

Topic: iotdevice-1/notify
{
    "d": {
        "field": "field_name",
        "value": "field_value"
    }
    "reqId": "string"
}
```

Formato de respuesta:

```
Mensaje entrante del servidor:

Tema: iotdm-1/response
{
    "rc": number,
    "reqId": "string"
}
```

### Códigos de respuesta para una solicitud Notify Attribute Change

|Código de respuesta |Mensaje |
|:---|:---|
|200   |La operación ha sido satisfactoria.|
|400   |El mensaje de entrada no coincide con el formato esperado, o uno de los valores está fuera del rango válido.|
|404   |El nombre del tema es incorrecto, o el dispositivo no está en la base de datos, o no hay ninguna observación para el campo del que se ha informado.|
|409   |Se ha producido un conflicto durante la actualización de la base de datos del dispositivo. Para resolver este conflicto, simplifique la operación si es necesario.|
|500   |Se ha producido un error interno.|
