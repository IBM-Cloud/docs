---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# Modo de funcionamiento
{: #about}

Puede obtener más información sobre los componentes, la arquitectura y el flujo de solicitudes que {{site.data.keyword.appid_short_notm}} utiliza.
{:shortdesc}


Puede utilizar el servicio de las siguientes maneras:

* Para añadir la autenticación a sus aplicaciones móviles y web
* Para otorgar acceso a los recursos de fondo protegidos y a las apps web
* Para proteger las aplicaciones Node.js y Swift alojadas en {{site.data.keyword.Bluemix_notm}}
* Para almacenar los datos de usuario, como por ejemplo las preferencias de la app o la información desde sus perfiles sociales públicos
* Para utilizar datos almacenados para crear experiencias de la app personalizadas
* Para proteger los recursos de los usuarios autenticados y anónimos

**Nota**: Los protocolos implementados son totalmente compatibles con OpenID Connect (OIDC).


## Componentes
{: #components}

* Panel de control: Descargar ejemplos de incorporación, consultar registros de actividad, configurar varios tipos de autenticación y de proveedores de identidad
* SDK de cliente: Crear apps móviles y web que utilizan el servicio para implementar la autenticación de usuario
    * Requisitos previos para Android: API 25 o superior, Java 8.x, Android SDK tools 25.2.5 o superior, Android SDK Platform Tools 25.0.3 o superior, Android Build Tools versión 25.0.2
    * Requisitos previos para iOS: iOS9 o superior, MacOS 10.11.5, Xcode 8.2
* SDK del servidor: proteja los recursos que se alojan en {{site.data.keyword.Bluemix_notm}}
    * Los tiempos de ejecución soportados son Node.js y Swift

## Visión general de la arquitectura
{: #architecture}

Con {{site.data.keyword.appid_short_notm}} puede añadir un nivel de seguridad a sus aplicaciones solicitando a los usuarios que inicien la sesión. También puede utilizar el SDK del servidor para proteger los recursos de fondo.

El siguiente diagrama muestra una visión general del funcionamiento del servicio {{site.data.keyword.appid_short_notm}}.

![Diagrama de la arquitectura de {{site.data.keyword.appid_short_notm}}](/images/appid_architecture2.png)

Figura 1. Diagrama de la arquitectura de {{site.data.keyword.appid_short_notm}}

<dl>
  <dt> SDK del cliente </dt>
    <dd> El SDK del cliente proporciona una clase de solicitud para comunicarse con sus recursos de la nube. El SDK del cliente inicia automáticamente el proceso de autenticación cuando detecta un desafío de autorización. </dd>
  <dt> Bluemix </dt>
    <dd>  El SDK del servidor extrae la señal de acceso de la solicitud y la valida con {{site.data.keyword.appid_short_notm}}. Tras la correcta autenticación, {{site.data.keyword.appid_short_notm}} devuelve las señales de identidad y de autorización a la aplicación.</dd>
  <dt> Proveedores de identidad </dt>
    <dd> Puede configurar Facebook, Google o ambos para autenticar sus apps. </dd>
</dl>


## Flujo de solicitudes
{: #request}

En el diagrama siguiente se describe el flujo de una solicitud, desde el SDK del cliente a los proveedores de identidad y de la aplicación de programa de fondo.

Flujo de solicitudes de ![{{site.data.keyword.appid_short_notm}}](/images/appidflow.png)


* Utilice el SDK del cliente de {{site.data.keyword.appid_short_notm}} para realizar una solicitud a los recursos de fondo protegidos por el SDK del servidor de {{site.data.keyword.appid_short_notm}}.
* El SDK del servidor de {{site.data.keyword.appid_short_notm}} detecta una solicitud no autorizada y devuelve HTTP 401 y el ámbito de autorización.
* El SDK del cliente detecta automáticamente el código HTTP 401 e inicia el proceso de autenticación.
* Cuando el SDK del cliente establece contacto con el servicio, el SDK del servidor devuelve el widget de inicio de sesión si hay más de un proveedor de identidad configurado. {{site.data.keyword.appid_short_notm}} llama al proveedor de identidad y presenta el formulario de inicio de sesión para dicho proveedor o devuelve un código de concesión que les permite autenticarse si no hay ningún proveedor de identidad configurado.
* {{site.data.keyword.appid_short_notm}} solicita al cliente que se autentique especificando un cambio de autenticación.
* Si Facebook o Google están configurados y el usuario inicia una sesión, la autenticación se gestiona mediante el flujo de OAuth del proveedor de identidad correspondiente.
* Si la autenticación finaliza con el mismo código de concesión, el código se envía al punto final de señal. El punto final devuelve dos señales: una señal de acceso y una de identidad. A partir de este momento, todas las solicitudes realizadas con el SDK del cliente tendrán una cabecera de autorización nueva.
* El SDK del cliente vuelve a enviar automáticamente la solicitud original que activó el flujo de autorización.
* El SDK del servidor extrae la cabecera de autorización de la solicitud, valida la cabecera con el servicio y otorga acceso a un recurso de fondo.
