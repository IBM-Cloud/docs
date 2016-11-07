---

copyright:
  years: 2016 lastupdated: "2016-10-09"
---
{:screen:  .screen}
{:shortdesc: .shortdesc}

# Ativando a autenticação do Google para apps iOS (Swift SDK)
{: #google-auth-ios}

Use o Google Sign-In para autenticar usuários no app
{{site.data.keyword.amafull}} iOS Swift. O {{site.data.keyword.amashort}} Swift SDK recém-liberado inclui e melhora a funcionalidade fornecida pelo Mobile Client Access Objective-C SDK existente.

**Nota:** embora o Objective-C SDK permaneça totalmente suportado e ainda seja considerado o SDK primário para o {{site.data.keyword.Bluemix_notm}} Mobile Services, há planos para descontinuar o Objective-C SDK posteriormente este ano em favor deste novo Swift SDK.



## Antes de iniciar
{: #google-auth-ios-before}
Você deve ter:

* Um projeto do iOS em Xcode. Ele não precisa ser instrumentado com o {{site.data.keyword.amashort}} client SDK.  
* Uma instância de um aplicativo {{site.data.keyword.Bluemix_notm}} que seja protegida pelo serviço {{site.data.keyword.amashort}}. Para obter mais informações sobre como criar um aplicativo backend do {{site.data.keyword.Bluemix_notm}}, consulte [Introdução](index.html).


## Preparando seu app para o Google Sign-In
{: #google-sign-in-ios}

Prepare seu app para o Google Sign-in seguindo as instruções fornecidas pelo Google em [Google Sign-In for iOS](https://developers.google.com/identity/sign-in/ios/start-integrating). 

Este processo:
* prepara um novo projeto no site do Google Developers, 
* cria o arquivo `GoogleService-Info.plist` e o valor `REVERSE_CLIENT_ID` para inclusão em seu projeto do Xcode e
* cria o **identificador de cliente do Google** para inclusão em seu aplicativo backend do {{site.data.keyword.Bluemix_notm}}.

As etapas a seguir fornecem um esboço resumido das tarefas necessárias para preparar seu app. 

**Nota:** não é necessário incluir o Google Sign-In CocoaPod. O SDK necessário é incluído pelo `BMSGoogleAuthentication` CocoaPod.

1. Observe o **Identificador de pacote configurável** em seu projeto do Xcode a partir da seção **Identidade** da guia **Geral** do destino principal. Ele é necessário para criar seu projeto do Google Sign-In.

1. Crie um projeto no Google Developer para Google Sign-In for iOS em https://developers.google.com/mobile/add?platform=ios. 

2. Inclua o serviço Google Sign-In no projeto.

3. Recupere o `GoogleService-Info.plist`.

  **Importante:** Quando você obtiver o arquivo
`GoogleService-Info.plist`, abra-o e anote o valor de
`CLIENT_ID`. Esse valor será necessário mais tarde para configurar o aplicativo backend do {{site.data.keyword.amashort}}.

1. Inclua o arquivo `GoogleService-Info.plist` em seu projeto do Xcode. Para obter mais informações, veja [Incluir o arquivo de configuração em seu projeto](https://developers.google.com/identity/sign-in/ios/start-integrating#add-config).

1. Atualize os Esquemas de URL em seu projeto do Xcode com o
`REVERSE_CLIENT_ID` e o identificador de pacote configurável. Para obter mais informações, veja [Incluir esquemas URL em seu projeto](https://developers.google.com/identity/sign-in/ios/start-integrating#add_a_url_scheme_to_your_project).

1. Atualize o arquivo project-Bridging-Header.h do seu app com o código a
seguir:

 ```
 #import <Google/SignIn.h>
 ```
 {: codeblock}

 Para obter mais informações sobre a atualização do arquivo de cabeçalho de
ponte, consulte a etapa 1. em
[Ativar
conexão](https://developers.google.com/identity/sign-in/ios/sign-in#enable_sign-in).

## Configurando o {{site.data.keyword.amashort}} para autenticação do Google
{: #google-auth-ios-config}

Agora que você tem um identificador de cliente do iOS, é possível ativar a autenticação do Google no painel do {{site.data.keyword.Bluemix}}.

1. Abra o seu serviço no painel do {{site.data.keyword.amashort}}. 

1. Clique em **Opções de dispositivo móvel** e tome nota da **Rota** (*applicationRoute*) e
do **GUID / TenantId do aplicativo** (*tenantId*). Você precisará desses valores ao inicializar o SDK e enviar solicitações para o
aplicativo backend.

1. Clique no botão **Configurar** no painel **Google**.

1. Em **ID do aplicativo para iOS**, especifique o valor
`CLIENT_ID` do arquivo `GoogleService-Info.plist` que
você obteve anteriormente e clique em **Salvar**.

## Configurando o {{site.data.keyword.amashort}} client SDK para iOS
{: #google-auth-ios-sdk}

### Instalando o CocoaPods
{: #install-cocoapods}

1. Abra o Terminal e execute o comando **pod --version**. Se você já tiver o CocoaPods instalado, o número da versão é exibido. É possível pular para a próxima seção para instalar o SDK.

1. Se você não tiver o CocoaPods instalado, execute:
```
sudo gem install cocoapods
```
{: codeblock}

Para obter mais informações, veja o
[website CocoaPods](https://cocoapods.org/).

### Instalando o {{site.data.keyword.amashort}} client Swift SDK com o CocoaPods
{: #facebook-auth-install-swift-cocoapods}

1. Se você não tiver nenhum `Podfile` em seu projeto do iOS, execute `pod init` para criar o arquivo.

1. Edite o `Podfile` e inclua as linhas a seguir no destino relevante.

 ```
 use_frameworks!
 pod 'BMSGoogleAuthentication'
 ```
 {: codeblock}
 
 **Nota:** se você já tiver instalado o {{site.data.keyword.amashort}} core SDK, será possível remover esta linha: `pod 'BMSSecurity'`. O pod `BMSGoogleAuthentication` instala todas as estruturas necessárias.
	
 **Dica:** é possível incluir `use_frameworks!` em
seu destino Xcode em vez de tê-lo no Podfile.

1. Salve o `Podfile` e execute `pod install` na
linha de comandos. O CocoaPods instala as dependências. Você verá o progresso e os componentes que foram incluídos.

 **Importante**: deve-se abrir agora o projeto usando o arquivo
`xcworkspace` que é gerado pelo CocoaPods. Normalmente, o nome é `{your-project-name}.xcworkspace`.  

1. Execute `open {your-project-name}.xcworkspace` na linha de
comandos para abrir sua área de trabalho de projeto do iOS.

1. Copie o arquivo `GoogleAuthenticationManager.swift` dos
arquivos de origem pod `BMSGoogleAuthentication` para o diretório de
projeto.

## Inicializando o {{site.data.keyword.amashort}} client Swift SDK
{: #google-auth-ios-initialize}

Para usar o SDK do cliente do {{site.data.keyword.amashort}}, inicialize-o passando o parâmetro `applicationGUID`
(`tenantID`).

Um local comum, mas não obrigatório, para colocar o código de inicialização é o método `application:didFinishLaunchingWithOptions` de delegado do seu aplicativo.

1. Importe as estruturas necessárias na classe em que você deseja usar o {{site.data.keyword.amashort}} client SDK. Inclua os cabeçalhos a seguir:

	 ```Swift 	let tenantId = "<serviceTenantID>" 	let regionName = <applicationBluemixRegion> 	func application(_ application: UIApplication,
didFinishLaunchingWithOptions launchOptions: 		[UIApplicationLaunchOptionsKey: Any]?) -> Bool {

	    let mcaAuthManager = MCAAuthorizationManager.sharedInstance
	    		mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
	 ///the regionName should be one of the following: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, or BMSClient.Region.sydney   
	    BMSClient.sharedInstance.authorizationManager = mcaAuthManager
		GoogleAuthenticationManager.sharedInstance.register()
		return true
	}

	// [START openurl]
	    func application(_ application: UIApplication,
			     open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
		return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, sourceApplication: sourceApplication, annotation: annotation)
      }

	    @available(iOS 9.0, *)
	    func application(_ app: UIApplication, open url: URL, options: [UIApplicationOpenURLOptionsKey : Any]) -> Bool {
		return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, options: options)
  }

	 ```

 No código:
 	* Substitua o `<serviceTenantID>` pelo valor que você recuperou a partir das **Opções de dispositivo móvel**
(veja [Configurando o Mobile Client Access para autenticação do Google](#google-auth-ios-config)). 
	* Substitua `<applicationBluemixRegion>` pela região em que seu aplicativo {{site.data.keyword.Bluemix_notm}} está hospedado. Para visualizar sua região do {{site.data.keyword.Bluemix_notm}}, clique no ícone de **Avatar** ![Ícone de Avatar](images/face.jpg "Ícone de Avatar") na barra de menus para abrir o widget **Conta e suporte**. O valor da região que aparece deve ser um dos seguintes: **US
South**, **United Kingdom** ou **Sydney** e corresponder aos valores requeridos no código: `BMSClient.Region.usSouth`,
`BMSClient.Region.unitedKingdom` ou `BMSClient.Region.sydney`.
	


## Testando a Autenticação
{: #google-auth-ios-testing}

Após o SDK do cliente ser inicializado e o Google Authentication Manager ser registrado, será possível começar a fazer solicitações a seu aplicativo backend móvel.

### Antes de iniciar
{: #google-auth-ios-testing-before}

Deve-se usar o modelo do {{site.data.keyword.mobilefirstbp}} e já ter um recurso protegido por {{site.data.keyword.amashort}} no terminal `/protected`. Se for necessário configurar um terminal `/protected`, consulte [Protegendo recursos](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).


1. Tente enviar uma solicitação para um terminal protegido de seu aplicativo backend móvel em seu navegador da área de trabalho, abrindo `{applicationRoute}/protected`. Substitua
o `{applicationRoute}` pelo valor que você recuperou a partir das **Opções
de dispositivo móvel** (veja [Configurando o Mobile Client
Access para autenticação do Google](#google-auth-ios-config)). Por exemplo,
`http://my-mobile-backend.mybluemix.net/protected`.

1. O terminal `/protected` de um aplicativo backend móvel criado com o MobileFirst Services Boilerplate é protegido com o
{{site.data.keyword.amashort}}, portanto, só pode ser acessado pelos aplicativos móveis instrumentados com o SDK do cliente
{{site.data.keyword.amashort}}. Como resultado, você verá `Unauthorized` no navegador de sua área de trabalho.

1. Use seu aplicativo iOS para fazer solicitação para o mesmo terminal.

 ```Swift 	let protectedResourceURL = "<your protected resource absolute path>" 	let request = Request(url: protectedResourceURL, method:
HttpMethod.GET) 	let callBack:BMSCompletionHandler = {(response: Response?, error: Error?) in
	   if error == nil {
	       print ("response:\(response?.responseText), no error")
	    } else {
	       print ("error: \(error)")
	    }
	}

	request.send(completionHandler: callBack)

	```
1. Execute o aplicativo. Você verá um pop-up da tela de Login do Google

 ![image](images/ios-google-login.png)

1. Quando você efetuar login e clicar em **OK**, estará autorizando o
{{site.data.keyword.amashort}} a usar sua identidade de usuário do Google para
propósitos de autenticação.

1. Sua solicitação deve ser bem-sucedida. A saída a seguir aparece no log.

 ```
response:Optional("Hello, this is a protected resource of the mobile backend application!"), no error

 ```
{: screen}

1. Também é possível incluir a funcionalidade de logout incluindo o código a seguir:

 ```
 GoogleAuthenticationManager.sharedInstance.logout(callBack)
 ```

  Se você chamar esse código depois que um usuário estiver conectado ao Google e ele tentar efetuar login novamente, ele será solicitado a autorizar o {{site.data.keyword.amashort}} a usar o Google para propósitos de autenticação. Neste ponto, o usuário pode clicar no nome do usuário <!--in the upper-right corner of the screen--> para selecionar e efetuar login com outro usuário.

   Passar `callBack` para a função de logout é opcional. Também é possível passar `nil`.
