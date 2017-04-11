---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-07"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}

{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# API REST HTTP para dispositivos de pasarela
{: #api_link}


Para acceder a la documentación de la API REST HTTP de {{site.data.keyword.iot_short_notm}} y obtener más información sobre cómo crear, actualizar, suprimir y listar dispositivos, consulte [API REST HTTP de {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html).

La única versión de la API REST HTTP de {{site.data.keyword.iot_short_notm}} soportada es la versión 2. Asegúrese de que las soluciones de {{site.data.keyword.iot_short_notm}} utilicen la versión 2.

## Conexiones de clientes
{: #client_connections}

Para obtener información sobre la seguridad del cliente y cómo conectar clientes a dispositivos de pasarela en {{site.data.keyword.iot_short_notm}}, consulte [Conexión de aplicaciones, dispositivos y pasarelas a {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html).


### Autenticación

Todas las solicitudes deben incluir una cabecera de autorización. La autenticación básica es el único método que se admite. Cuando un dispositivo realiza una solicitud HTTP a través de la API REST HTTP de {{site.data.keyword.iot_short_notm}}, serán necesarias las siguientes credenciales:

|Credencial|Entrada necesaria|
|:---|:---|
|Nombre de usuario| `g/{orgId}/{gwType}/{gwDevId}`
|Contraseña| La señal de autenticación que se ha generado automáticamente o que se ha especificado manualmente al registrar el dispositivo de pasarela.


donde:

**_orgId_**   
- Es el nombre de la organización, que debe coincidir con el nombre que se especifica en la cabecera de host.

**_gwType_**
- Es el tipo de pasarela.

**_gwDevId_**

- Es el identificador de dispositivo de la pasarela.

### Cabeceras de solicitud Content-Type

Debe proporcionarse una cabecera de solicitud `Content-Type` con la solicitud. En la tabla siguiente se muestra cómo se correlacionan los tipos soportados con los formatos internos de {{site.data.keyword.iot_short_notm}}:

|Cabecera Content-Type|Formato en {{site.data.keyword.iot_short_notm}}|
|:---|:---|
|text/plain|"text"
|application/json| "json"
|application/xml | "xml"
|application/octet-stream|"bin"

## Memoria caché del último suceso
{: #last-event-cache}

Al utilizar la {{site.data.keyword.iot_short_notm}} Last Event Cache API, puede recuperar el último suceso que ha enviado un dispositivo. Esta API funciona si el dispositivo está en línea o fuera de línea, lo que le permite recuperar el estado del dispositivo independientemente de la ubicación física del dispositivo o el estado de uso. Puede recuperar el último valor grabado de un ID de suceso para un dispositivo específico, o el último valor grabado para cada ID de suceso del que ha informado un dispositivo específico. Los últimos datos de sucesos de un dispositivo se pueden recuperar para cualquier suceso específico que se ha producido hasta hace un máximo de 365 días.

Para solicitar el valor más reciente para un ID de suceso específico, utilice la siguiente solicitud de API, que devuelve el último valor grabado para el ID de suceso “power”:

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

La respuesta incluye todos los ID de suceso enviados por el dispositivo. En el ejemplo siguiente, se devuelven valores para los sucesos “power” y “temperature”.

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
