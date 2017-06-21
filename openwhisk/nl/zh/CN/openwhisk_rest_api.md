---

copyright:
  years: 2017
lastupdated: "2017-05-04"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 使用 OpenWhisk REST API
{: #openwhisk_rest_api}

启用了 OpenWhisk 环境后，可以通过 REST API 调用将 OpenWhisk 与 Web 应用程序或移动应用程序配合使用。

有关用于操作、激活、包、规则和触发器的 API 的更多详细信息，请参阅 [OpenWhisk API 文档](http://petstore.swagger.io/?url=https://raw.githubusercontent.com/openwhisk/openwhisk/master/core/controller/src/main/resources/apiv1swagger.json)。


通过 REST API，可以使用系统中的所有功能。操作、触发器、规则、包、激活和名称空间具有集合和实体端点。

以下是集合端点：
- `https://{APIHOST}/api/v1/namespaces`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/actions`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/triggers`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/rules`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/packages`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/activations`

`{APIHOST}` 是 OpenWhisk API 主机名（例如，openwhisk.ng.bluemix.net、172.17.0.1、192.168.99.100、192.168.33.13 等）。对于 `{namespace}`，可以使用字符 `_` 来指定用户的 *缺省名称空间*。

您可以在集合端点上执行 GET 请求，以访存集合中的实体列表。

每一个实体类型都具有实体端点：
- `https://{APIHOST}/api/v1/namespaces/{namespace}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/actions/[{packageName}/]{actionName}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/triggers/{triggerName}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/rules/{ruleName}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/packages/{packageName}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/activations/{activationName}`

名称空间和激活端点仅支持 GET 请求。操作、触发器、规则和包端点支持 GET、PUT 和 DELETE 请求。操作、触发器和规则的端点还支持 POST 请求，其用于调用操作和触发器，以及启用或禁用规则。 

所有 API 都通过 HTTP 基本认证进行保护。可以使用 [wskadmin](../tools/admin/wskadmin) 工具来生成新的名称空间和认证。基本认证凭证位于 `~/.wskprops` 文件的 `AUTH` 属性中，以冒号分隔。您还可以使用 CLI 运行 `wsk property get --auth` 来检索这些凭证。


以下示例使用 [cURL](https://curl.haxx.se) 命令工具来获取 `whisk.system` 名称空间中所有包的列表：

```bash
curl -u USERNAME:PASSWORD https://openwhisk.ng.bluemix.net/api/v1/namespaces/whisk.system/packages
```
{: pre}

```json
  [
      {
    "name": "slack",
    "binding": false,
    "publish": true,
    "annotations": [
      {
        "key": "description",
        "value": "Package that contains actions to interact with the Slack messaging service"
      }
    ],
    "version": "0.0.1",
    "namespace": "whisk.system"
  }
]
```

在此示例中，认证是使用 `-u` 标志传递的，还可以将此值作为 URL 的一部分传递，例如 `https://$AUTH@{APIHOST}`

OpenWhisk API 支持 Web 客户端的请求-响应调用。OpenWhisk 使用 Cross-Origin Resource Sharing 头来响应 `OPTIONS` 请求。目前，允许所有源（即 Access-Control-Allow-Origin 为 "`*`"）且 Access-Control-Allow-Headers 会产生 Authorization 和 Content-Type。

**注意：**由于 OpenWhisk 目前仅支持每个名称空间一个密钥，因此建议除了简单的试验之外，不要使用 CORS。请使用 [Web 操作](webactions.md)或 [API 网关](apigateway.md)向公众公开操作，但不要将 OpenWhisk 授权密钥用于需要 CORS 的客户机应用程序。

## 使用 CLI 详细方式
{: #openwhisk_rest_api_cli_v}
OpenWhisk CLI 是 OpenWhisk REST API 的界面。可以通过 `-v` 标志以详细方式运行 CLI，这将显示有关 HTTP 请求和响应的所有信息。

下面将尝试获取当前用户的名称空间值。
```
wsk namespace list -v
```
{: pre}
```
REQUEST:
[GET]	https://openwhisk.ng.bluemix.net/api/v1/namespaces
Req Headers
{
  "Authorization": [
    "Basic XXXYYYY"
  ]
}
RESPONSE:Got response with code 200
Resp Headers
{
  "Content-Type": [
    "application/json; charset=UTF-8"
  ]
}
Response body size is 28 bytes
Response body received:
["john@example.com_dev"]
```

如您所见，显示的信息提供了 HTTP 请求的属性，它将使用基本授权头 `Basic XXXYYYY` 对 URL `https://openwhisk.ng.bluemix.net/api/v1/namespaces` 执行 HTTP 方法 `GET`。请注意，授权值是基本 64 位编码的 OpenWhisk 授权字符串。响应的内容类型是 `application/json`。

## 操作
{: #openwhisk_rest_api_actions}
要创建或更新操作，请在操作集合上使用 `PUT` 方法发送 HTTP 请求。例如，要使用单个文件内容创建名称为 `hello` 的 `nodejs:6` 操作，请使用以下命令：
```bash
curl -u $AUTH -d '{"namespace":"_","name":"hello","exec":{"kind":"nodejs:6","code":"function main(params) { return {payload:\"Hello \"+params.name}}"}}' -X PUT -H "Content-Type: application/json" https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/hello?overwrite=true 
```
{: pre}

要在操作上执行分块调用，使用 `POST` 方法和包含输入参数 `name` 的主体发送 HTTP 请求，请使用以下命令：
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/hello?blocking=true \
-X POST -H "Content-Type: application/json" \
-d '{"name":"John"}'  
```
{: pre}
您将得到以下响应：
```json
{
  "duration": 2,
  "name": "hello",
  "subject": "john@example.com_dev",
  "activationId": "c7bb1339cb4f40e3a6ccead6c99f804e",
  "publish": false,
  "annotations": [{
    "key": "limits",
    "value": {
      "timeout": 60000,
      "memory": 256,
      "logs": 10
    }
  }, {
    "key": "path",
    "value": "john@example.com_dev/hello"
  }],
  "version": "0.0.1",
  "response": {
    "result": {
          "payload": "Hello John"
    },
    "success": true,
    "status": "success"
  },
  "end": 1493327653769,
  "logs": [],
  "start": 1493327653767,
  "namespace": "john@example.com_dev"
}
```
如果只想获得 `response.result`，请使用查询参数 `result=true` 重新运行该命令：
```bash
curl -u $AUTH "https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/hello?blocking=true&result=true" \
-X POST -H "Content-Type: application/json" \
-d '{"name":"John"}' 
```
{: pre}
您将得到以下响应：
```json
{
  "payload": "hello John"
}
```

## 注释和 Web 操作
{: #openwhisk_rest_api_webactions}
要将操作创建为 Web 操作，您需要为 Web 操作添加[注释](annotations.md) `web-export=true`。由于 Web 操作可公共访问，因此应该使用注释 `final=true` 保护预定义的参数（即，将这些参数视为最终参数）。如果使用 CLI 标志 `--web true` 创建或更新操作，那么此命令将同时添加注释 `web-export=true` 和 `final=true`。

运行 curl 命令，以提供要在操作上设置的注释的完整列表
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/hello?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"namespace":"_","name":"hello","exec":{"kind":"nodejs:6","code":"function main(params) { return {payload:\"Hello \"+params.name}}"},"annotations":[{"key":"web-export","value":true},{"key":"raw-http","value":false},{"key":"final","value":true}]}'
```
{: pre}
现在，可以将此操作作为公共 URL 调用，而无需 OpenWhisk 授权。请尝试使用在 URL 末尾包含可选扩展名（如 `.json` 或 `.http`）的 Web 操作公共 URL 进行调用。
```bash
curl https://openwhisk.ng.bluemix.net/api/v1/web/john@example.com_dev/default/hello.json?name=John
```
{: pre}
```json
{
  "payload": "Hello John"
}
```
请注意，此示例源代码不会使用 `.http`；有关如何修改的信息，请参阅 [Web 操作](webactions.md)文档。
## 序列
{: #openwhisk_rest_api_sequences}
要创建操作序列，需要在创建时按所需顺序提供构成序列的操作的名称，这样第一个操作的输出将作为下一个操作的输入进行传递。

$ wsk action create sequenceAction --sequence /whisk.system/utils/split,/whisk.system/utils/sort

创建具有操作 `/whisk.system/utils/split` 和 `/whisk.system/utils/sort` 的序列。
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/sequenceAction?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"namespace":"_","name":"sequenceAction","exec":{"kind":"sequence","components":["/whisk.system/utils/split","/whisk.system/utils/sort"]},"annotations":[{"key":"web-export","value":true},{"key":"raw-http","value":false},{"key":"final","value":true}]}' 
```
{: pre}

指定操作的名称时请注意，操作名称必须是标准名称。

## 触发器
{: #openwhisk_rest_api_triggers}
要创建触发器，至少需要触发器的名称。还可以包含在触发器触发时通过规则传递到操作的缺省参数。

创建名称为 `events` 的触发器，缺省参数为 `type`，值设置为 `webhook`。
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/triggers/events?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"name":"events","parameters":[{"key":"type","value":"webhook"}]}' 
```
{: pre}

现在，每当您有需要触发此触发器的事件时，该事件都只会采纳一个使用 OpenWhisk 授权密钥通过 `POST` 方法发起的 HTTP 请求。

要使用参数 `temperature` 触发触发器 `events`，请发送以下 HTTP 请求。

```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/triggers/events \
-X POST -H "Content-Type: application/json" \
-d '{"temperature":60}' 
```
{: pre}

### 使用订阅源操作的触发器
{: #openwhisk_rest_api_triggers_feed}
有特殊触发器可以使用订阅源操作进行创建。订阅源操作是帮助配置订阅源提供程序的操作，该提供程序将负责在每次有触发器的事件时触发触发器。在 [feeds.md] 文档中可了解有关这些订阅源提供程序的更多信息。

一些利用订阅源操作的可用触发器为 periodic/alarms、Slack、Github、Cloudant/Couchdb 和 messageHub/Kafka。您还可以创建自己的订阅源操作和订阅源提供程序。

下面创建名称为 `periodic` 的触发器，以按指定频率（每 2 小时，即 02:00:00、04:00:00、...）触发。

使用 CLI 通过一个命令来执行上述操作
```bash
wsk trigger create periodic --feed /whisk.system/alarms/alarm \
  --param cron "0 */2 * * *" -v
```
{: pre}
如您所见，由于我们使用的是 `-v` 标志，这将发送两个 HTTP 请求，一个用于创建触发器 `periodic`，另一个用于调用订阅源操作 `/whisk.system/alarms/alarm`，该操作中的参数用于将订阅源提供程序配置为每 2 小时触发一次触发器。
要使用 REST API 执行相同操作，请首先创建触发器
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/triggers/periodic?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"name":"periodic","annotations":[{"key":"feed","value":"/whisk.system/alarms/alarm"}]}'  
```
{: pre}

如您所见，注释 `feed` 存储在触发器中。日后，删除触发器时，我们将使用此注释来了解要使用的订阅源操作。

现在，触发器已创建，接着将调用订阅源操作
```bash
curl -u $AUTH "https://openwhisk.ng.bluemix.net/api/v1/namespaces/whisk.system/actions/alarms/alarm?blocking=true&result=false" \
-X POST -H "Content-Type: application/json" \
-d "{\"authKey\":\"$AUTH\",\"cron\":\"0 */2 * * *\",\"lifecycleEvent\":\"CREATE\",\"triggerName\":\"/_/periodic\"}" 
```
{: pre}

删除触发器类似于创建触发器，只不过此时是要删除触发器，同时使用订阅源操作将订阅源提供程序配置为删除触发器的处理程序。

调用订阅源操作以删除订阅源提供程序中的触发器处理程序
```bash
curl -u $AUTH "https://openwhisk.ng.bluemix.net/api/v1/namespaces/whisk.system/actions/alarms/alarm?blocking=true&result=false" \
-X POST -H "Content-Type: application/json" \
-d "{\"authKey\":\"$AUTH\",\"lifecycleEvent\":\"DELETE\",\"triggerName\":\"/_/periodic\"}"  
```
{: pre}

现在，使用 `DELETE` 方法通过 HTTP 请求删除触发器
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/triggers/periodic \
-X DELETE -H "Content-Type: application/json" 
```
{: pre}

## 规则
{: #openwhisk_rest_api_rules}
要创建用于将触发器与操作相关联的规则，请使用 `PUT` 方法发送 HTTP 请求，并在请求主体中提供触发器和操作。
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/rules/t2a?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"name":"t2a","status":"","trigger":"/_/events","action":"/_/hello"}' 
```
{: pre}

可以启用或禁用规则，也可以通过更新规则的状态属性来更改规则的状态。例如，要禁用规则 `t2a`，请使用 `POST` 方法在请求的主体中发送 `status: "inactive"`。
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/rules/t2a?overwrite=true \
-X POST -H "Content-Type: application/json" \
-d '{"status":"inactive","trigger":null,"action":null}'  
```
{: pre}

## 包
{: #openwhisk_rest_api_packages}
要在包中创建操作，必须先创建包；要创建名称为 `iot` 的包，请使用 `PUT` 方法发送 HTTP 请求

```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/packages/iot?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"namespace":"_","name":"iot"}' 
```
{: pre}

## 激活
{: #openwhisk_rest_api_activations}
要获取最近 3 次激活的列表，请使用 `GET` 方法发送 HTTP 请求，并传递查询参数 `limit=3`
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/activations?limit=3
```
{: pre}

要获取激活的所有详细信息（包括结果和日志），请使用 `GET` 方法发送 HTTP 请求，并将激活标识作为路径参数传递
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/activations/f81dfddd7156401a8a6497f2724fec7b
```
{: pre}
