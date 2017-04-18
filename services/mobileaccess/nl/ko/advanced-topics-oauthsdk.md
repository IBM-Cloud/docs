---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-04-06"

---

{:codeblock:.codeblock}

**중요: {{site.data.keyword.amafull}} 서비스는 {{site.data.keyword.appid_full}} 서비스로 대체되었습니다. **

# 백엔드 애플리케이션 및 서비스 간의 통신
{: #backend-comm}

일부 시나리오에서는 {{site.data.keyword.Bluemix}}에서 실행 중인 사용자의 백엔드 애플리케이션에서 {{site.data.keyword.amafull}} 서비스가 보호하는 다른 백엔드 서비스(예: {{site.data.keyword.cloudant}} 서비스)로 요청을 전송해야 할 수 있습니다. 이러한 경우 OAuth 토큰을 요청에 추가해야 합니다. 

`bms-mca-oauth-sdk npmjs` 모듈을 사용하여 OAuth 토큰을 확보하여 요청에 삽입하십시오.

## bms-mca-oauth-sdk 모듈 설치
{: #sdk}

명령행에서 Node.js 애플리케이션 디렉토리를 열고 다음 명령을 실행하십시오. 

```Bash
npm install -save bms-mca-oauth-sdk
```
{: codeblock}

## bms-mca-oauth-sdk 모듈 사용
{: #using-sdk}

다음 코드는 `bms-mca-oauth-sdk` 모듈의 사용법을 보여줍니다. 


``` JavaScript
var oauthSDK = require('bms-mca-oauth-sdk');

var options = {

	// You can cache tokens to avoid extra roundtrips on every request
	// This property defines the number of tokens to be cached

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

	// In the request that you want to send to the protected resource,
	// add the authHeader value.

	request.headers.Authorization = authHeader;

	// Send request

});

```
{: codeblock}
