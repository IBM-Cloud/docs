---

copyright:

years: 2017
lastupdated: "2017-03-16"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# API
{: #api_overview}

Dispone de varias API para el desarrollo de código para dispositivos, pasarelas y aplicaciones que se conectan a {{site.data.keyword.iot_full}}.

Las API HTTP están protegidas con autenticación básica HTTP. Al generar una clave de API mediante el panel de instrumentos, se le presentará una clave y una señal de autenticación. Para obtener más información sobre claves de API y señales, consulte [Conexión de la clave de API](../platform_authorization.html#api-key).


## Acerca de las API HTTP
{: #api_about}

Después de registrar su propia organización, se le proporcionará un ID de organización de 6 caracteres, que necesitará en el nombre de host para cualquier llamada de API HTTP. Puede acceder al URL base de su organización en la siguiente dirección:

https://<**orgId**>.internetofthings.ibmcloud.com/api/v0002

Para autenticar solicitudes a la API de aplicación, establezca el nombre de usuario en la clave de API y la contraseña en la señal de autenticación. 

Para las API de mensajería, utilice la siguiente dirección:

https://<**orgId**>.messaging.internetofthings.ibmcloud.com/api/v0002

## API HTTP
{: #api_http}

API                     | Utilícela para...       
------------- | -------------
[Administración de la organización ![Icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/orgAdmin.html){: new_window} | Configurar una organización (incluyendo crear y suprimir dispositivos), comprobar el uso, el estado del servicio y diagnosticar problemas de conexión del dispositivo.
[Seguridad ![Icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/security.html){: new_window} | Gestionar la autenticación y las invitaciones de usuarios, y la autorización de usuarios, claves de API y dispositivos.
[Gestión de la información ![Icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/info-mgmt.html){: new_window} |  Acceder a los datos de sucesos del dispositivo, así como para obtener y actualizar la ubicación del dispositivo y obtener información meteorológica para dicha ubicación.
[Gestión de dispositivos ![Icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/deviceMgmt.html){: new_window} | Interactuar con dispositivos gestionados utilizando el protocolo de gestión de dispositivos.
[Mensajería ![Icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/http-messaging.html){: new_window}   | Publicar sucesos y enviar mandatos utilizando HTTP. **Nota:** para las API de mensajería, utilice la dirección *https://<**orgId**>.messaging.internetofthings.ibmcloud.com/api/v0002*



## API HTTP de extensión
{: #api_extension}

API                     | Utilícela para...       
------------- | -------------
[Extensión de AT&T ![Icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/ext-atnt.html){: new_window} | Administrar dispositivos AT&T.
[Extensión de Jasper ![Icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/ext-jasper.html){: new_window} | Administrar dispositivos Jasper.
[Extensión de Orange ![Icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/ext-orange.html){: new_window} | Visualizar los datos de la tarjeta SIM desde dispositivos que están conectados a su organización de {{site.data.keyword.iot_short_notm}} y tienen una tarjeta SIM de Orange instalada.
## API HTTP beta
{: #api_beta}

API                     | Utilícela para...       
------------- | -------------
[Seguridad de pasarela ![Icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html){: new_window}   | Comprobar y asignar roles a dispositivos de pasarela.
[Seguridad de dispositivos ![Icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-devices-beta.html){: new_window} | Comprobar y asignar roles a dispositivos.
[Correlación de interfaces ![Icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html){: new_window}   |   Correlacionar y acceder a datos del dispositivo mediante interfaces.
