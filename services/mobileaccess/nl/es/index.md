---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-07"

---

# Iniciación a {{site.data.keyword.amashort}}
{: #gettingstarted}

Añada seguridad a la app para móvil con el servicio {{site.data.keyword.amafull}}. Puede configurar la autorización del cliente para acceder a los recursos de fondo protegidos que se ejecutan en {{site.data.keyword.Bluemix_notm}}. Utilice proveedores de identidad (Google y Facebook), o identidades personalizadas para autenticar usuarios y otorgar acceso a las apps web y los recursos de fondo protegidos.
{:shortdesc}

**Nota:**: el servicio {{site.data.keyword.amashort}} se conocía anteriormente como Advanced Mobile Access.


Para comenzar a utilizar el servicio {{site.data.keyword.amashort}}:

1. Utilice una de las siguientes opciones para crear un servicio enlazado o no enlazado:
 * Cree una aplicación {{site.data.keyword.Bluemix_notm}} utilizando el contenedor modelo **MobileFirst Services Starter** del catálogo. Esto crea un servicio de {{site.data.keyword.amashort}} enlazado a una aplicación de programa de fondo de {{site.data.keyword.Bluemix_notm}}. 
 * Cree un servicio de {{site.data.keyword.amashort}} mediante el panel de control de {{site.data.keyword.amashort}}. Puede enlazar el servicio a una aplicación de programa de fondo existente y configurarlo en el panel de control de {{site.data.keyword.amashort}}.  

   Cuando utilice MobileFirst Services Starter, obtendrá una instancia de un tiempo de ejecución Node.js que se ejecuta en IBM {{site.data.keyword.Bluemix_notm}} para implementar la lógica del programa de fondo móvil. Se enlaza a la app Node.js un conjunto de servicios móviles principales que ofrecen funciones de seguridad, datos, envío y supervisión. Después de crear la app Node.js de {{site.data.keyword.Bluemix_notm}}, puede configurar el entorno de desarrollo y empezar a utilizar los SDK de {{site.data.keyword.Bluemix_notm}} Mobile Services. Puede utilizar los SDK para acceder a los servicios que están enlazados a la app de nube con sencillas llamadas API.

2. Recursos seguros del lado del servidor.

   Proteja los recursos del programa de fondo móvil que se estén ejecutando en los tiempos de ejecución Node.js o Liberty for Java&trade; con la seguridad OAuth habilitada para móvil. Para obtener más información, consulte [Protección de recursos](protecting-resources.html).
   Para obtener más información sobre la aplicación de fondo móvil predeterminada, consulte la aplicación de ejemplo [bms-hellotodo-strongloop](https://github.com/ibm-bluemix-mobile-services/bms-hellotodo-strongloop).

3. Configure su entorno de desarrollo {{site.data.keyword.amashort}} principal.

	####Desarrollo de cliente
   {: #client-development}

	Puede añadir el SDK de {{site.data.keyword.amashort}} a la app Android, iOS o Cordova existente:
   * Android: ([Configuración del SDK de Android](getting-started-android.html)) ([Ejemplo](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication))

   * iOS (SDK de Swift): ([Configuración del SDK de Swift para iOS](getting-started-ios-swift-sdk.html))
      ([Ejemplo](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication))

   * iOS (SDK de Objective-C): ([Configuración del SDK de Object-C para iOS](getting-started-ios.html)) ([Ejemplo](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication))

   * Cordova: ([Configuración del plugin de Cordova](getting-started-cordova.html)) ([Ejemplo](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloauthentication))

   **Nota:**  Si bien el SDK de Objective-C recibe total soporte y sigue considerándose como SDK principal para {{site.data.keyword.amashort}}, está previsto dejar de mantener este SDK a finales del año en favor del nuevo SDK de Swift. Si crea una aplicación, se recomienda utilizar el SDK de Swift (consulte [Configuración del SDK de Swift para iOS](getting-started-ios-swift-sdk.html)).

	####Desarrollo web
   {: #web-development}

   El servicio de {{site.data.keyword.amashort}} puede proteger su aplicación web, que no requiere SDK especiales. Puede aprovechar diferentes proveedores de identidad, además de la protección suministrada por el servicio de {{site.data.keyword.amashort}}. La integración de {{site.data.keyword.amashort}} permite que cualquier aplicación web, independientemente de la tecnología que implemente, aproveche el protocolo OAuth2. Para obtener información sobre cómo configurar la app web de {{site.data.keyword.amashort}} para que acceda al servicio de {{site.data.keyword.amashort}} utilizando otros proveedores de identidad, consulte: 

    * [Habilitación de la autenticación de Facebook para aplicaciones web](facebook-auth-web.html)

    * [Habilitación de la autenticación de Google para aplicaciones web](google-auth-web.html)

    * [Habilitación de la autenticación personalizada para aplicaciones web](custom-auth-web.html)

4. **Opcional:** configure un proveedor de identidad para su aplicación. Puede configurar un proveedor de identidad por aplicación. La configuración de un proveedor de identidad permite que los usuarios de la app para móvil puedan iniciar sesión con su cuenta de Facebook o Google+. También puede definir cómo deben iniciar sesión los usuarios creando una autenticación personalizada.
   * [Autenticación de usuarios con las credenciales de Facebook](facebook-auth-overview.html)
   * [Autenticación de usuarios con las credenciales de Google](google-auth-overview.html)
   * [Autenticación de usuarios con un proveedor de identidades personalizadas](custom-auth.html)


# Enlaces relacionados
{: #rellinks}

## Guías de aprendizaje y ejemplos
{: #samples}
* [Ejemplo android-helloauthentication](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication){: new_window}
* [Ejemplo ios-helloauthentication (SDK de Swift)](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication){: new_window}
* [Ejemplo ios-helloauthentication (SDK de Objective-C)](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication){: new_window}

## SDK
{: #sdk}
* [Core SDK (Android)](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}
* [Core SDK (plug-in de Cordova)](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}
* [Core SDK (iOS - Swift) ](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window}
* [SDK principal (iOS - Objective-C - En desuso) ](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master){: new_window}
* [Autenticación personalizada: ejemplo simple](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample){: new_window}
* [Autenticación personalizada: ejemplo avanzado](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management){: new_window}

## Referencia de API
{: api}
* [Android](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html){: new_window}
* [iOS (SDK de Objective-C - en desuso)](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html){: new_window}


## Enlaces relacionados
{: #general}
* [Visión general](overview.html){: new_window}
