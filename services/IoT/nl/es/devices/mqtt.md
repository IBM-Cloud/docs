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


# Conectividad de MQTT para dispositivos
{: #mqtt}

MQTT es el protocolo primario que utilizan los dispositivos y las aplicaciones para comunicarse con el {{site.data.keyword.iot_full}}. Las bibliotecas de cliente, la información y los ejemplos se proporcionan para ayudarle a conectar e integrar los dispositivos con {{site.data.keyword.iot_short_notm}}.
{:shortdesc}

## Conexiones de clientes
{: #client_connections}

Para obtener información sobre la seguridad del cliente y cómo conectar los clientes de MQTT a dispositivos en {{site.data.keyword.iot_short_notm}}, consulte [Conexión de aplicaciones, dispositivos y pasarelas a {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html).


## Conexión de dispositivos al servicio de Inicio rápido
{: #connecting_devices}

El servicio de Inicio rápido es el nivel más rápido de servicio. No ofrece confirmación de recepción y no da soporte a los niveles de calidad de servicio (QoS) de MQTT mayores que cero. Cuando se conecta al servicio de Inicio rápido, no se necesita la autenticación ni el registro, y el `orgId` se debe establecer en `quickstart`.

Si está grabando código de dispositivos para su uso con el Inicio rápido, tenga en cuenta que las siguientes características de servicio de {{site.data.keyword.iot_short_notm}} no están soportadas en la modalidad de Inicio rápido:

-  Suscripción a mandatos
-  Protocolo de gestión de dispositivo
-  Sesiones limpias o duraderas

**Importante:** Los mensajes que se envían desde dispositivos a una velocidad mayor que uno por segundo pueden ser descartados.


## Autenticación de MQTT
{: #mqtt_authentication}

Para pasarelas y dispositivos, {{site.data.keyword.iot_short_notm}} utiliza la autenticación basada en tokens de MQTT.

Para habilitar la autenticación MQTT, envíe un nombre de usuario y una contraseña al realizar una conexión MQTT.

### Nombre de usuario

El nombre de usuario es el mismo valor para todos los dispositivos: `use-token-auth`. Este valor hace que {{site.data.keyword.iot_short_notm}} utilice la señal de autenticación del dispositivo, que se especifica como la contraseña.

### Contraseña

La contraseña para cada dispositivo es la señal de autenticación única que se ha generado cuando el dispositivo se ha registrado con {{site.data.keyword.iot_short_notm}}.

## Publicación de sucesos
{: #publishing_events}

Los dispositivos publican en los temas de sucesos en el formato siguiente:

<pre class="pre">iot-2/evt/<var class="keyword varname">event_id</var>/fmt/<var class="keyword varname">format_string</var></pre>
{: codeblock}

Donde

-  **event_id** es el ID del suceso, por ejemplo `status`.  El ID de suceso puede ser cualquier serie válida en MQTT. Si no se utilizan comodines, las aplicaciones del suscriptor deben utilizar esta serie en su tema de suscripción para recibir los sucesos publicados en su tema.
-  **format_string** es una serie que define el tipo de contenido de la carga útil del mensaje para que el receptor del mensaje pueda determinar la forma de analizar el contenido. Los valores de tipo de contenido comunes incluyen, pero no se limitan a, "json", "xml", "txt" y "csv". El valor puede ser cualquier serie válida en MQTT.

**Importante:** La carga útil de mensajes está limitada a un máximo de 131072 bytes. Los mensajes mayores de este límite se rechazarán.

### Mensajes retenidos
Las organizaciones de {{site.data.keyword.iot_short_notm}} no tienen autorización para publicar mensajes MQTT retenidos. Si un dispositivo envía un mensaje retenido, el servicio {{site.data.keyword.iot_short_notm}} modifica el distintivo del mensaje retenido cuando tiene el valor true y procesa el mensaje como si el distintivo estuviera establecido en false.


## Suscripción a mandatos
{: #subscribing_to_commands}

Los dispositivos pueden suscribirse a temas de mandatos en el formato siguiente:

<pre class="pre">iot-2/cmd/<var class="keyword varname">command_id</var>/fmt/<var class="keyword varname">format_string</var></pre>
{: codeblock}

Donde
 - **command_id** es el ID del mandato, por ejemplo, `update`. El ID de mandato puede ser cualquier serie válida en el protocolo MQTT.  Si no se utilizan comodines, un dispositivo debe utilizar esta serie en su tema de suscripción para que reciba mandatos publicados en su tema.
 - **format_string** es una serie que define el tipo de contenido de la carga útil del mandato de modo que el receptor del mandato pueda determinar la forma de analizar el contenido. Los valores de tipo de contenido comunes incluyen, pero no se limitan a, "json", "xml", "txt" y "csv". El valor puede ser cualquier serie válida en MQTT.

Los dispositivos no pueden suscribirse a sucesos de otros dispositivos. Un dispositivo recibe mandatos publicados únicamente en su propio dispositivo.

## Dispositivos gestionados
{: #managed-devices}

El soporte para la gestión del ciclo de vida de dispositivos es opcional. El Protocolo de gestión de dispositivos utiliza la misma conexión MQTT que ya utiliza el dispositivo para el control de sucesos y de mandatos.

### Niveles de calidad de servicio y sesión limpia

Los dispositivos gestionados pueden publicar mensajes que tienen un nivel de calidad de servicio (QoS) de 0 o 1.

Los mensajes con QoS=0 pueden descartarse y no persisten una vez que se reinicia el servidor de mensajería. Los mensajes con QoS=1 se pueden poner en cola y persisten una vez que se reinicia el servidor de mensajería. La duración de la suscripción determina si se pone en cola una solicitud. El parámetro `cleansession` de la conexión que ha realizado la suscripción determina la duración de la suscripción.  

{{site.data.keyword.iot_short_notm}} publica solicitudes que tienen un nivel de QoS de 1 para dar soporte a la puesta en cola de mensajes. Para poner en cola mensajes que se envían mientras que un dispositivo gestionado no está conectado, configure el dispositivo para que no utilice sesiones limpias estableciendo el parámetro `cleansession` en false.

**Aviso:**
  Si el dispositivo gestionado utiliza una suscripción duradera, los mandatos que se envíen a su dispositivo mientras esté fuera de línea se notifican como operaciones anómalas si el dispositivo no vuelve a conectarse al servicio antes de que se exceda el tiempo de espera de la solicitud. Sin embargo, cuando el dispositivo vuelve a conectarse, el dispositivo procesa dichas solicitudes. Se especifica una suscripción duradera mediante el parámetro `cleansession=false`.

### Temas

Es necesario un dispositivo gestionado para suscribirse al tema siguiente para manejar las solicitudes y las respuestas del servicio {{site.data.keyword.iot_short_notm}}:

```
iotdm-1/#
```


Un dispositivo gestionado publica en los temas específicos del tipo de solicitud de gestión que se esté llevando a cabo:

- El dispositivo gestionado publica respuestas de gestión de dispositivos en `iotdevice-1/response`.
- Para otros temas en los que puede publicar un dispositivo gestionado, consulte [Protocolo de gestión de dispositivos](device_mgmt/index.html) y [Solicitudes de gestión de dispositivos](device_mgmt/requests.html).



### Formato de mensajes

Todos los mensajes se envían en formato JSON.

**Solicitudes**  
Las solicitudes se formatean tal como se muestra en el ejemplo de código siguiente:

<pre class="pre">{  "d": {...}, "<var class="keyword varname">reqId</var>": "b53eb43e-401c-453c-b8f5-94b73290c056" }</pre>
{: codeblock}

Donde:

 - **d** lleva todos los datos relevantes para la solicitud.
 - **reqId** es un identificador de la solicitud y se debe copiar en una respuesta. Si no es necesaria una respuesta, puede omitir el campo *reqId*.

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
 - **rc** es un código de resultado de la solicitud original.
 - **message** es un elemento opcional con una descripción de texto del código de respuesta.
 - **d** es un elemento de datos opcional que acompaña a la respuesta.
 - **reqId** es el ID de solicitud de la solicitud original, que se utiliza para correlacionar las respuestas con solicitudes. El dispositivo debe asegurarse de que todos los ID de solicitud sean exclusivos. Las respuestas a solicitudes {{site.data.keyword.iot_short_notm}} deben incluir el valor **reqId** correcto.

Para obtener más información sobre los mensajes de solicitud y de respuesta específicos, consulte [Protocolo de gestión de dispositivos](device_mgmt/index.html) y [Solicitudes de gestión de dispositivos](device_mgmt/requests.html).
