---

copyright:
  years: 2017 lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# Filtros de autorização e cabeçalhos
{: #auth}

O SDK do servidor {{site.data.keyword.appid_short}} fornece estratégias para proteger dois tipos de recursos: APIs e aplicativos da web.
{:shortdesc}


## Filtros de autorização
{: #auth-filter}

A estratégia de proteção de API retorna uma resposta HTTP 401 com uma lista de escopos para obter autorização para um cliente não autenticado. A estratégia de
proteção de aplicativo da web retorna um redirecionamento HTTP 302. O redirecionamento envia um cliente não autenticado para a página de login que é hospedada pelo
serviço do {{site.data.keyword.appid_short_notm}} ou diretamente para uma página de login do provedor de identidade, dependendo de sua configuração.



### Estratégia de API
{: #api}

A estratégia de API espera que as solicitações contenham um cabeçalho de autorização com um token de acesso válido. A resposta também pode incluir um token de
identidade, mas ele não é necessário; veja [Tokens de acesso e de identidade](/docs/services/appid/access-identity.html#access-and-identity).

Se um token for inválido ou estiver expirado, a estratégia de API retornará um erro HTTP 401 que conterá as informações a seguir: Www-Authenticate=Bearer
scope="{scope}" error="{error}". O componente `error` é opcional.

Se a solicitação retornar um token válido, o controle será transmitido para o próximo middleware e a propriedade `appIdAuthorizationContext`
será injetada no objeto de solicitação. Essa propriedade contém acesso e tokens de identidade originais, bem como informações de carga útil decodificadas como simples
objetos da JSON.


### Estratégia de aplicativo da web
{: #web}

Quando a classe de estratégia de aplicativo da web detectar tentativas não autenticadas para acessar um recurso protegido, ela automaticamente redirecionará um
navegador do usuário para a página de autenticação. Após a autenticação bem-sucedida, o usuário será retornado para a URL de retorno de chamada do aplicativo da web. O
serviço usa a classe de estratégia de aplicativo da web para obter tokens de acesso e de identidade. Após obter esses tokens, a classe de estratégia de aplicativo da
web armazena-os em uma sessão de HTTP sob `WebAppStrategy.AUTH_CONTEXT`. Cabe ao usuário decidir se deseja armazenar tokens de acesso e de identidade
no banco de dados de aplicativos.

## Cabeçalho de autorização
{: #auth-header}

O cabeçalho de autorização na solicitação recebida consiste em três partes que são separadas por espaços em branco: Portador, Token de acesso e ID do token. Token
de acesso é um componente obrigatório e Token de ID é opcional. A estrutura do cabeçalho esperada é: Authorization=Bearer {access_token} [{id_token}]
