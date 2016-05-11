---

copyright:
  years: 2016

---

# Ativando a autenticação do Google em apps iOS (Swift SDK)
{: #google-auth-ios}

## Antes de iniciar
{: #google-auth-ios-before}

* Deve-se ter um recurso que seja protegido pelo {{site.data.keyword.amashort}} e um projeto do iOS que seja instrumentado com o {{site.data.keyword.amashort}} Client SDK.  Para obter mais informações, consulte
[Introdução
ao {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) e
[Configurando
o iOS Swift SDK](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios-swift-sdk.html).
* Proteja manualmente seu aplicativo backend com o {{site.data.keyword.amashort}} Server SDK. Para obter mais informações, consulte [Protegendo recursos](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

## Preparando seu app para conexão no Google
{: #google-sign-in-ios}

Prepare seu app para conexão no Google seguindo as instruções que o Google fornece em
[Google
Sign-In para iOS](https://developers.google.com/identity/sign-in/ios/start-integrating). As etapas a seguir dão a você um esboço resumido das tarefas
que se deve executar para preparar seu app.

1. Ative o Google Sign-In para iOS em seu app. Para obter mais informações, consulte
[Tentar
Sign-In para iOS](https://developers.google.com/identity/sign-in/ios/start?ver=swift).

1. Obtenha um arquivo de configuração
(`GoogleService-Info.plist`) para seu projeto. Para obter o arquivo,
consulte [Ativar
serviços do Google para seu app](https://developers.google.com/mobile/add?platform=ios).

 **Importante:** Quando você obtiver o arquivo
`GoogleService-Info.plist`, abra-o e anote o valor de
`CLIENT_ID`. Esse valor será necessário mais tarde para configurar o
{{site.data.keyword.amashort}}.

1. Inclua o arquivo `GoogleService-Info.plist` em seu projeto
Xcode. Para obter mais informações, consulte
[Incluir
o arquivo de configuração em seu projeto](https://developers.google.com/identity/sign-in/ios/start-integrating#add-config)

1. Atualize os Esquemas de URL em seu projeto Xcode com o
`REVERSE_CLIENT_ID` e o identificador de pacote configurável. Para obter
mais informações, consulte
[Incluir
esquemas de URL em seu projeto](https://developers.google.com/identity/sign-in/ios/start-integrating#add_url_schemes_to_your_project).

1. Atualize o arquivo project-Bridging-Header.h do seu app com o código a
seguir:

 ```
 #import <Google/SignIn.h>
 ```

 Para obter mais informações sobre a atualização do arquivo de cabeçalho de
ponte, consulte a etapa 1. em
[Ativar
conexão](https://developers.google.com/identity/sign-in/ios/sign-in#enable_sign-in).

## Configurando o {{site.data.keyword.amashort}} para autenticação do Google
{: #google-auth-ios-config}

Agora que você possui um identificador de cliente iOS, poderá ativar a autenticação do Google no painel do {{site.data.keyword.Bluemix}}.

1. Abra seu app no painel do {{site.data.keyword.Bluemix_notm}}.

1. Clique em **Opções móveis** e anote a
**Rota** (*applicationRoute*) e o **GUID do
app** (*applicationGUID*). Eles serão necessários ao inicializar o SDK.

1. Clique no ladrilho {{site.data.keyword.amashort}}. O painel do {{site.data.keyword.amashort}} é carregado.

1. Clique no ladrilho **Google**.

1. Em **ID do aplicativo para iOS**, especifique o valor
`CLIENT_ID` do arquivo `GoogleService-Info.plist` que
você obteve anteriormente e clique em **Salvar**.

## Configurando o {{site.data.keyword.amashort}} Client SDK para iOS
{: #google-auth-ios-sdk}

### Instalando o CocoaPods
{: #google-auth-cocoapods}

O {{site.data.keyword.amashort}} Client SDK é distribuído com CocoaPods, um gerenciador de dependências para projetos iOS. O CocoaPods faz o download automático de artefatos de repositórios e os disponibiliza para o aplicativo iOS.

1. Abra o Terminal e execute o comando `pod --version`. Se você já tiver o CocoaPods instalado, o número da versão será exibido. É possível pular para a próxima seção deste tutorial.

1. Instale o CocoaPods executando `sudo gem install cocoapods`. Consulte o [website do CocoaPods](https://cocoapods.org/) se precisar de orientação adicional.

1. Feche o XCode.

1. Abra Terminal e `cd` no diretório de projeto.

1.  Execute `pod init`.

### Instalando o {{site.data.keyword.amashort}} Client SWift SDK usando
CocoaPods
{: #google-auth-ios-sdk-cocoapods}

1. Navegue para seu projeto do iOS.

1. Edite o `Podfile` para incluir as linhas a seguir:

 ```
 use_frameworks!
 pod 'BMSGoogleAuthentication'
 ```
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

## Inicializando o {{site.data.keyword.amashort}} Client Swift SDK
{: #google-auth-ios-initialize}

Para usar o {{site.data.keyword.amashort}} Client SDK, inicialize-o
passando os parâmetros `applicationGUID` e
`applicationRoute`.

Um local comum, mas não obrigatório, para colocar o código de inicialização é o método `application:didFinishLaunchingWithOptions` de delegado do seu aplicativo.

1. Obter valores de parâmetro do aplicativo. Abra seu app no painel do {{site.data.keyword.Bluemix_notm}}. Clique em **Opções de dispositivo móvel**. Os valores `applicationRoute` e `applicationGUID` são
exibidos nos campos **Rota** e **GUID do app**.

1. Importe as estruturas necessárias na classe em que você deseja usar o
{{site.data.keyword.amashort}} Client SDK. Inclua os cabeçalhos a seguir:

 ```Swift
 import UIKit
 import BMSCore
 import BMSSecurity
 ```

1. Use o código a seguir para inicializar o Client SDK. Substitua os valores
`<applicationRoute>` e `<applicationGUID>`
pelos valores de **Rota** e **GUID do app** que
você obteve das **Opções móveis** no painel
{{site.data.keyword.Bluemix_notm}}.

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 // Initialize the Client SDK.  
 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUId, bluemixRegion: BMSClient.<application Bluemix region>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

 GoogleAuthenticationManager.sharedInstance.register()
      return true
      }

 // [START openurl]
      func application(application: UIApplication, openURL url: NSURL, sourceApplication: String?,annotation: AnyObject) -> Bool {
             return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, sourceApplication: sourceApplication, annotation: annotation)
      }

 @available(iOS 9.0, *)
 func application(app: UIApplication, openURL url: NSURL, options: [String : AnyObject]) -> Bool {
 return GoogleAuthenticationManager.sharedInstance.handleApplicationOpenUrl(openURL: url, options: options)
  }
 ```

## Testando a Autenticação
{: #google-auth-ios-testing}

Depois que o Client SDK for inicializado e o gerenciador de autenticação do Google
for registrado, será possível começar a fazer solicitações ao seu backend móvel.

### Antes de iniciar
{: #google-auth-ios-testing-before}

Deve-se usar o modelo do {{site.data.keyword.mobilefirstbp}} e já ter um recurso protegido por {{site.data.keyword.amashort}} no terminal `/protected`. Se for necessário configurar um terminal `/protected`, consulte [Protegendo recursos](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).


1. Tente enviar uma solicitação para o terminal protegido de seu backend móvel no
navegador do desktop abrindo `{applicationRoute}/protected`, por
exemplo, `http://my-mobile-backend.mybluemix.net/protected`

1. O terminal `/protected` de um backend móvel criado com o Modelo do MobileFirst Services é protegido com o {{site.data.keyword.amashort}}, portanto, ele só pode ser acessado por aplicativos móveis instrumentados com o {{site.data.keyword.amashort}} Client SDK. Como resultado, você verá `Unauthorized` no navegador de sua área de trabalho.

1. Use seu aplicativo iOS para fazer solicitação para o mesmo terminal.

 ```Swift
 let protectedResourceURL = "<Your protected resource URL>" // any protected resource
 let request = Request(url: protectedResourceURL , method: HttpMethod.GET)
 let callBack:BmsCompletionHandler = {(response: Response?, error: NSError?) in
 if error == nil {
    print ("response:\(response?.responseText), no error")
 } else {
    print ("error: \(error)")
 }
 }

 request.sendWithCompletionHandler(callBack)
	```

1. Execute o aplicativo. Você verá um pop-up da tela de Login do Google

 ![image](images/ios-google-login.png)

1. Quando você efetuar login e clicar em **OK**, estará autorizando o
{{site.data.keyword.amashort}} a usar sua identidade de usuário do Google para
propósitos de autenticação.

1. 	Sua solicitação deve ser bem-sucedida. Você deverá ver a saída a seguir no log.

 ```
 onAuthenticationSuccess info = Optional({attributes = {};
     deviceId = 105747725068605084657;
     displayName = "donlonqwerty@gmail.com";
     isUserAuthenticated = 1;
     userId = 105747725068605084657;
 })
 response:Optional("Hello, this is a protected resource!"), no error
 ```

1. Também é possível incluir a funcionalidade de logout incluindo o código a seguir:

 ```
 GoogleAuthenticationManager.sharedInstance.logout(callBack)
 ```

  Se você chamar esse código depois que um usuário estiver conectado ao Google e ele tentar efetuar login novamente, ele será solicitado a autorizar o {{site.data.keyword.amashort}} a usar o Google para propósitos de autenticação. Neste ponto, o usuário pode clicar no nome do usuário no canto superior direito da tela para selecionar e efetuar login com outro usuário.

   Passar `callBack` para a função de logout é opcional. Também é possível passar `nil`.
