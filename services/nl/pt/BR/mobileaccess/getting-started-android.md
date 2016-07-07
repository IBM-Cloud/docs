---

copyright:
  years: 2015, 2016
  
---
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configurando o SDK do Android
{: #getting-started-android}

*Última atualização: 25 de maio de 2016*
{: .last-updated}

Instrumente seu aplicativo Android com o {{site.data.keyword.amashort}} client SDK, inicialize o SDK e faça as solicitações para recursos protegidos e desprotegidos.
{:shortdesc}

## Antes de Começar
{: #before-you-begin}
Você deve ter:
* Uma instância de um aplicativo {{site.data.keyword.Bluemix_notm}} que seja protegida pelo serviço {{site.data.keyword.amashort}}. Para obter mais informações sobre como criar um backend do {{site.data.keyword.Bluemix_notm}}, consulte [Introdução](index.html).
* Um projeto do Android Studio, incluindo o Gradle e o Android Studio SDK. Para obter mais informações sobre como configurar seu ambiente de desenvolvimento do Android, veja [Google Developer Tools](http://developer.android.com/sdk/index.html).


## Instalando o {{site.data.keyword.amashort}} client SDK
{: #install-mca-sdk}

O {{site.data.keyword.amashort}} client SDK é distribuído com o Gradle, um gerenciador de dependência para projetos Android. O Gradle faz download automaticamente dos artefatos de repositórios e os disponibiliza em seu aplicativo Android.

1. Crie um projeto Android Studio ou abra um projeto existente.

1. Abra o arquivo `build.gradle`.
**Dica**: o seu projeto Android pode ter dois arquivos `build.gradle`: para o projeto e o módulo do aplicativo. Use o arquivo do módulo do aplicativo.

1. Localize a seção **Dependências** do arquivo `build.gradle`.  Inclua uma dependência de compilação para o {{site.data.keyword.amashort}} client SDK:

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

1. Sincronize seu projeto com o Gradle. Clique em **Ferramentas &gt; Android &gt; Sincronizar projeto com arquivos Gradle**.

1. Abra o arquivo `AndroidManifest.xml` de seu projeto do Android. Inclua a permissão de acesso à Internet sob o elemento `<manifest>`:

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
```

## Inicializando o {{site.data.keyword.amashort}} client SDK
{: #initalize-mca-sdk}

Inicialize o SDK passando os parâmetros `context`, `applicationGUID` e `applicationRoute` para o método `initialize`.


1. Na página principal do painel do {{site.data.keyword.Bluemix_notm}}, clique em seu app. Clique em **Opções de dispositivo móvel**. Os valores **Rota do aplicativo** e **GUID do aplicativo** são necessários para inicializar o SDK.

2. Inicialize o {{site.data.keyword.amashort}} client SDK em seu aplicativo Android.  Um local comum, mas não obrigatório, para colocar o código de inicialização é o método `onCreate` da atividade principal em seu aplicativo Android.
<br/>Substitua os valores *applicationRoute* e *applicationGUID* pelos valores em **Opções de dispositivo móvel** no painel do {{site.data.keyword.Bluemix_notm}}.

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(),
					"applicationRoute",
					"applicationGUID");
```


## Fazendo uma solicitação para seu backend móvel
{: #request}

Após a inicialização do {{site.data.keyword.amashort}} client SDK, é possível começar a fazer solicitações para seu backend móvel.

1. Tente enviar uma solicitação para o terminal protegido de seu novo backend móvel. Em
seu navegador, abra esta URL: `{applicationRoute}/protected`. Por exemplo: `http://my-mobile-backend.mybluemix.net/protected`
<br/>O terminal `/protected` de um backend móvel criado com o modelo MobileFirst Services Starter está protegido com o {{site.data.keyword.amashort}}. Uma mensagem `Unauthorized` é retornada em seu navegador porque esse terminal pode ser acessado somente por aplicativos móveis instrumentados com o {{site.data.keyword.amashort}} client SDK.

1. Use seu aplicativo Android para fazer uma solicitação para o mesmo terminal. Inclua o código a seguir depois de inicializar `BMSClient`:

	```Java
	Request request = new Request("/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
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

1. Quando sua solicitação for bem-sucedida, você verá a saída a seguir no utilitário LogCat:

	![image](images/getting-started-android-success.png)

## Próximas etapas
{: #next-steps}

Quando você se conectou ao terminal protegido, nenhuma credencial foi necessária. Para requerer que os usuários efetuem login em seu aplicativo, deve-se configurar a autenticação do Facebook, do Google ou customizada.
* [Facebook](facebook-auth-android.html)
* [Google](google-auth-android.html)
* [Customizada](custom-auth-android.html)
