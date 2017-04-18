---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-15"

---

O serviço {{site.data.keyword.amafull}} foi substituído pelo serviço {{site.data.keyword.appid_full}}.

# Autenticação customizada do app da web
{: #custom-web}

Inclua a autenticação customizada em seu app da web

## Antes de iniciar
{: #before-you-begin}

Você deve ter:
* Um app da web com um terminal `/apps/:Guid/<RealmName>/handleChallengeAnswer`, que
retorna uma identidade do usuário no sucesso da autenticação. A estrutura JSON de identidade do usuário deve ser como a seguir:

   ```json
  userIdentity: {
  userName: <username>,
  displayName: <displayName>;
 };
```
* Uma instância de um aplicativo {{site.data.keyword.Bluemix_notm}} que seja protegida pelo serviço {{site.data.keyword.amashort}}. Para obter mais informações sobre como criar um backend do {{site.data.keyword.Bluemix_notm}}, consulte [Introdução](index.html).



## Configurando um aplicativo {{site.data.keyword.amashort}} para autenticação customizada


1. Abra seu app no painel do {{site.data.keyword.Bluemix_notm}}.
1. Clique no ladrilho {{site.data.keyword.amashort}}. O painel do {{site.data.keyword.amashort}} é carregado.
1. Clique no Tile customizado.
1. Insira a **região customizada**, a **URL do provedor de identidade customizado** e
**redirect_uri**. Clique em Salvar.

## Usando o {{site.data.keyword.amashort}} para autenticação da web customizada

Para iniciar o processo de autorização:

1. Redirecione de seu app da web para o terminal do servidor de autorizações a seguir:

    https://imf-newauthserver.bluemix.net/oauth/v2/authorization

  usando os parâmetros de consulta a seguir:
   ```
   response_type=’authorization_code’
   client_id= <bluemix\_app\_guid>
   redirect_uri= <uri for the redirect after getting an authorization code>
   scope= ‘openid’
   state= <state>
   ```

    O parâmetro `state` não está em uso no momento e pode ficar vazio.

    O parâmetro `redirect_uri` determina o redirecionamento após a autenticação bem-sucedida ou com falha do provedor de identidade customizado.

1. Após redirecionar para o terminal de autorização, você obtém um formulário de login. Insira o nome do usuário e a senha para iniciar a autenticação
em seu provedor de identidade e um redirecionamento para o `redirect_uri`.
A resposta retornada após uma autenticação bem-sucedida contém o código de autorização nos parâmetros de consulta da solicitação.

4. Faça uma solicitação `POST` para o terminal de token do servidor de autorizações:

 https://imf-newauthserver.bluemix.net/*oauth/v2/token

 usando os parâmetros de consulta a seguir:
 ```
 grant_type = 'authorization_code'
 client_id = <bluemix_app_guid>
 redirect_uri = <redirect_uri>
 code = <authorization code>
 ```
  O parâmetro `redirect_uri` deve corresponder ao `redirect_uri` da etapa 1. O código de autorização foi retornado pela solicitação na etapa 2.

  Certifique-se de enviar esta solicitação `POST` no período de 10 min, uma vez que o código de concessão é válido por 10 min, no máximo.

O corpo de resposta `POST` contém o *access_token* e o
*id_token* codificados em base64.

## Testando a Autenticação


Agora é possível começar a fazer solicitações para seus recursos protegidos.
Todas as solicitações para recursos protegidos devem conter o `access_token`.
Envie o token de acesso no campo de cabeçalho `the-Authorization-request`.
