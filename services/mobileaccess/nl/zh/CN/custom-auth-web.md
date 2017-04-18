---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

{{site.data.keyword.amafull}} 服务已替换为 {{site.data.keyword.appid_full}} 服务。

#针对 {{site.data.keyword.amashort}} Web 应用程序配置定制认证
{: #custom-web}

将定制认证和 {{site.data.keyword.amafull}} 安全功能添加到 Web 应用程序。

## 开始之前
{: #before-you-begin}

开始之前，必须具有：

* Web 应用程序。
* 资源，该资源受 {{site.data.keyword.amashort}} 服务的实例保护，而该服务已配置为使用定制的身份提供者（请参阅[配置定制认证](custom-auth-config-mca.html)）。  
* **TenantID** 值。在 {{site.data.keyword.amashort}}“仪表板”中打开服务。单击**移动选项**按钮。`tenantId`（也称为 `appGUID`）值会显示在**应用程序 GUID/TenantId** 字段中。您将需要此值来初始化授权管理器。
* **域名**。这是在 {{site.data.keyword.amashort}}“仪表板”的**管理**选项卡中**定制**部分的**域名**字段中指定的值。
* 后端应用程序的 URL（**应用程序路径**）。您将需要此值来向后端应用程序的受保护端点发送请求。
* {{site.data.keyword.Bluemix_notm}} **区域**。您可以在**头像**图标 ![“头像”图标](images/face.jpg "“头像”图标") 旁边的头中找到当前 {{site.data.keyword.Bluemix_notm}} 区域。显示的区域值应为以下某个值：`US South`、`United Kingdom` 或 `Sydney`，并对应于 Javascript 代码中需要的 SDK 值：`BMSClient.REGION_US_SOUTH`、`BMSClient.REGION_UK` 或 `BMSClient.REGION_SYDNEY`。您将需要此值来初始化 {{site.data.keyword.amashort}} 客户端。
* 最终重定向的 URI（授权流程完成后）。这是在**管理**选项卡的**定制**部分中输入的 **Web 应用程序重定向 URI** 值。

有关更多信息，请参阅：

* [{{site.data.keyword.amashort}} 入门](getting-started.html)
* [使用定制身份提供者](custom-auth.html)
* [创建定制身份提供者](custom-auth-identity-provider.html)
* [配置 {{site.data.keyword.amashort}} 进行定制认证](custom-auth-config-mca.html)


##配置定制身份提供者
{: #custom-auth-config}

创建定制身份提供者时，必须使用以下结构中的路径，定义 POST 方法：

`/apps/:tenantID/<your-realm-name>/handleChallengeAnswer`

`tenantID` 是 URL 参数，`<your-realm-name>` 是您选择的任何域名。

请求主体将包含 `challengeAnswer` 对象，其内含 `username` 和 `password`。

验证用户之后，此路径一定会返回以下结构的 JSON 对象。

```json
{
	status: "success",
	userIdentity: {
		userName: <user name>,
		displayName: <display name>
		attributes: <additional attributes json>
	}
}
```
{: codeblock}

**注：**`attributes` 为可选字段。

以下代码演示了这种 POST 请求。

```Java
var app = express();
var bodyParser = require('body-parser');
app.use(bodyParser.json());

var users = {
	"John": {
		password: "123",
		displayName: "John Doe"
	}
};

app.post('/apps/:tenantID/customAuthRealm_1/handleChallengeAnswer', function(req, res) {
	console.log ("tenantID " + req.params.tenantID);

	var challengeAnswer = req.body.challengeAnswer;
	console.log ("challengeAnswer " + JSON.stringify(challengeAnswer));

	if (challengeAnswer && users[challengeAnswer.username] && challengeAnswer.password === users[challengeAnswer.username].password) {
		res.json({
			status: "success",
			userIdentity: {
				userName: challengeAnswer.username,
				displayName: users[challengeAnswer.username].displayName
			}
		});
	} else {
		res.json({
			status: "failure"
		});
	}

});
```
{: codeblock}


##配置 {{site.data.keyword.amashort}} 进行定制认证
{: #custom-auth-config-mca}

配置定制身份提供者后，可以在 {{site.data.keyword.amashort}} 仪表板中启用定制认证。

1. 在 {{site.data.keyword.amashort}}“仪表板”中打开服务。
1. 在**管理**选项卡中，将**授权**切换为“开启”。
1. 展开**定制**部分。
1. 输入**域名**和**定制身份提供者 URL**。
1. 输入 **Web 应用程序重定向 URI** 值。这是成功授权后最终重定向的 URI。
1. 单击**保存**。


##使用定制身份提供者实施 {{site.data.keyword.amashort}} 授权流程
{: #custom-auth-flow}

针对每一个 {{site.data.keyword.amashort}} 服务实例会自动创建 `VCAP_SERVICES` 环境变量，该环境变量包含授权流程所需的属性。它包含 JSON 对象，通过单击 {{site.data.keyword.amashort}}“仪表板”中的**服务凭证**选项卡，可以查看该对象。

要请求用户授权，请将浏览器重定向到授权服务器端点。要这样做：

1. 从存储在 `VCAP_SERVICES` 环境变量的服务凭证中，检索授权端点 (`authorizationEndpoint`) 和客户端标识 (`clientId`)。

	`var cfEnv = require("cfenv");`

	`var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;`

	**注：**如果在添加 Web 支持之前，您已向应用程序添加了 {{site.data.keyword.amashort}} 服务，那么可能在服务凭证中没有令牌端点。请改为使用下列 URL，具体取决于 {{site.data.keyword.Bluemix_notm}} 区域：

	美国南部：

	`https://mobileclientaccess.ng.bluemix.net/oauth/v2/authorization`

	伦敦：

	`https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/authorization`

	悉尼：

	`https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/authorization`

2. 使用 `response_type("code")`、`client_id` 和 `redirect_uri` 作为查询参数，构建授权服务器 URI。  

3. 从 Web 应用程序重定向到生成的 URI。

   以下示例从 `VCAP_SERVICES` 变量检索参数，构建 URL，并发送重定向请求。

	```Java
	var cfEnv = require("cfenv");
	app.get("/protected", checkAuthentication, function(req, res, next) {
		res.send("Hello from protected endpoint");
	}
	);

	function checkAuthentication(req, res, next) {
		// Check if user is authenticated
		if (req.session.userIdentity) {
			next()
		} else {
			// If not - redirect to authorization server
			var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;
			var authorizationEndpoint = mcaCredentials.authorizationEndpoint;
			var clientId = mcaCredentials.clientId;
			var redirectUri = "http://some-server/oauth/callback"; // Your web application redirect uri
			var redirectUrl = authorizationEndpoint + "?response_type=code";
			redirectUrl += "&client_id=" + clientId;
			redirectUrl += "&redirect_uri=" + redirectUri;
			res.redirect(redirectUrl);
		}
	}
	```
	{: codeblock}

	请注意，`redirect_uri` 参数代表 Web 应用程序重定向 URI，因此必须与 {{site.data.keyword.amashort}} 仪表板中定义的 URI 一致。  

	`state` 参数可以随请求一起传递。此参数将会传播到定制身份提供者 POST 方法，可以从请求主体 (`req.body.stateId`) 进行访问。  

	重定向到授权端点之后，用户将获取登录表单。在定制身份提供者认证用户的凭证之后，{{site.data.keyword.amashort}} 服务将会调用 Web 应用程序重定向 URI，并提供授权代码作为查询参数。  

	重定向之后，用户会获取登录表单。在定制身份提供者认证用户的凭证之后，{{site.data.keyword.amashort}} 服务将会调用 Web 应用程序重定向 URI，并提供授权代码作为查询参数。

##获取令牌
{: custom-auth-tokens}

下一步是使用之前收到的授权代码获取访问令牌和身份令牌。要这样做：

1. 从存储在 `VCAP_SERVICES` 环境变量的服务凭证中检索 `authorizationEndpoint`、`clientId` 和 `secret`。

	**注：**如果在添加 Web 支持之前，您已向应用程序添加了 {{site.data.keyword.amashort}} 服务，那么可能在服务凭证中没有令牌端点。请改为使用下列 URL，具体取决于 {{site.data.keyword.Bluemix_notm}} 区域：

	美国南部：

	`https://mobileclientaccess.ng.bluemix.net/oauth/v2/token`

	伦敦：

	`https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/token`

	悉尼：

	`https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/token`

2. 使用 `grant_type`、`client_id`、`redirect_uri` 和 `code` 作为表单参数，`clientId` 和 `secret` 作为基本 HTTP 认证凭证，向令牌服务器 URI 发送 POST 请求。

	以下示例中的代码会检索必要的值，并使用 POST 请求发送这些值。

	```Java
	var cfEnv = require("cfenv");
	var base64url = require("base64url");
	app.get("/oauth/callback", function(req, res, next) {
		var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;
		var tokenEndpoint = mcaCredentials.tokenEndpoint;

		var formData = {
			grant_type: "authorization_code",
			client_id: mcaCredentials.clientId,
			redirect_uri: "http://some-server/oauth/callback",   // Your Web application redirect uri
			code: req.query.code
		}

		request.post({
			url: tokenEndpoint,
			formData: formData
		}, function (err, response, body) {
			var parsedBody = JSON.parse(body);

			req.session.accessToken = parsedBody.access_token;
			req.session.idToken = parsedBody.id_token;
			var idTokenComponents = parsedBody.id_token.split("."); // [header, payload, signature]
			var decodedIdentity= base64url.decode(idTokenComponents[1]);
			req.session.userIdentity = JSON.parse(decodedIdentity)["imf.user"];
			res.redirect("/");
		}
		).auth(mcaCredentials.clientId, mcaCredentials.secret);
  	}
	);
	```
	{: codeblock}

	请注意，`redirect_uri` 参数必须与之前授权请求中使用的 `redirect_uri` 相匹配。code 数值应该是在授权请求结束时响应中收到的授权代码。授权代码的有效时间仅为 10 分钟，之后您需要获取新代码。

	响应主体将包含 `access_token` 和 `id_token`，格式为 JWT，请参阅 [JWT Web 站点 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://jwt.io){: new_window}。

	在您收到访问令牌和身份令牌之后，您可以将 Web 会话标记为已认证，并且可以选择持久存储这些令牌


##使用获取的访问和身份令牌
{: #custom-auth-using-token}

身份令牌包含有关用户身份的信息。如果是定制认证，那么该令牌将包含认证时定制身份提供者所返回的所有信息。在 `imf.user` 字段下，`displayName` 字段将包含定制身份提供者返回的 `displayName`，而 `id` 字段将包含 `userName`。定制身份提供者返回的所有其他值都会在 `imf.user` 下的 `attributes` 字段中返回。  

有了访问令牌，就可以与 {{site.data.keyword.amashort}} 授权过滤器保护的资源进行通信（请参阅[保护资源](protecting-resources.html)）。要对受保护资源发出请求，请使用以下结构向请求添加 Authorization 头：

`Authorization=Bearer <accessToken> <idToken>`

####提示：
{: #tips_token}

* `<accessToken>` 和 `<idToken>` 必须以空格分隔。

* 身份令牌是可选的。如果您未提供身份令牌，那么虽然可以访问受保护资源，但是不会收到有关已授权用户的任何信息。
