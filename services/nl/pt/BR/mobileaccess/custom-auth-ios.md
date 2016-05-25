---

copyright:
  years: 2015, 2016

---

# Configurando o {{site.data.keyword.amashort}} Client SDK para iOS
{: #custom-ios}

Configure seu aplicativo iOS que está usando autenticação customizada para usar o {{site.data.keyword.amashort}} Client SDK e conecte seu aplicativo ao {{site.data.keyword.Bluemix}}.

**Dica:** Se você estiver desenvolvendo seu app iOS no Swift, considere o {{site.data.keyword.amashort}} Client Swift SDK. As instruções nesta página se aplicam ao {{site.data.keyword.amashort}} Client Objective-C SDK. Para obter instruções sobre o uso do Swift SDK, consulte [Configurando o {{site.data.keyword.amashort}} Client SDK for iOS (Swift SDK)](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-ios-swift-sdk.html)

## Antes de Começar
{: #before-you-begin}
Deve-se ter um recurso que seja protegido por uma instância do serviço {{site.data.keyword.amashort}} que está configurado para usar um provedor de identidade customizado.  Seu app móvel também deve ser instrumentado com o {{site.data.keyword.amashort}} Client SDK.  Para obter informações adicionais, consulte as seguintes informações:
 * [Introdução ao {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [Configurando o iOS Objective-C SDK](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios.html)
 * [Usando um provedor de identidade customizado](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [Criando um provedor de identidade customizado](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [Configurando o {{site.data.keyword.amashort}} para autenticação customizada](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)



## Instalando o Client SDK com o CocoaPods
{: #custom-ios-sdk-cocoapods}
Use o gerenciador de dependência CocoaPods para instalar o {{site.data.keyword.amashort}} Client SDK.

1. Abra o Terminal e navegue até o diretório-raiz de seu projeto iOS.

1. Edite o `Podfile` e inclua a linha a seguir.

	```
	pod 'IMFCore'
	```

1. Na linha de comandos, execute `pod install`.
O CocoaPods instala as dependências incluídas. O progresso e quais componentes foram incluídos são exibidos.

**Importante**: deve-se agora abrir o projeto usando um arquivo xcworkspace que foi gerado por CocoaPods. Normalmente, o nome é `{your-project-name}.xcworkspace`.

1. Execute `open {your-project-name}.xcworkspace` a partir da linha de comandos para abrir sua área de trabalho do projeto iOS.



### Inicializando o Client SDK
{: #custom-ios-sdk-initialize}

Inicialize o SDK passando os parâmetros de rota do aplicativo (`applicationRoute`) e GUID (`applicationGUID`). Um local comum, mas não obrigatório, para colocar o código de inicialização é o método `application:didFinishLaunchingWithOptions` de delegado do seu aplicativo

1. Obter valores de parâmetro do aplicativo. Abra seu app no painel do {{site.data.keyword.Bluemix_notm}}. Clique em **Opções móveis** para ver os valores de **Route** (`applicationRoute`) e **App GUID** (`applicationGUID`).

1. Importe a estrutura `IMFCore` na classe em que deseja usar o Client SDK.

	Objective-C:

	```Objective-C
	#import <IMFCore/IMFCore.h>
	```

	Swift:

	O {{site.data.keyword.amashort}} Client SDK é implementado com Objective-C. Pode ser necessário incluir um cabeçalho de ponte em seu projeto Swift para usar o SDK.

	* Clique com o botão direito no projeto em Xcode e selecione **Novo arquivo...**
	* Na categoria **Origem iOS**, selecione **Arquivo de cabeçalho**. Atribua um nome ao arquivo `BridgingHeader.h`.
	* Inclua `#import <IMFCore/IMFCore.h>` no cabeçalho de ponte.
	* Clique em seu projeto em Xcode e selecione a guia **Configurações de compilação**.
	* Procure por `Cabeçalho de ponte do Objective-C`.
	* Configure o valor para o local do seu arquivo `BridgingHeader.h`, por exemplo: `$(SRCROOT)/MyApp/BridgingHeader.h`
	* Verifique se o seu cabeçalho de ponte está sendo captado pelo Xcode, compilando o seu projeto.

1. Inicialize o Client SDK. Substitua applicationRoute e applicationGUID pelos valores de **Route** (`applicationRoute`) e **App GUID** (`applicationGUID`) que você obteve das **Opções móveis**.

	Objective-C:

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	Swift:

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",
	 							backendGUID: "applicationGUID")
	```


## Delegado IMFAuthenticationHandler
{: #custom-ios-sdk-authhandler}


O {{site.data.keyword.amashort}} Client SDK fornece a interface `IMFAuthenticationHandler` para implementar um fluxo de autenticação customizado. O `IMFAuthenticationHandler` expõe três métodos que são chamados em diferentes fases do processo de autenticação.

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
 						didReceiveAuthenticationChallenge:(NSDictionary*)challenge;
```

Esse método é chamado quando um desafio de autenticação customizada é recebido do serviço {{site.data.keyword.amashort}}. Os argumentos incluem

* O protocolo `IMFAuthenticationContext` é fornecido pelo {{site.data.keyword.amashort}} Client SDK para que o desenvolvedor possa relatar as respostas ou falhas dos desafios de autenticação durante a coleta de credenciais (por exemplo, usuário cancelado)
* `NSDictionary` que contém um desafio de autenticação customizada, conforme retornado por um Provedor de identidade customizado

Ao chamar o método `authenticationContext:didReceiveAuthenticationChallenge`, o {{site.data.keyword.amashort}} Client SDK está delegando controle ao desenvolvedor e se colocando em um modo aguardando credenciais. É responsabilidade do desenvolvedor coletar credenciais e relatá-las ao {{site.data.keyword.amashort}} Client SDK usando um dos métodos de protocolo `IMFAuthenticationContext`, como será descrito abaixo.

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
						didReceiveAuthenticationSuccess:(NSDictionary *)userInfo;
```

Esse método é chamado após uma autenticação bem-sucedida. Os argumentos incluem IMFAuthenticationContext e um NSDictionary opcional que contém informações estendidas sobre o sucesso da autenticação.

```
- (void)authenticationContext:(id<IMFAuthenticationContext>)context
						didReceiveAuthenticationFailure:(NSDictionary*)userInfo;
```

Esse método é chamado após uma falha de authenticação. Os argumentos incluem IMFAuthenticationContext e um NSDictionary opcional que contém informações estendidas sobre falha de autenticação.

## Protocolo IMFAuthenticationContext
{: #custom-ios-sdk-authcontext}


O `IMFAuthenticationContext` é fornecido como um argumento para o método `authenticationContext:didReceiveAuthenticationChallenge` de um `IMFAuthenticationHandler` customizado. É responsabilidade do desenvolvedor coletar credenciais e usar métodos `IMFAuthenticationContext` para retornar credenciais ao {{site.data.keyword.amashort}} Client SDK ou relatar uma falha. Use um dos métodos abaixo

```
-(void) submitAuthenticationChallengeAnswer:(NSDictionary*) answer;

-(void) submitAuthenticationFailure:(NSDictionary*) userInfo;
```

## Implementação de amostra de um IMFAuthenticationDelegate customizado
{: #custom-ios-sdk-sample}


A amostra IMFAuthenticationDelegate foi projetada para funcionar com a amostra de provedor de identidade customizado. É possível fazer download da amostra a partir do [repositório Github](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample).

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
					didReceiveAuthenticationChallenge:(NSDictionary *)challenge {

	NSLog(@"didReceiveAuthenticationChallenge :: %@", challenge);

	// In this sample the IMFAuthenticationDelegate immediately returns a hardcoded
	// set of credentials. In a real life scenario this is where developer would
	// show a login screen, collect credentials and invoke
	// [context submitAuthenticationChallengeAnswer:] API

	NSDictionary *challengeAnswer = [NSDictionary dictionaryWithObjectsAndKeys:
									 @"john.lennon", @"username",
									 @"12345", @"password", nil];

	[context submitAuthenticationChallengeAnswer:challengeAnswer];

	// In case there was a failure collecting credentials you need to report
	// it back to the IMFAuthenticationContext. Otherwise Mobile Client
	// Access Client SDK will remain in a waiting-for-credentials state
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

	func authenticationContext(context: IMFAuthenticationContext!,
					didReceiveAuthenticationChallenge challenge: [NSObject : AnyObject]!) {

		NSLog("didReceiveAuthenticationChallenge :: %@", challenge)

		// In this sample the IMFAuthenticationDelegate immediately returns a hardcoded
		// set of credentials. In a real life scenario this is where developer would
		// show a login screen, collect credentials and invoke
		// context.submitAuthenticationChallengeAnswer() API

		let challengeAnswer: [String:String] = [
			"username":"john.lennon",
			"password":"12345"
		]

		context.submitAuthenticationChallengeAnswer(challengeAnswer)

		// In case there was a failure collecting credentials you need to report
		// it back to the IMFAuthenticationContext. Otherwise Mobile Client
		// Access Client SDK will remain in a waiting-for-credentials state
		// forever
	}


	func authenticationContext(context: IMFAuthenticationContext!,
					didReceiveAuthenticationSuccess userInfo: [NSObject : AnyObject]!) {
		NSLog("didReceiveAuthenticationSuccess")
	}

	func authenticationContext(context: IMFAuthenticationContext!,
					didReceiveAuthenticationFailure userInfo: [NSObject : AnyObject]!) {
		NSLog("didReceiveAuthenticationFailure")
	}
}
```

## Registrando IMFAuthenticationDelegate customizado

Depois de criar um IMFAuthenticationDelegate customizado, registre-o com `IMFClient`. Chame o código a seguir em seu aplicativo antes de enviar quaisquer solicitações aos seus recursos protegidos. Use realmName que você especificou no painel do {{site.data.keyword.amashort}}.

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
Depois de inicializar o Client SDK e registrar um `IMFAuthenticationDelegate` customizado, é possível começar a fazer solicitações ao seu backend móvel.

### Antes de Começar
{: #custom-ios-testing-before}
 Deve-se ter um aplicativo que foi criado com o modelo do {{site.data.keyword.mobilefirstbp}} e ter um recurso que esteja protegido por {{site.data.keyword.amashort}} no terminal `/protected`.

1. Envie uma solicitação ao terminal protegido do backend móvel em seu navegador abrindo `{applicationRoute}/protected`, por exemplo, `http://my-mobile-backend.mybluemix.net/protected`.
  O terminal `/protected` de um backend móvel que é criado com o modelo do {{site.data.keyword.mobilefirstbp}} está protegido com {{site.data.keyword.amashort}}. O terminal pode ser acessado somente por aplicativos móveis que sejam instrumentados com o {{site.data.keyword.amashort}} Client SDK. Como resultado, uma mensagem `Unauthorized` é exibida em seu navegador.
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

