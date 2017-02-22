---

copyright:
  year: 2016, 2017
lastupdated: "2017-01-08"

---

# Ativando a autenticação do Facebook para apps da web
{: #facebook_web}

Use o Facebook para autenticar usuários em seu app da web.

## Antes de iniciar
{: #facebook-auth-android-before}
Você deve ter:
* Um app da web.  
* Uma instância de um aplicativo {{site.data.keyword.Bluemix_notm}} que seja protegida pelo serviço {{site.data.keyword.amashort}}. Para obter mais informações sobre como criar um backend do {{site.data.keyword.Bluemix_notm}}, consulte [Introdução](index.html).
* Um ID de aplicativo e um segredo de app do Facebook. Para obter mais informações, consulte [Obtendo um ID do aplicativo Facebook do Portal do Desenvolvedor do Facebook](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID).


## Configurando um aplicativo Facebook para seu website
Para usar o Facebook como provedor de identidade em seu website, deve-se incluir e configurar a plataforma website no aplicativo Facebook.

1. Abra o aplicativo Facebook no Portal do Desenvolvedor do Facebook.
1. Anote o ID do aplicativo para seu app e o segredo do app. Esse valor é necessário ao configurar seu projeto da web para autenticação do Facebook.
1. Na página **Configurações**, clique em **Incluir plataforma** e escolha **Website**.
1. Salve as mudanças.
1. Clique em **Login do Facebook** na barra lateral esquerda.
1. Insira o terminal de retorno de chamada do servidor de autorizações na caixa **URIs de redirecionamento válidos de OAuth**: https://imf-newauthserver.bluemix.net/oauth/{bluemix_app_guid}/callback. Salve as mudanças.




# Configurando o {{site.data.keyword.amashort}} para autenticação do Facebook
Depois que você tiver o ID de aplicativo e o segredo de app do Facebook e o aplicativo Facebook tiver sido configurado para atender Web clients, será possível ativar a autenticação do Facebook no painel do {{site.data.keyword.Bluemix_notm}}.

1. Abra seu app no painel do {{site.data.keyword.Bluemix_notm}}.
1. Clique no ladrilho {{site.data.keyword.amashort}}. O painel do {{site.data.keyword.amashort}} é carregado.
1. Clique no quadro Facebook.
1. Insira o ID de aplicativo e o segredo de app do Facebook e salve.




## Usando o Mobile Client Access para autenticação da web do Facebook

Para iniciar o processo de autorização:

1. Redirecione de seu app da web para o terminal do servidor de autorizações a seguir: https://imf-newauthserver.bluemix.net/oauth/v2/authorization.

1. Inclua os parâmetros de consulta a seguir:
   ```
    response_type='authorization_code'
    client_id= <bluemix_app_guid>
    redirect_uri= <uri for redirecting after receiving the authorization code>
    scope= 'openid'
    state= <state>
    ```


  O parâmetro `state` não está em uso por enquanto e pode permanecer vazio.
  O parâmetro `redirect_uri` é o URI para redirecionamento após a autenticação bem-sucedida ou com falha com o Facebook.

1. Após o redirecionamento para o terminal de autorização, você obterá um formulário de login
do      
   Facebook. Insira o nome do usuário e a senha para redirecionar para o `redirect_uri`.
   A resposta obtida após o redirecionamento contém o código de autorização nos parâmetros de consulta da solicitação.

1. Faça uma solicitação `POST` para o terminal de token do servidor de autorizações:

  https://imf-newauthserver.bluemix.net/oauth/v2/token

  usando os parâmetros de consulta a seguir:
  ```
  grant_type='authorization_code'
  client_id= <bluemix_app_guid>
  code= <authorization code>
  ```
O parâmetro `redirect_uri` deve corresponder ao `redirect_uri` da etapa 2.
O valor `code` é o código de autorização recebido na resposta no final da etapa 3.
Certifique-se de enviar esta solicitação `POST` no período de 10 min, uma vez que o código de autorização é válido durante 10 min, no máximo.

  O corpo de resposta `POST` deve conter o `access_token` e o `id_token` codificados em base64.

## Testando a Autenticação
Agora é possível começar a fazer solicitações para seus recursos protegidos.
Toda solicitação para recursos protegidos deve conter o `access_token` no campo de cabeçalho da solicitação de autorização.
