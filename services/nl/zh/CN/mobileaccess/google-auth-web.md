---

copyright:
  year: 2016

---

# 启用 Web 应用程序的 Google 认证
{: #google-auth-web}

上次更新时间：2016 年 7 月 18 日
{: .last-updated}

使用 Google 登录在 Web 应用程序上认证用户。添加 {{site.data.keyword.amashort}} 安全功能。 


## 开始之前
{: #before-you-begin}

您必须具有：
* Web 应用程序。
* 受 {{site.data.keyword.amashort}} 服务保护的 {{site.data.keyword.Bluemix_notm}} 应用程序实例。有关如何创建 {{site.data.keyword.Bluemix_notm}} 后端应用程序的更多信息，请参阅[入门](index.html)。




* 最终重定向的 URI（授权流程完成后）。



## 针对 Web 站点配置 Google 应用程序
要开始将 Google 用作身份提供者，请在 [Google 开发者控制台](https://console.developers.google.com)中创建项目。创建项目的步骤之一是获取 **Google 客户端标识**和**私钥**。Google 客户端标识和私钥是 Google 认证针对您的应用程序使用的唯一标识，设置 {{site.data.keyword.amashort}} 仪表板时需要这些标识。


1. 在 Google 开发者控制台中打开 Google 应用程序。 
3. 添加 Google+ API。 
3. 使用 OAuth 创建凭证。在应用程序类型中选择 Web 应用程序。在“授权重定向 URI”框中，输入 {{site.data.keyword.amashort}} 重定向 URI。
{{site.data.keyword.amashort}} 重定向授权 URI 可以从 {{site.data.keyword.amashort}} 仪表板的 Google 配置屏幕中获取（请参阅以下步骤）。 
6. 保存更改。记录 Google 客户端标识和应用程序私钥。


## 配置 {{site.data.keyword.amashort}} 进行 Google 认证
在您已经有 Google 应用程序标识和私钥之后，可以在 {{site.data.keyword.amashort}} 仪表板中启用 Google 认证。

1. 在 {{site.data.keyword.Bluemix_notm}}“仪表板”中打开应用程序。
1. 单击 {{site.data.keyword.amashort}} 磁贴。这将装入 {{site.data.keyword.amashort}}“仪表板”。
1. 单击 Google 面板上的按钮。
1. 在**针对 Web 配置**部分中：   
    * 记录 **Google 开发者控制台的 Mobile Client Access 重定向 URI** 文本框中的值。在
步骤 3 中，您需要将此值添加到 **Google 开发人员门户网站**的 **
客户端标识中 Web 应用程序的限制**下的**授权重定向 URI** 框中。
    * 输入 **Google 客户端标识**和**客户端私钥**。
    * 在 **Web 应用程序重定向 URI**中输入重定向 URI。
此值用于在完成授权流程之后可访问重定向 URI，由开发者确定。
1. 单击**保存**。


## 使用 Google 作为身份提供者实施 {{site.data.keyword.amashort}} 授权流程

针对每一个 {{site.data.keyword.amashort}} 服务实例会自动创建 `VCAP_SERVICES` 环境变量，该环境变量包含授权流程所需的属性。它包含 JSON 对象，通过单击应用程序左侧导航器的**环境变量**，可以查看该环境变量。

要启动授权过程：

1. 从存储在 `VCAP_SERVICES` 环境变量的服务凭证中，检索授权端点 (`authorizationEndpoint`) 和客户端标识 (`clientId`)。 

    **注：**如果在添加 Web 支持之前您已创建
{{site.data.keyword.amashort}} 服务，那么可能在服务凭证中没有授权端点。在此情况下，请根据您的 Bluemix 区
域，使用以下授权端点：


 	美国南部： 
 	```
 	  https://mobileclientaccess.ng.bluemix.net/oauth/v2/authorization
  ```
 	伦敦：
```
 	https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/authorization
  	```
  	悉尼：
  	```
  	https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/authorization
  	```
2. 使用 `response_type("code")`、`client_id` 和 `redirect_uri` 作为查询参数，构建授权服务器 URI。
3. 从 Web 应用程序重定向到生成的 URI。
  
以下示例从 `VCAP_SERVICES` 变量检索参数，构建 URL，并发送重定向请求。
  
```Java
 var cfEnv = require("cfenv"); 
 app.get("/protected", checkAuthentication, function(req, res, next){ 
 	res.send("Hello from protected endpoint"); 
 }); 

 app.get("/protected", checkAuthentication, function(req, res, next){ 
 	res.send("Hello from protected endpoint"); 
 	function checkAuthentication(req, res, next){ 

	// Check if user is authenticated 
 	if (req.session.userIdentity){ 
		next() 
	} else { 
		// If not - redirect to authorization server 
		var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials; 
		var authorizationEndpoint = mcaCredentials.authorizationEndpoint; 
		var clientId = mcaCredentials.clientId; 
		var redirectUri = "http://some-server/oauth/callback"; // Your web application redirect URI 
		var redirectUrl = authorizationEndpoint + "?response_type=code";
		redirectUrl += "&client_id=" + clientId; 
		redirectUrl += "&redirect_uri=" + redirectUri; 
		res.redirect(redirectUrl); 
	} 
} 
```

请注意，`redirect_uri` 参数代表 Web 应用程序重定向 URI，必须等于 {{site.data.keyword.amashort}} 仪表板中定义的 URI。重定向到授权端点之后，用户将从 Google 获取登录表单。
在用户授予使用 Google 身份登录的许可权之后，{{site.data.keyword.amashort}} 服务将会通
过提供授权代码作为查询参数来调
用 Web 应用程序重定向 URI。

## 获取令牌
下一步是使用之前收到的授权代码获取访问令牌和身份令牌。 

1. 从存储在 `VCAP_SERVICES` 环境变量的服务凭证中检索令牌
`tokenEndpoint`、`clientId` 和 `secret`。 
  
    **注：**如果在添加 Web 支持之前您已创建
{{site.data.keyword.amashort}} 服务，那么可能在服务凭证中没有授权端点。在此情况下，请根据您的 Bluemix 区
域，使用以下授权端点：
 
 	美国南部： 
 	```
 	     https://mobileclientaccess.ng.bluemix.net/oauth/v2/token
 ```
 	伦敦：
```
  	     https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/token
 ```
   	悉尼：
  	```
   	https:// mobileclientaccess.au-syd.bluemix.net/oauth/v2/token 
  	```

2. 使用 grant_type ("authorization_code")、client_id、redirect_uri 和 code 作为表单参数，向令牌服务器 URI 发送 post 请求。发送 `clientId` 和 `clientSecret` 作为基本 HTTP 认证凭证。
 
以下代码会检索必要的值，并使用 post 请求发送这些值。
    
```Java    
  var cfEnv = require("cfenv");
  var base64url = require("base64url ");
  var request = require('request');

   app.get("/oauth/callback", function(req, res, next){ 
	var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials; 
	var tokenEndpoint = mcaCredentials.tokenEndpoint; 
	var formData = { 
		grant_type: "authorization_code", 
		client_id: mcaCredentials.clientId, 
		redirect_uri: "http://some-server/oauth/callback",// Your web application redirect uri 
		code: req.query.code 
	} 

	request.post({ 
		url: tokenEndpoint, 
		formData: formData 
		}, function (err, response, body){ 
			var parsedBody = JSON.parse(body); 
			req.session.accessToken = parsedBody.access_token; 
			req.session.idToken = parsedBody.id_token; 
			var idTokenComponents = parsedBody.id_token.split("."); // [header, payload, signature] 
			var decodedIdentity= base64url(idTokenComponents[1]);
			req.session.userIdentity = JSON.parse(decodedIdentity)["imf.user"]; 
			res.redirect("/"); 
			}
	).auth(mcaCredentials.clientId, mcaCredentials.secret); 
  }
); 
```

`redirect_uri` 参数是 URI，用于在使用 Google+ 成功认证或认证失败之后进行重定向，且必须与步骤 1 中的 `redirect_uri` 匹配。  
   
请确保在 10 分钟内发送此 POST 请求，因为随后授权代码将到期。
10 分钟之后，需要新代码。

POST 响应主体将包含以 Base64 编码的 `access_token` 和
`id_token`。

在您收到访问令牌和身份令牌之后，您可以将 Web 会话标记为已认证，并可选择性地持久存储这些
令牌。  


##使用获取的访问和身份令牌 

身份令牌包含有关用户身份的信息。对于 Google 认证，该令牌将包含用户同意共享的所有信息，如全名、个
人档案照片的 URL 等。  

有了访问令牌，就可以与受 {{site.data.keyword.amashort}} 授权过滤器保护
的资源进行通信。请阅读有关[保护资源](protecting-resources.html)的内容。

要对受保护资源发出请求，请使用以下结构向请求添加 Authorization 头： 

`Authorization=Bearer <accessToken> <idToken>`

####提示：
{: tips} 

* `accessToken` 和 `idToken` 必须以空格分隔。

* `idToken` 是可选的。如果您未提供身份令牌，那么虽然可以访问受保护资源，但
是不会收到有关已授权用户的任何信息。 



