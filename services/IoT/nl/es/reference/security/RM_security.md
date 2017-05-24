---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Gestión de riesgos y de seguridad
{: #RM_security}

Puede mejorar la seguridad para habilitar la creación, imposición y notificación de la seguridad de la conexión de dispositivos. Con esta seguridad avanzada, se utilizan certificados y autenticación TLS (seguridad de capa de transporte), además de los ID de usuario y las señales que utiliza {{site.data.keyword.iot_short_notm}} para determinar cómo y cuándo se conectan los dispositivos a la plataforma. Si los certificados están habilitados, durante la comunicación entre los dispositivos y el servidor, a cualquier dispositivo que no tenga certificados válidos, según la configuración de los valores de seguridad, se le deniega el acceso, aunque utilice ID de usuario y contraseñas válidos.

## Certificados de cliente
{: #certificates}

Para configurar certificados los certificados del cliente y el acceso al servidor de los dispositivos, el operador del sistema importa los certificados de la entidad emisora de certificados (CA) asociada y los certificados del servidor de mensajería en {{site.data.keyword.iot_short_notm}}. Luego el analista de seguridad configura las políticas de seguridad de conexión de modo que las conexiones predeterminadas entre los dispositivos y la plataforma utilicen los niveles de seguridad Solo certificados o Certificados con señal de autenticación. El analista puede añadir distintas políticas para los distintos tipos de dispositivos.

Para obtener información sobre cómo configurar certificados, consulte [Configuración de certificados](set_up_certificates.html).

## Planes de organización y políticas de seguridad
Las políticas de seguridad reforzadas permiten a las organizaciones determinar cómo quieren conectar los dispositivos y la autenticación en la plataforma, utilizando políticas de conexión y políticas de listas negras y listas blancas. Las opciones de las políticas de seguridad disponibles para una organización dependen del tipo de plan de la organización, del siguiente modo:

**Plan estándar:**
- Los operadores del sistema pueden configurar las políticas de conexión con las siguientes opciones:
    - TLS opcional 
    - TLS con autenticación de señal
    - TLS con autenticación de señal y de certificado de cliente

**Plan de seguridad avanzada (ASP) o plan Lite:** 
- Los operadores del sistema pueden configurar las políticas de conexión con las siguientes opciones:
    - TLS opcional 
    - TLS con autenticación de señal
    - TLS con autenticación de certificado de cliente
    - TLS con autenticación de señal y de certificado de cliente
    - TLS con señal o certificado de cliente
- Los operadores del sistema pueden configura las listas negras o las listas blancas

## Políticas de conexión
{: #connect_policy}

Las políticas de conexión imponen cómo se conectan los dispositivos a la plataforma. Puede configurar políticas de conexión predeterminadas para todos los tipos de dispositivo y crear valores personalizados para tipos de dispositivo específicos. La política se puede definir de modo que permita conexiones sin cifrar, que imponga solo conexiones de seguridad de la capa de transporte (sólo TLS) y que habilite los dispositivos para que se autentiquen con certificados del lado del cliente.

Para obtener información sobre cómo configurar las políticas de seguridad de conexión, consulte [Configuración de políticas de seguridad](set_up_policies.html).

La seguridad de conexión también se puede configurar de modo que los operadores del sistema puedan utilizar su propio certificado de servidor de mensajería en lugar del certificado predeterminado que se proporciona. El uso de un certificado de servidor de mensajería personalizado puede resultar útil si los dispositivos del usuario se autenticarán ante el servidor durante el reconocimiento de TLS. Solo se admiten los certificados de servidor de mensajería personalizados que utilizan el mismo dominio que el servidor de mensajería de IoTP original (<orgId>.messaging.internetofthings.ibmcloud.com).

## Políticas de lista negra y lista blanca
{: #wl_bl}

Las políticas de lista negra y lista blanca proporcionan la posibilidad de controlar las ubicaciones desde las que los dispositivos pueden conectar con la cuenta de la organización. Una lista negra identifica todas las direcciones IP, CIDR o países a los que se denegará el acceso al servidor, mientras una lista blanca proporciona acceso explícito a determinadas direcciones IP.

Para obtener información sobre cómo configurar políticas de lista negra y lista blanca, consulte [Configuración de listas negras y listas blancas](set_up_policies.html#config_black_white).

## Panel de control de Risk and Security Management
{: #dashboard}

Finalmente, el operador del sistema y el analista de seguridad pueden utilizar el panel de control de Risk and Security Management para ver el estado general de la seguridad. Las tarjetas del panel de control ofrecen una completa visión general, así como el estado de conexión de los dispositivos.
