---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# ID プロバイダーの概要
{: #identity-providers-overview}

ID プロバイダーを使用して、アプリケーションに認証機能を提供します。
{:shortdesc}

モバイル・アプリケーションや Web アプリケーションで以下の ID プロバイダーを使用できます。

* **Facebook** - ユーザーは、Facebook の資格情報を使用してモバイル・アプリや Web アプリにログインします。
* **Google** - ユーザーは、Google+ の資格情報を使用してモバイル・アプリや Web アプリにログインします。
<!--* **Custom** - Bring your own identity provider. The identity providers should be compliant with OIDC. -->

## デフォルト構成の使用
{: #default-configuration}

初めて ID プロバイダーをセットアップするときに、{{site.data.keyword.appid_short_notm}} からデフォルト構成が示されます。このデフォルト構成は開発モードのみで使用できます。ID プロバイダーごとに、これらの資格情報は {{site.data.keyword.appid_short_notm}} インスタンスあたり毎日 100 回の使用に制限されています。アプリケーションを公開する前に、[デフォルトの構成](/docs/services/appid/identity-providers.html)を自分の資格情報に更新してください。
