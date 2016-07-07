---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Introdução ao
{{site.data.keyword.amashort}}
{: #gettingstarted}
*Última atualização: 15 de junho de 2016*
{: .last-updated}

Inclua a funcionalidade de segurança em seu app móvel com o serviço {{site.data.keyword.amafull}}. É possível configurar a autenticação de cliente e
os provedores de identidade para que os usuários possam efetuar login no app com suas
contas existentes do Google ou Facebook.
{:shortdesc}

**Nota:** O serviço {{site.data.keyword.amashort}} era
conhecido anteriormente como Advanced Mobile Access.


Para ativação e execução do serviço {{site.data.keyword.amashort}}, siga
estas etapas:

1.  Use o painel do {{site.data.keyword.Bluemix_notm}} para criar um aplicativo backend móvel ou configure um existente.
  - É possível selecionar o MobileFirst Services Starter no catálogo do Bluemix.
  - Ou é possível ligar o serviço a um aplicativo existente e configurá-lo.

   Ao usar o MobileFirst Services Starter, você obtém uma instância de um tempo de execução do Node.js que é executada no IBM {{site.data.keyword.Bluemix_notm}} para implementar sua lógica de backend customizada. Um conjunto de serviços móveis principais que fornecem funções de segurança, dados, push e monitoramento está ligado a esse app Node.js. Depois que o {{site.data.keyword.Bluemix_notm}} Node.js for criado, é possível configurar seu ambiente de desenvolvimento e começar a usar os SDKs de serviços móveis do {{site.data.keyword.Bluemix_notm}}. É possível usar os SDKs para acessar os serviços que estão ligados ao seu app em nuvem com chamadas API simples.
   
  
1. Recursos seguros do lado do servidor.

   Proteja seus recursos de backend móvel que estão em execução nos tempos de execução do Node.js ou do Liberty for Java&trade; com a segurança do OAuth ativada para dispositivo móvel. Para obter mais informações, consulte [Protegendo recursos](protecting-resources.html).
   Para saber mais sobre o aplicativo backend móvel padrão, consulte [bms-hellotodo-strongloop](https://github.com/ibm-bluemix-mobile-services/bms-hellotodo-strongloop).

1. Configure seu ambiente de desenvolvimento do lado do cliente principal do {{site.data.keyword.amashort}}.

   É possível incluir o
{{site.data.keyword.amashort}} SDK em seu app Android, Cordova ou iOS existente. É
possível também fazer download do aplicativo de amostra HelloAuthentication.
   * **Android**: ([Configurando o Android SDK](getting-started-android.html)) ([Amostra](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication))
  
   * **Cordova**: ([Configurando o plug-in do Cordova](getting-started-cordova.html)) ([Amostra](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloauthentication))
  
   * **iOS (Swift SDK)**: ([Configurando o iOS Swift SDK](getting-started-ios-swift-sdk.html)) ([Amostra](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication))
  
   * **iOS (Objective-C SDK)**: ([Configurando o iOS Object-C SDK](getting-started-ios.html)) ([Amostra](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloauthentication))
   
   **Nota:** embora o Objective-C SDK permaneça totalmente suportado e ainda seja considerado o SDK primário para o Bluemix Mobile Services, há planos para descontinuar esse SDK posteriormente este ano em favor do novo Swift SDK. Se você estiver criando um aplicativo, é altamente recomendável usar o Swift SDK (consulte [Configurando o iOS Swift SDK](getting-started-ios-swift-sdk.html)).

1. **Opcional:** configure um provedor de identidade para seu aplicativo. É possível configurar um provedor de identidade por aplicativo. A configuração de um provedor de identidade permite que os usuários do seu app móvel efetuem login com suas contas existentes do Facebook ou Google+. Ou é possível definir como os usuários efetuam login criando uma autenticação customizada.
   * [Autenticando usuários com as credenciais do Facebook](facebook-auth-overview.html)
   * [Autenticando usuários com as credenciais do Google](google-auth-overview.html)
   * [Autenticando usuários com um provedor de identidade customizado](custom-auth.html)

1. Configure o monitoramento e a criação de log do app.

    Para obter mais informações, consulte [Monitorando apps](app-monitoring.html).

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
* [Core SDK (iOS - Objective-C - descontinuado) ](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master){: new_window}
* [Autenticação customizada - amostra simples](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample){: new_window}
* [Autenticação customizada - amostra avançada](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management){: new_window}

## Referência de API
{: api}
* [Android](https://console.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html){: new_window}
* [iOS (Objective-C SDK) - descontinuado](https://console.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html){: new_window}


## Links relacionados
{: #general}
* [Visão geral](overview.html){: new_window}
