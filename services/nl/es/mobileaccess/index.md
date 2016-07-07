---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Iniciación a {{site.data.keyword.amashort}}
{: #gettingstarted}
*Última actualización: 15 de junio de 2016*
{: .last-updated}

Añada funciones de seguridad a la app para móvil con el servicio {{site.data.keyword.amafull}}. Puede configurar la autenticación de cliente y los proveedores de identidad de modo que los usuarios puedan iniciar una sesión en la app con sus cuentas existentes de Google o Facebook.
{:shortdesc}

**Note:**: el servicio {{site.data.keyword.amashort}} se conocía anteriormente como Advanced Mobile Access.


Para comenzar a utilizar el servicio {{site.data.keyword.amashort}}, siga estos pasos:

1.  Utilice el panel de control de {{site.data.keyword.Bluemix_notm}}  para crear una aplicación de fondo móvil o configurar una existente. 
  - Puede seleccionar MobileFirst Services Starter en el catálogo de Bluemix.
  - O bien puede enlazar el servicio a una aplicación existente y configurarla. 

   Cuando utilice MobileFirst Services Starter, obtendrá una instancia de un tiempo de ejecución Node.js que se ejecuta en IBM {{site.data.keyword.Bluemix_notm}} para implementar la lógica del programa de fondo móvil. Un conjunto de servicios móviles principales que proporcionan seguridad, datos, envíos por push y funciones de supervisión están enlazados a esa app Node.js. Tras crear la app Node.js de {{site.data.keyword.Bluemix_notm}}, puede configurar el entorno de desarrollo y empezar a utilizar los SDK de {{site.data.keyword.Bluemix_notm}} Mobile Services. Puede utilizar los SDK para acceder a los servicios que están enlazados a la app de nube con sencillas llamadas API.
   
  
1. Recursos seguros del lado del servidor.

   Proteja los recursos del programa de fondo móvil que se estén ejecutando en los tiempos de ejecución Node.js o Liberty for Java&trade; con la seguridad OAuth habilitada para móvil. Para obtener más información, consulte [Protección de recursos](protecting-resources.html).
   Para obtener más información sobre la aplicación de fondo móvil predeterminada, consulte [bms-hellotodo-strongloop](https://github.com/ibm-bluemix-mobile-services/bms-hellotodo-strongloop).

1. Configure su entorno de desarrollo de cliente {{site.data.keyword.amashort}} principal. 

   Puede añadir el SDK de {{site.data.keyword.amashort}} a la app Android, Cordova o iOS existente. También puede descargar la aplicación de ejemplo HelloAuthentication.
   * **Android**: ([Configuración del SDK de Android](getting-started-android.html)) ([Ejemplo](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication))
  
   * **Cordova**: ([Configuración del plugin de Cordova](getting-started-cordova.html)) ([Ejemplo](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloauthentication))
  
   * **iOS (SDK de Swift)**: ([Configuración del SDK de Swift para iOS](getting-started-ios-swift-sdk.html))
      ([Ejemplo](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication))
  
   * **iOS (SDK de Objective-C)**: ([Configuración del SDK de Object-C para iOS](getting-started-ios.html)) ([Ejemplo](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication))
   
   **Nota:** si bien el SDK de Objective-C sigue recibiendo total soporte y sigue considerándose el SDK principal para Bluemix Mobile Services, está previsto dejar de utilizar este SDK dentro de unos meses en favor del nuevo SDK de Swift. Si crea una aplicación, se recomienda utilizar el SDK de Swift (consulte [Configuración del SDK de Swift para iOS](getting-started-ios-swift-sdk.html)).

1. **Opcional:** configure un proveedor de identidad para su aplicación. Puede configurar un proveedor de identidad por aplicación. La configuración de un proveedor de identidad permite que los usuarios de la app para móvil puedan iniciar sesión con su cuenta de Facebook o Google+. También puede definir cómo deben iniciar sesión los usuarios creando una autenticación personalizada.
   * [Autenticación de usuarios con las credenciales de Facebook](facebook-auth-overview.html)
   * [Autenticación de usuarios con las credenciales de Google](google-auth-overview.html)
   * [Autenticación de usuarios con un proveedor de identidades personalizadas](custom-auth.html)

1. Configure la supervisión y el registro de la app.

    Para obtener más información, consulte [Supervisión de apps](app-monitoring.html).

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
