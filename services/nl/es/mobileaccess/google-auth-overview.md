---

copyright:
  años: 2015, 2016
  
---

# Utilización de Google para autenticar usuarios
{: #google-auth}
Puede configurar el servicio de {{site.data.keyword.amashort}} para proteger los recursos utilizando Google como proveedor de identidad. Los usuarios de la aplicación móvil podrán autenticarse con las credenciales de Google.

**Importante:** no es necesario instalar el SDK de Google por separado. El SDK de Google se instala automáticamente con los gestores de dependencias cuando configura el SDK del cliente de {{site.data.keyword.amashort}}.

## Flujo de {{site.data.keyword.amashort}}
{: #google-auth-overview}

En el siguiente diagrama simplificado se explica cómo {{site.data.keyword.amashort}} se integra con Google para la autenticación.

![imagen](images/mca-sequence-google.jpg)

1. Utilice el SDK de {{site.data.keyword.amashort}} para realizar una solicitud a los recursos de fondo que están protegidos por el SDK del servidor de {{site.data.keyword.amashort}}.
* El SDK del servidor de {{site.data.keyword.amashort}} detecta la solicitud no autorizada y devuelve un código HTTP 401 y un ámbito de autorización.
* El SDK del cliente de {{site.data.keyword.amashort}} detecta automáticamente el código error HTTP 401 e inicia el proceso de autenticación.
* El SDK del cliente de {{site.data.keyword.amashort}} contacta con el servicio de {{site.data.keyword.amashort}} y solicita que emita una cabecera de autorización.
* El servicio de {{site.data.keyword.amashort}} solicita al cliente que realice la autenticación con Google primero proporcionando el cambio de autenticación.
* El SDK del cliente de {{site.data.keyword.amashort}} utiliza el SDK de Google para iniciar el proceso de autenticación. Después de una autenticación correcta, el SDK de Google devuelve una señal de acceso de Google.
* La señal de acceso de Google se considera la respuesta al cambio de autenticación. La señal se envía al servicio de {{site.data.keyword.amashort}}.
* El servicio valida la respuesta con los servidores de Google.
* Si la validación es correcta, el servicio de {{site.data.keyword.amashort}} genera una cabecera de autorización y la devuelve al SDK del cliente de {{site.data.keyword.amashort}}. La cabecera de autorización contiene dos señales: una señal de acceso con información sobre permisos de acceso y una señal de ID que incluye información sobre la aplicación, el dispositivo y el usuario actuales.
* A partir de este momento, todas las solicitudes que se realicen con el SDK del cliente de {{site.data.keyword.amashort}} tendrán una cabecera de autorización nueva.
* El SDK del cliente de {{site.data.keyword.amashort}} vuelve a enviar automáticamente la solicitud original que activó el flujo de autorización.
* El SDK del servidor de {{site.data.keyword.amashort}} extrae la cabecera de autorización de la solicitud, la valida con el servicio de {{site.data.keyword.amashort}} y otorga acceso a un recurso de fondo.

## Próximos pasos
{: #google-auth-nextsteps}

* [Habilitación de la autenticación de Google en apps de Android](google-auth-android.html)
* [Habilitación de la autenticación de Google en apps de iOS](google-auth-ios.html)
* [Habilitación de la autenticación de Google en apps de Cordova](google-auth-cordova.html)
