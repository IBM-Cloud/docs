---

copyright:
  years: 2016

---

# Configurando o iOS Swift SDK
{: #getting-started-ios}

Instrumente seu aplicativo iOS com o {{site.data.keyword.amashort}} SDK, inicialize o SDK e faça solicitações aos recursos protegidos e desprotegidos.

## Antes de iniciar
{: #before-you-begin}
* Deve-se ter uma instância de um backend móvel que seja protegido pelo serviço {{site.data.keyword.amashort}}. Para obter mais informações sobre como criar um backend móvel, consulte [Introdução](getting-started.html).
* Assegure-se de ter configurado corretamente o Xcode. Para obter mais informações sobre como configurar o seu ambiente do iOS, consulte o [website do Apple Developer](https://developer.apple.com/support/xcode/).


## Instalando o {{site.data.keyword.amashort}} Client SDK
{: #install-mca-sdk-ios}
O {{site.data.keyword.amashort}} SDK é distribuído com CocoaPods, um gerenciador de dependências para projetos iOS. O CocoaPods faz o download automático de artefatos de repositórios e os disponibiliza para o aplicativo iOS.


### Instalar o CocoaPods
{: #install-cocoapods}
1. Abra o Terminal e execute o comando **pod --version**. Se você já tiver o CocoaPods instalado, o número da versão é exibido. É possível pular para a próxima seção para instalar o SDK.

1. Se você não tiver o CocoaPods instalado, execute:
```
sudo gem install cocoapods
```
Para obter mais informações, consulte o [website do
CocoaPods](https://cocoapods.org/).

### Instalar o {{site.data.keyword.amashort}} Client SDK com CocoaPods
{: #install-sdk-cocoapods}

1. No Terminal, navegue para o diretório-raiz do seu projeto iOS.

1. Se ainda não tiver inicializado sua área de trabalho para CocoaPods, execute o comando `pod init`.<br/>
O CocoaPods cria um arquivo `Podfile` para você, que fica onde você define as dependências de seu projeto iOS.

1. Edite o arquivo `Podfile` e inclua a linha a seguir nos destinos necessários:

	```
  use_frameworks!
	pod 'BMSSecurity'
	```
  **Dica:** é possível incluir `use_frameworks!` em
seu destino Xcode em vez de tê-lo no Podfile.

1. Salve o arquivo `Podfile` e execute `pod install` a partir da linha de comandos. <br/>Cocoapods instalam dependências incluídas. É possível ver o progresso e quais componentes foram incluídos.<br/>
**Importante**: o CocoaPods gera um arquivo `xcworkspace`.  Deve-se abrir esse arquivo para trabalhar em seu projeto futuro.

1. Abra sua área de trabalho do projeto iOS. Abra o arquivo `xcworkspace` que foi gerado por CocoaPods. Por exemplo: `{your-project-name}.xcworkspace`. Execute `open {your-project-name}.xcworkspace`.

## Inicializando o {{site.data.keyword.amashort}} Client SDK
{: #init-mca-sdk-ios}

 Inicialize o SDK passando os parâmetros `applicationRoute` e
`applicationGUID`. Um local comum, mas não obrigatório, para colocar o código de inicialização é o método `application:didFinishLaunchingWithOptions` de delegado do seu aplicativo.

1. Obter valores de parâmetro do aplicativo. Abra seu app no painel do {{site.data.keyword.Bluemix_notm}}. Clique em **Opções de dispositivo móvel**. Os valores `applicationRoute` e `applicationGUID` são
exibidos nos campos **Rota** e **GUID do app**.

1. Importe as estruturas necessárias na classe em que deseja usar o
{{site.data.keyword.amashort}} Client SDK.

 ```Swift
 import BMSCore
 import BMSSecurity
 ```  

1. Inicialize o {{site.data.keyword.amashort}} Client SDK. Substitua os
valores `<applicationRoute>` e
`<applicationGUID>` pelos valores de **Rota** e
**GUID do app** que você obteve das **Opções
móveis** no painel {{site.data.keyword.Bluemix_notm}}.

 ```Swift
 let backendURL = "<applicationRoute>"
 let backendGUID = "<applicationGUID>"

 func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

 // Initialize the Client SDK.  
 BMSClient.sharedInstance.initializeWithBluemixAppRoute(backendURL, bluemixAppGUID: backendGUID, bluemixRegion: BMSClient.<application Bluemix region>)

 BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance

 return true
 }
 ```

## Fazendo uma solicitação em seu backend móvel
{: #request}

Após a inicialização do {{site.data.keyword.amashort}} Client SDK, é possível começar a fazer solicitações para seu backend móvel.

1. Tente enviar uma solicitação a um terminal protegido em seu backend móvel no navegador. Abra a URL a seguir: `{applicationRoute}/protected`. Por exemplo: `http://my-mobile-backend.mybluemix.net/protected`
<br/>O terminal `/protected` de um backend móvel que foi criado com o modelo do MobileFirst Services Starter está protegido com o {{site.data.keyword.amashort}}. Uma
mensagem `Unauthorized` é retornada no navegador, pois esse terminal pode ser acessado somente por aplicativos móveis que sejam
instrumentados com o {{site.data.keyword.amashort}} Client SDK.

1. Use seu aplicativo iOS para fazer uma solicitação ao mesmo terminal. Inclua o código a seguir depois de inicializar `BMSClient`:

 ```Swift
 let customResourceURL = "<your protected resource's path>"
 let request = Request(url: customResourceURL, method: HttpMethod.GET)
 let callBack:MfpCompletionHandler = {(response: Response?, error: NSError?) em
     if error == nil {
         print ("response:\(response?.responseText), no error")
     } else {
         print ("error: \(error)")
     }
 }

 request.sendWithCompletionHandler(callBack)
 ```

1.  Quando sua solicitação for bem-sucedida, você verá a saída a seguir no console do Xcode:

 ```
 response:Optional("Hello, this is a protected resouce of the mobile backend application!"), no error
 ```

## Próximas etapas
{: #next-steps}
Quando você se conectou ao terminal protegido, nenhuma credencial foi necessária. Para requerer que os usuários efetuem login em seu aplicativo, deve-se configurar a autenticação do Facebook, do Google ou customizada.
  * [Facebook
](facebook-auth-ios-swift-sdk.html)
  * [Google](google-auth-ios-swift-sdk.html)
  * [Customizado
](custom-auth-ios-swift-sdk.html)
