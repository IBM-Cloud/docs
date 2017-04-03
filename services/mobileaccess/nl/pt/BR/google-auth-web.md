---

copyright:
  year: 2016, 2017
lastupdated: "2017-03-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

O serviço {{site.data.keyword.amafull}} foi substituído pelo serviço {{site.data.keyword.appid_full}}.

# Ativando a autenticação do Google para aplicativos da web
{: #google-auth-web}

Use o Google Sign-In para autenticar usuários em seu
aplicativo da web. Inclua a funcionalidade de segurança do {{site.data.keyword.amafull}}.


## Antes de iniciar
{: #before-you-begin}

Você deve ter:

* Um aplicativo da web.
* Uma instância de um aplicativo {{site.data.keyword.Bluemix_notm}} que seja protegida pelo serviço {{site.data.keyword.amashort}}. Para obter mais informações sobre como criar um aplicativo backend do {{site.data.keyword.Bluemix_notm}}, consulte [Introdução](index.html).
* O URI para o redirecionamento final (após o processo de autorização ser concluído).


## Configurando um aplicativo Google para seu website
{: #google-auth-config}

Para começar a usar o Google como um provedor de identidade, crie um projeto no
[Console do Google Developer ![Ícone de link
externo](../../icons/launch-glyph.svg "External link icon")](https://console.developers.google.com){: new_window}. Parte
da criação de um projeto é obter um **Identificador de cliente do Google** e um **Segredo**. O Identificador
de cliente do Google e o Segredo são os identificadores exclusivos para seu aplicativo usados pela autenticação do Google e são necessários para
configurar o painel {{site.data.keyword.amashort}}.

1. Abra seu aplicativo Google no Google Developer Console.
3. Inclua a API **Google+**.
3. Crie credenciais usando o OAuth. Selecione o aplicativo da web no tipo de aplicativo. Insira o URI de redirecionamento
{{site.data.keyword.amashort}} na caixa de URIs de redirecionamento autorizado. Obtenha o URI de autorização de redirecionamento do
{{site.data.keyword.amashort}} a partir da tela de configuração do Google do painel do {{site.data.keyword.amashort}} (veja as etapas a seguir).
4. Salve as mudanças. Note o **ID de cliente
do Google** e o **Segredo do
aplicativo**.


## Configurando o {{site.data.keyword.amashort}} para autenticação do Google
{: #google-auth-config-ama}

Depois de ter um ID de aplicativo e um segredo do Google, é possível ativar a autenticação do Google no painel do {{site.data.keyword.amashort}}.

1. Abra o painel
de serviço {{site.data.keyword.amashort}}.
1. Na guia **Gerenciar**, acione
**Autorização**.
1. Abra a seção **Google**.
1. Verifique **Incluir Google a um app da
web**
4. Na seção **Configurar para web**:   
    * Observe o valor na caixa de texto **URI de redirecionamento do Mobile Client Access para o Google Developer Console**. Esse é o valor necessário para incluir na caixa **URIs
de redirecionamento autorizado** em
**Restrições no Identificador de cliente para
aplicativo da web** do **Portal de
desenvolvedores do Google**.
    * Insira o **Identificador de cliente** e o **Segredo do cliente**.
    * Insira o URI de redirecionamento nos **URIs de redirecionamento de aplicativo da web**. Esse valor é para que o URI de
redirecionamento seja acessado após o processo de autorização ser concluído e é determinado pelo desenvolvedor.
5. Clique em **Salvar**.


## Implementando o fluxo de autorização {{site.data.keyword.amashort}} usando o Google como provedor de identidade
{: #google-auth-flow}

A variável de ambiente `VCAP_SERVICES` é criada automaticamente para cada instância de serviço do
{{site.data.keyword.amashort}} e contém propriedades necessárias para o processo de autorização. Ela consiste em um objeto JSON e pode ser visualizada clicando
na guia **Credenciais de serviço** no painel de serviço
{{site.data.keyword.amashort}}.

Para iniciar o processo de autorização:

1. Recupere o terminal de autorização (`authorizationEndpoint`) e o clientId (`clientId`) das credenciais
de serviço armazenadas na variável de ambiente `VCAP_SERVICES`.

	`var cfEnv = require("cfenv");`

	`var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;`

	**Nota:** se você tiver incluído o
serviço {{site.data.keyword.amashort}} em seu aplicativo
antes de incluir o suporte da web, talvez você não tenha o
terminal do token nas credenciais de serviço. Como alternativa, use as URLs a seguir, dependendo de sua região do {{site.data.keyword.Bluemix_notm}}:

	Sul dos EUA:

	`https://mobileclientaccess.ng.bluemix.net/oauth/v2/authorization`

	Londres:

	`https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/authorization`

	Sydney:

	`https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/authorization`

2. Construa o URI do servidor de autorizações usando `response_type("code")`, `client_id` e `redirect_uri` como parâmetros de consulta.

3. Redirecione a partir do seu aplicativo da web para o
URI gerado.

	O exemplo a seguir recupera os parâmetros da variável `VCAP_SERVICES`, construindo a URL e enviando a solicitação de redirecionamento.

	```Java
var cfEnv = require("cfenv"); 
app.get("/protected", checkAuthentication, function(req, res, next){
		res.send("Hello from protected endpoint"); 
 });

	function checkAuthentication(req, res, next){
		// Check if user is authenticated 
  if (req.session.userIdentity){
			next()
		} else {
			// If not - redirect to authorization server 
				var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials; 
				var authorizationEndpoint = mcaCredentials.authorizationEndpoint; 
				var clientId = mcaCredentials.clientId; 
				var redirectUri = "http://some-server/oauth/callback"; // Your Web application redirect URI 
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

	Após redirecionar para o terminal de autorização, o usuário obterá um formulário de login do Google. Depois que o usuário concede permissões para efetuar login
usando a identidade do Google, o serviço
{{site.data.keyword.amashort}} chama o URI de
redirecionamento de aplicativo da web, fornecendo o código de
concessão como um parâmetro de consulta.

## Obtendo os tokens
{: #google-auth-tokens}

A próxima etapa é obter token de acesso e tokens de identidade usando o código de concessão recebido anteriormente.

1. Recupere os tokens `tokenEndpoint`, `clientId` e `secret` das credenciais de serviço armazenadas na variável de ambiente `VCAP_SERVICES`.

	**Nota:** se você usou o
{{site.data.keyword.amashort}} antes de o suporte da web
ter sido incluído, talvez você não tenha um terminal de token
nas credenciais de serviço. Como alternativa, use as URLs a seguir, dependendo de sua região do Bluemix:

	Sul dos EUA:

	`https://mobileclientaccess.ng.bluemix.net/oauth/v2/token`

	Londres:

	`https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/token`

	Sydney:

	`https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/token`

2. Envie uma solicitação de post ao URI do servidor de token com grant_type ("authorization_code"), client_id, redirect_uri e code como parâmetros de formulário. Envie
`clientId` e `clientSecret` como Credenciais de autenticação HTTP básicas.

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
			redirect_uri: "http://some-server/oauth/callback",// Your Web application redirect uri
			code: req.query.code
		}

		request.post({
			url: tokenEndpoint,
			formData: formData
		}, function (err, response, body) {
			var parsedBody = JSON.parse(body); 
			req.session.accessToken = parsedBody.access_token; 
			req.session.idToken = parsedBody.id_token; 
			var idTokenComponents = parsedBody.id_token.split("."); // [header, payload, signature] 			var decodedIdentity= base64url.decode(idTokenComponents[1]);
			req.session.userIdentity = JSON.parse(decodedIdentity)["imf.user"]; 			res.redirect("/"); 		}
			).auth(mcaCredentials.clientId, mcaCredentials.secret); 
  }
	);
	```
	{: codeblock}

	O parâmetro `redirect_uri` é o URI
para redirecionamento, após a autenticação bem-sucedida ou com falha no Google+, e deve corresponder
ao `redirect_uri` definido no painel do {{site.data.keyword.amashort}}.  

	Certifique-se de enviar esta solicitação POST no período de 10 minutos, após o qual, o código de concessão expirará. Depois de 10 minutos, será necessário um novo código.

	O corpo de resposta POST contém o `access_token` e o `id_token` codificados em base64.

	Depois de receber o acesso e os tokens de identidade,
será possível sinalizar a sessão da web como autenticada e,
opcionalmente, persistir esses tokens.  


##Usando o acesso e o token de identidade obtidos
{: #google-auth-using-token}

O token de identidade contém informações sobre a identidade do usuário. Para autenticação do Google, o token contém todas as informações que o usuário concordou em compartilhar, como nome completo, URL da foto de perfil, etc.  

O token de acesso permite a comunicação com os recursos protegidos pelos filtros de autorização do {{site.data.keyword.amashort}}. Leia sobre [Protegendo recursos](protecting-resources.html).

Para fazer solicitações para recursos protegidos, inclua um cabeçalho de autorização nas solicitações com a estrutura a seguir:

`Authorization=Bearer <accessToken> <idToken>`

####Dicas:
{: #tips}

* O `accessToken` e o `idToken` devem ser separados por um espaço em branco.

* O `idToken` é opcional. Se você não fornecer o token de identidade, o recurso protegido poderá ser acessado, mas não receberá nenhuma informação sobre o usuário autorizado.
