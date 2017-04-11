---

copyright:
  years: 2017 lastupdated: "2017-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Configurando provedores de identidade
{: #setting-up-idp}

É possível configurar o Facebook, o Google ou ambos para autenticar os seus aplicativos e autorizar o acesso aos recursos de backend protegidos.
{:shortdesc}


## Facebook
{: #facebook}

Configure o serviço do {{site.data.keyword.appid_short}} para usar o Facebook como um provedor de identidade.

<!--- ### Sequence diagram
{: #facebook-sequence-diagram}--->

### Obtendo um ID do app e segredo por meio do Facebook
{: #getting-facebook-appid}

Para usar o Facebook como um provedor de identidade em seus apps móveis ou da web, deve-se incluir e configurar a plataforma do website em seu aplicativo
Facebook.

1. Efetue login em sua conta no site Facebook for Developers. Para obter informações sobre como criar um novo app Facebook, veja <a href="https://developers.facebook.com/docs/apps/register" target="_blank">Criando um aplicativo <img src="../../icons/launch-glyph.svg" alt="ícone de Link externo"></a>.
2. Tome nota do ID e do segredo do app Facebook. Você precisa desses valores para configurar o seu projeto da web para autenticação em seu painel de serviço.
3. Inclua a plataforma da web e insira a URL do site.
4. Na lista de produtos, selecione **Login do Facebook**.
5. No campo URLs válidas de redirecionamento de OAuth, insira a URL de terminal de retorno de chamada de servidor de autorizações. É possível incluir este valor depois de ter configurado seu serviço
{{site.data.keyword.appid_short_notm}} nas etapas seguintes.
6. Clique em **Salvar mudanças**.

### Configurando o {{site.data.keyword.appid_short_notm}} para autenticação do Facebook
{: #configuring-facebook-appid}

Quando você tiver o seu ID e segredo do app Facebook e o seu app Facebook for Developers estiver configurado para entregar Web clients, será possível editar
a autenticação do Facebook em seu painel de serviço.

1. Na guia **Gerenciar** de seu painel de serviço, selecione **Facebook** e clique em **Editar**.
2. Insira o ID e segredo do app Facebook que você obteve por meio do website do Facebook for Developers.
3. Copie o URI que estiver no campo **URI de redirecionamento para o Facebook for Developers**. Cole o URI no campo **URIs válidos de
redirecionamento de OAuth** na seção **Login do Facebook** do Facebook Developers Portal.
4. Clique em **Salvar**.
5. Opcional: para configurar a autenticação para apps da web, insira o URI de redirecionamento nos seus URIs de redirecionamento de aplicativo da web. Esse
valor é determinado pelo desenvolvedor e usado para acessar o URI de redirecionamento após o processo de autorização ser concluído.


## Google
{: #google}

Configure o serviço do {{site.data.keyword.appid_short_notm}} para usar o Google como um provedor de identidade.

<!--- ### Sequence diagram
{: #google-sequence-diagram}--->

### Obtendo um identificador de cliente e segredo por meio do Google
{: #google-client-id}

Para usar o Google como um provedor de identidade, obtenha um identificador de cliente e segredo do Google e crie um projeto no Google Developer Console.

1. Abra seu aplicativo Google no Google Developer Console.
2. Inclua a API do Google+.
3. Crie credenciais usando o OAuth. No campo **Tipo de aplicativo**, selecione **Aplicativo da web**. No campo
**URIs de redirecionamento autorizados**, insira o URI de redirecionamento de ID do App. É possível obter o URI de autorização de redirecionamento
de ID do App por meio da tela de configuração do Google do painel de serviço.
4. Salve as suas mudanças. Tome nota do identificador de cliente e segredo do Google.




### Configurando o {{site.data.keyword.appid_short_notm}} para autenticação do Google
{: #google-client-appid}

Quando você tiver o seu identificador de cliente e segredo do Google e o seu console do Google Developers estiver configurado para entregar Web clients, será
possível editar a autenticação do Google em seu painel de serviço.

1. Na guia **Gerenciar** de seu painel de serviço, selecione **Google** e clique em **Editar**.
3. Insira o Identificador de cliente e Segredo do Google que você obteve por meio do console do Google Developers.
4. Copie o URI que estiver no campo **URI de redirecionamento para o Google for Developers**. Cole o URI no campo **URIs
de redirecionamento autorizados** que estiver sob **Restrições** na seção **Identificador de cliente para aplicativo da
web** do Google Developers Portal.
5. Clique em **Salvar**.
6. Opcional: para configurar a autenticação para apps da web, insira o URI de redirecionamento no campo de URIs de redirecionamento de aplicativo da web. Esse
valor é determinado pelo desenvolvedor e usado para acessar o URI de redirecionamento após o processo de autorização ser concluído.



<!---[## Bring your own OAuth2/OIDC identity provider
{: #oauth2}

### About
{: #oauth2-about}
### Sequence diagram
{: #oauth2-sequence-diagram}
### Configuring AppID for BYOIDP OAuth2 authentication
{: #oauth2-appid} SHAWNA: Is this Interconnect?]--->
