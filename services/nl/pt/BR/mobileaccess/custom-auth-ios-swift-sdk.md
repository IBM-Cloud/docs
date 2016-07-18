---

copyright:
  years: 2016

---

# Configurando o {{site.data.keyword.amashort}} client SDK para iOS (Swift SDK)
{: #custom-ios}

Configure seu aplicativo iOS que está usando autenticação customizada para usar o {{site.data.keyword.amashort}} client SDK e conecte seu aplicativo ao {{site.data.keyword.Bluemix}}.  O {{site.data.keyword.amashort}} Swift SDK recém-liberado inclui e melhora a funcionalidade fornecida pelo Mobile Client Access Objective-C SDK existente.

**Nota:** embora o Objective-C SDK permaneça totalmente suportado e ainda seja considerado o SDK primário para o {{site.data.keyword.Bluemix_notm}} Mobile Services, há planos para descontinuar o Objective-C SDK posteriormente este ano em favor deste novo Swift SDK.

## Antes de iniciar
{: #before-you-begin}

Deve-se ter um recurso que seja protegido por uma instância do serviço {{site.data.keyword.amashort}} que seja configurada para usar um provedor de identidade customizado.  Seu app móvel também deve ser instrumentado com o {{site.data.keyword.amashort}} client SDK.  Para obter informações adicionais, consulte as seguintes informações:
 * [Introdução
ao {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/index.html)
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




### Inicializando o client SDK
{: #custom-ios-sdk-initialize}

Inicialize o SDK passando os parâmetros `applicationRoute` e
`applicationGUID`. Um local comum, mas não obrigatório, para colocar o código de inicialização é no método `application:didFinishLaunchingWithOptions` de delegado do seu aplicativo

1. Obter valores de parâmetro do aplicativo. Abra seu app no painel do {{site.data.keyword.Bluemix_notm}}. Clique em **Opções de dispositivo móvel**. Os
valores `applicationRoute` e `applicationGUID` são
exibidos nos campos **Rota** e **GUID do app**.

1. Importe as estruturas necessárias na classe em que deseja usar o {{site.data.keyword.amashort}} client SDK.

 ```Swift
 import UIKit
 import BMSCore
 import BMSSecurity
```

1. Inicialize o {{site.data.keyword.amashort}} client SDK, mude o gerenciador de autorização para ser MCAAuthorizationManager, defina um delegado de autenticação e registre-o. Substitua os
valores `<applicationRoute>` e
`<applicationGUID>` pelos valores de **Rota** e
**GUID do app** que você obteve das **Opções
móveis** no painel {{site.data.keyword.Bluemix_notm}}. 

  Substitua `<applicationBluemixRegion>` pela região em que seu aplicativo {{site.data.keyword.Bluemix_notm}} está hospedado. Para visualizar sua região do {{site.data.keyword.Bluemix_notm}}, clique no ícone de face (![Face](/face.png "Face")) no canto superior esquerdo do painel.
Para `<yourProtectedRealm>`, use o **Nome da região** definido no quadro **Customizado** do painel do {{site.data.keyword.amashort}}.

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"
 let customRealm = "<yourProtectedRealm>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<applicationBluemixRegion>)

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

## Testando a autenticação
{: #custom-ios-testing}

Depois de inicializar o client SDK e registrar uma delegação de autenticação customizada, será possível começar a fazer solicitações ao seu backend móvel.

### Antes de iniciar
{: #custom-ios-testing-before}

 Deve-se ter um aplicativo criado com o modelo do {{site.data.keyword.mobilefirstbp}} e ter um recurso que seja protegido pelo {{site.data.keyword.amashort}} no terminal `/protected`.

1. Envie uma solicitação para o terminal protegido do backend móvel em seu navegador abrindo `{applicationRoute}/protected`, por exemplo, `http://my-mobile-backend.mybluemix.net/protected`.
  O terminal `/protected` de um backend móvel criado com o modelo do {{site.data.keyword.mobilefirstbp}} está protegido com o {{site.data.keyword.amashort}}. O terminal pode ser acessado somente por aplicativos móveis que sejam instrumentados com o {{site.data.keyword.amashort}} client SDK. Como resultado, uma mensagem `Unauthorized` é exibida em seu navegador.

1. Use seu aplicativo iOS para fazer solicitação para o mesmo terminal. Inclua o
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

1.	Quando suas solicitações forem bem-sucedidas, você verá a saída a seguir no console Xcode:

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
