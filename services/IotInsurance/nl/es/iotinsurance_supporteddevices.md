---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-07"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Proveedores y dispositivos soportados
{: #supportedcloud}

{{site.data.keyword.iotinsurance_full}} da soporte a la integración con múltiples dispositivos y proveedores de nube.
{: shortdesc}

## Dispositivos soportados por proveedor
{: #supportedvendors}
La tabla siguiente contiene una lista de los proveedores y dispositivos soportados por {{site.data.keyword.iotinsurance_short}} y describe el tipo de integración. Están disponibles los siguientes tipos de integración:

  - **{{site.data.keyword.iot_short_notm}}** -el dispositivo o hub publica los sucesos del sensor directamente en {{site.data.keyword.iot_short_notm}}. {{site.data.keyword.iotinsurance_short}} puede procesar los sucesos del sensor directamente o después de que el transformador de {{site.data.keyword.iotinsurance_short}} los modifique ligeramente.

  - **Cloud to Cloud** - el dispositivo o hub publica los sucesos del sensor en la nube de un tercero. El transformador de {{site.data.keyword.iotinsurance_short}} lea estos sucesos desde la nube del tercero y los publica en {{site.data.keyword.iot_short_notm}}.

<table>
<thead>
<tr>
<th>Nombre del proveedor</th>
<th>Tipo de integración</th>
<th>Dispositivos probados</th>
<th>Información del proveedor </th>
</tr>
</thead>
<tbody>
<tr>
<td>Bosch E-Call</td>
<td>{{site.data.keyword.iot_short_notm}}.  
Se ha escrito una aplicación de pasarela para probar la integración.</td>
<td>Bosch Retrofit E-Call</td>
<td>[Sitio web del proveedor ![Icono de enlace externo](../../icons/launch-glyph.svg)](http://www.bosch-connectivity.com/en/what_we_offer/products_and_solutions_1/retrofit_ecall/connected_devices_3){: new_window}</td>
</tr>
<tr>
<td>EnOcean</td>
<td>{{site.data.keyword.iot_short_notm}}</td>
<td>
<ul>
<li>Botón</li>
<li>Contacto</li>
<li>Temperatura</li>
</ul>
</td>
<td>[Sitio web del proveedor ![Icono de enlace externo](../../icons/launch-glyph.svg)](https://www.enocean.com/en/</td>){: new_window}
</tr>
<tr>
<td>WiButler (iExergy)</td>
<td>{{site.data.keyword.iot_short_notm}}</td>
<td>
<ul>
<li>Detector de humos</li>
<li>Botón</li></td>
</ul>
<td>[Sitio web del proveedor ![Icono de enlace externo](../../icons/launch-glyph.svg)](https://www.wibutler.com/en_GB){: new_window}</td>
</tr>
<tr>
<td>Wink</td>
<td>Cloud to Cloud</td>
<td>Fuga de agua</td>
<td>[Sitio web del proveedor ![Icono de enlace externo](../../icons/launch-glyph.svg)](https://www.wink.com/){: new_window}</td>
</tr>
<tr>
<td>Yanzi</td>
<td>{{site.data.keyword.iot_short_notm}} y Cloud to Cloud</td>
<td>No se ha probado ningún sensor.</td>
<td>[Sitio web del proveedor ![Icono de enlace externo](../../icons/launch-glyph.svg)](https://ibm.ent.box.com/notes/126680846739){: new_window}</td>
</tr>
</tbody>
</table>

## Integración de nubes de proveedores y dispositivos
{: #integratingdevices}
Puede integrar sus nubes de proveedores y dispositivos con {{site.data.keyword.iotinsurance_short}}. En las siguientes secciones se describen los procedimientos de integración y los registros de usuario de ejemplo para cada proveedor.

Para obtener más información sobre la integración de sensores y dispositivos, consulte [Kit de herramientas del dispositivo](iotinsurance_device_toolkit.html):


### EnOcean
#### Procedimiento de integración
  1. Cree una pasarela en la instancia de {{site.data.keyword.iot_short_notm}} que está conectada a {{site.data.keyword.iotinsurance_short}}.
  2. Conecte el hub de EnOcean a la pasarela de {{site.data.keyword.iot_short_notm}}.
  3. Añada el identificador de pasarela al registro de usuario en {{site.data.keyword.iotinsurance_short}}.

#### Registro de usuario de ejemplo

```
{
    "username": "user@example.com",
    "password": "",
    "accessLevel": "13",
    "fullname": "John Doe",
    "email": "user@example.com",
    "phonenumber": "+123456789",
    "address": {
      ...
    },
    "gatewayIds": [
      "digital-concepts-gateway1"
    ],
    ...
}
```

### WiButler (iExergy)

#### Procedimiento de integración
La integración con datos de WiButler solo está soportada como prueba de concepto o vista previa técnica y no está destinado para uso de producción. El hardware de WiButler requiere una actualización de firmware para transmitir datos a {{site.data.keyword.iot_short_notm}}.

#### Registro de usuario de ejemplo

```
{
    "username": "user@example.com",
    "password": "",
    "accessLevel": "13",
    "fullname": "John Doe",
    "email": "user@example.com",
    "phonenumber": "+123456789",
    "address": {
      ...
    },
    "gatewayIds": [
      "Wibutler-Gateway-ID"
    ],
    ...
}
```

### Wink

#### Procedimiento de integración

**Opción 1**
  1. Obtenga las [señales de autorización de Wink ![Icono de enlace externo](../../icons/launch-glyph.svg)](http://docs.winkapiv2.apiary.io/#){: new_window}.
  2. Añada la señal de autorización al usuario correspondiente en el sistema de {{site.data.keyword.iotinsurance_short}} utilizando la API de {{site.data.keyword.iotinsurance_short}}.

**Opción 2**  
Integre utilizando la aplicación móvil (en desuso). Este método solo funciona con la versión 1.0 de {{site.data.keyword.iotinsurance_short}}.

#### Registro de usuario de ejemplo

```
{
  "username": "user@example.com",
  "password": "",
  ....
  "deviceID": "528DB5CA-7F3D-4478-A4EB-994E7F118B6B",
  "assets": [
    {
      "name": "default",
      "providers": [
        {
          "name": "wink",
          "tokens": {
            "data": {
              "access_token": "fjyw9nN_YhU-fZU9kCqTQ6Ijsr_9XdvO",
              "refresh_token": "OOMyB8JGCHgjOHku8zp2Yrevoeci48Ou",
              "token_type": "bearer",
              "token_endpoint": "https://api.wink.com/oauth2/token",
              "scopes": "full_access"
            },
            "errors": [],
            "pagination": {},
            "access_token": "fjyw9nN_YhU-fZU9kCqTQ6Ijsr_9XdvO",
            "refresh_token": "OOMyB8JGCHgjOHku8zp2Yrevoeci48Ou",
            "token_type": "bearer",
            "token_endpoint": "https://api.wink.com/oauth2/token",
            "scopes": "full_access"
          }
        }
      ]
    }
  ]
}

```

### Yanzi
#### Procedimiento de integración
**Opción 1**  
  Añada credenciales de la nube de Yanzi a yanzi-config.json en el directorio del proveedor del repositorio del transformador.  El objeto "yanziCloud" es la ubicación correcta de las credenciales.  

**Opción 2**  
  Yanzi utiliza la integración cloud-to-cloud entre la nube de Yanzi y {{site.data.keyword.iot_short_notm}}. La autorización para esta integración se produce en la nube de Yanzi. Una vez completada la autorización, la nube de Yanzi envía sucesos a {{site.data.keyword.iot_short_notm}}. También deberá añadir las credenciales de la instancia de {{site.data.keyword.iot_short_notm}} a yanzi-config.json en el directorio del proveedor del repositorio del transformador utilizando el objeto "iotfCredentials".

#### Registro de usuario de ejemplo

```
{
  "yanziCloud": {
      "cirrusHost": "wss://",
      "username": "",
      "password": "",
      "locationId": "",
      "unitDid": ""
  },
  "iotfCredentials": {
      "org": "",
      "apiKey": "",
      "apiToken": "",
      "type": "shared",
      "mqtt_host": "gbdprt.messaging.internetofthings.ibmcloud.com",
      "domain": "internetofthings.ibmcloud.com"
  }
}
```

### Weather Company Data
#### Procedimiento de integración
La integración con Weather Company Data solo está soportada como prueba de concepto o vista previa técnica y no está destinado para uso de producción.

Proporcione una dirección para recuperar las condiciones meteorológicas actuales (temperatura exterior) extraídas de Weather Company para una ubicación específica.



#### Registro de usuario de ejemplo

```
{ "username": "johndoe",
   "fullname": "John Doe",
    "firstname": "John",
    "lastname": "Doe",
    "password": "",
     "accessLevel": 13,
     "address": "Mies-van-der-Rohe-Straße 6, 80807 München, Germany",
     ...
}

```
