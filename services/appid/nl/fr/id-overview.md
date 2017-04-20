---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Présentation des fournisseurs d'identité
{: #identity-providers-overview}

Les fournisseurs d'identité sont utilisés pour fournir une authentification à vos applications.
{:shortdesc}

Vous pouvez utiliser les fournisseurs d'identité suivants dans vos applications mobiles et Web :

* **Facebook** - Vos utilisateurs se connectent à l'application mobile ou Web avec leurs données d'identification Facebook.
* **Google** -  Vos utilisateurs se connectent à l'application mobile ou Web avec leurs données d'identification Google+.
<!--* **Custom** - Bring your own identity provider. The identity providers should be compliant with OIDC. -->

## Utilisation de la configuration par défaut
{: #default-configuration}

{{site.data.keyword.appid_short_notm}} fournit une configuration par défaut lorsque vous mettez en place initialement vos fournisseurs d'identité. Vous ne pouvez utiliser la configuration par défaut qu'en mode développement. Pour chaque fournisseur d'identité, ces données d'identification sont limitées à 100 utilisations par instance {{site.data.keyword.appid_short_notm}} et par jour. Avant
de publier votre application, mettez à jour la [configuration par défaut](/docs/services/appid/identity-providers.html) en spécifiant vos propres données d'identification.
