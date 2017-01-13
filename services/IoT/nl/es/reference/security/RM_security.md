---

copyright:
  years: 2015,2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Gestión de riesgos y de seguridad
{: #RM_security}
Última actualización: 15 de noviembre de 2016
{: .last-updated}

El complemento Risk and Security Management permite a las organizaciones mejorar la seguridad de la plataforma IBM Watson IoT mediante la creación, imposición y notificación de la seguridad de la conexión de dispositivos.
Con este complemento se utilizan certificados y autenticación TLS (seguridad de capa de transporte) sobre los ID de usuario y señales que utiliza la plataforma Watson IoT para determinar cómo y cuándo se conectan los dispositivos a la plataforma. Durante la comunicación entre los dispositivos y el servidor, a cualquier dispositivo que no tenga certificados válidos con acceso al servidor, configurado en el complemento Risk and Security Management, se le deniega el acceso, aunque utilice ID de usuario y contraseñas válidos. 

**Nota:** para registrarse y habilitar el programa IBM Watson IoT Platform Risk and Security Management Beta, vaya a https://developer.ibm.com/iotplatform/2016/11/02/experience-the-latest-iot-security-capabilities-sign-up-to-our-november-beta-today/.

## Política de seguridad de conexión

La política de seguridad de conexión impone la forma en que los dispositivos se conectan a la plataforma. Puede configurar políticas de conexión predeterminadas para todos los tipos de dispositivo, así como valores personalizados para tipos de dispositivo específicos. La política se puede definir de modo que permita conexiones sin cifrar, que imponga solo conexiones de seguridad de la capa de transporte (sólo TLS) y que habilite los dispositivos para que se autentiquen con certificados del lado del cliente. Cuando se utilizan certificados del lado del cliente, la política de seguridad proporciona la opción adicional de utilizar solo certificado para la autenticación de cliente o de utilizar una combinación de certificado de cliente y par de señales de ID de cliente y señal de autenticación.   

La seguridad de conexión también se puede configurar de modo que los clientes utilicen su propio certificado del lado del servidor en lugar del certificado predeterminado que se proporciona. Esto puede resultar útil, por ejemplo, si los dispositivos del usuario autenticarán el servidor durante el reconocimiento de TLS. En este release inicial de Risk and Security Management, el nombre del dominio del servidor de la plataforma Watson IoT no se puede modificar y se debe utilizar tal cual en el certificado del servidor. 

## Certificados de cliente

Para configurar certificados los certificados del cliente y el acceso al servidor de los dispositivos, el operador del sistema importa los certificados de la entidad emisora de certificados (CA) asociada y los certificados del servidor de mensajería en la plataforma Watson IoT. Luego el analista de seguridad configura las políticas de seguridad de conexión de modo que las conexiones predeterminadas entre los dispositivos y la plataforma utilicen los niveles de seguridad Solo certificados o Certificados con señal de autenticación. El analista puede añadir distintas políticas para los distintos tipos de dispositivos.

## Políticas de lista blanca y lista negra

Las políticas de lista blanca y lista negra proporcionan la posibilidad de controlar las ubicaciones desde las que los dispositivos pueden conectar con la cuenta de la organización. Una lista negra identifica todas las direcciones IP, CIDR o países a los que se denegará el acceso al servidor, mientras una lista blanca proporciona acceso explícito a determinadas direcciones IP.

## Panel de control de Risk and Security Management

Finalmente, el operador del sistema y el analista de seguridad pueden utilizar el panel de control de Risk and Security Management para ver el estado general de la seguridad. Las tarjetas del panel de control ofrecen una completa visión general, así como el estado de conexión de los dispositivos. 
