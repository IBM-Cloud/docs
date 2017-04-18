---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-07"

---

# Configurando o SDK do cliente {{site.data.keyword.amashort}} para iOS (Objective-C)
{: #custom-ios}


Configure seu aplicativo iOS que está usando autenticação customizada para utilizar
o SDK do cliente {{site.data.keyword.amafull}} e conectar seu aplicativo ao {{site.data.keyword.Bluemix}}.

**Nota:** se você estiver desenvolvendo seu app iOS no Swift, considere o uso do {{site.data.keyword.amashort}} client Swift SDK. As instruções nesta página se aplicam ao {{site.data.keyword.amashort}} client Objective-C SDK. Para obter instruções sobre como usar o novo Swift SDK, consulte [Configurando o {{site.data.keyword.amashort}} client SDK for iOS (Swift SDK)](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-ios-swift-sdk.html).

## Antes de Começar
{: #before-you-begin}
Você deve ter:

* Um recurso que seja protegido por uma instância do
serviço {{site.data.keyword.amashort}} que está
configurado para usar um provedor de identidade customizado
(consulte
[Configurando autenticação customizada](https://console.stage1.ng.bluemix.net/docs/services/mobileaccess/custom-auth-config-mca.html)).  
* Seu valor **TenantID**. Abra o seu serviço no painel do {{site.data.keyword.amashort}}. Clique no botão **Opções móveis**. O valor
`tenantId` (também conhecido como
`appGUID`) é exibido no campo **App
GUID / TenantId**. Você precisará desse valor para
inicializar o Gerenciador de Autorização.
* Seu nome de **Domínio**. Este é o
valor que você especificou no campo **Nome do
domínio** da seção **Customizado**
na guia **Gerenciamento** do painel
{{site.data.keyword.amashort}} (consulte
[Configurando
autenticação customizada](https://console.stage1.ng.bluemix.net/docs/services/mobileaccess/custom-auth-config-mca.html)).
* A URL do seu aplicativo backend (**Rota de App**). Você precisará desse valor para enviar
solicitações para os terminais protegido do seu aplicativo
backend.
* A {{site.data.keyword.Bluemix_notm}}
**Região**. É possível encontrar a sua região
{{site.data.keyword.Bluemix_notm}} atual no cabeçalho,
próximo ao ícone **Avatar**
![ícone de avatar](images/face.jpg "ícone de avatar"). O valor da região que aparece deve ser um dos
seguintes: `US South`, `United Kingdom` ou `Sydney`, e corresponder
aos valores no SDK requeridos no código WebView Javascript:
`BMSClient.REGION_US_SOUTH`,
`BMSClient.REGION_UK` ou
`BMSClient.REGION_SYDNEY`. Você precisará desse
valor para inicializar o cliente
{{site.data.keyword.amashort}}.

Para obter informações adicionais, consulte as seguintes informações:
 * [Introdução
ao {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [Configurando o iOS Objective-C SDK](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios.html)
 * [Usando um provedor de identidade customizado](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [Criando um provedor de identidade customizado](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [Configurando o {{site.data.keyword.amashort}} para autenticação customizada](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)


## Instalando o client SDK com o CocoaPods
{: #custom-ios-sdk-cocoapods}
Use o gerenciador de dependência CocoaPods para instalar o {{site.data.keyword.amashort}} client SDK.

1. Abra o Terminal e navegue até o diretório-raiz de seu projeto iOS.

1. Edite o `Podfile` e inclua a linha a seguir.

	```
	pod 'IMFCore'
	```

1. Na linha de comandos, execute `pod install`.
O CocoaPods instala as dependências incluídas. O progresso e quais componentes foram incluídos são exibidos.

    **Importante**: deve-se agora abrir o projeto usando um arquivo xcworkspace que foi gerado por CocoaPods. Normalmente, o nome é `{your-project-name}.xcworkspace`.

1. Execute `open {your-project-name}.xcworkspace` a partir da linha de comandos para abrir sua área de trabalho do projeto iOS.

### Inicializando o client SDK
{: #custom-ios-sdk-initialize}

Inicialize o SDK passando os parâmetros **Rota de App** (`applicationRoute`) e
**TenantID**
(`tenantID`). 

Um local comum, mas não obrigatório, para colocar o código de inicialização é o método `application:didFinishLaunchingWithOptions` de delegado do seu aplicativo

1. Importe a estrutura `IMFCore` na classe em que você deseja usar o client SDK.

	Objective-C:

	```Objective-C
	#import <IMFCore/IMFCore.h>
	```

	Swift:

	O {{site.data.keyword.amashort}} client SDK é implementado com Objective-C. Pode ser necessário incluir um cabeçalho de ponte em seu projeto Swift para usar o SDK.

	* Clique com o botão direito no projeto em Xcode e selecione **Novo arquivo...**
	* Na categoria **Origem iOS**, selecione **Arquivo de cabeçalho**. Atribua um nome ao arquivo `BridgingHeader.h`.
	* Inclua `#import <IMFCore/IMFCore.h>` no cabeçalho de ponte.
	* Clique em seu projeto em Xcode e selecione a guia **Configurações de compilação**.
	* Procure por `Cabeçalho de ponte do Objective-C`.
	* Configure o valor para o local do seu arquivo `BridgingHeader.h`, por exemplo: `$(SRCROOT)/MyApp/BridgingHeader.h`
	* Verifique se o seu cabeçalho de ponte está sendo captado pelo Xcode, compilando o seu projeto.

1. Inicialize o client SDK. Substitua o **Rota de App** (`applicationRoute`) e
**TenantID**
(`tenantID`) com valores. Para obter mais
informações sobre como obter esses valores, consulte
[Antes de iniciar](##before-you-begin).

	Objective-C:

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"tenantID"];
	```

	Swift:

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",
	 							backendGUID: "tenantID")
	```

## Inicializando o AuthorizationManager
Inicialize o AuthorizationManager passando o parâmetro `tenantId`
do serviço {{site.data.keyword.amashort}}. 


### Objective-C:

```Objective-
 [[IMFAuthorizationManager sharedInstance]  initializeWithTenantId: @"tenantId"];
```

### Swift:

```Swift
  IMFAuthorizationManager.sharedInstance().initializeWithTenantId("tenantId")
```


## Delegado IMFAuthenticationHandler
{: #custom-ios-sdk-authhandler}


O {{site.data.keyword.amashort}} client SDK fornece a interface `IMFAuthenticationHandler` para implementar um fluxo de autenticação customizado. O `IMFAuthenticationHandler` expõe três métodos que são chamados em diferentes fases do processo de autenticação.

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
 						didReceiveAuthenticationChallenge:(NSDictionary*)challenge;
```

Esse método é chamado quando um desafio de autenticação customizada é recebido do serviço {{site.data.keyword.amashort}}. Os argumentos incluem

* O protocolo `IMFAuthenticationContext` é fornecido pelo {{site.data.keyword.amashort}} client SDK para que o desenvolvedor possa relatar as respostas ou falhas dos desafios de autenticação durante a coleta de credenciais (por exemplo, usuário cancelado)
* `NSDictionary` que contém um desafio de autenticação customizada, conforme retornado por um Provedor de identidade customizado

Ao chamar o método `authenticationContext:didReceiveAuthenticationChallenge`, o {{site.data.keyword.amashort}} client SDK está delegando controle para o desenvolvedor e se colocando em um modo de espera de credenciais. É responsabilidade do desenvolvedor coletar credenciais e relatá-las de volta para o {{site.data.keyword.amashort}} client SDK usando um dos métodos de protocolo `IMFAuthenticationContext` a seguir:

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
						didReceiveAuthenticationSuccess:(NSDictionary *)userInfo;
```

Esse método é chamado após uma autenticação bem-sucedida. Os argumentos incluem `IMFAuthenticationContext` e um `NSDictionary` opcional que contém informações estendidas sobre o sucesso da autenticação.

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
						didReceiveAuthenticationFailure:(NSDictionary*)userInfo;
```

Esse método é chamado após uma falha de authenticação. Os argumentos incluem `IMFAuthenticationContext` e um `NSDictionary` opcional que contém informações estendidas sobre a falha de autenticação.

## Protocolo IMFAuthenticationContext
{: #custom-ios-sdk-authcontext}


O protocolo `IMFAuthenticationContext` é fornecido como um argumento para o método `authenticationContext:didReceiveAuthenticationChallenge` de um `IMFAuthenticationHandler` customizado. É responsabilidade do desenvolvedor coletar credenciais e usar métodos `IMFAuthenticationContext` para retornar credenciais para o {{site.data.keyword.amashort}} client SDK ou relatar uma falha. 
```
-(void) submitAuthenticationChallengeAnswer:(NSDictionary*) answer;

-(void) submitAuthenticationFailure:(NSDictionary*) userInfo;
```

## Implementação de amostra de um IMFAuthenticationDelegate customizado
{: #custom-ios-sdk-sample}


A amostra IMFAuthenticationDelegate foi projetada para funcionar com a amostra de provedor de identidade customizado. É possível fazer download da amostra a partir do [repositório GitHub](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample).

Objective-C:

``` Objective-C
CustomAuthenticationDelegate.h
-----------------------------------
#import <Foundation/Foundation.h>

@import IMFCore;
@interface CustomAuthenticationDelegate : NSObject <IMFAuthenticationDelegate>
@end


CustomAuthenticationDelegate.m
-----------------------------------
#import "CustomAuthenticationDelegate.h"

@implementation CustomAuthenticationDelegate

-(void)authenticationContext:(id<IMFAuthenticationContext>)context
					didReceiveAuthenticationChallenge:(NSDictionary *)challenge{

	NSLog(@"didReceiveAuthenticationChallenge :: %@", challenge);

	// In this sample, the IMFAuthenticationDelegate immediately returns a hardcoded
	// set of credentials. In a real life scenario, a developer would
	// show a login screen, collect credentials and invoke the
	// [context submitAuthenticationChallengeAnswer:] API

	NSDictionary *challengeAnswer = [NSDictionary dictionaryWithObjectsAndKeys:
									 @"john.lennon", @"username",
									 @"12345", @"password", nil];

	[context submitAuthenticationChallengeAnswer:challengeAnswer];

	// In case there is a failure collecting credentials, report
	// the failure to IMFAuthenticationContext. Otherwise, the Mobile Client
	// Access client SDK remains in a waiting-for-credentials state
	// forever
}

-(void)authenticationContext:(id<IMFAuthenticationContext>)context
					didReceiveAuthenticationSuccess:(NSDictionary *)userInfo{
	NSLog(@"didReceiveAuthenticationSuccess");


}

-(void)authenticationContext:(id<IMFAuthenticationContext>)context
					didReceiveAuthenticationFailure:(NSDictionary *)userInfo{
	NSLog(@"didReceiveAuthenticationFailure");

}

@end
```

Implementação do Swift:

```Swift
import Foundation

class CustomAuthenticationDelegate : NSObject, IMFAuthenticationDelegate{

	func authenticationContext(context: IMFAuthenticationContext!, didReceiveAuthenticationChallenge challenge: [NSObject : AnyObject]!) {

		NSLog("didReceiveAuthenticationChallenge :: %@", challenge)

		// In this sample, the IMFAuthenticationDelegate immediately returns a hardcoded
		// set of credentials. In a real life scenario a developer would
		// show a login screen, collect credentials and invoke the
		// context.submitAuthenticationChallengeAnswer() API

		let challengeAnswer: [String:String] = [
			"username":"john.lennon",
			"password":"12345"
		]

		context.submitAuthenticationChallengeAnswer(challengeAnswer)

		// In case there is a failure collecting credentials, report
		// it back to IMFAuthenticationContext. Otherwise, the Mobile Client
		// Access client SDK remains in a waiting-for-credentials state
		// forever
	}


	func authenticationContext(context: IMFAuthenticationContext!,
					didReceiveAuthenticationSuccess userInfo: [NSObject : AnyObject]!) {
		NSLog("didReceiveAuthenticationSuccess")
	}

	func authenticationContext(context: IMFAuthenticationContext!, didReceiveAuthenticationFailure userInfo: [NSObject : AnyObject]!) {
		NSLog("didReceiveAuthenticationFailure")
	}
}
```

## Registrando IMFAuthenticationDelegate customizado

Depois de criar um `IMFAuthenticationDelegate` customizado, registre com o `IMFClient`. Chame o código a seguir em seu aplicativo antes de enviar quaisquer solicitações aos seus recursos protegidos. Use o `realmName` especificado no painel do {{site.data.keyword.amashort}}.

Aplicativos Objective-C:

```Objective-C
[[IMFClient sharedInstance]
				registerAuthenticationDelegate:[CustomAuthenticationDelegate new]
										forRealm:realmName];
```

Aplicativos Swift:
```Swift
IMFClient.sharedInstance().registerAuthenticationDelegate(CustomAuthenticationDelegate(),
									forRealm: realmName)
```


## Testando a Autenticação
{: #custom-ios-testing}
Depois de inicializar o client SDK e registrar um `IMFAuthenticationDelegate` customizado, é possível começar a fazer solicitações para seu aplicativo backend móvel.

### Antes de Começar
{: #custom-ios-testing-before}
 Deve-se ter um aplicativo que foi criado com o modelo do {{site.data.keyword.mobilefirstbp}} e ter um recurso que esteja protegido por {{site.data.keyword.amashort}} no terminal `/protected`.

1. Envie uma solicitação para o terminal protegido do aplicativo backend móvel em seu navegador abrindo `{applicationRoute}/protected`, por exemplo, `http://my-mobile-backend.mybluemix.net/protected`.
  O terminal `/protected` de um aplicativo backend móvel criado com o modelo {{site.data.keyword.mobilefirstbp}} está protegido com o {{site.data.keyword.amashort}}. O terminal pode ser acessado somente por aplicativos móveis que sejam instrumentados com o {{site.data.keyword.amashort}} client SDK. Como resultado, uma mensagem `Unauthorized` é exibida em seu navegador.
1. Use seu aplicativo iOS para fazer solicitação ao mesmo terminal. Inclua o código a seguir depois de inicializar `BMSClient` e registrar seu `IMFAuthenticationDelegate` customizado:

	Objective-C:

	```Objective-C
	NSString *requestPath = [NSString stringWithFormat:@"%@/protected",
								[[IMFClient sharedInstance] backendRoute]];

	IMFResourceRequest *request =  [IMFResourceRequest requestWithPath:requestPath
																method:@"GET"];

	[request sendWithCompletionHandler:^(IMFResponse *response, NSError *error) {
		if (error){
			NSLog(@"Error :: %@", [error description]);
		} else {
			NSLog(@"Response :: %@", [response responseText]);
			NSLog(@"%@", [[IMFAuthorizationManager sharedInstance] userIdentity]);
		}
	}];
	```

	Swift:

	```Swift
	let requestPath = IMFClient.sharedInstance().backendRoute + "/protected"

	let request = IMFResourceRequest(path: requestPath, method: "GET");
	request.sendWithCompletionHandler { (response, error) -> Void in
		if (nil != error){
			NSLog("Error :: %@", error.description)
		} else {
			NSLog("Response :: %@", response.responseText)
			NSLog("%@", IMFAuthorizationManager.sharedInstance().userIdentity)
		}
	};

	```
1. 	Quando suas solicitações forem bem-sucedidas, você verá a saída a seguir no console Xcode:

	![image](images/ios-custom-login-success.png)

	Também é possível incluir a funcionalidade de logout incluindo o código a seguir:

	Objective C:

	```Objective-C
	[[IMFAuthorizationManager sharedInstance] logout : callBack]
	```

	Swift:

	```Swift
	IMFAuthorizationManager.sharedInstance().logout(callBack)
	```

 Se você chamar esse código depois que um usuário estiver conectado, ele será desconectado. Quando o usuário tentar efetuar login novamente, ele deverá responder ao desafio recebido do servidor novamente.

 Passar `callBack` para a função de logout é opcional. Também é possível passar `nil`.
