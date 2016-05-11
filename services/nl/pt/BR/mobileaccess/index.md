---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Introdução ao
{{site.data.keyword.amashort}}
{: #gettingstarted}
*Última atualização: 21 de março de 2016*

Inclua a funcionalidade de segurança e monitoramento em seu app móvel com o serviço
{{site.data.keyword.amafull}}. É possível configurar a autenticação de cliente e
os provedores de identidade para que os usuários possam efetuar login no app com suas
contas existentes do Google ou Facebook. Também é possível incluir função de monitoramento no app,
permitindo criação de log e estatísticas de uso do cliente.
{:shortdesc}

**Nota:** O serviço {{site.data.keyword.amashort}} era
conhecido anteriormente como Advanced Mobile Access.


Para ativação e execução do serviço {{site.data.keyword.amashort}}, siga
estas etapas:

1. Configure o ambiente de desenvolvimento no lado do cliente.
É possível incluir o
{{site.data.keyword.amashort}} SDK em seu app Android, Cordova ou iOS existente. É
possível também fazer download do aplicativo de amostra HelloAuthentication.
   * **Android**: ([SDK](getting-started-android.html)) ([Amostra](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication))
   * **Cordova**: ([SDK](getting-started-cordova.html)) ([Amostra](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloauthentication))
   * **iOS (Swift-C SDK)**: ([SDK](getting-started-ios-swift-sdk.html)) ([Amostra](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication))
   * **iOS (Objective-C SDK)**: ([SDK](getting-started-ios.html)) ([Amostra](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication))

1. Recursos seguros do lado do servidor. Proteja seus recursos de backend móvel
que estão em execução nos tempos de execução do Node.js ou Liberty for Java&trade; com a
segurança do OAuth ativada para dispositivo móvel. Para obter mais informações, veja [Protegendo recursos](protecting-resources.html).

1. Opcional: configure um provedor de identidade para seu aplicativo. É possível configurar um provedor de identidade por aplicativo. A configuração de um provedor de identidade permite que os usuários do seu app móvel efetuem login com suas contas existentes do Facebook ou Google+. Ou é possível definir como os usuários efetuam login criando uma autenticação customizada.
   * [Facebook
](facebook-auth-overview.html)
   * [Google](google-auth-overview.html)
   * [Customizado
](custom-auth.html)

1. Configure o monitoramento e a criação de log do app.  Para obter mais informações, veja [Monitoramento de app](app-monitoring.html).

# Links relacionados
{: #rellinks}

## Tutoriais e amostras
{: #samples}
* [Amostra android-helloauthentication](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication){: new_window}
* [Amostra ios-helloauthentication (Swift SDK)](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication){: new_window}
* [Amostra ios-helloauthentication (Objective-C SDK)](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication){: new_window}

## SDK
{: #sdk}
* [Core SDK (Android)](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}
* [Core SDK (plug-in do Cordova)](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}
* [Core SDK (iOS - Swift) ](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window}
* [Core SDK (iOS - Objective-C) ](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master){: new_window}
* [Autenticação customizada - amostra simples](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample){: new_window}
* [Autenticação customizada - amostra avançada](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management){: new_window}

## Referência de API
{: api}
* [Android](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html){: new_window}
* [iOS (Objective-C SDK)](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html){: new_window}


## Links relacionados
{: #general}
* [Visão geral](overview.html){: new_window}
