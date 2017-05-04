---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# ID 제공자 개요
{: #identity-providers-overview}

ID 제공자는 애플리케이션에 대해 인증을 제공하는 데 사용됩니다.
{:shortdesc}

모바일 및 웹 애플리케이션에서 다음과 같은 ID 제공자를 사용할 수 있습니다. 

* **Facebook** - 사용자는 자신의 Facebook 신임 정보로 모바일 또는 웹 앱에 로그인합니다.
* **Google** - 사용자는 자신의 Google+ 신임 정보로 모바일 또는 웹 앱에 로그인합니다.
<!--* **Custom** - Bring your own identity provider. The identity providers should be compliant with OIDC. -->

## 기본 구성 사용
{: #default-configuration}

{{site.data.keyword.appid_short_notm}}는 ID 제공자를 처음 설정할 때 기본 구성을 제공합니다. 개발 모드에서만 기본 구성을 사용할 수 있습니다. 각 ID 제공자의 경우, 이러한 신임 정보는 하루에 {{site.data.keyword.appid_short_notm}} 인스턴스당 100회의 사용으로 제한됩니다. 애플리케이션을 공개하기 전에 사용자 자신의 신임 정보에 대해 [기본 구성](/docs/services/appid/identity-providers.html)을 업데이트하십시오. 
