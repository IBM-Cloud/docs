---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-08"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

#Configurando a autenticação customizada para aplicativos
da web
{{site.data.keyword.amashort}}
{: #custom-web}

Inclua a autenticação customizada e a funcionalidade de
segurança do {{site.data.keyword.amafull}} em seu app da
web.

## Antes de iniciar
{: #before-you-begin}

Antes de iniciar, deve-se ter:

* Um aplicativo da web.
* Um recurso que seja protegido por uma instância do
serviço {{site.data.keyword.amashort}} que está
configurado para usar um provedor de identidade customizado
(consulte
[Configurando autenticação customizada](custom-auth-config-mca.html)).  
* Seu valor **TenantID**. Abra o seu serviço no painel do {{site.data.keyword.amashort}}. Clique no botão **Opções móveis**. O valor
`tenantId` (também conhecido como
`appGUID`) é exibido no campo **App
GUID / TenantId**. Você precisará desse valor para
inicializar o Gerenciador de Autorização.
* Seu nome de **Domínio**. Este é o
valor que você especificou no campo **Nome do
domínio** da seção **Customizado**
no guia **Gerenciamento** do painel {{site.data.keyword.amashort}}.
* A URL do seu aplicativo backend (**Rota de App**). Você precisará desse valor para enviar
solicitações para os terminais protegido do seu aplicativo
backend.
* A {{site.data.keyword.Bluemix_notm}}
**Região**. É possível encontrar a sua região
{{site.data.keyword.Bluemix_notm}} atual no cabeçalho,
próximo ao ícone **Avatar**
![ícone de avatar](images/face.jpg "ícone de avatar"). O valor da região que aparece deve ser um dos
seguintes: `US South`, `United Kingdom` ou `Sydney`, e corresponder aos
valores de SDK requeridos no código Javascript:
`BMSClient.REGION_US_SOUTH`,
`BMSClient.REGION_SYDNEY` ou
`BMSClient.REGION_UK`. Você precisará desse
valor para inicializar o cliente
{{site.data.keyword.amashort}}.
* O URI para o redirecionamento final (após o processo de autorização ser concluído). Este é o valor **URIs de redirecionamento de aplicativo da
web** que você inseriu na seção
**Customizado** da guia
**Gerenciamento**.

Para mais Informações:

* [Introdução
ao {{site.data.keyword.amashort}}](getting-started.html)
* [Usando um provedor de identidade customizado](custom-auth.html)
* [Criando um provedor de identidade customizado](custom-auth-identity-provider.html)
* [Configurando o {{site.data.keyword.amashort}} para autenticação customizada](custom-auth-config-mca.html)


##Configurando um provedor de identidade customizado
{: #custom-auth-config}

Ao criar um provedor de identidade customizado, deve-se definir um método POST com uma rota na estrutura a seguir:

`/apps/:tenantID/<your-realm-name>/handleChallengeAnswer`

`tenantID` é um parâmetro URL e
`<your-realm-name>` é qualquer nome de região escolhido.

O corpo da solicitação conterá um objeto `challengeAnswer` que
contém `username` e `password`.

Após validar o usuário, essa rota deverá retornar um objeto JSON da estrutura a seguir.

```json
{
	status: "success", 
            userIdentity: {
		userName: <user name>, 
                displayName: <display name> 
                attributes: <additional attributes json> 
            }
}
```
{: codeblock}

**Nota:** o campo `attributes` é opcional.

O código a seguir demonstra uma solução de POST.

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
{: codeblock}


##Configurando o {{site.data.keyword.amashort}} para autenticação customizada
{: #custom-auth-config-mca}

Após ter seu provedor de identidade customizado configurado, será possível ativar a autenticação customizada no painel {{site.data.keyword.amashort}}.

1. Abra o seu serviço no painel do {{site.data.keyword.amashort}}.
1. Na guia **Gerenciar**, acione
**Autorização**.
1. Expanda a seção **Customizado**.
1. Insira o **Nome do domínio**,
**URL do provedor de identidade customizado**.
1. Insira o valor **URIs de redirecionamento de
aplicativo da web**. Este é o URI do redirecionamento
final após autorização bem-sucedida.
1. Clique em **Salvar**.


##Implementando o fluxo de autorização {{site.data.keyword.amashort}} usando um provedor de identidade customizado
{: #custom-auth-flow}

A variável de ambiente `VCAP_SERVICES` é criada automaticamente para cada instância de serviço do {{site.data.keyword.amashort}} e contém propriedades necessárias para o processo de autorização. Ele consiste em um objeto JSON e pode ser visualizado na guia
**Credenciais de serviço** no painel
{{site.data.keyword.amashort}}.

Para solicitar autorização do usuário, redirecione o navegador para o terminal do servidor de autorizações. Para fazer isso:

1. Recupere o terminal de autorização (`authorizationEndpoint`) e o ID do cliente (`clientId`) por meio das credenciais de serviço armazenadas
na variável de ambiente `VCAP_SERVICES`.

	`var cfEnv = require("cfenv");`

	`var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;`

	**Nota:** se você tiver incluído o serviço {{site.data.keyword.amashort}} em seu aplicativo antes de incluir o suporte da web, talvez você
não tenha o
terminal do token nas credenciais de serviço. Como alternativa, use as URLs a seguir, dependendo de sua região do {{site.data.keyword.Bluemix_notm}}:

	Sul dos EUA:

	`https://mobileclientaccess.ng.bluemix.net/oauth/v2/authorization`

	Londres:

	`https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/authorization`

	Sydney:

	`https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/authorization`

2. Construa o URI do servidor de autorizações usando `response_type("code")`, `client_id` e
`redirect_uri` como parâmetros de consulta.  

3. Redirecione a partir do seu aplicativo da web para o
URI gerado.

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
	{: codeblock}

	Observe que o parâmetro `redirect_uri`
representa seu URI de redirecionamento de aplicativo da web e
deve ser igual àquele
definido no painel {{site.data.keyword.amashort}}.  

	Um parâmetro `state` pode ser transmitido junto com a solicitação. Esse parâmetro será propagado para o método POST do
provedor de identidade customizado e pode ser acessado a partir do corpo da solicitação (`req.body.stateId`).  

	Após redirecionar para o terminal de autorização, o usuário obterá um formulário de login. Após as credenciais do usuário terem sido autenticadas com o
provedor de identidade customizado, o serviço
{{site.data.keyword.amashort}} chamará seu URI
de redirecionamento de aplicativo da web fornecendo o código de
concessão como um parâmetro de consulta.  

	Após redirecionar, o usuário obtém um formulário de login. Após as credenciais do usuário serem autenticadas pelo provedor
de identidade customizado, o serviço
{{site.data.keyword.amashort}} chamará o URI de
redirecionamento de aplicativo da web, fornecendo o código de
concessão como um parâmetro de consulta.

##Obtendo os tokens
{: custom-auth-tokens}

A próxima etapa é obter o token de acesso e o token de identidade usando o código de concessão recebido anteriormente. Para fazer isso:

1. Recupere `authorizationEndpoint`, `clientId` e `secret` das credenciais de serviço
armazenadas na variável de ambiente `VCAP_SERVICES`.

	**Nota:** se você tiver incluído o
serviço {{site.data.keyword.amashort}} em seu aplicativo
antes de incluir o suporte da web, talvez você não tenha o
terminal do token nas credenciais de serviço. Como alternativa, use as URLs a seguir, dependendo de sua região do {{site.data.keyword.Bluemix_notm}}:

	Sul dos EUA:

	`https://mobileclientaccess.ng.bluemix.net/oauth/v2/token`

	Londres:

	`https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/token`

	Sydney:

	`https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/token`

2. Envie uma solicitação de POST para o URI do servidor de token com
`grant_type`, `client_id`,
`redirect_uri` e `code` como parâmetros de forma e
`clientId` e `secret` como credenciais de autenticação
HTTP básica.

	O exemplo a seguir, o código a seguir recupera os valores necessários e os envia
com uma solicitação de POST.

	```Java
var cfEnv = require("cfenv");
var base64url = require("base64url ");
app.get("/oauth/callback", function(req, res, next){
		var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials; 
    var tokenEndpoint = mcaCredentials.tokenEndpoint;

		var formData = {
			grant_type: "authorization_code",
			client_id: mcaCredentials.clientId,
			redirect_uri: "http://some-server/oauth/callback",   // Your Web application redirect uri
			code: req.query.code
		}

		request.post({
			url: tokenEndpoint,
			formData: formData
		}, function (err, response, body) {
			var parsedBody = JSON.parse(body);

			req.session.accessToken = parsedBody.access_token; 
      req.session.idToken = parsedBody.id_token; 
      var idTokenComponents = parsedBody.id_token.split("."); // [header, payload, signature] 
			var decodedIdentity= base64url.decode(idTokenComponents[1]);
			req.session.userIdentity = JSON.parse(decodedIdentity)["imf.user"]; 
			res.redirect("/"); 
		}
		).auth(mcaCredentials.clientId, mcaCredentials.secret); 
  }
	);
	```
	{: codeblock}

	Observe que o parâmetro `redirect_uri` deve corresponder ao `redirect_uri` usado na solicitação de
autorização anteriormente. O valor do parâmetro de código deve ser o código de concessão recebido na resposta no fim da solicitação de autorização. O
código de concessão é válido por 10 minutos somente, após os quais será necessário obter um novo código.

	O corpo de resposta conterá `access_token` e `id_token`
no formato JWT; veja o [website do JWT ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://jwt.io "Ícone de link externo"){: new_window}.

	Assim que tiver recebido o acesso e os tokens de
identidade, será possível sinalizar a sessão da web como
autenticada e opcionalmente persistir esses tokens


##Usando o acesso e o token de identidade obtidos
{: #custom-auth-using-token}

O token de identidade contém informações sobre a identidade do usuário. No caso de uma autenticação customizada, o token conterá todas as informações retornadas pelo provedor de identidade customizado mediante a autenticação. No
campo `imf.user`, o campo `displayName` conterá o `displayName` retornado pelo provedor de
identidade customizado e o campo `id` conterá `userName`.  Todos os outros valores retornados pelo provedor de
identidade customizado serão retornados no campo `attributes` em `imf.user`.  

O token de acesso permite comunicação com recursos protegidos pelos filtros de autorização do {{site.data.keyword.amashort}} (veja [Protegendo recursos](protecting-resources.html)). Para fazer solicitações para recursos protegidos, inclua um cabeçalho de autorização nas solicitações com a estrutura a seguir:

`Authorization=Bearer <accessToken> <idToken>`

####Dicas:
{: #tips_token}

* O `<accessToken>` e o `<idToken>` devem ser separados por um espaço em branco.

* O token de identidade é opcional. Se você não fornecer o token de identidade, o recurso protegido poderá ser acessado, mas não receberá nenhuma informação sobre o usuário autorizado.
