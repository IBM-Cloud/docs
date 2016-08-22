---

copyright:
  year: 2016

---

# 启用 Web 应用程序的 Facebook 认证

*上次更新时间：2016 年 7 月 18 日*
{: .last-updated}

使用 Facebook 在 Web 应用程序上认证用户。

## 开始之前
{: #facebook-auth-android-before}
您必须具有：
* Web 应用程序。 
* 受 {{site.data.keyword.amashort}} 服务保护的 {{site.data.keyword.Bluemix_notm}} 应用程序实例。有关如何创建 {{site.data.keyword.Bluemix_notm}} 后端应用程序的更多信息，请参阅[入门](index.html)。




* 最终重定向的 URI（授权流程完成后）。


## 针对 Web 站点配置 Facebook 应用程序
要在 Web 站点上将 Facebook 用作身份提供者，必须在 Facebook 应用程序上添加并配置 Web 站点平台。

1. 登录到 Facebook 开发人员门户网站 (https://developers.facebook.com)。
2. 打开或创建应用程序。
1. 记录**应用程序标识**和**应用程序私钥**。在 {{site.data.keyword.amashort}} 仪表板中配置 Web 项目以进行 Facebook 认证时需要这些值。
1. 如果不存在 Web 站点平台，请添加一个。
1. 从“产品”列表中，添加或打开 **Facebook 登录**。
1. 在**有效的 OAuth 重定向 URI** 框中输入授权服务器回调端点 URI。在以下的 {{site.data.keyword.amashort}} 仪表板配置步骤中，查找此授权重定向 URI。
2. 保存更改。




# 配置 {{site.data.keyword.amashort}} 进行 Facebook 认证
已拥有 Facebook 应用程序标识和应用程序私钥并且将 Facebook 应用程序配置为向 Web 客户端提供服务后，可以在 {{site.data.keyword.Bluemix_notm}} 仪表板中启用 Facebook 认证。

1. 打开 {{site.data.keyword.Bluemix_notm}} 仪表板。
1. 单击相关应用程序磁贴。这时将装入应用程序。
2. 单击 {{site.data.keyword.amashort}} 服务的磁贴。
1. 单击 **Facebook** 面板中的**配置**按钮。
2. 记录 **Facebook 开发者控制台的 Mobile Client Access 重定向 URI** 文本框中的值。在上述步骤 6 中，您需要将此值添加到 Facebook 开发人员门户网站的 **Facebook 登录**中的**有效的 OAuth 重定向 URI** 框中。
1. 输入 Facebook **应用程序标识**和**应用程序私钥**。
2. 在 **Web 应用程序重定向 URI**中输入重定向 URI。
此值用于在完成授权流程之后可访问重定向 URI，由开发者确定。
3. 单击**保存**。




## 使用 Facebook 作为身份提供者实施 {{site.data.keyword.amashort}} 授权流程

针对每一个 {{site.data.keyword.amashort}} 服务实例会自动创建 `VCAP_SERVICES` 环境变量，该环境变量包含授权流程所需的属性。它包含 JSON 对象，通过单击应用程序左侧导航器的**环境变量**，可以查看该环境变量。

要启动授权过程：

1. 从存储在 `VCAP_SERVICES` 环境变量的服务凭证中，检索授权端点 (`authorizationEndpoint`) 和客户端标识 (`clientId`)。 

    **注：**如果在添加 Web 支持之前您已创建 {{site.data.keyword.amashort}} 服务，那么您可能在服务凭证中没有授权端点。在此情况下，请根据您的 Bluemix 区域，使用以下授权端点：
  
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
    }
  ); 
  
  function checkAuthentication(req, res, next){
  // Check if user is authenticated 
  
    if (req.session.userIdentity){   
       next()  
     } else {   
  // If not - redirect to authorization server   
        var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;   
        var authorizationEndpoint = mcaCredentials.authorizationEndpoint;   
        var clientId = mcaCredentials.clientId;   
        var redirectUri = "http://some-server/oauth/callback"; 
         // Your web application redirect uri   

        var redirectUrl = authorizationEndpoint + "?response_type=code";
        redirectUrl += "&client_id=" + clientId;   
        redirectUrl += "&redirect_uri=" + redirectUri;   
  
        res.redirect(redirectUrl);  
  
      } 
  }
  
 ```

   `redirect_uri` 参数是 URI，用于在使用 Facebook 成功认证或认证失败之后进行重定向。
   

 重定向到授权端点之后，用户将从 Facebook 获取登录表单。在 Facebook 授权用户的凭证之后，{{site.data.keyword.amashort}} 服务将会调用 Web 应用程序重定向 URI，并提供授权代码作为查询参数。  
## 获取令牌

下一步是使用之前收到的授权代码获取访问令牌和身份令牌：

 1.  从存储在 `VCAP_SERVICES` 环境变量的服务凭证中检索令牌 `tokenEndpoint`、`clientId` 和 `secret`。 
 
    **注：**如果在添加 Web 支持之前，您已使用 Mobile Client Access，那么您可能在服务凭证中没有令牌端点。在此情况下，请根据您的 Bluemix 区域，改用以下 URL： 

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
     https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/token
 ```

 1. 使用授权类型 ("authorization_code")、`clientId` 和重定向 URI 作为表单参数，向令牌服务器 URI 发送 post 请求。发送 `clientId` 和 `secret` 作为基本 HTTP 认证凭证。
 
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
      redirect_uri: "http://some-server/oauth/callback",
     // Your web application redirect uri 
      code: req.query.code 
   } 

 
    request.post({ 
        url: tokenEndpoint, 
        formData: formData 
      }, function (err, response, body){ 
        var parsedBody = JSON.parse(body); 
        req.session.accessToken = parsedBody.access_token; 
        req.session.idToken = parsedBody.id_token; 
        var idTokenComponents = parsedBody.id_token.split("."); 
        // [header, payload, signature] 
        var decodedIdentity= base64url(idTokenComponents[1]);
        req.session.userIdentity = JSON.parse(decodedIdentity)["imf.user"]; 
        res.redirect("/"); 
        }
   ).auth(mcaCredentials.clientId, mcaCredentials.secret); 

   }
  ); 
   
  ```
 
 请注意，`redirect_uri` 参数必须与之前授权请求中使用的 `redirect_uri` 相匹配。
`code` 参数值应该是从授权请求的响应中收到的授权代码。授权代码的有效时间仅为 10 分钟，之后必须检索新代码。


响应主体将包含访问代码和令牌标识，格式为 JWT (https://jwt.io/)。

在您获得访问令牌并收到身份令牌之后，您可以将 Web 会话标记为已认证，并可选择性地持久存储这些令牌。  

##使用获取的访问和身份令牌 

身份令牌包含有关用户身份的信息。如果是 Facebook 认证，那么该令牌将包含用户同意共享的所有信息，如全名、年龄组、个人档案照片的 URL 等。  

有了访问令牌，可以与 {{site.data.keyword.amashort}} 授权过滤器保护的资源进行通信，请参阅[保护资源](protecting-resources.html)。


要对受保护资源发出请求，请使用以下结构，向请求添加 Authorization 头： 

`Authorization=Bearer <accessToken> <idToken>`

**注：** 

* `accessToken` 和 `idToken` 必须以空格分隔。

* `idToken` 是可选的。如果您未提供身份令牌，那么虽然可以访问受保护资源，但是不会收到有关已授权用户的任何信息。 
 



