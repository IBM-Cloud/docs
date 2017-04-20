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

# Usando o {{site.data.keyword.amashort}} com um ambiente de desenvolvimento local
{: #protecting-local}

É possível configurar seu desenvolvimento local para usar o serviço {{site.data.keyword.amafull}} que está em execução no {{site.data.keyword.Bluemix}}. Especificamente, é possível desenvolver o código localmente usando o SDK do servidor {{site.data.keyword.amashort}} e enviar solicitações
{{site.data.keyword.amashort}} ao servidor de desenvolvimento. Essas solicitações serão protegidas pelo serviço
{{site.data.keyword.amashort}} que está em execução no {{site.data.keyword.Bluemix}}.

## Antes de iniciar
{: #before-you-begin}

Você deve ter:

* Uma instância de um aplicativo {{site.data.keyword.Bluemix_notm}} que seja protegida pelo serviço {{site.data.keyword.amashort}}. Para obter mais informações sobre como criar um aplicativo backend do {{site.data.keyword.Bluemix_notm}}, consulte [Introdução](index.html).
* Seu **TenantID**. Abra o seu serviço no painel do {{site.data.keyword.amafull}}. Clique no botão **Opções móveis**. Os valores
`tenantId` (também conhecido como
`appGUID`) são exibidos no campo **App
GUID / TenantId**. Você precisará desse valor para
inicializar o Gerenciador de Autorização.
* Sua **Rota do aplicativo**. Esta é a
URL do seu aplicativo backend. Você precisa desse valor para
enviar solicitações para seus terminais protegidos.
* A {{site.data.keyword.Bluemix_notm}}
**Região**.  É possível encontrar a sua região
{{site.data.keyword.Bluemix_notm}} atual no cabeçalho,
próximo ao ícone **Avatar**
![ícone de avatar](images/face.jpg "ícone de avatar"). O valor da região
que aparece deve ser um dos valores a seguir: `US South`, `Sydney`
ou `United Kingdom`. Para a sintaxe exata requerida pelo SDK, veja os comentários
nas amostras de código. Você precisará desse
valor para inicializar o cliente
{{site.data.keyword.amashort}}.
* Um projeto Android Studio, configure para trabalhar com Gradle. Para obter mais informações
sobre como configurar seu ambiente de desenvolvimento Android, veja [Google Developer Tools ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](http://developer.android.com/sdk/index.html){: new_window}.

## Configurando o SDK do servidor
{: #serversetup}

O SDK do servidor {{site.data.keyword.amashort}} requer que duas variáveis do ambiente sejam configuradas. Quando você estiver desenvolvendo código do lado do servidor no {{site.data.keyword.Bluemix_notm}}, essas variáveis serão fornecidas pela infraestrutura do {{site.data.keyword.Bluemix_notm}}.

* `VCAP_SERVICES`: contém informações sobre serviços que estão ligados ao aplicativo backend móvel.
* `VCAP_APPLICATION`: contém informações sobre o aplicativo backend móvel.

Para usar o {{site.data.keyword.amashort}} com um servidor de desenvolvimento local, deve-se incluir manualmente essas variáveis de ambiente.

1. Abra o painel {{site.data.keyword.Bluemix_notm}} do seu aplicativo backend móvel que é protegido com o serviço
{{site.data.keyword.amashort}}.

1. Em seu ambiente de desenvolvimento local, configure a variável de ambiente *VCAP_APPLICATION*. A variável deve conter um objeto JSON em sequência com uma única propriedade.
	```JavaScript
	{
	    application_id: "appGUID"
	}
	```
	{: codeblock}

1. Clique na guia **Mostrar credenciais** no painel do {{site.data.keyword.amashort}}. Um objeto JSON é exibido com credenciais de acesso que o {{site.data.keyword.amashort}} fornece para seu aplicativo backend móvel.

1. Em seu ambiente de desenvolvimento local, configure a variável de ambiente `VCAP_SERVICES`. O valor dessa variável deve ser um objeto JSON em sequência que contém as credenciais do {{site.data.keyword.amashort}}.  Consulte a amostra a seguir para obter mais informações.

## Código do servidor de amostra
{: #local-dev-sample}

Para usar o serviço {{site.data.keyword.amashort}} em um ambiente de desenvolvimento Node.js local, inclua o código a seguir.  

```JavaScript
var vcapApplication = {
	application_id:"tenantID"
};

var vcapServices = {
	"AdvancedMobileAccess": [
		{
			"credentials": {
				"admin_url": "https://mobile.ng.bluemix.net/imfmobileplatformdashboard/?appGuid=appGUID",
				"clientId": "tenantID",
				"secret": "secret",
				"serverUrl": "https://imf-authserver.ng.bluemix.net/imf-authserver",
				"tenantId": "tenantId"
			}
		}
	]
};

process.env["VCAP_APPLICATION"] = JSON.stringify(vcapApplication);
process.env["VCAP_SERVICES"] = JSON.stringify(vcapServices);

// Agora, é possível requerer o módulo bms-mca-token-validation-strategy:
var MCABackendStrategy =
	require('bms-mca-token-validation-strategy').MCABackendStrategy;

// Restante de seu código
```
{: codeblock}

Para obter informações sobre a localização do valor *tenantID*, veja [Antes de iniciar](#before-you-begin).


## Configurando aplicativos {{site.data.keyword.amashort}} para trabalhar com um servidor de desenvolvimento local
{: #configuring-local}

Inicialize os SDKs do cliente {{site.data.keyword.amashort}} com a URL real do seu aplicativo {{site.data.keyword.Bluemix_notm}} e use o localhost (ou endereço IP) em cada uma de suas solicitações. Consulte as amostras a seguir.

Substitua a região pela região apropriada. Veja os exemplos de código para a sintaxe correta.

Substitua os valores *appGUID* e *bluemixAppRoute*. Para obter informações sobre como obter esses valores, consulte
[Antes de iniciar](#before-you-begin).

Pode ser necessário mudar `localhost` para um endereço IP real de seu servidor de desenvolvimento nos exemplos a seguir.

### Android
{: #android}

```Java
String baseRequestUrl = "http://localhost:3000";
String bluemixAppRoute = "http://myapp.mybluemix.net";
String bluemixAppGUID = "your-bluemix-app-guid";
String tenantId = "your-MCA-service-tenantID";


BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_UK);

//  set your MCA application region here. Currently possible values are BMSClient.REGION_US_SOUTH, BMSClient.REGION_SYDNEY, or BMSClient.REGION_UK

BMSClient.getInstance().setAuthorizationManager(
					MCAAuthorizationManager.createInstance(this, "<MCAServiceTenantId>"));

Request request =
			new Request(baseRequestUrl + "/resource/path", Request.GET);

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
{: codeblock}


### iOS - Swift
{: #swift}

```Swift

 let baseRequestUrl = "http://localhost:3000";
 let tenantId = "<serviceTenantID>"
 let regionName = <applicationBluemixRegion>
 //possible values: BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, or BMSClient.Region.sydney
 let mcaAuthManager = MCAAuthorizationManager.sharedInstance
 mcaAuthManager.initialize(tenantId: tenantId, bluemixRegion: regionName)
 BMSClient.sharedInstance.authorizationManager = mcaAuthManager


 let requestPath = baseRequestUrl + "/protectedResource"
 let request = Request(url: requestPath, method: HttpMethod.GET)

    request.send { (response, error) in
	if let error = error {
            print("Connection failure")
     		print("Error :: \(error)");
     		print("Status :: \(response?.statusCode)");
    	} else {
            print("Connection success")
            print("Response :: \(response?.responseText)")
        }
    }

```
{: codeblock}


### Cordova
{: #cordova}

```JavaScript
var baseRequestUrl = "http://localhost:3000";
var bluemixAppRoute = "http://myapp.mybluemix.net";
var bluemixAppGUID = "your-bluemix-app-guid";
Var tenantId = "your-MCA-service-tenantID";

BMSClient.initialize(<applicationBluemixRegion>);

var success = function(data){
   	console.log("success", data);
}

var failure = function(error){
	console.log("failure", error);
}

var request = new MFPRequest(baseRequestUrl +
							"/resource/path", MFPRequest.GET);

request.send(success, failure);
```
{: codeblock}
