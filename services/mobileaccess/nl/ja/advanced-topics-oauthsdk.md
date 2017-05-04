---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-04-06"

---

{:codeblock:.codeblock}

**重要: {{site.data.keyword.amafull}} サービスは {{site.data.keyword.appid_full}} サービス**に置き換えられます。

# バックエンドのアプリケーションおよびサービス間の通信
{: #backend-comm}

場合によっては、{{site.data.keyword.Bluemix}} 上で実行しているバックエンド・アプリケーションから、{{site.data.keyword.amafull}} サービスで保護されている別のバックエンド・サービス (例えば {{site.data.keyword.cloudant}} サービス) に要求を送信する必要があります。そういったケースでは、要求に OAuth トークンを追加する必要があります。

OAuth トークンを取得して要求に注入するには、`bms-mca-oauth-sdk npmjs` モジュールを使用します。

## bms-mca-oauth-sdk モジュールのインストール
{: #sdk}

コマンド・ラインで、Node.js アプリケーション・ディレクトリーを開き、以下のコマンドを実行します。

```Bash
npm install -save bms-mca-oauth-sdk
```
{: codeblock}

## bms-mca-oauth-sdk モジュールの使用
{: #using-sdk}

以下のコードは、`bms-mca-oauth-sdk` モジュールの使用法を示します。


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
