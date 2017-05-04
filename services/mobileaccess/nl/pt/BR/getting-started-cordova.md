---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-04-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

**Importante: o serviço {{site.data.keyword.amafull}} foi substituído pelo serviço {{site.data.keyword.appid_full}}.**

# Configurando o plug-in do Cordova
{: #getting-started-cordova}

Instrua seu aplicativo cliente Cordova com o client SDK
{{site.data.keyword.amafull}}. Inicialize o Gerenciador de Autorização em seu código
Android (Java) ou iOS (Objective C usando o Swift SDK e o arquivo de cabeçalho relevante). Inicialize o cliente e faça solicitações para os recursos
protegidos
e desprotegidos da WebView.

{:shortdesc}

## Antes de iniciar
{: #before-you-begin}
Você deve ter:

* Uma instância de um aplicativo
{{site.data.keyword.Bluemix_notm}}. Para obter mais informações sobre como criar um aplicativo backend do {{site.data.keyword.Bluemix_notm}}, consulte [Introdução](index.html).
* Uma instância de um serviço
{{site.data.keyword.amafull}}.
* A URL do seu aplicativo backend (**Rota de App**). Você precisará desse valor para enviar
solicitações para os terminais protegido do seu aplicativo
backend.
* Seu valor **TenantID**. Abra o seu serviço no painel do {{site.data.keyword.amashort}}. Clique no botão **Opções móveis**. O valor
`tenantId` (também conhecido como
`appGUID`) é exibido no campo **App
GUID / TenantId**. Você precisará desse valor para
inicializar o Gerenciador de Autorização.
* A {{site.data.keyword.Bluemix_notm}}
**Região**. É possível encontrar a sua região
{{site.data.keyword.Bluemix_notm}} atual no cabeçalho,
próximo ao ícone **Avatar**
![ícone de avatar](images/face.jpg "ícone de avatar"). O valor da região que aparece deve ser um dos
seguintes: `US South`, `United Kingdom` ou `Sydney`, e corresponder aos
valores de SDK requeridos no código WebView Javascript:
`BMSClient.REGION_US_SOUTH`,
`BMSClient.REGION_SYDNEY` ou
`BMSClient.REGION_UK`. Você precisará desse
valor para inicializar o cliente
{{site.data.keyword.amashort}}.
* Um aplicativo Cordova ou um projeto existente. Para obter mais informações sobre como
configurar seu aplicativo Cordova, veja o [website Cordova ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://cordova.apache.org/){: new_window}.

## Instalando o plug-in {{site.data.keyword.amashort}} Cordova
{: #getting-started-cordova-plugin}

O SDK do cliente {{site.data.keyword.amashort}} para Cordova é um plug-in Cordova que agrupa os SDKs do cliente
{{site.data.keyword.amashort}} nativos. Ele é distribuído usando a interface de linha de comandos (CLI) do Cordova e `npmjs`, um repositório de plug-in para projetos do Cordova. A CLI Cordova faz download automaticamente dos plug-ins a partir dos repositórios e os disponibiliza ao seu aplicativo Cordova.

1. Inclua Android e/ou plataformas iOS ao seu
aplicativo Cordova. Execute um ou ambos os comandos a seguir a partir da linha de comandos:

	###Android
	{: #install-cordova-android}

	```
	cordova platform add android
	```
	{: codeblock}

	###iOS
	{: #install-cordova-ios}

	```Bash
	cordova platform add ios
	```
	{: codeblock}

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
	{: codeblock}

	O valor *minSdkVersion* deve ser `15` ou mais alto. Consulte o [Guia da Plataforma
Android ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://cordova.apache.org/docs/en/latest/guide/platforms/android/){: new_window} para manter-se atualizado com relação ao
*targetSdkVersion* suportado para o SDK Android.

3. Se você incluiu o sistema operacional iOS, atualize o elemento `<platform name="ios">` com uma declaração de destino:

	```XML
	<platform name="ios">
		<preference name="deployment-target" value="8.0"/>
		<!-- add deployment target declaration -->
	 </platform>
	```
	{: codeblock}

4. Instale o plug-in Cordova do {{site.data.keyword.amashort}}:

 	```Bash
	cordova plugin add bms-core
	```
	{: codeblock}

5. Configure sua plataforma para Android, iOS ou ambos.

	####Android
	{: #cordova-android}

	Antes de abrir seu projeto no Android Studio, compile seu aplicativo Cordova
por meio da interface da linha de comandos (CLI) para evitar erros de compilação.

	```Bash
	cordova build android
	```
	{: codeblock}

	####iOS
	{: #cordova-ios}

	Configure seu projeto Xcode conforme segue.

	1. Use a versão mais recente do Xcode para abrir seu arquivo `xcode.proj` no diretório `<app_name>/platforms/ios`.

		**Importante:** se você receber uma
mensagem para converter para a versão mais recente da sintaxe do
Swift, clique em **Cancelar**.

	2. Compile e execute seu aplicativo com Xcode.

	**Nota**: você pode receber o seguinte erro ao executar `cordova build ios`. Esse problema é devido a um erro em um plug-in de dependência que está sendo
rastreado no [Problema 12 ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://github.com/blakgeek/cordova-plugin-cocoapods-support/issues/12){: new_window}. Você ainda pode executar o projeto do iOS em XCode por meio de um simulador ou dispositivo.

	```
	xcodebuild: erro: impossível localizar um destino correspondente ao identificador de destino fornecido:
			{ platform:iOS Simulator }

		Opção do especificador de dispositivo necessário ausente.
		O tipo de dispositivo “Simulador iOS” requer que qualquer “nome” ou “id” seja especificado.
		Forneça o “nome” ou “id”.
	```

6. Verifique se o plug-in foi instalado com sucesso, executando o comando a seguir:

	```Bash
	cordova plugin list
	```
	{: codeblock}

7. Ativar Compartilhamento Keychain para iOS
alternando
**Compartilhamento Keychain** para
`Ligado` na guia
**Recursos**.

8. Ative **Define módulo** para iOS
alternando **Define módulo** para
`YES` na guia **Configurações de
construção** > **Pacote**.


## Inicializando o cliente {{site.data.keyword.amashort}}
no Cordova WebView (Javascript)
{: #getting-started-cordova-initialize}

Para usar o cliente
SDK {{site.data.keyword.amashort}}, deve-se inicializar o SDK passando o
`applicationBluemixRegion`.

Inclua a chamada a seguir no arquivo `index.js` para inicializar o {{site.data.keyword.amashort}} client SDK.

```JavaScript
BMSClient.initialize(<applicationBluemixRegion>);
```
{: codeblock}

**NB:** substitua `<
applicationBluemixRegion>` pela região em que seu
{{site.data.keyword.Bluemix_notm}} serviço está
hospedado, consulte [Antes
de iniciar](#before-you-begin).

##Inicializando o {{site.data.keyword.amashort}}
AuthorizationManager do seu código nativo
{: #initializing-auth-manager}

Para usar `BMSAuthorizationManager`, você
precisará incluir o fragmento de código a seguir. O código
nativo a seguir inicializa o
`BMSAuthorizationManager` com o serviço
{{site.data.keyword.amashort}}
`tenantId` (consulte
[Antes de iniciar](#before-you-begin)).

### Android (Java)

No método `OnCreate` no arquivo
`MainActivity.java`, inclua o código
antes de `loadUrl`.
```Java
MCAAuthorizationManager mcaAuthorizationManager = MCAAuthorizationManager.createInstance(this.getApplicationContext(),"<tenantId>");
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);
```
{: codeblock}
### iOS (Objective C)
Inclua a inicialização Gerenciador de Autorização no
`AppDelegate.m` de acordo com sua versão do
Xcode.

```Objective-C
  #import "<your_module_name>-Swift.h"
  [CDVBMSClient initMCAAuthorizationManagerManagerWithTenantId:@"<tenantId>"];
```
{: codeblock}

**Nota:** o nome do arquivo de
cabeçalho importado é composto por seu nome de módulo concatenado
para a sequência `-Swift.h`, por exemplo, se o
nome do seu módulo for `Cordova`, a linha
de importação seria `#import "Cordova-Swift.h"`.
Para localizar o nome do módulo, acesse `Configurações
de construção` > `Pacote` >
`Nome do módulo de produto`.
Substitua seu ID do
locatário `<tenantId>` (consulte
[Antes de
iniciar](#before-you-begin)).


## Fazendo uma solicitação para o serviço de backend móvel
{: #getting-started-request}

Após a inicialização do cliente SDK
{{site.data.keyword.amashort}}, é possível
iniciar as solicitações para seu serviço de backend móvel.

1. Tente enviar uma solicitação para um terminal
protegido do seu aplicativo backend móvel. Em
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

	 var request = new BMSRequest("<your route>/protected", BMSRequest.GET);

	 request.send(success, failure);
	```
	{: codeblock}

3. Quando a solicitação for bem-sucedida, você verá a saída a seguir no console LogCat ou Xcode (dependendo da plataforma que estiver sendo usada):

	![Mensagem de êxito](images/getting-started-android-success.png)

	## Próximas etapas
	{: #next-steps}

	Quando você se conectou ao terminal protegido, nenhuma credencial foi necessária. Para requerer que os usuários efetuem login em seu aplicativo, deve-se configurar a autenticação do Facebook, do Google ou customizada.
	* [Facebook](facebook-auth-cordova.html)
	* [Google](google-auth-cordova.html)
	* [Customizada](custom-auth-cordova.html)
