---

copyright:
  years: 2015, 2016 lastupdated: "2016-10-02"  
---
{:shortdesc: .shortdesc} 

# Configurando o plug-in do Cordova
{: #getting-started-cordova}


Instrumente seu aplicativo Cordova com o SDK do cliente {{site.data.keyword.amafull}}, inicialize o SDK e faça solicitações aos
recursos protegidos e não protegidos.

{:shortdesc}

## Antes de Começar
{: #before-you-begin}
Você deve ter:
* Uma instância de um aplicativo {{site.data.keyword.Bluemix_notm}} que seja protegida pelo serviço {{site.data.keyword.amashort}}. Para obter mais informações sobre como criar um aplicativo backend do {{site.data.keyword.Bluemix_notm}}, consulte [Introdução](index.html).

* Um aplicativo Cordova ou um projeto existente. Para obter mais informações sobre como configurar seu aplicativo Cordova, consulte o [website Cordova](https://cordova.apache.org/).

## Instalando o plug-in {{site.data.keyword.amashort}} Cordova
{: #getting-started-cordova-plugin}

O SDK do cliente {{site.data.keyword.amashort}} para Cordova é um plug-in Cordova que agrupa os SDKs do cliente
{{site.data.keyword.amashort}} nativos. Ele é distribuído usando a interface de linha de comandos (CLI) do Cordova e `npmjs`, um repositório de plug-in para projetos do Cordova. A CLI Cordova faz download automaticamente dos plug-ins a partir dos repositórios e os disponibiliza ao seu aplicativo Cordova.

1. Inclua as plataformas Android e iOS em seu aplicativo Cordova. Execute um ou ambos os comandos a seguir a partir da linha de comandos:
   	
	###Android
	{: #install-cordova-android}

	```
	cordova platform add android
	```
	
	###iOS
	{: #install-cordova-ios}

	```Bash
	cordova platform add ios
	```

2. Se você incluiu a plataforma Android, deve-se incluir o nível mínimo de API suportado no arquivo `config.xml` do aplicativo Cordova. Abra
o arquivo `config.xml` e inclua a linha a seguir no elemento `<platform
name="android">`:

	```XML
	<platform name="android">  
		<preference name="android-minSdkVersion" value="15"/>
  	<preference name="android-targetSdkVersion" value="23"/>
		<!-- add minimum and target Android API level declaration -->
	</platform>
	```
	
	O valor *minSdkVersion* deve ser `15` ou mais alto. O valor *targetSdkVersion* deve ser o Android SDK mais recente disponível no Google.

3. Se você incluiu o sistema operacional iOS, atualize o elemento `<platform name="ios">` com uma declaração de destino:

	```XML
	<platform name="ios">
		<preference name="deployment-target" value="8.0"/>
		<!-- add deployment target declaration -->
	 </platform>
	```

4. Instale o plug-in do Cordova do {{site.data.keyword.amashort}}:

 	```Bash
	cordova plugin add ibm-mfp-core
	```

5. Configure sua plataforma para Android, iOS ou ambos.

	####Android
	{: #cordova-android}

	Antes de abrir seu projeto no Android Studio, compile seu aplicativo Cordova
por meio da interface da linha de comandos (CLI) para evitar erros de compilação.
	
	```Bash
	cordova build android
	```
	
	####iOS
	{: #cordova-ios}

	Configure seu projeto Xcode conforme a seguir, para evitar erros de compilação.

	1. Use a versão mais recente do Xcode para abrir seu arquivo `xcode.proj` no diretório `<app_name>/platforms/ios`.

		**Importante:** se você receber uma mensagem para converter para a versão mais recente da sintaxe do
Swift, clique em **Cancelar**.

	2. Acesse **Configurações de compilação > Compilador Swift - Geração de código > Cabeçalho de ponte do Objective-C** e
inclua o caminho a seguir:

		`<your_project_name>/Plugins/ibm-mfp-core/Bridging-Header.h`

	3. Acesse **Configurações de compilação > Vinculação > Caminhos de procura Runpath** e inclua o parâmetro Frameworks a seguir:

		`@executable_path/Frameworks`

	4. Compile e execute seu aplicativo com Xcode.

6. Verifique se o plug-in foi instalado com sucesso, executando o comando a seguir:

	```Bash
	cordova plugin list
	```

## Inicializando o plug-in do cliente {{site.data.keyword.amashort}}
{: #getting-started-cordova-initialize}

Para usar o {{site.data.keyword.amashort}} client SDK, deve-se inicializar o SDK passando os parâmetros *applicationGUID* e *applicationRoute*.

1. Localize os valores de rota e de GUID do app na página principal do painel do {{site.data.keyword.Bluemix_notm}}. Clique no nome do seu aplicativo e depois em **Opções móveis** para exibir os valores **Rota de aplicativo** e **GUID de aplicativo** para inicializar o SDK.

3. Inclua a chamada a seguir no arquivo `index.js` para inicializar o {{site.data.keyword.amashort}} client SDK. 

	```JavaScript
	BMSClient.initialize("applicationRoute", "applicationGUID");
	```

  * Substitua `applicationRoute` e
`applicationGUID` pelos valores de **Opções móveis**
no painel {{site.data.keyword.Bluemix_notm}}.

##Inicializando o {{site.data.keyword.amashort}} AuthorizationManager
{: #initializing-auth-manager}

Use o código JavaScript a seguir no aplicativo Cordova para inicializar o
{{site.data.keyword.amashort}} AuthorizationManager.

```JavaScript
  MFPAuthorizationManager.initialize("tenantId");
```

Substitua o valor `tenantId` pelo `tenantId` do serviço
{{site.data.keyword.amashort}}. Esse valor pode ser localizado clicando no
botão **Mostrar credenciais** no quadro do serviço
{{site.data.keyword.amashort}}.

## Fazendo uma solicitação ao aplicativo backend móvel
{: #getting-started-request}

Após o SDK do cliente {{site.data.keyword.amashort}} ser inicializado, será possível começar a fazer solicitações ao seu aplicativo
backend móvel.

1. Tente enviar uma solicitação a um terminal protegido do seu novo aplicativo backend móvel. Em
seu navegador, abra a URL a seguir: `{applicationRoute}/protected` (por
exemplo: `http://my-mobile-backend.mybluemix.net/protected`).

	O terminal `/protected` de um aplicativo backend móvel que foi criado com o modelo MobileFirst Services Starter é protegido com {{site.data.keyword.amashort}}. Uma mensagem `Unauthorized` é retornada no navegador. Essa mensagem é retornada porque esse terminal é acessado somente por aplicativos móveis instrumentados com o {{site.data.keyword.amashort}} client SDK.

2. Use seu aplicativo Cordova para fazer uma solicitação para o mesmo terminal. Inclua o código a seguir depois de inicializar `BMSClient`:

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

3. Quando a solicitação for bem-sucedida, você verá a saída a seguir no console LogCat ou Xcode (dependendo da plataforma que estiver sendo usada):

	![image](images/getting-started-android-success.png)

	## Próximas Etapas
	{: #next-steps}

	Quando você se conectou ao terminal protegido, nenhuma credencial foi necessária. Para requerer que os usuários efetuem login em seu aplicativo, deve-se configurar a autenticação do Facebook, do Google ou customizada.
	* [Facebook](facebook-auth-cordova.html)
	* [Google](google-auth-cordova.html)
	* [Customizada](custom-auth-cordova.html)
