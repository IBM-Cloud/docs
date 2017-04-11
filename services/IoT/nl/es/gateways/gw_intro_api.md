---

copyright:
 years: 2015, 2017
lastupdated: "2017-03-16"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}

{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# API de mensajería HTTP para dispositivos de pasarela (Beta)
{: #api}

**Importante:** La API HTTP de {{site.data.keyword.iot_full}} para la característica de dispositivo de pasarela solo está disponible como parte de un programa beta limitado. Las actualizaciones futuras pueden incluir cambios que no son compatibles con la versión actual de esta característica. Pruébela y [denos su opinión ![Icono de enlace externo](../../../icons/launch-glyph.svg)](https://developer.ibm.com/answers/smart-spaces/17/internet-of-things.html){: new_window}.

## Acceso a la documentación de la API de mensajería HTTP para dispositivos de pasarela
{: #rest_messaging_api}

Para acceder a la documentación de la API de mensajería HTTP de {{site.data.keyword.iot_short_notm}} y obtener más información sobre cómo enviar sucesos desde dispositivos de pasarela, consulte [API de mensajería HTTP de {{site.data.keyword.iot_short_notm}} ![Icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/http-messaging.html){: new_window}.


## Conexiones de clientes
{: #client_connections}

Para obtener información sobre la seguridad del cliente y cómo conectar clientes a dispositivos de pasarela en {{site.data.keyword.iot_short_notm}}, consulte [Conexión de aplicaciones, dispositivos y pasarelas a {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html).


## Publicación de sucesos
{: #event_publication}

Además de utilizar el protocolo de mensajería MQTT, también puede configurar los dispositivos de pasarela para publicar sucesos en el {{site.data.keyword.iot_short_notm}} a través de HTTP utilizando los mandatos de la API de mensajería HTTP.

Para enviar una solicitud `POST` desde un dispositivo conectado a {{site.data.keyword.iot_short_notm}}, utilice uno de los URL siguientes:

### Solicitud POST no segura
<pre class="pre"><code class="hljs">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

### Solicitud POST segura
<pre class="pre"><code class="hljs">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

**Notas importantes:**
- Solo puede enviar sucesos de dispositivo de pasarela mediante la mensajería HTTP. Utilice el protocolo de mensajería MQTT para enviar solicitudes para otras características de gestión de dispositivos de pasarela y de control.
- Las conexiones HTTP solo se pueden reutilizar para publicar sucesos para el mismo dispositivo porque la cabecera HTTP de autorización no se puede cambiar.
- El puerto 443, el puerto SSL predeterminado, también se puede especificar para llamadas de API HTTP seguras.
- Si a una pasarela no se le ha asignado el rol *Pasarela estándar*, puede publicar sucesos en nombre de cualquiera de los dispositivos de la organización. Asigne el rol *Pasarela estándar* si quiere comprobar los niveles de autorización del dispositivo y registrar automáticamente su dispositivo. **Nota:** este comportamiento está sujeto a cambios.

Para obtener más información sobre el rol de las pasarelas y los grupos de recursos, consulte [Control de acceso de pasarela (Beta)](../gateways/gateway-access-control.html).

### Autenticación

Todas las solicitudes deben incluir una cabecera de autorización. La autenticación básica es el único método que se admite. Cuando un dispositivo realiza una solicitud HTTP a través de la API REST HTTP de {{site.data.keyword.iot_short_notm}}, serán necesarias las siguientes credenciales:

|Credencial|Entrada necesaria|
|:---|:---|
|Nombre de usuario| `g/{orgId}/{gwType}/{gwDevId}` o `g-{orgId}-{gwType}-{gwDevId}`
|Contraseña| La señal de autenticación que se ha generado automáticamente o que se ha especificado manualmente al registrar el dispositivo de pasarela.


Donde:

<dl>
<dt>orgId</dt>  
<dd>El nombre de organización, que debe coincidir con el nombre que el especificado en la cabecera de host.</dd>

<p></p>
<dt>gwType</dt>  
<dd>El tipo de pasarela.</dd>
<dd>Si utiliza un guión "-" como delimitador en el nombre de usuario, este valor no debe incluir un guión.</dd>
<p></p>
<dt>gwDevId</dt>  
<dd>El identificador de dispositivo de la pasarela.</dd>
</dl>


### Cabeceras de solicitud Content-Type

Debe proporcionarse una cabecera de solicitud `Content-Type` con la solicitud. En la tabla siguiente se muestra cómo se correlacionan los tipos soportados con los formatos internos de {{site.data.keyword.iot_short_notm}}:

|Cabecera Content-Type|Formato en {{site.data.keyword.iot_short_notm}}|
|:---|:---|
|text/plain|"text"
|application/json| "json"
|application/xml | "xml"
|application/octet-stream|"bin"

### Calidad de servicio

De forma parecida a la calidad de servicio MQTT "at most once" del servicio de entrega de nivel 0, la mensajería REST HTTP proporciona entrega de mensajes no persistentes pero valida que la solicitud sea correcta y que se pueda entregar al servidor antes de que envíe la respuesta HTTP. Una respuesta que contiene un código de estado HTTP de 200 confirma que el mensaje se ha entregado al servidor. Al utilizar la calidad MQTT "at most once" del nivel de servicio o el equivalente HTTP para entregar mensajes de sucesos, el dispositivo o la aplicación debe implementar la lógica de reintento para garantizar la entrega.

Para obtener más información sobre el protocolo MQTT y la calidad de los niveles de servicio para {{site.data.keyword.iot_short_notm}}, consulte [Mensajería MQTT](../reference/mqtt/index.html).

Para obtener más información sobre la gestión de dispositivos de pasarela mediante interfaces de programación de aplicaciones, consulte [API REST HTTP para dispositivos de pasarela](../gateways/gw_api.html).
