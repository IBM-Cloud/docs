---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Configurando e usando o {{site.data.keyword.ssoshort}}

O serviço {{site.data.keyword.ssofull}} pode ser configurado para suportar provedores de autenticação do usuário alternativos para o {{site.data.keyword.iot_full}}.
{: .shortdesc}

O {{site.data.keyword.ssoshort}} suporta SAML 2.0, IBM Cloud Directory, provedores sociais (Facebook, LinkedIn, Google +) e Github. Para obter mais informações sobre o serviço SSO do {{site.data.keyword.Bluemix_notm}}, veja [Introdução ao Single Sign On ![Ícone de link externo](../../icons/launch-glyph.svg)](https://console.{DomainName}/docs/services/SingleSignOn/index.html){:new_window}.

## Configurando o {{site.data.keyword.ssoshort}}

Para configurar o {{site.data.keyword.ssoshort}} siga estas etapas:

1. Em seu painel {{site.data.keyword.Bluemix}}, inclua um serviço {{site.data.keyword.ssoshort}}.
2. Configure os provedores de autenticação a serem usados pelo serviço {{site.data.keyword.ssoshort}}.

## Crie um aplicativo simulado e ligue-o ao serviço {{site.data.keyword.ssoshort}}

O serviço {{site.data.keyword.ssoshort}} não pode ser ligado diretamente a outros serviços, então, um aplicativo simulado deve ser criado para recuperar os dados de configuração necessários do serviço {{site.data.keyword.ssoshort}}.

1. No painel {{site.data.keyword.Bluemix_notm}}, inclua o aplicativo {{site.data.keyword.sdk4nodefull}}.
2. Clique no aplicativo {{site.data.keyword.sdk4nodefull}} no painel {{site.data.keyword.Bluemix_notm}} e clique em **Ligar um serviço ou API**.
3. Selecione o serviço {{site.data.keyword.ssoshort}} e clique em **Incluir**.
4. O aplicativo {{site.data.keyword.sdk4nodefull}} deve agora ser estagiado novamente.
5. Clique no aplicativo {{site.data.keyword.sdk4nodefull}} no painel {{site.data.keyword.Bluemix_notm}}.
6. Selecione o serviço {{site.data.keyword.ssoshort}} e clique em **Integrar**.
7. Insira o retorno para URL:
`https://<orgid>.internetofthings.ibmcloud.com/get-ibmsso-access-token` em que `<orgid>` é o ID da sua organização {{site.data.keyword.iot_short_notm}}.

## Configurando o {{site.data.keyword.iot_short_notm}} for {{site.data.keyword.ssoshort}}

Após ligar e configurar o aplicativo {{site.data.keyword.sdk4nodefull}} e o serviço {{site.data.keyword.ssoshort}}, o {{site.data.keyword.iot_short_notm}} deve ser configurado. O {{site.data.keyword.iot_short_notm}} pode ser configurado usando a UI do {{site.data.keyword.iot_short_notm}} ou usando a API do {{site.data.keyword.iot_short_notm}}. As etapas a seguir devem ser executadas antes de configurar usando a UI ou a API:

1. Clique no aplicativo {{site.data.keyword.sdk4nodefull}} no painel {{site.data.keyword.Bluemix_notm}}.
2. Clique em **Variáveis de ambiente** na barra de navegação.
3. Copie o JSON exibido para um arquivo de texto provisório. O JSON deve ter o seguinte formato:
```
{
  "SingleSignOn": [
    {
        "name": "ssoServiceTest",
        "label": "SingleSignOn",
        "plan": "standard"
        "credentials": {
          "secret": "string",
          "tokenEndpointUrl": "string",
          "authorizationEndpointUrl": "string",
          "issuerIdentifier": "string",
          "clientId": "string",
          "serverSupportedScope": [
              "openid"
          ]
        }
    }
}
```

### Configurando o {{site.data.keyword.iot_short_notm}} para o {{site.data.keyword.ssoshort}} usando a UI

1. Abra o painel {{site.data.keyword.iot_short_notm}}.
2. Clique em **Extensões** na barra de navegação.
3. Clique em **Configurar** no ícone {{site.data.keyword.ssoshort}}.
4. Insira os dados de configuração do arquivo de texto provisório nos campos clientID, secret e issuerIdentifier.
5. Clique em **Pronto**.

### Configurando o {{site.data.keyword.iot_short_notm}} for {{site.data.keyword.ssoshort}} usando a API

Para configurar o {{site.data.keyword.iot_short_notm}} for {{site.data.keyword.ssoshort}} usando a API, o método deve ser `POST`, a URL deve ser
`https://<orgID>.internetofthings.ibmcloud.com/api/v0002/authentication/ssoconfig`, em que `<orgID>` é o ID da sua organização {{site.data.keyword.iot_short_notm}}. A autorização deve ser Sem Autorização ou Autorização básica, usando o ID e o token de chave API. O corpo deve conter os dados de configuração `secret`, `clientId`e `issuerIdentifier` como JSON no formato a seguir:
```
{
 "secret": "myclientpwd",
 "clientId": "myclientid",
 "issuerIdentifier": "mybmssoinstance.iam.ibmcloud.com"
}
```

Um status de 200 será retornado se a chamada API foi bem-sucedida.
