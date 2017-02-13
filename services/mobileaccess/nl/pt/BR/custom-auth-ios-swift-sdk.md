---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-16"

---

{:codeblock:.codeblock}


# Configurando a autenticação customizada para seu aplicativo {{site.data.keyword.amashort}} iOS (Swift SDK)
{: #custom-ios}

Configure seu aplicativo iOS que está usando autenticação customizada para utilizar
o SDK do cliente {{site.data.keyword.amafull}} e conectar seu aplicativo ao {{site.data.keyword.Bluemix}}.  


## Antes de iniciar
{: #before-you-begin}

Antes de começar, deve-se ter:

* Um recurso que seja protegido por uma instância do
serviço {{site.data.keyword.amashort}} que está
configurado para usar um provedor de identidade customizado
(consulte
[Configurando autenticação customizada](custom-auth-config-mca.html)).  
* Seu valor **TenantID**. Abra o seu serviço no painel do {{site.data.keyword.amashort}}. Clique no botão **Opções móveis**. O valor
`tenantId` (também conhecido como
`appGUID`) é exibido no campo **App
GUID / TenantId**. Você precisará desse valor para
inicializar o Gerenciador de Autorização.
* Seu nome de **Domínio**. Este é o
valor que você especificou no campo **Nome do
domínio** da seção **Customizado**
no guia **Gerenciamento** do painel {{site.data.keyword.amashort}}.
* A URL do seu aplicativo backend (**Rota de App**). Você precisará desse valor para enviar
solicitações para os terminais protegido do seu aplicativo
backend.
* A {{site.data.keyword.Bluemix_notm}}
**Região**. É possível encontrar a sua região
{{site.data.keyword.Bluemix_notm}} atual no cabeçalho,
próximo ao ícone **Avatar**
![ícone de avatar](images/face.jpg "ícone de avatar"). O valor da região que aparece deve ser um dos seguintes: **US South**, **United Kingdom** ou
**Sydney** e corresponde às constantes requeridas no código: `BMSClient.Region.usSouth`,
`BMSClient.Region.unitedKingdom` ou `BMSClient.Region.sydney`.

Para obter informações adicionais, consulte as seguintes informações:
 * [Introdução
ao {{site.data.keyword.amashort}}](index.html)
 * [Configurando o iOS Swift SDK](getting-started-ios-swift-sdk.html)
 * [Usando um provedor de identidade customizado](custom-auth.html)
 * [Criando um provedor de identidade customizado](custom-auth-identity-provider.html)
 * [Configurando o {{site.data.keyword.amashort}} para autenticação customizada](custom-auth-config-mca.html)

### Ativar Compartilhamento Keychain para iOS
{: #enable_keychain}

Ative `Compartilhamento Keychain`. Acesse
a guia `Recursos` e mude
`Compartilhamento Keychain` para
`On` em seu projeto Xcode.


### Inicializando o client SDK
{: #custom-ios-sdk-initialize}

Inicialize o SDK passando o parâmetro
`applicationGUID`
(**TenantId**). Um local comum, mas não obrigatório, para colocar o código de inicialização é o método `application:didFinishLaunchingWithOptions` de delegado do seu aplicativo.

1. Importe as estruturas necessárias na classe em que deseja usar o {{site.data.keyword.amashort}} client SDK.

	```Swift
	import UIKit
	import BMSCore
	import BMSSecurity
	```
	{: codeblock}

1. Inicialize o SDK do cliente {{site.data.keyword.amashort}}, mude o
gerenciador de autorização para `MCAAuthorizationManager`, bem como
defina e registre uma delegação de autenticação.

```Swift

	let tenantId = "<serviceTenantID>"
	let regionName = <applicationBluemixRegion>
	let customRealm = "<yourProtectedRealm>"

	func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: 
		[UIApplicationLaunchOptionsKey: Any]?) -> Bool {

		let mcaAuthManager = MCAAuthorizationManager.sharedInstance
	    		mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
	 //the regionName should be one of the following BMSClient.Region constants: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, or BMSClient.Region.sydney   
		BMSClient.sharedInstance.authorizationManager = mcaAuthManager

	//Auth delegate for handling custom challenge
 class MyAuthDelegate : AuthenticationDelegate {
		func onAuthenticationChallengeReceived(_ authContext: AuthenticationContext, challenge: AnyObject){
		    print("onAuthenticationChallengeReceived")
		    let answer = try? Utils.parseJsonStringtoDictionary( "{\"userName\":\"" + "test" + "\",\"password\":\"" + "test" + "\"}")
			authContext.submitAuthenticationChallengeAnswer(answer)
		}

		func onAuthenticationSuccess(_ info: AnyObject?) {
		    print("onAuthenticationSuccess info = \(info)")
           print("onAuthenticationSuccess")
      }

		func onAuthenticationFailure(_ info: AnyObject?){
		     print("onAuthenticationFailure info = \(info)")
        print("onAuthenticationFailure")
      }
	     }

	     let delegate = MyAuthDelegate()
	     mcaAuthManager.registerAuthenticationDelegate(delegate, realm: customRealm)

	     return true
 }


```
{: codeblock}

No código:
* Substitua `MCAServiceTenantId` pelo valor
**TenantId** e `<
applicationBluemixRegion>` pela sua
{{site.data.keyword.amashort}}
**Região** (consulte
[Antes de iniciar](##before-you-begin)).
* Use o `realmName` que você especificou
no painel {{site.data.keyword.amashort}} (consulte
[Configurando a autenticação customizada](custom-auth-config-mca.html)).
* Substitua `<applicationBluemixRegion>` pela região em que seu aplicativo {{site.data.keyword.Bluemix_notm}} está hospedado. Para visualizar a região do {{site.data.keyword.Bluemix_notm}}, clique no ícone de Avatar ![ícone de Avatar](images/face.jpg "ícone de avatar") na barra de menus para abrir o widget **Conta e suporte**.  O valor da região que aparece deve ser um dos seguintes: **US South**, **United Kingdom** ou
**Sydney** e corresponde às constantes requeridas no código: `BMSClient.Region.usSouth`,
`BMSClient.Region.unitedKingdom` ou `BMSClient.Region.sydney`.


## Testando a Autenticação
{: #custom-ios-testing}

Após inicializar o SDK do cliente e registrar um delegado de autenticação customizado, é possível começar a fazer solicitações ao seu
aplicativo backend móvel.

### Antes de iniciar
{: #custom-ios-testing-before}

 Deve-se ter um aplicativo que foi criado com o modelo {{site.data.keyword.mobilefirstbp}} e um recurso que seja protegido pelo {{site.data.keyword.amashort}} no terminal `/protected`.

1. Envie uma solicitação para o terminal protegido de seu aplicativo backend móvel em seu navegador abrindo `{applicationRoute}/protected`. Substitua o `{applicationRoute}`
pelo valor recuperado a partir das **Opções de dispositivo móvel** (veja
[Configurando o Mobile Client Access para autenticação customizada](#custom-auth-ios-configmca)). Por exemplo,
`http://my-mobile-backend.mybluemix.net/protected`.

 O terminal `/protected` de um aplicativo backend móvel criado com o modelo {{site.data.keyword.mobilefirstbp}} está protegido com o {{site.data.keyword.amashort}}. O terminal pode ser acessado somente por aplicativos móveis que sejam instrumentados com o {{site.data.keyword.amashort}} client SDK. Como resultado, uma mensagem `Unauthorized` é exibida em seu navegador.

1. Use seu aplicativo iOS para fazer solicitação ao mesmo terminal. Inclua o
código a seguir depois de inicializar `BMSClient` e registrar a
delegação de autenticação customizada:

    ```Swift

	let protectedResourceURL = "<your protected resource absolute path>"
	let request = Request(url: protectedResourceURL, method: HttpMethod.GET)

	let callBack:BMSCompletionHandler = {(response: Response?, error: Error?) in
	   if error == nil {
	       print ("response:\(response?.responseText), no error")
	    } else {
	       print ("error: \(error)")
	    }
	}
	request.send(completionHandler: callBack)
     ```
     {: codeblock}

1. Quando suas solicitações forem bem-sucedidas, você verá a saída a seguir no console Xcode:

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
	 {: codeblock}

1. Também é possível incluir a funcionalidade de logout incluindo o código a seguir:

	 ```
	 MCAAuthorizationManager.sharedInstance.logout(callBack)
	 ```
	 {: codeblock}

 Se você chamar esse código depois que um usuário estiver conectado, ele será desconectado. Quando o usuário tentar efetuar login novamente, ele deverá responder ao desafio recebido do servidor novamente.

 Passar `callBack` para a função de logout é opcional. Também é possível passar `nil`.
