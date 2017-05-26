---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-26"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# API 网关
{: #openwhisk_apigateway}

OpenWhisk 操作可通过由 API Management 进行管理而受益。

API 网关充当 [Web 操作](webactions.md)的代理，并为这些操作提供更多功能，包括 HTTP 方法路由、客户机标识/私钥、速率限制、CORS、查看 API 使用情况和响应日志，以及定义 API 共享策略。
有关 API 网关功能的更多信息，可以阅读 [API Management 文档](/docs/apis/management/manage_openwhisk_apis.html#manage_openwhisk_apis)

## 使用浏览器通过 OpenWhisk Web 操作创建 API。

使用 API 网关，可以将 OpenWhisk 操作作为 API 公开。定义 API 后，可以应用安全性和速率限制策略，查看 API 使用情况和响应日志，以及定义 API 共享策略。在 OpenWhisk“仪表板”中，单击 [API 选项卡](https://console.ng.bluemix.net/openwhisk/apimanagement)。


## 使用 CLI 通过 OpenWhisk Web 操作创建 API

### OpenWhisk CLI 配置

使用 apihost `wsk property set --apihost openwhisk.ng.bluemix.net` 配置 OpenWhisk CLI。
为了能使用 `wsk api`，CLI 配置文件 `~/.wskprops` 需要包含 Bluemix 访问令牌。
要获取访问令牌，请使用 CLI 命令 `wsk bluemix login`；有关该命令的更多信息，请运行 `wsk bluemix login -h`

**注：**如果该命令在要求单点登录 (SSO) 时出错，说明目前不支持此功能。作为变通方法，请使用 `cf login` 登录 Cloud Foundry CLI，然后将主目录配置文件 `~/.cf/config.json` 中的访问令牌复制到 `~/.wskprops` 文件作为属性 `APIGW_ACCESS_TOKEN="value of AccessToken`。复制访问令牌字符串时，请除去前缀 `Bearer`。

**注：**使用 `wsk api-experimental` 创建的 API 将继续运行一段较短的时间，但您应该开始将 API 迁移到 Web 操作，并使用新的 CLI 命令 `wsk api` 重新配置现有 API。

### 使用 CLI 创建第一个 API

1. 创建具有以下内容的 JavaScript 文件。对于此示例，文件名为“hello.js”。
  ```javascript
  function main({name:name='Serverless API'}) {
      return {payload: `Hello world ${name}`};
  }
  ```
  {: codeblock}
  
2. 通过以下 JavaScript 函数创建 Web 操作。对于此示例，操作名为“hello”。确保添加标志 `--web true`
  
  ```
  wsk action create hello hello.js --web true
  ```
  {: pre}
  ```
  ok: created action hello
  ```
  
3. 创建基本路径为 `/hello`、路径为 `/world`、方法为 `get` 且响应类型为 `json` 的 API
  
  ```
  wsk api create /hello /world get hello --response-type json
  ```
  ```
  ok: created API /hello/world GET for action /_/hello
  https://${APIHOST}:9001/api/21ef035/hello/world
  ```
  这将生成新 URL，用于通过 **GET** HTTP 方法公开 `hello` 操作。
  
4. 通过向该 URL 发送 HTTP 请求来尝试公开 echo 操作。
  
  ```
  $ curl https://${APIHOST}:9001/api/21ef035/hello/world?name=OpenWhisk
  ```
  ```json
  {
  "payload": "Hello world OpenWhisk"
  }
  ```
  调用了 Web 操作 `hello`，返回的 JSON 对象包含通过查询参数发送的 `name` 参数。可以通过简单的查询参数或通过请求主体将参数传递到操作。Web 操作将允许您在没有 OpenWhisk 授权 API 密钥的情况下，以公共方式调用操作。
  
### 完全控制 HTTP 响应
  
  `--response-type` 标志用于控制将由 API 网关代理的 Web 操作的目标 URL。如上文中使用 `--response-type json` 将返回 JSON 格式的完整操作结果，并自动将 Content-Type 头设置为 `application/json`，这样您可以轻松开始使用。 
  
  开始使用后，您希望对 HTTP 响应属性（如 `statusCode`、`headers`）具有完全控制权，并在 `body` 中返回不同的内容类型。为此，可以使用 `--response-type http`，这将通过 `http` 扩展名来配置 Web 操作的目标 URL。

  您可以选择更改操作代码，以符合返回具有 `http` 扩展名的 Web 操作的要求，或者将操作包含在序列中，将其结果传递给新操作，由新操作将结果转换为适合 HTTP 响应的正确格式。您可以在 [Web 操作](webactions.md)文档中阅读有关响应类型和 Web 操作扩展名的更多信息。

  更改 `hello.js` 的代码，以返回 JSON 属性 `body`、`statusCode` 和 `headers`
  ```javascript
  function main({name:name='Serverless API'}) {
      return { 
    body: new Buffer(JSON.stringify({payload:`Hello world ${name}`})).toString('base64'), 
        statusCode:200, 
        headers:{ 'Content-Type': 'application/json'}
      };
  }
  ```
  {: codeblock}
  请注意，body 需要返回的是 `base64` 编码的内容，而不是字符串。
  
  使用已修改的结果更新操作
  ```
  wsk action update hello hello.js --web true
  ```
  {: pre}
  使用 `--response-type http` 更新 API
  ```
  wsk api create /hello /world get hello --response-type http
  ```
  {: pre}
  下面将调用更新后的 API
  ```
  curl https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/hello/world
  ```
  {: pre}
  ```json
  {
  "payload": "Hello world Serverless API"
  }
  ```
  现在您已完全控制 API，可以控制内容（如返回 HTML）或设置状态码，例如“找不到”(404)、“未授权”(401) 或者甚至是“内部错误”(500)。
### 公开多个 Web 操作

假设要为您朋友的读书俱乐部公开一组操作。
您有一系列操作可实现该读书俱乐部的后端：

| 操作 | HTTP 方法 (HTTP method) | 描述 |
| ----------- | ----------- | ------------ |
| getBooks    | GET | 获取书籍详细信息  |
| postBooks   | POST | 添加书籍 |
| putBooks    | PUT | 更新书籍详细信息 |
| deleteBooks | DELETE | 删除书籍 |

为读书俱乐部创建名为 `Book Club` 的 API，并将 `/club` 作为其 HTTP URL 基本路径，将 `books` 作为其资源。
```
wsk api create -n "Book Club" /club /books get getBooks --response-type http
wsk api create /club /books post postBooks              --response-type http
wsk api create /club /books put putBooks                --response-type http
wsk api create /club /books delete deleteBooks          --response-type http
```

请注意，使用基本路径 `/club` 公开的第一个操作将获取名为 `Book Club` 的 API 标签，在 `/club` 下公开的其他所有操作都将与 `Book Club` 相关联。

列出刚才公开的所有操作。

```
wsk api list -f
```
```
ok: APIs
Action: getBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: get
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
Action: postBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: post
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
Action: putBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: put
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
Action: deleteBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: delete
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```

现在，我们来做一件有意思的事情：使用 HTTP **POST** 添加新书 `JavaScript:The Good Parts`
```
curl -X POST -d '{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}' https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```
```
{
  "result": "success"
}
```

使用操作 `getBooks` 通过 HTTP **GET** 获取书籍列表
```
curl -X GET https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```
```
{
  "result": [{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}]
}
```

### 导出配置
将名为 `Book Club` 的 API 导出到文件，我们可以基于此文件将其用作输入来重新创建 API。 
```
wsk api get "Book Club" > club-swagger.json
```

通过先删除公共基本路径下所有公开的 URL 来测试 Swagger 文件。
可以使用基本路径 `/club` 或 API 名称标签“`Book Club`”来删除所有公开的 URL：
```
wsk api delete /club
```
```
ok: deleted API /club
```
### 更改配置

您可以在 OpenWhisk“仪表板”中编辑配置，请单击 [API 选项卡](https://console.ng.bluemix.net/openwhisk/apimanagement)来设置安全性、速率限制和其他功能。

### 导入配置

现在，使用 `club-swagger.json` 文件复原名为 `Book Club` 的 API：
```
wsk api create --config-file club-swagger.json
```
```
ok: created api /books delete for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
ok: created api /books get for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
ok: created api /books post for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
ok: created api /books put for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```

可以验证该 API 是否已重新创建
```
wsk api list /club
```
```
ok: apis
Action                    Verb         API Name        URL
getBooks                   get         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
postBooks                 post         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
putBooks                   put         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
deleteBooks             delete         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```
