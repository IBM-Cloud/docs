---

copyright:
  years: 2015, 2016

---

# Ativando a autenticação do Google para apps Android
{: #google-auth-android}

## Antes de Começar
{: #before-you-begin}
Você deve ter:

* Um projeto do Android no Android Studio que esteja configurado para trabalhar com Gradle. Ele não precisa ser instrumentado com o {{site.data.keyword.amashort}} client SDK.  
* Uma instância de um aplicativo {{site.data.keyword.Bluemix_notm}} que seja protegida pelo serviço {{site.data.keyword.amashort}}. Para obter mais informações sobre como criar um backend do {{site.data.keyword.Bluemix_notm}}, consulte [Introdução](index.html).

Configurar a autenticação do Google para seu app Android do {{site.data.keyword.amashort}} irá requerer configuração adicional de:
* O aplicativo {{site.data.keyword.Bluemix_notm}}
* Seu projeto do Android Studio

## Criando um projeto no Console do desenvolvedor do Google
{: #create-google-project}

Para iniciar o uso do Google como um provedor de identidade, crie um projeto no [Console do desenvolvedor do Google](https://console.developers.google.com).
Parte da criação de um projeto é obter um identificador de cliente do Google. O identificador de cliente do Google é um identificador exclusivo para seu aplicativo usado pela autenticação do Google e é necessário para configurar o aplicativo {{site.data.keyword.Bluemix_notm}}.

No console:

1. Crie um projeto usando a API do **Google+**.
2. Inclua o acesso de usuário **OAuth**.
3. Antes de incluir as credenciais, deve-se escolher a plataforma (Android).
4. Inclua as credenciais. Para concluir a criação de credenciais, é necessário incluir a **impressão digital do certificado de assinatura**.



### Configurando o certificado de assinatura
Para que o Google verifique a autenticidade de seu aplicativo, deve-se especificar uma impressão digital do certificado de assinatura.

O sistema operacional Android requer que todos os aplicativos instalados em um dispositivo Android sejam assinados com um certificado de desenvolvedor. Um aplicativo Android pode ser construído em dois modos: depuração e liberação. É aconselhável geralmente ter certificados diferentes para os modos de depuração e liberação.  Certificados usados para assinatura de aplicativos Android no modo de depuração são empacotados com o Android SDK.  Em geral, o Android SDK é instalado automaticamente pelo Android Studio. Quando desejar liberar seu aplicativo para o Google Play, deve-se assinar o app com outro certificado que, em geral, você mesmo gera. Para obter mais informações, consulte [Assinando aplicativos Android](http://developer.android.com/tools/publishing/app-signing.html).

Um keystore que contém um certificado para ambientes de desenvolvimento é armazenado em um arquivo `~/.android/debug.keystore`. A senha padrão do keystore é: `android`. Esse certificado é usado para construir aplicativos no modo de depuração.

1. Recupere a impressão digital do certificado de assinatura do ambiente de desenvolvimento do cliente:

	```XML
	keytool -exportcert -alias androiddebugkey -keystore ~/.android/debug.keystore -list -v
	```
	Também é possível usar a mesma sintaxe para recuperar o hash chave do certificado no modo de liberação. Substitua o caminho do alias e do keystore no comando.

1. No diálogo Credencial do console do Google, localize a linha iniciada com `SHA1` em **Impressões digitais do certificado**. Copie o valor da impressão digital obtida ao executar o comando **keytool** para a caixa de texto.

###Nome do Pacote

1. No diálogo Credenciais, insira o nome do pacote do aplicativo Android. 

  Para localizar o nome do pacote do aplicativo Android, abra o arquivo `AndroidManifest.xml` no Android Studio e procure: `<manifest package="{your-package-name}">`. 

1. Quando terminar, clique em **Criar**. **Isso conclui a criação de credenciais.**

###Identificador de cliente do Google

Quando as credenciais são criadas com êxito, a página de credenciais exibe o identificador de cliente do Google. Anote esse valor. Será necessário registrar esse valor no aplicativo {{site.data.keyword.Bluemix}}.


## Configurando o {{site.data.keyword.amashort}} para autenticação do Google
{: #google-auth-android-config}

Agora que você possui um identificador de cliente do Google para Android, é possível ativar a autenticação do Google no Painel do {{site.data.keyword.amashort}}.

1. Abra seu app no painel do {{site.data.keyword.Bluemix_notm}}.

1. Clique em **Opções móveis** e anote a
**Rota** (`applicationRoute`) e o **GUID do
app** (`applicationGUID`). Eles serão necessários ao inicializar o SDK.

1. Clique no ladrilho {{site.data.keyword.amashort}}. O painel do {{site.data.keyword.amashort}} é carregado.

1. Clique no ladrilho **Google**.

1. Em **ID do aplicativo para Android**, especifique o identificador de cliente do Google para Android e clique em **Salvar**.

## Configurando o {{site.data.keyword.amashort}} client SDK para Android
{: #google-auth-android-sdk}

1. Retorne para o Android Studio.

1. Abra o arquivo `build.gradle` do módulo do app.

	Seu projeto do Android pode ter dois arquivos `build.gradle`: um para o projeto e outro para o módulo do aplicativo. Use o módulo do aplicativo.

  Localize a seção de dependências e inclua uma nova dependência de compilação para o Client SDK:

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'googleauthentication',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// outras dependências  
	}
	```

	**Nota:** será possível remover a dependência do módulo `core` do grupo `com.ibm.mobilefirstplatform.clientsdk.android`, se você o tiver. O módulo `googleauthentication` faz download dele automaticamente para você. O módulo `googleauthentication` faz download e instala o Google SDK no projeto do Android.

1. Sincronize seu projeto com o Gradle clicando em **Ferramentas > Android > Sincronizar projeto com arquivos Gradle**.

1. Abra o arquivo `AndroidManifest.xml` de seu projeto do Android.

1. Inclua a permissão de acesso à Internet sob o elemento `<manifest>`:

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
	<uses-permission android:name="android.permission.GET_ACCOUNTS" />
	<uses-permission android:name="android.permission.USE_CREDENTIALS" />
	```

1. Para usar o {{site.data.keyword.amashort}} client SDK, deve-se inicializá-lo passando os parâmetros de contexto, applicationGUID e applicationRoute.

	Um local comum, mas não obrigatório, para colocar o código de inicialização é no método onCreate da atividade principal em seu aplicativo Android

1. Inicialize o client SDK e registre o gerenciador de autenticação do Google. Substitua
*applicationRoute* e *applicationGUID* pelos valores de
**Rota** e **GUID do app** da seção
**Opções móveis** no painel.

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(),
					"applicationRoute",
					"applicationGUID");

	GoogleAuthenticationManager.getInstance().register(this);
	```

1. Inclua o código a seguir em sua Atividade:

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		GoogleAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
	```

## Testando a Autenticação
{: #google-auth-android-test}
Depois que o client SDK é inicializado e o Gerenciador de autenticação do Google é registrado, é possível começar a fazer solicitações para seu aplicativo backend móvel.

### Antes de Começar
{: #google-auth-android-testing-before}
Deve-se ter um aplicativo backend móvel que tenha sido criado com o modelo MobileFirst Services Starter e já ter um recurso protegido pelo {{site.data.keyword.amashort}} no terminal `/protected`. Para obter mais informações, consulte [Protegendo recursos](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

1. Tente enviar uma solicitação para o terminal protegido de seu aplicativo backend móvel no navegador de sua área de trabalho abrindo `{applicationRoute}/protected`, por exemplo: `http://my-mobile-backend.mybluemix.net/protected`.
 O terminal `/protected` de um aplicativo backend móvel criado com o Modelo MobileFirst Services está protegido com o {{site.data.keyword.amashort}}. Portanto, só é possível acessá-lo por aplicativos móveis que sejam instrumentados com o {{site.data.keyword.amashort}} client SDK. Como resultado, você verá `Unauthorized` no navegador de sua área de trabalho.

1. Use seu aplicativo Android para fazer solicitação para o mesmo terminal. Inclua o código a seguir depois de inicializar a instância `BMSClient` e registrar o `GoogleAuthenticationManager`.

	```Java
	Request request = new Request("/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
			Log.d("MyApp", AuthorizationManager.getInstance().getUserIdentity().toString());
		}
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

1. Execute seu aplicativo. Uma tela Login do Google é exibida como pop-up. Após o login, o app solicita permissão para acessar recursos:

	![image](images/android-google-login.png)

	Dependendo de seu dispositivo Android e de você estar conectado atualmente no Google, é possível que você tenha uma interface com o usuário diferente.

  Ao clicar em **OK** você está autorizando o {{site.data.keyword.amashort}} a usar sua identidade de usuário do Google para propósitos de autenticação.

1. 	Depois que sua solicitação for bem-sucedida, será possível ver a saída a seguir na ferramenta LogCat:

	![image](images/android-google-login-success.png)

 Também é possível incluir a funcionalidade de logout incluindo o código a seguir:

 ```Java
 GoogleAuthenticationManager.getInstance().logout(getApplicationContext(), listener);
 ```

 Se você chamar esse código depois que um usuário estiver conectado ao Google, ele será desconectado do Google. Quando o usuário tentar efetuar login novamente, ele deverá selecionar uma conta do Google com a qual será conectado novamente. Quando tentar efetuar login com um ID do Google conectado anteriormente, o usuário não será solicitado a fornecer suas credenciais novamente. Para que as credenciais de login sejam solicitadas novamente, o usuário deve remover sua conta do Google do dispositivo Android.

 O valor para `listener` passado para a função de logout pode ser `null`.
