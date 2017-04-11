---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Conectividad de MQTT para pasarelas
{: #mqtt}

MQTT es el protocolo primario que utilizan los dispositivos y las aplicaciones para comunicarse con el {{site.data.keyword.iot_full}}. Las bibliotecas de cliente, la información y los ejemplos se proporcionan para ayudarle a utilizar clientes de MQTT como pasarelas para conectar dispositivos a {{site.data.keyword.iot_short_notm}}.
{:shortdesc}

## Conexiones de clientes
{: #client_connections}

Para obtener información sobre la seguridad del cliente y cómo conectar clientes de MQTT como pasarelas, consulte [Conexión de aplicaciones, dispositivos y pasarelas a {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html).

## Autenticación de MQTT
{: #authentication}
Para pasarelas y dispositivos, {{site.data.keyword.iot_short_notm}} utiliza la autenticación basada en tokens de MQTT.

Para habilitar la autenticación MQTT, envíe un nombre de usuario y una contraseña al realizar una conexión MQTT.

### Nombre de usuario
{: #username}

El nombre de usuario es el mismo valor para todas las pasarelas: `use-token-auth`. Este valor hace que {{site.data.keyword.iot_short_notm}} utilice la señal de autenticación de la pasarela, que se especifica como la contraseña.

### Contraseña
{: #password}

La contraseña para cada pasarela es la única señal de autenticación que se ha generado cuando la pasarela se ha registrado con {{site.data.keyword.iot_short_notm}}.

## Publicación de sucesos
{: #pub_events}

Una pasarela puede publicar sucesos de sí misma y en nombre de cualquier dispositivo que esté conectado a través de la pasarela. Para publicar sucesos, utilice el tema siguiente y sustituya el `typeId` y `deviceId` correspondientes en función del origen pretendido del suceso:

<pre class="pre">iot-2/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/evt/<var class="keyword varname">eventId</var>/fmt/<var class="keyword varname">formatString</var></pre>
{: codeblock}


**Ejemplo**


|    |'typeID'|'deviceID'|
|:---|:---|:---|
|Pasarela 1 |mi_pasarela |pasarela1 |
|Dispositivo 1 |mi_dispositivo |dispositivo1 |

-   La Pasarela 1 puede publicar sus propios sucesos de estado:
      
    `iot-2/type/mygateway/id/gateway1/evt/status/fmt/json`
-   La Pasarela 1 puede publicar sucesos de estado en nombre del Dispositivo 1:
      
    `iot-2/type/mydevice/id/device1/evt/status/fmt/json`

**Importante:** La carga útil de mensajes está limitada a un máximo de 131072 bytes. Los mensajes mayores de este límite se rechazarán.

### Mensajes retenidos
Las organizaciones de {{site.data.keyword.iot_short_notm}} no tienen autorización para publicar mensajes MQTT retenidos. Si una pasarela envía un mensaje retenido, el servicio {{site.data.keyword.iot_short_notm}} modifica el distintivo del mensaje retenido cuando tiene el valor true y procesa el mensaje como si el distintivo estuviera establecido en false.

## Suscripción a mandatos
{: #subscribing_cmds}

Una pasarela puede suscribirse a los mandatos que se direccionan a la propia pasarela y a cualquier dispositivo de la organización, incluidas otras pasarelas. Para suscribirse a los mandatos, utilice el tema siguiente y sustituya los `typeId` y `deviceId` apropiados:

<pre class="pre">iot-2/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/cmd/<var class="keyword varname">commandId</var>/fmt/<var class="keyword varname">formatString</var></pre>
{: codeblock}

El comodín `+` de MQTT puede utilizarse para `typeId`, `deviceId`, `commandId` y `formatString` para suscribirse a varios orígenes de mandatos.

**Ejemplo:**

|Dispositivo |`typeId`|`deviceId`|
|:---|:---|
|Pasarela 1| mi_pasarela   | pasarela1   |
|Dispositivo 1 | mi_dispositivo    | dispositivo1    |


-   La Pasarela 1 puede suscribirse a los mandatos dirigidos a la pasarela:
      
    `iot-2/type/mygateway/id/gateway1/cmd/+/fmt/+`
-   La Pasarela 1 puede suscribirse a mandatos que se envían a Dispositivo 1:
      
    `iot-2/type/mydevice/id/device1/cmd/+/fmt/+`
-   La Pasarela 1 puede suscribirse a cualquier mandato que se envía a los dispositivos de tipo `mydevice`:
       
     `iot-2/type/mydevice/id/+/cmd/+/fmt/+`

**Importante:** Las sesiones persistentes de MQTT que se especifican como `cleansession=false` no buscan dispositivos que se conectan a pasarelas. Si un dispositivo se conecta a la pasarela A y, más adelante, se conecta a la pasarela B, no recibe ningún mensaje que se haya publicado en la pasarela A para dicho dispositivo mientras ha estado desconectado. Una pasarela es propietaria del cliente y la suscripción de MQTT, pero no los dispositivos que estén conectados a la pasarela.

## Registro automático de pasarelas
{: #auto-reg}

Los dispositivos de pasarela pueden registrar automáticamente dispositivos que estén conectados a ellas. Cuando una pasarela publica un mensaje o se suscribe a un tema en nombre de un dispositivo no registrado, dicho dispositivo se registra automáticamente.

Las solicitudes de registro de los dispositivos de pasarela están limitadas a 128 solicitudes pendientes a la vez. Intentar conectar muchos dispositivos nuevos puede causar un retraso en el registro de los dispositivos a través de la pasarela.

**Aviso**

Si la pasarela no puede registrar un dispositivo automáticamente, no intentará registrar dicho dispositivo de nuevo durante un período corto de tiempo. Los mensajes o suscripciones del dispositivo fallido se descartarán durante ese momento.

## Notificaciones de pasarelas
{: #notification}

Cuando se producen errores durante la validación del tema de publicación o suscripción o durante el registro automático, se enviará una notificación al dispositivo de pasarela. Una pasarela puede recibir estas notificaciones si se suscribe al tema siguiente, sustituyendo los valores `typeId` y `deviceId`:

```
iot-2/type/**typeId**/id/**deviceId**/notify
```
<pre class="pre">iot-2/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/notify</pre>
{: codeblock}

Los mensajes que se han recibido en el tema de notificación utilizan el formato siguiente:

```   
{
   "Request": "<Request_Type>",
   "Time": "<Timestamp>",
   "Topic": "<Topic>",
   "Type": "<Device_Type>",
   "Id": "<Device_Id>",
   "Client": "<Client_ID>",
   "RC": "<Return_Code>",
   "Message": "<Message>"
}
```
Donde
-   Los valores de `Request_Type` son `publish` o `subscribe`
-   `Timestamp` es la hora en formato ISO 8601
-   `Topic` es el tema de solicitud de la pasarela
-   `Device_Type` es el tipo de dispositivo del tema
-   `Device_Id` es el ID de dispositivo del tema
-   `Client_ID` es el ID de cliente de la solicitud
-   `Return_Code` es el código de retorno
-   `Message` es el mensaje de error

Una pasarela puede recibir las siguientes notificaciones:

-   El tema no coincide con ninguna de las reglas de tema permitidas.
-   El tipo de dispositivo no es válido.
-   El ID de dispositivo no es válido.
-   Se ha alcanzado el número máximo de dispositivos por pasarela.
-   Se ha alcanzado el número máximo de dispositivos por organización.
-   No se ha podido crear el dispositivo debido a errores internos.

## Pasarelas gestionadas
{: #managed_gateways}

El soporte para la gestión del ciclo de vida de dispositivos es opcional. El protocolo de gestión de dispositivos que utiliza {{site.data.keyword.iot_short_notm}} utiliza la misma conexión de MQTT que utiliza la pasarela para los sucesos y el control de mandatos.

### Niveles de calidad de servicio y sesión limpia
{: #quality_service}

Las pasarelas gestionadas pueden publicar mensajes que tienen un nivel de calidad de servicio (QoS) de 0 o 1.

Los mensajes con QoS=0 pueden descartarse y no persisten una vez que se reinicia el servidor de mensajería. Los mensajes con QoS=1 se pueden poner en cola y persisten una vez que se reinicia el servidor de mensajería. La duración de la suscripción determina si se pone en cola una solicitud. El parámetro `cleansession` de la conexión que ha realizado la suscripción determina la duración de la suscripción.  

{{site.data.keyword.iot_short_notm}} publica solicitudes que tienen un nivel de QoS de 1 para dar soporte a la puesta en cola de mensajes. Para poner en cola mensajes que se envían mientras una pasarela gestionada no está conectada, configure el dispositivo para no utilizar sesiones limpias estableciendo el parámetro `cleansession` en false.

**Aviso**

Cuando una pasarela gestionada utiliza una suscripción duradera, se informa de los mandatos de gestión de dispositivos que se envían a la pasarela mientras está fuera de línea como operaciones fallidas si la pasarela no se vuelve a conectar al servicio antes de que la solicitud exceda el tiempo de espera. Cuando la pasarela vuelva a conectarse, las solicitudes las procesará la pasarela. Las suscripciones duraderas las especifica el parámetro `cleansession=false`.

La pasarela es propietaria de la sesión de MQTT, independientemente de los dispositivos que están detrás de ella. Cuando un dispositivo envía una solicitud de suscripción a través de una pasarela, la solicitud no itinera a otras pasarelas, independientemente de si las opciones `cleansession=false` se han establecido.

### Temas
{: #topics}

Una pasarela gestionada debe suscribirse a los temas siguientes para manejar las solicitudes y las respuestas de {{site.data.keyword.iot_short_notm}}:

-   La pasarela gestionada se suscribe a las respuestas de gestión de dispositivos en:  
<pre class="pre">iotdm-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/response/+</pre>
{: codeblock}
-   La pasarela gestionada se suscribe a las solicitudes de gestión de dispositivos en:  
<pre class="pre">iotdm-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/+</pre>
{: codeblock}

Una pasarela gestionada publica las respuestas y solicitudes siguientes:

- Las respuestas de gestión de dispositivos se publican en:  
<pre class="pre">iotdevice-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/response/</pre>
{: codeblock}
- Las solicitudes de gestión de dispositivos se publican en:  
<pre class="pre">iotdevice-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/</pre>
{: codeblock}

La pasarela puede procesar mensajes de Protocolo de gestión de dispositivos para sí misma y en nombre de otros dispositivos conectados utilizando los **typeId** y **deviceId** relevantes.

### Formato de mensajes
{: #msg_format}

Todos los mensajes se envían en formato JSON.

**Solicitudes**

Las solicitudes se formatean tal como se muestra en el ejemplo de código siguiente:

```   
    {  "d": {...}, "reqId": "b53eb43e-401c-453c-b8f5-94b73290c056" }
```

-   `d` lleva todos los datos que son relevantes para la solicitud
-   `reqId` es un identificador de la solicitud y se debe copiar en una respuesta. Si no es necesaria una respuesta, el campo no se utilizará.

**Respuestas**

Las respuestas se formatean tal como se muestra en el ejemplo de código siguiente:

```
    {
        "rc": 0,
        "message": "success",
        "d": {...},
        "reqId": "b53eb43e-401c-453c-b8f5-94b73290c056"
    }
```
Donde:
-   `rc` es un código de resultado de la solicitud original.
-   `message` es un elemento opcional con una descripción de texto del código de respuesta.
-   `d` es un elemento de datos opcional que acompaña a la respuesta.
-   `reqId` es el ID de solicitud de la solicitud original. El ID de solicitud se utiliza para correlacionar respuestas con solicitudes, y el dispositivo necesita asegurarse de que todos los ID de solicitud sean exclusivos. Las respuestas a las solicitudes de {{site.data.keyword.iot_short_notm}} deben contener el valor `reqId` correcto.
