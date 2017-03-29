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

# Web 操作
{: #openwhisk_webactions}

Web 操作是经过注释的 OpenWhisk 操作，可快速支持您构建基于 Web 的应用程序。这将允许您对 Web 应用程序可以匿名访问的后端逻辑进行编程，而无需 OpenWhisk 认证密钥。由操作开发者来决定实现其自己所需的认证和授权（即 OAuth 流）。
{: shortdesc}

Web 操作激活将与创建操作的用户相关联。此操作会将操作激活的成本从调用者转移到操作所有者。

我们来执行以下 JavaScript 操作 `hello.js`：
```javascript
function main({name}) {
  var msg = 'you did not tell me who you are.';
  if (name) {
    msg = `hello ${name}!`
  }
  return {body: `<html><body><h3>${msg}</h3></body></html>`}
}
```
{: codeblock}

您可使用注释 `web-export` 在包 `demo` 中为名称空间 `guest` 创建 *Web 操作* `hello`：
```
wsk package create demo
```
{: pre}
```
wsk action create /guest/demo/hello hello.js -a web-export true
```
{: pre}

`web-export` 注释允许通过新的 REST 接口将该操作作为 Web 操作进行访问。构造的 URL 如下所示：`https://openwhisk.ng.bluemix.net/api/v1/web/{QUALIFIED ACTION NAME}.{EXT}`。操作的标准名称由三个部分构成：名称空间、包名和操作名称。

*操作的标准名称必须包含其包名，如果操作不在指定的包中，那么包名为“default”。*

例如，`guest/demo/hello`。URI 的最后一个部分是`扩展名`，通常为 `.http`，但也允许使用其他值，如后文所述。Web 操作 API 路径可与 `curl` 或 `wget` 配合使用，而不使用 API 密钥。甚至可以直接在浏览器中进行输入。

尝试在 Web 浏览器中打开 [https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.http?name=Jane](https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.http?name=Jane)。或者，尝试通过 `curl` 调用该操作：
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.http?name=Jane
```
{: pre}

下面是执行 HTTP 重定向的 Web 操作的示例：
```javascript
function main() {
  return { 
    headers: { location: 'http://openwhisk.org' },
    statusCode: 302
  }
}
```
{: codeblock}  

或者，设置 cookie：
```javascript
function main() {
  return { 
    headers: { 
      'Set-Cookie': 'UserID=Jane; Max-Age=3600; Version=',
      'Content-Type': 'text/html'
    }, 
    statusCode: 200,
    body: '<html><body><h3>hello</h3></body></html>' }
}
```
{: codeblock}

或者，返回 `image/png`：
```javascript
function main() {
    let png = <base 64 encoded string>
    return { headers: { 'Content-Type': 'image/png' },
             statusCode: 200,
             body: png };
}
```
{: codeblock}

Or returns `application/json`:
```javascript
function main(params) { 
    return {
        statusCode: 200,
        headers: { 'Content-Type': 'application/json' },
        body: new Buffer(JSON.stringify(params)).toString('base64'),
    };
}
```
{: codeblock}

It is important to be aware of the [响应大小限制](./openwhisk_reference.html)很重要，因为超过预定义系统限制的响应将失败。例如，大对象不应通过 OpenWhisk 内嵌发送，而是应转移到对象存储。

## 使用操作处理 HTTP 请求
{: #openwhisk_webactions_http}

不属于 Web 操作的 OpenWhisk 操作不仅需要认证，而且必须使用 JSON 对象进行响应。相反，Web 操作可以在无认证的情况下进行调用，也可用于实现通过不同类型的 *headers*、*statusCode* 和 *body* 内容进行响应的 HTTP 处理程序。Web 操作仍必须返回 JSON 对象，但如果其结果包含以下一个或多个项作为顶级 JSON 属性，那么 OpenWhisk 系统（即`控制器`）将以不同的方式处理 Web 操作：

- `headers`：JSON 对象，其中键是头名称，值是这些头的字符串值（缺省情况下没有 headers）。
- `statusCode`：有效 HTTP 状态码（缺省值为 200 OK）。
- `body`：字符串，为明文或基本 64 位编码的字符串（对于二进制数据）。

控制器在终止请求/响应时，会将操作指定的头（如有）传递到 HTTP 客户机。与此类似，控制器将使用给定状态码（如果存在）进行响应。最后，主体会作为响应主体进行传递。除非在操作结果的 `headers` 中声明 `content-type 头`，否则主体会视为字符串进行传递（或者直接导致出错）。定义了 `content-type` 后，控制器将确定响应是二进制数据还是明文，然后根据需要使用基本 64 位解码器对字符串进行解码。如果主体未能正确解码，那么会向调用者返回错误。

*注*：JSON 对象或数组会视为二进制数据，并且必须进行基本 64 位编码，如上例中所示。

## HTTP 上下文

所有 Web 操作在调用时都会接收其他 HTTP 请求详细信息以作为操作输入自变量的参数。这些参数包括：

- `__ow_method`（类型：字符串）：请求的 HTTP 方法。
- `__ow_headers`（类型：字符串到字符串的映射）：请求头。
- `__ow_path`（类型：字符串）：请求的未匹配路径（使用操作扩展名后，匹配会停止）。
- `__ow_user`（类型：字符串）：用于标识经 OpenWhisk 认证的主体的名称空间
- `__ow_body`（类型：字符串）：请求主体实体，内容为二进制时为基本 64 位编码字符串，其他情况均为明文字符串
- `__ow_query`（类型：字符串）：请求中的查询参数（以未解析字符串的形式提供）

请求不得覆盖以上指定的任何 `__ow_` 参数；加以覆盖会导致请求失败，并返回状态“400 错误请求”。

仅当 Web 操作[注释为需要认证](./openwhisk_annotations.html#openwhisk_annotations_webactions)并允许 Web 操作实现其自己的授权策略时，才会显示 `__ow_user`。仅当 Web 操作选择处理[“原始”HTTP 请求](#raw-http-handling)时，`__ow_query` 才可用。这是包含从 URI 中解析出的查询参数的字符串（用 `&` 分隔）。处理“原始”HTTP 请求时或者 HTTP 请求实体不是 JSON 对象或表单数据时，会显示 `__ow_body` 属性。在其他情况下，Web 操作接收查询和主体参数作为操作自变量中的第一类属性，其中主体参数优先于查询参数，而查询参数又优先于操作和包参数。

## 其他功能

Web 操作额外提供了一些功能，包括：

- `内容扩展名`：请求必须将其所需的内容类型指定为 `.json`、`.html`、`.http`、`.svg` 或 `.text` 中的一种。为此，请在 URI 中添加操作名称的扩展名，以便将操作 `/guest/demo/hello` 引用为 `/guest/demo/hello.http`（举例而言）来接收返回的 HTTP 响应。为了方便起见，检测不到扩展名时将采用 `.http` 扩展名。
- `从结果预测字段`：操作名称后跟的路径用于预测响应的一个或多个级别。例如，
`/guest/demo/hello.html/body`。这允许返回字典 `{body: "..." }` 的操作预测 `body` 属性，并直接返回其字符串值。预测的路径将采用绝对路径模式（如在 XPath 中一样）。
- `查询和主体参数作为输入`：操作会接收查询参数以及请求主体中的参数。合并参数的优先顺序如下：包参数、操作参数、查询参数、主体参数；若发生重叠，这些参数都会覆盖先前的值。例如，`/guest/demo/hello.http?name=Jane` 会将自变量 `{name: "Jane"}` 传递到操作。
- `表单数据`：除了标准 `application/json` 外，Web 操作还可以从数据 `application/x-www-form-urlencoded data` 接收 URL 编码的数据作为输入。
- `通过多个 HTTP 动词激活`：Web 操作可通过 HTTP 方法 `GET`、`POST`、`PUT`、`PATCH` 和 `DELETE` 中的任一种方法以及 `HEAD` 和 `OPTIONS` 进行调用。
- `非 JSON 主体和原始 HTTP 实体处理`：Web 操作可接受非 JSON 对象的 HTTP 请求主体，并可选择始终接收此类值作为不透明值（当不是二进制时为明文，其他情况均为基本 64 位编码的字符串）。

以下示例简要概括了在 Web 操作中可如何使用这些功能。考虑具有以下主体的操作 `/guest/demo/hello`：
```javascript
function main(params) { 
    return { response: params };
}
```

此操作在作为 Web 操作调用时，您可以通过从结果对不同的路径投影来变更该 Web 操作的响应。
例如，要返回整个对象，并查看操作接收的自变量：

```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json
```
{: pre}
```json
{
  "response": {
    "__ow_method": "get",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

查询参数为：
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json?name=Jane
```
{: pre}
```json
{
  "response": {
    "name": "Jane",
    "__ow_method": "get",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

或表单数据：
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json -d "name":"Jane"
```
{: pre}
```json
{
  "response": {
    "name": "Jane",
    "__ow_method": "post",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "10",      
      "content-type": "application/x-www-form-urlencoded",      
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

或 JSON 对象：
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json -H 'Content-Type: application/json' -d '{"name":"Jane"}'
```
{: pre}
```json
{
  "response": {
    "name": "Jane",
    "__ow_method": "post",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "15",      
      "content-type": "application/json",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

以及仅对名称（作为文本）进行投影：
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.text/response/name?name=Jane
```
{: pre}
```
Jane
```

在上述显示的内容中，为了方便起见，查询参数、表单数据和 JSON 对象体实体均视为字典，其值可以直接作为操作输入属性进行访问。但对于选择以更直接的方式处理 HTTP 请求实体的 Web 操作，或者当 Web 操作接收到非 JSON 对象的实体时，情况就不是这样了。

下面是将“文本”content-type 用于上述相同示例的示例：
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json -H 'Content-Type: text/plain' -d "Jane"
```
{: pre}
```json
{
  "response": {
    "__ow_method": "post",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "4",      
      "content-type": "text/plain",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": "",
    "__ow_body": "Jane"
  }
}
```


## 内容扩展名
{: #openwhisk_webactions_extensions}

调有 Web 操作时，内容扩展名通常是必需的；缺少扩展名时将采用 `.http` 为缺省值。`.json` 和 `.http` 扩展名无需投影路径。`.html`、`.svg` 和 `.text` 扩展名则需要投影路径，但是为了方便起见，将采用缺省路径来与扩展名相匹配。所以，要调用 Web 操作并接收 `.html` 响应，该操作必须使用包含顶级属性 `html` 的 JSON 对象进行响应（或者响应必须为显式提供的路径）。换言之，`/guest/demo/hello.html` 相当于显式预测 `html` 属性，如 `/guest/demo/hello.html/html` 中所示。操作的标准名称必须包含其包名，如果操作不在指定的包中，那么包名为 `default`。


## 受保护的参数
{: #openwhisk_webactions_protected}

操作参数也可能受到保护并且被视为不可改变。要最终完成参数并使操作可通过 Web 访问，必须将 `final` 和 `web-export` 这两个[注释](openwhisk_annotations.html)附加到操作，这两个注释都必须设置为 `true` 才能生效。重新访问早先的操作部署，我们将按如下所示添加注释：

```
wsk action create /guest/demo/hello hello.js \
      --parameter name Jane \
      --annotation final true \
      --annotation web-export true
```
{: pre}

这些更改的结果是 `name` 绑定到 `Jane`，并且因为是最终注释，所以查询或主体参数都无法将其覆盖。这将保护操作不被意外或有意尝试更改此值的查询或主体参数覆盖。 

## 禁用 Web 操作
{: #openwhisk_webactions_disable}

要禁止通过新的 API (`https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/web/`) 调用 Web 操作，只需除去该注释或将其设置为 `false` 即可。

```
wsk action update /guest/demo/hello hello.js \
      --annotation web-export false
```

## 原始 HTTP 处理
{: #raw-http-handling}

Web 操作可选择直接解释和处理入局 HTTP 主体，而不将 JSON 对象提升为操作输入可用的第一类属性（例如，`args.name`，而不是解析 `args.__ow_query`）。通过 `raw-http` [注释](openwhisk_annotations.html)可执行此操作。使用上文所示的相同示例，但现在作为将 `name` 同时接收为查询参数和 HTTP 请求主体中 JSON 值的“原始”HTTP Web 操作：
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json?name=Jane -X POST -H "Content-Type: application/json" -d '{"name":"Jane"}'
```
{: pre}
```json
{
    "response": {
    "__ow_method": "post",
    "__ow_query": "name=Jane",
    "__ow_body": "eyJuYW1lIjoiSmFuZSJ9",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "15",
      "content-type": "application/json",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"      
    },
    "__ow_path": ""
  }
}
```

请注意，在本例中，因为 JSON 内容被视为二进制值，因此会进行基本 64 位编码。操作必须对此值进行基本 64 位解码和 JSON 解析，才可恢复 JSON 对象。OpenWhisk 使用 [Spray](https://github.com/spray/spray) 框架来[确定](https://github.com/spray/spray/blob/master/spray-http/src/main/scala/spray/http/MediaType.scala#L282)哪些内容类型是二进制，哪些是明文。


### 启用原始 HTTP 处理

原始 HTTP Web 操作可通过值为 `true` 的 `raw-http` [注释](openwhisk_annotations.html)来启用。

```
wsk action create /guest/demo/hello hello.js \
      --annotation web-export true
      --annotation raw-http true
```
{: pre}

**注：**由于 `raw-http` 隐含了 `web-export`，因此我们计划改进 CLI，以便未来更方便地添加（和除去）这些注释。


### 禁用原始 HTTP 处理

禁用原始 HTTP 可通过将 `raw-http` [注释](openwhisk_annotations.html)值设置为 `false` 来完成。

```
wsk update create /guest/demo/hello hello.js \
      --annotation web-export true
      --annotation raw-http false
```
{: pre}

**注：**单个操作的所有注释必须同时进行设置，可在创建操作时设置，也可在更新操作时设置。这是由于对 API 和 CLI 的当前限制造成的。如果不这样做，将导致除去先前附加的任何注释。


## 错误处理
{: #openwhisk_webactions_errors}

OpenWhisk 操作失败时，有两种不同的失败方式。第一种称为*应用程序错误*，类似于捕获的异常：操作返回包含顶级 `error` 属性的 JSON 对象。第二种是*开发者错误*，当操作以灾难性的方式失败并且未生成响应时发生（这类似于未捕获的异常）。对于 Web 操作，控制器按如下所示处理应用程序错误：

- 将忽略任何指定的路径预测，控制器将改为预测 `error` 属性。
- 控制器将操作扩展名隐含的内容处理应用于 `error` 属性的值。

开发者应该了解可如何使用 Web 操作，并相应地生成错误响应。例如，与 `.http` 扩展名配合使用的 Web 操作应该返回 HTTP 响应，例如：`{error: { statusCode: 400 }`。若未能这样做，扩展名中隐含的内容类型与错误响应中的操作内容类型将不匹配。对于属于序列的 Web 操作必须格外注意，以便构成序列的组件可以在需要时生成充分的错误。

