---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-08"

---

{:codeblock:.codeblock}

# Comunicando-se entre aplicativos backend e serviços
{: #backend-comm}

Em alguns cenários, pode ser necessário enviar solicitações de seu aplicativo backend que está em execução no {{site.data.keyword.Bluemix}} para outro serviço de backend que está protegido pelo serviço {{site.data.keyword.amafull}} (por exemplo, o serviço {{site.data.keyword.cloudant}}). Nesses casos, deve-se incluir um token OAuth na solicitação.

Use o módulo `bms-mca-oauth-sdk npmjs` para obter e injetar tokens OAuth nas solicitações.

## Instalando o módulo bms-mca-oauth-sdk
{: #sdk}

Em uma linha de comandos, abra o diretório do aplicativo Node.js e execute o comando a seguir:

```Bash
npm install -save bms-mca-oauth-sdk
```
{: codeblock}

## Usando o módulo bms-mca-oauth-sdk
{: #using-sdk}

O código a seguir demonstra como usar o módulo `bms-mca-oauth-sdk`.


``` JavaScript
var oauthSDK = require('bms-mca-oauth-sdk');

var options = {

	// É possível armazenar tokens em cache para evitar roundtrips extras em cada solicitação
	// Essa propriedade define o número de tokens a serem armazenados em cache

	cacheSize: 100,

	// The following properties are retrieved automatically when your Node.js
	// runs on {{site.data.keyword.Bluemix_notm}} and bound to an instance of {{site.data.keyword.amashort}} Service.
	// Alternatively, you can get these property values by clicking Show Credentials
	// on the {{site.data.keyword.amashort}} Service tile in your {{site.data.keyword.Bluemix_notm}} application dashboard

	appId: "tenantID",				// a.k.a. Bluemix applicationGUID
	clientId: "clientId",			
	secret: "secret",
	serverUrl: "serverUrl"
};

oauthSDK.getAuthorizationHeader(options).then(function(authHeader){

	// In the request that you want to send to the protected
resource, 	// add the authHeader value.

	request.headers.Authorization = authHeader;

	// Enviar solicitação

});

```
{: codeblock}
