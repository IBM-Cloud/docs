---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-15"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Configurando a autenticação customizada para seu aplicativo {{site.data.keyword.amashort}} Android
{: #custom-android}


Configure seu aplicativo Android com a autenticação customizada para usar o SDK do cliente {{site.data.keyword.amashort}} e
conecte seu aplicativo ao {{site.data.keyword.Bluemix}}.

## Antes de Começar
{: #before-you-begin}
Antes de começar, deve-se ter:

* Um recurso que seja protegido por uma instância do
serviço {{site.data.keyword.amashort}} que está
configurado para usar um provedor de identidade customizado
(consulte
[Configurando autenticação customizada](custom-auth-config-mca.html)).  
* Seu valor **TenantID**. Abra o seu serviço no painel do {{site.data.keyword.amashort}}. Clique no botão **Opções móveis**. O valor
`tenantId` (também conhecido como
`appGUID`) é exibido no campo **App
GUID / TenantId**. Você precisará desse valor para
inicializar o Gerenciador de Autorização.
* Seu nome de **Domínio**. Este é o
valor que você especificou no campo **Nome do
domínio** da seção **Customizado**
no guia **Gerenciamento** do painel {{site.data.keyword.amashort}}.
* A URL do seu aplicativo backend (**Rota de App**). Você precisará desse valor para enviar
solicitações para os terminais protegido do seu aplicativo
backend.
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

Para obter informações adicionais, consulte as seguintes informações:
 * [Introdução
ao {{site.data.keyword.amashort}}](getting-started.html)
 * [Configurando o SDK do Android](getting-started-android.html)
 * [Usando um provedor de identidade customizado](custom-auth.html)
 * [Criando um provedor de identidade customizado](custom-auth-identity-provider.html)
 * [Configurando o {{site.data.keyword.amashort}} para autenticação customizada](custom-auth-config-mca.html)



## Inicializando o {{site.data.keyword.amashort}} client SDK
{: #custom-android-initialize}
Se você tiver um app Android instrumentado com o
{{site.data.keyword.amashort}} Android SDK, será possível
ignorar esta seção.
1. Em seu projeto Android no Android Studio, abra o arquivo `build.gradle` do seu módulo de aplicativo (não o projeto `build.gradle`).

1. No arquivo `build.gradle`, localize a seção `dependencies` e verifique se a dependência a
seguir existe:

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
        name:'core',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// other dependencies  
	}
	```
	{: codeblock}

1. Sincronizar seu projeto com o Gradle. Clique em **Ferramentas > Android > Sincronizar projeto com arquivos Gradle**.

1. Abra o arquivo `AndroidManifest.xml` de seu projeto Android.
Inclua a permissão de acesso à Internet no elemento `<manifest>`:

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
	```
	{: codeblock}

1. Inicialize o SDK.  
	Um local comum, mas não obrigatório, para colocar o código de inicialização é o método `onCreate` da atividade principal em seu aplicativo Android.

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_UK);
	```
	{: codeblock}

Substitua o `BMSClient.REGION_UK` pela
região {{site.data.keyword.amashort}}. Para mais informações sobre como obter esses
valores, consulte [Antes de
iniciar](#before-you-begin).


## Interface AuthenticationListener
{: #custom-android-authlistener}

O {{site.data.keyword.amashort}} client SDK fornece a interface `AuthenticationListener` para que seja possível implementar um fluxo de autenticação customizada. A interface `AuthenticationListener` expõe três métodos que são chamados em diferentes fases durante o processo de autenticação.

### Método onAuthenticationChallengeReceived
{: #custom-onAuth}
Chame esse método quando um desafio de autenticação customizada for recebido do serviço {{site.data.keyword.amashort}}.

```Java
void onAuthenticationChallengeReceived(AuthenticationContext authContext, JSONObject challenge, Context context);
```
{: codeblock}


#### Argumentos
{: #custom-android-onAuth-arg}

* `AuthenticationContext`: fornecido pelo {{site.data.keyword.amashort}} client SDK para que seja possível relatar as respostas ou falhas dos desafios de autenticação durante a coleta de credenciais.  Por exemplo, quando um usuário cancela a autenticação.
* `JSONObject`: contém um desafio de autenticação customizada, conforme retornado por um provedor de identidade customizado.
* `Context`: uma referência ao Contexto Android que foi usado quando a solicitação foi enviada. Geralmente esse argumento representa uma Atividade Android.

Ao chamar o método `onAuthenticationChallengeReceived`, o {{site.data.keyword.amashort}} client SDK está delegando controle ao desenvolvedor.  O serviço aguarda as credenciais. O desenvolvedor deve coletar credenciais e as relatar de volta ao {{site.data.keyword.amashort}} client SDK usando um dos métodos de interface `AuthenticationContext`.

### Método onAuthenticationSuccess
{: #custom-android-authlistener-onsuccess}
Chame esse método após uma autenticação bem-sucedida. Os argumentos incluem o Contexto Android e um JSONObject opcional que contenha informações estendidas sobre o sucesso da autenticação.
```Java
void onAuthenticationSuccess(Context context, JSONObject info);
```
{: codeblock}

### Método onAuthenticationFailure
{: #custom-android-authlistener-onfail}
Chame esse método após falhas de autenticação. Os argumentos incluem o Contexto Android e um `JSONObject` opcional
que contém informações estendidas sobre a falha de autenticação.
```Java
void onAuthenticationFailure(Context context, JSONObject info);
```
{: codeblock}

## Interface AuthenticationContext
{: #custom-android-authcontext}

O `AuthenticationContext` é fornecido como um argumento para o método `onAuthenticationChallengeReceived` de um `AuthenticationListener` customizado. Deve-se coletar credenciais e usar os métodos `AuthenticationContext` para retornar credenciais para o {{site.data.keyword.amashort}} client SDK ou relatar uma falha. Use um dos métodos a
seguir.

```Java
void submitAuthenticationChallengeAnswer(JSONObject answer);
```
{: codeblock}

```Java
void submitAuthenticationFailure (JSONObject info);
```
{: codeblock}

## Implementação de amostra de um AuthenticationListener customizado
{: #custom-android-samplecustom}

Essa amostra de AuthenticationListener foi projetada para funcionar com um provedor de identidade customizado. É possível fazer download dessa amostra no [Repositório Github ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample "Ícone de link externo"){: new_window}.

```Java
package com.ibm.helloworld;
import android.content.Context;
import android.util.Log;
import com.ibm.mobilefirstplatform.clientsdk.android.security.mca.api.AuthenticationContext;
import com.ibm.mobilefirstplatform.clientsdk.android.security.mca.api.AuthenticationListener;
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
		// Access client SDK will remain in a waiting-for-credentials state
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
{: codeblock}

## Registrando um AuthenticationListener customizado
{: #custom-android-register}

Depois de criar um AuthenticationListener customizado, registre-o com `BMSClient` antes de começar a usar o listener. Inclua o código a seguir em seu aplicativo. Esse código deve ser chamado antes de enviar quaisquer solicitações aos seus recursos protegidos.

```Java
MCAAuthorizationManager mcaAuthorizationManager = 
      MCAAuthorizationManager.createInstance(this.getApplicationContext(),"<MCAServiceTenantId>");
mcaAuthorizationManager.registerAuthenticationListener(realmName, new CustomAuthenticationListener());
BMSClient.getInstance().setAuthorizationManager(mcaAuthorizationManager);

```
{: codeblock}


No código:
* Substitua `MCAServiceTenantId` pelo
valor **TenantId** (consulte
[Antes de iniciar](##before-you-begin)).
* Use o `realmName` que você especificou
no painel {{site.data.keyword.amashort}} (consulte
[Configurando a autenticação customizada](custom-auth-config-mca.html)).


## Testando a Autenticação
{: #custom-android-testing}
Depois que o cliente SDK é inicializado e um AuthenticationListener customizado é registrado, é possível começar a fazer solicitações para seu aplicativo backend móvel.

### Antes de testar
{: #custom-android-testing-before}
Deve-se ter um aplicativo que possui um recurso que seja
protegido pelo {{site.data.keyword.amashort}} no terminal
`/protected`.


1. Envie uma solicitação ao terminal protegido (`{applicationRoute}/protected`) do seu aplicativo backend móvel a partir do
navegador, por exemplo, `http://my-mobile-backend.mybluemix.net/protected`. Para informações sobre como obter o valor `{applicationRoute}`, veja
[Antes de iniciar](#before-you-begin).

1. O terminal `/protected` de um aplicativo backend móvel criado com o modelo {{site.data.keyword.mobilefirstbp}} está protegido com o {{site.data.keyword.amashort}}. O terminal pode ser acessado somente por aplicativos móveis que sejam instrumentados com o {{site.data.keyword.amashort}} client SDK. Como resultado, uma mensagem `Unauthorized` é exibida em seu navegador.

1. Use o seu aplicativo Android para fazer uma solicitação para o mesmo terminal protegido que inclui o `{applicationRoute}`. Inclua o código a seguir depois de inicializar `BMSClient` e registrar seu AuthenticationListener customizado.

	```Java
	Request request = new Request("{applicationRoute}/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
			Log.d("MyApp",  MCAAuthorizationManager.getInstance().getUserIdentity().toString());
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
	{: codeblock}

1. 	Quando sua solicitação for bem-sucedida, a saída a seguir estará na ferramenta LogCat:

	![image](images/android-custom-login-success.png)

 Também é possível incluir a funcionalidade de logout incluindo o código a seguir:

 ```Java
 MCAAuthorizationManager.getInstance().logout(getApplicationContext(), listener);
 ```
 {: codeblock}


 Se você chamar esse código depois que um usuário estiver conectado, ele será desconectado. Quando o usuário tentar efetuar login novamente, ele deverá responder ao desafio recebido do servidor novamente.

 O valor para `listener` passado para a função de logout pode ser `null`.
