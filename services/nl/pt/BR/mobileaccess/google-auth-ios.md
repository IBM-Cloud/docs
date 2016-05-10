---

copyright:
  years: 2015, 2016

---

# Ativando a autenticação do Google em apps iOS
{: #google-auth-ios}

**Dica:** Se você estiver desenvolvendo seu app iOS no Swift,
considere o {{site.data.keyword.amashort}} Client Swift SDK. As instruções nesta
página se aplicam ao {{site.data.keyword.amashort}} Client Objective-C SDK. Para
obter instruções sobre como usar o Swift SDK, consulte
[Ativando
a autenticação do Google em apps iOS (Swift SDK)](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html)

## Antes de Começar
{: #google-auth-ios-before}
* Deve-se ter um recurso que seja protegido pelo {{site.data.keyword.amashort}} e um projeto do iOS que seja instrumentado com o {{site.data.keyword.amashort}} Client SDK.  Para obter mais informações, consulte
[Introdução
ao {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) e
[Configurando
o iOS Objective-C SDK](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios.html).
* Proteja manualmente seu aplicativo backend com o {{site.data.keyword.amashort}} Server SDK. Para obter mais informações, consulte [Protegendo recursos](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).


## Configurando um projeto do Google para a plataforma iOS
{: #google-auth-ios-project}
Para iniciar o uso do Google como provedor de identidade, crie um projeto no Console do desenvolvedor do Google para obter um identificador de cliente do Google.  Esse identificador de cliente é um identificador exclusivo para que o Google saiba qual aplicativo está tentando se conectar.   Se você já tiver o projeto do Google, poderá ignorar as etapas que descrevem a criação do projeto e iniciar com a inclusão de credenciais.



1. Crie um projeto no [Console do desenvolvedor do Google](https://console.developers.google.com).
Se você já tiver um projeto, poderá ignorar as etapas que descrevem a criação do projeto e iniciar com a inclusão de credenciais.
   1.    Abra o menu do novo projeto. 
         
         ![image](images/FindProject.jpg)

   2.    Clique em **Criar um projeto**.
   
         ![image](images/CreateAProject.jpg)


1. Na lista **APIs sociais**, escolha **API do Google+**.

     ![image](images/chooseGooglePlus.jpg)

1. Clique em **Ativar** na próxima tela.

1. Selecione a guia **Tela de consentimento** e forneça o nome do produto mostrado aos usuários. Outros valores são opcionais. Clique em **Salvar**.

    ![image](images/consentScreen.png)
    
1. Na lista **Credenciais**, escolha o identificador de cliente OAuth.

     ![image](images/chooseCredentials.png)
     


1. Neste momento, será apresentada a você uma opção de tipo de aplicativo. Selecione **iOS**.

1. Forneça um nome significativo para seu cliente iOS. Especifique o ID do
pacote configurável do seu aplicativo iOS. Para descobrir o ID do pacote configurável do
seu aplicativo iOS, procure **Identificador de pacote configurável**
no arquivo `info.plist` ou na guia **Geral** do
projeto Xcode.

1. Anote seu novo identificador de cliente iOS. É necessário o valor ao configurar o aplicativo no {{site.data.keyword.Bluemix}}.


## Configurando o {{site.data.keyword.amashort}} para autenticação do Google
{: #google-auth-ios-config}

Agora que você possui um identificador de cliente iOS, poderá ativar a autenticação do Google no painel do {{site.data.keyword.Bluemix_notm}}.

1. Abra seu app no painel do {{site.data.keyword.Bluemix_notm}}.

1. Clique em **Opções móveis** e anote a
**Rota** (`applicationRoute`) e o **GUID do
app** (`applicationGUID`). Eles serão necessários ao inicializar o SDK.

1. Clique no ladrilho {{site.data.keyword.amashort}}. O painel do {{site.data.keyword.amashort}} é carregado.

1. Clique no ladrilho **Google**.

1. Em **ID do aplicativo para iOS**, especifique o ID do
cliente iOS para Android e clique em **Salvar**.

	Nota: além do identificador de cliente do Google, o valor reverso também é necessário para sua configuração do cliente (veja abaixo). Para acessar ambos os valores, faça download da plist de exemplo usando o ícone de lápis:
		![download do arquivo info.plist](images/download_plist.png)

## Configurando o {{site.data.keyword.amashort}} Client SDK para iOS
{: #google-auth-ios-sdk}

### Instalando o {{site.data.keyword.amashort}} Client SDK usando
CocoaPods
{: #google-auth-ios-sdk-cocoapods}

1. Navegue para seu projeto do iOS.

1. Edite o `Podfile` para incluir a linha a seguir:

	```
	pod 'IMFGoogleAuthentication'
	```

1. Salve o `Podfile` e execute `pod install` na
linha de comandos. O CocoaPods instala as dependências. Você verá o progresso e os componentes que foram incluídos.

  **Importante**: deve-se abrir agora o projeto usando o arquivo
`xcworkspace` que é gerado pelo CocoaPods. Normalmente, o nome é `{your-project-name}.xcworkspace`.  

1. Execute `open {your-project-name}.xcworkspace` na linha de
comandos para abrir sua área de trabalho de projeto do iOS.

### Configurando o projeto do iOS para autenticação do Google
{: #google-auth-ios-googleauth}
Configure a integração do Google atualizando o arquivo `info.plist`. O
arquivo `info.plist` normalmente está na pasta `Arquivos de
apoio` em seu projeto Xcode. É possível editar o arquivo no editor de lista de propriedades ou com um editor de texto.

* Configure a integração do Google incluindo os esquemas de URL a seguir no
arquivo `info.plist`
	![info.plist file](images/ios-google-infoplist-settings.png)

	O primeiro Esquema de URL é uma versão reservada do ID do cliente do Google
Developer Console.  Por exemplo, se o ID do cliente for
`123123-abcabc.apps.googleusercontent.com`, o Esquema de URL será:
`com.googleusercontent.apps.123123-abcabc`. 

	O segundo Esquema de URL é o ID do pacote configurável de seu aplicativo

* Utilize um editor de texto. Clique com o botão direito em
`info.plist` e selecione **Abrir como > Código fonte**. Inclua
o XML a seguir no arquivo:

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
	Atualize ambos os Esquemas de URL.

	**Importante**: Não substitua qualquer propriedade existente
no arquivo `info.plist`. Se você tiver propriedades de sobreposição,
precisará mesclar as propriedades manualmente. Para obter mais informações, consulte
[Tentar
Sign-In para iOS](https://developers.google.com/identity/sign-in/ios/start).

## Inicializando o {{site.data.keyword.amashort}} Client SDK
{: #google-auth-ios-initialize}

Para usar o {{site.data.keyword.amashort}} Client SDK, inicialize-o
passando os parâmetros applicationGUID e applicationRoute.

Um local comum, mas não obrigatório, para colocar o código de inicialização é o método `application:didFinishLaunchingWithOptions` de delegado do seu aplicativo.

1. Obtenha os valores applicationGUID e applicationRoute. No painel
{{site.data.keyword.Bluemix_notm}}, clique em seu app. Clique em **Opções de dispositivo móvel**. Os valores Application Route e Application GUID são exibidos.

1. Importe as estruturas necessárias na classe em que você deseja usar o
{{site.data.keyword.amashort}} Client SDK. Inclua os cabeçalhos a seguir:

	Objective-C:

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>
	```

	Swift:

	O {{site.data.keyword.amashort}} Client SDK é implementado com Objective-C. Pode ser necessário incluir um cabeçalho de ponte em seu projeto Swift para usar o SDK.

	1. Clique com o botão direito no projeto em Xcode e selecione **Novo arquivo...**
	2. Na categoria **Origem iOS**, selecione **Arquivo de cabeçalho**.
	3. Dê o nome `BridgingHeader.h`
	4. Inclua as importações a seguir em seu cabeçalho de ponte:

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>
	```
	5. Clique em seu projeto em Xcode e selecione a guia **Configurações de compilação**.
	6. Procure por `Cabeçalho de ponte do Objective-C`.
	7. Configure o valor para o local do seu arquivo `BridgingHeader.h`, por exemplo: `$(SRCROOT)/MyApp/BridgingHeader.h`.
	8. Assegure-se de que seu cabeçalho de ponte esteja sendo selecionado pelo Xcode, compilando o seu projeto.

3. Use o código a seguir para inicializar o Client SDK.  Substitua
*applicationRoute* e *applicationGUID* pelos valores de
**Rota** e **GUID do app** que você obteve das
**Opções móveis**.

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



1. Registre o Manipulador de autenticação do Google incluindo o código a seguir no
método `application:didFinishLaunchingWithOptions` na delegação do seu
app. Inclua este código imediatamente após a inicialização do IMFClient:

	Objective-C:

	```Objective-C
	[[IMFGoogleAuthenticationHandler sharedInstance] registerWithDefaultDelegate];
	```

	Swift:

	```Swift
	IMFGoogleAuthenticationHandler.sharedInstance().registerWithDefaultDelegate()
	```

1. Inclua o código a seguir no delegado do app.

	Objective-C:

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

	Swift:

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
Deve-se estar usando o modelo do {{site.data.keyword.mobilefirstbp}} e já ter um recurso protegido pelo {{site.data.keyword.amashort}} no terminal `/protected`. Se for necessário configurar um terminal `/protected`, consulte [Protegendo recursos](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).


1. Tente enviar uma solicitação para o terminal protegido de seu backend móvel no
navegador do desktop abrindo `{applicationRoute}/protected`, por
exemplo, `http://my-mobile-backend.mybluemix.net/protected`

1. O terminal `/protected` de um backend móvel criado com o Modelo do MobileFirst Services é protegido com o {{site.data.keyword.amashort}}, portanto, ele só pode ser acessado por aplicativos móveis instrumentados com o {{site.data.keyword.amashort}} Client SDK. Como resultado, você verá `Unauthorized` no navegador de sua área de trabalho.

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

1. Execute o aplicativo. Você verá um pop-up da tela de Login do Google

	![image](images/ios-google-login.png)

	Essa tela poderá parecer um pouco diferente se o app Facebook não estiver instalado em seu dispositivo, ou se você não estiver atualmente conectado ao Facebook.

1. Ao clicar em **OK** você está autorizando o {{site.data.keyword.amashort}} a usar sua identidade de usuário do Google para propósitos de autenticação.

1. 	Sua solicitação deve ser bem-sucedida. Você deverá ver a saída a seguir no LogCat

	![image](images/ios-google-login-success.png)
	
	
	Também é possível incluir a funcionalidade de logout incluindo o código a seguir:
	
	Objective C:
	
	```Objective-C
	[[IMFGoogleAuthenticationHandler sharedInstance] logout : callBack]
	```

	Swift:

	```Swift
	IMFGoogleAuthenticationHandler.sharedInstance().logout(callBack)
	```


	Se você chamar esse código depois que um usuário estiver conectado ao Google e ele tentar efetuar login novamente, ele será solicitado a autorizar o Mobile Client Access a usar o Google para propósitos de autenticação. Neste ponto, o usuário pode clicar no nome do usuário no canto superior direito da tela para selecionar e efetuar login com outro usuário.

	Passar `callBack` para a função de logout é opcional. Também é possível passar `nil`.
