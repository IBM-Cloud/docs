---

copyright:
  years: 2017
lastupdated: "2017-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# Sobre {{site.data.keyword.appid_short_notm}}
{: #gettingstarted}

Com o {{site.data.keyword.appid_full}} os desenvolvedores podem proteger e incluir a autenticação em seus apps {{site.data.keyword.Bluemix}},
com algumas linhas de código. Os desenvolvedores também podem gerenciar dados específicos do usuário para construir experiências personalizadas de app.
{:shortdesc}


É possível usar o serviço das maneiras a seguir:

* Para incluir autenticação em seus aplicativos móveis e da web
* Para conceder acesso a recursos de backend protegidos e aplicativos da web
* Para proteger aplicativos Node.js e Swift que estão hospedados no {{site.data.keyword.Bluemix_notm}}
* Para armazenar dados do usuário, como preferências de app ou informações de seus perfis sociais públicos
* Para usar dados armazenados para construir experiências personalizadas de app
* Para proteger recursos para usuários autenticados e anônimos

**Nota**: os protocolos implementados são totalmente compatíveis com o OpenID Connect (OIDC).


## Componentes
{: #components}

* Painel - Faça download de amostras de migração, veja logs de atividade, configure vários tipos de autenticação e provedores de identidade
* SDK do cliente - Compile apps móveis e da web que usem o serviço para implementar a autenticação do usuário
    * Pré-requisitos para Android: API 25 ou superior, Java 8.x, ferramentas do Android SDK 25.2.5 ou superior, Android SDK Platform Tools 25.0.3 ou superior,
Android Build Tools versão 25.0.2
    * Pré-requisitos para iOS: iOS9 ou superior, MacOS 10.11.5, Xcode 8,2
* SDK do servidor - Proteja os recursos que são hospedados no {{site.data.keyword.Bluemix_notm}}
    * Os tempos de execução suportados são Node.js e Swift

## Visão geral da arquitetura

Fluxo do ![{{site.data.keyword.appid_short_notm}}](/images/appid_flow.png)

Figura 1. Diagrama de arquitetura do {{site.data.keyword.appid_short_notm}}

É possível proteger os seus recursos em nuvem com o SDK do servidor {{site.data.keyword.appid_short_notm}}. Use a classe de solicitação que é fornecida
pelo SDK do cliente do {{site.data.keyword.appid_short_notm}} para se comunicar com os seus recursos em nuvem protegidos.

* O SDK do servidor detecta uma solicitação não autorizada e retorna o desafio de autorização HTTP 401.
* O SDK do cliente detecta um Desafio de autorização HTTP 401 e inicia automaticamente o processo de autenticação com base na configuração dos provedores de
identidade.
* A autenticação é tentada de acordo com os provedores de identidade configurados atualmente
* Após a autenticação bem-sucedida, o serviço retorna tokens de autorização e identidade.
* O SDK do cliente inclui automaticamente o token de autorização na solicitação original e reenvia a solicitação para o recurso em nuvem.
* O SDK do servidor extrai o token de acesso da solicitação e a valida com o {{site.data.keyword.appid_short_notm}}.
O acesso é concedido e a resposta é retornada ao aplicativo.

<!--## Sequence diagrams
{: #sequence-diagrams}

[Anton?]-->

## Tokens de acesso e de identidade
{: #access-and-identity}

O {{site.data.keyword.appid_short}} usa dois tipos de tokens: de acesso e de identidade. Os tokens são formatados como
<a href="https://jwt.io/introduction/" target="_blank">Tokens da web da JSON <img src="../../icons/launch-glyph.svg" alt="ícone de Link externo"></a>.


### Token de Acesso
{: #access-tokens notoc}

O token de acesso permite a comunicação com os recursos protegidos pelos filtros de autorização do {{site.data.keyword.appid_short_notm}}; veja
[Protegendo recursos](/docs/services/appid/protecting-resources.html).
O token adequa-se às especificações do JavaScript Object Signing and Encryption (JOSE) e tem o formato a seguir:

```
Header: {

    "typ": "JOSE", // header type, according to spec

    "alg": "RS256", // algorithm, according to spec

}
Payload: {

    "iss": "", // issuer, the AppID server that issued this token. StringOrURL

    "sub": "", // subject, who this token was issued to. Most probably userId

    "aud": "", // audience, who is this token intended for. OAuth2 client_id.

    "exp: "", // expiration timestamp, epoch time

    "iat": "", // issued at timestamp, epoch time

    "tenant": "xxx", the AppID tenantId the token was issued for

    "auth_by": "appid_anon / appid_facebook / appid_google",

    "scope": "", // the scope[s] this token was issued for

}
```
{:screen}

### Token de identidade
{: #identity-tokens notoc}

O token de identidade contém informações sobre o usuário, incluindo nome, e-mail, sexo, foto e local.

```
Header: {
    "typ": "JOSE", // header type, according to spec
    "alg": "RS256", // algorithm, according to spec
} Payload: {
    "iss": "", // issuer, the AppID server that issued this token. StringOrURL
    "sub": "", // subject, who this token was issued to. AppID userid.

    "aud": "", // audience, who is this token intended for. OAuth2 client_id.
    "exp: "", // expiration timestamp, epoch time
    "iat": "", // issued at timestamp, epoch time
    "tenant": "xxx", // the AppID tenantId the token was issued for

    "name": "John Smith", // user's full name as reported by IDP, mandatory,

    "email": "js@mail.com", // user's email as reported by IDP, only if available,

    "gender", "male", // user's gender as reported by IDP, only if available,

    "locale": "en", // user's locale as reported by IDP, only if available

    "picture": "https://url.to.photo", // URL to user's picture, only if available

    "auth_by": "appid_facebook/appid_google", // the name of IDP used for authentication, mandatory

    "identities": [

        "provider: "appid_facebook/appid_google", // mandatory

        "id": "unique user id as reported by IDP", // mandatory

        "profile": { ... } // JSON object returned by IDP,  mandatory

      },

      {...}, {...} // more linked identities

    ],

    "oauth_client":{

      "type": "serverapp/mobileapp from client registration", // mandatory

      "name": "client_name as reported during client registration", // mandatory

      "software_id": "software_id as reported during client registration", // mandatory

      "software_version": "software_version as reported during client registration", // mandatory

      "device_id": "device_id from client registration", //mobile only

      "device_model": "device_model from client registration", //mobile only

      "device_os": "device_os from client registration", //mobile only

    }

}
```
{:screen}


## Visão geral de provedores de identidade
{: #identity-providers-overview}

É possível usar os provedores de identidade a seguir em seus aplicativos móveis e da web:

* **Facebook** - os seus usuários efetuam login no app móvel ou da web com suas credenciais do Facebook.
* **Google** - os seus usuários efetuam login no app móvel ou da web com suas credenciais do Google+.
<!--* **Custom** - Bring your own identity provider. The identity providers should be compliant with OIDC. -->

## Usando a configuração padrão
{: #default-configuration}

O {{site.data.keyword.appid_short_notm}} fornecerá uma configuração padrão quando você inicialmente configurar os seus provedores de identidade. É
possível usar a configuração padrão apenas no modo de desenvolvimento. Para cada provedor de identidade, essas credenciais são limitadas a 100 usos por
instância do {{site.data.keyword.appid_short_notm}}, por dia. Antes de publicar o seu aplicativo, atualize a configuração padrão para as suas próprias
credenciais. Para atualizar a sua configuração, veja [configurando provedores de identidade](/docs/services/appid/identity-providers.html).
