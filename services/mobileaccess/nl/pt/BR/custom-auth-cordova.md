---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Configurando a autenticação customizada para seu aplicativo {{site.data.keyword.amashort}} Cordova
{: #custom-cordova}

Instrua seu aplicativo Cordova para usar autenticação personalizada e o cliente SDK {{site.data.keyword.amafull}} para acessar seu aplicativo protegido.

## Antes de Começar
{: #before-you-begin}
* Um recurso que seja protegido por uma instância do
serviço {{site.data.keyword.amashort}} que está
configurado para usar um provedor de identidade customizado
(consulte
[Configurando autenticação customizada](custom-auth-config-mca.html)).  
* Seu valor **TenantID**. Abra o seu serviço no painel do {{site.data.keyword.amashort}}. Clique no botão **Opções móveis**. O valor
`tenantId` (também conhecido como
`appGUID`) é exibido no campo **App
GUID / TenantId**. Você precisará desse valor para
inicializar o Gerenciador de Autorização.
* Seu nome de **Domínio**. Este é o
valor que você especificou no campo **Nome do
domínio** da seção **Customizado**
no guia **Gerenciamento** do painel {{site.data.keyword.amashort}}.
* A {{site.data.keyword.Bluemix_notm}}
**Região**. É possível encontrar a sua região
{{site.data.keyword.Bluemix_notm}} atual no cabeçalho,
próximo ao ícone **Avatar**
![ícone de avatar](images/face.jpg "ícone de avatar"). O valor da região que aparece deve ser um dos seguintes: `US South`, `United Kingdom` ou `Sydney`. A sintaxe exata das constantes SDK correspondentes é fornecida nos exemplos de código.

Para obter informações adicionais, consulte as seguintes informações:

 * [Configurando o {{site.data.keyword.amashort}} para autenticação customizada](custom-auth-config-mca.html). Isso mostra como configurar o serviço {{site.data.keyword.amashort}} para autenticação customizada. Aqui você define o valor **Domínio**.
 * [Configurando o Cordova SDK](getting-started-cordova.html). Informações sobre como configurar o aplicativo cliente Cordova.
 * [Usando um provedor de identidade customizado](custom-auth.html). Como autenticar usuários com um provedor de identidade customizado.
 * [Criando um provedor de identidade customizado](custom-auth-identity-provider.html). Alguns exemplos de como um provedor de identidade customizado funciona.

## Configure seu código Cordova WebView
### Inicializando o cliente SDK {{site.data.keyword.amashort}} no Cordova WebView
{: #custom-cordova-sdk}
Inicialize o SDK passando o parâmetro `< applicationBluemixRegion>` no arquivo `index.js`.

```JavaScript
BMSClient.initialize("<applicationBluemixRegion>");
```
{: codeblock}

Substitua `<applicationBluemixRegion>` pela sua região (consulte [Antes de iniciar](#before-you-begin)).


### Interface do listener de autenticação
{: #custom-cordva-auth}

O {{site.data.keyword.amashort}} client SDK fornece uma interface de listener de autenticação para implementar um fluxo de autenticação customizado. Deve-se incluir os métodos a seguir que são chamados em diferentes fases de um processo de autenticação.

```JavaScript
var customAuthenticationListener = {
	onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...},
	onAuthenticationSuccess: function(info){...},
	onAuthenticationFailure: function(info){...}
}
```
{: codeblock}

Cada método manipula uma fase diferente de um processo de autenticação.

### Método onAuthenticationChallengeReceived
{: #onAuthenticationChallengeReceived}
Esse método é chamado quando um desafio de autenticação customizado é recebido do serviço {{site.data.keyword.amashort}}.
```JavaScript
onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...}
```
{: codeblock}

* `authenticationContext`: fornecido pelo {{site.data.keyword.amashort}} client SDK para que o desenvolvedor possa relatar respostas de desafio ou falha de autenticação durante a coleta de credenciais, como o cancelamento da solicitação de autenticação pelo usuário.
* `challenge`: um objeto JSON que contém um desafio de autenticação customizado, conforme retornado por um provedor de identidade customizado.

Ao chamar o método `onAuthenticationChallengeReceived`, o {{site.data.keyword.amashort}} client SDK delega controle ao desenvolvedor. O {{site.data.keyword.amashort}} aguarda credenciais. O desenvolvedor deve coletar credenciais e relatá-las de volta para o {{site.data.keyword.amashort}} client SDK usando um dos métodos da interface `authContext` a seguir.

```JavaScript
onAuthenticationSuccess: function(info){...}
```
{: codeblock}

Este método é chamado após uma autenticação bem-sucedida. Os argumentos incluem um objeto JSON opcional que contém informações estendidas sobre o sucesso da autenticação.

```JavaScript
onAuthenticationFailure: function(info){...}
```
{: codeblock}

Esse método é chamado após uma falha de autenticação. Os argumentos incluem um objeto JSON opcional que contém informações estendidas sobre a falha de autenticação.

### authenticationContext
{: #custom-cordova-authcontext}

O valor `authenticationContext` é fornecido como um argumento para o método `onAuthenticationChallengeReceived` de um listener de autenticação customizado. O desenvolvedor deve coletar credenciais e usar os métodos `authenticationContext` para retornar credenciais para o {{site.data.keyword.amashort}} client SDK ou relatar uma falha. Use um dos métodos a seguir:

```JavaScript
authenticationContext.submitAuthenticationChallengeAnswer(challengeAnswer);
```
{: codeblock}

```JavaScript
authenticationContext.submitAuthenticationFailure(info);
```
{: codeblock}

O código a seguir demonstra como um listener de autenticação do cliente pode coletar
credenciais, lidar com desafios e fornecer respostas de autenticação.

## Implementação de amostra de um fluxo de trabalho do listener de autenticação customizado
{: #custom-cordova-authlisten-sample}

Essa amostra de listener de autenticação foi projetada para trabalhar com um provedor de identidade customizado. É possível fazer download do provedor de identidade customizado [neste repositório Github ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample "Ícone de link externo"){: new_window}.

```JavaScript
var customAuthenticationListener = {
	onAuthenticationChallengeReceived: function(authenticationContext, challenge) {
		console.log("onAuthenticationChallengeReceived :: ", challenge);

		// Nesta amostra, o listener de autenticação retorna imediatamente um conjunto de
		// credenciais codificado permanentemente. Em um cenário da vida real este é o local onde o desenvolvedor
  // mostraria uma tela de login, coletaria credenciais e chamaria
  // a API authenticationContext.submitAuthenticationChallengeAnswer()

		var challengeResponse = {
			username: "john.lennon",
			password: "12345"
		}

		authenticationContext.submitAuthenticationChallengeAnswer(challengeResponse);

		// In case there was a failure collecting credentials you need to report 		// it back to the authenticationContext. Otherwise Mobile Client
			// Access client SDK will remain in a waiting-for-credentials state
			// forever

	},

	onAuthenticationSuccess: function(info){
		console.log("onAuthenticationSuccess :: ", info);
	},

	onAuthenticationFailure: function(info){ 		console.log("onAuthenticationFailure :: ", info); 	}
}
```
{: codeblock}

## Registrando um listener de autenticação customizado no WebView Cordova
{: #custom-cordova-authreg}

Após criar um listener de autenticação customizado, você deverá registrá-lo com `BMSClient` antes de poder iniciar o uso. Inclua o código a seguir no aplicativo.  Chame esse código antes de enviar quaisquer solicitações para seus recursos protegidos.

```Java
BMSClient.registerAuthenticationListener(<realmName>, customAuthenticationListener);
```
{: codeblock}
 Use o `realmName` especificado no painel do {{site.data.keyword.amashort}}.

## Configure o Gerenciador de autorização no código nativo

O Gerenciador de autorização {{site.data.keyword.amashort}} deve ser registrado em sua plataforma de código nativo.

**Android** (incluir ao `onCreate` na atividade principal)

```
String tenantId = "<tenantId>";
MCAAuthorizationManager.createInstance(this.getApplicationContext(),tenantId);
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
```
{: codeblock}

**iOS Objective-C** (incluir ao
`AppDelegate.m`)

Registre seu Gerenciador de autorização de acordo com sua versão do Xcode.

```
# import "<your_module_name>-Swift.h"

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions

{  

    //[CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];
 }
```
{: codeblock}

Nota: para o nome do arquivo de cabeçalho Swift correto, substitua `your_module_name`
pelo nome do módulo do seu projeto, por exemplo, se o nome do seu módulo for `Cordova`,
então, ele deverá ser `#import "Cordova-Swift.h"`. Para localizar o nome do módulo, acesse **Construir configurações > Pacote > Nome do módulo do produto**.

**Nota:** substitua o `tenantId` pelo seu ID do locatário localizado no botão **Opções móveis** no painel de serviço {{site.data.keyword.amashort}}.


## Ativar Compartilhamento Keychain para iOS

Ative o `Compartilhamento Keychain` acessando a guia `Recursos` e colocando o `Compartilhamento Keychain` em modo `Ativado` em seu projeto Xcode.


## Testando a Autenticação
{: #custom-cordova-test}
Depois que o client SDK é inicializado e um `AuthenticationListener` customizado é registrado, é possível iniciar as solicitações para seu aplicativo backend móvel.

### Antes de Começar
{: #custom-cordova-testing-before}
Deve-se ter um aplicativo que foi criado com o modelo do {{site.data.keyword.mobilefirstbp}} e ter um recurso que esteja protegido por {{site.data.keyword.amashort}} no terminal `/protected`.


1. Envie uma solicitação para o terminal protegido do aplicativo backend móvel em seu navegador abrindo `{applicationRoute}/protected`, por exemplo, `http://my-mobile-backend.mybluemix.net/protected`.
 O terminal `/protected` de um aplicativo backend móvel criado com o modelo {{site.data.keyword.mobilefirstbp}} está protegido com o {{site.data.keyword.amashort}}. O terminal pode ser acessado somente por aplicativos móveis que sejam instrumentados com o cliente SDK {{site.data.keyword.amashort}}. Como resultado, uma mensagem `Unauthorized` é exibida em seu navegador.

1. Use seu aplicativo Cordova para fazer solicitação para o mesmo terminal. Inclua o código a seguir depois de inicializar `BMSClient` e registrar o AuthenticationListener customizado.

	```JavaScript
	var success = function(data){
    	console.log("success", data);
    }
	var failure = function(error)
    	{console.log("failure", error);
    }
	var request = new BMSRequest("<your-application-route>", BMSRequest.GET);
	request.send(success, failure);
	```
	{: codeblock}

	Substitua `<
your-application-route>` pela URL do aplicativo backend
(consulte [Antes de
iniciar](#before-you-begin)).

1. 	Quando sua solicitação for bem-sucedida, a saída a
seguir estará no console `LogCat` ou Xcode:

	![image](images/android-custom-login-success.png)

	![image](images/ios-custom-login-success.png)
