---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-03"

---
{:shortdesc: .shortdesc}

# Ativando a autenticação do Facebook para seus aplicativos iOS (Objective-C SDK)
{: #facebook-auth-ios}

Para usar o Facebook como um provedor de identidade em seus aplicativos {{site.data.keyword.amafull}} iOS, inclua e configure a Plataforma iOS para seu aplicativo Facebook.

{:shortdesc}

**Nota:** embora o SDK do Objective-C permaneça totalmente suportado e ainda seja considerado o SDK
primário para o {{site.data.keyword.Bluemix}} Mobile Services, há planos para descontinuá-lo posteriormente este ano em
favor do novo SDK do Swift (veja [Configurando o SDK do
Swift iOS](facebook-auth-ios-swift-sdk.html)).

## Antes de Começar
{: #before-you-begin}

Você deve ter:
* Um projeto do iOS configurado para trabalhar com CocoaPods.  Para obter mais informações, veja **Instalar o
CocoaPods** em [Configurando o SDK iOS](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios.html).  
   **Nota:** não é necessário instalar o {{site.data.keyword.amashort}} client SDK principal antes de continuar.
* Uma instância de um aplicativo {{site.data.keyword.Bluemix_notm}} que é protegida pelo serviço {{site.data.keyword.amashort}}. Para obter mais informações sobre como criar um backend do {{site.data.keyword.Bluemix_notm}}, consulte [Introdução](index.html).
* Seu valor **AppGUID**. Abra o seu serviço no painel do {{site.data.keyword.amashort}}. Clique no botão **Opções móveis**. O valor
`appGUID` (também conhecido como
`tenantId`) é exibido no campo **App
GUID / TenantId**. Você precisará desse valor para
inicializar o Gerenciador de Autorização.
* Um aplicativo do Facebook e um ID do aplicativo. Para obter mais
informações, consulte
[Criando um aplicativo no website Facebook for Developers](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID).

## Configurando seu aplicativo Facebook para a plataforma iOS
{: #facebook-auth-ios-config}
No site Facebook for Developers:

1. Efetue login em sua conta em [Facebook for Developers](https://developers.facebook.com). 

1. Assegure-se de que a plataforma iOS tenha sido incluída em seu app. Ao incluir ou
configurar a plataforma iOS, será necessário fornecer o **bundleId** do
seu aplicativo iOS. Para
localizar o **bundleId** de seu aplicativo
iOS, procure o **Identificador de pacote
configurável** no arquivo
`info.plist` ou na guia
**Geral** do projeto Xcode.

1. Clique em **Salvar Configurações**.

	**Dica**: considere a ativação do sufixo de esquema URL ou a Conexão única se estiver planejamento usar esses recursos.

1. Clique em **Salvar Configurações**.

## Configurando o {{site.data.keyword.amashort}} para autenticação do Facebook
{: #facebook-auth-ios-configmca}

Depois de configurado o ID do aplicativo Facebook e seu aplicativo Facebook para atender clientes iOS, é possível ativar a autenticação do Facebook no {{site.data.keyword.amashort}}.

1. Abra o seu serviço no painel do {{site.data.keyword.amashort}}.
1. Na guia **Gerenciar**, acione
**Autorização**.
	1. Expanda a seção **Facebook**.
	1. Inclua o **ID do aplicativo Facebook** e clique em **Salvar**.

## Configurando o {{site.data.keyword.amashort}}
SDK do client Facebook para iOS
{: #facebook-auth-ios-sdk}

### Instalando o CocoaPods
{: #facebook-auth-cocoapods}

O {{site.data.keyword.amashort}} client SDK é distribuído com o CocoaPods, um gerenciador de dependência para projetos iOS. O CocoaPods faz o download automático de artefatos de repositórios e os disponibiliza para o aplicativo iOS.

1. Abra o Terminal e execute o comando `pod --version`. Se você já tiver o CocoaPods instalado, o número da versão será exibido. É possível pular para a próxima seção deste tutorial.

1. Instale o CocoaPods executando `sudo gem install cocoapods`. Consulte o [website do CocoaPods](https://cocoapods.org/) se precisar de orientação adicional.

### Instalando o {{site.data.keyword.amashort}}
SDK do client Facebook com o CocoaPods
{: #facebook-auth-install-cocoapods}

1. Em seu projeto iOS, edite o `Podfile` e a linha a seguir:

	```
	pod 'IMFFacebookAuthentication'
	```
{: codeblock}

1. Salve o `Podfile` e execute o comando `pod install` a partir da linha de comandos. O CocoaPods instala as dependências. O progresso e quais componentes foram incluídos são exibidos.
 **Importante**: deve-se abrir agora o projeto usando o arquivo
`xcworkspace` que é gerado pelo CocoaPods. Normalmente, o nome é `{your-project-name}.xcworkspace`.  

1. Execute `open {your-project-name}.xcworkspace` a partir da linha de comandos para abrir sua área de trabalho do projeto iOS.

### Configurando seu projeto do iOS para autenticação do Facebook
{: #facebook-auth-ios-configproject}

1. Localize o arquivo `info.plist`, normalmente localizado na pasta `Arquivos de apoio` em seu projeto Xcode.

1. Configure a integração do Facebook incluindo as propriedades a seguir em seu arquivo `info.plist`:

	![image](images/ios-facebook-infoplist-settings.png)

Também é possível atualizar o arquivo `info.plist` clicando com o botão direito no arquivo, selecionando **Abrir como > Código-fonte** e incluindo o XML a seguir:

```XML
<key>CFBundleURLTypes</key>
<array>
	<dict>
		<key>CFBundleURLSchemes</key>
		<array>
			<string>fb{your-facebook-application-id}</string>
		</array>
	</dict>
</array>
<key>FacebookAppID</key>
<string>{your-facebook-application-id}</string>
<key>FacebookDisplayName</key>
<string>MyApp</string>
<key>LSApplicationQueriesSchemes</key>
<array>
	<string>fbauth</string>
	<string>fbauth2</string>
</array>
<key>NSAppTransportSecurity</key>
<dict>
    <key>NSExceptionDomains</key>
    <dict>
        <key>facebook.com</key>
        <dict>
            <key>NSIncludesSubdomains</key>
            <true/>
            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
            <false/>
        </dict>
        <key>fbcdn.net</key>
        <dict>
            <key>NSIncludesSubdomains</key>
            <true/>
            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
            <false/>
        </dict>
        <key>akamaihd.net</key>
        <dict>
            <key>NSIncludesSubdomains</key>
            <true/>
            <key>NSThirdPartyExceptionRequiresForwardSecrecy</key>
            <false/>
        </dict>
    </dict>
</dict>
```
{: codeblock}

Atualize o esquema URL e as propriedades
`FacebookappID`
com o **ID do aplicativo Facebook**.

 **Importante**: assegure-se de não substituir quaisquer propriedades existentes no arquivo `info.plist`. Se você tiver propriedades de sobreposição, deverá mesclá-las manualmente. Para obter mais informações, consulte [Configurar o projeto Xcode](https://developers.facebook.com/docs/ios/getting-started/) e [Preparando seus apps para iOS9](https://developers.facebook.com/docs/ios/ios9).


## Inicializando o {{site.data.keyword.amashort}} client SDK
{: #facebook-auth-ios-initalize}

Inicialize o client SDK passando a rota do app (`applicationRoute`) e o GUID do app (`applicationGUID`).

Um local comum, mas não obrigatório, para colocar o código de inicialização é o método `application:didFinishLaunchingWithOptions` de delegado do seu aplicativo.


1. Importe a estrutura necessária na classe em que deseja usar o {{site.data.keyword.amashort}} client SDK incluindo os cabeçalhos a seguir:

	####Objective-C
	{: #framework-objc}

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFFacebookAuthentication/IMFFacebookAuthenticationHandler.h>
	#import <FacebookSDK/FacebookSDK.h>
	```	

	####Swift
	{: #bridgingheader-swift}

	O {{site.data.keyword.amashort}} client SDK é implementado usando Objective-C; portanto, pode ser necessário incluir um cabeçalho ponte em seu projeto swift.

	1. Clique com o botão direito no projeto em Xcode e selecione **Novo arquivo...**
		1. Na categoria **Origem iOS**, selecione `Arquivo de cabeçalho`.
		1. Denomine-o `BridgingHeader.h`.
		1. Inclua importações ao seu cabeçalho de ponte:

			```Objective-C
			#import <IMFCore/IMFCore.h>
			#import <IMFFacebookAuthentication/IMFFacebookAuthenticationHandler.h>
			#import <FacebookSDK/FacebookSDK.h>
			```

	1. Clique em seu projeto em Xcode e selecione a guia **Configurações de compilação**.
		1. Procure por **Cabeçalho de ponte do Objective-C**.
		1. Configure o valor para o local do seu arquivo `BridgingHeader.h`, por exemplo: `$(SRCROOT)/MyApp/BridgingHeader.h`.
		1. Assegure-se de que seu cabeçalho de ponte esteja sendo selecionado pelo Xcode, compilando o seu projeto. Nenhuma mensagem de falha deve ser vista.

2. Inicialize o client SDK.	Para obter informações sobre a obtenção de`applicationRoute` e `applicationGUID`, veja [Antes de iniciar](#before-you-begin).

	####Objective-C
	{: #approute-objc}

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	####Swift
	{: #approute-swift}

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",
	 							backendGUID: "applicationGUID")
	```

1. Inicialize o `AuthorizationManager` passando o parâmetro
`tenantId` do serviço {{site.data.keyword.amashort}}. Veja [Antes de iniciar](#before-you-begin).

	####Objective-C
	{: #authman-objc}

	```Objective-C
     [[IMFAuthorizationManager sharedInstance]  initializeWithTenantId: @"tenantId"];
	```

	####Swift
	{: #authman-swift}

	```Swift
  IMFAuthorizationManager.sharedInstance().initializeWithTenantId("tenantId")
	```

1. Notifique o Facebook SDK sobre a ativação do app e registre o Manipulador de
autenticação do Facebook incluindo o código a seguir no método
`application:didFinishLaunchingWithOptions` na delegação do app. Inclua esse código após a inicialização da instância IMFClient.

	####Objective-C
	{: #activate-objc}

	```Objective-C
		[FBAppEvents activateApp];
		[[IMFFacebookAuthenticationHandler sharedInstance] registerWithDefaultDelegate];
	```

	####Swift
	{: #activate-swift}

	```Swift
		FBAppEvents.activateApp()
		IMFFacebookAuthenticationHandler.sharedInstance().registerWithDefaultDelegate()
	```

1. Inclua o código a seguir no delegado do app.

	####Objective-C
	{: #appdelegate-objc}

	```Objective-C
	- (BOOL)application:(UIApplication *)application openURL:(NSURL *)url
			sourceApplication:(NSString *)sourceApplication annotation:(id)annotation {

		return [FBAppCall handleOpenURL:url sourceApplication:sourceApplication];
	}
	```

	####Swift
	{: #appdelegate-swift}

	```Swift
	func application(application: UIApplication, openURL url: NSURL,
					sourceApplication: String?, annotation: AnyObject) -> Bool {

		return FBAppCall.handleOpenURL(url, sourceApplication: sourceApplication)

	}
```


## Testando a Autenticação
{: #facebook-auth-ios-testing}
Após a inicialização do client SDK e o registro do Gerenciador de autenticação do Facebook, será possível começar a fazer solicitações para seu backend móvel.

### Antes de Começar
{: #facebook-auth-ios-testing-before}
Deve-se usar o modelo do {{site.data.keyword.mobilefirstbp}} e já ter um recurso protegido por {{site.data.keyword.amashort}} no terminal `/protected`. Se for necessário configurar um terminal `/protected`, consulte [Protegendo recursos](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

1. Tente enviar uma solicitação para o terminal protegido de seu backend móvel recém-criado em seu navegador. Abra a URL a seguir: `{applicationRoute}/protected`.
Por exemplo: `http://my-mobile-backend.mybluemix.net/protected`
<br/>O terminal `/protected` de um backend móvel criado com o modelo do MobileFirst Services Starter é protegido com o {{site.data.keyword.amashort}}. Uma mensagem `Unauthorized` é retornada no navegador. Essa mensagem é retornada porque esse terminal só pode ser acessado por aplicativos móveis instrumentados com o {{site.data.keyword.amashort}} client SDK.

1. Use seu aplicativo iOS para fazer uma solicitação ao mesmo terminal.

	####Objective-C
	{: #requestpath-objc}

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

	####Swift
	{: #requestpath-swift}

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

1. Execute o aplicativo. Uma tela de login do Facebook é exibida.

	![image](images/ios-facebook-login.png)

	Essa tela pode parecer ligeiramente diferente se você não tiver o app Facebook instalado em seu dispositivo ou se não estiver com login efetuado atualmente no Facebook.

1. Clique em **OK** para autorizar o {{site.data.keyword.amashort}} a usar sua identidade de usuário do Facebook para propósitos de autenticação.

1. 	Quando sua solicitação for bem-sucedida, a saída a seguir será exibida no
console do Xcode:	![image](images/ios-facebook-login-success.png)

	Também é possível incluir a funcionalidade de logout incluindo o código a seguir:

	####Objective-C
	{: #logout-objc}

	```Objective-C
	[[IMFFacebookAuthenticationHandler sharedInstance] logout : callBack]
	```
{: codeblock}

	####Swift
	{: #logout-swift}

	```Swift
	IMFFacebookAuthenticationHandler.sharedInstance().logout(callBack)
	```
{: codeblock}

	Se você chamar esse código depois que um usuário estiver conectado ao Facebook e ele tentar efetuar login novamente, ele será solicitado a autorizar o {{site.data.keyword.amashort}} a usar o Facebook para propósitos de autenticação.

	Para alternar usuários, deve-se chamar esse código e o usuário deve efetuar logout do Facebook em seu navegador.

  Passar `callBack` para a função de logout é opcional. Também é possível passar `nil`.
