---

copyright:
  years: 2015, 2016
  
---

# 백엔드 간 통신
{: #backend-comm}

일부 고급 시나리오에서는 {{site.data.keyword.Bluemix}}에서 실행 중인 사용자의 백엔드 애플리케이션에서
{{site.data.keyword.amashort}} 서비스가 보호하는 다른 백엔드 서비스(예:
{{site.data.keyword.cloudant}} 서비스)로 요청을 전송해야 할 수 있습니다. 이러한 경우
OAuth 토큰을 요청에 추가해야 합니다. 

OAuth 토큰을 확보하여 요청에 삽입하려면 `bms-mca-oauth-sdk` npmjs 모듈을 사용하십시오. 

## bms-mca-oauth-sdk 모듈 설치
{: #sdk}

명령행에서 Node.js 애플리케이션 디렉토리를 열고 다음 명령을 실행하십시오. 

```Bash
npm install -save bms-mca-oauth-sdk
```

## bms-mca-oauth-sdk 모듈 사용
{: #using-sdk}

다음 코드는 `bms-mca-oauth-sdk` 모듈의 사용법을 보여줍니다. 


``` JavaScript
var oauthSDK = require('bms-mca-oauth-sdk');

var options = {

	// You can cache tokens to avoid extra roundtrips on every request
	// This property defines the number of tokens to be cached

	cacheSize: 100,

	// All of the below properties are retrieved automatically when your Node.js
	// runs on {{site.data.keyword.Bluemix_notm}} and bound to an instance of {{site.data.keyword.amashort}} Service.
	// Alternatively you can get these properties values by clicking Show Credentials
	// on the {{site.data.keyword.amashort}} Service tile in your {{site.data.keyword.Bluemix_notm}} application dashboard

	appId: "appId",				// Bleumix applicationGUID, a.k.a tenantId
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
