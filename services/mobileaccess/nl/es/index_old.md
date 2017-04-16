---

copyright:
  years: 2015, 2016
  
---

{:shortdesc: .shortdesc}

# Iniciación a {{site.data.keyword.amashort}}
{: #getting-started}

El servicio de {{site.data.keyword.amafull}} le proporciona funcionalidades de seguridad y supervisión para la aplicación móvil. También puede configurar la autenticación de cliente y los proveedores de identidad. También puede añadir funciones de supervisión a la app, los cuales habilitan los registros clientes y las estadísticas de uso.

Nota: el servicio {{site.data.keyword.amashort}} se conocía anteriormente como Advanced Mobile Access.
{: shortdesc}

1. Configure un programa de fondo móvil en Bluemix y configure el SDK en su app para móvil. Para obtener más información, consulte
[Guía de inicio](getting-started.html).
1. Recursos seguros del lado del servidor. Proteja los recursos del programa de fondo móvil que se estén ejecutando en los tiempos de ejecución Node.js o Liberty for Java&trade; con la seguridad OAuth habilitada para móvil. Para obtener más información, consulte [Protección de recursos](protecting-resources.html).
1. Opcional: configura un proveedor de identidad para la aplicación. Puede configurar un proveedor de identidad por aplicación. La configuración de un proveedor de identidad permite que los usuarios de la app para móvil puedan iniciar sesión con su cuenta de Facebook o Google+. También puede definir cómo deben iniciar sesión los usuarios creando una autenticación personalizada.
   * [Facebook](facebook-auth-overview.html)
   * [Google](google-auth-overview.html)
   * [Personalizada](custom-auth.html)
1. Configure la supervisión y el registro de la app.  Para obtener más información, consulte [Supervisión de la app](app-monitoring.html).


># Enlaces relacionados {:class="linklist"}
>## Guías de aprendizaje y ejemplos {:id="samples"}
>* [android-helloauthentication](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication)
>* [ios-helloauthentication](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication)
>
># Enlaces relacionados {:class="linklist"}
>## Referencia de API{:id="api"}
>* [Referencia de la API Core (Android)](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)
>* [Referencia de la API Core (iOS)](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)
>
># Enlaces relacionados {:class="linklist"}
>## SDK {:id="sdk"}
>* [Core SDK (iOS) ](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master)  
>* [bms-clientsdk-android-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)
>* [bms-clientsdk-cordova-plugin-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core)
>
>{:elementKind="article" id="rellinks"}
