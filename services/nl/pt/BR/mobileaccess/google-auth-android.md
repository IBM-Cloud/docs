---

copyright:
  years: 2015, 2016

---

# Ativando a autenticação do Google em apps Android
{: #google-auth-android}

## Antes de Começar
{: #before-you-begin}

* Deve-se ter um recurso que seja protegido pelo {{site.data.keyword.amashort}} e um projeto do Android que seja instrumentado com o {{site.data.keyword.amashort}} Client SDK.  Para obter mais informações, consulte [Introdução ao {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) e [Configurando o Android SDK](https://console.{DomainName}/docs/services/mobileaccess/getting-started-android.html).  
* Proteja manualmente seu aplicativo backend com o {{site.data.keyword.amashort}} Server SDK. Para obter mais informações, consulte [Protegendo recursos](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

## Configurando um projeto do Google para a plataforma Android
{: #google-auth-android-project}
Para iniciar o uso do Google como um provedor de identidade, crie um projeto no Console do desenvolvedor do Google. Parte da criação de um projeto é obter um identificador de cliente do Google. O identificador de cliente do Google é um identificador exclusivo para seu aplicativo usado pela autenticação do Google.

1. Crie um projeto no [Console do desenvolvedor do Google](https://console.developers.google.com).
Se você já tiver um projeto, poderá ignorar as etapas que descrevem a criação do projeto e iniciar com a inclusão de credenciais.
   1.    Abra o menu do novo projeto. 
         
         ![image](images/FindProject.jpg)

   2.    Clique em **Criar um projeto**.
   
         ![image](images/CreateAProject.jpg)


   1. Na lista **APIs sociais**, escolha **API do Google+**.

     ![image](images/chooseGooglePlus.jpg)

   1. Clique em **Ativar** na próxima tela.

1. Selecione a guia **Tela de consentimento** e forneça o nome do produto mostrado aos usuários. Outros valores são opcionais. Clique em **Salvar**.

    ![image](images/consentScreen.png)
    
1. Na lista **Credenciais**, escolha o identificador de cliente OAuth.

     ![image](images/chooseCredentials.png)
     


1. Selecione um tipo de aplicativo. Clique em **Android**. Forneça um nome significativo para seu cliente Android.

1. Para que o Google verifique a autenticidade de seu aplicativo, deve-se especificar uma impressão digital do certificado de assinatura.

	 **Mais sobre a segurança do Android:** o sistema operacional Android requer que todos os aplicativos instalados em um dispositivo Android sejam assinados com um certificado de desenvolvedor. Um aplicativo Android pode ser construído em dois modos: depuração e liberação. É aconselhável geralmente ter certificados diferentes para os modos de depuração e liberação.  Certificados usados para assinatura de aplicativos Android no modo de depuração são empacotados com o Android SDK.  Em geral, o Android SDK é instalado automaticamente pelo Android Studio. Quando desejar liberar seu aplicativo para o Google Play, deve-se assinar o app com outro certificado que, em geral, você mesmo gera. Para obter mais informações, consulte [Assinando aplicativos Android](http://developer.android.com/tools/publishing/app-signing.html).

1. Um keystore que contém um certificado para ambientes de desenvolvimento é armazenado em um arquivo `~/.android/debug.keystore`. A senha padrão do keystore é: `android`. Esse certificado é usado para construir aplicativos no modo de depuração.

     1. Recupere a impressão digital do certificado de assinatura:

	```XML
	keytool -exportcert -alias androiddebugkey -keystore ~/.android/debug.keystore -list -v
	```
	Também é possível usar a mesma sintaxe para recuperar o hash chave do certificado no modo de liberação. Substitua o caminho do alias e do keystore no comando.

1. Localize a linha que começa com `SHA1` em **Impressões digitais do certificado**. Copie a impressão digital obtida ao executar o comando **keytool** para o Console do desenvolvedor do Google.

1. Especifique o nome do pacote do aplicativo Android. Para localizar o nome do pacote do aplicativo Android, abra o arquivo `AndroidManifest.xml` no Android Studio e procure: `<manifest package="{your-package-name}">`. Quando terminar, clique em **Criar**.

Aparece um diálogo exibindo o identificador de cliente do Google. Anote esse valor. É necessário registrar esse valor no {{site.data.keyword.Bluemix}}.


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

## Configurando o {{site.data.keyword.amashort}} Client SDK para Android
{: #google-auth-android-sdk}

1. Retorne para o Android Studio.

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
    	// outras dependências  
	}
	```

	É possível remover a dependência no módulo `core` do grupo `com.ibm.mobilefirstplatform.clientsdk.android`, se você o tiver. O módulo `googleauthentication` faz download dele automaticamente para você. O módulo `googleauthentication` faz download e instala o Google SDK no projeto Android.

1. Sincronize seu projeto com o Gradle clicando em **Ferramentas > Android > Sincronizar projeto com arquivos Gradle**.

1. Abra o arquivo `AndroidManifest.xml` de seu projeto do Android.

1. Inclua a permissão de acesso à Internet sob o elemento `<manifest>`:

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
	<uses-permission android:name="android.permission.GET_ACCOUNTS" />
	<uses-permission android:name="android.permission.USE_CREDENTIALS" />
	```

1. Para usar o {{site.data.keyword.amashort}} Client SDK, deve-se inicializá-lo passando os parâmetros context, applicationGUID e applicationRoute.

	Um local comum, mas não obrigatório, para colocar o código de inicialização é no método onCreate da atividade principal em seu aplicativo Android

1. Inicialize o Client SDK e registre o gerenciador de autenticação do Google. Substitua
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
Após a inicialização do Client SDK e do registro do Gerenciador de autenticação do Google, é possível começar a fazer solicitações para seu backend móvel.

### Antes de Começar
{: #google-auth-android-testing-before}
Deve-se ter um backend móvel criado com o modelo do MobileFirst Services Starter e já ter um recurso protegido pelo {{site.data.keyword.amashort}} no terminal `/protected`. Para obter mais informações, consulte [Protegendo recursos](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

1. Tente enviar uma solicitação para o terminal protegido do backend móvel no
navegador do desktop abrindo `{applicationRoute}/protected`; por exemplo:
`http://my-mobile-backend.mybluemix.net/protected`.
 O terminal `/protected` de um backend móvel criado com o Modelo do MobileFirst Services é protegido com o {{site.data.keyword.amashort}}. Portanto, só é possível acessá-lo por aplicativos móveis que sejam instrumentados com o {{site.data.keyword.amashort}} Client SDK. Como resultado, você verá `Unauthorized` no navegador de sua área de trabalho.

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

1. Execute o aplicativo. Uma tela Login do Google é exibida como pop-up. Após o login, o app solicita permissão para acessar recursos:

	![image](images/android-google-login.png)

	Dependendo de seu dispositivo Android e de você estar conectado atualmente no Google, é possível que você tenha uma interface com o usuário diferente.

  Ao clicar em **OK** você está autorizando o {{site.data.keyword.amashort}} a usar sua identidade de usuário do Google para propósitos de autenticação.

1. 	Depois que sua solicitação for bem-sucedida, será possível ver a saída a seguir na ferramenta LogCat:

	![image](images/android-google-login-success.png)

1. Também é possível incluir a funcionalidade de logout incluindo o código a seguir:

 ```Java
 GoogleAuthenticationManager.getInstance().logout(getApplicationContext(),, listener);
 ```

 Se você chamar esse código depois que um usuário estiver conectado ao Google, ele será desconectado do Google. Quando o usuário tentar efetuar login novamente, ele deverá selecionar uma conta do Google com a qual será conectado novamente. Quando tentar efetuar login com um ID do Google conectado anteriormente, o usuário não será solicitado a fornecer suas credenciais novamente. Para que as credenciais de login sejam solicitadas novamente, o usuário deve remover sua conta do Google do dispositivo Android.

 O valor para `listener` passado para a função de logout pode ser nulo.
