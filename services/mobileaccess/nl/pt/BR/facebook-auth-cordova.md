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


# Ativando a autenticação do Facebook para apps Cordova
{: #facebook-auth-cordova}

Para configurar os aplicativos Cordova {{site.data.keyword.amafull}}
para integração de autenticação do Facebook,
configure cada plataforma separadamente. O aplicativo Cordova já
deve estar instrumentado com o SDK
{{site.data.keyword.amashort}}.

Sua plataforma nativa e o código Cordova WebView
Javascript requerem mudanças para permitir a autenticação do
Facebook.

Use o ambiente de desenvolvimento nativo para fazer mudanças no código nativo, por exemplo, no Android Studio ou no Xcode.
{:shortdesc}

## Antes de Começar
{: #facebook-auth-before}

Você deve ter:
* Um projeto Cordova (Android ou iOS) que seja
instrumentado com o cliente SDK {{site.data.keyword.amashort}}, consulte
[
Configurando o plug-in do Cordova](getting-started-cordova.html#getting-started-cordova-plugin).
* Uma instância de um aplicativo {{site.data.keyword.Bluemix_notm}} que seja protegida pelo serviço {{site.data.keyword.amashort}}. Para obter mais informações sobre como criar um serviço de
backend do {{site.data.keyword.Bluemix_notm}}, consulte
[Introdução](index.html).
* Sua rota do aplicativo. Esta é a URL do seu aplicativo
backend.
* O valor `tenantId`. Abra o painel de
serviço do {{site.data.keyword.amashort}}. Clique em **Opções de dispositivo móvel**. O valor
`tenantId` (também conhecido como
`appGUID`) é exibido no campo **App
GUID / TenantId**. Você precisará desses valores para
inicializar o SDK e para enviar solicitações para o serviço de
backend.
*  Localize a região na qual o seu serviço
{{site.data.keyword.Bluemix_notm}} está
hospedado. É possível encontrar a sua região atual
{{site.data.keyword.Bluemix_notm}} no cabeçalho,
próximo ao ícone **Avatar**
![ícone de avatar
](images/face.jpg "ícone de avatar") na barra de menus. O valor da região deve ser um destes: US South, Sydney ou UK. Os valores constantes de
SDK exatos que correspondem a esses nomes são indicados nos exemplos de código.
* Um aplicativo do Facebook e um ID do app. Para obter mais informações, veja [Obtendo um ID do app Facebook no
Portal do Desenvolvedor do Facebook](facebook-auth-overview.html#facebook-appID).



## Configurando a plataforma Android
{: #facebook-auth-cordova-android}

As etapas necessárias para configurar a plataforma Android
de um aplicativo Cordova para integração da autenticação do
Facebook são muito semelhantes às etapas necessárias para
aplicativos Android nativos. Para obter mais informações, consulte [Ativando a autenticação do Facebook em apps Android](facebook-auth-android.html). Execute as etapas a seguir:

* [Configurando
seu aplicativo Facebook para a plataforma Android](facebook-auth-android.html#facebook-auth-android-config). Isso configura a autenticação do Facebook no site Facebook Developers para aplicativos Android.
* [Configurando
MCA para autenticação no Facebook](facebook-auth-android.html#facebook-auth-android-mca). Isso
configura seu serviço {{site.data.keyword.amashort}} no
servidor {{site.data.keyword.Bluemix}} para autenticação
do Facebook Android.


### Configurando o SDK do cliente do Facebook do {{site.data.keyword.amashort}}
para a plataforma Android
{: #configure_android}

O {{site.data.keyword.amashort}} cliente
SDK do Facebook deve ser incluído pelo Gradle em seu projeto de app do
Android
nativo.

1. Na pasta do projeto Android, abra o arquivo `build.gradle`
para o módulo do aplicativo (**não** o arquivo
`build.gradle` do projeto). Localize a seção de dependências e inclua
uma nova dependência de compilação para o SDK do cliente:

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'facebookauthentication',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// other dependencies  
	}
	```
	{: codeblock}

2. Clique em **Ferramentas > Android >
Sincronizar projeto com arquivos Gradle** para
sincronizar seu projeto com o Gradle.

3. Abra o arquivo `android/res/values/strings.xml` e inclua uma sequência `<facebook_app_id>` que contenha o seu ID do app
Facebook.

	```XML
	<resources>
		<string name="app_name">HelloCordova</string>
		<string name="launcher_name">@string/app_name</string>
		<string name="activity_name">@string/launcher_name</string>
		<string name="facebook_app_id">"<facebook_app_id>"</string>
	</resources>
	```
	{: codeblock}

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
    {: codeblock}

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
    {: codeblock}

5. Inclua o seguinte em seu código Java da atividade.

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
	   super.onActivityResult(requestCode, resultCode, data);
		FacebookAuthenticationManager.getInstance()
	      .onActivityResultCalled(requestCode, resultCode, data);
	}
	```
	{: codeblock}

### Inicializar o Gerenciador de autorização em seu
código Android nativo
{: #initialize_android}

A API `FacebookAuthenticationManager` ainda deve ser registrada em seu código nativo. Inclua esse código ao método de atividade principal
`onCreate`
usando o `<tenantId>` (consulte
[Antes de iniciar](#before-you-begin)).

```
String tenantId = "<tenantId>";
MCAAuthorizationManager mcaAuthorizationManager = MCAAuthorizationManager.createInstance(this.getApplicationContext(),tenantId);
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
FacebookAuthenticationManager.getInstance().registerDefaultAuthenticationListener(this);
```
{: codeblock}


## Configurando a plataforma iOS
{: #facebook-auth-cordova-ios}

As etapas necessárias para configurar a plataforma iOS do aplicativo Cordova para integração
da autenticação do Facebook são semelhantes às etapas necessárias para aplicativos iOS Swift nativos
(arquivos de cabeçalho são necessários para usar o código Objective-C com o SDK Swift). A principal diferença é que o Cordova CLI atualmente não suporta o gerenciador de dependência CocoaPods. Deve-se incluir manualmente arquivos que sejam necessários
para integrar o cliente {{site.data.keyword.amashort}}
com a autenticação do Facebook. Para mais informações,
consulte
[Ativando a autenticação do Facebook para apps iOS (Swift SDK)](facebook-auth-ios-swift-sdk.html). Execute as etapas a seguir:

* [Configurando
seu aplicativo Facebook para a plataforma iOS](facebook-auth-ios-swift-sdk.html#facebook-auth-ios-config). Isto
configura o serviço de autenticação do Facebook no site Facebook
Developers.
* [Configurando
MCA para autenticação no Facebook](facebook-auth-ios-swift-sdk.html#facebook-auth-ios-configmca). Isso
configura seu serviço {{site.data.keyword.amashort}} no servidor
{{site.data.keyword.Bluemix}}.
* [Configurando o cliente SDK do Facebook MCA para iOS](facebook-auth-ios-swift-sdk.html#facebook-auth-ios-sdk). Isso
instala o {{site.data.keyword.amashort}} iOS Swift SDK para autorização do Facebook usando CocoaPods.


### Ativar Compartilhamento Keychain para iOS
{: #enable_keychain}

Ative `Compartilhamento Keychain`. Acesse
a guia `Recursos` e mude
`Compartilhamento Keychain` para
`On` em seu projeto Xcode.

### Inicialize o {{site.data.keyword.amashort}}
Gerenciador de autorização em Objective-C
{: #initialize_objc}

O Gerenciador de autorização deve ser inicializado no
código nativo Objective-C no arquivo `app-delegate.m `, de acordo com sua versão do Xcode.

```
	#import "<your_module_name>-Swift.h"

	- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {

	    [CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];

	    [[FacebookAuthenticationManager sharedInstance] register];

	    self.viewController = [[MainViewController alloc] init];

	    [[FacebookAuthenticationManager sharedInstance] onFinishLaunchingWithApplication:application withOptions:launchOptions];


	    return [super application:application didFinishLaunchingWithOptions:launchOptions];
	}


	- (BOOL)application: (UIApplication *)application openURL: (NSURL *)url sourceApplication: (NSString *)sourceApplication annotation: (id)annotation {

	   return [[FacebookAuthenticationManager sharedInstance] onOpenURLWithApplication:application 
	   		url:url sourceApplication:sourceApplication annotation:annotation];
	}

```
{: codeblock}

**Nota:** o nome do arquivo de
cabeçalho importado é composto por seu nome de módulo concatenado
para a sequência `-Swift.h`, por exemplo, se o
nome do seu módulo for `Cordova`, a linha
de importação seria `#import "Cordova-Swift.h"`.
Para localizar o nome do módulo, acesse `Configurações
de construção` > `Pacote` >
`Nome do módulo de produto`.

Substitua seu ID do
locatário `<tenantId>` (consulte
[Antes de
iniciar](#facebook-auth-before)).


##Inicializando o cliente SDK
{{site.data.keyword.amashort}} no Cordova WebView
{: #initialize_webview}

Para todas as plataformas, use o código JavaScript a
seguir em seu Cordova Javascript WebView para inicializar o
cliente SDK
{{site.data.keyword.amashort}}.

```javascript
BMSClient.initialize(<applicationBluemixRegion>);
```
{: codeblock}

Substitua
`<applicationBluemixRegion>` pela sua
região (consulte [Antes de
iniciar](#facebook-auth-before)).

## Testando a Autenticação
{: #facebook-auth-cordova-test}

Após o SDK do cliente ser inicializado e o gerenciador de
autenticação do Facebook ser registrado, é possível começar a
fazer solicitações ao serviço de backend móvel.

### Antes de Começar
{: #testing_auth_before}

Deve-se estar usando o modelo do {{site.data.keyword.mobilefirstbp}} e já ter um recurso protegido pelo {{site.data.keyword.amashort}} no terminal `/protected`. Para obter mais informações, consulte [Protegendo recursos](protecting-resources.html).

1. Tente enviar uma solicitação para o terminal protegido
do seu aplicativo backend móvel a partir do seu
navegador. Abra
a URL a seguir: `{applicationRoute}/protected`. Por exemplo: `http://my-mobile-backend.mybluemix.net/protected`.

	O valor do terminal `/protected`
deve ser qualquer terminal protegido de um serviço de backend
móvel que foi criado com o modelo MobileFirst Services
Starter e é protegido com o {{site.data.keyword.amashort}}. Uma mensagem `Unauthorized` é retornada no navegador. Essa mensagem é retornada porque esse terminal só pode ser acessado por aplicativos móveis instrumentados com o {{site.data.keyword.amashort}} client SDK.

1. Use seu aplicativo Cordova para fazer solicitação para o mesmo terminal. Inclua o código a seguir depois de inicializar `BMSClient`:

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error){
    	console.log("failure", error);
    }
	var request = new BMSRequest("<applicationRoute}/protected>", BMSRequest.GET);
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
