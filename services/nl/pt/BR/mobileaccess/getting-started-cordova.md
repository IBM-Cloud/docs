---

copyright:
  years: 2015, 2016
  
---

# Configurando o plug-in do Cordova
{: #getting-started-cordova}

Instrumente seu aplicativo Cordova com o {{site.data.keyword.amashort}} Client SDK, inicialize o SDK e faça solicitações para recursos protegidos e não protegidos.

## Antes de Começar
{: #before-you-begin}

- Deve-se ter uma instância de um backend móvel que seja protegido pelo serviço {{site.data.keyword.amashort}}. Para obter mais informações sobre como criar um backend móvel, consulte [Introdução](getting-started.html).

- Crie um aplicativo Cordova ou use um projeto existente. Para obter mais informações sobre como configurar seu aplicativo Cordova, consulte o [website do Cordova](https://cordova.apache.org/).

## Instalando o plug-in do Cordova do {{site.data.keyword.amashort}}
{: #getting-started-cordova-plugin}

O {{site.data.keyword.amashort}} Client SDK para Cordova é um plug-in do Cordova que está agrupando os {{site.data.keyword.amashort}} Client SDKs nativos. Ele é distribuído usando a interface de linha de comandos (CLI) do Cordova e `npmjs`, um repositório de plug-in para projetos do Cordova. O Cordova CLI faz download automaticamente de plug-ins de repositórios e os torna disponíveis para seu aplicativo Cordova.

1. Inclua as plataformas Android e iOS em seu aplicativo Cordova. Execute um ou ambos os comandos a seguir a partir da linha de comandos:

	```Bash
	cordova platform add android
	```

	```Bash
	cordova platform add ios
	```

1. Se você incluiu a plataforma Android, deve-se incluir o nível mínimo de API suportado no arquivo `config.xml` do aplicativo Cordova. Abra o arquivo `config.xml` e inclua a linha a seguir no elemento `<platform name="android">`:

	```XML
	<platform name="android">  
		<preference name="android-minSdkVersion" value="15"/>
  	<preference name="android-targetSdkVersion" value="23"/>
		<!-- add minimum and target Android API level declaration -->
	</platform>
	```

	O valor *minSdkVersion* deve ser maior que `15`. O valor *targetSdkVersion* deve ser o Android SDK mais recente disponível no Google.

1. Se você incluiu o sistema operacional iOS, atualize o elemento `<platform name="ios">` com uma declaração de destino:

	```XML
	<platform name="ios">
    <preference name="deployment-target" value="8.0"/>
		<!-- add deployment target declaration -->
	</platform>
	```

1. Instale o plug-in Cordova do {{site.data.keyword.amashort}}:

 	```Bash
	cordova plugin add ibm-mfp-core
	```

1. Configure a plataforma do Android e/ou iOS.

	* **Android**

		Antes de abrir seu projeto no Android Studio, compile seu aplicativo Cordova
por meio da interface da linha de comandos (CLI) para evitar erros de compilação.

		```
		cordova build android
		```

	* **iOS**

		Configure seu projeto Xcode conforme a seguir, para evitar erros de compilação.

		1. Use a versão mais recente do Xcode para abrir o arquivo xcode.proj no
diretório &lt;*app_name*&gt;/platforms/ios.

		**Importante:** se você receber uma mensagem para "Converter na sintaxe mais recente do Swift", clique em Cancelar.

		2. Acesse **Configurações de compilação > Compilador Swift - Geração de
códigos > Cabeçalho de ponte Objective-C** e inclua o caminho a seguir:

			```
			<your_project_name>/Plugins/ibm-mfp-core/Bridging-Header.h
			```

		3. Acesse **Configurações de compilação > Link > Caminhos da procura
Runpath** e inclua o parâmetro Frameworks a seguir:

			```
			@executable_path/Frameworks
			```

		4. Compile e execute seu aplicativo com Xcode.

1. Verifique se o plug-in foi instalado com êxito executando o comando a seguir:

	```Bash
	cordova plugin list
	```

## Inicializando o plug-in do Cliente {{site.data.keyword.amashort}}
{: #getting-started-cordova-initialize}

Para usar o {{site.data.keyword.amashort}} Client SDK, deve-se inicializar o SDK passando os parâmetros *applicationGUID* e *applicationRoute*.

1. Localize os valores de rota e de GUID do app na página principal do painel do {{site.data.keyword.Bluemix_notm}}. Clique no nome do app e, em seguida, em **Opções de dispositivo móvel** para exibir os valores **Application route** e **Application GUID** para inicializar o SDK.

3. Inclua a chamada a seguir no arquivo `index.js` para inicializar o {{site.data.keyword.amashort}} Client SDK. Substitua
*applicationRoute* e *applicationGUID* pelos valores das
**Opções móveis** no painel
{{site.data.keyword.Bluemix_notm}}.

	```JavaScript
	BMSClient.initialize("applicationRoute", "applicationGUID");
	```

## Fazendo uma solicitação para o backend móvel
{: #getting-started-request}

Após a inicialização do {{site.data.keyword.amashort}} Client SDK, é possível começar a fazer solicitações para seu backend móvel.

1. Tente enviar uma solicitação para um terminal protegido de seu novo backend móvel. Em seu navegador, abra esta URL: `{applicationRoute}/protected`. Por exemplo:

	```
	http://my-mobile-backend.mybluemix.net/protected
	```

	O terminal `/protected` de um backend móvel que foi criado com o
modelo MobileFirst Services Starter é protegido com
{{site.data.keyword.amashort}}. Uma mensagem `Unauthorized` é retornada no navegador. Essa mensagem é retornada porque esse terminal é acessado somente por aplicativos móveis instrumentados com o {{site.data.keyword.amashort}} Client SDK.

1. Use seu aplicativo Cordova para fazer uma solicitação para o mesmo terminal. Inclua o código a seguir depois de inicializar `BMSClient`:

	```Javascript
	var success = function(data){
	console.log("success", data);
	}

	var failure = function(error){
		console.log("failure", error);
	}

	var request = new MFPRequest("/protected", MFPRequest.GET);

	request.send(success, failure);
	```

1. Quando a solicitação for bem-sucedida, você verá a saída a seguir no console LogCat ou Xcode (dependendo da plataforma que estiver sendo usada):

	![image](images/getting-started-android-success.png)

	## Próximas Etapas
	{: #next-steps}

	Quando você se conectou ao terminal protegido, nenhuma credencial foi necessária. Para requerer que os usuários efetuem login em seu aplicativo, deve-se configurar a autenticação do Facebook, do Google ou customizada.
	* [Facebook](facebook-auth-cordova.html)
	* [Google](google-auth-cordova.html)
	* [Customizada](custom-auth-cordova.html)
