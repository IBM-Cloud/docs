---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-14"
---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# API REST HTTP para dispositivos
{: #api}

**Importante:** La API REST HTTP de {{site.data.keyword.iot_full}} para la característica de dispositivos sólo está disponible como parte de un programa beta limitado. Las actualizaciones futuras pueden incluir cambios que no son compatibles con la versión actual de esta característica. Pruébela y [denos su opinión ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/answers/smart-spaces/17/internet-of-things.html){: new_window}.

## Acceso a la documentación de la API REST HTTP
{: #api_link}

Para acceder a la documentación de la API REST HTTP de {{site.data.keyword.iot_short_notm}} y obtener más información sobre cómo integrar dispositivos en su organización, consulte [API](../reference/api.html).

La única versión de la API REST HTTP de {{site.data.keyword.iot_short_notm}} soportada es la versión 2. Asegúrese de que las soluciones de {{site.data.keyword.iot_short_notm}} utilicen la versión 2.

## Conexiones de clientes
{: #client_connections}

Para obtener información sobre la seguridad del cliente y cómo conectar clientes a dispositivos en {{site.data.keyword.iot_short_notm}}, consulte [Conexión de aplicaciones, dispositivos y pasarelas a {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html).

# API de mensajería de REST HTTP para dispositivos
{: #rest_messaging_api}

Para acceder a la documentación de API de mensajería HTTP de {{site.data.keyword.iot_short_notm}} y obtener más información sobre cómo publicar sucesos utilizando HTTP, consulte [API de mensajería HTTP de {{site.data.keyword.iot_short_notm}} ![Icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/http-messaging.html){: new_window}.

## Publicación de sucesos
{: #event_publication}

Además de utilizar el protocolo de mensajería MQTT, también puede configurar los dispositivos para publicar sucesos en el {{site.data.keyword.iot_short_notm}} a través de HTTP utilizando mandatos de la API REST HTTP.

Utilice uno de los URL siguientes para enviar una solicitud `POST` desde un dispositivo conectado a {{site.data.keyword.iot_short_notm}}:

### Solicitud POST no segura
<pre class="pre"><code class="hljs">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

### Solicitud POST segura

<pre class="pre"><code class="hljs">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

**Nota: **el puerto 443, el puerto SSL predeterminado, también se puede especificar para llamadas de API HTTP seguras.

Si está conectando un dispositivo o una aplicación al servicio de Quickstart, utilice uno de los siguientes URL en su lugar:

### Solicitud POST no segura para Quickstart
<pre class="pre"><code class="hljs">http://quickstart.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

### Solicitud POST segura para Quickstart
<pre class="pre"><code class="hljs">https://quickstart.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

**Notas importantes:**
- En la versión de la API REST HTTP actual, sólo puede enviar sucesos de dispositivo mediante la mensajería HTTP. Utilice el protocolo de mensajería MQTT para enviar solicitudes para otras características de gestión de dispositivos y de control.
- Las conexiones HTTP se pueden utilizar para publicar sucesos para el mismo dispositivo sólo cuando no se puede cambiar la cabecera HTTP de autorización.
- El puerto 443, el puerto SSL predeterminado, también se puede especificar para llamadas de API HTTP seguras.

### Autenticación

Todas las solicitudes deben incluir una cabecera de autorización. La autenticación básica es el único método que se admite. Cuando un dispositivo realiza una solicitud HTTP a través de la API REST HTTP de {{site.data.keyword.iot_short_notm}}, serán necesarias las siguientes credenciales:

|Credencial|Entrada necesaria|
|:---|:---|
|Nombre de usuario|`use-token-auth`
|Contraseña| La señal de autenticación que se ha generado automáticamente o que se ha especificado manualmente al registrar el dispositivo.


### Cabeceras de solicitud Content-Type

Debe proporcionarse una cabecera de solicitud `Content-Type` con la solicitud. En la tabla siguiente se muestra cómo se correlacionan los tipos soportados con los formatos internos de {{site.data.keyword.iot_short_notm}}.

|Cabecera Content-Type|Formato en {{site.data.keyword.iot_short_notm}}|
|:---|:---|
|text/plain|"text"
|application/json| "json"
|application/xml | "xml"
|application/octet-stream|"bin"

### Calidad de servicio

De forma parecida a la calidad de servicio MQTT "at most once" del servicio de entrega de nivel 0, la mensajería REST HTTP proporciona entrega de mensajes no persistentes pero valida que la solicitud sea correcta y que se pueda entregar al servidor antes de que envíe la respuesta HTTP. Una respuesta que contiene un código de estado HTTP de 200 confirma que el mensaje se ha entregado al servidor. Al utilizar la calidad MQTT "at most once" del nivel de servicio o el equivalente HTTP para entregar mensajes de sucesos, el dispositivo o la aplicación debe implementar la lógica de reintento para garantizar la entrega.

Para obtener más información sobre el protocolo MQTT y la calidad de los niveles de servicio para {{site.data.keyword.iot_short_notm}}, consulte [Mensajería MQTT](../reference/mqtt/index.html).

## Memoria caché del último suceso
{: #last-event-cache}

Al utilizar la {{site.data.keyword.iot_short_notm}} Last Event Cache API, puede recuperar el último suceso que ha enviado un dispositivo. Esto funciona si el dispositivo está en línea o fuera de línea, lo que le permite recuperar el estado del dispositivo independientemente de la ubicación física del dispositivo o el estado de uso. Puede recuperar el último valor grabado de un ID de suceso para un dispositivo específico, o el último valor grabado para cada ID de suceso del que ha informado un dispositivo específico. Los últimos datos de sucesos de un dispositivo se pueden recuperar para cualquier suceso específico que se ha producido hasta hace un máximo de 365 días.

Para solicitar el valor más reciente para un ID de suceso específico, utilice la siguiente solicitud de API, que devuelve el último valor grabado para el ID de suceso “power”.

```
GET /api/v0002/device/types/<device-type>/devices/<device-id>/events/power
```

La respuesta se devuelve en el siguiente formato JSON:

```
{
    "deviceId": "<device-id>",
    "eventId": "power",
    "format": "json",
    "payload": "eyJzdGF0ZSI6Im9uIn0=",
    "timestamp": "2016-03-14T14:12:06.527+0000",
    "typeId": "<device-type>"
}
```

**Nota:** Mientras la respuesta de la API está en formato JSON, las cargas útiles de sucesos se pueden grabar en cualquier formato. Las cargas útiles devueltas por la API de memoria caché de último suceso están codificadas en base64.

Para solicitar el valor más reciente para cada ID de suceso del que ha informado un dispositivo, utilice la siguiente solicitud API:

```
GET /api/v0002/device/types/<device-type>/devices/<device-id>/events
```

La respuesta incluirá todos los ID de suceso enviados por el dispositivo. En el ejemplo siguiente, se devuelven valores para los sucesos “power” y “temperature”.

```
[
    {
        "deviceId": "<device-id>",
        "eventId": "power",
        "format": "json",
        "payload": "eyJzdGF0ZSI6Im9uIn0=",
        "timestamp": "2016-03-14T14:12:06.527+0000",
        "typeId": "<device-type>"
    },
    {
        "deviceId": "<device-id>",
        "eventId": "temperature",
        "format": "json",
        "payload": "eyJpbnRlcm5hbCI6MjIsICJleHRlcm5hbCI6MTZ9",
        "timestamp": "2016-03-14T14:17:44.891+0000",
        "typeId": "<device-type>"
    }
]
```
