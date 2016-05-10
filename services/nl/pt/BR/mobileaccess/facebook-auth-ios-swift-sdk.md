---

copyright:
  years: 2016

---

# Ativando a autenticação do Facebook em apps iOS (Swift SDK)
{: #facebook-auth-ios}

Para usar o Facebook como provedor de identidade em seus aplicativos iOS, inclua e
configure a Plataforma iOS para seu aplicativo Facebook.

## Antes de iniciar
{: #facebook-auth-ios-before}

* Deve-se ter um recurso que seja protegido por {{site.data.keyword.amashort}} e um projeto iOS que seja instrumentado com o
{{site.data.keyword.amashort}} Client SDK.  Para obter mais informações, consulte
[Introdução
ao {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) e
[Configurando
o iOS Swift SDK](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios-swift-sdk.html).
* Proteja manualmente seu aplicativo backend com o {{site.data.keyword.amashort}} Server SDK. Para obter mais informações, consulte [Protegendo recursos](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).
* Crie um ID do aplicativo Facebook. Para obter mais informações, consulte [Obtendo um ID do aplicativo Facebook do Portal do Desenvolvedor do Facebook](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID).

## Configurando seu aplicativo Facebook para a plataforma iOS
{: #facebook-auth-ios-config}

1. Efetue log-in no [painel do
seu app do Facebook](https://developers.facebook.com/apps/).

1. Anote o **ID do app** do seu app. Esse valor é necessário ao
configurar seu projeto do iOS para autenticação do Facebook.

1. Clique em **Configurações > Incluir plataforma > iOS**.

1. Especifique o *bundleId* de seu aplicativo iOS. Para localizar o *bundleId* de seu aplicativo iOS, procure o **Identificador de pacote configurável** no arquivo `info.plist` ou na guia **Geral** do projeto Xcode.
**Dica**: considere a ativação do sufixo de esquema URL ou a Conexão única se estiver planejamento usar esses recursos.

1. Clique em **Salvar Configurações**.

## Configurando o {{site.data.keyword.amashort}} para autenticação do Facebook
{: #facebook-auth-ios-configmca}

Depois de configurado o ID do aplicativo Facebook e seu aplicativo Facebook para atender clientes iOS, é possível ativar a autenticação do Facebook no {{site.data.keyword.amashort}}.

1. Abra seu app no painel do {{site.data.keyword.Bluemix}}.

1. Clique em **Opções móveis** e anote a
**Rota** (*applicationRoute*) e o **GUID do
app** (*applicationGUID*). Eles serão necessários ao inicializar o SDK.

1. Clique no ladrilho {{site.data.keyword.amashort}}. O painel do {{site.data.keyword.amashort}} é carregado.

1. Clique no ladrilho **Facebook**.

1. Especifique o ID do aplicativo Facebook e clique em **Salvar**.

## Configurando o {{site.data.keyword.amashort}} Client SDK para iOS
{: #facebook-auth-ios-sdk}

### Instalando o CocoaPods
{: #facebook-auth-cocoapods}

O {{site.data.keyword.amashort}} Client SDK é distribuído com CocoaPods, um gerenciador de dependências para projetos iOS. O CocoaPods faz o download automático de artefatos de repositórios e os disponibiliza para o aplicativo iOS.

1. Abra o Terminal e execute o comando `pod --version`. Se você já tiver o CocoaPods instalado, o número da versão será exibido. É possível pular para a próxima seção deste tutorial.

1. Instale o CocoaPods executando `sudo gem install cocoapods`. Consulte o [website do CocoaPods](https://cocoapods.org/) se precisar de orientação adicional.

1. Feche o XCode.

1. Abra Terminal e `cd` no diretório de projeto.

1.  Execute `pod init`.

### Instalando o {{site.data.keyword.amashort}} Client Swift SDK com CocoaPods
{: #facebook-auth-install-swift-cocoapods}

1. Em seu projeto do iOS, edite o `Podfile` e inclua as linhas a
seguir:

 ```
use_frameworks!
pod 'BMSFacebookAuthentication'
	```
 **Dica:** é possível incluir `use_frameworks!` em seu destino Xcode em vez de tê-lo no Podfile.

1. Salve o `Podfile` e execute o comando `pod install` a partir da linha de comandos. O CocoaPods instala as dependências. O progresso e quais componentes foram incluídos são exibidos.

 **Importante**: deve-se abrir agora o projeto usando o arquivo
`xcworkspace` que é gerado pelo CocoaPods. Normalmente, o nome é `{your-project-name}.xcworkspace`.  

1. Execute `open {your-project-name}.xcworkspace` a partir da linha de comandos para abrir sua área de trabalho do projeto iOS.

### Configurando seu projeto do iOS para autenticação do Facebook
{: #facebook-auth-ios-configproject}

1. Localize o arquivo `info.plist`, normalmente localizado na pasta `Arquivos de apoio` em seu projeto Xcode.

1. Configure a integração do Facebook incluindo as propriedades a seguir em seu arquivo `info.plist`:

   ![image](images/ios-facebook-infoplist-settings.png)

   Atualize o esquema URL e as propriedades FacebookappID com seu ID do aplicativo Facebook

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
	<string>{your-faceebook-application-name}</string>
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
   Atualize o esquema URL e as propriedades FacebookappID com seu ID do aplicativo Facebook. Atualize
o FacebookDisplayName com o nome do seu aplicativo do Facebook.

    **Importante**: assegure-se de não substituir quaisquer propriedades existentes no arquivo `info.plist`. Se você tiver propriedades de sobreposição, deverá mesclá-las manualmente. Para obter mais informações, consulte [Configurar o projeto Xcode](https://developers.facebook.com/docs/ios/getting-started/) e [Preparando seus apps para iOS9](https://developers.facebook.com/docs/ios/ios9).

## Inicializando o {{site.data.keyword.amashort}} Client Swift SDK
{: #facebook-auth-ios-initalize-swift}

Inicialize o Client SDK passando os parâmetros `applicationGUID` e `applicationRoute`.

Um local comum, mas não obrigatório, para colocar o código de inicialização é o método `application:didFinishLaunchingWithOptions` de delegado do seu aplicativo

1. Obter valores de parâmetro do aplicativo. Abra seu app no painel do {{site.data.keyword.Bluemix_notm}}. Clique em **Opções de dispositivo móvel**. Os valores `applicationRoute` e `applicationGUID` são
exibidos nos campos **Rota** e **GUID do app**.

1. Importe a estrutura necessária na classe em que deseja usar o {{site.data.keyword.amashort}} Client SDK incluindo os cabeçalhos a seguir:

 ```swift
 import UIKit
 import BMSCore
 import BMSSecurity
 ```
2. Inicialize o Client SDK.	Substitua os valores
`<applicationRoute>` e `<applicationGUID>`
pelos valores de **Rota** e **GUID do app** que
você obteve das **Opções móveis** no painel
{{site.data.keyword.Bluemix_notm}}.

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<application Bluemix region>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

 FacebookAuthenticationManager.sharedInstance.register()
 ```

1. Notifique o Facebook SDK sobre a ativação do app e registre o Manipulador de
autenticação do Facebook incluindo o código a seguir no método
`application:didFinishLaunchingWithOptions` na delegação do app. Inclua
esse código imediatamente após a inicialização da instância BMSClient e registre o
Facebook como gerenciador de autenticação.

 ```Swift
  return FacebookAuthenticationManager.sharedInstance.onFinishLaunching(application, withOptions: launchOptions)
 ```

1. Copie o arquivo `FacebookAuthenticationManager.swift` dos
arquivos de origem pod `BMSFacebookAuthentication` para o diretório de
projeto.

1. Inclua o código a seguir no delegado do app.

 ```Swift
	func application(application: UIApplication, openURL url: NSURL, sourceApplication: String?,annotation: AnyObject) -> Bool {

		return FacebookAuthenticationManager.sharedInstance.onOpenURL(application, url: url, sourceApplication: sourceApplication, annotation: annotation)

	}
 ```

## Testando a Autenticação
{: #facebook-auth-ios-testing}

Depois que o Client SDK for inicializado e o Gerenciador de autenticação do Facebook for registrado, será possível começar a fazer solicitações ao seu backend móvel.

### Antes de iniciar
{: #facebook-auth-ios-testing-before}

Deve-se usar o modelo do {{site.data.keyword.mobilefirstbp}} e já ter um recurso protegido por {{site.data.keyword.amashort}} no terminal `/protected`. Se for necessário configurar um terminal `/protected`, consulte [Protegendo recursos](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

1. Tente enviar uma solicitação para o terminal protegido de seu backend móvel recém-criado no navegador. Abra a URL a seguir: `{applicationRoute}/protected`.
Por exemplo: `http://my-mobile-backend.mybluemix.net/protected`
<br/>O terminal `/protected` de um backend móvel que foi criado com o modelo do MobileFirst Services Starter está protegido com o {{site.data.keyword.amashort}}. Uma mensagem `Unauthorized` é retornada no navegador. Essa mensagem é retornada porque esse terminal só pode ser acessado somente por
aplicativos móveis instrumentados com o {{site.data.keyword.amashort}} Client SDK.

1. Use seu aplicativo iOS para fazer uma solicitação ao mesmo terminal.

	```Swift
  let protectedResourceURL = "<Your protected resource URL>" // any protected resource
  let request = Request(url: protectedResourceURL , method: HttpMethod.GET)
  let callBack:BmsCompletionHandler = {(response: Response?, error: NSError?) em

  if error == nil {
     print ("response:\(response?.responseText), no error")
  } else {
     print ("error: \(error)")
  }
  }

  request.sendWithCompletionHandler(callBack)
 ```

1. Execute o aplicativo. Uma tela de login do Facebook é exibida.

   ![image](images/ios-facebook-login.png)

   Essa tela poderá parecer um pouco diferente se você não estiver conectado ao Facebook no momento.

1. Clique em **OK** para autorizar o {{site.data.keyword.amashort}} a usar a identidade do usuário do Facebook para fins de autenticação.

1. 	Quando sua solicitação for bem-sucedida, a saída a seguir será exibida no console do Xcode:

 ```
 "onAuthenticationSuccess info = Optional({
     attributes =     {
     };
     deviceId = 218227041863639;
     displayName = "Don+Lon";
     isUserAuthenticated = 1;
     userId = 218227041863639;
 })
 response:Optional("Hello, this is a protected resouce of the mobile backend application!"), no error
 ```

1. Também é possível incluir a funcionalidade de logout incluindo o código a seguir:

 ```
FacebookAuthenticationManager.sharedInstance.logout(callBack)
```

 Se você chamar esse código depois que um usuário estiver conectado ao Facebook e ele tentar efetuar login novamente, ele será solicitado a autorizar o {{site.data.keyword.amashort}} a usar o Facebook para propósitos de autenticação.

 Para alternar usuários, deve-se chamar esse código e o usuário deve efetuar logout do Facebook em seu navegador.

 Passar ```callBack``` para a função de logout é opcional. Também é possível passar `nil`.
