---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Iniciación a {{site.data.keyword.mobilepushshort}}

{: #gettingstartedtemplate}


{:shortdesc}

El servicio de Notificaciones push proporciona una plataforma unificada para enviar y gestionar notificaciones push móviles que están pensadas para plataformas iOS y Android. Este servicio gestiona la correlación de los usuarios de la aplicación a sus dispositivos, plataforma de dispositivo,
        y maneja el envío de notificaciones push a los mismos. Con este servicio, puede enviar difusiones, unicasts (en función del ID de dispositivo) y también notificaciones push (o temas) de etiquetas a los usuarios de la aplicación móvil. También puede utilizar las [API REST](https://mobile.{DomainName}/imfpushrestapidocs/) y SDK para desarrollar más las aplicaciones de cliente.

En esta sección se describe cómo configurar notificaciones push básicas. Al utilizar
      una notificación básica, las notificaciones se difunden en lugar de llegar a un conjunto específico
      de usuarios utilizando etiquetas.

1. [Configurar credenciales para un
              proveedor de notificaciones](t__main_push_config_provider.html)
2. [Habilitar la app para móvil para recibir notificaciones](c_enable_push.html)
3. [Enviar notificaciones básicas](t_send_push_notifications.html)

# Enlaces relacionados
{: #rellinks}

* [Visión general ](c_overview_push.md){: new_window}

## Guías de aprendizaje y ejemplos {:id="samples"}
{: #samples}
* [aplicación de ejemplo helloPush Android](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/){: new_window}
- [aplicación de ejemplo Cordova](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-hellopush){: new_window}
* [aplicación de ejemplo helloPush iOS](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-hellopush/){: new_window}

## SDK
{: #sdk}
* [SDK de Android](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-push){: new_window}
* [SDK de Cordova](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push){: new_window}
* [SDK de iOS](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master){: new_window}

## Referencia de API
{: #api}
* [Referencia de API push (Android)](https://classicdocs.ng.bluemix.net/docs/api/content/api/mobilefirst/android/push-api-doc/overview-summary.html){: new_window}
* [iOS de Referencia de la API IMFPush](https://classicdocs.ng.bluemix.net/docs/api/content/api/mobilefirst/ios/IMFPush_api-doc/html/index.html){: new_window}
* [Referencia API de REST](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window}
