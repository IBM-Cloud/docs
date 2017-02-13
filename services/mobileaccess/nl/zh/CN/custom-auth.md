---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 使用定制身份提供者认证用户
{: #custom-id}


创建使用 {{site.data.keyword.amafull}} 服务的定制身份提供者，并实施自己的逻辑来收集和验证凭证。定制身份提供者是一种用于公开 RESTful 接口的 Web 应用程序。可以在内部部署或 {{site.data.keyword.Bluemix}} 上托管定制身份提供者。唯一的要求是定制身份提供者必须可从公共因特网进行访问，以便其能与 {{site.data.keyword.amashort}} 服务进行通信。

## {{site.data.keyword.amashort}} 定制身份请求流程
{: #custom-id-ovr}


### {{site.data.keyword.amashort}} 客户端请求流程
 下图演示了 {{site.data.keyword.amashort}} 如何集成定制身份提供者。

![请求流程图](images/mca-sequence-custom.jpg)

* 使用 {{site.data.keyword.amashort}} SDK 对受 {{site.data.keyword.amashort}} 服务器 SDK 保护的后端资源发起请求。
* {{site.data.keyword.amashort}} 服务器 SDK 检测到未授权的请求，然后返回 HTTP 401 和授权作用域。
* {{site.data.keyword.amashort}} 客户端 SDK 自动检测到上述 HTTP 401，然后启动认证过程。
* {{site.data.keyword.amashort}} 客户端 SDK 访问 {{site.data.keyword.amashort}} 服务，并请求 Authorization 头。
* {{site.data.keyword.amashort}} 服务与定制身份提供者进行通信，以启动认证过程。
* 定制身份提供者向 {{site.data.keyword.amashort}} 服务返回认证质询。
* {{site.data.keyword.amashort}} 服务向 {{site.data.keyword.amashort}} 客户端 SDK 返回认证质询。
* {{site.data.keyword.amashort}} 客户端 SDK 将认证委派给您创建的定制类。您负责收集凭证并将这些凭证返回给 {{site.data.keyword.amashort}} 客户端 SDK。
* 开发者向 {{site.data.keyword.amashort}} SDK 提供凭证后，这些凭证会作为认证质询回复发送到 {{site.data.keyword.amashort}} 服务。
* {{site.data.keyword.amashort}} 服务会通过定制身份提供者来验证认证质询回复。
* 如果验证成功，{{site.data.keyword.amashort}} 服务会生成 Authorization 头，并将其返回给 {{site.data.keyword.amashort}} 客户端 SDK。Authorization 头包含两个令牌：一个是访问令牌，用于包含访问许可权信息；一个是标识令牌，用于包含有关当前用户、设备和应用程序的信息。
* 从此刻开始，通过 {{site.data.keyword.amashort}} 客户端 SDK 发起的请求全部具有新获取的 Authorization 头。
* {{site.data.keyword.amashort}} 客户端 SDK 自动重新发送触发了授权流程的原始请求。
* {{site.data.keyword.amashort}} 服务器 SDK 从请求中抽取 Authorization 头，通过 {{site.data.keyword.amashort}} 服务对其进行验证，然后授予对后端资源的访问权。

### {{site.data.keyword.amashort}} Web 应用程序请求流程
{: #mca-custom-web-sequence}

{{site.data.keyword.amashort}} Web 应用程序请求流程类似于移动客户端的流程。但是，{{site.data.keyword.amashort}} 保护 Web 应用程序而非 {{site.data.keyword.Bluemix_notm}} 后端资源。

  * Web 应用程序会发送初始请求（例如，通过登录表单）。
  * 最终重定向会指向 Web 应用程序本身的受保护区域，而非后端受保护资源。

## 了解定制身份提供者
{: #custom-id-about}

通过定制身份提供者，可以提供要发送给客户端的定制认证质询。您可以全面定制认证流程。

在创建定制身份提供者时，您可以执行以下操作：

1. 定制要由 {{site.data.keyword.amashort}} 服务发送给移动或 Web 客户端应用程序的认证质询。认证质询是包含任何定制数据的 JSON 对象。客户端可以使用此定制数据来定制认证流程。

  定制认证质询示例：

	```JavaScript
	{
		status: "challenge",
		challenge: {
			message:"Enter username and password",
			retriesLeft: 2,
			minUsernameLenth: 8
		}
	}
	```
	{: codeblock}

1. 在客户端上实施任何定制凭证收集流程，包括多步认证和多形式认证。与定制认证质询类似，您必须设计定制认证质询回复的结构。

  客户端发送的定制认证质询回复的示例：

	```JavaScript
	{
		username:"bob.smith",
		password:"abcd1234",
		pincode:"1234"
	}
	```
	{: codeblock}

1. 实现用于验证所提供认证质询回复的定制逻辑。

1. 定义包含任何所需定制属性的定制用户身份对象。下面是成功认证后，客户端获取的定制用户身份对象的示例：

	```JavaScript
	{
		username:"bob.smith",
		displayName:"Bob Smith",
		attributes:{
			age: 30,
			accountNumber: 12345,
			lastLogin: "Sept 1st, 2015"
		}
	}
	```
	{: codeblock}

### 定制身份提供者的样本实现
{: #custom-sample}

开发定制身份提供者时，可以将定制身份提供者的以下任何 Node.js 样本实现用作参考。请从 GitHub 存储库下载完整应用程序代码。

 * [简单样本 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample "外部链接图标"){: new_window}
 * [高级样本 ![外部链接图标](../../icons/launch-glyph.svg "外部链接图标")](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management "外部链接图标"){: new_window}

## {{site.data.keyword.amashort}} 服务器与定制身份提供者之间的典型通信
{: #custom-id-comm}

1. {{site.data.keyword.amashort}} 服务向定制身份提供者发送 `startAuthorization` 请求。
1. 定制身份提供者使用要发送到客户端的定制认证质询进行响应。
1. {{site.data.keyword.amashort}} 服务将接收自定制身份提供者的定制认证质询发送到客户端，并且最终接收来自客户端的认证质询回复。
1. {{site.data.keyword.amashort}} 服务将包含认证质询回复的 `handleChallengeAnswer` 请求发送到定制身份提供者。
1. 定制身份提供者验证认证质询回复，并使用包含用户身份信息的 success 应答进行响应。
1. （可选）定制身份提供者从客户端收到质询回复后，可能会提供更多质询。通过发送多个质询，可支持多步认证过程。

## 有状态和无状态应用程序
{: #custom-id-state}

缺省情况下，定制身份提供者被视为无状态应用程序。在某些情况下，定制身份提供者可能需要存储与认证过程相关的状态。示例用例是多步认证，其中定制身份提供者需要存储第一个认证步骤的结果后，才能继续执行下一步。要支持有状态功能，定制身份提供者必须生成 stateID，并在对 {{site.data.keyword.amashort}} 服务的响应中提供此 stateID。{{site.data.keyword.amashort}} 服务必须在属于客户端认证过程的后续请求中传递此 stateID。

## 定制域
{: #custom-id-custom}

一个定制身份提供者支持一个定制认证域。要处理传入认证质询，请在客户端应用程序中创建并注册 `AuthenticationDelegate`/	`AuthenticationListener` 的一个实例。在 {{site.data.keyword.amashort}}“仪表板”中配置定制身份提供者时，定义定制认证域名。域会识别传入请求的特定 {{site.data.keyword.amashort}} 服务实例。

## 后续步骤
{: #next-steps}

* [创建定制身份提供者](custom-auth-identity-provider.html)
* [配置 {{site.data.keyword.amashort}} 进行定制认证](custom-auth-config-mca.html)
* [针对 Android 配置定制认证](custom-auth-android.html)
* [针对 iOS (Swift SDK) 配置定制认证](custom-auth-ios-swift-sdk.html)
* [针对 Cordova 配置定制认证](custom-auth-cordova.html)
