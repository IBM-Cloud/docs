---

copyright:
  years: 2017
lastupdated: "2017-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Protegendo recursos de backend
{: #protecting-resources}

O SDK do servidor {{site.data.keyword.appid_short}} fornece estratégias para proteger dois tipos de recursos: APIs e aplicativos da web.
{:shortdesc}


## Acessando recursos protegidos por meio de SDKs do cliente
{: #accessing}

Chamar um recurso protegido ativa o widget de login, se necessário. Se um token válido já foi obtido, o widget de login não será ativado e o recurso será
acessado diretamente.


### Usando o SDK do Swift
{: #requesting-swift notoc}

1. Importe o BMSCore.

  ```swift
  import BMSCore
  ```
  {:pre}

2. Chame uma solicitação de recurso protegido.

  ```swift
  BMSClient.sharedInstance.initialize(bluemixRegion: AppID.<region>)
  BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid:AppID.sharedInstance)
  var request:Request =  Request(url: "<your protected resource url>")
  request.send(completionHandler: {(response:Response?, error:Error?) in
      //code handling the response here
  })
  ```
  {:pre}


### Usando o SDK do Android
{: #requesting-android notoc}

1. Chame uma solicitação de recurso protegido.

  ```java
  BMSClient bmsClient = BMSClient.getInstance();
  bmsClient.initialize(getApplicationContext(), AppID.REGION_UK);

  AppIDAuthorizationManager appIdAuthMgr = new AppIDAuthorizationManager(AppID.getInstance())
  bmsClient.setAuthorizationManager(appIdAuthMgr);

  Request request = new Request("<your protected resource url>", Request.GET);
  request.send(this, new ResponseListener() {
  @Override
		public void onSuccess (Response response) {
     //code handling the response here
  }
  @Override
		public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
      //code handling the failure here
  });
  ```
  {:pre}



## Filtros de autorização
{: #auth-filter}

A estratégia de proteção de API retorna uma resposta HTTP 401 com uma lista de escopos para obter autorização para um cliente não autenticado. A estratégia de
proteção de aplicativo da web retorna um redirecionamento HTTP 302. O redirecionamento envia um cliente não autenticado para a página de login que é hospedada pelo
serviço do {{site.data.keyword.appid_short_notm}} ou diretamente para uma página de login do provedor de identidade, dependendo de sua configuração.



### Estratégia de API
{: #api notoc}

A estratégia de API espera que as solicitações contenham um cabeçalho de autorização com um token de acesso válido. A resposta também pode incluir um token de
identidade, mas ele não é necessário; veja [Tokens de acesso e de identidade](/docs/services/appid/about.html#acess-and-identity).

Se um token for inválido ou estiver expirado, a estratégia de API retornará um erro HTTP 401 que conterá as informações a seguir: Www-Authenticate=Bearer
scope="{scope}" error="{error}". O componente `error` é opcional.

Se a solicitação retornar um token válido, o controle será transmitido para o próximo middleware e a propriedade `appIdAuthorizationContext`
será injetada no objeto de solicitação. Essa propriedade contém acesso e tokens de identidade originais, bem como informações de carga útil decodificadas como simples
objetos da JSON.


### Estratégia de aplicativo da web
{: #web notoc}

Quando a classe de estratégia de aplicativo da web detectar tentativas não autenticadas para acessar um recurso protegido, ela automaticamente redirecionará um
navegador do usuário para a página de autenticação. Após a autenticação bem-sucedida, o usuário será retornado para a URL de retorno de chamada do aplicativo da web. O
serviço usa a classe de estratégia de aplicativo da web para obter tokens de acesso e de identidade. Após obter esses tokens, a classe de estratégia de aplicativo da
web armazena-os em uma sessão de HTTP sob `WebAppStrategy.AUTH_CONTEXT`. Cabe ao usuário decidir se deseja armazenar tokens de acesso e de identidade
no banco de dados de aplicativos.

## Cabeçalho de autorização
{: #auth-header}

O cabeçalho de autorização na solicitação recebida consiste em três partes que são separadas por espaços em branco: Portador, Token de acesso e ID do token. Token
de acesso é um componente obrigatório e Token de ID é opcional. A estrutura do cabeçalho esperada é: Authorization=Bearer {access_token} [{id_token}]
