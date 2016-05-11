---

copyright:
  years: 2015, 2016

---

# カスタム ID プロバイダーの作成
{: #custom-create}
カスタム ID プロバイダーを作成するには、次の RESTful API を公開する Web アプリケーションを開発します。

```
POST <base_url>/apps/<tenant_id>/<realm_name>/<request_type>
```

* `base_url`: カスタム ID プロバイダー Web アプリケーションのベース URL を指定します。このベース URL は、{{site.data.keyword.amashort}} ダッシュボードに登録される URL です。
* `tenant_id` : テナントの固有 ID を指定します。{{site.data.keyword.amashort}} は、この API を起動するときに、常に {{site.data.keyword.Bluemix}} アプリ GUID (`applicationGUID`) を提供します。
* `realm_name` : {{site.data.keyword.amashort}} ダッシュボードで定義されたカスタム・レルム名を指定します。
* `request_type` : 以下のいずれかを指定します。
	* `startAuthorization`: 認証プロセスの最初のステップを指定します。カスタム ID プロバイダーは、「challenge」、「success」、または「failure」のいずれかの状況とともに応答する必要があります。
	* `handleChallengeAnswer`: モバイル・クライアントからの認証チャレンジ応答を処理します。

## `startAuthorization` API
{: #custom-startauthorization}

`POST <base_url>/apps/<tenant_id>/<realm_name>/startAuthorization`

`startAuthorization` API は、認証プロセスの最初のステップとして使用されます。カスタム ID プロバイダーは、「challenge」、「success」、または「failure」のいずれかの状況とともに応答する必要があります。

認証プロセスの柔軟性を最大にできるように、カスタム ID プロバイダーは、モバイル・クライアントによって要求本体に入れて送信されたすべての HTTP ヘッダーへのアクセス権限を持ちます。それらのヘッダーの形式は次のとおりです。

```JavaScript
{
    "headers" : {
    	"header1": "value1",  
    	"header2" : "value2"
    }
}
```

カスタム ID プロバイダーは、認証チャレンジとともに応答を返すか、または、即時成功または失敗を返します。応答 HTTP 状況は `HTTP 200` でなければならず、応答 JSON には以下のプロパティーが含まれている必要があります。

* `status` : 要求の `success`、`challenge`、または `failure` を指定します。
* `stateId` (オプション): モバイル・クライアントで認証セッションを識別するための、ランダムに生成されるストリング ID を指定します。この属性は、カスタム ID プロバイダーが状態を保管しない場合は省略可能です。
* `challenge` : モバイル・クライアントに送り返される認証チャレンジを表す JSON オブジェクトを指定します。この属性は、status が `challenge` に設定されている場合のみクライアントに送信されます。
* `userIdentity` : ユーザー ID を表す JSON オブジェクトを指定します。ユーザー ID は、プロパティー (`userName`、`displayName` など) および属性からなります。詳しくは、[ユーザー ID オブジェクト](#custom-user-identity)を参照してください。このプロパティーは、status が `success` に設定されている場合のみモバイル・クライアントに送信されます。

以下に例を示します。

```
{
	"status":"challenge",
	"stateId":"some-random-guid"
	"challenge":{
		message:"Enter username and password",
		attemptsLeft: 3
	}
}
```

## `handleChallengeAnswer` API
{: #custom-handleChallengeAnswer}

`POST <base_url>/apps/<tenant_id>/<realm_name>/handleChallengeAnswer`

`handleChallengeAnswer` API は、モバイル・クライアントからの認証チャレンジ応答を処理します。`startAuthorization` API と同様に、`handleChallengeAnswer` API は、`challenge`、`success`、または `failure` のいずれかの状況で応答します。

`startAuthorization` 要求と同様に、カスタム ID プロバイダーは、モバイル・クライアントによって要求本体に入れて送信されたすべての HTTP ヘッダーへのアクセス権限を持ちます。モバイル・クライアント要求ヘッダーに加えて、`handleChallengeAnswer` 要求の本体にも `stateId` および `challengeAnswer` プロパティーが含まれます。

### `handleChallengeAnswer` 要求本体の例
{: #custom-handleChallengeAnswer-example}

```JavaScript
{
    "headers" : {
    	"header1": "value1",  
    	"header2" : "value2"
	},
    "stateId" : "123123123",
    "challengeAnswer" : {
    	"pinCode":12345
 	}
}
```

`handleChallengeAnswer` API からの応答は、`startAuthorization` API の応答と同じ構造でなければなりません。

## ユーザー ID オブジェクト
{: #custom-user-identity}

成功した認証要求に対する応答は、以下の属性を持つユーザー ID オブジェクトを含んでいなければなりません。
* `userName` : 固有のユーザー名を指定します。
* `displayName` : ユーザーの表示名を指定します。
* `attributes` (オプション) : カスタム・ユーザー属性を含む JSON オブジェクトを指定します。

### ユーザー ID オブジェクトの例
{: #custom-user-identity-example}
```JavaScript
{
    "userName" : "janesmith",
    "displayName" : "Jane Smith",
    "attributes" : {
        "Language" : "French",
        "Country" : "Canada"
    }
}
```

ユーザー ID オブジェクトは、許可ヘッダーの一部としてモバイル・クライアントに送信される ID トークンを生成するために、{{site.data.keyword.amashort}} サービスによって使用されます。認証が成功した後、モバイル・クライアントはユーザー ID オブジェクトへの全アクセス権限を持ちます。

## セキュリティーに関する考慮事項
{: #custom-security}

{{site.data.keyword.amashort}} サービスからカスタム ID プロバイダーへの各要求には許可ヘッダーが含まれ、それによってカスタム ID プロバイダーは、許可されたソースからその要求が着信していることを検証できます。厳密には必須ではありませんが、カスタム ID プロバイダーに {{site.data.keyword.amashort}} Server SDK を装備することによって許可ヘッダーを検証することを検討してください。この SDK を使用するには、カスタム ID プロバイダー・アプリケーションが Node.js または Liberty for Java&trade;&trade; を使用して実装され、{{site.data.keyword.Bluemix_notm}} 上で実行される必要があります。

許可ヘッダーは、認証プロセスをトリガーしたモバイル・クライアントおよびモバイル・アプリについての情報を含みます。セキュリティー・コンテキストを使用して、このデータを取得できます。詳しくは、[リソースの保護](protecting-resources.html)を参照してください。

## カスタム ID プロバイダーのサンプル実装
{: #custom-sample}
カスタム ID プロバイダーを開発する際に参考として使用できる、カスタム ID プロバイダーの Node.js 実装のサンプルを以下に示します。GitHub リポジトリーから、完全なアプリケーション・コードをダウンロードしてください。

* [簡単なサンプル](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)
* [高度なサンプル](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management)

<!---
 ### JSON structure (simple sample)
{: #custom-sample-json}
This implementation assumes that the supplied authentication challenge answer is a JSON object with the following structure:

```
{
 	username: "my.username",
 	password: "my.password"
 }
 ```

### Custom identity provider sample code (simple sample)
{: #custom-sample-code}
```JavaScript
var express = require('express');
var cfenv = require('cfenv');
var log4js = require('log4js');
var jsonParser = require('body-parser').json();

// Using hardcoded user repository
var userRepository = {
	"john.lennon":      { password: "12345", displayName:"John Lennon", dob:"October 9, 1940"},
	"paul.mccartney":   { password: "67890", displayName:"Paul McCartney", dob:"June 18, 1942"},
	"ringo.starr":      { password: "abcde", displayName:"Ringo Starr", dob: "July 7, 1940"},
	"george.harrison":  { password: "fghij", displayName: "George Harrison", dob:"Feburary 25, 1943"}
}

var app = express();
var logger = log4js.getLogger("CustomIdentityProviderApp");
logger.info("Starting up");

app.post('/apps/:tenantId/:realmName/startAuthorization', jsonParser, function(req, res){
	var tenantId = req.params.tenantId;
	var realmName = req.params.realmName;
	var headers = req.body.headers;

	logger.debug("startAuthorization", tenantId, realmName, headers);

	var responseJson = {
		status: "challenge",
		challenge: {
			text: "Enter username and password"
		}
	};

	res.status(200).json(responseJson);
});

app.post('/apps/:tenantId/:realmName/handleChallengeAnswer', jsonParser, function(req, res){
	var tenantId = req.params.tenantId;
	var realmName = req.params.realmName;
	var challengeAnswer = req.body.challengeAnswer;


	logger.debug("handleChallengeAnswer", tenantId, realmName, challengeAnswer);

	var username = req.body.challengeAnswer["username"];
	var password = req.body.challengeAnswer["password"];

	var userObject = userRepository[username];

	var responseJson = { status: "failure" };

	if (userObject && userObject.password == password ){
		logger.debug("Login success for userId ::", username);
		responseJson.status = "success";
		responseJson.userIdentity = {
			userName: username,
			displayName: userObject.displayName,
			attributes: {
				dob: userObject.dob
			}
		}
	} else {
		logger.debug("Login failure for userId ::", username);
	}

	res.status(200).json(responseJson);
});

app.use(function(req, res, next){
	res.status(404).send("This is not the URL you're looking for");
});

var server = app.listen(cfenv.getAppEnv().port, function () {
	var host = server.address().address;
	var port = server.address().port;
	logger.info('Server listening at %s:%s', host, port);
});
```
--->

## 次のステップ
{: #next-steps}
* [カスタム認証用の {{site.data.keyword.amashort}} の構成 ](custom-auth-config-mca.html)
* [Android 用のカスタム認証の構成 ](custom-auth-android.html)
* [iOS 用のカスタム認証の構成 ](custom-auth-ios.html)
* [Cordova 用のカスタム認証の構成 ](custom-auth-cordova.html)
