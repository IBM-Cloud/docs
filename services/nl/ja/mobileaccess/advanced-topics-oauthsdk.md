---

copyright:
  years: 2015, 2016
  
---

# バックエンド間の通信
{: #backend-comm}

高機能シナリオでは、{{site.data.keyword.Bluemix}} 上で実行しているバックエンド・アプリケーションから、{{site.data.keyword.amashort}} サービスで保護されている別のバックエンド・サービス (例えば {{site.data.keyword.cloudant}} サービス) に要求を送信する必要がある場合があります。そういったケースでは、要求に OAuth トークンを追加する必要があります。

OAuth トークンを取得して要求に注入するには、`bms-mca-oauth-sdk` npmjs モジュールを使用します。

## bms-mca-oauth-sdk モジュールのインストール
{: #sdk}

コマンド・ラインで、Node.js アプリケーション・ディレクトリーを開き、以下のコマンドを実行します。

```Bash
npm install -save bms-mca-oauth-sdk
```

## bms-mca-oauth-sdk モジュールの使用
{: #using-sdk}

以下のコードは、`bms-mca-oauth-sdk` モジュールの使用法を示します。


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
