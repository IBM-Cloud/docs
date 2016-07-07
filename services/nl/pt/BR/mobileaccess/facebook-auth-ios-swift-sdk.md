---

copyright:
  years: 2016

---
{:screen: .screen}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}

# Ativando a autenticação do Facebook para apps iOS (Swift SDK)
{: #facebook-auth-ios}

*Última atualização: 15 de junho de 2016*
{: .last-updated}

Para usar o Facebook como provedor de identidade em seus aplicativos iOS, inclua e
configure a Plataforma iOS para seu aplicativo Facebook.
{:shortdesc}

## Antes de iniciar
{: #facebook-auth-ios-before}
 Você deve ter
* Um projeto do iOS configurado para trabalhar com CocoaPods. Para obter mais informações, consulte **Instalar o CocoaPods** em [Configurando o iOS Swift SDK](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios-swift-sdk.html).
**Nota:** não é necessário instalar o {{site.data.keyword.amashort}} client SDK principal antes de continuar.
* Uma instância de um aplicativo {{site.data.keyword.Bluemix_notm}} que seja protegida pelo serviço {{site.data.keyword.amashort}}. Para obter mais informações sobre como criar um backend do {{site.data.keyword.Bluemix_notm}}, consulte [Introdução](index.html).
* Um ID de aplicativo do Facebook. Para obter mais informações, consulte [Obtendo um ID do aplicativo Facebook do Portal do Desenvolvedor do Facebook](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID).


**Importante:** não é necessário instalar separadamente o próprio SDK do Facebook. O Facebook SDK é instalado automaticamente pelo pod `BMSFacebookAuthentication` abaixo. É possível ignorar a etapa **Incluir o Facebook SDK em seu projeto do Xcode** no **Portal do Desenvolvedor do Facebook**.

**Nota:** embora o Objective-C SDK permaneça totalmente suportado e ainda seja considerado o SDK primário para o {{site.data.keyword.Bluemix_notm}} Mobile Services, há planos para descontinuar o Objective-C SDK posteriormente este ano em favor deste novo Swift SDK.
## Configurando seu aplicativo Facebook para a plataforma iOS
{: #facebook-auth-ios-config}

1. Efetue log-in no [painel do
seu app do Facebook](https://developers.facebook.com/apps/).

1. Anote o **ID do app** do seu app. Esse valor é necessário ao
configurar seu projeto do iOS para autenticação do Facebook.

1. Clique em **Configurações > Incluir plataforma > iOS**.

1. Especifique o *bundleId* de seu aplicativo iOS. Para localizar o *bundleId* de seu aplicativo iOS, procure o **Identificador de pacote configurável** no arquivo `info.plist` ou na guia **Geral** do projeto do Xcode.
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

## Configurando o {{site.data.keyword.amashort}} client SDK para iOS
{: #facebook-auth-ios-sdk}

### Instalando o CocoaPods
{: #install-cocoapods}

1. Abra o Terminal e execute o comando **pod --version**. Se você já tiver o CocoaPods instalado, o número da versão é exibido. É possível pular para a próxima seção para instalar o SDK.

1. Se você não tiver o CocoaPods instalado, execute:
```
sudo gem install cocoapods
```
Para obter mais informações, consulte o [website do
CocoaPods](https://cocoapods.org/).

### Instalando o {{site.data.keyword.amashort}} client Swift SDK com o CocoaPods
{: #facebook-auth-install-swift-cocoapods}

1. Se você não tiver nenhum `Podfile` em seu projeto do iOS, execute `pod init` para criar o arquivo.

1. Edite o `Podfile` e inclua as linhas a seguir:

 ```
use_frameworks!
pod 'BMSFacebookAuthentication'

	```

   **Nota:** se você tiver esta linha em seu arquivo pod: `pod 'BMSSecurity'`, ela deverá ser removida. O pod `BMSFacebookAuthentication` instala todas as estruturas necessárias.

   **Dica:** é possível incluir `use_frameworks!` em seu destino Xcode em vez de tê-lo no Podfile.

1. Salve o `Podfile` e execute o comando `pod install` a partir da linha de comandos. O CocoaPods instala as dependências. O progresso e quais componentes foram incluídos são exibidos.

 **Importante**: deve-se abrir agora o projeto usando o arquivo
`xcworkspace` que é gerado pelo CocoaPods. Normalmente, o nome é `{your-project-name}.xcworkspace`.  

1. Execute `open {your-project-name}.xcworkspace` a partir da linha de comandos para abrir sua área de trabalho do projeto iOS.

### Configurando seu projeto do iOS para autenticação do Facebook
{: #facebook-auth-ios-configproject}

1. Localize o arquivo `info.plist`, normalmente localizado na pasta `Arquivos de apoio` em seu projeto do Xcode.

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

## Inicializando o {{site.data.keyword.amashort}} client Swift SDK
{: #facebook-auth-ios-initalize-swift}

Inicialize o client SDK passando os parâmetros `applicationGUID` e `applicationRoute`.

Um local comum, mas não obrigatório, para colocar o código de inicialização é no método `application:didFinishLaunchingWithOptions` de delegado do seu aplicativo.

1. Obtenha os valores de parâmetros do aplicativo. Abra seu app no painel do {{site.data.keyword.Bluemix_notm}}. Clique em **Opções de dispositivo móvel**. Os valores `applicationRoute` e `applicationGUID` são
exibidos nos campos **Rota** e **GUID do app**.

1. Importe a estrutura necessária na classe em que deseja usar o {{site.data.keyword.amashort}} client SDK incluindo os cabeçalhos a seguir:

	```swift
 import UIKit
 import BMSCore
 import BMSSecurity
 ```
2. Inicialize o client SDK. Substitua os
valores `<applicationRoute>` e
`<applicationGUID>` pelos valores de **Rota** e
**GUID do app** que você obteve das **Opções
móveis** no painel {{site.data.keyword.Bluemix_notm}}.
Substitua `<applicationBluemixRegion>` pela região em que seu aplicativo {{site.data.keyword.Bluemix_notm}} está hospedado. Para visualizar sua região do {{site.data.keyword.Bluemix_notm}}, clique no ícone de face (![face](images/face.jpg "Ícone de Face")) no canto superior esquerdo do painel.

```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<applicationBluemixRegion>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

 FacebookAuthenticationManager.sharedInstance.register()
 ```

1. Notifique o Facebook SDK sobre a ativação do app e registre o Manipulador de autenticação do Facebook incluindo o código a seguir no método `application:didFinishLaunchingWithOptions` no delegado de seu app. Inclua
esse código imediatamente após a inicialização da instância BMSClient e registre o
Facebook como gerenciador de autenticação.

 ```Swift
  return FacebookAuthenticationManager.sharedInstance.onFinishLaunching(application, withOptions: launchOptions)
 ```

1. Copie o arquivo `FacebookAuthenticationManager.swift` dos arquivos de origem pod `BMSFacebookAuthentication` para o diretório de projeto.

1. Inclua o código a seguir no delegado de seu app.

	```Swift
	func application(application: UIApplication, openURL url: NSURL,
					sourceApplication: String?, annotation: AnyObject) -> Bool {

		return FacebookAuthenticationManager.sharedInstance.onOpenURL(application, url: url, sourceApplication: sourceApplication, annotation: annotation)

	}
 ```

## Testando a autenticação
{: #facebook-auth-ios-testing}

Após a inicialização do client SDK e o registro do Gerenciador de autenticação do Facebook, será possível começar a fazer solicitações para seu backend móvel.

### Antes de iniciar
{: #facebook-auth-ios-testing-before}

Deve-se usar o modelo do {{site.data.keyword.mobilefirstbp}} e já ter um recurso protegido por {{site.data.keyword.amashort}} no terminal `/protected`. Se for necessário configurar um terminal `/protected`, consulte [Protegendo recursos](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

1. Tente enviar uma solicitação para o terminal protegido de seu backend móvel recém-criado em seu navegador. Abra a URL a seguir: `{applicationRoute}/protected`.
Por exemplo: `http://my-mobile-backend.mybluemix.net/protected`
<br/>O terminal `/protected` de um backend móvel que foi criado com o modelo MobileFirst Services Starter está protegido com o {{site.data.keyword.amashort}}. Uma mensagem `Unauthorized` é retornada no navegador. Essa mensagem é retornada porque esse terminal só pode ser acessado somente por aplicativos móveis instrumentados com o {{site.data.keyword.amashort}} client SDK.

1. Use seu aplicativo iOS para fazer uma solicitação para o mesmo terminal.

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

1. Execute seu aplicativo. Uma tela de login do Facebook é exibida.
 
   ![image](images/ios-facebook-login.png)

   Essa tela poderá parecer um pouco diferente se você não estiver conectado ao Facebook no momento.

1. Clique em **OK** para autorizar o {{site.data.keyword.amashort}} a usar a identidade do usuário do Facebook para propósitos de autenticação.

1.	Quando sua solicitação for bem-sucedida, a saída a seguir será exibida no console do Xcode:

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
  {: screen}

1. Também é possível incluir a funcionalidade de logout incluindo o código a seguir:

 ```
FacebookAuthenticationManager.sharedInstance.logout(callBack)
```

 Se você chamar esse código depois que um usuário estiver conectado ao Facebook e ele tentar efetuar login novamente, ele será solicitado a autorizar o {{site.data.keyword.amashort}} a usar o Facebook para propósitos de autenticação.

 Para alternar usuários, deve-se chamar esse código e o usuário deve efetuar logout do Facebook em seu navegador.

 Passar `callBack` para a função de logout é opcional. Também é possível passar `nil`.
