---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-22"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Gestión de riesgos y de seguridad
{: #RM_security}

El complemento Risk and Security Management permite a las organizaciones mejorar la seguridad de {{site.data.keyword.iot_full}} mediante la creación, imposición y notificación de la seguridad de la conexión de dispositivos. Con este complemento se utilizan certificados y autenticación TLS (seguridad de capa de transporte) sobre los ID de usuario y señales que utiliza {{site.data.keyword.iot_short_notm}} para determinar cómo y cuándo se conectan los dispositivos a la plataforma. Durante la comunicación entre los dispositivos y el servidor, a cualquier dispositivo que no tenga certificados válidos con acceso al servidor, configurado en el complemento Risk and Security Management, se le deniega el acceso, aunque utilice ID de usuario y contraseñas válidos.

## Política de seguridad de conexión
{: #connect_policy}

La política de seguridad de conexión impone la forma en que los dispositivos se conectan a la plataforma y se utilizan con planes de seguridad gratuitos y avanzados. Puede configurar políticas de conexión predeterminadas para todos los tipos de dispositivo, así como valores personalizados para tipos de dispositivo específicos. La política se puede definir de modo que permita conexiones sin cifrar, que imponga solo conexiones de seguridad de la capa de transporte (sólo TLS) y que habilite los dispositivos para que se autentiquen con certificados del lado del cliente.

Si utiliza un plan de seguridad estándar, las políticas de conexión no están disponibles. Para obtener información sobre cómo configurar las políticas de seguridad de conexión, consulte [Configuración de políticas de seguridad](set_up_policies.html).

La seguridad de conexión también se puede configurar de modo que los clientes utilicen su propio certificado del lado del servidor en lugar del certificado predeterminado que se proporciona. Esto puede resultar útil, por ejemplo, si los dispositivos del usuario se autenticarán ante el servidor durante el reconocimiento de TLS. En este release inicial de Risk and Security Management, el nombre del dominio del servidor de {{site.data.keyword.iot_short_notm}} no se puede modificar y se debe utilizar tal cual en el certificado del servidor.



## Certificados de cliente
{: #certificates}

Para configurar certificados los certificados del cliente y el acceso al servidor de los dispositivos, el operador del sistema importa los certificados de la entidad emisora de certificados (CA) asociada y los certificados del servidor de mensajería en {{site.data.keyword.iot_short_notm}}. Luego el analista de seguridad configura las políticas de seguridad de conexión de modo que las conexiones predeterminadas entre los dispositivos y la plataforma utilicen los niveles de seguridad Solo certificados o Certificados con señal de autenticación. El analista puede añadir distintas políticas para los distintos tipos de dispositivos.

Para obtener información sobre cómo configurar certificados, consulte [Configuración de certificados](set_up_certificates.html).

## Políticas de lista negra y lista blanca
{: #wl_bl}

Las políticas de lista negra y lista blanca proporcionan la posibilidad de controlar las ubicaciones desde las que los dispositivos pueden conectar con la cuenta de la organización. Una lista negra identifica todas las direcciones IP, CIDR o países a los que se denegará el acceso al servidor, mientras una lista blanca proporciona acceso explícito a determinadas direcciones IP.

Para obtener información sobre cómo configurar políticas de lista negra y lista blanca, consulte [Configuración de listas negras y listas blancas](set_up_policies.html#config_black_white).

## Panel de control de Risk and Security Management
{: #dashboard}

Finalmente, el operador del sistema y el analista de seguridad pueden utilizar el panel de control de Risk and Security Management para ver el estado general de la seguridad. Las tarjetas del panel de control ofrecen una completa visión general, así como el estado de conexión de los dispositivos.
