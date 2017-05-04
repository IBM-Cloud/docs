---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Überblick über Identitätsprovider
{: #identity-providers-overview}

Identitätsprovider werden eingesetzt, um die Authentifizierung für Ihre Anwendungen bereitzustellen.
{:shortdesc}

Sie können in Ihren mobilen Anwendungen sowie in Ihren Webanwendungen folgende Identitätsprovider verwenden:

* **Facebook** - Ihre Benutzer melden sich bei der mobilen oder Web-App mit ihren Facebook-Berechtigungsnachweisen an.
* **Google** - Ihre Benutzer melden sich bei der mobilen oder Web-App mit ihren Google+-Berechtigungsnachweisen an.
<!--* **Custom** - Bring your own identity provider. The identity providers should be compliant with OIDC. -->

## Standardkonfiguration verwenden
{: #default-configuration}

{{site.data.keyword.appid_short_notm}} stellt eine Standardkonfiguration bereit, wenn Sie Ihre Identitätsprovider erstmalig einrichten. Die Standardkonfiguration können Sie nur im Entwicklungsmodus verwenden. Diese Berechtigungsnachweise sind pro Identitätsprovider auf 100 Benutzer pro {{site.data.keyword.appid_short_notm}}-Instanz und pro Tag beschränkt. Bevor Sie Ihre Anwendung veröffentlichen, aktualisieren Sie die [Standardkonfiguration](/docs/services/appid/identity-providers.html) mit Ihren eigenen Berechtigungsnachweisen. 
