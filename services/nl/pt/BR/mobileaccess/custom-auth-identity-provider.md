---

copyright:
  years: 2015, 2016

---

# Criando um provedor de identidade customizado
{: #custom-create}
Para criar um provedor de identidade customizado, desenvolva um aplicativo da web que exponha uma API RESTful:

```
POST <base_url>/apps/<tenant_id>/<realm_name>/<request_type>
```

* `base_url`: especifica a URL base do aplicativo da web do provedor de identidade customizado. A URL base é a URL a ser registrada no painel do {{site.data.keyword.amashort}}.
* `tenant_id`: especifica o identificador exclusivo do locatário. Quando
o {{site.data.keyword.amashort}} chama essa API, ele sempre fornece o GUID
do app {{site.data.keyword.Bluemix}} (`applicationGUID`).
* `realm_name`: especifica o nome do domínio customizado definido no painel do {{site.data.keyword.amashort}}.
* `request_type`: especifica um de:
	* `startAuthorization`: especifica uma primeira etapa do processo de autenticação. O provedor de identidade customizado deve responder com um status "desafio", "sucesso" ou "falha".
	* `handleChallengeAnswer`: manipula uma resposta do desafio de autenticação do cliente móvel.

## API `startAuthorization`
{: #custom-startauthorization}

`POST <base_url>/apps/<tenant_id>/<realm_name>/startAuthorization`

A API `startAuthorization` é usada como uma primeira etapa do processo de autenticação. Um provedor de identidade customizado deve responder com um status "desafio", "sucesso" ou "falha".

Para permitir flexibilidade máxima do processo de autenticação, um provedor de identidade customizado possui acesso a todos os cabeçalhos de HTTP enviados por um cliente móvel no corpo da solicitação. Os cabeçalhos são fornecidas no formato a seguir:

```JavaScript
{
    "headers" : {
    	"header1": "value1",  
    	"header2" : "value2"
    }
}
```

Um provedor de identidade customizado pode responder com um desafio de autenticação ou com sucesso ou falha imediato. O status de HTTP da resposta deve ser `HTTP 200` e o JSON de resposta deve conter as propriedades a seguir:

* `status`: especifica `success`, `challenge` ou `failure` da solicitação.
* `stateId` (opcional): especifica um identificador de sequência gerado aleatoriamente para identificar a sessão de autenticação com o cliente móvel. Esse atributo poderá ser omitido se o provedor de identidade customizado não armazenar nenhum estado.
* `challenge`: especifica um objeto JSON que representa um desafio de autenticação a ser enviado de volta para o cliente móvel. Esse atributo só será enviado para o cliente se o status estiver configurado como `challenge`.
* `userIdentity`: especifica um objeto JSON que representa uma identidade do usuário.  A identidade do usuário consiste em propriedades, como `userName`, `displayName` e atributos.  Para obter mais informações, consulte [Objeto de identidade do usuário](#custom-user-identity). Esta propriedade só será enviada para o cliente móvel se o status estiver configurado como `success`.

Por exemplo:

```
{
	"status":"challenge",
	"stateId":"some-random-guid"
	"challenge":{
		message:"Enter username and password",
		attemptsLeft: 3
	}
}
```

## `handleChallengeAnswer` API
{: #custom-handleChallengeAnswer}

`POST <base_url>/apps/<tenant_id>/<realm_name>/handleChallengeAnswer`

A API `handleChallengeAnswer` manipula uma resposta do desafio de autenticação do cliente móvel. Como a API `startAuthorization`, a API `handleChallengeAnswer` responde com o status `challenge`, `success` ou `failure`.

Da mesma forma que a solicitação `startAuthorization`, o provedor de identidade customizado possui acesso a todos os cabeçalhos de HTTP enviados pelo cliente móvel no corpo da solicitação. Além dos cabeçalhos de solicitação do cliente móvel, o corpo da solicitação `handleChallengeAnswer` também inclui as propriedades `stateId` e `challengeAnswer`.

### Exemplo de corpo da solicitação `handleChallengeAnswer`
{: #custom-handleChallengeAnswer-example}

```JavaScript
{
    "headers" : {
    	"header1": "value1",  
    	"header2" : "value2"
	},
    "stateId" : "123123123",
    "challengeAnswer" : {
    	"pinCode":12345
 	}
}
```

A resposta de uma API `handleChallengeAnswer` deve ter a mesma estrutura que a resposta da API `startAuthorization`.

## Objeto de identidade do usuário
{: #custom-user-identity}

Uma resposta a uma solicitação de autenticação bem-sucedida deve incluir um objeto de identidade do usuário, com os atributos a seguir:
* `userName`: especifica um nome de usuário exclusivo.
* `displayName`: especifica o nome de exibição do usuário.
* `attributes` (opcional): especifica um objeto JSON que contém atributos customizados do usuário.

### Exemplo de objeto de identidade do usuário
{: #custom-user-identity-example}
```JavaScript
{
    "userName" : "janesmith",
    "displayName" : "Jane Smith",
    "attributes" : {
        "Language" : "French",
        "Country" : "Canada"
    }
}
```

O objeto de identidade do usuário é usado pelo serviço {{site.data.keyword.amashort}} para gerar um token de ID que é enviado para o cliente móvel como parte do cabeçalho de autorização. Após a autenticação bem-sucedida, o cliente móvel possui acesso completo ao objeto de identidade do usuário.

## Considerações de segurança
{: #custom-security}

Cada solicitação do serviço {{site.data.keyword.amashort}} para um provedor de identidade customizado contém um cabeçalho de autorização para que o provedor de identidade customizado possa verificar se a solicitação está vindo de uma origem autorizada. Embora não seja estritamente obrigatório, considere validar o cabeçalho de autorização instrumentando seu provedor de identidade customizado com um {{site.data.keyword.amashort}} Server SDK. Para usar esse SDK, seu aplicativo provedor de identidade customizado deve ser
implementado com o Node.js ou o Liberty for Java&trade;&trade; e executado no
{{site.data.keyword.Bluemix_notm}}.

O cabeçalho de autorização contém informações sobre o cliente móvel e o app móvel que acionou o processo de autenticação. É possível usar o contexto de segurança para recuperar esses dados. Para obter mais informações, consulte [Protegendo recursos](protecting-resources.html).

## Implementação de amostra do provedor de identidade customizado
{: #custom-sample}
É possível usar qualquer uma das implementações de amostra Node.js a seguir de um provedor de identidade customizado como referência ao desenvolver seu provedor de identidade customizado. Faça download do código do aplicativo completo dos repositórios GitHub.

* [Amostra simples](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)
* [Amostra avançada](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management)

<!---
 ### JSON structure (simple sample)
{: #custom-sample-json}
This implementation assumes that the supplied authentication challenge answer is a JSON object with the following structure:

```
{
 	username: "my.username",
 	password: "my.password"
 }
 ```

### Custom identity provider sample code (simple sample)
{: #custom-sample-code}
```JavaScript
var express = require('express');
var cfenv = require('cfenv');
var log4js = require('log4js');
var jsonParser = require('body-parser').json();

// Using hardcoded user repository
var userRepository = {
	"john.lennon":      { password: "12345", displayName:"John Lennon", dob:"October 9, 1940"},
	"paul.mccartney":   { password: "67890", displayName:"Paul McCartney", dob:"June 18, 1942"},
	"ringo.starr":      { password: "abcde", displayName:"Ringo Starr", dob: "July 7, 1940"},
	"george.harrison":  { password: "fghij", displayName: "George Harrison", dob:"Feburary 25, 1943"}
}

var app = express();
var logger = log4js.getLogger("CustomIdentityProviderApp");
logger.info("Starting up");

app.post('/apps/:tenantId/:realmName/startAuthorization', jsonParser, function(req, res){
	var tenantId = req.params.tenantId;
	var realmName = req.params.realmName;
	var headers = req.body.headers;

	logger.debug("startAuthorization", tenantId, realmName, headers);

	var responseJson = {
		status: "challenge",
		challenge: {
			text: "Enter username and password"
		}
	};

	res.status(200).json(responseJson);
});

app.post('/apps/:tenantId/:realmName/handleChallengeAnswer', jsonParser, function(req, res){
	var tenantId = req.params.tenantId;
	var realmName = req.params.realmName;
	var challengeAnswer = req.body.challengeAnswer;


	logger.debug("handleChallengeAnswer", tenantId, realmName, challengeAnswer);

	var username = req.body.challengeAnswer["username"];
	var password = req.body.challengeAnswer["password"];

	var userObject = userRepository[username];

	var responseJson = { status: "failure" };

	if (userObject && userObject.password == password ){
		logger.debug("Login success for userId ::", username);
		responseJson.status = "success";
		responseJson.userIdentity = {
			userName: username,
			displayName: userObject.displayName,
			attributes: {
				dob: userObject.dob
			}
		}
	} else {
		logger.debug("Login failure for userId ::", username);
	}

	res.status(200).json(responseJson);
});

app.use(function(req, res, next){
	res.status(404).send("This is not the URL you're looking for");
});

var server = app.listen(cfenv.getAppEnv().port, function () {
	var host = server.address().address;
	var port = server.address().port;
	logger.info('Server listening at %s:%s', host, port);
});
```
--->

## Próximas Etapas
{: #next-steps}
* [Configurando o {{site.data.keyword.amashort}} para autenticação customizada](custom-auth-config-mca.html)
* [Configurando a autenticação customizada para Android](custom-auth-android.html)
* [Configurando a autenticação customizada para iOS](custom-auth-ios.html)
* [Configurando a autenticação customizada para Cordova](custom-auth-cordova.html)
