---

copyright:
  years: 2016

---

# Configurando o {{site.data.keyword.amashort}} Client SDK for iOS (Swift SDK)
{: #custom-ios}

Configure seu aplicativo iOS que está usando autenticação customizada para usar o {{site.data.keyword.amashort}} Client SDK e conecte seu aplicativo ao {{site.data.keyword.Bluemix}}.

## Antes de iniciar
{: #before-you-begin}

Deve-se ter um recurso que seja protegido por uma instância do serviço {{site.data.keyword.amashort}} que seja configurada para usar um provedor de identidade customizado.  Seu app móvel também devem ser instrumentado com o {{site.data.keyword.amashort}} Client SDK.  Para obter informações adicionais, consulte as seguintes informações:
 * [Introdução
ao {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [Configurando o iOS Swift SDK](https://console.{DomainName}/docs/services/mobileaccess/getting-started-ios-swift-sdk.html)
 * [Usando um provedor de identidade customizado](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [Criando um provedor de identidade customizado](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [Configurando o {{site.data.keyword.amashort}} para autenticação customizada](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)


## Configurando o {{site.data.keyword.amashort}} para autenticação customizada
 {: #custom-auth-ios-configmca}

 1. Abra seu app no painel do {{site.data.keyword.Bluemix_notm}}.

 1. Clique em **Opções móveis** e anote a
**Rota** (*applicationRoute*) e o **GUID do
app** (*applicationGUID*). Eles serão necessários ao inicializar o SDK.

 1. Clique no ladrilho {{site.data.keyword.amashort}}. O painel do {{site.data.keyword.amashort}} é carregado.

 1. Clique no ladrilho **Customizado**.

 1. Em **Nome da região**, especifique sua região de
autenticação customizada.

 1. Em **URL**, especifique a applicationRoute.

 1. Clique em **Salvar**.

## Configurando o {{site.data.keyword.amashort}} Client SDK para iOS
 {: #custom-auth-ios-sdk}

### Instalando o CocoaPods
 {: #custom-auth-cocoapods}

 O {{site.data.keyword.amashort}} Client SDK é distribuído com CocoaPods, um gerenciador de dependências para projetos iOS. O CocoaPods faz o download automático de artefatos de repositórios e os disponibiliza para o aplicativo iOS.

 1. Abra o Terminal e execute o comando `pod --version`. Se você já tiver o CocoaPods instalado, o número da versão será exibido. É possível pular para a próxima seção deste tutorial.

 1. Instale o CocoaPods executando `sudo gem install cocoapods`. Consulte o [website do CocoaPods](https://cocoapods.org/) se precisar de orientação adicional.

 1. Feche o XCode.

 1. Abra Terminal e `cd` no diretório de projeto.

 1.  Execute `pod init`.

### Instalando o Client SDK com o CocoaPods
{: #custom-ios-sdk-cocoapods}

Use o gerenciador de dependência CocoaPods para instalar o {{site.data.keyword.amashort}} Client SDK.

1. Abra o Terminal e navegue até o diretório-raiz de seu projeto iOS.

1. Edite `Podfile` e inclua as linhas a seguir.

 ```
 use_frameworks!
 pod 'BMSSecurity'
 ```
 **Dica:** é possível incluir `use_frameworks!` em
seu destino Xcode em vez de tê-lo no Podfile.

1. Na linha de comandos, execute `pod install`.
O CocoaPods instala as dependências incluídas. O progresso e quais componentes foram incluídos são exibidos.

 **Importante**: deve-se agora abrir o projeto usando um arquivo xcworkspace que foi gerado por CocoaPods. Normalmente, o nome é `{your-project-name}.xcworkspace`.  

1. Execute `open {your-project-name}.xcworkspace` a partir da linha de comandos para abrir sua área de trabalho do projeto iOS.

### Inicializando o Client SDK
{: #custom-ios-sdk-initialize}

Inicialize o SDK passando os parâmetros `applicationRoute` e
`applicationGUID`. Um local comum, mas não obrigatório, para colocar o código de inicialização é o método `application:didFinishLaunchingWithOptions` de delegado do seu aplicativo

1. Obter valores de parâmetro do aplicativo. Abra seu app no painel do {{site.data.keyword.Bluemix_notm}}. Clique em **Opções de dispositivo móvel**. Os
valores `applicationRoute` e `applicationGUID` são
exibidos nos campos **Rota** e **GUID do app**.

1. Importe as estruturas necessárias na classe em que deseja usar o
{{site.data.keyword.amashort}} Client SDK.

 ```Swift
 import UIKit
 import BMSCore
 import BMSSecurity
```

1. Inicialize o {{site.data.keyword.amashort}} Client SDK, mude o
gerenciador de autorização para ser MCAAuthorizationManager e defina uma delegação de
autenticação e registre-a. Substitua os valores
`<applicationRoute>` e
`<applicationGUID>` pelos valores de **Rota** e
**GUID do app** que você obteve das **Opções
móveis** no painel {{site.data.keyword.Bluemix_notm}}.

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"
 let customRealm = "<your protected resource's realm>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<application Bluemix region>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

  //Auth delegate for handling custom challenge
 class MyAuthDelegate : AuthenticationDelegate {
      func onAuthenticationChallengeReceived(authContext: AuthenticationContext, challenge: AnyObject){
          print("onAuthenticationChallengeReceived")
              let answer = <An answer to the challenge sent by the backend (Should be of type [String:AnyObject])>
              authContext.submitAuthenticationChallengeAnswer(answer)
      }

      func onAuthenticationSuccess(info: AnyObject?) {
           print("onAuthenticationSuccess info = \(info)")
           print("onAuthenticationSuccess")
      }

      func onAuthenticationFailure(info: AnyObject?){
        print("onAuthenticationFailure info = \(info)")
        print("onAuthenticationFailure")
      }
  }

  let delegate = MyAuthDelegate()
  let mcaAuthManager = MCAAuthorizationManager.sharedInstance

 do {
      try mcaAuthManager.registerAuthenticationDelegate(delegate, realm: customRealm)
  } catch {
      print("error with register: \(error)")
  }
 return true
 }   
 ```

## Testando a Autenticação
{: #custom-ios-testing}

Depois de inicializar o Client SDK e registrar uma delegação de autenticação
customizada, é possível começar a fazer solicitações ao backend móvel.

### Antes de iniciar
{: #custom-ios-testing-before}

 Deve-se ter um aplicativo que foi criado com o modelo do {{site.data.keyword.mobilefirstbp}} e ter um recurso que esteja protegido por {{site.data.keyword.amashort}} no terminal `/protected`.

1. Envie uma solicitação ao terminal protegido do backend móvel em seu navegador
abrindo `{applicationRoute}/protected`, por exemplo,
`http://my-mobile-backend.mybluemix.net/protected`.
  O terminal `/protected` de um backend móvel criado com o modelo do {{site.data.keyword.mobilefirstbp}} é protegido com o {{site.data.keyword.amashort}}. O terminal só pode ser acessado por aplicativos móveis que sejam instrumentados com o {{site.data.keyword.amashort}} Client SDK. Como resultado, uma mensagem `Unauthorized` é exibida em seu navegador.

1. Use seu aplicativo iOS para fazer solicitação ao mesmo terminal. Inclua o
código a seguir depois de inicializar `BMSClient` e registrar a
delegação de autenticação customizada:

 ```Swift
 let customResourceURL = "<your protected resource's path>"
 let request = Request(url: customResourceURL, method: HttpMethod.GET)
 let callBack:BmsCompletionHandler = {(response: Response?, error: NSError?) in
  if error == nil {
      print ("response:\(response?.responseText), no error")
  } else {
      print ("error: \(error)")
  }
 }

 request.sendWithCompletionHandler(callBack)
 ```

1. 	Quando suas solicitações forem bem-sucedidas, você verá a saída a seguir no console Xcode:

 ```
 onAuthenticationSuccess info = Optional({
     attributes =     {
     };
     deviceId = don;
     displayName = "Don+Lon";
     isUserAuthenticated = 1;
     userId = don;
 })
 response:Optional("Hello Don Lon"), no error
 ```

1. Também é possível incluir a funcionalidade de logout incluindo o código a seguir:

 ```
 MCAAuthorizationManager.sharedInstance.logout(callBack)
 ```  

 Se você chamar esse código depois que um usuário estiver conectado, ele será desconectado. Quando o usuário tentar efetuar login novamente, ele deverá responder ao desafio recebido do servidor novamente.

 Passar `callBack` para a função de logout é opcional. Também é possível passar `nil`.
