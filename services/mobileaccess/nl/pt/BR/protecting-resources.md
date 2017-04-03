---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-15"

---

{:shortdesc: .shortdesc}
{:codeblock:.codeblock}

O serviço {{site.data.keyword.amafull}} foi substituído pelo serviço {{site.data.keyword.appid_full}}.

# Protegendo recursos de backend com o serviço {{site.data.keyword.amashort}}
{: #protecting-resources}


Com o serviço {{site.data.keyword.amafull}}, é possível proteger seus aplicativos backend Node.js e baseados em Java que estão em execução no {{site.data.keyword.Bluemix_notm}} com a segurança e o monitoramento de OAuth ativados pelo dispositivo móvel.
{:shortdesc}

## Antes de iniciar
{: #before-you-begin}
Antes de iniciar, assegure-se de que o serviço Node.js exista em seu aplicativo backend {{site.data.keyword.Bluemix_notm}}.


## Filtro de autorização
{: #auth-filter}
O {{site.data.keyword.amashort}} server SDK tem filtros de autorização que podem ser usados para proteger seus aplicativos backend.  O filtro de autorização intercepta solicitações recebidas e valida se um cabeçalho de autorização estiver presente. Se o cabeçalho de autorização não estiver presente ou for inválido, o filtro retorna uma resposta com HTTP 401. O
SDK cliente {{site.data.keyword.amashort}} sabe como interceptar uma resposta HTTP 401 que é retornada pelo SDK do servidor
{{site.data.keyword.amashort}} e aciona o fluxo de autenticação.
## Cabeçalho de autorização
{: #auth-header}
O cabeçalho de autorização na solicitação recebida consiste em três partes: Condutor, Token de acesso e Token do ID, que são separados por espaços em branco. `Token de acesso` é um componente obrigatório, enquanto que `Token do ID` é opcional.

O cabeçalho de autorização recebido é processado pelo respectivo filtro de autorização. O filtro valida as assinaturas do token de acesso e do token do ID, a data de expiração e a integridade estrutural. Depois que a validação é aprovada, um objeto de contexto de segurança é incluído no objeto da solicitação. É possível obter uma referência para o contexto de segurança usando a API relevante.

O contexto de segurança contém o assunto, usuário, dispositivo e as informações do aplicativo armazenadas com uma estrutura a seguir:
```JSON
{
    "imf.sub":"myclientid",
    "imf.user": {
        "id":"user-name",
        "authBy":"myrealm",
        "displayName":"display-name"
    },
    "imf.device": {
        "id":"device-id",
        "platform":"iOSnative",
        "model":"device-model",
        "osVersion":"device-os"
    },
    "imf.application": {
        "id":"ios.bundle.id",
        "version":"1.0"
    }
}
```
{: codeblock}

* `imf.sub`: especificará o assunto do token do ID ou o ID exclusivo do cliente se nenhum token de ID existir.
* `imf.user`: especifica a identidade do usuário que é extraída do token do ID. Se não existir nenhum token de ID, esse campo reterá um objeto vazio.
* `imf.device`: especifica a identidade do dispositivo que é extraída do token do ID. Se não existir nenhum token de ID, esse campo reterá um objeto vazio.
* `imf.application`: especifica a identidade do aplicativo que é extraída do token do ID. Se não existir nenhum token de ID, esse campo reterá um objeto em branco.

## Próximas etapas
{: #next-steps}
* [Protegendo recursos de Node.js](protecting-resources-nodejs.html)
* [Protegendo os recursos do Liberty for Java&trade;](protecting-resources-java.html)
* [Desenvolvimento local](protecting-resources-local.html)
