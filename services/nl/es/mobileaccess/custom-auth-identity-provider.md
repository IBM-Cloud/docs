---

copyright:
  años: 2015, 2016

---

# Creación de un proveedor de identidad personalizado
{: #custom-create}
Para crear un proveedor de identidad personalizado, desarrolle una aplicación web que exponga una API RESTful:

```
POST <url_base>/apps/<id_arrendatario>/<nombre_reino>/<tipo_solicitud>
```

* `url_base`: especifica el URL base de la aplicación web del proveedor de identidad personalizado. El URL base es el URL que se va a registrar en el panel de control de {{site.data.keyword.amashort}}.
* `id_arrendatario`: indica el identificador exclusivo del arrendatario. Cuando {{site.data.keyword.amashort}} invoca esta API, siempre proporciona el GUID de la app de {{site.data.keyword.Bluemix}} (`applicationGUID`).
* `nombre_reino`: especifica el nombre de reino personalizado definido en el panel de control de {{site.data.keyword.amashort}}.
* `tipo_solicitud`: indica una de las siguientes opciones:
	* `startAuthorization`: indica un primer paso del proceso de autenticación. El proveedor de identidad personalizado debe responder con el estado "challenge", "success" o "failure".
	* `handleChallengeAnswer`: gestiona una respuesta a un cambio de autenticación desde el cliente móvil.

## API `startAuthorization`
{: #custom-startauthorization}

`POST <url_base>/apps/<id_arrendatario>/<nombre_reino>/startAuthorization`

La API `startAuthorization` se utiliza como primer paso del proceso de autenticación. Un proveedor de identidad personalizado debe responder con el estado "challenge", "success" o "failure".

Para permitir la máxima flexibilidad del proceso de autenticación, el proveedor de identidad personalizado tendrá acceso a todas las cabeceras HTTP enviadas desde el cliente móvil en el cuerpo de la solicitud. Las cabeceras se proporcionan con el formato siguiente:

```JavaScript
{
    "headers" : {
    	"header1": "value1",  
    	"header2" : "value2"
    }
}
```

El proveedor de identidad personalizada puede responder con un cambio de autenticación o un error o éxito inmediatos. El estado HTTP de respuesta debe ser `HTTP 200` y JSON de respuesta debe incluir las propiedades siguientes:

* `status`: especifica el estado `success`, `challenge` o `failure` de la solicitud.
* `stateId` (opcional): indica un identificador de serie generado de forma aleatoria para identificar la sesión de autenticación con el cliente móvil. Este atributo se puede omitir si el proveedor de identidad personalizado no almacena ningún estado.
* `challenge`: especifica un objeto JSON que representa un cambio de autenticación que se volverá a enviar al cliente móvil. Este atributo solo se envía al cliente si el estado se define en `challenge`.
* `userIdentity`: indica un objeto JSON que representa una identidad de usuario.  La identidad de usuario consiste en propiedades como `userName`, `displayName` y attributes.  Para obtener más información, consulte [Objeto de identidad de usuario](#custom-user-identity). Esta propiedad solo se envía al cliente móvil si el estado se establece en `success`.

Por ejemplo:

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

## API `handleChallengeAnswer`
{: #custom-handleChallengeAnswer}

`POST <url_base>/apps/<id_arrendatario>/<nombre_reino>/handleChallengeAnswer`

La API `handleChallengeAnswer` gestiona una respuesta a un cambio de autenticación desde el cliente móvil. Igual que la API `startAuthorization`, la API `handleChallengeAnswer` responde con el estado `challenge`, `success` o `failure`.

De forma similar a la solicitud `startAuthorization`, el proveedor de identidad personalizado tiene acceso a todas las cabeceras HTTP enviadas desde el cliente móvil en el cuerpo de la solicitud. Además de las cabeceras de solicitud del cliente móvil, el cuerpo de la solicitud `handleChallengeAnswer` también incluye las propiedades `stateId` y `challengeAnswer`.

### Ejemplo de cuerpo de la solicitud `handleChallengeAnswer`
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

La respuesta de la API `handleChallengeAnswer` debe tener la misma estructura que la respuesta de la API `startAuthorization`.

## Objeto de identidad de usuario
{: #custom-user-identity}

Una respuesta a una solicitud de autenticación con éxito debe incluir un objeto de identidad de usuario con los atributos siguientes:
* `userName`: especifica un nombre de usuario exclusivo.
* `displayName`: indica el nombre de visualización del usuario.
* `attributes` (opcional): especifica un objeto JSON que contiene atributos personalizados de usuario.

### Ejemplo de objeto de identidad de usuario
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

El objeto de identidad de usuario se utiliza en el servicio de {{site.data.keyword.amashort}} para generar una señal de ID que se envía al cliente móvil como parte de la cabecera de autorización. Después de una autenticación satisfactoria, el cliente móvil tendrá acceso al objeto de identidad de usuario.

## Consideraciones sobre seguridad
{: #custom-security}

Cada solicitud del servicio de {{site.data.keyword.amashort}} a un proveedor de identidad personalizado contiene una cabecera de autorización, de forma que el proveedor pueda verificar que la solicitud proviene de un origen autorizado. Aunque no es estrictamente obligatorio, piense en la posibilidad de validar la cabecera de autorización instrumentando el proveedor de identidad personalizado con un SDK del servidor de {{site.data.keyword.amashort}}. Para utilizar este SDK, la aplicación del proveedor de identidad personalizado debe implementarse en con Node.js o Liberty for Java&trade;&trade; y ejecutarse en {{site.data.keyword.Bluemix_notm}}.

La cabecera de autorización contiene información sobre el cliente móvil y la app móvil que han activado el proceso de autenticación. Puede utilizar el contexto de seguridad para recuperar estos datos. Para obtener más información, consulte [Protección de recursos](protecting-resources.html)

## Implementación de ejemplo de un proveedor de identidad personalizado
{: #custom-sample}
Puede hacer referencia a cualquiera de las siguientes implementaciones del ejemplo Node.js de un proveedor de identidad personalizado cuando desarrolle el proveedor de identidad personalizado. Descargue el código completo de la aplicación desde los repositorios de GitHub. 

* [Ejemplo simple](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-sample)
* [Ejemplo avanzado](https://github.com/ibm-bluemix-mobile-services/bms-mca-custom-identity-provider-with-user-management)

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

## Próximos pasos
{: #next-steps}
* [Configuración de {{site.data.keyword.amashort}} para la autenticación personalizada](custom-auth-config-mca.html)
* [Configuración de la autenticación personalizada para Android](custom-auth-android.html)
* [Configuración de la autenticación personalizada para iOS](custom-auth-ios.html)
* [Configuración de la autenticación personalizada para Cordova](custom-auth-cordova.html)
