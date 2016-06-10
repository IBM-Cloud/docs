---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Introdução ao {{site.data.keyword.mobilepushshort}}

{: #gettingstartedtemplate}


{:shortdesc}

O serviço de notificações push fornece uma plataforma unificada para enviar e
gerenciar notificações push móveis que são destinadas a plataformas iOS e Android. Esse serviço gerencia o mapeamento dos usuários de aplicativos para seus dispositivos, plataforma do
dispositivo e manipula o despacho de notificações push para eles. Com esse serviço, é
possível enviar transmissões, unicasts, (com base no deviceID) e também notificações push
de tags (ou tópicos) para seus usuários de aplicativo móvel. É possível também usar um
SDK e [APIs REST](https://mobile.{DomainName}/imfpushrestapidocs/) para
desenvolver melhor seus aplicativos cliente.

Esta
seção descreve como configurar notificações push básicas. Ao usar uma
notificação básica, as notificações são transmitidas em vez de
atingirem um conjunto específico de usuários usando tags.

1. [Configure
credenciais para um provedor de notificação](t__main_push_config_provider.html)
2. [Ative o app móvel para receber
notificações](c_enable_push.html)
3. [Enviar notificações básicas](t_send_push_notifications.html)

# Links relacionados
{: #rellinks}

* [Visão geral](c_overview_push.md){: new_window}

## Tutoriais e Amostras {:id="samples"}
{: #samples}
* [Aplicativo de amostra Android helloPush](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/){: new_window}
- [Aplicativo de amostra Cordova](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-hellopush){: new_window}
* [Aplicativo de amostra iOS helloPush](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-hellopush/){: new_window}

## SDK
{: #sdk}
* [Android SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-push){: new_window}
* [Cordova SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push){: new_window}
* [iOS SDK](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master){: new_window}

## Referência de API
{: #api}
* [Referência de API Push (Android)](https://classicdocs.ng.bluemix.net/docs/api/content/api/mobilefirst/android/push-api-doc/overview-summary.html){: new_window}
* [Referência de API IMFPush (iOS)](https://classicdocs.ng.bluemix.net/docs/api/content/api/mobilefirst/ios/IMFPush_api-doc/html/index.html){: new_window}
* [Referência da API REST
](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window}
