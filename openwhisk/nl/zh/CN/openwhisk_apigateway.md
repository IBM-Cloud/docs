---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# API 网关（试验性）
{: #openwhisk_apigateway}

[Web 操作](openwhisk_webactions.html)已发布一般可用性版本。

Web 操作允许您在没有操作的授权 API 密钥的情况下，通过 POST 之外的 HTTP 方法调用操作。

作为用户反馈的结果，Web 操作是选择用于构建能够处理 HTTP 事件的 OpenWhisk 操作的一种编程模型。

大多数 API 网关功能已合并到 Web 操作中，因此 Web 操作允许您处理任何 HTTP 请求并返回 HTTP 响应，同时完全通过 Web 操作进行控制。

修改后的 OpenWhisk API 网关集成将很快可用。它将配置为代理 Web 操作，为其提供 API 网关功能，例如速度限制、OAuth 令牌验证、API 密钥等等。

**注：**使用 `wsk api-experimental` 创建的 API 将继续正常运行，但您应该开始将 API 迁移到 Web 操作。

## OpenWhisk CLI 配置
{: #openwhisk_apigateway_cli}
此试验性功能仅适用于新的 OpenWhisk 认证模型，在新模型中，现在每个名称空间都有关联的唯一认证密钥。
有关如何为特定名称空间设置认证密钥的信息，请遵循[配置 CLI](https://console.ng.bluemix.net/openwhisk/cli) 中的指示信息。

## 公开 OpenWhisk 操作
{: #openwhisk_apigateway_hello}

公开 OpenWhisk 已经预安装的简单操作

```
wsk api-experimental create /hello /echo get /whisk.system/utils/echo
```
{: pre}
```
ok: created api /echo GET for action /whisk.system/utils/echo
https://21ef035.api-gw.mybluemix.net/hello/echo
```
{: screen}
这将生成新 URL，用于通过 **GET** HTTP 方法公开 `echo` 操作。

通过向该 URL 发送 HTTP 请求来尝试公开 echo 操作。
```
curl https://21ef035.api-gw.mybluemix.net/hello/echo?marco=polo
```
{: pre}
这将调用 `echo` 操作，并返回包含所发送参数的 JSON 字符串。
```
{
  "marco":"polo"
}
```
{: screen}

可以通过简单的查询参数或通过请求主体将参数传递到操作。

### 公开多个操作
{: #openwhisk_apigateway_actions}

假设要为您朋友的读书俱乐部公开一组操作。
您有一系列操作可实现该读书俱乐部的后端：

| 操作 | HTTP 方法 | 描述 |
| ----------- | ----------- | ------------ |
| getBooks    | GET | 获取书籍详细信息  |
| postBooks   | POST | 添加书籍 |
| putBooks    | PUT | 更新书籍详细信息 |
| deleteBooks | DELETE | 删除书籍 |

为读书俱乐部创建名为 `Book Club` 的 API，并将 `/club` 作为其 HTTP URL 基本路径，将 `books` 作为其资源。
```
wsk api-experimental create -n "Book Club" /club /books get getBooks
wsk api-experimental create /club /books post postBooks
wsk api-experimental create /club /books put putBooks
wsk api-experimental create /club /books delete deleteBooks
```
{: pre}

请注意，使用基本路径 `/club` 公开的第一个操作将获取名为 `Book Club` 的 API 标签，在 `/club` 下公开的其他所有操作都将与 `Book Club` 相关联。

列出刚才公开的所有操作。

```
wsk api-experimental list
```
{: pre}
```
ok: apis
Action                   Verb          API Name        URL
getBooks                   get         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
postBooks                 post         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
putBooks                   put         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
deleteBooks             delete         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: screen}

现在，我们来做一件有意思的事情：使用 HTTP **POST** 添加新书 `JavaScript:The Good Parts`
```
curl -X POST -d '{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}' https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: pre}
```
{
  "result": "success"
}
```
{: screen}

使用操作 `getBooks` 通过 HTTP **GET** 获取书籍列表
```
curl -X GET https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: pre}
```
{
  "result": [{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}]
}
```

### 导出配置
将名为 `Book Club` 的 API 导出到文件，我们可以基于此文件将其用作输入来重新创建 API。 
```
wsk api-experimental get "Book Club" > club-swagger.json
```
{: pre}

通过先删除公共基本路径下所有公开的 URL 来测试 Swagger 文件。
可以使用基本路径 `/club` 或 API 名称标签“`Book Club`”来删除所有公开的 URL：
```
wsk api-experimental delete /club
```
{: pre}
```
ok: deleted API /club
```
{: screen}

现在，使用 `club-swagger.json` 文件复原名为 `Book Club` 的 API：
```
wsk api-experimental create --config-file club-swagger.json
```
{: pre}
```
ok: created api /books delete for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
ok: created api /books get for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
ok: created api /books post for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
ok: created api /books put for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: screen}

可以验证该 API 是否已重新创建
```
wsk api-experimental list /club
```
{: pre}
```
ok: apis
Action                    Verb         API Name        URL
getBooks                   get         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
postBooks                 post         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
putBooks                   put         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
deleteBooks             delete         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: screen}

- **注**：目前这是试验性功能，是为了让用户有机会及早试用并提出反馈意见。下面是已经收到的反馈意见：
  - 无法定制对跨源资源共享 (CORS) 的 HTTP 访问控制；目前，生成的 API 响应头配置为允许任何 HTTP 动词或源（即 *）。始终会返回以下头：
    - Access-Control-Allow-Origin：*
    - Access-Control-Allow-Headers：Authorization 和 Content-Type
    - Access-Control-Allow-Methods：GET、POST、PUT、DELETE、PATCH、HEAD 和 OPTIONS
  - 请求和响应仅支持内容类型 `application/json`。
  - 没有编程方式可控制来自 OpenWhisk 操作的响应。
  - 所有 OpenWhisk 操作均通过公共访问进行公开，无法配置定制 API 密钥。
  - 不支持路径参数，只支持查询参数和请求主体。
  - 如果创建 API 时未包含 API 名称，那么该 API 的名称将为基本路径，并且无法对其进行更改。
  - 通过输入文件重新创建 API 时，需要先删除该 API。
  - 导出 API 时，会包含 OpenWhisk API 密钥，这是敏感信息，没有模板可用。
