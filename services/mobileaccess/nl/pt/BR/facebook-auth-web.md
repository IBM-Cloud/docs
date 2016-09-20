---

copyright:
  year: 2016

---

# Ativando a autenticação do Facebook para aplicativos da web

Última atualização: 27 de julho de 2016
{: .last-updated}

Use o Facebook para autenticar usuários em seu app da web. Inclua a funcionalidade de segurança do {{site.data.keyword.amashort}}. 

## Antes de começar
{: #facebook-auth-android-before}
Você deve ter:

* Um app da web. 
* Uma instância de um aplicativo {{site.data.keyword.Bluemix_notm}} que é protegida pelo serviço {{site.data.keyword.amashort}}. Para obter mais informações sobre como criar um aplicativo backend do {{site.data.keyword.Bluemix_notm}}, consulte [Introdução](index.html).
* O URI para o redirecionamento final (após o processo de autorização ser concluído).


## Configurando um aplicativo Facebook para seu website
Para usar o Facebook como um provedor de identidade em seu website, deve-se incluir e configurar a plataforma do website em seu aplicativo Facebook.

1. Efetue login no [Portal de desenvolvedores do Facebook](https://developers.facebook.com).
2. Abra ou crie seu aplicativo.
3. Observe o **ID do aplicativo** e o **Segredo do aplicativo**. Esses valores são necessários ao
configurar seu projeto da web para autenticação do Facebook no painel {{site.data.keyword.amashort}}.
4. Inclua a plataforma **Website**, se não existir.
5. Inclua ou abra o **Login do Facebook** na lista Produtos.
6. Insira o URI do terminal de retorno de chamada do servidor de autorizações na caixa **URIs de redirecionamento de OAuth válidos**. Localize esse URI de redirecionamento de autorização nas etapas de configuração do painel {{site.data.keyword.amashort}} a seguir.
7. Salve as mudanças.




## Configurando o {{site.data.keyword.amashort}} para autenticação do Facebook
Depois que você tiver o ID de aplicativo e o segredo de app do Facebook e o aplicativo Facebook tiver sido configurado para atender Web clients, será possível ativar a autenticação do Facebook no painel do {{site.data.keyword.Bluemix_notm}}.

1. Abra o painel {{site.data.keyword.Bluemix_notm}}.
2. Clique no quadro do app relevante para carregar o app.
3. Clique no tile para o serviço {{site.data.keyword.amashort}}.
4. Clique no botão **Configurar** no painel **Facebook**.
5. Observe o valor na caixa de texto **URI de redirecionamento do Mobile Client Access para o Facebook Developer Console**. Você precisará desse valor para incluir na caixa **URIs de redirecionamento de OAuth válidos** no **Login do Facebook** do Portal de desenvolvedores do Facebook na etapa seis de Configurando um aplicativo Facebook para seu website.
6. Insira o **ID do aplicativo** e **Segredo do aplicativo** do Facebook.
7. Insira o URI de redirecionamento nos **URIs de redirecionamento de aplicativo da web**. Esse valor é para que o URI de
redirecionamento seja acessado após o processo de autorização ser concluído e é determinado pelo desenvolvedor.
8. Clique em **Salvar**.




## Implementar o fluxo de autorização do {{site.data.keyword.amashort}} usando o Facebook como provedor de identidade

A variável de ambiente `VCAP_SERVICES` é criada automaticamente para cada instância de serviço do
{{site.data.keyword.amashort}} e contém propriedades necessárias para o processo de autorização. Ela consiste em um objeto JSON e pode ser visualizada clicando em **Variáveis de ambiente** em <!--the left-side navigator of--> seu aplicativo.

Para iniciar o processo de autorização:

1. Recupere o terminal de autorização (`authorizationEndpoint`) e o identificador de cliente (`clientId`) das credenciais de serviço armazenadas na variável de ambiente `VCAP_SERVICES`. 

    **Nota:** caso tenha criado o serviço {{site.data.keyword.amashort}} antes de o suporte da web ser
incluído, não será possível ter terminais de autorização nas credenciais de serviço. Neste caso, use os terminais de autorização a seguir
dependendo da região do Bluemix:
  
  Sul dos EUA: 
  ```
  https://mobileclientaccess.ng.bluemix.net/oauth/v2/authorization
   ```
  Londres: 
   ``` 
 https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/authorization
   ```
  Sydney: 
    ```
 https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/authorization
  ```
2. Construa o URI do servidor de autorizações usando `response_type("code")`, `client_id` e
`redirect_uri` como parâmetros de consulta. 
3. Redirecione a partir do seu aplicativo da web para o URI gerado.



O exemplo a seguir recupera os parâmetros da variável `VCAP_SERVICES`, construindo a URL e enviando a solicitação de redirecionamento.

  ```Java
  var cfEnv = require("cfenv"); 

  app.get("/protected", checkAuthentication, function(req, res, next){  
      res.send("Hello from protected endpoint"); 
    }
  ); 
  
  function checkAuthentication(req, res, next){
  // Check if user is authenticated 
  
    if (req.session.userIdentity){   
       next()  
     } else {   
  // If not - redirect to authorization server   
        var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;   
        var authorizationEndpoint = mcaCredentials.authorizationEndpoint;   
        var clientId = mcaCredentials.clientId;   
        var redirectUri = "http://some-server/oauth/callback"; 
         // Your web application redirect URI   

        var redirectUrl = authorizationEndpoint + "?response_type=code";
        redirectUrl += "&client_id=" + clientId;   
        redirectUrl += "&redirect_uri=" + redirectUri;   
  
        res.redirect(redirectUrl);  
  
      } 
  }
  
 ```

   O parâmetro `redirect_uri` é o URI para redirecionamento, após a autenticação bem-sucedida ou malsucedida com o Facebook.
   

 Após redirecionar para o terminal de autorização, o usuário obterá um formulário de login do Facebook. Após o Facebook autorizar a
identidade do usuário, o serviço {{site.data.keyword.amashort}} chamará seu URI de redirecionamento de aplicativo da web, fornecendo o
código de concessão como um parâmetro de consulta.  

## Obtendo os tokens

A próxima pintura é obter o acesso e os tokens de identidade usando o código de concessão recebido anteriormente:

 1.  Recupere o token `tokenEndpoint`, `clientId` e `secret` das credenciais de serviço
na variável de ambiente `VCAP_SERVICES`. 
 
    **Nota:** se você usou o {{site.data.keyword.amashort}} antes de o suporte da web ter sido incluído, talvez você não tenha um terminal de token nas credenciais de serviço. Como alternativa, use as URLs a seguir, dependendo de sua região do Bluemix: 

    Sul dos EUA: 
    ```
    https://mobileclientaccess.ng.bluemix.net/oauth/v2/token 
     ```
    Londres: 
      ```
    https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/token  
     ```
    Sydney: 
      ```
    https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/token 
    ```

 1. Envie uma solicitação de post ao URI do servidor de token com tipo de concessão ("authorization_code"), `clientId` e o URI de redirecionamento como parâmetros de formulário. Envie
`clientId` e `secret` como credenciais de autenticação HTTP básicas.
 
O código a seguir recupera os valores necessários e os envia com uma solicitação de post.

  ```Java
  var cfEnv = require("cfenv");
  var base64url = require("base64url ");
  var request = require('request');
  
  app.get("/oauth/callback", function(req, res, next){ 
    var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials; 
    var tokenEndpoint = mcaCredentials.tokenEndpoint; 
    var formData = { 
      grant_type: "authorization_code", 
      client_id: mcaCredentials.clientId, 
      redirect_uri: "http://some-server/oauth/callback",
     // Your web application redirect uri 
      code: req.query.code 
   } 

 
    request.post({ 
        url: tokenEndpoint, 
        formData: formData 
      }, function (err, response, body){ 
        var parsedBody = JSON.parse(body); 
        req.session.accessToken = parsedBody.access_token; 
        req.session.idToken = parsedBody.id_token; 
        var idTokenComponents = parsedBody.id_token.split("."); 
        // [header, payload, signature] 
        var decodedIdentity= base64url(idTokenComponents[1]);
        req.session.userIdentity = JSON.parse(decodedIdentity)["imf.user"]; 
        res.redirect("/"); 
        }
   ).auth(mcaCredentials.clientId, mcaCredentials.secret); 

   }
  ); 
   
  ```
 
 Observe que o parâmetro `redirect_uri` deve corresponder ao `redirect_uri` usado para a solicitação
de autorização anterior. O valor de parâmetro `code` deve ser o código de concessão recebido na resposta da solicitação de
autorização. O código de concessão é válido por 10 minutos, após os quais um novo código deve ser recuperado.

O corpo de resposta conterá o código de acesso e o ID do token no formato JWT (https://jwt.io/).

Assim que tiver obtido acesso e recebido os tokens de identidade, será possível sinalizar a sessão da web como autenticada e, opcionalmente, persistir esses tokens.  

##Usando o acesso e o token de identidade obtidos 

O token de identidade contém informações sobre a identidade do usuário. No caso de autenticação do Facebook, o token conterá todas as
informações que o usuário concordou em compartilhar, como nome completo, grupo de idade, URL da foto de perfil, etc.  

O token de acesso permite a comunicação com os recursos protegidos pelos filtros de autorização {{site.data.keyword.amashort}},
consulte [Protegendo recursos](protecting-resources.html).


Para fazer solicitações para recursos protegidos, inclua um cabeçalho de autorização nas solicitações com a estrutura a seguir: 

`Authorization=Bearer <accessToken> <idToken>`

#### Dicas
{: tips} 

* Deve-se separar o `accessToken` e o `idToken` com um espaço em branco.

* O `idToken` é opcional. Se você não fornecer o token de identidade, o recurso protegido poderá ser acessado, mas não receberá nenhuma informação sobre o usuário autorizado. 
 



