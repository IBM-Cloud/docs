---

copyright:
  years: 2017 lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Visão geral de provedores de identidade
{: #identity-providers-overview}

Os provedores de identidade são usados para fornecer autenticação para os seus aplicativos.
{:shortdesc}

É possível usar os seguintes provedores de identidade em seus aplicativos móveis e da web:

* **Facebook** - os seus usuários efetuam login no app móvel ou da web com suas credenciais do Facebook.
* **Google** - os seus usuários efetuam login no app móvel ou da web com suas credenciais do Google+.
<!--* **Custom** - Bring your own identity provider. The identity providers should be compliant with OIDC. -->

## Usando a configuração padrão
{: #default-configuration}

O {{site.data.keyword.appid_short_notm}} fornecerá uma configuração padrão quando você inicialmente configurar os seus provedores de identidade. É
possível usar a configuração padrão apenas no modo de desenvolvimento. Para cada provedor de identidade, essas credenciais são limitadas a 100 usos por
instância do {{site.data.keyword.appid_short_notm}}, por dia. Antes de publicar o seu aplicativo, atualize a
[configuração padrão](/docs/services/appid/identity-providers.html) para as suas próprias credenciais.
