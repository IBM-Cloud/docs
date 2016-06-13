---

copyright:
 years: 2015, 2016

---

# 使用 REST API
{: #push-api-rest}

您可以将 REST（具象状态传输）API（应用程序编程接口）用于推送通知。还可以使用 SDK 和 [Push API](https://mobile.{DomainName}/imfpushrestapidocs/) 来进一步开发您的客户机应用程序。

通过 Push REST API，后端服务器应用程序和客户机可以访问 Push 功能。

- 设备注册
- 注册
- 消息
- 预订
- 标记

要获取 REST API 的基本 URL，请执行以下操作：

1. 在 Bluemix®“目录”的“样板”部分中创建后端应用程序，这会自动将该 Push 服务绑定到此应用程序。如果已创建后端应用程序，请务必将该应用程序绑定到 Push Notification Service。 

1. 在 Bluemix“仪表板”的主页中，转至**应用程序**区域，然后单击您的应用程序。

3. 单击“移动选项”。路径和应用程序 GUID 值会显示在应用程序的详细信息页面顶部。



## 接受语言头
{: #push-api-rest-accept}

“Accept-Language”头指定要将哪种语言用于 [Push REST API](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window} 输出的错误消息。支持的错误消息语言如下：简体中文、繁体中文、英语（美国）、德语、法语、意大利语、日语、韩语、葡萄牙语和西班牙语。

## appSecret
{: #push-api-rest-secret}

应用程序绑定到 Push Notifications 后，该服务会生成一个 appSecret（唯一密钥），并会在响应头中传递该密钥。如果是使用 IBM® Push Notifications for Bluemix Rest API，请使用 REST API 参考来获取有关需要保护哪些 API 的信息。有关 REST API 的信息，请参阅 REST API 参考。

请求头必须包含 appSecret。如果不包含，服务器会返回“401 未授权”错误代码。将推送通知添加到应用程序时，会创建特定的 AppID。在响应中，您会得到一个名为 appSecret 的头，该头用于创建标记或发送消息。该操作通过目录或样板中的服务来执行。

要获取 appSecret 值，请执行以下操作：

1. 单击绑定到推送服务的 *app-name*。
2. 单击**显示凭证**链接以显示 appSecret (AppID)。

**显示凭证**屏幕将显示有关 appSecret 的信息：

```
{
 "imfpush_Dev": [
{
     "name": "testapp1",
     "label": "imfpush_Dev",
     "plan": "Basic",
     "credentials": {
       "url": "http://imfpush.ng.bluemix.net/imfpush/v1/apps/b615b280-b37e-4042-8815-38a758f234e2",
       "admin_url": "//mobile.ng.bluemix.net/imfpushdashboard/?appGuid=b615b280-b37e-4042-8815-38a758f234e2",
       "appSecret": "8dac71a5-2219-42b3-a9f3-dbb828ba1f04"  
       }
   }
 ]
}
``` 

##Push REST API 过滤器
{: #push-api-rest-filters}

过滤器定义搜索条件，该条件用于限制从 Push 的 GET API 返回的数据。针对要过滤的 GET 操作结果应用过滤器。过滤器会限制结果中包含的条目数。例如，可以使用过滤器来搜索以“test”开头的标记。要生成过滤器，可以使用以下语法。

**名称**
要应用过滤器的字段名称。

**运算符**
为 ==（完全匹配）或 =@（包含子字符串），用于描述要使用的过滤匹配。

**表达式**
要包含在结果中的值。

如果表达式中出现逗号和反斜杠，必须用反斜杠将它们转义。

使用多个过滤器时，可以使用 AND 和 OR 逻辑来组合这些过滤器。

- 对于 AND 逻辑，在查询中使用多个过滤器。
- 对于 OR 逻辑，在过滤表达式内部使用逗号 (,)。
- 对于 AND 和 OR 逻辑，单个查询可以同时包含 AND 和 OR 逻辑。使用 AND 表达式组合多个过滤器时，会先对每个过滤器单独求值，然后再执行 AND 运算。

对于设备 GET API，将支持以下组合：
-名称为 platform 字段。
- 运算符可以为 == 或 =@，但 platform 除外
- 对于 platform，运算符必须是 ==。如果使用运算符 =@，那么值可以为子字符串。
- 如果使用 ==，那么值必须为完全匹配的字符串。

对于预订 GET API，将支持以下组合：

- 名称可以是以下某个字段：tagName 或 deviceId
- 运算符可以为 == 或 =@，但 platform 除外
- 对于 platform，运算符必须是 ==
- 如果使用 =@ 运算符，那么值可以为子字符串。如果使用 == 运算符，那么值必须为完全匹配的字符串。
- 对于标记 GET API，将支持以下组合：
- 名称可以是以下某个字段：“name”或“description”
- 如果使用运算符 =@，那么值可以为子字符串。
- 如果使用 ==，那么值必须为完全匹配的字符串。
