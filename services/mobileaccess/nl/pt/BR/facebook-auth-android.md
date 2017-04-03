---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

O serviço {{site.data.keyword.amafull}} foi substituído pelo serviço {{site.data.keyword.appid_full}}.

# Ativando a autenticação do Facebook para apps Android
{: #facebook-auth-android}

Para usar o Facebook como provedor de identidade em seus
{{site.data.keyword.amafull}} aplicativos clientes
Android, inclua e configure o cliente Android para acessar seu
aplicativo Facebook no site Facebook for Developers.
{:shortdesc}

## Antes de Começar
{: #before-you-begin}

Você deve ter:

* Uma instância de um serviço
{{site.data.keyword.amafull}} e um aplicativo
{{site.data.keyword.Bluemix_notm}}. Para obter mais informações sobre como criar um aplicativo backend do {{site.data.keyword.Bluemix_notm}}, consulte [Introdução](index.html).
* A URL do seu aplicativo backend (**Rota de App**). Você precisará desse valor para enviar
solicitações para os terminais protegidos do seu aplicativo
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
seguintes: `US South`, `United Kingdom` ou `Sydney`, e corresponder ao
valor de SDK requerido no código WebView Javascript:
`BMSClient.REGION_US_SOUTH`,
`BMSClient.REGION_SYDNEY` ou
`BMSClient.REGION_UK`. Você precisará desse
valor para inicializar o cliente
{{site.data.keyword.amashort}}.
* Um projeto do Android que esteja configurado para trabalhar com Gradle. O projeto não precisa ser instrumentado com o {{site.data.keyword.amashort}} client SDK.  
* Um app Facebook com uma plataforma Android no [site
Facebook for Developers ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://developers.facebook.com/){: new_window}.

**Importante:** não é necessário instalar separadamente o Facebook SDK (`com.facebook.FacebookSdk`). O Facebook SDK é instalado automaticamente pelo Gradle quando você inclui o {{site.data.keyword.amashort}} Facebook client SDK. É possível ignorar esta etapa ao incluir a plataforma Android no site Facebook for Developers.

## Configurando o aplicativo site no Facebook for Developers
{: #facebook-auth-android-config}

No website Facebook for Developers:

1. Efetue login em sua conta no [website Facebook for Developers ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://developers.facebook.com){: new_window}.

1. Na **Lista de Produtos**, escolha
**Facebook Login**.

1. Inclua ou configure a plataforma Android.

1. Especifique o nome do pacote do aplicativo Android no prompt Nome do pacote do Google Play. Para localizar o nome do pacote do seu
aplicativo Android, procure `<manifest ..... package="{your-package-name}">` no arquivo
`AndroidManifest.xml` no projeto Android Studio.

1. Especifique o nome de classe de sua atividade principal no prompt **Nome de classe**. O nome de classe é o valor da propriedade `android:name` no gabinete de atividade. Se
houver mais de uma atividade no arquivo `AndroidManifest.xml`, procure a atividade que contenha o `<intent-filter>`:

	```XML
	<activity
		android:name=".MainActivity"
		android:label="@string/app_name">
		<intent-filter>
			<action android:name="android.intent.action.MAIN"/>
			<category android:name="android.intent.category.LAUNCHER"/>
		</intent-filter>
	</activity>
	```
	{: codeblock}

1. Para que o Facebook assegure a autenticidade de seu aplicativo, deve-se especificar um hash de seu certificado de desenvolvedor SHA1.

	**Mais sobre a segurança do Android:** o sistema operacional Android requer que todos os aplicativos instalados em um dispositivo Android sejam assinados com um certificado de desenvolvedor. O aplicativo Android pode ser construído em dois modos: depuração e liberação.

	Use certificados diferentes para os modos de depuração e liberação.  Certificados usados para assinatura de aplicativos Android no modo de depuração são empacotados com o Android SDK que, em geral, é instalado automaticamente pelo Android Studio. Quando desejar liberar seu app no armazenamento do Google Play, você deverá assinar seu app com outro certificado que, em geral, você mesmo gera.

	É possível inserir dois conjuntos de hashes de chave com o Facebook: um hash de chave
para aplicativos que são construídos no modo de depuração com um certificado de depuração e
outro hash de chave para aplicativos que são construídos no modo de liberação com um certificado
de liberação. Para obter mais informações, veja [Assinando seus
aplicativos Android ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](http://developer.android.com/tools/publishing/app-signing.html){: new_window}.

1. O keystore que contém o certificado que você está usando para o ambiente de desenvolvimento é armazenado no arquivo `~/.android/debug.keystore`. A senha do keystore padrão é: `android`. Use esse certificado para construir aplicativos no modo de depuração.

1. Recupere o hash chave do certificado no modo de depuração:

	```XML
	keytool -exportcert -alias androiddebugkey -keystore ~/.android/debug.keystore | openssl sha1 -binary | openssl base64
	```
	{: codeblock}

	**Dica**: é possível usar a mesma sintaxe para recuperar o hash chave do seu certificado de modo de liberação. Substitua o caminho do alias e do keystore no comando.

1. Copie e cole o hash chave que obteve com o comando **keytool** para um prompt de Hashes chave de
desenvolvimento/liberação no site Facebook for Developers.

	**Dica**: considere a ativação da conexão única se você estiver planejando usar esse recurso.

1. Clique em **Salvar Configurações**.

## Configurando o serviço {{site.data.keyword.amashort}}
para autenticação do Facebook
{: #facebook-auth-android-mca}

Após ter o ID do Aplicativo Facebook e ter configurado o Aplicativo Facebook para atender a clientes Android, é possível ativar a autenticação do Facebook com o painel {{site.data.keyword.amashort}}.

1. Abra o seu serviço {{site.data.keyword.amashort}} no painel.
1. Na guia **Gerenciar**, acione
**Autorização**.
1. Expanda a seção **Facebook**.
1. Inclua o **ID do aplicativo Facebook**.
1. Clique em **Salvar**.

## Configurando o cliente Android SDK {{site.data.keyword.amashort}}
para autenticação do Facebook
{: #facebook-auth-android-sdk}

Para configurar o cliente SDK para Android, use o gerenciador de dependência Gradle no Android Studio.

1.  Abra o arquivo `build.gradle` do módulo do app.
Seu projeto Android pode ter dois arquivos `build.gradle`: para o projeto e o módulo do aplicativo. Use o arquivo do módulo do aplicativo.

1. Localize a seção de dependências do arquivo `build.gradle` e inclua uma nova dependência de compilação para o Client SDK:

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'facebookauthentication',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// other dependencies  
	}
	```
	{: codeblock}

	**Nota:** é possível remover a dependência no módulo `core` do grupo `com.ibm.mobilefirstplatform.clientsdk.android`, se estiver em seu arquivo. O módulo `facebookauthentication` faz download do módulo `core`, assim como do próprio SDK do Facebook, automaticamente.

	Depois que você salva as atualizações, o módulo `facebookauthentication` faz download e instala todos os SDKs necessários no projeto do Android.

1. Sincronize seu projeto com o Gradle clicando em
**Ferramentas > Android > Sincronizar projeto com
arquivos Gradle**.

1. Abra o arquivo `res/values/strings.xml` e inclua uma sequência `facebook_app_id` que contenha seu ID do aplicativo Facebook:

	```XML
	<resources>
		<string name="app_name">HelloWorld</string>
		<string name="action_settings">Settings</string>
		<string name="facebook_app_id">522733366802111</string>
	</resources>
	```
	{: codeblock}

1. No arquivo `AndroidManifest.xml` do projeto do Android:
	* Inclua a permissão de acesso à Internet sob o elemento `<manifest>`:

		```XML
	<uses-permission android:name="android.permission.INTERNET" />
		```
		{: codeblock}

	* Inclua metadados necessários para o Facebook SDK no elemento `<application>`:

		```XML
    <application .......>

			<meta-data
			android:name="com.facebook.sdk.ApplicationId"
			android:value="@string/facebook_app_id"/>

			<activity ...../>
    <activity ...../>
    </application>
		```
		{: codeblock}

	* Inclua um elemento de Atividade do Facebook sob as atividades existentes:

		```XML
    <application .....>
			<activity ...../>
		<activity ...../>

			<activity android:name="com.facebook.FacebookActivity"
				android:configChanges="keyboard|keyboardHidden|screenLayout|screenSize|orientation"
				android:theme="@android:style/Theme.Translucent.NoTitleBar"
				android:label="@string/app_name" />
		</application>
		```
		{: codeblock}

1. Inicialize o cliente SDK e registre o gerenciador de
autenticação. Inicialize o SDK do cliente do {{site.data.keyword.amashort}} passando **context** e **region**.

	Um local comum, mas não obrigatório, para colocar o código de inicialização é o método `onCreate` da atividade principal em seu aplicativo Android.<br/>

	```Java 	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_UK);

	BMSClient.getInstance().setAuthorizationManager(
					MCAAuthorizationManager.createInstance(this, "<MCAServiceTenantId>"));

	FacebookAuthenticationManager.getInstance().register(this);
	```
	{: codeblock}

   * Substitua `BMSClient.REGION_UK` pela região apropriada.
   * Substitua `<
MCAServiceTenantId>` pelo valor `tenantId`

	Para mais
informações sobre como obter esses valores, consulte
[Antes de iniciar](#before-you-begin)).

	**Nota:** se seu aplicativo Android está definindo como destino o Android versão 6.0 (API nível 23) ou superior, deve-se assegurar que o aplicativo tenha uma chamada `android.permission.GET_ACCOUNTS` antes de chamar `register`. Para obter
mais informações, veja [esse
tópico ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://developer.android.com/training/permissions/requesting.html){: new_window} no site Android Developers.

1. Inclua o código a seguir em sua Atividade:

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		FacebookAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
	```
	{: codeblock}


## Testando a Autenticação
{: #testing_auth}

Após a inicialização do client SDK e o registro do Gerenciador de autenticação do Facebook, será possível começar a fazer solicitações para seu backend móvel.

### Antes de iniciar o teste
{: #facebook-auth-android-testing-before}

Deve-se estar usando o modelo {{site.data.keyword.mobilefirstbp}} e já ter um recurso protegido pelo {{site.data.keyword.amashort}}
no terminal `/protected`. Se for necessário configurar um terminal `/protected`, consulte [Protegendo recursos](protecting-resources.html).

1. Tente enviar uma solicitação a um terminal protegido do seu aplicativo backend móvel recém-criado em seu navegador. Abra a URL a seguir:

	`{applicationRoute}/protected`. Por exemplo: `http://my-mobile-backend.mybluemix.net/protected`.  

	O terminal `/protected` de um aplicativo backend móvel que foi criado com o modelo MobileFirst Services Starter é protegido com {{site.data.keyword.amashort}}. Uma mensagem `Unauthorized` é retornada no navegador. Essa mensagem é retornada porque esse terminal só pode ser acessado por aplicativos móveis instrumentados com o {{site.data.keyword.amashort}} client SDK.

1. Use seu aplicativo Android para fazer solicitação ao mesmo terminal. Inclua
o código a seguir depois de inicializar `BMSClient` e registrar
`FacebookAuthenticationManager`.

	```Java
	Request request = new Request("{applicationRoute}/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText()); 			Log.d("MyApp", MCAAuthorizationManager.getInstance().getUserIdentity().toString()); 		}
		@Override
		public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
			if (null != t) {
				Log.d("Myapp", "onFailure :: " + t.getMessage());
			} else if (null != extendedInfo) {
				Log.d("Myapp", "onFailure :: " + extendedInfo.toString());
			} else {
				Log.d("Myapp", "onFailure :: " + response.getResponseText());
			}
		}
	});
	```
	{: codeblock}

1. Execute o aplicativo. Uma tela de login do Facebook é exibida.

	![image](images/android-facebook-login.png)

	Essa tela poderá parecer um pouco diferente se o app Facebook não estiver instalado em seu dispositivo, ou se você não estiver atualmente conectado ao Facebook.

1. Clique em **OK** para autorizar o {{site.data.keyword.amashort}} a usar sua identidade de usuário do Facebook para propósitos de autenticação.

1. Quando sua solicitação for bem-sucedida, a saída a seguir estará no utilitário LogCat:

	![image](images/android-facebook-login-success.png)

	Também é possível incluir a funcionalidade de logout incluindo o código a seguir:

	```
	FacebookAuthenticationManager.getInstance().logout(getApplicationContext(), listener);
	```
	{: codeblock}

	Se você chamar esse código depois que um usuário estiver conectado ao Facebook, ele será desconectado. Quando o usuário tentar efetuar login novamente, ele será solicitado a fornecer as credenciais do Facebook.

	O valor para `listener` passado para a função de logout pode ser `null`.
