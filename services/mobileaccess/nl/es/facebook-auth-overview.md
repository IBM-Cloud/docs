---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Autenticación de usuarios con las credenciales de Facebook
{: #facebook-auth-overview}

Puede configurar el servicio de {{site.data.keyword.amafull}} para proteger los recursos utilizando Facebook como proveedor de identidad. Los usuarios de la aplicación móvil o web podrán autenticarse con las credenciales de Facebook.

{:shortdesc}

**Importante**: no es necesario instalar por separado el SDK del cliente proporcionado por Facebook. El SDK de Facebook se instala automáticamente por los gestores de dependencias cuando configura el SDK del cliente de Facebook de {{site.data.keyword.amashort}}.

## Flujo de solicitudes de {{site.data.keyword.amashort}}
{: #mca-facebook-sequence}

### Flujo de solicitudes de cliente móvil

Consulte el siguiente diagrama en el que se explica cómo {{site.data.keyword.amashort}} se integra con Facebook para la autenticación, desde una aplicación de cliente móvil.

![Diagrama del flujo de solicitudes de cliente móvil](images/mca-sequence-facebook.jpg)

* Utilice el SDK del cliente de {{site.data.keyword.amashort}} para realizar una solicitud a los recursos de fondo protegidos por el SDK del servidor de {{site.data.keyword.amashort}}.
* El SDK del servidor de {{site.data.keyword.amashort}} detecta una solicitud no autorizada y devuelve el código HTTP 401 y un ámbito de autorización.
* El SDK del cliente de {{site.data.keyword.amashort}} detecta automáticamente el código error HTTP 401 e inicia el proceso de autenticación.
* El SDK del cliente de {{site.data.keyword.amashort}} contacta con el servicio de {{site.data.keyword.amashort}} y solicita una cabecera de autorización.
* El servicio de {{site.data.keyword.amashort}} solicita al cliente que realice la autenticación con Facebook primero proporcionando el cambio de autenticación.
* El SDK del cliente de {{site.data.keyword.amashort}} utiliza el SDK de Facebook para iniciar el proceso de autenticación. Después de una autenticación correcta, el SDK de Facebook devuelve una señal de acceso de Facebook.
* La señal de acceso de Facebook se considera la respuesta al cambio de autenticación. La señal se envía al servicio de {{site.data.keyword.amashort}}.
* El servicio valida la respuesta con los servidores de Facebook.
* Si la validación es correcta, el servicio de {{site.data.keyword.amashort}} genera una cabecera de autorización y la devuelve al SDK del cliente de {{site.data.keyword.amashort}}. La cabecera de autorización contiene dos señales: una señal de acceso con información sobre permisos de acceso y una señal de ID que incluye información sobre la aplicación, el dispositivo y el usuario actuales.
* A partir de este momento, todas las solicitudes que se realicen con el SDK del cliente de {{site.data.keyword.amashort}} tendrán una cabecera de autorización nueva.
* El SDK del cliente de {{site.data.keyword.amashort}} vuelve a enviar automáticamente la solicitud original que activó el flujo de autorización.
* El SDK del servidor de {{site.data.keyword.amashort}} extrae la cabecera de autorización de la solicitud, la valida con el servicio de {{site.data.keyword.amashort}} y otorga acceso a un recurso de fondo.

### Flujo de solicitud de aplicación web de {{site.data.keyword.amashort}}
{: #mca-facebook-web-sequence}

El flujo de solicitud de aplicación web de {{site.data.keyword.amashort}} es similar al flujo del cliente móvil. Sin embargo, {{site.data.keyword.amashort}} protege la aplicación web, en lugar de un recurso de fondo de {{site.data.keyword.Bluemix_notm}}.

  * La solicitud inicial la envía la aplicación web (desde un formulario de inicio de sesión, por ejemplo).
  * El redireccionamiento final es en el área protegida de la propia aplicación web, en lugar de en el recurso protegido de fondo.


## Creación de una aplicación en el sitio web de Facebook for Developers
{: #facebook-appID}

Para empezar a utilizar Facebook como proveedor de identidad, cree una aplicación en el sitio web Facebook for Developers. Durante este proceso, se creará un ID de app de Facebook. Este es un identificador exclusivo utilizado por Facebook para saber qué aplicación está intentando conectarse.

Necesita este valor para configurar la autenticación de Facebook para la aplicación móvil o web.

1. Acceda al sitio [Facebook for Developers ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developers.facebook.com "Icono de enlace externo"){: new_window}.

1. Abra la lista desplegable **Mis apps** y seleccione **Añadir una nueva app**.

1. Especifique los valores **Nombre de visualización** y **Valores de correo electrónico de contacto** y elija una **Categoría** de la lista desplegable.

1. Pulse **Crear un nuevo ID de app**.

1. Puede aparecer una comprobación de seguridad. Realice la acción solicitada.

1. Aparecerá la página **Configuración del producto**. Copie el **ID de app** que se muestra.

## Pasos siguientes
{: #next-steps}

* [Habilitación de la autenticación de Facebook para apps de Android](facebook-auth-android.html)
* [Habilitación de la autenticación de Facebook para apps de iOS (SDK de Swift)](facebook-auth-ios-swift-sdk.html)
* [Habilitación de la autenticación de Facebook para apps de Cordova](facebook-auth-cordova.html)
