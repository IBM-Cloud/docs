---

copyright:
  years: 2015, 2016

---
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Ativando a autenticação do Facebook para apps Cordova
{: #facebook-auth-cordova}

*Última atualização: 15 de junho de 2016*
{: .last-updated}


Para configurar aplicativos Cordova para integração da autenticação do Facebook, deve-se fazer mudanças no código nativo do aplicativo Cordova, em Java, Objective-C ou Swift. Configure cada plataforma separadamente. Esse aplicativo Cordova já deve estar instrumentado com o {{site.data.keyword.amashort}} SDK. 


Use o ambiente de desenvolvimento nativo para fazer mudanças no código nativo, por exemplo, no Android Studio ou no Xcode.
{:shortdesc}

## Antes de Começar
{: #facebook-auth-before}
Você deve ter:
* Um projeto do Cordova que seja instrumentado com o {{site.data.keyword.amashort}} client SDK. Consulte [Configurando o plug-in do Cordova](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html).
* Uma instância de um aplicativo {{site.data.keyword.Bluemix_notm}} que seja protegida pelo serviço {{site.data.keyword.amashort}}. Para obter mais informações sobre como criar um backend {{site.data.keyword.Bluemix_notm}, consulte [Introdução](index.html).
* Um ID de aplicativo do Facebook. Para obter mais informações, consulte [Obtendo um ID do aplicativo Facebook do Portal do Desenvolvedor do Facebook](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID).



## Configurando a plataforma Android
{: #facebook-auth-cordova-android}

As etapas necessárias para configurar a plataforma Android de um aplicativo Cordova para integração da autenticação do Facebook são muito semelhantes às etapas necessárias para aplicativos Android nativos. Para obter mais informações, consulte [Ativando a autenticação do Facebook em apps Android](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-android.html). Execute as etapas a seguir:

* Configurando o aplicativo Facebook para a plataforma Android
* Configurando o {{site.data.keyword.amashort}} para autenticação do Facebook
* Configurando o {{site.data.keyword.amashort}} client SDK para Android

A única diferença quando você estiver configurando aplicativos Cordova é que deve-se inicializar o {{site.data.keyword.amashort}} client SDK em seu código JavaScript em vez de no código Java (consulte [Testando a autenticação](#facebook-auth-cordova-test)). A API `FacebookAuthenticationManager` ainda deve ser registrada em seu código nativo.

## Configurando a plataforma iOS
{: #facebook-auth-cordova-ios}

As etapas necessárias para configurar a plataforma iOS do aplicativo Cordova para integração da autenticação do Facebook são semelhantes às etapas necessárias para aplicativos iOS nativos. A principal diferença é que o Cordova CLI atualmente não suporta o gerenciador de dependência CocoaPods. Deve-se incluir manualmente arquivos que sejam necessários para integração à autenticação do Facebook. Para obter mais informações, consulte [Ativando a autenticação do Facebook em apps iOS](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html). Execute as etapas a seguir:

* Configurando o aplicativo Facebook para a plataforma iOS
* Configurando o {{site.data.keyword.amashort}} para autenticação do Facebook

### Instalando manualmente o {{site.data.keyword.amashort}} SDK para autenticação do Facebook e Facebook SDK
{: #facebook-auth-cordova-ios-sdk}
1. Faça download do archive que contém o [{{site.data.keyword.Bluemix_notm}} Mobile Services SDK para iOS](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master).

1. Acesse o diretório `Sources/Authenticators/IMFFacebookAuthentication` e copie (arraste e solte) todos os arquivos para o projeto do iOS no Xcode. Copie os seguintes arquivos:
  * IMFDefaultFacebookAuthenticationDelegate.h
  * IMFDefaultFacebookAuthenticationDelegate.m
  * IMFFacebookAuthenticationDelegate.h
  * IMFFacebookAuthenticationHandler.h
  * IMFFacebookAuthenticationHandler.m

	Quando solicitado pelo Xcode, selecione **Copiar arquivos...**.

1. Faça download e instale o [Facebook SDK v3.19](https://developers.facebook.com/resources/facebook-ios-sdk-3.19.pkg).

1. O Facebook SDK será instalado no diretório `~/Documents/FacebookSDK`. Navegue até esse diretório e copie (arraste e solte) o arquivo `FacebookSDK.framework` para o projeto do iOS no Xcode.

1. 	Clique na raiz do projeto na área de janela esquerda de Xcode e selecione **Fases da compilação**.

1. Inclua o arquivo `FacebookSDK.framework` na lista de
bibliotecas vinculadas em **Vincular binário com bibliotecas**.

 Consulte
[Configurando
a plataforma iOS para autenticação do Facebook](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html). Registre a API IMFFacebookAuthenticationHandler em código nativo conforme descrito na seção Inicializando o {{site.data.keyword.amashort}} client SDK. Não inicialize IMFClient em seu código nativo.

Inclua a linha a seguir no método `application:openURL:sourceApplication:annotation` de delegado do seu aplicativo. Esse
código assegura que todos os plug-ins do Cordova sejam notificados dos respectivos eventos.

```
[[ NSNotificationCenter defaultCenter] postNotification:
		[NSNotification notificationWithName:CDVPluginHandleOpenURLNotification object:url]];      
```

## Inicializando o {{site.data.keyword.amashort}} client SDK
{: #facebook-auth-cordova-init}

Use o código JavaScript a seguir em seu aplicativo Cordova para inicializar o {{site.data.keyword.amashort}} client SDK.

```JavaScript
BMSClient.initialize("applicationRoute", "applicationGUID");
```

Substitua *applicationRoute* e *applicationGUID* pelos
valores obtidos para **Rota** e **GUID do app** das
**Opções móveis**.

## Testando a Autenticação
{: #facebook-auth-cordova-test}
Depois que o client SDK for inicializado e o Gerenciador de autenticação do Facebook for registrado, será possível começar a fazer solicitações ao seu backend móvel.

### Antes de Começar
Deve-se estar usando o modelo do {{site.data.keyword.mobilefirstbp}} e já ter um recurso protegido pelo {{site.data.keyword.amashort}} no terminal `/protected`. Para obter mais informações, consulte [Protegendo recursos](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

1. Tente enviar uma solicitação para o terminal protegido de seu backend móvel recém-criado em seu navegador. Abra a URL a seguir: `{applicationRoute}/protected`. Por exemplo: `http://my-mobile-backend.mybluemix.net/protected`
<br/>O terminal `/protected` de um backend móvel criado com o modelo MobileFirst Services Starter está protegido com o {{site.data.keyword.amashort}}. Uma mensagem `Unauthorized` é retornada no navegador. Essa mensagem é retornada porque esse terminal só pode ser acessado por aplicativos móveis instrumentados com o {{site.data.keyword.amashort}} client SDK.

1. Use seu aplicativo Cordova para fazer solicitação para o mesmo terminal. Inclua o código abaixo depois de inicializar `BMSClient`:

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error)
    	{console.log("failure", error);
    }
	var request = new MFPRequest("/protected", MFPRequest.GET);
	request.send(success, failure);
	```

1. Execute o aplicativo. Uma tela de Login do Facebook é exibida como pop-up:

	![image](images/android-facebook-login.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	![image](images/ios-facebook-login.png)

	> Essa tela poderá parecer um pouco diferente se o app Facebook não estiver instalado em seu dispositivo, ou se você não estiver atualmente conectado ao Facebook.

1. Clique em **OK** para autorizar o {{site.data.keyword.amashort}} a usar sua identidade de usuário do Facebook para propósitos de autenticação.

1. 	Quando sua solicitação for bem-sucedida, a saída a seguir estará no console do
utilitário LogCat ou do Xcode:

	![Mensagem de êxito de autenticação do Facebook para Android](images/android-facebook-login-success.png)

	![Mensagem de êxito de autenticação do Facebook para iOS](images/ios-facebook-login-success.png)
