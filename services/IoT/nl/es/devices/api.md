---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# API REST HTTP para dispositivos
{: #api}
Última actualización: 09 de septiembre de 2016
{: .last-updated}

**Importante:** La API REST HTTP de {{site.data.keyword.iot_full}} para la característica de dispositivos sólo está disponible como parte de un programa beta limitado. Las actualizaciones futuras pueden incluir cambios que no son compatibles con la versión actual de esta característica. Pruébela y [denos su opinión](https://developer.ibm.com/answers/smart-spaces/17/internet-of-things.html).

## Acceso a la API REST HTTP
{: #api_link}

Para acceder a la API REST HTTP de {{site.data.keyword.iot_short_notm}} y obtener más información sobre cómo integrar dispositivos en su organización, vaya a https://docs.internetofthings.ibmcloud.com/swagger/v0002.html.

La única versión de la API REST HTTP de {{site.data.keyword.iot_short_notm}} soportada es la versión 2. Asegúrese de que las soluciones de {{site.data.keyword.iot_short_notm}} utilicen la versión 2.

# API de mensajería de REST HTTP para dispositivos
{: #rest_messaging_api}

## Publicación de sucesos
{: #event_publication}

Además de utilizar el protocolo de mensajería MQTT, también puede configurar los dispositivos para publicar sucesos en el {{site.data.keyword.iot_short_notm}} a través de HTTP utilizando mandatos de la API REST HTTP.

Utilice uno de los URL siguientes para enviar una solicitud `POST` desde un dispositivo conectado a {{site.data.keyword.iot_short_notm}}:

### Solicitud POST no segura
<pre class="pre">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

### Solicitud POST segura
<pre class="pre">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

Si está conectando un dispositivo o una aplicación al servicio de Quickstart, utilice uno de los siguientes URL en su lugar:

### Solicitud POST no segura para Quickstart
<pre class="pre">http://quickstart.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

### Solicitud POST segura para Quickstart
<pre class="pre">https://quickstart.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

**Notas importantes:**
- En la versión de la API REST HTTP actual, sólo puede enviar sucesos de dispositivo mediante la mensajería HTTP. Utilice el protocolo de mensajería MQTT para enviar solicitudes para otras características de gestión de dispositivos y de control.
- Las conexiones HTTP se pueden utilizar para publicar sucesos para el mismo dispositivo sólo cuando no se puede cambiar la cabecera HTTP de autorización.

### Autenticación

Todas las solicitudes deben incluir una cabecera de autorización. La autenticación básica es el único método que se admite. Cuando un dispositivo realiza una solicitud HTTP a través de la API REST HTTP de {{site.data.keyword.iot_short_notm}}, serán necesarias las siguientes credenciales:

```
nombre de usuario = "use-token-auth"
contraseña = Señal de autenticación
```

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
