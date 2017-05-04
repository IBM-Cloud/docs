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

# Ativando a autenticação do Google para apps Android
{: #google-auth-android}

Use o Google para autenticar usuários em seu aplicativo
{{site.data.keyword.amafull}} Android. Inclua a funcionalidade de segurança do {{site.data.keyword.amashort}}.

## Antes de iniciar
{: #before-you-begin}

Você deve ter:

* Uma instância de um serviço
{{site.data.keyword.amafull}} e um aplicativo
{{site.data.keyword.Bluemix_notm}}. Para obter mais informações sobre como criar um aplicativo backend do {{site.data.keyword.Bluemix_notm}}, consulte [Introdução](index.html).
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
* Um projeto do Android que esteja configurado para trabalhar com Gradle. O projeto não precisa ser instrumentado com o {{site.data.keyword.amashort}} client SDK.  

Configurar a autenticação do Google para seu app Android do {{site.data.keyword.amashort}} irá requerer configuração adicional de:

* O aplicativo {{site.data.keyword.Bluemix_notm}}
* Seu projeto do Android Studio

## Criando um projeto no Console do desenvolvedor do Google
{: #create-google-project}

Para começar a usar o Google como um provedor de identidade, crie um projeto no
[Console do Google Developer ![Ícone de link
externo](../../icons/launch-glyph.svg "External link icon")](https://console.developers.google.com){: new_window}.
Parte da criação de um projeto é obter um identificador de cliente do Google.  O identificador de cliente do Google é um identificador
exclusivo para seu aplicativo usado pela autenticação do Google
e é necessário para configurar o serviço
{{site.data.keyword.amashort}}.

No console:

1. Crie um projeto usando a API do **Google+**.
2. Inclua o acesso de usuário **OAuth**.
3. Antes de incluir as credenciais, deve-se escolher a plataforma (Android).
4. Inclua as credenciais.

Para concluir a criação de credenciais, é necessário incluir a **impressão digital do certificado de assinatura**.


### Configurando o certificado de assinatura
{: #signing_cert}

Para que o Google verifique a autenticidade de seu aplicativo, deve-se especificar uma impressão digital do certificado de assinatura.

O sistema operacional Android requer que todos os aplicativos instalados em um dispositivo Android sejam assinados com um certificado de desenvolvedor. Um aplicativo Android pode ser construído em dois modos: depuração e liberação. É aconselhável geralmente ter certificados diferentes para os modos de depuração e liberação.  Certificados usados para assinatura de aplicativos Android no modo de depuração são empacotados com o Android SDK.  Em geral, o Android SDK é instalado automaticamente pelo Android Studio. Quando desejar liberar seu aplicativo para o Google Play, deve-se assinar o app com outro certificado que, em geral, você mesmo gera. Para obter mais informações, veja [Assinando seus
aplicativos Android ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](http://developer.android.com/tools/publishing/app-signing.html){: new_window}.

Um keystore que contém um certificado para ambientes de desenvolvimento é armazenado em um arquivo `~/.android/debug.keystore`. A senha padrão do keystore é: `android`. Esse certificado é usado para construir aplicativos no modo de depuração.

1. Recupere a impressão digital do certificado de assinatura do ambiente de desenvolvimento do cliente:

	```XML
	keytool -exportcert -alias androiddebugkey -keystore ~/.android/debug.keystore -list -v
	```
	{: codeblock}

	Também é possível usar a mesma sintaxe para recuperar o hash chave do certificado no modo de liberação. Substitua o caminho do alias e do keystore no comando.

1. No diálogo Credencial do console do Google, localize a linha iniciada com `SHA1` em **Impressões digitais do certificado**. Copie o valor da impressão digital obtida ao executar o comando **keytool** para a caixa de texto.

###Nome do Pacote

1. No diálogo Credenciais, insira o nome do pacote do aplicativo Android.

	Para localizar o nome do pacote de seu aplicativo Android, abra o arquivo
`AndroidManifest.xml` no Android Studio e procure:

	```
	<manifest package="{your-package-name}">
	```
	{: codeblock}

1. Quando terminar, clique em **Criar**. Isso conclui a criação de credenciais.

###Identificador de cliente do Google
{: #google-client-id}

Quando as credenciais são criadas com êxito, a página de credenciais exibe o identificador de cliente do Google. Anote esse valor. Será necessário registrar esse valor no aplicativo {{site.data.keyword.Bluemix}}.


## Configurando o {{site.data.keyword.amashort}} para autenticação do Google
{: #google-auth-android-config}

Agora que você possui um identificador de cliente do Google para Android, é possível ativar a autenticação do Google no Painel do {{site.data.keyword.amashort}}.

1. Abra o seu serviço no painel do {{site.data.keyword.amashort}}.
1. Na guia **Gerenciar**, acione
**Autorização**.
1. Expanda a seção **Google**.
1. No **ID do Cliente para Android**,
especifique o identificador de cliente do Google para Android e
clique em **Salvar**.

## Configurando o {{site.data.keyword.amashort}} client SDK para Android
{: #google-auth-android-sdk}

No seu projeto Android Studio.

1. Abra o arquivo `build.gradle` do módulo do app.

	Seu projeto Android pode ter dois arquivos `build.gradle`: um para o projeto e outro para o módulo do aplicativo. Use o módulo do aplicativo.

	Localize a seção de dependências e inclua uma nova dependência de compilação para o Client SDK:

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'googleauthentication',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// other dependencies  
	}
	```
	{: codeblock}

	**Nota:** será possível remover a dependência do módulo `core` do grupo `com.ibm.mobilefirstplatform.clientsdk.android`, se você o tiver. O módulo `googleauthentication` faz download dele automaticamente para você. O módulo `googleauthentication` faz download e instala o Google+ SDK no projeto do Android.

1. Sincronize seu projeto com o Gradle clicando em **Ferramentas > Android > Sincronizar projeto com arquivos Gradle**.

1. Abra o arquivo `AndroidManifest.xml` de seu projeto Android.

1. Inclua a permissão de acesso à Internet no elemento `<manifest>`:

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
	<uses-permission android:name="android.permission.GET_ACCOUNTS" />
	<uses-permission android:name="android.permission.USE_CREDENTIALS" />
	```
	{: codeblock}

1. Para usar o SDK do cliente do {{site.data.keyword.amashort}}, deve-se inicializar o SDK passando os parâmetros **context** e **region**.

	Um local comum, mas não obrigatório, para colocar o código de inicialização é o método `onCreate` da atividade principal em seu aplicativo Android.

1. Inicialize o client SDK e registre o gerenciador de autenticação do Google.

	```Java 	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_UK);

	BMSClient.getInstance().setAuthorizationManager(
					MCAAuthorizationManager.createInstance(this, "<MCAServiceTenantId>"));

	GoogleAuthenticationManager.getInstance().register(this);
	```
	{: codeblock}

	* Substitua `BMSClient.REGION_UK` pela
sua {{site.data.keyword.Bluemix_notm}}
**Região**.
	* Substitua `<
MCAServiceTenantId>` pelo valor
**TenantId**.

	Para obter mais
informações sobre como obter esses valores, consulte
[Antes de iniciar](##before-you-begin).

	**Nota:** se seu aplicativo Android está definindo como destino o Android versão 6.0 (API nível 23) ou superior, deve-se assegurar que o aplicativo tenha uma chamada `android.permission.GET_ACCOUNTS` antes de chamar `register`. Para obter
mais informações, veja [Solicitando permissões no
Android ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://developer.android.com/training/permissions/requesting.html){: new_window}.

1. Inclua o código a seguir em sua Atividade:

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		GoogleAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
	```
	{: codeblock}

## Testando a Autenticação
{: #google-auth-android-test}

Depois que o cliente SDK é inicializado e o Gerenciador de
autenticação do Google é registrado, é possível começar a fazer
solicitações para seu aplicativo backend.

Antes de iniciar o teste, deve-se ter um aplicativo backend móvel que tenha sido criado com o modelo **MobileFirst Services Starter** e já ter um recurso protegido pelo terminal `/protected` do {{site.data.keyword.amashort}}. Para obter mais informações, consulte [Protegendo recursos](protecting-resources.html).

1. Tente enviar uma solicitação para o terminal protegido de seu aplicativo backend móvel no navegador de sua área de trabalho abrindo `{applicationRoute}/protected`, por exemplo: `http://my-mobile-backend.mybluemix.net/protected`.  Para informações sobre como obter o valor `{applicationRoute}`, veja
[Antes de iniciar](#before-you-begin).

	O terminal `/protected` de um aplicativo backend móvel criado com o Modelo MobileFirst Services está protegido com o {{site.data.keyword.amashort}}. Portanto, só é possível acessá-lo por aplicativos móveis que sejam instrumentados com o {{site.data.keyword.amashort}} client SDK. Como resultado, você verá `Unauthorized` no navegador de sua área de trabalho.

1. Use o seu aplicativo Android para fazer uma solicitação para o mesmo terminal protegido. Inclua o código a seguir depois de inicializar a instância `BMSClient` e registrar o `GoogleAuthenticationManager`.

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

1. Execute o aplicativo. Uma tela Login do Google é exibida como pop-up. Após o login, o app solicita permissão para acessar recursos:

	![image](images/android-google-login.png)

	Dependendo do seu dispositivo Android e se está atualmente conectado no Google, é possível que você tenha uma UI diferente.

	Ao clicar em **OK** você está autorizando o {{site.data.keyword.amashort}} a usar sua identidade de usuário do Google para propósitos de autenticação.

1. 	Depois que sua solicitação for bem-sucedida, será possível ver a saída a seguir na ferramenta LogCat:

	![image](images/android-google-login-success.png)

	Também é possível incluir a funcionalidade de logout incluindo o código a seguir:

	```Java
 GoogleAuthenticationManager.getInstance().logout(getApplicationContext(), listener);
	```
	{: codeblock}

	Se você chamar esse código depois que um usuário estiver conectado ao Google, ele será desconectado do Google. Quando o usuário tentar efetuar login novamente, ele deverá selecionar uma conta do Google para efetuar login novamente. Quando tentar efetuar login com um ID do Google conectado anteriormente, o usuário não será solicitado a fornecer suas credenciais novamente. Para que as credenciais de login sejam solicitadas novamente, o usuário deve remover sua conta do Google do dispositivo Android.

	O valor para `listener` passado para a função de logout pode ser `null`.
