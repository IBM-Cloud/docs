---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-01"

---

{:screen: .screen}
{:shortdesc: .shortdesc}


# Ativando a autenticação do Google para apps iOS Objective C
{: #google-auth-ios}


Use o Google Sign-In para autenticar usuários no app
{{site.data.keyword.amafull}} iOS.

**Nota:** embora o Objective-C SDK permaneça totalmente suportado e ainda seja considerado o SDK primário para o {{site.data.keyword.Bluemix_notm}} Mobile Services, há planos para descontinuar esse SDK posteriormente este ano em favor do novo Swift SDK. Para novos aplicativos, é altamente recomendável usar o Swift SDK. As instruções nesta página se aplicam ao {{site.data.keyword.amashort}} client Objective-C SDK. Para obter instruções sobre como usar o Swift SDK, consulte [Ativando a autenticação do Google em apps iOS (Swift SDK)](https://console.{DomainName}/docs/services/mobileaccess/google-auth-ios-swift-sdk.html).

## Antes de Começar
{: #before-you-begin}
Você deve ter:
* Uma instância de um serviço
{{site.data.keyword.amafull}} e um aplicativo
{{site.data.keyword.Bluemix_notm}}. Para obter mais informações sobre como criar um aplicativo backend do {{site.data.keyword.Bluemix_notm}}, consulte [Introdução](index.html).
* A URL do seu aplicativo backend (**Rota de App**). Você precisará desse valor para enviar
solicitações para os terminais protegido do seu aplicativo
backend.
* Seu valor **TenantID**. Abra o seu serviço no painel do {{site.data.keyword.amashort}}. Clique no botão **Opções móveis**. O valor
`tenantId` (também conhecido como
`appGUID`) é exibido no campo **App
GUID / TenantId**. Você precisará desse valor para
inicializar o Gerenciador de Autorização.

## Configurando um projeto do Google para a plataforma iOS
{: #google-auth-ios-project}
Para iniciar o uso do Google como provedor de identidade, crie um projeto no Console do desenvolvedor do Google para obter um identificador de cliente do Google.  Esse identificador de cliente é um identificador exclusivo para que o Google saiba qual aplicativo está tentando se conectar.   

1. Se você não tiver criado um projeto do Google iOS, siga as etapas no site [Google Developer
Console](https://console.developers.google.com).

1. A partir da lista de **APIs sociais**, escolha **API do Google+** e clique em **Ativar**.

1. A partir da lista de **Credenciais**, clique no botão **Criar credenciais** e escolha **Identificador de cliente
do OAuth**.

1. Neste momento, será apresentada a você uma opção de tipo de aplicativo. Selecione **iOS**.

1. Forneça um nome significativo para seu cliente iOS. Especifique o ID do
pacote configurável do seu aplicativo iOS. Para descobrir o ID do pacote configurável do
seu aplicativo iOS, procure **Identificador de pacote configurável**
no arquivo `info.plist` ou na guia **Geral** do
projeto Xcode.

1. Tome nota de seu novo identificador de cliente do Google iOS. É necessário o valor ao configurar o aplicativo no {{site.data.keyword.Bluemix}}.




## Configurando o {{site.data.keyword.amashort}} para autenticação do Google
{: #google-auth-ios-config}

Agora que você tem um identificador de cliente do Google iOS, é possível ativar a autenticação do Google no painel do {{site.data.keyword.Bluemix_notm}}.

1. Abra o seu serviço no painel do {{site.data.keyword.amashort}}.
1. Na guia **Gerenciar**, acione
**Autorização**.
1. Expanda a seção **Google**.
1. Em **ID do aplicativo para iOS**,
especifique o ID de cliente do Google para iOS.
1. Clique em **Salvar**.


## Configurando o {{site.data.keyword.amashort}} Google client SDK for iOS
{: #google-auth-ios-sdk}

### Instalando o {{site.data.keyword.amashort}} client SDK usando o CocoaPods
{: #google-auth-ios-sdk-cocoapods}

1. Navegue para seu projeto do iOS.

1. Edite o `Podfile` para incluir a linha a seguir:

	```
	pod 'IMFGoogleAuthentication'
	```
{: codeblock}

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

	O primeiro Esquema de URL é uma versão reversa do identificador de cliente do Console do desenvolvedor do Google.  Por exemplo, se o identificador de cliente for `123123-abcabc.apps.googleusercontent.com`, o Esquema de URL será: `com.googleusercontent.apps.123123-abcabc`.

	O segundo Esquema de URL é o ID do pacote configurável de seu aplicativo

* Utilize um editor de texto. Clique com o botão direito em `info.plist` e selecione **Abrir como > Código-fonte**. Inclua
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
{: codeblock}

	Atualize ambos os Esquemas de URL.

	**Importante**: Não substitua qualquer propriedade existente
no arquivo `info.plist`. Se você tiver propriedades de sobreposição,
precisará mesclar as propriedades manualmente. Para obter mais informações, veja
[Tentar conexão para iOS](https://developers.google.com/identity/sign-in/ios/start).

## Inicializando o {{site.data.keyword.amashort}} client SDK
{: #google-auth-ios-initialize}

Para usar o cliente
SDK {{site.data.keyword.amashort}}, inicialize-o
passando o TenantID e os parâmetros de rota do
app.

Um local comum, mas não obrigatório, para colocar o código de inicialização é o método `application:didFinishLaunchingWithOptions` de delegado do seu aplicativo.

1. Importe as estruturas necessárias na classe em que você deseja usar o {{site.data.keyword.amashort}} client SDK. Inclua os cabeçalhos a seguir:

	#### Objective-C:

	```Objective-C
	#import <IMFCore/IMFCore.h>
	#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>
	```
{: codeblock}

	#### Swift:

	O {{site.data.keyword.amashort}} client SDK é implementado com Objective-C. Pode ser necessário incluir um cabeçalho de ponte em seu projeto Swift para usar o SDK.

	1. Clique com o botão direito no Xcode e selecione **Novo arquivo...**.

	2. Na categoria **Origem iOS**, selecione **Arquivo de cabeçalho**.

	3. Denomine-o `BridgingHeader.h`.

	4. Inclua as importações a seguir em seu cabeçalho de ponte:
		
	   `#import <IMFCore/IMFCore.h>`
		
	   `#import <IMFGoogleAuthentication/IMFGoogleAuthenticationHandler.h>`
	
	5. Clique em seu projeto em Xcode e selecione a guia **Configurações de compilação**.

	6. Procure por `Cabeçalho de ponte do Objective-C`.

	7. Configure o valor para o local do seu arquivo `BridgingHeader.h`, por exemplo: `$(SRCROOT)/MyApp/BridgingHeader.h`.

	8. Assegure-se de que seu cabeçalho de ponte esteja sendo selecionado pelo Xcode, compilando o seu projeto.

3. Use o código a seguir para inicializar o client SDK.  Substitua `< applicationRoute>` e
`< TenantID>` pela
**Route** e **TenantID**.

	#### Objective-C:

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"<applicationRoute>"
			backendGUID:@"<TenantID>"];
	```
{: codeblock}

	#### Swift:

	```Swift
	IMFClient.sharedInstance().initializeWithBackendRoute("<applicationRoute>",
	 							backendGUID: "<TenantID>")
	```
{: codeblock}

1. Inicialize o `AuthorizationManager` passando o parâmetro
`tenantId` do serviço {{site.data.keyword.amashort}}. 
  ####Objective-C
	
  ```Objective-C
     [[IMFAuthorizationManager sharedInstance]  initializeWithTenantId: @"tenantId"];
  ```
 {: codeblock}

  ####Swift

  ```Swift
  IMFAuthorizationManager.sharedInstance().initializeWithTenantId("tenantId")
  ```
 {: codeblock}

1. Registre o Manipulador de autenticação do Google incluindo o código a seguir no
método `application:didFinishLaunchingWithOptions` na delegação do seu
app. Inclua este código imediatamente após a inicialização do IMFClient:

	#### Objective-C:

	```Objective-C
	[[IMFGoogleAuthenticationHandler sharedInstance] registerWithDefaultDelegate];
	```
{: codeblock}

	#### Swift:

	```Swift
	IMFGoogleAuthenticationHandler.sharedInstance().registerWithDefaultDelegate()
	```
{: codeblock}

1. Inclua o código a seguir no delegado do app.

	#### Objective-C:

	```Objective-C
	- (void)applicationDidBecomeActive:(UIApplication *)application {
		[[IMFGoogleAuthenticationHandler sharedInstance] handleDidBecomeActive];
	}

	- (BOOL)application: (UIApplication *)application openURL: (NSURL *)url sourceApplication: (NSString *)sourceApplication annotation: (id)annotation {

		BOOL shouldHandleGoogleURL = [GPPURLHandler handleURL:url sourceApplication:sourceApplication annotation:annotation];

		[[IMFGoogleAuthenticationHandler sharedInstance] handleOpenURL:shouldHandleGoogleURL];
		return  shouldHandleGoogleURL;
	}
	```
{: codeblock}

	#### Swift:

	```Swift
	func application(application: UIApplication, openURL url: NSURL,
					sourceApplication: String?, annotation: AnyObject) -> Bool {

		let shouldHandleGoogleURL = GPPURLHandler.handleURL(url,
				sourceApplication: sourceApplication, annotation: annotation)

		IMFGoogleAuthenticationHandler.sharedInstance().handleOpenURL(shouldHandleGoogleURL)

		return shouldHandleGoogleURL;
	}
```
{: codeblock}

## Testando a Autenticação
{: #google-auth-ios-testing}
Após a inicialização do client SDK, é possível começar a fazer solicitações para seu backend móvel.

### Antes de Começar
{: #google-auth-ios-testing-before}
Deve-se usar o modelo do {{site.data.keyword.mobilefirstbp}} e já ter um recurso protegido por {{site.data.keyword.amashort}} no terminal `/protected`. Se for necessário configurar um terminal `/protected`, consulte [Protegendo recursos](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).


1. Tente enviar uma solicitação para o terminal protegido de seu backend móvel no
navegador do desktop abrindo `{applicationRoute}/protected`, por
exemplo, `http://my-mobile-backend.mybluemix.net/protected`

1. O terminal `/protected` de um backend móvel criado com o Modelo do MobileFirst Services está protegido com o {{site.data.keyword.amashort}}; portanto, ele só pode ser acessado por aplicativos móveis instrumentados com o {{site.data.keyword.amashort}} client SDK. Como resultado, você verá `Unauthorized` no navegador de sua área de trabalho.

1. Use seu aplicativo iOS para fazer solicitação para o mesmo terminal.

	#### Objective-C:

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
{: codeblock}

	#### Swift:

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
{: codeblock}

1. Execute o aplicativo. Você verá um pop-up da tela de Login do Google

	![image](images/ios-google-login.png)

	Essa tela poderá parecer um pouco diferente se o app Facebook não estiver instalado em seu dispositivo, ou se você não estiver atualmente conectado ao Facebook.

1. Ao clicar em **OK** você está autorizando o {{site.data.keyword.amashort}} a usar sua identidade de usuário do Google para propósitos de autenticação.

1. 	Sua solicitação deve ser bem-sucedida. Você deverá ver a saída a seguir no LogCat

	![image](images/ios-google-login-success.png)
		
	Também é possível incluir a funcionalidade de logout incluindo o código a seguir:

	#### Objective C:

	```Objective-C
	[[IMFGoogleAuthenticationHandler sharedInstance] logout : callBack]
	```
{: codeblock}

	#### Swift:

	```Swift
	IMFGoogleAuthenticationHandler.sharedInstance().logout(callBack)
	```
{: codeblock}

	Se você chamar esse código depois que um usuário estiver conectado ao Google e ele tentar efetuar login novamente, ele será solicitado a autorizar o {{site.data.keyword.amashort}} a usar o Google para propósitos de autenticação. Neste
ponto, o usuário pode clicar no nome do usuário <!--in the upper-right corner of the screen--> para selecionar e efetuar login com outro usuário.

	Passar `callBack` para a função de logout é opcional. Também é possível passar `nil`.
