---

copyright:
  years: 2015, 2016

---

# 创建定制身份提供者
{: #custom-create}
要创建定制身份提供者，请开发用于公开 RESTful API 的 Web 应用程序：

```
POST <base_url>/apps/<tenant_id>/<realm_name>/<request_type>
```

* `base_path`：指定定制身份提供者 Web 应用程序的基本 URL。基本 URL 是要在 {{site.data.keyword.amashort}}“仪表板”中注册的 URL。
* `tenant_id`：指定租户的唯一标识。{{site.data.keyword.amashort}} 调用此 API 时，会始终提供{{site.data.keyword.Bluemix}}应用程序 GUID (`applicationGUID`)。
* `realm_name`：指定在 {{site.data.keyword.amashort}}“仪表板”中定义的定制域名。
* `request_type`：指定下列其中一项：
	* `startAuthorization`：指定认证过程的第一步。定制身份提供者必须使用“challenge”、“success”或“failure”状态进行响应。
	* `handleChallengeAnswer`：处理来自移动客户端的认证质询响应。

## `startAuthorization` API
{: #custom-startauthorization}

`POST <base_url>/apps/<tenant_id>/<realm_name>/startAuthorization`

`startAuthorization` API 用作认证过程的第一步。定制身份提供者必须使用“challenge”、“success”或“failure”状态进行响应。

为了使认证过程实现最大的灵活性，定制身份提供者有权访问请求主体中移动客户端发送的所有 HTTP 头。提供的头的格式如下：

```JavaScript
{
    "headers" : {
    	"header1": "value1",  
    	"header2" : "value2"
    }
}
```

定制身份提供者可能会使用认证质询进行响应，也可能会使用直接的 success 或 failure 进行响应。响应 HTTP 状态必须为 `HTTP 200`，并且响应 JSON 必须包含以下属性：

* `status`：指定请求的 `success`、`challenge` 或 `failure`。
* `stateId`（可选）：指定随机生成的字符串标识，以标识移动客户端的认证会话。如果定制身份提供者未存储任何状态，那么可以省略此属性。
* `challenge`：指定表示要发送回移动客户端的认证质询的 JSON 对象。仅当 status 设置为 `challenge` 时，才会发送此属性。
* `userIdentity`：指定表示用户身份的 JSON 对象。用户身份由 `userName`、`displayName` 等属性组成。有关更多信息，请参阅[用户身份对象](#custom-user-identity)。仅当 status 设置为 `success` 时，才会将此属性发送到移动客户端。

例如：


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

`handleChallengeAnswer` API 处理来自移动客户端的认证质询响应。与 `startAuthorization` API 一样，`handleChallengeAnswer` API 也是使用 `challenge`、`success` 或 `failure` 状态进行响应。

与 `startAuthorization` 请求类似，定制身份提供者有权访问请求主体中移动客户端发送的所有 HTTP 头。除了移动客户端请求头外，`handleChallengeAnswer` 请求的主体还包含 `stateId` 和 `challengeAnswer` 属性。

### `handleChallengeAnswer` 请求主体示例
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

来自 `handleChallengeAnswer` API 的响应必须具有与 `startAuthorization` API 的响应相同的结构。

## 用户身份对象
{: #custom-user-identity}

对成功认证请求的响应必须包含用户身份对象以及以下属性：
* `userName`：指定唯一的用户名。
* `displayName`：指定用户的显示名称。
* `attributes`（可选）：指定包含定制用户属性的 JSON 对象。

### 用户身份对象示例
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

用户身份对象由 {{site.data.keyword.amashort}} 服务用于生成标识令牌，此令牌会作为 Authorization 头的一部分发送到移动客户端。成功认证后，移动客户端即对用户身份对象具有完全访问权。

## 安全注意事项
{: #custom-security}

从 {{site.data.keyword.amashort}} 服务到定制身份提供者的每个请求都包含一个 Authorization 头，这样定制身份提供者就能验证该请求是否来自授权的源。请考虑通过在定制身份提供者中安装 {{site.data.keyword.amashort}} 服务器 SDK 来验证 Authorization 头，不过这并不是严格必需的。要使用此 SDK，定制身份提供者应用程序必须使用 Node.js 或 Liberty for Java&trade;&trade; 来实现，并在 {{site.data.keyword.Bluemix_notm}} 上运行。

Authorization 头包含有关触发了认证过程的移动客户端和移动应用程序的信息。可以使用安全上下文来检索此数据。有关更多信息，请参阅[保护资源](protecting-resources.html)

## 定制身份提供者的样本实现
{: #custom-sample}
开发定制身份提供者时，可以将定制身份提供者的以下任何 Node.js 样本实现用作参考。请从 GitHub 存储库下载完整应用程序代码。

* [简单样本](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)
* [高级样本](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management)

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

## 后续步骤
{: #next-steps}
* [配置 {{site.data.keyword.amashort}} 进行定制认证](custom-auth-config-mca.html)
* [针对 Android 配置定制认证](custom-auth-android.html)
* [针对 iOS 配置定制认证](custom-auth-ios.html)
* [针对 Cordova 配置定制认证](custom-auth-cordova.html)
