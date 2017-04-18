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

# Introdução ao
{{site.data.keyword.amashort}}
{: #gettingstarted}

Inclua segurança em seu app móvel com o serviço {{site.data.keyword.amafull}}. É possível configurar a autorização do cliente para acessar recursos de
backend protegidos em execução no {{site.data.keyword.Bluemix}}. Use provedores de identidade (Google e Facebook) ou identidades
customizadas para autenticar usuários e conceder acesso a
recursos backend protegidos e apps da web.
{:shortdesc}

**Nota:** O serviço {{site.data.keyword.amashort}} era
conhecido anteriormente como Advanced Mobile Access.


Para fazer com que o serviço {{site.data.keyword.amashort}} funcione:

1. Use uma das opções a seguir para criar um limite ou um
serviço desvinculado:
 * Crie um aplicativo usando o modelo do
{{site.data.keyword.Bluemix_notm}}
**MobileFirst Services Starter** no catálogo. Isso cria um limite de serviço
{{site.data.keyword.amashort}}
para um aplicativo backend
{{site.data.keyword.Bluemix_notm}}.
 * Crie um serviço {{site.data.keyword.amashort}} usando o console do  {{site.data.keyword.amashort}}. É possível vincular o serviço a um aplicativo backend e configurá-lo no console do {{site.data.keyword.amashort}}.

   Ao usar o MobileFirst Services Starter, você obtém uma instância de um tempo de execução do Node.js que é executada no IBM {{site.data.keyword.Bluemix_notm}} para implementar sua lógica de backend customizada. Um conjunto de serviços móveis principais que fornece segurança, dados, push e funções de
monitoramento está vinculado a esse app Node.js. Após o app Node.js do {{site.data.keyword.Bluemix_notm}} ser criado, será possível configurar seu ambiente de desenvolvimento e iniciar o uso dos SDKs do {{site.data.keyword.Bluemix_notm}} Mobile Services. É possível usar os SDKs para acessar os serviços que estão ligados ao seu app em nuvem com chamadas API simples.

	Para obter mais informações sobre como criar e trabalhar com projetos, aplicativos e
serviços, veja o [Painel móvel do IBM Bluemix](https://console.{DomainName}/docs/mobile/index.html).

2. Recursos seguros do lado do servidor.

   Proteja seus recursos de backend móveis que estejam em execução nos tempos de execução Node.js ou Liberty for Java&trade; com a segurança OAuth ativada para dispositivo móvel. Para obter mais informações, veja [Protegendo recursos](protecting-resources.html).
   Para saber mais sobre o aplicativo backend móvel padrão, veja o aplicativo de amostra
[bms-hellotodo-strongloop ![ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-bluemix-mobile-services/bms-hellotodo-strongloop "Ícone de link externo"){: new_window}.

3. Configure seu ambiente de desenvolvimento principal do {{site.data.keyword.amashort}}.

  ####Desenvolvimento do Cliente
  {: #client-development}

	É possível incluir o {{site.data.keyword.amashort}} SDK no app Android, iOS ou Cordova existente, como a seguir:
   * Android: ([configurando o Android SDK](getting-started-android.html)) [Amostra ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication "Ícone de link externo"){: new_window}
    * iOS (Swift SDK): ([configurando o iOS Swift SDK](getting-started-ios-swift-sdk.html)) [Amostra ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication "Ícone de link externo"){: new_window}    
   * Cordova: ([configurando o plug-in do Cordova](getting-started-cordova.html)) [Amostra ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-bluemix-mobile-services/bms-samples-cordova-helloauthentication "Ícone de link externo"){: new_window}


 ####Desenvolvimento da Web
 {: #web-development}

   O serviço {{site.data.keyword.amashort}} pode
proteger seu aplicativo da web, não requerendo SDK especial. É possível alavancar diferentes provedores de identidade, além da proteção fornecida pelo serviço {{site.data.keyword.amashort}}. A integração do {{site.data.keyword.amashort}} permite que qualquer aplicativo da web, independentemente da tecnologia que ele implementa, aproveite o protocolo OAuth2. Para obter informações sobre como configurar seu
{{site.data.keyword.amashort}} aplicativo da web para
acessar o serviço {{site.data.keyword.amashort}} usando
diferentes provedores de identidade, consulte:

   * [Ativando a
autenticação do Facebook para aplicativos da web](facebook-auth-web.html)
   * [Ativando a
autenticação do Google para aplicativos da web](google-auth-web.html)
   * [Ativando a
autenticação customizada para aplicativos da web](custom-auth-web.html)

**Opcional:** configure um provedor de identidade para seu aplicativo. É possível configurar um provedor de identidade por aplicativo. A configuração de um provedor de identidade permite que os usuários do seu app móvel efetuem login com suas contas existentes do Facebook ou Google+. Ou é possível definir como os usuários efetuam login criando uma autenticação customizada.
   * [Autenticando usuários com as credenciais do Facebook](facebook-auth-overview.html)
   * [Autenticando usuários com as credenciais do Google](google-auth-overview.html)
   * [Autenticando usuários com um provedor de identidade customizado](custom-auth.html)

## Tutoriais e amostras
{: #samples}

* [Amostra android-helloauthentication ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloauthentication "Ícone de link externo"){: new_window}
* [Amostra ios-helloauthentication (Swift SDK) ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication "Ícone de link externo"){: new_window}

## SDK
{: #sdk}

* [Core SDK (Android) ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core "Ícone de link externo"){: new_window}

* [Amostra ios-helloauthentication (Swift SDK) ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-helloauthentication "Ícone de link externo"){: new_window}

* [Autenticação customizada - amostra simples ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample "Ícone de link externo"){: new_window}

* [Autenticação customizada - amostra avançada ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management "Ícone de link externo"){: new_window}


