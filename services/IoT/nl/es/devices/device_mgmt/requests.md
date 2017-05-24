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


# Solicitudes de gestión de dispositivos
{: #requests}


El {{site.data.keyword.iot_full}} proporciona acciones que se pueden iniciar para uno o varios dispositivos. Estas acciones se pueden iniciar mediante el panel de instrumentos o la API REST. Los tipos de acciones disponibles son **acciones de dispositivos** y **acciones de firmware**.

## Iniciación de las solicitudes de gestión de dispositivos mediante el panel de instrumentos
{: #initiating-dm-dashboard}

Se pueden iniciar solicitudes mediante el panel de control utilizando al separador **Acciones** de la página Dispositivos. Pulse **Iniciar acción** para seleccionar una acción, seleccione los dispositivos y especifique cualquier parámetro adicional al que da soporte la acción seleccionada.

## Iniciación de las solicitudes de gestión de dispositivos mediante la API REST
{: #initiating-dm-api}

Las solicitudes se pueden iniciar utilizando el siguiente ejemplo API REST:  

`POST https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

Para obtener más información sobre el cuerpo de una solicitud de gestión de dispositivos, consulte la [Documentación de la API ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}.

## Acciones de dispositivos
{: #device-actions}

Un dispositivo puede especificar que da soporte a las acciones de dispositivos cuando publica una solicitud de gestión. Una solicitud device action indica a la {{site.data.keyword.iot_short_notm}} que el dispositivo está disponible para responder a acciones de rearranque de dispositivo y de restablecimiento de dispositivo.


## Acciones de dispositivos: rearrancar
{: #device-actions-reboot}

Puede iniciar la acción de reinicio de dispositivo mediante el panel de instrumentos de {{site.data.keyword.iot_short_notm}} o mediante la API REST.

Para iniciar un rearranque de dispositivo utilizando la API REST, emita una solicitud POST en:

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

Proporcione la siguiente información:

- La acción `device/reboot`
- Una lista de dispositivos que se rearrancan, con un máximo de 5000 dispositivos

Ejemplo de solicitud de rearranque de dispositivo:

```
{
    "action": "device/reboot",
    "devices": [
        {
            "typeId": "someType",
            "deviceId": "someId"
        }
    ]
}
```

Una vez que se inicie una solicitud, se publicará un mensaje MQTT en todos los dispositivos especificados en el cuerpo de la solicitud de reinicio. Para cada dispositivo, se debe enviar de vuelta una respuesta para indicar si se puede iniciar la acción de reinicio. Si esta operación se puede iniciar inmediatamente, establezca el parámetro `rc` en `202`. Si falla el intento de reinicio, establezca el parámetro `rc` en `500` y establezca el parámetro `message` en consonancia. Si el rearranque no está soportado, establezca el parámetro `rc` en `501` y establezca opcionalmente el parámetro `message` en consonancia.

La acción de reinicio se completa cuando el dispositivo envía una solicitud Manage Device después del rearranque.

### Tema para la solicitud device reboot

El servidor publica una solicitud de rearranque en un dispositivo en el tema siguiente:

```
iotdm-1/mgmt/initiate/device/reboot
```

### Formato de mensaje para la solicitud device reboot


Formato de solicitud:

```
Mensaje entrante del servidor:

Tema: iotdm-1/mgmt/initiate/device/reboot
{
    "reqId": "string"
}
```

Formato de respuesta:

```
Mensaje saliente del dispositivo:

Tema: iotdevice-1/response
{
    "rc": "response_code",
    "message": "string",
    "reqId": "string"
}
```

## Acciones de dispositivos: restablecimiento de fábrica
{: #device-actions-factory-reset}

Puede iniciar la acción de restablecimiento de fábrica utilizando el panel de instrumentos {{site.data.keyword.iot_short_notm}} o utilizando la API REST.

Para iniciar un restablecimiento de fábrica de dispositivo utilizando la API REST, emita una solicitud POST en:

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

Se proporcionará la siguiente información:

- La acción `device/factoryReset`
- Una lista de dispositivos a restablecer, con un máximo de 5000 dispositivos

El ejemplo siguiente proporciona una solicitud de restablecimiento de dispositivos de ejemplo:

```
{
    "action": "device/factoryReset",
    "devices": [
        {
            "typeId": "someType",
            "deviceId": "someId"
        }
    ]
}
```

Cuando se inicia una solicitud de restablecimiento de dispositivos, se publicará un mensaje MQTT en todos los dispositivos especificados en el cuerpo de la solicitud. Para cada dispositivo, debe devolverse una respuesta para indicar si la acción de restablecimiento de fábrica se puede iniciar. El código de respuesta se establece en `202` si esta acción se puede iniciar inmediatamente. Si falla el intento de restablecimiento de fábrica, establezca el parámetro `rc` en `500` y establezca el parámetro `message` en consonancia. Si la acción de restablecimiento de fábrica no está soportada, establezca el parámetro `rc` en `501` y, opcionalmente, establezca el parámetro `message` en consonancia.

La acción de restablecimiento de fábrica se completa cuando el dispositivo envía una solicitud Manage Device después del restablecimiento de fábrica.

### Tema para la solicitud factory reset

El servidor publica la solicitud siguiente en un dispositivo:

```
iotdm-1/mgmt/initiate/device/factory_reset
```


### Formato de mensaje para la solicitud factory reset


Formato de solicitud:

```
El tema siguiente muestra el mensaje entrante del servidor:

Topic: iotdm-1/mgmt/initiate/device/factory_reset
{
    "reqId": "string"
}
```

Formato de respuesta:

```
El tema siguiente muestra un mensaje saliente del dispositivo:

Tema: iotdevice-1/response
{
    "rc": "response_code",
    "message": "string",
    "reqId": "string"
}
```


## Acciones de firmware
{: #firmware-actions}

El nivel de firmware conocido para estar en un dispositivo se almacena en el atributo `deviceInfo.fwVersion`. Los atributos `mgmt.firmware` se utilizan para realizar una actualización de firmware y observar su estado.

**Importante:** El dispositivo gestionado debe dar soporte a la observación del atributo `mgmt.firmware` para dar soporte a las acciones de firmware.

El proceso de actualización de firmware está separado en acciones distintas:
- Descarga de firmware
- Actualización de firmware

El estado de cada acción de firmware se almacena en otro atributo en el dispositivo. El atributo `mgmt.firmware.state` describe el estado de la descarga de firmware. En la tabla siguiente se describen los valores posibles que se pueden establecer para el atributo `mgmt.firmware.state`:

 |Valor |Estado  | Significado |
 |:---|:---|:---|
 |0  | Desocupado        | El dispositivo no está descargando firmware. |  
 |1  | Descargando | El dispositivo está descargando firmware. |
 |2  | Descargado  | El dispositivo ha descargado satisfactoriamente una actualización de firmware y está preparado para instalarla. |


El atributo `mgmt.firmware.updateStatus` describe el estado de la actualización de firmware. Los valores posibles del atributo `mgmt.firmware.updateStatus` son:

|Valor |Estado | Significado |  
|:---|:---|:---|
|0 | Correcto | El firmware se ha actualizado correctamente. |
|1 | En curso | La actualización de firmware se ha iniciado pero no se ha completado todavía.|
|2 | Fuera de memoria | Se ha detectado una condición de fuera de memoria durante la operación.|
|3 | Se ha perdido la conexión     | La conexión se ha perdido durante la descarga de firmware. |
|4 | La verificación ha fallado | El firmware no ha pasado la verificación. |
|5 | Imagen no soportada   | La imagen de firmware descargada no está soportada por el dispositivo. |
|6 | URI no válido         | El dispositivo no ha podido descargar el firmware desde la URI proporcionada. |

## Acciones de firmware: descargar
{: #firmware-actions-download}

Puede iniciar la acción de descarga de firmware mediante el panel de instrumentos de {{site.data.keyword.iot_short_notm}} o mediante la API REST.

Para iniciar una descarga de firmware mediante la API REST, emita una solicitud POST en:

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

Se proporcionará la siguiente información:

- La acción `firmware/download`
- Una lista de dispositivos para recibir la imagen, con un máximo de 5000 dispositivos
- El URI de la imagen de firmware (opcional)
- Serie de verificación para validar la imagen (opcional)
- Nombre de firmware (opcional)
- Versión de firmware (opcional)

En el ejemplo siguiente se muestra la solicitud de descarga de firmware en la que se basan todos los mensajes de ejemplo siguientes:

```
{
   "action" : "firmware/download",
   "parameters" : [{
         "name" : "uri",
         "value" : "some uri for firmware location"
      }, {
         "name" : "name",
         "value" : "some firmware name"
      }, {
         "name" : "verifier",
         "value" : "some validation code"
      }, {
         "name" : "version",
         "value" : "some firmware version"
      }
   ],
   "devices" : [{
         "typeId" : "someType",
         "deviceId" : "someId"
      }
   ]
}
```

Si no se especifica ningún parámetro opcional, se omitirá el primer paso del siguiente proceso.

El servidor de gestión de dispositivos de {{site.data.keyword.iot_short_notm}} utiliza el Protocolo de gestión de dispositivos para enviar una solicitud a los dispositivos, lo que inicia la descarga de firmware. El proceso de descarga consta de los pasos siguientes:

1. Se envía una solicitud de actualización de detalles de firmware en el tema `iotdm-1/device/update`.
La solicitud de actualización permite validarse al dispositivo si el firmware solicitado difiere del firmware actualmente instalado. Si hay una diferencia, establezca el parámetro `rc` en `204`, que se convierte en el estado `Changed`.  
En el ejemplo siguiente se muestra qué mensaje se espera para la solicitud de descarga de firmware de ejemplo enviada anteriormente y qué respuesta se envía cuando se detecta una diferencia:
```
   Solicitud entrante de la {{site.data.keyword.iot_short_notm}}:

   Tema: iotdm-1/device/update
   Mensaje:
   {
      "reqId" : "f38faafc-53de-47a8-a940-e697552c3194",
      "d" : {
         "fields" : [{
               "field" : "mgmt.firmware",
               "value" : {
                  "version" : "some firmware version",
                  "name" : "some firmware name",
                  "uri" : "some uri for firmware location",
                  "verifier" : "some validation code",
                  "state" : 0,
                  "updateStatus" : 0,
                  "updatedDateTime" : ""
               }
            }
         ]
      }
   }

   Respuesta saliente del dispositivo:

   Tema: iotdevice-1/response
   Mensaje:
   {
      "rc" : 204,
      "reqId" : "f38faafc-53de-47a8-a940-e697552c3194"
   }
   ```
   Esta respuesta desencadena la siguiente solicitud.
2. Se ha enviado la solicitud de observación para el estado de descarga de firmware `iotdm-1/observe`.
La solicitud de observación verifica si el dispositivo está preparado para iniciar la descarga de firmware. Cuando la descarga puede iniciarse de forma inmediata, establezca el parámetro `rc` en `200` (`Aceptar`), el atributo `mgmt.firmware.state` en
   `0` (`Desocupado`) y el atributo `mgmt.firmware.updateStatus` en `0` (`Desocupado`). El código siguiente es un intercambio de ejemplo entre el {{site.data.keyword.iot_short_notm}} y el dispositivo:
   ```
   Solicitud entrante de la {{site.data.keyword.iot_short_notm}}:

   Tema: iotdm-1/observe
   Mensaje:
   {
      "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8",
      "d" : {
         "fields" : [ {
            "field" : "mgmt.firmware"
            }
         ]
      }
   }

   Respuesta saliente del dispositivo:

   Tema: iotdevice-1/response
   Mensaje:
   {
      "rc" : 200,
      "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8"
   }
   ```
Este intercambio desencadena el último paso.  

3. La solicitud de descarga se envía en el tema `iotdm-1/mgmt/initiate/firmware/download`:

   La solicitud de descarga indica a un dispositivo que empiece la descarga de firmware. Si la acción se puede iniciar inmediatamente, establezca el parámetro `rc` en `202`. El código siguiente proporciona un ejemplo de la iniciación de una solicitud de descarga:

   ```
   Solicitud entrante de la {{site.data.keyword.iot_short_notm}}:

   Tema: iotdm-1/mgmt/initiate/firmware/download
   Mensaje:
   {
      "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
   }

   Respuesta saliente del dispositivo:

   Tema: iotdevice-1/response
   Mensaje:
   {
      "rc" : 202,
      "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
   }
   ```

Después de que se inicie una descarga de firmware de esta forma, el dispositivo necesita informar sobre el estado de la descarga al {{site.data.keyword.iot_short_notm}}. El dispositivo informa del estado publicando un mensaje en el tema `iotdevice-1/notify`, donde el atributo `mgmt.firmware.state` se establece en `1` (`Descargando`) o `2` (`Descargado`).
Los ejemplos siguientes muestran un ejemplo de la iniciación de la descarga de firmware:

```
Mensaje saliente del dispositivo:

Tema: iotdevice-1/notify
Mensaje:
{
   "reqId" : "123456789",
   "d" : {
      "fields" : [ {
         "field" : "mgmt.firmware",
         "value" : {
                 "state" : 1
             }
      } ]
   }
}


Espere un momento...


Mensaje saliente del dispositivo:

Tema: iotdevice-1/notify
Mensaje:
{
   "reqId" : "1234567890",
   "d" : {
      "fields" : [ {
         "field" : "mgmt.firmware",
         "value" : {
                 "state" : 2
             }
      } ]
   }
}
```



Una vez que se publique la notificación con el atributo `mgmt.firmware.state` establecido en `2`, se desencadenará una solicitud en el tema `iotdm-1/cancel`. Esta solicitud cancela la observación del atributo `mgmt.firmware`.
Después de que se envíe una respuesta que tenga el parámetro `rc` establecido en `200`, la descarga de firmware se habrá completado. El código siguiente proporciona un ejemplo:

```
Solicitud entrante de la {{site.data.keyword.iot_short_notm}}:

Tema: iotdm-1/cancel
Mensaje:
{
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f",
   "d" : {
      "fields" : [{
            "field" : "mgmt.firmware"
         }
      ]
   }
}


Mensaje saliente del dispositivo:

Tema: iotdevice-1/response
Mensaje:
{
   "rc" : 200,
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f"
}
```

La siguiente información es útil para el manejo de errores:

- Si el atributo `mgmt.firmware.state` no es `0` ("Desocupado"), envía un error que tiene el código de respuesta `400` y un texto de mensaje opcional.
- Si el atributo `mgmt.firmware.uri` no está establecido o no es un URI válido, establezca el parámetro `rc` en `400`.
- Si falla el intento de descarga de firmware, establezca el parámetro `rc` en `500` y, opcionalmente, establezca el parámetro `message` en consonancia.
- Si la descarga de firmware no está soportada, establezca el parámetro `rc` en `500` y, opcionalmente, establezca el parámetro `message` en consonancia.
- Cuando el dispositivo reciba una solicitud de ejecución, cambie el atributo `mgmt.firmware.state` de `0` (Desocupado) a `1` (Descargando).
- Cuando la descarga se haya completado correctamente, establezca el atributo `mgmt.firmware.state` en `2` (Descargado).
- Si se produce un error durante la descarga, establezca el atributo `mgmt.firmware.state` en `0` (Desocupado) y establezca el atributo `mgmt.firmware.updateStatus` en uno de los siguientes valores de estado de error:
  - 2 (Sin memoria)
  - 3 (Se ha perdido la conexión)
  - 6 (URI no válido)
- Si se ha establecido un verificador de firmware, el dispositivo intenta verificar la imagen de firmware. Si falla la verificación de la imagen, establezca el atributo `mgmt.firmware.state` en `0` (Desocupado) y establezca el atributo `mgmt.firmware.updateStatus` en el valor de estado de error `4` (La verificación ha fallado).

## Acciones de firmware: actualizar
{: #firmware-actions-update}

La instalación del firmware descargado se inicia utilizando la API REST emitiendo una solicitud POST a:

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

Se proporcionará la siguiente información:

- La acción `firmware/update`
- La lista de dispositivos que recibirán la imagen, todos con el mismo tipo de dispositivo.
- El URI de la imagen de firmware (opcional)
- Serie de verificación para validar la imagen (opcional)
- Nombre de firmware (opcional)
- Versión de firmware (opcional)

El código siguiente es una solicitud de ejemplo:

```
   {
      "action" : "firmware/update",
      "devices" : [{
            "typeId" : "someType",
            "deviceId" : "someId"
         }
      ]
   }

```

Si no se especifica ningún parámetro opcional, el primer mensaje que reciba el dispositivo será una solicitud de actualización de dispositivo. Esta solicitud de actualización de dispositivo es similar al primer mensaje de la solicitud de descarga de firmware.

Para supervisar el estado de la actualización de firmware, el {{site.data.keyword.iot_short_notm}} primero desencadena una solicitud de observador en el tema `iotdm-1/observe`. Cuando el dispositivo esté listo para iniciar el proceso de actualización, se envía una respuesta que tenga el parámetro `rc` establecido en `200`, el atributo `mgmt.firmware.state` establecido en `0`, y el atributo `mgmt.firmware.updateStatus` establecido en `0`.

El código siguiente proporciona un ejemplo:

```
Solicitud entrante de la {{site.data.keyword.iot_short_notm}}:

Tema: iotdm-1/observe
Mensaje:
{
   "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8",
   "d" : {
      "fields" : [
         {
            "field": "mgmt.firmware"
         }
      ]
   }
}

Respuesta saliente del dispositivo:

Tema: iotdevice-1/response
Mensaje:
{
   "rc" : 200,
   "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8",
   "d" : {
      "fields" : [{
            "field" : "mgmt.firmware",
            "value" : {
               "state" : 0,
               "updateStatus" : 0
            }
         }
      ]
   }
}
```



Cuando la actualización de firmware se haya descargado satisfactoriamente, el servidor de gestión de dispositivos del {{site.data.keyword.iot_short_notm}} utiliza el Protocolo de gestión de dispositivos para solicitar que los dispositivos especificados inicien la instalación de firmware mediante el tema `iotdm-1/mgmt/initiate/firmware/update`.
Si esta operación se puede iniciar inmediatamente, establezca el parámetro `rc` en `202`.
Si el firmware no se ha descargado antes de forma correcta, establezca el parámetro `rc` en `400`.

El código siguiente muestra un ejemplo:

```
Solicitud entrante de la {{site.data.keyword.iot_short_notm}}:

Tema: iotdm-1/mgmt/initiate/firmware/update
Mensaje:
{
   "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
}

Respuesta saliente del dispositivo:

Tema: iotdevice-1/response
Mensaje:
{
   "rc" : 202,
   "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
}
```

Para finalizar la solicitud de actualización de firmware, el dispositivo informa de su estado de actualización a la {{site.data.keyword.iot_short_notm}} utilizando un mensaje de estado publicado en su tema `iotdevice-1/notify`.
Cuando haya finalizado una actualización de firmware, el atributo `mgmt.firmware.updateStatus` se establece en `0` (Satisfactorio), el atributo `mgmt.firmware.state` se establece en `0` (Desocupado). La imagen de firmware descargada se puede suprimir del dispositivo, y el atributo `deviceInfo.fwVersion` se establece en el valor del atributo `mgmt.firmware.version`.

El código siguiente proporciona un ejemplo de un mensaje de notificación:

```
Mensaje saliente del dispositivo:

Tema: iotdevice-1/notify
Mensaje:
{
   "d" : {
      "fields": [
         {
            "field" : "mgmt.firmware",
            "value" : {
               "state" : 0,
               "updateStatus" : 0
            }
         }
      ]
   }
}
```

Cuando el {{site.data.keyword.iot_short_notm}} recibe notificación de una actualización de firmware completada, ésta desencadena una última solicitud en el tema `iotdm-1/cancel` para cancelar la observación del atributo `mgmt.firmware`.


Cuando se envíe una respuesta que tenga el parámetro `rc` establecido en `200`, se completa la solicitud de actualización de firmware, como se muestra en el ejemplo siguiente:

```
Solicitud entrante de la {{site.data.keyword.iot_short_notm}}:

Tema: iotdm-1/cancel
Mensaje:
{
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f",
   "d" : {
      "fields" : [
         {
            "field" : "mgmt.firmware"
         }
      ]
   }
}


Mensaje saliente del dispositivo:

Tema: iotdevice-1/response
Mensaje:
{
   "rc" : 200,
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f"
}
```

La lista siguiente proporciona alguna información útil para el manejo de errores y de procesos:

- Si falla el intento de actualización de firmware, establezca el parámetro `rc` en `500` y, opcionalmente, establezca el parámetro `message` para que contenga información relevante.
- Si la actualización de firmware no está soportada, establezca el parámetro `rc` en `501` y, opcionalmente, establezca el parámetro `message` para que contenga información relevante.
- Si el atributo `mgmt.firmware.state` no es `2` (Descargado), envíe un error que tenga el parámetro `rc` establecido en `400` y un texto de mensaje opcional.
- De lo contrario, establezca el atributo `mgmt.firmware.updateStatus` en `1` (En curso), y la instalación de firmware normalmente se inicia.
- Si falla la instalación de firmware, establezca el atributo `mgmt.firmware.updateStatus` en uno de los valores siguientes:
  - `2` (Sin memoria)
  - `5` (Imagen no soportada)


**Importante:** Todos los parámetros que se listan como parte del atributo `mgmt.firmware` deben establecerse al mismo tiempo, de modo que si hay una observación actual para `mgmt.firmware`, sólo se enviará un único mensaje de notificación.

## Recetas sobre las acciones de dispositivo y acciones de firmware

En las siguientes recetas se muestra el flujo completo necesario para realizar acciones de dispositivo y de firmware.

- [Gestión de dispositivos en WIoT Platform – Retrotracción y restablecimiento de valores de fábrica ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-roll-back-factory-reset/){: new_window}

- [Actualización de firmware iniciada por el dispositivo ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-device-initiated-firmware-upgrade/){: new_window}

- [Actualización de firmware iniciada por la plataforma ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-platform-initiated-firmware-upgrade/){: new_window}

- [Actualización de firmware iniciada por la plataforma con ejecución de fondo ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-platform-initiated-firmware-upgrade/){: new_window}

- [Retrotracción y restablecimiento de valores de fábrica de firmware ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-roll-back-factory-reset/){: new_window}
