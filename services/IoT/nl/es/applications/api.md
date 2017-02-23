---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-12-01"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# API REST HTTP para aplicaciones
{: #api}

Utilice la API REST HTTP de {{site.data.keyword.iot_full}} para crear y personalizar aplicaciones que interactúan con su organización en {{site.data.keyword.iot_short_notm}}.
{:shortdesc}

## Capacidades
{: #capabilities}

La API REST HTTP de {{site.data.keyword.iot_short_notm}} da soporte a las siguientes funciones para aplicaciones:

- Recuperación de información de la organización
- Operaciones de dispositivo masivas (listar, añadir y eliminar)
- Operaciones de tipo de dispositivo (listar, crear, suprimir, ver detalles y actualizar)
- Operaciones de dispositivo (listar, añadir, eliminar, ver detalles, actualizar, ver ubicación y ver información de gestión)
- Operaciones de diagnóstico de dispositivo (borrar registros, recuperar registros, añadir información de registro, suprimir registros, obtener registros específicos, borrar los códigos de error, obtener códigos de error del dispositivo y añadir códigos de error)
- Determinación de problemas de conexión (sucesos de registro de conexión de dispositivos de la lista)
- Memoria caché del último suceso (ver el último suceso para un dispositivo específico)
- Operaciones de solicitud de gestión de dispositivos (listar solicitudes de gestión de dispositivos, iniciar solicitudes, borrar el estado de las solicitudes, obtener detalles de una solicitud, listar todos los estados de solicitud por dispositivo y obtener el estado de solicitud para un dispositivo específico)
- Operaciones de gestión de uso (recuperar la cantidad total de datos utilizados)
- Publicación de sucesos de dispositivos (beta)
- Consulta del estado del servicio (recuperar estados de servicio por organización)

## Acceso a la documentación de la API REST HTTP
{: #api_link}

Para acceder a la documentación de la API REST HTTP de {{site.data.keyword.iot_short_notm}} y obtener más información sobre cómo crear y personalizar las aplicaciones, vaya a https://docs.internetofthings.ibmcloud.com/swagger/v0002.html.

La única versión de la API REST HTTP de {{site.data.keyword.iot_short_notm}} soportada es la versión 2. Asegúrese de que las soluciones de {{site.data.keyword.iot_short_notm}} utilicen la versión 2.



# API de mensajería de REST HTTP para aplicaciones
{: #rest_messaging_api}

## Publicación de sucesos y mandatos
{: #event_command_publication}

Además de utilizar el protocolo de mensajería MQTT, también puede configurar las aplicaciones para publicar sucesos y mandatos en {{site.data.keyword.iot_short_notm}} a través de HTTP utilizando uno de los siguientes mandatos de API REST HTTP:

### Solicitud POST de sucesos no seguros
<pre class="pre">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

### Solicitud POST de sucesos seguros
<pre class="pre">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

**Nota:** el puerto 443, el puerto SSL predeterminado, también se puede especificar para llamadas de API HTTP seguras.

### Solicitud POST de mandatos no seguros
<pre class="pre">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/commands/<var class="keyword varname">eventId</var></pre>
{: codeblock}

### Solicitud POST de mandatos seguros
<pre class="pre">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/commands/<var class="keyword varname">eventId</var></pre>
{: codeblock}

Si está conectando un dispositivo o aplicación al servicio de Quickstart, sustituya **orgId** por la serie 'quickstart'.

**Notas:** 
- Mientras las aplicaciones puedan reutilizar una conexión HTTP para publicar sucesos o mandatos en distintos dispositivos, no se podrá cambiar la cabecera HTTP de autorización. 
- El puerto 443, el puerto SSL predeterminado, también se puede especificar para llamadas de API HTTP seguras.

### Autenticación

Todas las solicitudes deben incluir una cabecera de autorización. La autenticación básica es el único método que se admite. Las aplicaciones se autentican utilizando claves API. Cuando una aplicación hace una solicitud a través de la API REST HTTP de {{site.data.keyword.iot_short_notm}}, serán necesarias las siguientes credenciales:

```
nombre de usuario = clave API (por ejemplo, a-orgId-a84ps90Ajs)
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
