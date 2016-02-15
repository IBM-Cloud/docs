# Ativando a autenticação do Google em apps iOS
{: #google-auth-ios}

## Antes de Começar
{: #google-auth-ios-before}
* Deve-se ter um recurso que seja protegido pelo {{site.data.keyword.amashort}} e um projeto do iOS que seja instrumentado com o {{site.data.keyword.amashort}} Client SDK. Para obter mais informações, consulte [Introdução ao {{site.data.keyword.amashort}}](getting-started.html) e [Configurando o iOS SDK](getting-started-ios.html).  
* Proteja manualmente seu aplicativo backend com o {{site.data.keyword.amashort}} Server SDK. Para obter mais informações, consulte [Protegendo recursos](protecting-resources.html).


## Configurando um projeto do Google para a plataforma iOS
{: #google-auth-ios-project}
Para iniciar o uso do Google como provedor de identidade, crie um projeto no Console do desenvolvedor do Google para obter um identificador de cliente do Google. Esse identificador de cliente é um identificador exclusivo para que o Google saiba qual aplicativo está tentando se conectar. Se você já tiver o projeto do Google, poderá ignorar as etapas que descrevem a criação do projeto e iniciar com a inclusão de credenciais.

1. Abra o [Console do desenvolvedor do Google](https://console.developers.google.com).

1. Crie um projeto. Clique em **Criar projeto**.

1. Selecione seu projeto e clique em **Usar APIs do Google**. Também é possível clicar em **Ativar APIs e obter credenciais como chaves**.

1. Na lista de APIs, escolha a API Google+ e clique em **Ativar API**.

1. Clique em **Credenciais > Incluir credenciais** e selecione **Identificador de cliente OAuth 2.0**.

1. Você pode ser solicitado a configurar um nome de produto no console de consentimento. Continue para fazer isso.

1. Neste momento, será apresentada a você uma opção de tipo de aplicativo. Selecione **iOS**.

1. Forneça um nome significativo para seu cliente iOS. Especifique o bundleId do aplicativo iOS. Para localizar o bundleId de seu aplicativo iOS, procure **Identificador de pacote configurável** no arquivo `info.plist` ou na guia **Geral** do projeto do Xcode.

1. Anote seu novo identificador de cliente iOS. É necessário o valor ao configurar o aplicativo no {{site.data.keyword.Bluemix_notm}}.


## Configurando o {{site.data.keyword.amashort}} para autenticação do Google
{: #google-auth-ios-config}

Agora que você possui um identificador de cliente iOS, poderá ativar a autenticação do Google no painel do {{site.data.keyword.Bluemix_notm}}.

1. Abra o Painel do {{site.data.keyword.Bluemix}} e clique no aplicativo {{site.data.keyword.Bluemix_notm}}

1. Clique em **Opções de dispositivo móvel** e anote os valores *applicationRoute* e *applicationGUID*. Esses valores serão necessários para inicializar o SDK.

1. Clique em um quadro do {{site.data.keyword.amashort}}

1. Você atingirá o Painel do {{site.data.keyword.amashort}}

1. Clique em **Configurar a autenticação**

1. Clique em **Google**

1. Especifique o identificador de cliente para iOS obtido nas etapas anteriores e clique em **Salvar**

## Configurando o {{site.data.keyword.amashort}} Client SDK para iOS
{: #google-auth-ios-sdk}

### Instalando o {{site.data.keyword.amashort}} Client SDK usando Cocoapods
{: #google-auth-ios-sdk-cocoapods}

1. Navegue para o projeto do iOS

1. Edite o `Podfile` e inclua a linha abaixo no destino requerido

	```
	pod 'IMFGoogleAuthentication'
	```

1. Salve o `Podfile` e execute `pod install` a partir da linha de comandos

1. O Cocoapods instalará as dependências incluídas. Você verá o progresso e os componentes que foram incluídos.

	> Deste ponto em diante, você sempre precisará abrir seu projeto usando um arquivo xcworkspace gerado pelo Cocoapods. Em geral, o nome é {your-project-name}.xcworkspace.  

1. Execute `open {your-project-name}.xcworkspace` a partir da linha de comandos para abrir sua área de trabalho do projeto do iOS

### Configurando o projeto do iOS para autenticação do Google
{: #google-auth-ios-googleauth}

1. Localize o arquivo `info.plist`, localizado geralmente na pasta `Arquivos de suporte` no projeto do Xcode

1. Configure a integração do Google, incluindo os dois esquemas URL abaixo no arquivo `info.plist`

	![image](images/ios-google-infoplist-settings.png)

	> O primeiro Esquema de URL é o identificador de cliente invertido obtido no Console do desenvolvedor do Google. Por exemplo: se seu identificador de cliente for `123123-abcabc.apps.googleusercontent.com`, seu Esquema de URL deverá ser `com.googleusercontent.apps.123123-abcabc`

	> O segundo Esquema de URL é um ID do pacote configurável de seu aplicativo

1. Como alternativa, é possível atualizar o arquivo `info.plist` clicando com o botão direito nele, selecionando `Abrir como` -> `Código-fonte` e incluindo o XML abaixo

	```XML
	<key>CFBundleURLTypes</key>
	<array>
		<dict>
			<key>CFBundleTypeRole</key>
			<string>Editor</string>
			<key>CFBundleURLSchemes</key>
			<array>
				<string>com.googleusercontent.apps.123123-abcabc</string>
			</array>
		</dict>
		<dict>
			<key>CFBundleTypeRole</key>
			<string>Editor</string>
			<key>CFBundleURLSchemes</key>
			<array>
				<string>com.ibm.HelloWorld</string>
			</array>
		</dict>
	</array>

	```
	> Atualize ambos os Esquemas de URL conforme descritos acima

	> Certifique-se de que não esteja substituindo propriedades existentes em `info.plist`. Se você tiver propriedades de sobreposição, será necessário mesclar manualmente. Consulte as seções [Tentar conectar-se para o iOS](https://developers.google.com/identity/sign-in/ios/start) da documentação do Google para obter informações adicionais.

## Inicializando o {{site.data.keyword.amashort}} Client SDK
{: #google-auth-ios-initialize}

Para ser capaz de usar o {{site.data.keyword.amashort}} Client SDK, será necessário inicializá-lo passando os parâmetros applicationGUID e applicationRoute.

> Um local comum, mas não obrigatório, para colocar o código de inicialização é no método `application:didFinishLaunchingWithOptions` de de delegado do seu aplicativo. 1. Abra a página principal do Painel do {{site.data.keyword.Bluemix_notm}} e clique no app criado anteriormente. Isso abrirá o painel do app backend do dispositivo móvel.

2. Clique em `Opções de dispositivo móvel` na parte superior direita do painel. Os valores de Rota do aplicativo e GUID do aplicativo serão exibidos.

1. Importe a estrutura necessária na classe que você deseja usar o {{site.data.keyword.amashort}} Client SDK, incluindo os cabeçalhos abaixo

	Aplicativos Objective-C:

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>
	```

	Aplicativos Swift:

	O {{site.data.keyword.amashort}} Client SDK é implementado usando Objective-C, portanto, pode ser necessário incluir um cabeçalho de ponte no projeto swift para que seja possível utilizá-lo.

	* Clique com o botão direito no projeto no Xcode e selecione `Novo arquivo...`
	* Na categoria `Origem do iOS`, selecione `Arquivo de cabeçalho`
	* Dê o nome `BridgingHeader.h`
	* Inclua as importações abaixo no cabeçalho de ponte

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>
	```
	* Clique no projeto no Xcode e selecione a guia `Configurações de compilação`
	* Procure `Cabeçalho de ponte do Objective-C`
	* Configure o valor para o local de seu arquivo `BridgingHeader.h`, por exemplo, `$(SRCROOT)/MyApp/BridgingHeader.h`
	* Certifique-se de que seu cabeçalho de ponte esteja sendo assimilado pelo Xcode ao construir seu projeto; você não deve ver mensagens de falha

3. Use o código abaixo para inicializar o Client SDK

	Aplicativos Objective-C:

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	Aplicativos Swift:

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",
	 							backendGUID: "applicationGUID")
	```

	> Substitua applicationRoute e applicationGUID pelos valores obtidos de Opções de dispositivo móvel

1. Registre o Manipulador de autenticação do Google incluindo o código abaixo no método `application:didFinishLaunchingWithOptions` no app delegado. Recomenda-se fazer isso logo após a inicialização do IMFClient

	Aplicativos Objective-C:

	```Objective-C
	[[IMFGoogleAuthenticationHandler sharedInstance] registerWithDefaultDelegate];
	```

	Aplicativos Swift:

	```Swift
	IMFGoogleAuthenticationHandler.sharedInstance().registerWithDefaultDelegate()
	```

1. Inclua o código abaixo no app delegado

	Aplicativos Objective-C:

	```Objective-C
	- (void)applicationDidBecomeActive:(UIApplication *)application {
		[[IMFGoogleAuthenticationHandler sharedInstance] handleDidBecomeActive];
	}

	- (BOOL)application: (UIApplication *)application openURL: (NSURL *)url
					sourceApplication: (NSString *)sourceApplication annotation: (id)annotation {

		BOOL shouldHandleGoogleURL = [GPPURLHandler handleURL:url sourceApplication:sourceApplication annotation:annotation];

		[[IMFGoogleAuthenticationHandler sharedInstance] handleOpenURL:shouldHandleGoogleURL];
		return  shouldHandleGoogleURL;
	}
	```

	Aplicativos Swift:

	```Swift
	func application(application: UIApplication, openURL url: NSURL,
					sourceApplication: String?, annotation: AnyObject) -> Bool {

		let shouldHandleGoogleURL = GPPURLHandler.handleURL(url,
				sourceApplication: sourceApplication, annotation: annotation)

		IMFGoogleAuthenticationHandler.sharedInstance().handleOpenURL(shouldHandleGoogleURL)

		return shouldHandleGoogleURL;
	}
```

## Testando a Autenticação
{: #google-auth-ios-testing}
Após a inicialização do Client SDK, é possível começar a fazer solicitações para seu backend móvel.

### Antes de Começar
{: #google-auth-ios-testing-before}
Deve-se estar usando o texto padrão do {{site.data.keyword.mobilefirstbp}} e já ter um recurso protegido pelo {{site.data.keyword.amashort}} no terminal `/protected`. Se for necessário configurar um terminal `/protected`, consulte [Protegendo recursos](protecting-resources.html).


1. Tente enviar uma solicitação para o terminal protegido de seu backend móvel no navegador de sua área de trabalho abrindo `http://{appRoute}/protected`, por exemplo, `http://my-mobile-backend.mybluemix.net/protected`

1. O terminal `/protected` de um backend móvel criado com o Texto padrão do MobileFirst Services é protegido com o {{site.data.keyword.amashort}}, portanto, ele só pode ser acessado por aplicativos móveis instrumentados com o {{site.data.keyword.amashort}} Client SDK. Como resultado, você verá `Unauthorized` no navegador de sua área de trabalho.

1. Use seu aplicativo iOS para fazer solicitação para o mesmo terminal.

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
			NSLog("%@", IMFAuthorizationManager.sharedInstance().userIdentity)
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

1. Execute o aplicativo. Você verá um pop-up da tela de Login do Google

	![image](images/ios-google-login.png)

	Essa tela poderá parecer um pouco diferente se o app Facebook não estiver instalado em seu dispositivo, ou se você não estiver atualmente conectado ao Facebook.

1. Ao clicar em **OK** você está autorizando o {{site.data.keyword.amashort}} a usar sua identidade de usuário do Google para propósitos de autenticação.

1. 	Sua solicitação deve ser bem-sucedida. Você deverá ver a saída a seguir no LogCat

	![image](images/ios-google-login-success.png)
