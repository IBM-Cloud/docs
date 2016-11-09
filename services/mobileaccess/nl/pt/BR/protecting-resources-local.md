---

copyright:
  years: 2015, 2016 lastupdated: "2016-10-10"
---
{:shortdesc: .shortdesc} 

# Usando o {{site.data.keyword.amashort}} com um ambiente de desenvolvimento local
{: #protecting-local}

É possível configurar seu desenvolvimento local para usar o serviço {{site.data.keyword.amafull}} que está em execução no {{site.data.keyword.Bluemix}}. Especificamente, é possível desenvolver o código localmente usando o SDK do servidor {{site.data.keyword.amashort}} e enviar solicitações
{{site.data.keyword.amashort}} ao servidor de desenvolvimento. Essas solicitações serão protegidas pelo serviço
{{site.data.keyword.amashort}} que está em execução no {{site.data.keyword.Bluemix}}.

## Antes de iniciar
{: #before-you-begin}
Você deve ter:

* Uma instância de um aplicativo {{site.data.keyword.Bluemix_notm}} que seja protegida pelo serviço {{site.data.keyword.amashort}}. Para obter mais informações sobre como criar um aplicativo backend do {{site.data.keyword.Bluemix_notm}}, consulte [Introdução](index.html).
* Os seus valores de parâmetros de serviço. Abra o seu serviço no painel do {{site.data.keyword.Bluemix_notm}}. Clique em **Opções de
dispositivo móvel**. Os valores `applicationRoute` e `appGUID` (também conhecidos como `tenantId`) são
exibidos nos campos **Rota** e **GUID / TenantId do aplicativo**. Você precisará desses valores para inicializar o SDK e para
enviar solicitações para o aplicativo backend.
*  Localize a região na qual o seu aplicativo {{site.data.keyword.Bluemix_notm}} está hospedado. Para visualizar sua região do {{site.data.keyword.Bluemix_notm}}, clique no ícone de **Avatar** ![Ícone de Avatar](images/face.jpg "Ícone de Avatar") na barra de menus para abrir o widget **Conta e suporte**. O valor da região deve ser um destes: **US South**, **Sydney** ou **UK**. Os valores constantes de
SDK exatos que correspondem a esses nomes são indicados nos exemplos de código. 

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

Substitua o *appGUID* pelo valor `appGUID` obtido em [Antes de iniciar](#before-you-begin). 

1. Clique em **Mostrar credenciais** no tile do serviço {{site.data.keyword.amashort}} em seu
aplicativo backend móvel no painel {{site.data.keyword.Bluemix_notm}}. Um objeto JSON é exibido com credenciais de acesso que o {{site.data.keyword.amashort}} fornece para seu aplicativo backend móvel.

1. Em seu ambiente de desenvolvimento local, configure a variável de ambiente `VCAP_SERVICES`. O valor dessa variável deve ser um objeto JSON em sequência que contém as credenciais do {{site.data.keyword.amashort}}.  Veja a amostra a seguir para obter mais informações.

## Código do servidor de amostra
{: #local-dev-sample}

Para usar o serviço {{site.data.keyword.amashort}} em um ambiente de desenvolvimento Node.js local, inclua o código a seguir.  

```JavaScript
var vcapApplication = {
	application_id:"appGUID"
};

var vcapServices = {
	"AdvancedMobileAccess": [
		{
			"credentials": {
				"admin_url": "https://mobile.ng.bluemix.net/imfmobileplatformdashboard/?appGuid=appGUID",
				"clientId": "appGUID",
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

Substitua o *appGUID* pelo valor `appGUID` obtido em [Antes de iniciar](#before-you-begin). 


## Configurando aplicativos {{site.data.keyword.amashort}} para trabalhar com um servidor de desenvolvimento local
{: #configuring-local}

Inicialize os SDKs do cliente {{site.data.keyword.amashort}} com a URL real do seu aplicativo {{site.data.keyword.Bluemix_notm}} e use o localhost (ou endereço IP) em cada uma de suas solicitações. Veja as amostras a seguir.

Substitua a região pela região apropriada.

Substitua os valores *appGUID* e *bluemixAppRoute* pelos valores obtidos em [Antes de iniciar](#before-you-begin). 

Pode ser necessário mudar `localhost` para um endereço IP real de seu servidor de desenvolvimento nos exemplos a seguir.

### Android
{: #android}
```Java
String baseRequestUrl = "http://localhost:3000";
String bluemixAppRoute = "http://myapp.mybluemix.net";
String bluemixAppGUID = "your-bluemix-app-guid";
String tenantId = "your-MCA-service-tenantID";

BMSClient.getInstance().initialize(bluemixAppRoute, bluemixAppGUID, BMSClient.REGION_UK); 
//  set your MCA application region here. Currently possible values are BMSClient.REGION_US_SOUTH, BMSClient.REGION_SYDNEY, or BMSClient.REGION_UK
BMSClient.getInstance().setAuthorizationManager(
                 MCAAuthorizationManager.createInstance(this, tenantId));

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



### iOS - Objective C
{: #objc}

```Objective-C
NSString *baseRequestUrl = @"http://localhost:3000";
NSString *bluemixAppRoute = @"http://myapp.mybluemix.net";
NSString *bluemixAppGUID = @"your-bluemix-app-guid";
NSString *tenantId = "your-MCA-service-tenantID";

[[IMFClient sharedInstance]
			initializeWithBackendRoute:bluemixAppRoute
			backendGUID:bluemixAppGUID];
			
[[IMFAuthorizationManager sharedInstance]  initializeWithTenantId: tenantId];


NSString *requestPath = [NSString stringWithFormat:@"%@/resource/path",
								baseRequestUrl];

IMFResourceRequest *request =  [IMFResourceRequest
				requestWithPath:requestPath
				method:@"GET"];

[request sendWithCompletionHandler:^(IMFResponse *response, NSError *error) {
	if (error){
		NSLog(@"Error :: %@", [error description]);
	} else {
		NSLog(@"Response :: %@", [response responseText]);
	}
}];
```


### iOS - Swift
{: #swift}

```Swift

let baseRequestUrl = "http://localhost:3000"
let bluemixAppRoute = "http://myapp.mybluemix.net"
let tenantId = "your-MCA-service-tenantID"
let regionName = BMSClient.Region.usSouth
// set your MCA application region here. Currently these can be BMSClient.Region.usSouth, BMSClient.Region.unitedKingdom, BMSClient.Region.sydney

BMSClient.sharedInstance.initialize(bluemixAppRoute: bluemixAppRoute, bluemixAppGUID: tenantId, bluemixRegion: regionName)

BMSClient.sharedInstance.authorizationManager = MCAAuthorizationManager.sharedInstance
           
let requestPath = baseRequestUrl + "/resource/path"               
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


### Cordova
{: #cordova}

```JavaScript
var baseRequestUrl = "http://localhost:3000";
var bluemixAppRoute = "http://myapp.mybluemix.net";
var bluemixAppGUID = "your-bluemix-app-guid";
Var tenantId = "your-MCA-service-tenantID";

BMSClient.initialize(bluemixAppRoute, bluemixAppGUID);

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

