---

copyright:
  year: 2016, 2017
lastupdated: "2017-04-06"

---

**Importante: o serviço {{site.data.keyword.amafull}} foi substituído pelo serviço {{site.data.keyword.appid_full}}.**

# Ativando a autenticação do Google para apps da web
{: #google-auth-web}

Use o Google Sign-In para autenticar usuários em seu app da web.


## Antes de iniciar
{: #before-you-begin}

Você deve ter:
* Um app da web.
* Uma instância de um aplicativo {{site.data.keyword.Bluemix_notm}} que seja protegida pelo serviço {{site.data.keyword.amashort}}. Para obter mais informações sobre como criar um backend do {{site.data.keyword.Bluemix_notm}}, consulte [Introdução](index.html).

## Configurando um aplicativo Google para seu website
Para iniciar o uso do Google como um provedor de identidade, crie um projeto no [Console do desenvolvedor do Google](https://console.developers.google.com). Parte da criação de um projeto é obter um identificador de cliente e um segredo do Google. O identificador de cliente e o segredo do Google são os identificadores exclusivos para seu aplicativo usados pela autenticação do Google e são necessários para configurar o aplicativo {{site.data.keyword.Bluemix_notm}}.

1. Crie um projeto usando a API do Google+.
1. Crie credenciais usando **OAuth**. Para criar as credenciais, é necessário:
    * Selecionar o tipo de aplicativo **aplicativo da web**.
    * Fornecer o valor **Authorized redirect URIs**:

     https://imf-newauthserver.bluemix.net/oauth/{bluemix_app_guid}/callback
1. Conclua a criação de credenciais e anote o identificador de cliente e o segredo do Google.


## Configurando o Mobile Client Access para autenticação do Google
Depois de ter um ID de aplicativo e um segredo do Google, é possível ativar a autenticação do Google no painel do {{site.data.keyword.amashort}}.

1. Abra seu app no painel do {{site.data.keyword.Bluemix_notm}}.
1. Clique no ladrilho {{site.data.keyword.amashort}}. O painel do {{site.data.keyword.amashort}} é carregado.
1. Clique no quadro Google.
1. Insira o identificador de cliente e o segredo do Google e salve.


## Usando o Mobile Client Access para autenticação da web do Google
Para iniciar o processo de autorização:

1. Redirecione de seu app da web para o terminal do servidor de autorizações a seguir:  
  https://imf-newauthserver.bluemix.net/oauth/v2/authorization

  usando os parâmetros de consulta a seguir:
	```
   response_type='authorization_code'
   client_id= <bluemix_app_guid>
   redirect_uri= <uri which you want to return to after getting a grant code>
   scope= ‘openid’
   state= <state>
	```

  O parâmetro `state` não está em uso por enquanto e pode permanecer vazio.

  O URI do parâmetro `redirect_uri` é o redirecionamento após a autenticação bem-sucedida ou com falha com o Google.
  A resposta obtida após o redirecionamento contém o código de autorização nos parâmetros de consulta da solicitação.
1. Faça uma solicitação `POST` para o terminal de token do servidor de autorizações:

 https://imf-newauthserver.bluemix.net/oauth/v2/token


  usando os parâmetros de consulta a seguir:

	```
  	grant_type=’authorization_code’
    client_id= < bluemix_app_guid >
    redirect_uri= <redirect_uri >
    code= <authorization code>
	```
  O parâmetro `redirect_uri` deve corresponder ao `redirect_uri` da etapa 1 e o valor `<authorization code>` é recebido da resposta.
  Certifique-se de enviar esta solicitação `POST` no período de 10 min, uma vez que o código de concessão é válido por 10 min, no máximo.

O corpo de resposta `POST` deve conter o `access_token` e o `id_token` codificados em base64.

## Testando a Autenticação

Agora é possível começar a fazer solicitações para seus recursos protegidos.
Toda solicitação para recursos protegidos deve conter o token de acesso no campo de cabeçalho da solicitação de autorização.
