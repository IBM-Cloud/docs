---

copyright:
  years: 2015, 2016 lastupdated: "2016-10-10"
---
{:shortdesc: .shortdesc}
{:screen:.screen}


# Configurando o SDK do Android
{: #getting-started-android}

Instrumente seu aplicativo Android com o {{site.data.keyword.amafull}} client SDK, inicialize o SDK e faça as solicitações para recursos protegidos e desprotegidos.

{:shortdesc}

## Antes de Começar
{: #before-you-begin}
Você deve ter:
* Uma instância de um aplicativo {{site.data.keyword.Bluemix_notm}} que seja protegida pelo serviço {{site.data.keyword.amashort}}. Para obter mais informações sobre como criar um aplicativo backend do {{site.data.keyword.Bluemix_notm}}, consulte [Introdução](index.html).
* Os seus valores de parâmetros de serviço. Abra o seu serviço no painel do {{site.data.keyword.Bluemix_notm}}. Clique em **Opções de
dispositivo móvel**. Os valores `applicationRoute` e `tenantId` (também conhecidos como `appGUID`) são
exibidos nos campos **Rota** e **GUID / TenantId do aplicativo**. Você precisará desses valores para inicializar o SDK e para
enviar solicitações para o aplicativo backend.
* Um projeto Android Studio, configure para trabalhar com Gradle. Para obter mais informações sobre como configurar seu ambiente de desenvolvimento do Android, veja [Google Developer Tools](http://developer.android.com/sdk/index.html).

## Instalando o {{site.data.keyword.amashort}} client SDK
{: #install-mca-sdk}

O {{site.data.keyword.amashort}} client SDK é distribuído com o Gradle, um gerenciador de dependência para projetos Android. O Gradle
faz download automaticamente de artefatos a partir de repositórios e os disponibiliza ao seu aplicativo Android.

1. Crie um projeto Android Studio ou abra um projeto existente.

1. Abra o arquivo `build.gradle` para seu aplicativo (**não** o arquivo `build.gradle`
do projeto).

1. Localize a seção **dependências** do arquivo `build.gradle`.  Inclua uma dependência de compilação para o {{site.data.keyword.amashort}} client SDK:

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

1. Sincronizar seu projeto com o Gradle. Clique em **Ferramentas &gt; Android &gt; Sincronizar projeto com arquivos Gradle**.

1. Abra o arquivo `AndroidManifest.xml` para seu projeto Android. Inclua a permissão de acesso à Internet no elemento `<manifest>`:

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
```

## Inicializando o {{site.data.keyword.amashort}} client SDK
{: #initalize-mca-sdk}

Inicialize o SDK do cliente passando os parâmetros **context** e **region** para o
método `initialize`. Um local comum, mas não obrigatório, para colocar o código de inicialização é o método `onCreate` da atividade principal em seu aplicativo Android.

```Java 	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_UK);
BMSClient.getInstance().setAuthorizationManager(
                 MCAAuthorizationManager.createInstance(this, "MCAServiceTenantId"));

```

   * Substitua o `BMSClient.REGION_UK` pela região apropriada.  Para visualizar sua região do {{site.data.keyword.Bluemix_notm}}, clique no ícone de **Avatar** ![Ícone de Avatar](images/face.jpg "Ícone de Avatar") na barra de menus para abrir o widget **Conta e suporte**. O valor da região deve ser um destes: `BMSClient.REGION_US_SOUTH`,
`BMSClient.REGION_SYDNEY` ou `BMSClient.REGION_UK`.
   * Substitua "MCAServiceTenantId" pelo valor **tenantId** (veja [Antes de iniciar](#before-you-begin)). 

## Fazendo uma solicitação para seu aplicativo backend móvel
{: #request}

Após o SDK do cliente {{site.data.keyword.amashort}} ser inicializado, será possível começar a fazer solicitações ao seu aplicativo
backend móvel.

1. Tente enviar uma solicitação a um terminal protegido do seu novo aplicativo backend móvel. Em
seu navegador, abra a URL a seguir: `{applicationRoute}/protected`
(por exemplo `http://my-mobile-backend.mybluemix.net/protected`).   Para informações sobre como obter o valor `{applicationRoute}`, veja
[Antes de iniciar](#before-you-begin). 
	
	O terminal `/protected` de um aplicativo backend móvel que foi criado com o modelo MobileFirst Services Starter é protegido com {{site.data.keyword.amashort}}. Uma mensagem `Unauthorized` é retornada em seu navegador, porque esse terminal só pode ser acessado por aplicativos móveis instrumentados com o SDK do cliente {{site.data.keyword.amashort}}.

1. Use seu aplicativo Android para fazer uma solicitação ao mesmo terminal. Inclua o código a seguir depois de inicializar o `BMSClient`:

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

1. Quando suas solicitações forem bem-sucedidas, você verá a saída a seguir no utilitário LogCat:

	![image](images/getting-started-android-success.png)

## Próximas Etapas
{: #next-steps}

Quando você se conectou ao terminal protegido, nenhuma credencial foi necessária. Para requerer que os usuários efetuem login no aplicativo, deve-se configurar autenticação do Facebook, Google ou customizada.
* [Facebook
](facebook-auth-android.html)
* [Google](google-auth-android.html)
* [Customizada
](custom-auth-android.html)
