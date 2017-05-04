---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Visión general de los proveedores de identidad
{: #identity-providers-overview}

Los proveedores de identidad se utilizan para proporcionar autenticación a sus aplicaciones.
{:shortdesc}

Puede utilizar los siguientes proveedores de identidad en sus aplicaciones web y móviles:

* **Facebook**: Los usuarios inician sesión en la app móvil o web con las credenciales de Facebook.
* **Google**: Los usuarios inician sesión en la app móvil o web con las credenciales de Google+.
<!--* **Custom** - Bring your own identity provider. The identity providers should be compliant with OIDC. -->

## Utilización de la configuración predeterminada
{: #default-configuration}

{{site.data.keyword.appid_short_notm}} proporciona una configuración predeterminada cuando se configuran inicialmente los proveedores de identidad. Puede utilizar la configuración predeterminada sólo en modalidad de desarrollo. Para cada proveedor de identidad, estas credenciales se limitan a 100 usos por instancia de {{site.data.keyword.appid_short_notm}}, por día. Antes de publicar la aplicación, actualice la [configuración predeterminada](/docs/services/appid/identity-providers.html) con sus propias credenciales.
