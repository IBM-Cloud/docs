---

copyright:
  years: 2015, 2016

---

# Configurando o {{site.data.keyword.amashort}} Client SDK para Cordova
{: #custom-cordova}
Configure seu aplicativo Cordova que está usando autenticação customizada para usar o {{site.data.keyword.amashort}} Client SDK e conecte o aplicativo ao {{site.data.keyword.Bluemix}}.


## Antes de Começar
{: #before-you-begin}
Deve-se ter um recurso que seja protegido por uma instância do serviço {{site.data.keyword.amashort}} que seja configurada para usar um provedor de identidade customizado.  Seu app móvel também devem ser instrumentado com o {{site.data.keyword.amashort}} Client SDK.  Para obter informações adicionais, consulte as seguintes informações:
 * [Introdução
ao {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [Configurando o Cordova SDK](https://console.{DomainName}/docs/services/mobileaccess/getting-started-cordova.html)
 * [Usando um provedor de identidade customizado](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [Criando um provedor de identidade customizado](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [Configurando o {{site.data.keyword.amashort}} para autenticação customizada](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)

## Inicializando o {{site.data.keyword.amashort}} Client SDK
{: #custom-cordova-sdk}
Inicialize o SDK passando os parâmetros applicationGUID e applicationRoute.

1. Obtenha os valores de parâmetro do aplicativo. Abra seu app no painel do {{site.data.keyword.Bluemix_notm}}. Clique em **Opções de dispositivo móvel**. Os
valores **Route** (`applicationRoute`) e
**App GUID** (`applicationGUID`) são exibidos.
1. Inicialize o Client SDK.

	```JavaScript
	BMSClient.initialize(applicationRoute, applicationGUID);

	```
 Substitua *applicationRoute* e *applicationGUID* pelos valores
**Route** e **App GUID** no painel
**Opções móveis** de seu aplicativo no painel
{{site.data.keyword.Bluemix_notm}} dashboard.

## Interface do listener de autenticação
{: #custom-cordva-auth}

O {{site.data.keyword.amashort}} Client SDK fornece uma interface de listener de autenticação para implementar um fluxo de autenticação customizado. Deve-se incluir os métodos a seguir que são chamados em diferentes fases de um processo de autenticação.

```JavaScript
var customAuthenticationListener = {
	onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...},
	onAuthenticationSuccess: function(info){...},
	onAuthenticationFailure: function(info){...}
}
```

Cada método manipula uma fase diferente de um processo de autenticação.

### Método onAuthenticationChallengeReceived
{: #onAuthenticationChallengeReceived}
Esse método é chamado quando um desafio de autenticação customizado é recebido do serviço {{site.data.keyword.amashort}}.
```JavaScript
onAuthenticationChallengeReceived: function(authenticationContext, challenge) {...}
```

#### Argumentos
{: #onAuthenticationChallengeReceived-args}
* `authenticationContext`: fornecido pelo {{site.data.keyword.amashort}} Client SDK para que o desenvolvedor possa relatar respostas de desafio ou falha de autenticação durante a coleção de credenciais, como o cancelamento da solicitação de autenticação pelo usuário.
* `challenge`: um objeto JSON que contém um desafio de autenticação customizado, conforme retornado por um provedor de identidade customizado.

Ao chamar o método `onAuthenticationChallengeReceived`, o {{site.data.keyword.amashort}} Client SDK delega controle ao desenvolvedor. O {{site.data.keyword.amashort}} aguarda credenciais. O desenvolvedor deve coletar credenciais e relatá-las de volta para o {{site.data.keyword.amashort}} Client SDK usando um dos métodos da interface `authContext` a seguir.

```JavaScript
onAuthenticationSuccess: function(info){...}
```

Este método é chamado após uma autenticação bem-sucedida. Os argumentos incluem um JSONObject opcional que contém informações estendidas sobre o sucesso da autenticação.

```JavaScript
onAuthenticationFailure: function(info){...}
```

Esse método é chamado após uma falha de autenticação. Os argumentos incluem um JSONObject opcional que contém informações estendidas sobre a falha de autenticação.

## authenticationContext
{: #custom-cordova-authcontext}

O valor `authenticationContext` é fornecido como um argumento para o método `onAuthenticationChallengeReceived` de um listener de autenticação customizado. O desenvolvedor deve coletar credenciais e usar os métodos `authenticationContext` para retornar credenciais para o {{site.data.keyword.amashort}} Client SDK ou relatar uma falha. Use um dos métodos a seguir:

```JavaScript
authenticationContext.submitAuthenticationChallengeAnswer(challengeAnswer);

authenticationContext.submitAuthenticationFailure(info);
```

## Implementação de amostra de um listener de autenticação customizado
{: #custom-cordova-authlisten-sample}

Essa amostra de listener de autenticação foi projetada para trabalhar com um provedor de identidade customizado. É possível fazer download do provedor de identidade customizado a partir [deste repositório Github](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample).

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

		// In case there was a failure collecting credentials you need to report 		// it back to the authenticationContext. Otherwise Mobile
Client 		// Access Client SDK will remain in a waiting-for-credentials state 		// forever

	},

	onAuthenticationSuccess: function(info){ 		console.log("onAuthenticationSuccess :: ", info); 	},

	onAuthenticationFailure: function(info){ 		console.log("onAuthenticationFailure :: ", info); 	}
}
```

## Registrando um listener de autenticação customizado
{: #custom-cordova-authreg}

Depois de criar um listener de autenticação customizado, registre-o com `BMSClient` antes de iniciar sua utilização. Inclua o código a seguir no aplicativo.  Chame esse código antes de enviar quaisquer solicitações para seus recursos protegidos.

```Java
BMSClient.registerAuthenticationListener(realmName, customAuthenticationListener);
```
 Use o *realmName* especificado no painel do {{site.data.keyword.amashort}}.


## Testando a Autenticação
{: #custom-cordova-test}
Após a inicialização do Client SDK e do registro de um AuthenticationListener customizado, é possível começar a fazer solicitações para seu backend móvel.

### Antes de Começar
{: #custom-cordova-testing-before}
Deve-se ter um aplicativo criado com o modelo do {{site.data.keyword.mobilefirstbp}} e ter um recurso que seja protegido pelo {{site.data.keyword.amashort}} no terminal `/protected`.


1. Envie uma solicitação ao terminal protegido do backend móvel em seu navegador
abrindo `{applicationRoute}/protected`, por exemplo,
`http://my-mobile-backend.mybluemix.net/protected`.
 O terminal `/protected` de um backend móvel criado com o modelo do {{site.data.keyword.mobilefirstbp}} é protegido com o {{site.data.keyword.amashort}}. O terminal só pode ser acessado por aplicativos móveis que sejam instrumentados com o {{site.data.keyword.amashort}} Client SDK. Como resultado, uma mensagem `Unauthorized` é exibida em seu navegador.

1. Use seu aplicativo Cordova para fazer solicitação para o mesmo terminal. Inclua o código a seguir depois de inicializar `BMSClient` e registrar o AuthenticationListener customizado.

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

1. 	Quando sua solicitação for bem-sucedida, a saída a seguir estará no console LogCat ou Xcode:

	![image](images/android-custom-login-success.png)

	![image](images/ios-custom-login-success.png)
