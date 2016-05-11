---

copyright:
  years: 2015, 2016

---

# Configurando o iOS Objective-C SDK
{: #getting-started-ios}

Instrumente seu aplicativo iOS com o {{site.data.keyword.amashort}} SDK, inicialize o SDK e faça solicitações aos recursos protegidos e desprotegidos.

**Dica:** Se você estiver desenvolvendo seu app iOS no Swift,
considere o {{site.data.keyword.amashort}} Client Swift SDK. Para obter detalhes,
consulte [Configurando o iOS Swift SDK](getting-started-ios-swift-sdk.html)

## Antes de Começar
{: #before-you-begin}
* Deve-se ter uma instância de um backend móvel que seja protegido pelo serviço {{site.data.keyword.amashort}}. Para obter mais informações sobre como criar um backend móvel, veja [Introdução](getting-started.html).
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
Para obter mais informações, consulte o
[website do CocoaPods](https://cocoapods.org/).

### Instalar o {{site.data.keyword.amashort}} Client SDK com CocoaPods
{: #install-sdk-cocoapods}

1. No Terminal, navegue para o diretório-raiz do seu projeto iOS.

1. Se ainda não tiver inicializado sua área de trabalho para CocoaPods, execute o comando `pod init`.<br/>
O CocoaPods cria um arquivo `Podfile` para você, que fica onde você define as dependências de seu projeto iOS.

1. Edite o arquivo `Podfile` e inclua a linha a seguir nos destinos necessários:

	```
	pod 'IMFCore'
	```

1. Salve o arquivo `Podfile` e execute `pod install` a partir da linha de comandos. <br/>Cocoapods instalam dependências incluídas. É possível ver o progresso e quais componentes foram incluídos.<br/>
**Importante**: o CocoaPods gera um arquivo `xcworkspace`.  Deve-se abrir esse arquivo para trabalhar em seu projeto futuro.

1. Abra sua área de trabalho do projeto iOS. Abra o arquivo `xcworkspace` que foi gerado por CocoaPods. Por exemplo: `{your-project-name}.xcworkspace`. Execute `open {your-project-name}.xcworkspace`.

## Inicializando o {{site.data.keyword.amashort}} Client SDK
{: #init-mca-sdk-ios}

Para usar o {{site.data.keyword.amashort}} Client SDK, deve-se inicializar
o SDK passando os parâmetros **Rota**
(`applicationRoute`) e **GUID do app**
(`applicationGUID`).


1. Na página principal do painel do {{site.data.keyword.Bluemix_notm}}, clique em seu app. Clique em **Opções de dispositivo móvel**. Você
precisa dos valores **Rota** e **GUID do app** para
inicializar o SDK.

1. Importe a estrutura `IMFCore` na classe em que você deseja usar
o {{site.data.keyword.amashort}} Client SDK, incluindo o cabeçalho a seguir:

	**Objective-C:**
	 ```Objective-C
	#import <IMFCore/IMFCore.h>
	```

	**Swift:**

	O {{site.data.keyword.amashort}} Client SDK é implementado com Objective-C. Pode ser necessário incluir um cabeçalho de ponte em seu projeto Swift:

	1. Clique com o botão direito em seu projeto em Xcode e selecione **Novo arquivo..**.
	1. Na categoria **Origem iOS**, clique em **Arquivo de cabeçalho**. Atribua um nome ao arquivo `BridgingHeader.h`.
	1. Inclua a linha a seguir em seu cabeçalho de ponte: `#import <IMFCore/IMFCore.h>`
	1. Clique em seu projeto em Xcode e selecione a guia **Configurações de compilação**.
	1. Procure por `Cabeçalho de ponte do Objective-C`.
	1. Configure o valor para o local do seu arquivo `BridgingHeader.h`, por exemplo, `$(SRCROOT)/MyApp/BridgingHeader.h`.
	1. Assegure-se de que seu cabeçalho de ponte esteja sendo selecionado pelo Xcode, compilando o seu projeto. Nenhuma mensagem de falha deve ser vista.

1. Use o código a seguir para inicializar o {{site.data.keyword.amashort}} Client SDK.  Um local comum, mas não obrigatório, para colocar o código de inicialização é o método `application:didFinishLaunchingWithOptions` de delegado do seu aplicativo. <br/>Substitua os valores *applicationRoute* e *applicationGUID* pelos valores em **Opções de dispositivo móvel** no painel do {{site.data.keyword.Bluemix_notm}}.

	**Objective-C:
                    
**

	```Objective-C
	[[IMFClient sharedInstance]
			initializeWithBackendRoute:@"applicationRoute"
			backendGUID:@"applicationGUID"];
	```

	**Swift:**

	```Swift
IMFClient.sharedInstance().initializeWithBackendRoute("applicationRoute",backendGUID: "applicationGUID")
	```

## Fazendo uma solicitação em seu backend móvel
{: #request}

Depois que o {{site.data.keyword.amashort}} Client SDK for inicializado, será possível começar a fazer solicitações para o seu backend móvel.

1. Tente enviar uma solicitação a um terminal protegido em seu backend móvel no navegador. Abra a URL a seguir: `{applicationRoute}/protected`. Por exemplo: `http://my-mobile-backend.mybluemix.net/protected`
<br/>O terminal `/protected` de um backend móvel que foi criado com o modelo do MobileFirst Services Starter está protegido com o {{site.data.keyword.amashort}}. Uma
mensagem `Unauthorized` é retornada no navegador, pois esse terminal pode ser acessado somente por aplicativos móveis que sejam
instrumentados com o {{site.data.keyword.amashort}} Client SDK.

1. Use seu aplicativo iOS para fazer uma solicitação ao mesmo terminal. Inclua o código a seguir depois de inicializar o `IMFClient`:

	**Objective-C:
                    
**

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

	**Swift:**

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
Quando você se conectou ao terminal protegido, nenhuma credencial foi necessária. Para requerer que os usuários efetuem login no aplicativo, deve-se configurar autenticação do Facebook, Google ou customizada.
  * [Facebook
](facebook-auth-ios.html)
  * [Google](google-auth-ios.html)
  * [Customizada
](custom-auth-ios.html)
