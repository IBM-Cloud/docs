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

# Configuración de la autenticación personalizada para las aplicaciones web de {{site.data.keyword.amashort}}
{: #custom-web}

Añadir autenticación personalizada y funcionalidad de seguridad de {{site.data.keyword.amafull}} a su app web.

## Antes de empezar
{: #before-you-begin}

Antes de empezar, debe tener:

* Una app web.
* Un recurso protegido mediante una instancia del servicio {{site.data.keyword.amashort}} configurado para que utilice un proveedor de identidad personalizado (consulte [Configuración de la autenticación personalizada](custom-auth-config-mca.html)).  
* El valor de **TenantID**. Abra el servicio en el panel de control de {{site.data.keyword.amashort}}. Pulse el botón **Opciones móviles**. El valor `tenantId` (también conocido como `appGUID`) se muestra en el campo **GUID de app / TenantId**. Necesitará este valor para inicializar el gestor de autorización.
* Su nombre de **Dominio**. Es el valor que ha especificado en el campo **Nombre de dominio** de la sección **Personalizado** del separador **Gestión** del panel de control de {{site.data.keyword.amashort}}.
* El URL de la aplicación de programa de fondo (**Ruta de app**). Necesitará estos valores para enviar solicitudes a los puntos finales protegidos de la aplicación de programa de fondo.
* Su {{site.data.keyword.Bluemix_notm}} **Región**. Encontrará su región de {{site.data.keyword.Bluemix_notm}} actual en la cabecera, junto al icono **Avatar** ![icono Avatar](images/face.jpg "icono Avatar"). El valor de región que aparece debe ser uno de los siguientes: `EE.UU. Sur`, `Reino Unido` o `Sidney` y debe corresponder con los valores de SDK necesarios en el código Javascript: `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_SYDNEY` o `BMSClient.REGION_UK`. Necesitará este valor para inicializar el cliente {{site.data.keyword.amashort}}.
* El URI para la redirección final (una vez que finalice el proceso de autorización). Es el valor de **URI de redirección de su aplicación web** que ha especificado en la sección **Personalizado** del separador **Gestión**.

Para obtener más información:

* [Iniciación a {{site.data.keyword.amashort}}](getting-started.html)
* [Utilización de un proveedor de identidad personalizado](custom-auth.html)
* [Creación de un proveedor de identidad personalizado](custom-auth-identity-provider.html)
* [Configuración de {{site.data.keyword.amashort}} para la autenticación personalizada](custom-auth-config-mca.html)


## Creación de un proveedor de identidad personalizado
{: #custom-auth-config}

Al crear un proveedor de identidad personalizado, debe definir un método POST con una ruta en la estructura siguiente:

`/apps/:tenantID/<your-realm-name>/handleChallengeAnswer`

`tenantID` es un parámetro de URL y `<your-realm-name>` es cualquier nombre de dominio que haya elegido.

El cuerpo de la solicitud contendrá un objeto `challengeAnswer` que contiene `nombre de usuario` y `contraseña`.

Después de validar el usuario, esta ruta debe devolver un objeto JSON de la estructura siguiente:

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

**Nota:** El campo `attributes` es opcional.

El código siguiente muestra una solicitud POST.

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


## Configuración de {{site.data.keyword.amashort}} para la autenticación personalizada
{: #custom-auth-config-mca}

Una vez que haya configurado el proveedor de identidad personalizado, puede habilitar la autenticación personalizada en el panel de control {{site.data.keyword.amashort}}.

1. Abra el servicio en el panel de control de {{site.data.keyword.amashort}}.
1. En el separador **Gestionar**, active **Autorización**.
1. Expanda la sección **Personalizada**.
1. Especifique el **Nombre de dominio** y el **URL de proveedor de identidad personalizado**.
1. Especifique el valor **URI de redireccionamiento de la aplicación web**. Es el URI de la última redirección después de una autorización correcta.
1. Pulse **Guardar**.


## Implementación del flujo de autorización de {{site.data.keyword.amashort}} utilizando un proveedor de identidad personalizado
{: #custom-auth-flow}

La variable de entorno `VCAP_SERVICES` se crea automáticamente para cada instancia de servicio de {{site.data.keyword.amashort}} y contiene propiedades que son necesarias para el proceso de autorización. Consta de un objeto JSON y se puede ver en el separador **Credenciales de servicio** del panel de control de {{site.data.keyword.amashort}}.

Para solicitar la autorización de usuario, redirija el navegador al punto final del servidor de autorización. Para ello:

1. Recupere el punto final de autorización (`authorizationEndpoint`) y el ID de cliente (`clientId`) de las credenciales de servicio almacenadas en la variable de entorno `VCAP_SERVICES`.

	`var cfEnv = require("cfenv");`

	`var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;`

	**Nota:** En el caso de que haya añadido el servicio de {{site.data.keyword.amashort}} a la aplicación antes de que se añadiera el soporte web, es posible que no tenga el punto final de la señal en las credenciales del servicio. En este caso, utilice las URL siguientes, en función de la región de {{site.data.keyword.Bluemix_notm}}:

	EE.UU. sur:

	`  https://mobileclientaccess.ng.bluemix.net/oauth/v2/authorization 
  `

	Londres:

	` https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/authorization
   `

	Sídney:

	`  https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/authorization 
  `

2. Cree el URI del servidor de autorizaciones utilizando `response_type("code")`, `client_id` y `redirect_uri` como parámetros de consulta.  

3. Redireccione desde su app web al URI generado.

   En el ejemplo siguiente se recuperan los parámetros de la variable `VCAP_SERVICES`, se crea el URL y se envía la solicitud de redireccionamiento.

	```Java
var cfEnv = require("cfenv"); 
app.get("/protected", checkAuthentication, function(req, res, next){ 
		res.send("Hello from protected endpoint"); 
  }
	);

	function checkAuthentication(req, res, next){ 
		// Compruebe si el usuario está autenticado
  if (req.session.userIdentity){ 
			next()
		} else {
			// Si no - redireccione al servidor de autorizaciones
    var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;
    var authorizationEndpoint = mcaCredentials.authorizationEndpoint;
    var clientId = mcaCredentials.clientId;
    var redirectUri = "http://some-server/oauth/callback"; // El URI de redirección de la aplicación web
    var redirectUrl = authorizationEndpoint + "?response_type=code";
    redirectUrl += "&client_id=" + clientId;
    redirectUrl += "&redirect_uri=" + redirectUri;
    res.redirect(redirectUrl);
  } 
	}
	```
	{: codeblock}

	Tenga en cuenta que el parámetro `redirect_uri` representa su URI de redirección de aplicación Web y debe ser igual a la definida en el panel de control de {{site.data.keyword.amashort}}.  

	Un parámetro `state` se puede pasar junto con la solicitud. Este parámetro se propagará al método POST del proveedor de identidad personalizado, y se puede acceder a él desde el cuerpo de la solicitud (`req.body.stateId`).  

	Una vez que haya redirigido al punto final de autorización, el usuario obtendrá un formulario de inicio de sesión. Una vez que se hayan autenticado las credenciales de usuario con el proveedor de identidad personalizado, el servicio de {{site.data.keyword.amashort}} llamará al URI de redirección de la aplicación Web que suministra el código de concesión como un parámetro de consulta.  

	Tras el redireccionamiento, el usuario obtendrá un formulario de inicio de sesión. Una vez que el proveedor de identidad personalizado autentique las credenciales del usuario, el servicio de {{site.data.keyword.amashort}} llamará al URI de redirección de la aplicación web, facilitando el código de concesión como un parámetro de consulta.

## Obtención de las señales
{: custom-auth-tokens}

El siguiente paso consiste en obtener la señal de acceso y la señal de identidad utilizando el código de concesión recibido anteriormente. Para ello:

1. Recupere `authorizationEndpoint`, `clientId` y `secret` de las credenciales de servicio almacenadas en la variable de entorno `VCAP_SERVICES`.

	**Nota:** En el caso de que haya añadido el servicio de {{site.data.keyword.amashort}} a la aplicación antes de que se añadiera el soporte Web, es posible que no tenga el punto final de la señal en las credenciales del servicio. En este caso, utilice las URL siguientes, en función de la región de {{site.data.keyword.Bluemix_notm}}:

	EE.UU. sur:

	`    https://mobileclientaccess.ng.bluemix.net/oauth/v2/token 
     `

	Londres:

	`    https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/token  
     `

	Sídney:

	`     https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/token 
 `

2. Envíe una solicitud POST al URI de servidor de señal con `grant_type`, `client_id`, `redirect_uri` y `code` como parámetros de formulario y `clientId` y `secret` como credenciales de autenticación HTTP básicas.

	En el siguiente ejemplo, el código siguiente recupera los valores necesarios, y los envía con una solicitud POST.

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

	Tenga en cuenta que el parámetro `redirect_uri` debe coincidir con el `redirect_uri` utilizado previamente en la solicitud de autorización. El valor de parámetro code debe ser el código de concesión recibido en la respuesta al final de la solicitud de autorización. El código de concesión es válido solo para 10 minutos, tras los que necesitará obtener un código nuevo.

	El cuerpo de respuesta contendrá `access_token` e `id_token` en formato JWT. Consulte el [sitio web de JWT ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://jwt.io "Icono de enlace externo"){: new_window}.

	Una vez que haya recibido acceso, y la identidad de las señales, puede señalar la sesión web como autenticada y, opcionalmente, persistir estas señales


## Utilización de la señal de identidad y del acceso obtenido
{: #custom-auth-using-token}

La señal de identidad contiene información sobre la identidad del usuario. En caso de una autenticación personalizada, la señal contendrá toda la información devuelta por el proveedor de identidad personalizado al autenticar. En el campo `imf.user`, el campo `displayName` contendrá el `displayName` devuelto por el proveedor de identidad personalizado, y el campo `id` contendrá el `userName`.  Todos los demás valores devueltos por el proveedor de identidad personalizado se devuelven en el campo `attributes` en `imf.user`.  

La señal de acceso permite la comunicación con los recursos protegidos por los filtros de autorización de {{site.data.keyword.amashort}} (consulte [Protección de recursos](protecting-resources.html)). Para realizar solicitudes a los recursos protegidos, añada una cabecera de autorización a las solicitudes con la estructura siguiente:

`Authorization=Bearer <accessToken> <idToken>`

#### Sugerencias:
{: #tips_token}

* El `<accessToken>` y el `<idToken>` deben estar separados por un espacio en blanco.

* La señal de identidad es opcional. En el caso de que no proporcione la señal de identidad, podrá acceder al recurso protegido, pero no recibirá ninguna información sobre el usuario autorizado.
