---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# 身份提供者概述
{: #identity-providers-overview}

身份提供者用于为应用程序提供认证。
{:shortdesc}

可以在移动和 web 应用程序中使用以下身份提供者：

* **Facebook** - 用户使用自己的 Facebook 凭证登录到移动或 Web 应用程序。
* **Google** - 用户使用自己的 Google+ 凭证登录到移动或 Web 应用程序。
<!--* **Custom** - Bring your own identity provider. The identity providers should be compliant with OIDC. -->

## 使用缺省配置
{: #default-configuration}

初始设置身份提供者时，{{site.data.keyword.appid_short_notm}} 提供了缺省配置。缺省配置只能用于开发方式。对于每个身份提供者，这些凭证限制为每个 {{site.data.keyword.appid_short_notm}} 实例每天 100 次使用。在发布应用程序之前，请将[缺省配置](/docs/services/appid/identity-providers.html)更新为您自己的凭证。
