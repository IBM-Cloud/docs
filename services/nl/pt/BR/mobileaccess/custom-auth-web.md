---

copyright:
  years: 2016

---

#Configurando a autenticação customizada para aplicativos da web {{site.data.keyword.amashort}}
{: #custom-web}

Última atualização: 21 de julho de 2016
{: .last-updated}

Inclua a autenticação customizada e a funcionalidade de segurança do {{site.data.keyword.amashort}} em seu app da web.

## Antes de começar
{: #before-you-begin}
Antes de iniciar, deve-se ter:

*	Um app da web. 
*	Uma instância de um aplicativo {{site.data.keyword.Bluemix_notm}} que seja protegida pelo serviço {{site.data.keyword.amashort}}. Para
obter mais informações sobre como criar um aplicativo backend {{site.data.keyword.Bluemix_notm}}, consulte [Introdução ao {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html).
*	O URI para o redirecionamento final (após o processo de autorização ser concluído).


Para mais Informações:
 * [Introdução ao {{site.data.keyword.amashort}}](https://console.{DomainName}/docs/services/mobileaccess/getting-started.html)
 * [Usando um provedor de identidade customizado](https://console.{DomainName}/docs/services/mobileaccess/custom-auth.html)
 * [Criando um provedor de identidade customizado](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-identity-provider.html)
 * [Configurando o {{site.data.keyword.amashort}} para autenticação customizada](https://console.{DomainName}/docs/services/mobileaccess/custom-auth-config-mca.html)


##Configurando um provedor de identidade customizado 

Ao criar um provedor de identidade customizado, deve-se definir um método POST com uma rota na estrutura a seguir: 

`/apps/:tenantID/<your-realm-name>/handleChallengeAnswer`

`tenantID` é um parâmetro URL e `<your-realm-name>` é qualquer nome da região que escolher. 

O corpo da solicitação conterá um objeto `challengeAnswer` que contém `username` e
`password`. Após validar o usuário, essa rota deve retornar um objeto JSON da estrutura a seguir. 


```json { 
            status: "success", 
            userIdentity: { 
                userName: <user name>, 
                displayName: <display name> 
                attributes: <additional attributes json> 
            } 
        } 

 ```

**Nota:** o campo `attributes` é opcional. 

O código a seguir demonstra tal solicitação de post.

```Java
var app = express();
var bodyParser = require('body-parser');
app.use(bodyParser.json());

var users = {
    "John": {
      password: "123",
      displayName: "John Doe"
    }
};

app.post('/apps/:tenantID/customAuthRealm_1/handleChallengeAnswer',
         function(req, res) {
         console.log ("tenantID " + req.params.tenantID);
         
         var challengeAnswer = req.body.challengeAnswer;
         console.log ("challengeAnswer " + JSON.stringify(challengeAnswer));

         if (challengeAnswer && users[challengeAnswer.username] && challengeAnswer.password === users[challengeAnswer.username].password) {
         res.json({
                  status: "success",
                  userIdentity: {
                  userName: challengeAnswer.username,
                  displayName: users[challengeAnswer.username].displayName
                  }
                  });
         } else {
         res.json({
                  status: "failure"
                  });
         }
         
         });

```


##Configurando o {{site.data.keyword.amashort}} para autenticação customizada 

Após ter seu provedor de identidade customizado configurado, será possível ativar a autenticação customizada no painel {{site.data.keyword.amashort}}. 

1. Abra o painel {{site.data.keyword.Bluemix_notm}}. 
2. Clique no tile do aplicativo {{site.data.keyword.amashort}} relevante. O painel do aplicativo é carregado. 
3. Clique no botão **Configurar** no Tile customizado. 
4. Na caixa de texto **Nome de região**, insira o nome da região configurado em seu terminal do manipulador do provedor
de identidade customizado. t
5. Insira a URL do provedor de identidade customizado. 
6. Insira o URI de redirecionamento de aplicativo da web a ser usado pelo painel {{site.data.keyword.amashort}} após a
autenticação bem-sucedida. 
7. Salve. 


##Implementando o fluxo de autorização {{site.data.keyword.amashort}} usando um provedor de identidade customizado 

A variável de ambiente `VCAP_SERVICES` é criada automaticamente para cada instância de serviço do {{site.data.keyword.amashort}} e contém propriedades necessárias para o processo de autorização. Ela consiste em um objeto JSON e pode ser visualizada clicando em **Variáveis de ambiente** na barra de navegação à esquerda de seu aplicativo.

Para solicitar autorização do usuário, redirecione o navegador para o terminal do servidor de autorizações. Para fazer isso: 

1. Recupere o terminal de autorização (`authorizationEndpoint`) e clientId (`clientId`) das
credenciais de serviço armazenadas na variável de ambiente `VCAP_SERVICES`. 

  **Nota:** se você tiver incluído o serviço {{site.data.keyword.amashort}} em seu aplicativo antes de incluir o suporte da web, talvez você
não tenha o
terminal do token nas credenciais de serviço. Como alternativa, use as URLs a seguir, dependendo de sua região do {{site.data.keyword.Bluemix_notm}}: 
 
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
1. Redirecione a partir do seu aplicativo da web para o URI gerado. 

O exemplo a seguir recupera os parâmetros da variável `VCAP_SERVICES`, constrói a URL e envia a solicitação de
redirecionamento.

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
    var redirectUri = "http://some-server/oauth/callback"; // Your web application redirect uri 
    var redirectUrl = authorizationEndpoint + "?response_type=code";
    redirectUrl += "&client_id=" + clientId; 
    redirectUrl += "&redirect_uri=" + redirectUri; 
    res.redirect(redirectUrl); 
  } 

} 

 ```
 
Observe que o parâmetro `redirect_uri` representa seu URI de aplicativo da web e deve ser igual àquele definido no painel {{site.data.keyword.amashort}}.  

Um parâmetro `state` pode ser transmitido junto com a solicitação. Esse parâmetro será propagado para o método POST do
provedor de identidade customizado e pode ser acessado a partir do corpo da solicitação (`req.body.stateId`).  

Após redirecionar para o terminal de autorização, o usuário obterá um formulário de login. Após as credenciais do usuário serem autenticadas com o provedor de identidade customizado, o serviço {{site.data.keyword.amashort}} chamará o URI de redirecionamento de aplicativo da web fornecendo o código de concessão como um parâmetro de consulta.  

Após redirecionar, o usuário obtém um formulário de login. Após as credenciais do usuário serem autenticadas pelo provedor de identidade
customizado, o serviço {{site.data.keyword.amashort}} chamará o URI de redirecionamento de aplicativo da web, fornecendo o código de
concessão como um parâmetro de consulta. 

##Obtendo os tokens

A próxima etapa é obter o token de acesso e o token de identidade usando o código de concessão recebido anteriormente. Para fazer isso: 

1. Recupere `authorizationEndpoint`, `clientId` e `secret` das credenciais de serviço
armazenadas na variável de ambiente `VCAP_SERVICES`. 

   **Nota:** se você tiver incluído o serviço {{site.data.keyword.amashort}} em seu aplicativo antes de incluir o suporte da web, talvez você
não tenha o
terminal do token nas credenciais de serviço. Como alternativa, use as URLs a seguir, dependendo de sua região do {{site.data.keyword.Bluemix_notm}}: 

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
1. Envie uma solicitação de post ao URI do servidor de token com `grant_type`,
`client_id`,
`redirect_uri` e `code` como parâmetros de formulário e `clientId` e `secret`
como credenciais de autenticação HTTP básicas.


O exemplo a seguir, o código a seguir, recupera os valores necessários e os envia com uma solicitação de post.


 ```Java
var cfEnv = require("cfenv");
var base64url = require("base64url ");
app.get("/oauth/callback", function(req, res, next){ 
    var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials; 
    var tokenEndpoint = mcaCredentials.tokenEndpoint; 

    var formData = { 
      grant_type: "authorization_code", 
      client_id: mcaCredentials.clientId, 
      redirect_uri: "http://some-server/oauth/callback",   // Your web application redirect uri 
      code: req.query.code 
    } 

  request.post({ 
    url: tokenEndpoint, 
    formData: formData 
    }, function (err, response, body){ 
      var parsedBody = JSON.parse(body); 

      req.session.accessToken = parsedBody.access_token; 
      req.session.idToken = parsedBody.id_token; 
      var idTokenComponents = parsedBody.id_token.split("."); // [header, payload, signature] 
      var decodedIdentity= base64url(idTokenComponents[1]);
      req.session.userIdentity = JSON.parse(decodedIdentity)["imf.user"]; 
      res.redirect("/"); 
    }
    ).auth(mcaCredentials.clientId, mcaCredentials.secret); 
  }
); 

 ```
Observe que o parâmetro `redirect_uri` deve corresponder ao `redirect_uri` usado na solicitação de
autorização anteriormente. O valor do parâmetro de código deve ser o código de concessão recebido na resposta no fim da solicitação de autorização. O
código de concessão é válido por 10 minutos somente, após os quais será necessário obter um novo código.

O corpo de resposta conterá `access_token` e `id_token` no formato JWT (https://jwt.io/).

Assim que tiver recebido o acesso e os tokens de identidade, será possível sinalizar a sessão da web como autenticada e opcionalmente
persistir esses tokens

##Usando o acesso e o token de identidade obtidos 

O token de identidade contém informações sobre a identidade do usuário. No caso de uma autenticação customizada, o token conterá todas as informações retornadas pelo provedor de identidade customizado mediante a autenticação. No
campo `imf.user`, o campo `displayName` conterá o `displayName` retornado pelo provedor de
identidade customizado e o campo `id` conterá `userName`.  Todos os outros valores retornados pelo provedor de
identidade customizado serão retornados no campo `attributes` em `imf.user`.  

O token de acesso permite comunicação com recursos protegidos pelos filtros de autorização do {{site.data.keyword.amashort}} (consulte [Protegendo recursos](protecting-resources.html)). Para fazer solicitações para recursos protegidos, inclua um cabeçalho de autorização nas solicitações com a estrutura a seguir: 

`Authorization=Bearer <accessToken> <idToken>` 

####Dicas: 
{: #tips_token}

* O `<accessToken>` e o `<idToken>` devem ser separados por um espaço em branco.

* O token de identidade é opcional. Se você não fornecer o token de identidade, o recurso protegido poderá ser acessado, mas não receberá nenhuma informação sobre o usuário autorizado. 



