---

copyright:
  year: 2016, 2017
lastupdated: "2017-01-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Habilitación de la autenticación de Google para aplicaciones web
{: #google-auth-web}

Utilice el inicio de sesión de Google para autenticar usuarios para la aplicación web. Añada la funcionalidad de seguridad de {{site.data.keyword.amafull}}.


## Antes de empezar
{: #before-you-begin}

Debe tener lo siguiente:

* Una app web.
* Una instancia de una aplicación {{site.data.keyword.Bluemix_notm}} que esté protegida por el servicio {{site.data.keyword.amashort}}. Para obtener más información sobre la creación de una aplicación de fondo {{site.data.keyword.Bluemix_notm}}, consulte [Cómo empezar](index.html).
* El URI para la redirección final (una vez que finalice el proceso de autorización).


## Configuración de la aplicación de Google para su sitio web
{: #google-auth-config}

Para empezar a utilizar Google como proveedor de identidad, cree un proyecto en la [Google Developer Console ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.developers.google.com "Icono de enlace externo"){: new_window}.
Parte de la creación de un proyecto consiste en obtener un **ID de cliente de Google** y **Secreto**. El ID de cliente de Google y Secreto son los únicos identificadores para la aplicación utilizados por la autenticación de Google y se necesitan para configurar el panel de control de {{site.data.keyword.amashort}}.

1. Abra la aplicación de Google en la consola del desarrollador de Google.
3. Añada la API de **Google+**.
3. Cree credenciales mediante OAuth. Seleccione la Aplicación web en el tipo de aplicación. Especifique el URI de redireccionamiento de {{site.data.keyword.amashort}} en el recuadro URI de redirección autorizados. Obtenga el URI de autorización de redireccionamiento de {{site.data.keyword.amashort}} desde la pantalla de configuración de Google del panel de control de {{site.data.keyword.amashort}} (consulte los pasos siguientes).
4. Guarde los cambios realizados. Anote el **ID de cliente de Google** y el **Secreto de la aplicación**.


## Configuración de {{site.data.keyword.amashort}} para la autenticación de Google
{: #google-auth-config-ama}

Una vez que ya tenga el ID de aplicación y el secreto de Google puede habilitar la autenticación de Google en el panel de control de {{site.data.keyword.amashort}}.

1. Abra el panel de control del servicio de {{site.data.keyword.amashort}}.
1. En el separador **Gestionar**, active **Autorización**.
1. Abra la sección **Google**.
1. Marque **Añadir Google a la app web**
4. En la sección **Configurar para web**:   
    * Anote el valor en el recuadro de texto de **URI de redireccionamiento de Mobile Client Access para la consola de Google Developer**. Este es el valor que tiene que añadir al recuadro **URI de redirección autorizados** en **Restricciones en el ID de cliente para la aplicación web** del **Portal de Google Developers**.
    * Especifique el **ID de cliente** y el **Secreto de cliente**.
    * Especifique el URI de redireccionamiento en las **URI de redireccionamiento de la aplicación web**. Este valor es para que se acceda a la URI de redireccionamiento una vez que se haya completado el proceso de autorización, y que lo determine el desarrollador.
5. Pulse **Guardar**.


## Implementación del flujo de autorización de {{site.data.keyword.amashort}} utilizando Google como proveedor de identidad
{: #google-auth-flow}

La variable de entorno `VCAP_SERVICES` se crea automáticamente para cada instancia de servicio de {{site.data.keyword.amashort}} y contiene propiedades necesarias para el proceso de autorización. Consta de un objeto JSON y se puede ver pulsando en el separador **Credenciales de servicio** del panel de control del servicio de {{site.data.keyword.amashort}}.

Para iniciar el proceso de autorización:

1. Recupere el punto final de autorización (`authorizationEndpoint`) y el clientId (`clientId`) de las credenciales de servicio almacenadas en la variable de entorno `VCAP_SERVICES`.

	`var cfEnv = require("cfenv");`

	`var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;`

	**Nota:** En el caso de que haya añadido el servicio de {{site.data.keyword.amashort}} a la aplicación antes de que se añadiera el soporte Web, es posible que no tenga el punto final de la señal en las credenciales del servicio. En este caso, utilice las URL siguientes, en función de la región de {{site.data.keyword.Bluemix_notm}}:

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

	En el ejemplo siguiente se recuperan los parámetros de la variable `VCAP_SERVICES`, creando el URL y enviando la solicitud de redireccionamiento.

	```Java
var cfEnv = require("cfenv"); 
app.get("/protected", checkAuthentication, function(req, res, next){ 
		res.send("Hello from protected endpoint"); 
 }); 

	app.get("/protected", checkAuthentication, function(req, res, next){ 
		res.send("Hello from protected endpoint"); 
 	function checkAuthentication(req, res, next){ 

			// Compruebe si el usuario está autenticado
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
	   	}
       }
	```
	{: codeblock}

	Tenga en cuenta que el parámetro `redirect_uri` representa su URI de redirección de aplicación Web y debe ser igual a la definida en el panel de control de {{site.data.keyword.amashort}}.

	Una vez que haya redirigido al punto final de autorización, el usuario obtendrá un formulario de inicio de sesión de Google. Después de que el usuario otorgue permisos para iniciar la sesión utilizando su identidad de Google, el servicio de {{site.data.keyword.amashort}} invocará el URI de redireccionamiento de la aplicación web, suministrando el código de concesión como un parámetro de consulta.

## Obtención de las señales
{: #google-auth-tokens}

El siguiente paso consiste en obtener la señal de acceso y las señales de identidad utilizando el código de concesión previamente recibido.

1. Recupere la señal `tokenEndpoint`, `clientId` y `secret` desde las credenciales de servicio, almacenadas en la variable de entorno `VCAP_SERVICES`.

	**Nota: ** En el caso de que haya utilizado {{site.data.keyword.amashort}} antes de que se añadiera el soporte web, es posible que no tenga puntos finales de la señal en las credenciales del servicio. En este caso, utilice los URL siguientes, en función de la región de Bluemix:

	EE.UU. sur:

	`    https://mobileclientaccess.ng.bluemix.net/oauth/v2/token 
     `

	Londres:

	`    https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/token  
     `

	Sídney:

	`     https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/token 
 `

2. Envíe una solicitud POST al URI de servidor de señal con grant_type ("authorization_code"), client_id, redirect_uri y code como parámetros de formulario. Envíe `clientId` y `clientSecret` como credenciales de autenticación HTTP básicas.

	El código siguiente recupera los valores necesarios, y los envía con una solicitud POST.

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

	El parámetro `redirect_uri` es el URI para la redirección, después de una autenticación satisfactoria o con error con Google+, y debe coincidir con el `redirect_uri` definido en el panel de control de {{site.data.keyword.amashort}}.  

	Asegúrese de enviar esta solicitud POST en el plazo de 10 minutos tras los cuales caducará el código de concesión. Después de 10 minutos, se necesitará un código nuevo.

	El cuerpo de la respuesta POST contiene el `access_token` y el `id_token` codificado en base64.

	Una vez que haya recibido el acceso, y la identidad de las señales, puede señalar la sesión web como autenticada y, opcionalmente, persistir estas señales.  


## Utilización de la señal de identidad y del acceso obtenido
{: #google-auth-using-token}

La señal de identidad contiene información sobre la identidad del usuario. En el caso de la autenticación de Google, la señal contiene toda la información que el usuario esté de acuerdo en compartir, como el nombre completo, el URL de la foto de perfil, etc.  

La señal de acceso permite comunicaciones con los recursos que están protegidos por filtros de autorización de {{site.data.keyword.amashort}}. Más información sobre [Protección de recursos](protecting-resources.html).

Para realizar solicitudes a los recursos protegidos, añada una cabecera de autorización a las solicitudes con la estructura siguiente:

`Authorization=Bearer <accessToken> <idToken>`

#### Sugerencias:
{: #tips}

* El `accessToken` e `idToken` deben estar separados por un espacio en blanco.

* El `idToken` es opcional. En el caso de que no proporcione la señal de identidad, se puede acceder al recurso protegido, pero no recibirá ninguna información sobre el usuario autorizado.
