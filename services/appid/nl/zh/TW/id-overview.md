---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# 身分提供者概觀
{: #identity-providers-overview}

身分提供者用來提供鑑別給您的應用程式。
{:shortdesc}

您可以在行動及 Web 應用程式中使用下列身分提供者：

* **Facebook** - 您的使用者利用其 Facebook 認證來登入行動或 Web 應用程式。
* **Google** - 您的使用者利用其 Google+ 認證來登入行動或 Web 應用程式。
<!--* **Custom** - Bring your own identity provider. The identity providers should be compliant with OIDC. -->

## 使用預設配置
{: #default-configuration}

{{site.data.keyword.appid_short_notm}} 會在您一開始設定身分提供者時提供預設配置。您只能在開發模式中使用預設配置。對於每一個身分提供者，這些認證限制為每天每個 {{site.data.keyword.appid_short_notm}} 實例可以使用 100 次。發佈應用程式之前，請將[預設配置](/docs/services/appid/identity-providers.html)更新為您自己的認證。
