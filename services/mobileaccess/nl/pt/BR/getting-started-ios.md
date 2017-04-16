---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-02"

---
{:shortdesc: .shortdesc}

# Configurando o iOS Objective-C SDK
{: #getting-started-ios}

Instrumente seu aplicativo iOS com o SDK {{site.data.keyword.amafull}}, inicialize o SDK e faça solicitações aos recursos protegidos
e não protegidos.

{:shortdesc}

**Importante:** embora o Objective-C SDK permaneça totalmente suportado e ainda seja considerado o SDK primário para o {{site.data.keyword.Bluemix_notm}} Mobile Services, há planos para descontinuar o Objective-C SDK posteriormente este ano em favor do novo Swift SDK. Para novos aplicativos, é altamente recomendável usar o SDK do Swift (veja
[Configurando o SDK do Swift iOS](getting-started-ios-swift-sdk.html)).

## Antes de Começar
{: #before-you-begin}
Você deve ter:
* Uma instância de um aplicativo {{site.data.keyword.Bluemix_notm}} que é protegida pelo serviço {{site.data.keyword.amashort}}. Para obter mais informações sobre como criar um aplicativo backend do {{site.data.keyword.Bluemix_notm}}, consulte [Introdução](index.html).
* Seu **TenantID**. Abra o seu serviço no painel do {{site.data.keyword.amashort}}. Clique em **Opções de dispositivo móvel**. Os valores
`tenantId` (também conhecido como
`appGUID`) são exibidos no campo **App
GUID / TenantId**. Você precisará desse
valor para inicializar o {{site.data.keyword.amashort}}
Authorization Manager.
* Sua **Rota do aplicativo**. Esta é a
URL do seu aplicativo backend. Você precisa desse valor para
enviar solicitações para seus terminais protegidos.
* Um projeto do Xcode.  


## Instalando o {{site.data.keyword.amashort}} client SDK
{: #install-mca-sdk-ios}
O {{site.data.keyword.amashort}} SDK é distribuído com CocoaPods, um gerenciador de dependências para projetos iOS. O CocoaPods faz download automaticamente dos artefatos de repositórios e os disponibiliza para seu aplicativo iOS.


### Instalar o CocoaPods
{: #install-cocoapods}

1. Abra o Terminal e execute o comando **pod --version**. Se você já tiver o CocoaPods instalado, o número da versão é exibido. Pule
para a próxima seção para instalar o SDK.

1. Se você não tiver o CocoaPods instalado, execute:

```
sudo gem install cocoapods
```

Para obter mais informações, consulte o [website do
CocoaPods](https://cocoapods.org/).

### Instalar o {{site.data.keyword.amashort}} client SDK com o CocoaPods
{: #install-sdk-cocoapods}

1. No Terminal, navegue para o diretório-raiz do seu projeto iOS.

1. Se ainda não tiver inicializado sua área de trabalho para CocoaPods, execute o comando `pod init`.<br/>
O CocoaPods cria um arquivo `Podfile` para você, que fica onde você define as dependências de seu projeto iOS.

1. Edite o arquivo `Podfile` e inclua a linha a seguir nos destinos necessários:


	`pod 'IMFCore'`

1. Salve o arquivo `Podfile` e execute `pod install` a partir da linha de comandos. <br/>O
Cocoapods instala dependências incluídas e exibe os componentes incluídos.<br/>

	**Importante**: o CocoaPods gera um arquivo `xcworkspace`.  Deve-se abrir esse arquivo para trabalhar em seu projeto futuro.

1. Abra sua área de trabalho do projeto iOS. Abra o arquivo `xcworkspace` que foi gerado por CocoaPods. Por exemplo: `{your-project-name}.xcworkspace`. Execute `open {your-project-name}.xcworkspace`.

## Inicializando o {{site.data.keyword.amashort}} client SDK
{: #init-mca-sdk-ios}

1. Importe a estrutura `IMFCore` na classe em que você deseja usar o {{site.data.keyword.amashort}} client SDK incluindo o cabeçalho a seguir:

	####Objective-C
	{: #imfcore-objc}

	```Objective-C
	  #import <IMFCore/IMFCore.h>
	```

	####Swift
	{: #sdk-swift}

	O {{site.data.keyword.amashort}} client SDK é implementado com Objective-C. Pode ser necessário incluir um cabeçalho de ponte em seu projeto Swift:
	1. Clique com o botão direito do mouse no projeto em
Xcode e selecione **Novo Arquivo**.
	1. Na categoria **Origem iOS**, clique em **Arquivo de cabeçalho**. Atribua um nome ao arquivo `BridgingHeader.h`.
	1. Inclua a linha a seguir em seu cabeçalho de ponte:
`#import < IMFCore/IMFCore.h>`.
	1. Clique em seu projeto no Xcode e selecione a guia **Configurações de compilação**.
	1. Procure por `Cabeçalho de ponte do Objective-C`.
	1. Configure o valor para o local do seu arquivo `BridgingHeader.h`, por exemplo, `$(SRCROOT)/MyApp/BridgingHeader.h`.
	1. Assegure-se de que seu cabeçalho de ponte esteja sendo selecionado pelo Xcode, compilando o seu projeto. Nenhuma mensagem de falha deve ser vista.

1. Use o código a seguir para inicializar o {{site.data.keyword.amashort}} client SDK.  Um local comum, mas não obrigatório, para colocar o código de inicialização é o método `application:didFinishLaunchingWithOptions` de delegado do seu aplicativo. <br/> Para informações sobre como obter o
`applicationRoute` e o
`applicationGUID`, consulte
[Antes de iniciar](#before-you-begin). 

	####Objective-C
	{: #sharedinstance-objc}

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	####Swift
	{: #sharedinstance-swift}
	```Swift
 		MFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",backendGUID: "applicationGUID")
	```

## Inicializando o AuthorizationManager
Inicialize o `AuthorizationManager` passando o parâmetro
`tenantId` do serviço {{site.data.keyword.amashort}}. Para obter informações sobre como obter esses valores, consulte
[Antes de iniciar](#before-you-begin). 

#### Objective-C

```Objective-C
[[IMFAuthorizationManager sharedInstance]  initializeWithTenantId: @"<tenantId>"];
```

#### Swift

```Swift
IMFAuthorizationManager.sharedInstance().initializeWithTenantId("<tenantId>")
```

	
## Fazendo uma solicitação para seu aplicativo backend móvel
{: #request}

Após o SDK do cliente {{site.data.keyword.amashort}} ser inicializado, será possível começar a fazer solicitações ao seu aplicativo
backend móvel.

1. Tente enviar uma solicitação a um terminal protegido em seu aplicativo backend móvel em seu navegador. Abra
a URL a seguir: `{applicationRoute}/protected`. Por exemplo: `http://my-mobile-backend.mybluemix.net/protected`
<br/>O terminal `/protected` de um aplicativo backend móvel que foi criado com o modelo MobileFirst Services Starter é
protegido com {{site.data.keyword.amashort}}. Uma mensagem `Unauthorized` é retornada em seu navegador porque esse terminal pode ser acessado somente por aplicativos móveis instrumentados com o {{site.data.keyword.amashort}} client SDK.

1. Use seu aplicativo iOS para fazer uma solicitação ao mesmo terminal. Inclua o código a seguir depois de inicializar o `IMFClient`:

	####Objective-C
	{: #nsstring-objc}

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
		}
	}];
	```

	####Swift
	{: #imfclientrequestpath-swift}

	```Swift
	let requestPath = IMFClient.sharedInstance().backendRoute + "/protected"

	let request = IMFResourceRequest(path: requestPath, method: "GET");
	request.sendWithCompletionHandler { (response, error) -> Void in
		if (nil != error){
			NSLog("Error :: %@", error.description)
		} else {
			NSLog("Response :: %@", response.responseText)
		}
	};

	```

1.  Quando sua solicitação for bem-sucedida, você verá a saída a seguir no console do Xcode:

	![image](images/getting-started-ios-success.png)

## Próximas Etapas
{: #next-steps}
Quando você se conecta ao terminal protegido, nenhuma credencial é necessária. Para requerer que os usuários efetuem login no aplicativo, deve-se configurar autenticação do Facebook, Google ou customizada.
  * [Facebook
](facebook-auth-ios.html)
  * [Google](google-auth-ios.html)
  * [Customizada
](custom-auth-ios.html)
