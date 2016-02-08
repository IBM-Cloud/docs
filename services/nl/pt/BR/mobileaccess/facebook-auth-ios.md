# Ativando a autenticação do Facebook em apps iOS
{: #facebook-auth-ios}

Para usar o Facebook como provedor de identidade em seus aplicativos iOS, inclua e configure a Plataforma iOS para seu aplicativo Facebook.

## Antes de Começar
{: #facebook-auth-ios-before}
* Deve-se ter um recurso que seja protegido por {{site.data.keyword.amashort}} e um projeto iOS que seja instrumentado com o
{{site.data.keyword.amashort}} Client SDK. Para obter mais informações, veja [Introdução ao {{site.data.keyword.amashort}}](getting-started.html) e [Configurando o SDK do iOS](getting-started-ios.html).  
* Proteja manualmente seu aplicativos backend com o {{site.data.keyword.amashort}}  Server SDK. Para obter mais informações, veja [Protegendo recursos](protecting-resources.html).
* Crie um ID do aplicativo Facebook. Para obter mais informações, veja [Obtendo um ID do aplicativo Facebook a partir do Portal do desenvolvedor do Facebook](facebook-auth-overview.html#facebook-appID).

## Configurando seu aplicativo Facebook para a plataforma iOS
{: #facebook-auth-ios-config}


1. Em seu aplicativo Facebook no Portal do desenvolvedor do Facebook, clique em **Configurações > Incluir plataforma > iOS**.

1. Especifique o *bundleId* de seu aplicativo iOS. Para localizar o *bundleId* de seu aplicativo iOS, procure o **Identificador de pacote configurável** no arquivo `info.plist` ou na guia **Geral** do projeto Xcode.
**Dica**: considere a ativação do sufixo de esquema URL ou a Conexão única se estiver planejamento usar esses recursos.

1. Clique em **Salvar Configurações**.

## Configurando o {{site.data.keyword.amashort}} para autenticação do Facebook
{: #facebook-auth-ios-configmca}

Depois de configurado o ID do aplicativo Facebook e seu aplicativo Facebook para atender clientes iOS, é possível ativar a autenticação do Facebook no {{site.data.keyword.amashort}}.

1. Abra seu app no painel do {{site.data.keyword.Bluemix_notm}}. 

1. Clique em **Opções de dispositivo móvel** e anote os valores *applicationRoute* e *applicationGUID*. Eles serão necessários ao inicializar o SDK.

1. Clique no ladrilho {{site.data.keyword.amashort}}. O painel do {{site.data.keyword.amashort}} é carregado.

1. Clique em **Configurar autenticação > Facebook**.

1. Especifique o ID do aplicativo Facebook e clique em **Salvar**.

## Configurando o {{site.data.keyword.amashort}} Client SDK para iOS
{: #facebook-auth-ios-sdk}

### Instalando o CocoaPods
{: #facebook-auth-cocoapods}

O {{site.data.keyword.amashort}} Client SDK é distribuído com CocoaPods, um gerenciador de dependências para projetos iOS. O CocoaPods faz o download automático de artefatos de repositórios e os disponibiliza para o aplicativo iOS. 

1. Abra o Terminal e execute o comando `pod --version`. Se você já tiver o CocoaPods instalado, o número da versão será exibido. É possível pular para a próxima seção deste tutorial.

1. Instale o CocoaPods executando `sudo gem install cocoapods`. Consulte o [website do CocoaPods](https://cocoapods.org/) se precisar de orientação adicional.

### Instalando o {{site.data.keyword.amashort}} Client SDK com CocoaPods
{: #facebook-auth-install-cocoapods}

1. Em seu projeto iOS, edite o `Podfile` e a linha a seguir:

	```
	pod 'IMFFacebookAuthentication'
	```

1. Salve o `Podfile` e execute o comando `pod install` a partir da linha de comandos. O CocoaPods instala as dependências. O progresso e quais componentes foram incluídos são exibidos. **Importante**: a partir desse ponto, deve-se abrir o seu projeto usando um arquivo `xcworkspace` que é gerado por CocoaPods. Normalmente, o nome é `{your-project-name}.xcworkspace`.  

1. Execute `open {your-project-name}.xcworkspace` a partir da linha de comandos para abrir sua área de trabalho do projeto iOS. 

### Configurando o projeto iOS para autenticação do Facebook
{: #facebook-auth-ios-configproject}

1. Localize o arquivo `info.plist`, normalmente localizado na pasta `Arquivos de apoio` em seu projeto Xcode.

1. Configure a integração do Facebook incluindo as propriedades a seguir em seu arquivo `info.plist`:

	![image](images/ios-facebook-infoplist-settings.png)

	Atualize o esquema URL e as propriedades FacebookappID com seu ID do aplicativo Facebook 

Também é possível atualizar o arquivo `info.plist` clicando com o botão direito no arquivo, selecionando **Abrir como > Código-fonte** e incluindo o XML a seguir:

	```
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
	Atualize o esquema URL e as propriedades FacebookappID com seu ID do aplicativo Facebook.

 **Importante**: assegure-se de não substituir quaisquer propriedades existentes no arquivo `info.plist`. Se você tiver propriedades de sobreposição, deverá mesclá-las manualmente. Para obter mais informações, consulte [Configurar o projeto Xcode](https://developers.facebook.com/docs/ios/getting-started/) e [Preparando seus apps para iOS9](https://developers.facebook.com/docs/ios/ios9).

## Inicializando o {{site.data.keyword.amashort}} Client SDK
{: #facebook-auth-ios-initalize}

Inicialize o Client SDK passando os parâmetros `applicationGUID` e `applicationRoute`.

Um local comum, mas não obrigatório, para colocar o código de inicialização é o método `application:didFinishLaunchingWithOptions` de delegado do seu aplicativo

1. Abra a página principal do painel do {{site.data.keyword.Bluemix_notm}} e clique em seu app. Clique em **Opções de dispositivo móvel**. Os valores *Rota do aplicativo* e *GUID do aplicativo* são exibidos.

1. Importe a estrutura necessária na classe em que deseja usar o {{site.data.keyword.amashort}} Client SDK incluindo os cabeçalhos a seguir:

	**Objective-C**

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFFacebookAuthentication/IMFFacebookAuthenticationHandler.h>
	#import <FacebookSDK/FacebookSDK.h>
```

	**Swift**

	O {{site.data.keyword.amashort}} Client SDK é implementado usando Objective-C, portanto pode ser necessário incluir um cabeçalho de ponte em seu projeto swift.

	1. Clique com o botão direito no projeto em Xcode e selecione **Novo arquivo...**
	* Na categoria **Origem iOS**, selecione `Arquivo de cabeçalho`
	* Atribua um nome a ele `BridgingHeader.h`
	* Inclua importações ao seu cabeçalho de ponte:

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFFacebookAuthentication/IMFFacebookAuthenticationHandler.h>
	#import <FacebookSDK/FacebookSDK.h>
```
	* Clique em seu projeto em Xcode e selecione a guia **Configurações de compilação**.
	* Procure por **Cabeçalho de ponte do Objective-C**.
	* Configure o valor para o local do seu arquivo `BridgingHeader.h`, por exemplo: `$(SRCROOT)/MyApp/BridgingHeader.h`.
	* Assegure-se de que seu cabeçalho de ponte esteja sendo selecionado pelo Xcode, compilando o seu projeto. Nenhuma mensagem de falha deve ser vista.

3. Inicialize o Client SDK. Substitua os valores applicationRoute e applicationGUID pelos valores obtidos a partir de **Opções de dispositivo móvel** no painel do {{site.data.keyword.Bluemix_notm}}.

	**Objective-C**

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	**Swift**

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",
	 							backendGUID: "applicationGUID")
	```



1. Notifique o SDK do Facebook sobre a ativação do app e registre o Manipulador de autenticação do Facebook incluindo o código a seguir no método `application:didFinishLaunchingWithOptions` no delegado do seu app. Inclua esse código imediatamente após a inicialização da instância IMFClient.

	**Objective-C**

	```Objective-C
		[FBAppEvents activateApp];
		[[IMFFacebookAuthenticationHandler sharedInstance] registerWithDefaultDelegate];
```

	**Swift**

	```Swift
		FBAppEvents.activateApp()
		IMFFacebookAuthenticationHandler.sharedInstance().registerWithDefaultDelegate()
```

1. Inclua o código a seguir no delegado do app.

	**Objective-C**

	```Objective-C
	- (BOOL)application:(UIApplication *)application openURL:(NSURL *)url
			sourceApplication:(NSString *)sourceApplication annotation:(id)annotation {

		return [FBAppCall handleOpenURL:url sourceApplication:sourceApplication];

	}
```

	**Swift**

	```Swift
	func application(application: UIApplication, openURL url: NSURL,
					sourceApplication: String?, annotation: AnyObject) -> Bool {

		return FBAppCall.handleOpenURL(url, sourceApplication: sourceApplication)

	}
```

## Testando a Autenticação
{: #facebook-auth-ios-testing}
Depois que o Client SDK for inicializado e o Gerenciador de autenticação do Facebook for registrado, será possível começar a fazer solicitações ao seu backend móvel.

### Antes de Começar
{: #facebook-auth-ios-testing-before}
Deve-se usar o texto padrão do {{site.data.keyword.mobilefirstbp}} e já ter um recurso protegido por {{site.data.keyword.amashort}} no terminal `/protected`. Se você precisar configurar um terminal `/protected`, veja [Protegendo recursos](protecting-resources.html).

1. Tente enviar uma solicitação para o terminal protegido de seu backend móvel recém-criado no navegador. Abra a URL a seguir: `http://{appRoute}/protected`.
Por exemplo: `http://my-mobile-backend.mybluemix.net/protected`
<br/>O terminal `/protected` de um backend móvel que foi criado com o texto padrão do MobileFirst Services Starter está protegido com o {{site.data.keyword.amashort}}. Uma mensagem `Unauthorized` é retornada no navegador. Essa
mensagem é retornada porque esse terminal pode ser acessado somente por aplicativos móveis que sejam instrumentados com o {{site.data.keyword.amashort}} Client SDK.

1. Use seu aplicativo iOS para fazer uma solicitação ao mesmo terminal.

	**Objective-C**

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
			NSLog("%@", IMFAuthorizationManager.sharedInstance().userIdentity)
		}
	}];
	```

	**Swift**

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

1. Clique em **OK** para autorizar o {{site.data.keyword.amashort}} a usar a identidade do usuário do Facebook para fins de autenticação.

1. 	Quando sua solicitação for bem-sucedida, a saída a seguir será exibida no console do Xcode:

	![image](images/ios-facebook-login-success.png)
