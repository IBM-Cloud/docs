---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.mobilepushshort}} 服务错误消息
{: #errors}
上次更新时间：2017 年 2 月 13 日
{: .last-updated}


在响应 REST API 请求时，会返回以下 {{site.data.keyword.mobilepushshort}} 错误消息。

样本错误响应：
```
	{
		"message": "Missing APNs credentials",
     "docUrl": "https://www.ng.bluemix.net/docs/troubleshoot/errors/mobilepush/index.html#FPWSE0003E",
     "code":   "FPWSE0003E"

}
```
		    {: codeblock}

要获取有关错误的更多信息，请在文档中搜索相关错误代码。

## FPWSE0001E
{: #error_fpwse0001e}

**说明**：服务器上没有您尝试查询的资源，例如标记或预订。

**用户响应**：请创建在消息中报告的资源。或者，您可以提供正确的标识来查询该资源。


## FPWSE0002E
{: #error_fpwse0002e}

**说明**：服务器上已存在您尝试创建的资源。资源可以是标记、预订等。

**用户响应**：请使用其他标识来创建该资源。


## FPWSE0003E
{: #error_fpwse0003e}

**说明**：{{site.data.keyword.mobilepushshort}} 服务的必备配置不完整。可能是您在尝试获取 Apple 推送通知服务 (APNs) 凭证，但凭证尚未配置。

**用户响应**：请确保已使用有效的 APNs 安全证书配置 {{site.data.keyword.mobilepushshort}}服务。有关的更多信息，请参阅[配置 APN 的凭证 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](t_push_provider_ios.html){: new_window}。


## FPWSE0004E
{: #error_fpwse0004e}

**说明**：请求中包含的 JSON 主体无效。


**用户响应**：请确保在请求中使用有效的 JSON 语法。



## FPWSE0005E
{: #error_fpwse0005e}

**说明**：对 {{site.data.keyword.mobilepushshort}} 服务器发出的请求不正确或不完整，因为 JSON 主体未包含完成 API 请求所需的属性值。例如，密码无效或设备令牌缺失。


**用户响应**：请查看消息以了解缺失或无效的属性值，然后提供必需信息。



## FPWSE0006E
{: #error_fpwse0006e}

**说明**：请求的 JSON 主体具有 {{site.data.keyword.mobilepushshort}} 服务器无法识别的参数。


**用户响应**：请验证请求中的 JSON 主体是否遵循 {{site.data.keyword.mobilepushshort}} 服务器所预期的请求格式。有关的更多信息，请参阅 [REST API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://mobile.{DomainName}/imfpush/){: new_window}。



## FPWSE0007E 
{: #error_fpwse0007e}

**说明**：请求 URL 中的查询字符串具有无法识别的参数。例如，如果预订删除请求具有 deviceId 和 tagName 以外的参数，那么可能会发生此错误。


**用户响应**：请验证请求中的 JSON 主体是否遵循 {{site.data.keyword.mobilepushshort}} 服务器所预期的请求格式。有关的更多信息，请参阅 [REST API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://mobile.{DomainName}/imfpush/){: new_window}。



## FPWSE0008E
{: #error_fpwse0008e}

**说明**：请求 URL 中的查询字符串缺少必需参数。例如，预订删除请求中可能缺少 deviceId 和 tagName 参数。


**用户响应**：请验证请求中的 JSON 主体是否遵循 {{site.data.keyword.mobilepushshort}} 服务器所预期的请求格式。有关的更多信息，请参阅 [REST API ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://mobile.{DomainName}/imfpush/){: new_window}。



## FPWSE0009E
{: #error_fpwse0009e}

**说明**：尝试发送通知，但设备没有向应用程序注册。

**用户响应**：请在尝试发送通知之前，确保设备已向应用程序注册。



## FPWSE0010E
{: #error_fpwse0010e}

**说明**：提交到服务器的请求导致异常状况。以下某个情况可能会导致此错误：

- {{site.data.keyword.mobilepushshort}} 使用的内部子系统未在响应。
- {{site.data.keyword.mobilepushshort}} 无法处理请求所导致的错误状况。
- {{site.data.keyword.mobilepushshort}} 服务需要管理员的帮助。

**用户响应**：请重试请求。如果问题仍然存在，请联系 IBM 软件支持。



## FPWSE0011E
{: #error_fpwse0011e}

**说明**：服务器上已存在该标记预订。例如，在创建已存在的预订时。

**用户响应**：请使用唯一标记名称来创建预订。



## FPWSE0012E
{: #error_fpwse0012e}

**说明**：服务器上不存在该标记预订。所提交请求的内容是检索或删除不存在的预订时，会发生此错误。


**用户响应**：请在请求中使用正确的标记名称和设备标识。



## FPWSE0013E
{: #error_fpwse0013e}

**说明**：请求中的 JSON 有效内容无效。


**用户响应**：请确保 JSON 有效内容有效。


## FPWSE0025E
{: #error_fpwse0025e}

**解释**：服务器当前无法处理请求。

**用户响应**：请稍后重新提交请求。


## FPWSE1007E 
{: #error_fpwse1007e}

**说明**：已对此应用程序禁用 {{site.data.keyword.mobilepushshort}} 服务。这可能是由于计费问题，也可能是管理员已禁用该应用程序。


**用户响应**：请参阅 Bluemix 文档中的故障诊断主题，以检查服务状态，查看故障诊断信息或了解有关获取帮助的信息。



## FPWSE1079E
{: #error_fpwse1079e}

**说明**：为查询操作提供的偏移值无效。

**用户响应**：请确保偏移值大于或等于零。



## FPWSE1080E 
{: #error_fpwse1080e}

**说明**：为查询操作提供的大小值无效。

**用户响应**：请确保大小值大于零。



