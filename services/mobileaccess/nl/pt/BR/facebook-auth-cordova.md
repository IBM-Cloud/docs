---

copyright:
  years: 2015, 2016 lastupdated: "2016-10-02"
---
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Ativando a autenticação do Facebook para apps Cordova
{: #facebook-auth-cordova}


Para configurar aplicativos {{site.data.keyword.amafull}} Cordova para
integração de autenticação do Facebook, faça mudanças no código nativo do aplicativo
Cordova, em Java, Objective-C ou Swift. Configure cada plataforma separadamente. Esse aplicativo Cordova já deve estar instrumentado com o {{site.data.keyword.amashort}} SDK. 


Use o ambiente de desenvolvimento nativo para fazer mudanças no código nativo, por exemplo, no Android Studio ou no Xcode.
{:shortdesc}

## Antes de Começar
{: #facebook-auth-before}
Você deve ter:
* Um projeto do Cordova que seja instrumentado com o SDK do cliente {{site.data.keyword.amashort}}. Veja
[Configurando o plug-in do Cordova](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html).
* Uma instância de um aplicativo {{site.data.keyword.Bluemix_notm}} que seja protegida pelo serviço {{site.data.keyword.amashort}}. Para obter mais informações sobre como criar um aplicativo backend do {{site.data.keyword.Bluemix_notm}}, consulte [Introdução](index.html).
* Um ID do app Facebook. Para obter mais informações, veja
[Obtendo um ID do app Facebook a partir do Portal do desenvolvedor do Facebook](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID).



## Configurando a plataforma Android
{: #facebook-auth-cordova-android}

As etapas necessárias para configurar a plataforma Android de um aplicativo Cordova para integração da autenticação do Facebook são muito semelhantes às etapas necessárias para aplicativos Android nativos. Para obter mais informações, veja [Ativando a autenticação do Facebook em apps Android](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-android.html). Execute as etapas a seguir:

* Configurando o aplicativo Facebook para a plataforma Android
* Configurando o {{site.data.keyword.amashort}} para autenticação do Facebook

### Configurando o {{site.data.keyword.amashort}} client SDK para Android

Configure o SDK do cliente {{site.data.keyword.amashort}} para Android
dentro do aplicativo Cordova.

1. Na pasta do projeto Android, abra o arquivo `build.gradle`
para o módulo do aplicativo (**não** o arquivo
`build.gradle` do projeto). Localize a seção de dependências e inclua
uma nova dependência de compilação para o SDK do cliente:

	```Gradle
	dependencies {
     		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
     		name:'facebookauthentication',
     		version: '1.+',
     		ext: 'aar',
     		transitive: true
     		// other dependencies  
		 }
	```
	
2. Sincronize seu projeto com o Gradle clicando em **Ferramentas > Android > Sincronizar projeto com arquivos Gradle**.

3. Abra o arquivo `android/res/values/strings.xml` e inclua uma sequência `facebook_app_id` que contenha o seu ID do app
Facebook.

	```XML
	<resources>
		<string name="app_name">HelloCordova</string>
		<string name="launcher_name">@string/app_name</string>
		<string name="activity_name">@string/launcher_name</string>
		<string name="facebook_app_id">522733366802111</string>
	</resources>
	```
	
4. No arquivo `AndroidManifest.xml` do seu projeto Android
(`android/manifests/AndroidManifest.xml`):

	* Inclua metadados necessários para o Facebook SDK no elemento <application>:

	```XML
	<application .......>
	
	  <meta-data
			android:name="com.facebook.sdk.ApplicationId"
			android:value="@string/facebook_app_id"/>
	
	  <activity ...../>
		<activity ...../>
	</application>
	```

	* Inclua um elemento de Atividade do Facebook sob as atividades existentes:

	```XML
	<application .....>
		<activity ...../>
		<activity ...../>
	
		<activity   android:name="com.facebook.FacebookActivity"
	              android:configChanges="keyboard|keyboardHidden|screenLayout|screenSize|orientation"
	              android:theme="@android:style/Theme.Translucent.NoTitleBar"
	              android:label="@string/app_name" 
			    />
	</application>
	```

2. Para aplicativos Cordova, inicialize o SDK do cliente {{site.data.keyword.amashort}} em seu código JavaScript em vez de no código Java. A API `FacebookAuthenticationManager` ainda deve ser registrada em seu código nativo. Inclua
este código no método `onCreate` de atividade principal:  

	```Java
	FacebookAuthenticationManager.getInstance().registerDefaultAuthenticationListener(this);
	```

6. Inclua o código a seguir em sua Atividade:

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
	      super.onActivityResult(requestCode, resultCode, data);
		FacebookAuthenticationManager.getInstance()
	          .onActivityResultCalled(requestCode, resultCode, data);
	}
	```

## Configurando a plataforma iOS
{: #facebook-auth-cordova-ios}

As etapas necessárias para configurar a plataforma iOS do aplicativo Cordova para integração da autenticação do Facebook são semelhantes às etapas necessárias para aplicativos iOS nativos. A principal diferença é que o Cordova CLI atualmente não suporta o gerenciador de dependência CocoaPods. Deve-se incluir manualmente arquivos que sejam necessários para integração à autenticação do Facebook. Para obter mais informações, veja [Ativando a autenticação do Facebook em apps iOS](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html). Execute as etapas a seguir:

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

1. Clique na raiz do projeto em Xcode e selecione **Fases da construção**.

1. Inclua o arquivo `FacebookSDK.framework` na lista de
bibliotecas vinculadas em **Vincular binário com bibliotecas**.

 Veja
[Configurando
a plataforma iOS para autenticação do Facebook](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-ios.html). Registre a API IMFFacebookAuthenticationHandler em código nativo conforme descrito na seção Inicializando o {{site.data.keyword.amashort}} client SDK. Não inicialize IMFClient em seu código nativo.

Inclua a linha a seguir no método `application:openURL:sourceApplication:annotation` de delegado do seu aplicativo. Esse
código assegura que todos os plug-ins do Cordova sejam notificados dos respectivos eventos.

```
[[ NSNotificationCenter defaultCenter] postNotification:
		[NSNotification notificationWithName:CDVPluginHandleOpenURLNotification object:url]];      
```
{: codeblock}

## Inicializando o {{site.data.keyword.amashort}} client SDK
{: #facebook-auth-cordova-init}

Use o código JavaScript a seguir em seu aplicativo Cordova para inicializar o {{site.data.keyword.amashort}} client SDK.

```JavaScript
BMSClient.initialize("applicationRoute", "applicationGUID");
```
{: codeblock}

Substitua `applicationRoute` e
`applicationGUID` pelos valores obtidos para
**Route** e **App GUID** em **Opções
móveis**.
	



##Inicializando o {{site.data.keyword.amashort}} AuthorizationManager
Use o código JavaScript a seguir no aplicativo Cordova para inicializar o
{{site.data.keyword.amashort}} AuthorizationManager.
```JavaScript
  MFPAuthorizationManager.initialize("tenantId");
```
{: codeblock}

Substitua o valor `tenantId` pelo `tenantId` do serviço
{{site.data.keyword.amashort}}. Esse valor você obtém clicando no botão
**Mostrar credenciais** no quadro do serviço
{{site.data.keyword.amashort}}.



## Testando a Autenticação
{: #facebook-auth-cordova-test}
Após o SDK do cliente ser inicializado e o gerenciador de autenticação do Facebook ser registrado, é possível começar a fazer solicitações para o aplicativo backend móvel.

### Antes de Começar
Deve-se estar usando o modelo do {{site.data.keyword.mobilefirstbp}} e já ter um recurso protegido pelo {{site.data.keyword.amashort}} no terminal `/protected`. Para obter mais informações, veja [Protegendo recursos](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

1. Tente enviar uma solicitação para o terminal protegido do seu aplicativo backend móvel recém-criado a partir do seu navegador. Abra a URL a seguir: `{applicationRoute}/protected`. Por exemplo: `http://my-mobile-backend.mybluemix.net/protected`
<br/>O terminal `/protected` de um aplicativo backend móvel que foi criado com o modelo MobileFirst Services Starter é
protegido com {{site.data.keyword.amashort}}. Uma mensagem `Unauthorized` é retornada no navegador. Essa mensagem é retornada porque esse terminal só pode ser acessado por aplicativos móveis instrumentados com o {{site.data.keyword.amashort}} client SDK.

1. Use seu aplicativo Cordova para fazer solicitação para o mesmo terminal. Inclua o código a seguir depois de inicializar `BMSClient`:

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error){
    	console.log("failure", error);
    }
	var request = new MFPRequest("/protected", MFPRequest.GET);
	request.send(success, failure);
	```
{: codeblock}

1. Execute o aplicativo. Uma tela de login do Facebook é exibida:

	![image](images/android-facebook-login.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;	![image](images/ios-facebook-login.png)

	Essa tela pode parecer ligeiramente diferente se você não tiver o app Facebook instalado em seu dispositivo ou se não estiver com login efetuado atualmente no Facebook.

1. Clique em **OK** para autorizar o {{site.data.keyword.amashort}} a usar sua identidade de usuário do Facebook para propósitos de autenticação.

1. 	Quando sua solicitação for bem-sucedida, a saída a seguir estará no console do
utilitário LogCat ou do Xcode:

	![Mensagem de êxito de autenticação do Facebook para Android](images/android-facebook-login-success.png)

	![Mensagem de êxito de autenticação do Facebook para iOS](images/ios-facebook-login-success.png)
