---

copyright:
  years: 2015, 2016

---

# Configurando o {{site.data.keyword.amashort}} Client SDK para Android
{: #custom-android}
Configure seu aplicativo Android que está usando autenticação customizada para usar o {{site.data.keyword.amashort}} Client SDK e conecte seu aplicativo ao {{site.data.keyword.Bluemix}}.

## Antes de Começar
{: #before-you-begin}
Deve-se ter um recurso que seja protegido por uma instância do serviço {{site.data.keyword.amashort}} que está configurado para usar um provedor de identidade customizado.  Seu
app móvel também deve ser instrumentado com o {{site.data.keyword.amashort}} Client SDK.  Para obter informações adicionais, consulte as seguintes informações:
 * [Introdução
ao {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [Configurando o SDK do Android](https://console.{DomainName}/docs/services/mobileaccess/getting-started-android.html)
 * [Usando um provedor de identidade customizado](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [Criando um provedor de identidade customizado](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [Configurando o {{site.data.keyword.amashort}} para autenticação customizada](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)


## Inicializando o {{site.data.keyword.amashort}} Client SDK
{: #custom-android-initialize}
1. Em seu projeto Android em Android Studio, abra o arquivo `build.gradle` de seu módulo do app.
<br/>**Dica:** o projeto Android pode ter dois arquivos `build.gradle`: para o projeto e para o módulo do aplicativo. Use o arquivo do módulo do aplicativo.

1. No arquivo `build.gradle`, localize a seção `dependencies` e verifique a dependência de compilação a seguir. Inclua essa dependência se ela ainda não estiver lá.

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'core',
        version: '1.+',
        ext: 'aar',
        transitive: true
    	// other dependencies  
	}
	```

1. Sincronizar seu projeto com o Gradle. Clique em **Ferramentas > Android > Sincronizar projeto com arquivos Gradle**.

1. Abra o arquivo `AndroidManifest.xml` de seu projeto Android.
Inclua a permissão de acesso à Internet no elemento `<manifest>`:

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
	```

1. Inicialize o SDK.  
Um local comum, mas não obrigatório, para colocar o código de inicialização é o método `onCreate` da atividade principal em seu aplicativo Android.
Substitua *applicationRoute* e *applicationGUID* pelos valores
**Route** e **App GUID** que você obtém quando
clica em **Opções móveis** em seu app no painel
{{site.data.keyword.Bluemix_notm}}.

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(),
					"applicationRoute",
					"applicationGUID");					
	```

## Interface AuthenticationListener
{: #custom-android-authlistener}

O {{site.data.keyword.amashort}} Client SDK fornece a interface `AuthenticationListener` para que seja possível
implementar um fluxo de autenticação customizada. A interface `AuthenticationListener` expõe três métodos que são chamados em fases diferentes do processo de autenticação.

### Método onAuthenticationChallengeReceived
{: #custom-onAuth}
Chame esse método quando um desafio de autenticação customizada for recebido do serviço {{site.data.keyword.amashort}}.

```Java
void onAuthenticationChallengeReceived(AuthenticationContext authContext, JSONObject challenge, Context context);
```
#### Argumentos
{: #custom-android-onAuth-arg}

* `AuthenticationContext`: Fornecido pelo {{site.data.keyword.amashort}} Client SDK para que seja possível relatar as respostas ou falhas dos desafios de autenticação durante a coleta de credenciais.  Por exemplo, quando um usuário cancela a autenticação.
* `JSONObject`: contém um desafio de autenticação customizada, conforme retornado por um provedor de identidade customizado.
* `Context`: uma referência ao Contexto Android que foi usado quando a solicitação foi enviada. Geralmente esse argumento representa uma Atividade Android.

Ao chamar o método `onAuthenticationChallengeReceived`, o {{site.data.keyword.amashort}} Client SDK está delegando controle ao desenvolvedor.  O serviço aguarda as credenciais. O
desenvolvedor deve coletar credenciais e as relatar de volta ao {{site.data.keyword.amashort}} Client SDK usando um dos métodos de interface `AuthenticationContext`.

### Método onAuthenticationSuccess
{: #custom-android-authlistener-onsuccess}
Chame esse método após uma autenticação bem-sucedida. Os argumentos incluem o Contexto Android e um JSONObject opcional que contenha informações estendidas sobre o sucesso da autenticação.
```Java
void onAuthenticationSuccess(Context context, JSONObject info);
```

### Método onAuthenticationFailure
{: #custom-android-authlistener-onfail}
Chame esse método após falhas de autenticação. Os argumentos incluem o Contexto Android e um JSONObject opcional que contém informações estendidas sobre falha de autenticação.
```Java
void onAuthenticationFailure(Context context, JSONObject info);
```

## Interface AuthenticationContext
{: #custom-android-authcontext}

O `AuthenticationContext` é fornecido como um argumento para o método `onAuthenticationChallengeReceived` de um `AuthenticationListener` customizado. Deve-se
coletar credenciais e usar os métodos `AuthenticationContext` para retornar credenciais para o {{site.data.keyword.amashort}} Client SDK ou relatar uma falha. Use um dos métodos a
seguir.

```Java
void submitAuthenticationChallengeAnswer(JSONObject answer);
```
```Java
void submitAuthenticationFailure (JSONObject info);
```

## Implementação de amostra de um AuthenticationListener customizado
{: #custom-android-samplecustom}

Essa amostra de AuthenticationListener foi projetada para funcionar com um provedor de identidade customizado. É possível fazer o download dessa amostra a partir do [repositório Github](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample).

```Java
package com.ibm.helloworld;
import android.content.Context;
import android.util.Log;
import com.ibm.mobilefirstplatform.clientsdk.android.security.api.AuthenticationContext;
import com.ibm.mobilefirstplatform.clientsdk.android.security.api.AuthenticationListener;
import org.json.JSONException;
import org.json.JSONObject;

public class CustomAuthenticationListener implements AuthenticationListener {
	@Override
	public void onAuthenticationChallengeReceived (AuthenticationContext authContext,
											JSONObject challenge, Context context) {

		log("onAuthenticationChallengeResceived :: " + challenge.toString());

		// In this sample the AuthenticationListener immediatelly returns a hardcoded
		// set of credentials. In a real life scenario this is where developer would
		// show a login screen, collect credentials and invoke
		// authContext.submitAuthenticationChallengeAnswer() API

		JSONObject challengeResponse = new JSONObject();
		try {
			challengeResponse.put("username", "john.lennon");
			challengeResponse.put("password", "12345");
			authContext.submitAuthenticationChallengeAnswer(challengeResponse);
		} catch (JSONException e){

			// In case there was a failure collecting credentials you need to report
			// it back to the AuthenticationContext. Otherwise Mobile Client
			// Access Client SDK will remain in a waiting-for-credentials state
			// forever

			log("This should never happen...");
			authContext.submitAuthenticationFailure(null);
		}
	}

	@Override
	public void onAuthenticationSuccess (Context context, JSONObject info) {
		log("onAuthenticationSuccess :: " + info.toString());
	}

	@Override
	public void onAuthenticationFailure (Context context, JSONObject info) {
		log("onAuthenticationFailure :: " + info.toString());
	}

	private void log(String text){
		Log.d("CustomAuthListener", text);
	}
}
```

## Registrando um AuthenticationListener customizado
{: #custom-android-register}

Depois de criar um AuthenticationListener customizado, registre-o com `BMSClient` antes de começar a usar o listener. Inclua o código a seguir em seu aplicativo. Esse código deve ser chamado antes de enviar quaisquer solicitações aos seus recursos protegidos.

```Java
BMSClient.getInstance().registerAuthenticationListener(realmName,
									new CustomAuthenticationListener());
```

Use o *realmName* especificado no painel do {{site.data.keyword.amashort}}.


## Testando a Autenticação
{: #custom-android-testing}
Depois que o Client SDK for inicializado e um AuthenticationListener customizado for registrado, será possível começar a fazer solicitações ao seu backend móvel.

### Antes de Começar
{: #custom-android-testing-before}
Deve-se ter um aplicativo que foi criado com o modelo do {{site.data.keyword.mobilefirstbp}} e ter um recurso que esteja protegido por {{site.data.keyword.amashort}} no terminal `/protected`.


1. Envie uma solicitação ao terminal protegido do backend móvel em seu navegador
abrindo `{applicationRoute}/protected`, por exemplo,
`http://my-mobile-backend.mybluemix.net/protected`.

1. O terminal `/protected` de um backend móvel que é criado com o modelo do {{site.data.keyword.mobilefirstbp}} está protegido com {{site.data.keyword.amashort}}. O
terminal pode ser acessado somente por aplicativos móveis que sejam instrumentados com o {{site.data.keyword.amashort}} Client SDK. Como resultado, uma mensagem `Unauthorized` é exibida em seu navegador.

1. Use seu aplicativo Android para fazer solicitação ao mesmo terminal. Inclua o código a seguir depois de inicializar `BMSClient` e registrar seu AuthenticationListener customizado.

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

1. 	Quando sua solicitação for bem-sucedida, a saída a seguir estará na ferramenta LogCat:

	![image](images/android-custom-login-success.png)

1. Também é possível incluir a funcionalidade de logout incluindo o código a seguir:

 ```Java
 AuthorizationManager.getInstance().logout(getApplicationContext(), listener);
 ```

 Se você chamar esse código depois que um usuário estiver conectado, ele será desconectado. Quando o usuário tentar efetuar login novamente, ele deverá responder ao desafio recebido do servidor novamente.

 O valor para `listener` passado para a função de logout pode ser nulo.
