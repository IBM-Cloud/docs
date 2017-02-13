---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Iniciación a {{site.data.keyword.amashort}}
{: #gettingstarted}

Añada seguridad a la app para móvil con el servicio {{site.data.keyword.amafull}}. Puede configurar la autorización del cliente para acceder a los recursos de fondo protegidos que se ejecutan en {{site.data.keyword.Bluemix}}. Utilice proveedores de identidad (Google y Facebook), o identidades personalizadas para autenticar usuarios y otorgar acceso a las apps web y los recursos de fondo protegidos.
{:shortdesc}

**Nota:**: el servicio {{site.data.keyword.amashort}} se conocía anteriormente como Advanced Mobile Access.


Para comenzar a utilizar el servicio {{site.data.keyword.amashort}}:

1. Utilice una de las siguientes opciones para crear un servicio enlazado o no enlazado:
 * Cree una aplicación {{site.data.keyword.Bluemix_notm}} utilizando el contenedor modelo **MobileFirst Services Starter** del catálogo. Esto crea un servicio de {{site.data.keyword.amashort}} enlazado a una aplicación de programa de fondo de {{site.data.keyword.Bluemix_notm}}.
 * Cree un servicio de {{site.data.keyword.amashort}} mediante la consola de {{site.data.keyword.amashort}}. Puede enlazar el servicio a una aplicación de programa de fondo existente y configurarlo en la consola de {{site.data.keyword.amashort}}.

   Cuando utilice MobileFirst Services Starter, obtendrá una instancia de un tiempo de ejecución Node.js que se ejecuta en IBM {{site.data.keyword.Bluemix_notm}} para implementar la lógica del programa de fondo móvil. Se enlaza a la app Node.js un conjunto de servicios móviles principales que ofrecen funciones de seguridad, datos, envío y supervisión. Después de crear la app Node.js de {{site.data.keyword.Bluemix_notm}}, puede configurar el entorno de desarrollo y empezar a utilizar los SDK de {{site.data.keyword.Bluemix_notm}} Mobile Services. Puede utilizar los SDK para acceder a los servicios que están enlazados a la app de nube con sencillas llamadas API.

	Para obtener más información sobre cómo crear y trabajar con proyectos, aplicaciones y servicios, consulte [Panel de control de IBM Bluemix Mobile](https://console.{DomainName}/docs/mobile/index.html).

2. Recursos seguros del lado del servidor.

   Proteja los recursos del programa de fondo móvil que se estén ejecutando en los tiempos de ejecución Node.js o Liberty for Java&trade; con la seguridad OAuth habilitada para móvil. Para obtener más información, consulte [Protección de recursos](protecting-resources.html).
   Para obtener más información sobre la aplicación de fondo móvil predeterminada, consulte la aplicación de ejemplo [bms-hellotodo-strongloop ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-hellotodo-strongloop "Icono de enlace externo"){: new_window}.

3. Configure su entorno de desarrollo {{site.data.keyword.amashort}} principal.

  ####Desarrollo de cliente
  {: #client-development}

	Puede añadir el SDK de {{site.data.keyword.amashort}} a la app Android, iOS o Cordova existente:
   * Android: ([Configuración del SDK de Android](getting-started-android.html)) [Ejemplo ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication "Icono de enlace externo"){: new_window}
    * iOS (Swift SDK): ([Configuración del SDK de Swift de iOS](getting-started-ios-swift-sdk.html)) [Ejemplo ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication "Icono de enlace externo"){: new_window}    
   * Cordova: ([Configuración del plug-in de Cordova](getting-started-cordova.html)) [Ejemplo ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloauthentication "Icono de enlace externo"){: new_window}


 ####Desarrollo web
 {: #web-development}

   El servicio de {{site.data.keyword.amashort}} puede proteger su aplicación web, que no requiere SDK especiales. Puede aprovechar diferentes proveedores de identidad, además de la protección suministrada por el servicio de {{site.data.keyword.amashort}}. La integración de {{site.data.keyword.amashort}} permite que cualquier aplicación web, independientemente de la tecnología que implemente, aproveche el protocolo OAuth2. Para obtener información sobre cómo configurar la app web de {{site.data.keyword.amashort}} para que acceda al servicio de {{site.data.keyword.amashort}} utilizando otros proveedores de identidad, consulte:

   * [Habilitación de la autenticación de Facebook para aplicaciones web](facebook-auth-web.html)
   * [Habilitación de la autenticación de Google para aplicaciones web](google-auth-web.html)
   * [Habilitación de la autenticación personalizada para aplicaciones web](custom-auth-web.html)

**Opcional:** configure un proveedor de identidad para su aplicación. Puede configurar un proveedor de identidad por aplicación. La configuración de un proveedor de identidad permite que los usuarios de la app para móvil puedan iniciar sesión con su cuenta de Facebook o Google+. También puede definir cómo deben iniciar sesión los usuarios creando una autenticación personalizada.
   * [Autenticación de usuarios con las credenciales de Facebook](facebook-auth-overview.html)
   * [Autenticación de usuarios con las credenciales de Google](google-auth-overview.html)
   * [Autenticación de usuarios con un proveedor de identidades personalizadas](custom-auth.html)

## Guías de aprendizaje y ejemplos
{: #samples}

* [Ejemplo de android-helloauthentication ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication "Icono de enlace externo"){: new_window}
* [Ejemplo de ios-helloauthentication (SDK de Swift) ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication "Icono de enlace externo"){: new_window}

## SDK
{: #sdk}

* [SDK de Core (Android) ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core "Icono de enlace externo"){: new_window}

* [Ejemplo de ios-helloauthentication (SDK de Swift) ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication "Icono de enlace externo"){: new_window}

* [Autenticación personalizada - ejemplo sencillo ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample "Icono de enlace externo"){: new_window}

* [Autenticación personalizada - ejemplo avanzado ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management "Icono de enlace externo"){: new_window}


