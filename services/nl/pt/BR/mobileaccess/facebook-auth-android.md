---

copyright:
  years: 2015, 2016

---

# Ativando a autenticação do Facebook em apps Android
{: #facebook-auth-android}
Para usar o Facebook como provedor de identidade nos aplicativos Android, inclua e configure a plataforma Android do aplicativo Facebook.

## Antes de Começar
{: #facebook-auth-android-before}
 * Deve-se ter um recurso que seja protegido pelo {{site.data.keyword.amashort}} e um projeto do Android que seja instrumentado com o {{site.data.keyword.amashort}} Client SDK.  Para obter mais informações, consulte [Introdução ao {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html) e [Configurando o Android SDK](https://console.{DomainName}/docs/services/mobileaccess/getting-started-android.html).  
 * Proteja manualmente seu aplicativo backend com o {{site.data.keyword.amashort}} Server SDK. Para obter mais informações, consulte [Protegendo recursos](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).
 * Crie um ID do aplicativo Facebook. Para obter mais informações, consulte [Obtendo um ID do aplicativo Facebook do Portal do Desenvolvedor do Facebook](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID).


## Configurando um aplicativo Facebook para a plataforma Android
{: #facebook-auth-android-config}
Para usar o Facebook como provedor de identidade nos aplicativos Android, deve-se incluir e configurar a plataforma Android para o aplicativo Facebook.

1. Abra o aplicativo Facebook no Portal do Desenvolvedor do Facebook.

1. Clique em **Configurações &gt; Incluir plataforma &gt; Android**.

1. Especifique o nome do pacote do aplicativo Android no prompt Nome do pacote do Google Play. Para localizar o nome do pacote do aplicativo Android, abra os arquivos `AndroidManifest.xml` no Android Studio e procure `<manifest ..... package="{your-package-name}">`.

1. Especifique o nome de classe de sua atividade principal no prompt **Nome de classe**. Para localizar o nome de classe da atividade principal do aplicativo Android, abra o arquivo `AndroidManifest.xml` e procure a declaração de atividade com filtro de intento semelhante ao fragmento de código a seguir:

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

1. Para que o Facebook assegure a autenticidade de seu aplicativo, deve-se especificar um hash de seu certificado de desenvolvedor SHA1.

	**Mais sobre a segurança do Android:** o sistema operacional Android requer que todos os aplicativos instalados em um dispositivo Android sejam assinados com um certificado de desenvolvedor. O aplicativo Android pode ser construído em dois modos: depuração e liberação. <br/>
  Use certificados diferentes para os modos de depuração e liberação.  Certificados usados para assinatura de aplicativos Android no modo de depuração são empacotados com o Android SDK que, em geral, é instalado automaticamente pelo Android Studio. Quando desejar liberar seu app no armazenamento do Google Play, você deverá assinar seu app com outro certificado que, em geral, você mesmo gera. <br/>É possível inserir dois conjuntos de hashes chaves com o facebook: um hash chave para aplicativos construídos no modo de depuração com um certificado de depuração e outro hash chave para aplicativos construídos no modo de liberação com um certificado de liberação. Para obter mais informações, consulte [Assinando aplicativos Android](http://developer.android.com/tools/publishing/app-signing.html).

1. O keystore que contém o certificado que você está usando para o ambiente de desenvolvimento é armazenado no arquivo `~/.android/debug.keystore`. A senha do keystore padrão é: `android`. Use esse certificado para construir aplicativos no modo de depuração.

1. Recupere o hash chave do certificado no modo de depuração:

	```XML
	keytool -exportcert -alias androiddebugkey -keystore ~/.android/debug.keystore | openssl sha1 -binary | openssl base64
	```

	**Dica**: é possível usar a mesma sintaxe para recuperar o hash chave do certificado no modo de liberação. Substitua o caminho do alias e do keystore no comando.

1. Copie e cole o hash chave obtido com o comando **keytool** em um prompt de Hashes chaves de Desenvolvimento/Liberação no Portal do Desenvolvedor do Facebook.

	**Dica**: considere a ativação da conexão única se você estiver planejando usar esse recurso.

1. Clique em **Salvar Configurações**.

## Configurando o {{site.data.keyword.amashort}} para autenticação do Facebook
{: #facebook-auth-android-mca}
Depois que você tiver o ID do aplicativo Facebook e tiver configurado o aplicativo Facebook para atender clientes Android, será possível ativar a autenticação do Facebook no painel do {{site.data.keyword.amashort}}.

1. Abra seu app no painel do {{site.data.keyword.Bluemix_notm}}.

1. Clique em **Opções móveis** e anote a
**Rota** (`applicationRoute`) e o **GUID do
app** (`applicationGUID`). Eles serão necessários ao inicializar o SDK.

1. Clique no ladrilho {{site.data.keyword.amashort}}. O painel do {{site.data.keyword.amashort}} é carregado.

1. Clique no ladrilho **Facebook**.

1. Especifique o ID do aplicativo Facebook e clique em **Salvar**.

## Configurando o {{site.data.keyword.amashort}} Client SDK para Android
{: #facebook-auth-android-sdk}
Para configurar o cliente SDK para Android, use o gerenciador de dependência Gradle no Android Studio.

1.  Abra o arquivo `build.gradle` do módulo do app.
Seu projeto Android pode ter dois arquivos `build.gradle`: para o projeto e para o módulo do aplicativo. Use o arquivo do módulo do aplicativo.

1. Localize a seção de dependências do arquivo `build.gradle` e inclua uma nova dependência de compilação para o Client SDK:

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'facebookauthentication',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// outras dependências  
	}
```

	É possível remover a dependência no módulo `core` do grupo `com.ibm.mobilefirstplatform.clientsdk.android`, se estiver em seu arquivo. O módulo `facebookauthentication` faz download do módulo `core` automaticamente.

  Após o salvamento de suas atualizações, o módulo `facebookauthentication` faz download e instala o Facebook SDK no projeto do Android.


1. Sincronize seu projeto com o Gradle. Clique em **Ferramentas > Android > Sincronizar projeto com arquivos do Gradle**.

1. Abra o arquivo `res/values/strings.xml` e inclua uma sequência `facebook_app_id` que contenha seu ID do aplicativo Facebook:

	```XML
	<resources>
		<string name="app_name">HelloWorld</string>
		<string name="action_settings">Settings</string>
		<string name="facebook_app_id">522733366802111</string>
	</resources>
```

1. No arquivo `AndroidManifest.xml` do projeto do Android:
   1. Inclua a permissão de acesso à Internet sob o elemento `<manifest>`:

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
```
  2. Inclua metadados necessários para o Facebook SDK no elemento `<application>`:

	```XML
	<application .......>

		<meta-data android:name="com.facebook.sdk.ApplicationId" android:value="@string/facebook_app_id"/>

		<activity ...../>
		<activity ...../>
	</application>
```

   1. Inclua um elemento de Atividade do Facebook sob as atividades existentes:

	```XML
	<application .....>
		<activity ...../>
		<activity ...../>

		<activity 	android:name="com.facebook.FacebookActivity"
					android:configChanges=
						"keyboard|keyboardHidden|screenLayout|screenSize|orientation"
					android:theme="@android:style/Theme.Translucent.NoTitleBar"
					android:label="@string/app_name" />

	</application>
```

1. Inicialize o Client SDK e registre o gerenciador de autenticação do Facebook. Inicialize
o {{site.data.keyword.amashort}} Client SDK passando os parâmetros de contexto,
GUID do app (`applicationGUID`) e rota
(`applicationRoute`).<br/>
 Um local comum, embora não obrigatório, para colocar o código de inicialização está no
método `onCreate` da atividade principal em seu aplicativo Android.<br/>
 Substitua *applicationRoute* e *applicationGUID* pelos valores
de **Rota** e **GUID do app** no menu
**Opções móveis** da página principal de seu app no painel Bluemix.

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(),
					"applicationRoute",
					"applicationGUID");

	FacebookAuthenticationManager.getInstance().register(this);
```


1. Inclua o código a seguir em sua Atividade:

	```Java
	@Override
	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		FacebookAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
```

## Testando a Autenticação
Após a inicialização do Client SDK e do registro do Gerenciador de autenticação do Facebook, é possível começar a fazer solicitações para seu backend móvel.

### Antes de Começar
{: #facebook-auth-android-testing-before}
Deve-se estar usando o modelo do {{site.data.keyword.mobilefirstbp}} e já ter um recurso protegido pelo {{site.data.keyword.amashort}} no terminal `/protected`. Se for necessário configurar um terminal `/protected`, consulte [Protegendo recursos](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

1. Tente enviar uma solicitação para o terminal protegido de seu backend móvel recém-criado em seu navegador. Abra
a URL a seguir: `{applicationRoute}/protected`. Por exemplo: `http://my-mobile-backend.mybluemix.net/protected`
<br/>O terminal `/protected` de um backend móvel criado com o Modelo do MobileFirst Services Starter é protegido com o {{site.data.keyword.amashort}}. Uma mensagem `Unauthorized` é retornada no navegador. Essa mensagem é retornada porque esse terminal só pode ser acessado por aplicativos móveis instrumentados com o {{site.data.keyword.amashort}} Client SDK.

1. Use seu aplicativo Android para fazer solicitação para o mesmo terminal. Inclua
o código a seguir depois de inicializar `BMSClient` e registrar
`FacebookAuthenticationManager`.

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

1. Execute o aplicativo. Uma tela de login do Facebook é exibida.

	![image](images/android-facebook-login.png)

	Essa tela poderá parecer um pouco diferente se o app Facebook não estiver instalado em seu dispositivo, ou se você não estiver atualmente conectado ao Facebook.

1. Clique em **OK** para autorizar o {{site.data.keyword.amashort}} a usar sua identidade de usuário do Facebook para propósitos de autenticação.

1. 	Quando sua solicitação for bem-sucedida, a saída a seguir estará no utilitário LogCat:

	![image](images/android-facebook-login-success.png)

1. Também é possível incluir a funcionalidade de logout incluindo o código a seguir:

 ```
FacebookAuthenticationManager.getInstance().logout(getApplicationContext(), listener);
 ```

 Se você chamar esse código depois que um usuário estiver conectado ao Facebook, ele será desconectado. Quando o usuário tentar efetuar login novamente, ele será solicitado a fornecer as credenciais do Facebook.

 O valor para `listener` passado para a função de logout pode ser nulo.
