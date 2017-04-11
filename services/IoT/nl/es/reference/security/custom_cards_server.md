---

copyright:
  years: 2016, 2017
lastupdated: "2016-11-29"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Protección del servidor de tarjetas personalizadas
{: #securing_custom_cards}

Los servidores de tarjetas personalizadas son servidores web estándares que alojan el código javascript de las tarjetas personalizadas. Para garantizar la integridad del entorno de {{site.data.keyword.iot_short_notm}}, debe proteger el servidor de tarjetas personalizadas realizando los pasos necesarios para proteger el origen de las tarjetas como se describe en este tema.
{:shortdesc}

**Importante:** Las tarjetas personalizadas se ofrecen en este momento como una característica experimental y la extensión de tarjetas personalizadas se habilita por sesión de navegador. La configuración de la conexión de tarjetas personalizadas y los paquetes de tarjetas no se comparten globalmente en la organización de {{site.data.keyword.iot_short_notm}}.

## Requisito de rol de {{site.data.keyword.Bluemix_notm}}
{: #roles_requirements}

Debe tener derechos de administrador de {{site.data.keyword.iot_short_notm}} para crear una conexión de servidor de tarjetas personalizadas.

## Consideraciones de seguridad del servidor de tarjetas personalizadas
{: #server_requirements}

{{site.data.keyword.iot_short_notm}} establece los siguientes requisitos:
- El directorio que sirve el contenido de tarjetas personalizadas en el servidor no debe requerir credenciales para acceder.  
No se proporciona autenticación para el servidor de tarjetas personalizadas cuando se conecta para acceder y cargar tarjetas personalizadas.
- El servidor debe utilizar el protocolo HTTP Secure (HTTPS).
- El servidor debe soportar conexiones CORS (Cross-Origin Resource Sharing).  

Para proteger el código de tarjetas personalizadas y el propio servidor de tarjetas, el servidor de tarjetas debe localizarse y protegerse mediante defensa en profundidad. Esto incluye la protección de cortafuegos para restringir el acceso al servidor de tarjetas personalizadas.

El proceso de tarjetas personalizadas se encuentra siempre entre el navegador de un usuario y el servidor de tarjetas personalizadas. El programa de fondo de {{site.data.keyword.iot_short_notm}} nunca está implicado en el proceso o en el ajuste del código y de la información de tarjetas personalizadas.

No hay restricciones colocadas en el código JavaScript que pueda elegir para desplegar en las tarjetas del servidor de tarjetas personalizado. El código Javascript en las tarjetas personalizadas tiene acceso a toda la información guardada en el navegador, como cualquier otra tarjeta que se ejecute en el panel de control.  Asegúrese de que el servidor de tarjetas personalizadas correcto facilite el código al navegador para mostrar y procesar las tarjetas personalizadas.

Las tarjetas ejecutan su código en la sesión del navegador {{site.data.keyword.iot_short_notm}} exactamente como se ha escrito. Además, se crea la conexión del servidor de tarjetas personalizadas sin credenciales proporcionadas al servidor de tarjetas personalizado. Un navegador de usuarios puede conectarse a cualquier servidor de tarjetas personalizadas configurado.

Es importante que sólo configure los servidores de tarjetas personalizadas protegidos y conocidos para facilitar tarjetas personalizadas a los paneles de control de los usuarios.   
