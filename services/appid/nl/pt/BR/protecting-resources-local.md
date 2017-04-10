---

copyright:
  years:  2017
lastupdated: "2017-03-30"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}



# Usando o {{site.data.keyword.appid_short_notm}} com um ambiente de desenvolvimento local
{: #protecting-local}

É possível configurar o seu ambiente local para usar o serviço do {{site.data.keyword.appid_short}}. Especificamente, é possível desenvolver o código
localmente usando o SDK do servidor {{site.data.keyword.appid_short_notm}} e enviar solicitações ao servidor de desenvolvimento.
{:shortdesc}


## Configurando o SDK do servidor
{: #serversetup}

Para usar o {{site.data.keyword.appid_short_notm}} com um servidor de desenvolvimento local, deve-se passar o parâmetro de opção quando você estiver
criando a sua estratégia, com os atributos a seguir:

* APIStrategy: `oauthServerUrl`
* WebAppStrategy: tenantId, clientId, secret, oauthServerUrl, redirectUri

Configure o seu atributo 'redirectUri' para a sua porta de app de host local com o caminho de retorno de chamada, ou seja:
`http://localhost:<port>/callback`. O terminal de retorno de chamada conclui o processo de autorização.

Para obter as suas credenciais de serviço, conclua as etapas a seguir:

1. Abra o seu painel do {{site.data.keyword.Bluemix_notm}} e clique na guia **Credenciais de serviço**.
2. Clique em **Mostrar credenciais**. As suas credenciais de acesso são exibidas como um Objeto da JSON.

Para obter amostras e mais informações, veja <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">o repositório do GitHub
do SDK do servidor <img src="../../icons/launch-glyph.svg" alt="ícone de Link externo"></a>.


## Configurando aplicativos {{site.data.keyword.appid_short_notm}} para trabalhar com um servidor de desenvolvimento local
{: #configuring-local}

Para configurar os seus apps para trabalharem com um servidor de desenvolvimento local, use o host local em cada uma de suas solicitações.

1. Substitua o ID do locatário pelo seu ID do locatário do {{site.data.keyword.appid_short_notm}}. É possível localizar esse ID em seu painel de
serviço.
2. Substitua a região pela região apropriada, conforme mostrado na tabela a seguir.

<table> <caption> Tabela 1. Regiões do {{site.data.keyword.Bluemix_notm}} e regiões do {{site.data.keyword.appid_short_notm}} correspondentes para Android e iOS </caption>
<tr>
  <th> Região do Bluemix </th>
  <th> Android </th>
</tr>
<tr>
  <td> Sul dos Estados Unidos </td>
  <td> AppID.REGION_US_SOUTH </td>
</tr>
<tr>
  <td> Sydney </td>
  <td> AppID.REGION_SYDNEY </td>
</tr>
<tr>
  <td> United Kingdom </td>
  <td> AppID.REGION_UK </td>
</tr>
</table>



### Android
{: #android}
```java
String baseRequestUrl = "http://localhost:<port>"; //set to your server running port
String tenantId = "your-AppID-service-tenantID";
String region = AppID.REGION_UK; //set your App ID application region here. Currently possible values are AppID.REGION_US_SOUTH, AppID.REGION_SYDNEY, or
AppID.REGION_UK.

BMSClient bmsClient= BMSClient.getInstance();
bmsClient.initialize(getApplicationContext(), region);
AppID appId = AppID.getInstance();
appId.initialize(getApplicationContext(), tenantId, region);

AppIDAuthorizationManager appIDAuthorizationManager = new AppIDAuthorizationManager(appId);
bmsClient.setAuthorizationManager(appIDAuthorizationManager);

Request request = new Request(baseRequestUrl + "/resource/path", Request.GET);
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
{:pre}

### iOS - Swift
{: #swift}
```swift

 let baseRequestUrl = "http://localhost:<port>"; //set to your server running port
 let tenantId = "your-AppID-service-tenantID"
 let region = AppID.REGION_UK; //set your App ID application region here. Currently possible values are AppID.REGION_US_SOUTH, AppID.REGION_SYDNEY, or
AppID.REGION_UK.

BMSClient.sharedInstance.initialize(bluemixRegion: region)
BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid:AppID.sharedInstance)

var request:Request =  Request(url: baseRequestUrl + "/resource/path", method: HttpMethod.GET)
request.send(completionHandler: {(response:Response?, error:Error?) in
    if let error = error {
            print("Connection failure")
     		print("Error :: \(error)");
     		print("Status :: \(response?.statusCode)");
    	} else {
            print("Connection success")
           print("Response :: \(response?.responseText)")
        }
});
```
{:pre}
