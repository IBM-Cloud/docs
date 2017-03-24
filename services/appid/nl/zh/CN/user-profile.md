---

copyright:
  years: 2017
lastupdated: "2017-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# 用户概要文件
{: #user-profile}

用户概要文件是由 {{site.data.keyword.appid_short}} 存储并维护的实体。概要文件保存用户的属性和身份，可以是匿名的，也可以链接到身份提供者管理的身份。
{:shortdesc}

{{site.data.keyword.appid_short_notm}} 提供了用于匿名登录或通过向 OpenId Connect (OIDC) IdP 认证来登录的 API，请参阅[配置身份提供者](https://console.stage1.ng.bluemix.net/docs/services/appid/identity-providers.html#setting-up-idp)。用户概要文件属性 API 端点是通过在登录和授权过程中由 {{site.data.keyword.appid_short_notm}} 生成的访问令牌保护的资源。


## 存储、读取和删除用户属性
{: #storing-data}

{{site.data.keyword.appid_short_notm}} 提供了用于对用户属性执行 CRUD 操作的 [REST API](http://mobileclientaccess.stage1.mybluemix.net/swagger-ui/#!/Authorization_Server_V3/authorization)，以及用于 [Android](https://github.com/ibm-cloud-security/appid-clientsdk-android) 和 [Swift](https://github.com/ibm-cloud-security/appid-clientsdk-swift) 移动客户端的 SDK。


## OAuth 身份
{: #oauth}

调用 OAuth 登录 API 时，{{site.data.keyword.appid_short_notm}} 会使用 OAuth 2.0 和 OIDC 协议通过所选身份提供者来授权和认证调用者。一旦认证后，该身份就与 {{site.data.keyword.appid_short_notm}} 用户记录相关联。{{site.data.keyword.appid_short_notm}} 会返回一个可用于访问用户属性的访问令牌，以及一个保存了身份提供者所提供身份信息的身份令牌。相同的用户记录及其属性还可由使用此相同身份进行认证的任何客户端再次访问。


## 匿名用户
{: #anonymous}

匿名登录时，{{site.data.keyword.appid_short_notm}} 会创建一个标记为匿名的特别用户记录。{{site.data.keyword.appid_short_notm}} 会向调用者返回匿名访问令牌和身份令牌。通过使用匿名访问令牌，用户应用程序可以创建、读取、更新和删除存储在用户记录中的属性。例如，开发者可以创建一个应用程序，用户在其中无须登录即可立即开始向购物车添加项目。


## 已识别用户
{: #identified}

具有身份提供者所提供身份的匿名用户可以成为已识别用户。在以下步骤中概述了从匿名用户转为已知用户的流程：

* 开发者将匿名访问令牌传递到登录 API。
* {{site.data.keyword.appid_short_notm}} 通过身份提供者认证调用者。
* {{site.data.keyword.appid_short_notm}} 找到访问令牌定义的匿名用户记录，然后为其分配身份。
    **注**：只能将尚未分配给其他用户的身份分配给匿名记录。如果身份已经与其他 {{site.data.keyword.appid_short_notm}} 用户关联，那么访问令牌和身份令牌会包含该用户的记录信息，并提供对其属性的访问权。先前的匿名用户及其属性将无法通过新的访问令牌进行访问。在此令牌到期之前，仍可通过匿名访问令牌来访问这些信息。开发者可以选择要如何将匿名用户的匿名属性与已知用户的属性合并。
* 从 {{site.data.keyword.appid_short_notm}} 收到的新访问令牌和身份令牌指向已知用户，并且身份令牌包含从身份提供者接收到的公共信息。
* 此用户的匿名令牌会变为无效。

此用户在匿名状态时包含的属性可通过新的访问令牌进行访问。可以添加、更改或删除新令牌。然后，在用户使用相同身份从任何客户端登录时，此用户及其属性都将进行解析并且可访问。


## 数据分隔和加密
{: #data}

{{site.data.keyword.appid_short_notm}} 存储并加密用户概要文件属性。作为多租户服务，每个租户都具有指定的加密密钥，并且每个租户中的用户数据只使用该租户的密钥进行加密。

{{site.data.keyword.appid_short_notm}} 确保私有信息在加密后才进行存储。
