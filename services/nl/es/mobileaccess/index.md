---

copyright:
  años: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Iniciación a {{site.data.keyword.amashort}}
{: #gettingstarted}
*Última actualización: 21 Marzo de 2016*

Añada funciones de seguridad y supervisión a la app para móvil con el servicio {{site.data.keyword.amafull}}. Puede configurar la autenticación de cliente y los proveedores de identidad de modo que los usuarios puedan iniciar una sesión en la app con sus cuentas existentes de Google o Facebook. También puede añadir funciones de supervisión a la app, los cuales habilitan los registros clientes y las estadísticas de uso.
{:shortdesc}

**Note:**: el servicio {{site.data.keyword.amashort}} se conocía anteriormente como Advanced Mobile Access.


Para comenzar a utilizar el servicio {{site.data.keyword.amashort}}, siga estos pasos:

1. Configure el entorno de desarrollo del cliente.
Puede añadir el SDK de {{site.data.keyword.amashort}} a la app Android, Cordova o iOS existente. También puede descargar la aplicación de ejemplo HelloAuthentication.
   * **Android**: ([SDK](getting-started-android.html)) ([Ejemplo](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication))
   * **Cordova**: ([SDK](getting-started-cordova.html)) ([Ejemplo](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloauthentication))
   * **iOS (SDK de Swift-C)**: ([SDK](getting-started-ios-swift-sdk.html)) ([Ejemplo](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication))
   * **iOS (SDK de Objective-C)**: ([SDK](getting-started-ios.html)) ([Ejemplo](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication))

1. Recursos seguros del lado del servidor. Proteja los recursos del programa de fondo móvil que se estén ejecutando en los tiempos de ejecución Node.js o Liberty for Java&trade; con la seguridad OAuth habilitada para móvil. Para obtener más información, consulte [Protección de recursos](protecting-resources.html).

1. Opcional: configura un proveedor de identidad para la aplicación. Puede configurar un proveedor de identidad por aplicación. La configuración de un proveedor de identidad permite que los usuarios de la app para móvil puedan iniciar sesión con su cuenta de Facebook o Google+. También puede definir cómo deben iniciar sesión los usuarios creando una autenticación personalizada.
   * [Facebook](facebook-auth-overview.html)
   * [Google](google-auth-overview.html)
   * [Personalizada](custom-auth.html)

1. Configure la supervisión y el registro de la app.  Para obtener más información, consulte [Supervisión de la app](app-monitoring.html).

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
* [Core SDK (iOS - Objective-C) ](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master){: new_window}
* [Autenticación personalizada: ejemplo simple](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample){: new_window}
* [Autenticación personalizada: ejemplo avanzado](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management){: new_window}

## Referencia de API
{: api}
* [Android](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html){: new_window}
* [iOS (SDK de Objective-C)](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html){: new_window}


## Enlaces relacionados
{: #general}
* [Visión general](overview.html){: new_window}
