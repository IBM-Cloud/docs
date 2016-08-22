---

copyright:
  year: 2016

---

# Habilitación de la autenticación de Facebook para aplicaciones web

*Última actualización: 18 de julio de 2016*
{: .last-updated}

Utilice Facebook para autenticar usuarios para la app web.

## Antes de empezar
{: #facebook-auth-android-before}
Debe tener lo siguiente:
* Una app web. 
* Una instancia de una aplicación {{site.data.keyword.Bluemix_notm}} que esté protegida por el servicio {{site.data.keyword.amashort}}. Para obtener más información sobre la creación de una aplicación de fondo {{site.data.keyword.Bluemix_notm}}, consulte [Cómo empezar](index.html).
* El URI para la redirección final (una vez que finalice el proceso de autorización).


## Configuración de la aplicación de Facebook para su sitio web
Para utilizar Facebook como proveedor de identidad en su sitio web, debe añadir y configurar la plataforma de sitio web en su aplicación de Facebook.

1. Inicie la sesión en el Facebook Developers Portal (https://developers.facebook.com).
2. Abra o cree la app.
1. Tenga en cuenta el **ID de aplicación** y el **Secreto de app**. Necesitará estos valores al configurar el proyecto web para la autenticación de Facebook en el panel de control de {{site.data.keyword.amashort}}.
1. Añada la plataforma del sitio web en el caso de que no exista.
1. Añada o abra el **Inicio de sesión de Facebook** desde la lista de Productos.
1. Especifique el URI de punto final de devolución de llamada del servidor de autorización en el cuadro **URI de redirección de OAuth válidos**. Busque este URI de redireccionamiento de autorización en los pasos de configuración del panel de control de {{site.data.keyword.amashort}} a continuación.
2. Guarde los cambios realizados.




# Configuración de {{site.data.keyword.amashort}} para la autenticación de Facebook
Una vez que tenga el ID de la aplicación de Facebook y el secreto de la app, y que la autenticación de Facebook esté configurada para prestar servicio a clientes web, puede habilitar la autenticación de Facebook en el panel de control de {{site.data.keyword.Bluemix_notm}}.

1. Abra el panel de control {{site.data.keyword.Bluemix_notm}}.
1. Pulse el mosaico de aplicación relevante. La aplicación se cargará.
2. Pulse el mosaico para el servicio de {{site.data.keyword.amashort}}.
1. Pulse el botón **Configurar** del panel **Facebook**.
2. Anote el valor en el recuadro de texto de **URI de redireccionamiento de Mobile Client Access para la consola de Facebook Developer**. Este es el valor que tiene que añadir al recuadro **URI de redirección de OAuth válido** en el **Inicio de sesión de Facebook** del portal de Facebook Developers en el paso 6 anterior.
1. Especifique el **ID de aplicación** y el **Secreto de la app** de Facebook.
2. Especifique el URI de redireccionamiento en las **URI de redireccionamiento de la aplicación web**. Este valor es para que se acceda a la URI de redireccionamiento una vez que se haya completado el proceso de autorización, y que lo determine el desarrollador.
3. Pulse **Guardar**.




## Implementación del flujo de autorización de {{site.data.keyword.amashort}} utilizando Facebook como proveedor de identidad

La variable de entorno `VCAP_SERVICES` se crea automáticamente para cada instancia de servicio de {{site.data.keyword.amashort}} y contiene propiedades necesarias para el proceso de autorización. Consta de un objeto JSON y se puede ver si se pulsa **Variables de entorno** en el navegador de la izquierda de la aplicación.

Para iniciar el proceso de autorización:

1. Recupere el punto final de autorización (`authorizationEndpoint`) y el ID de cliente (`clientId`) de las credenciales de servicio almacenadas en la variable de entorno `VCAP_SERVICES`. 

    **Nota:** En el caso de que haya creado el servicio de {{site.data.keyword.amashort}} antes de que se añadiera el soporte web, es posible que no tenga puntos finales de autorización en las credenciales de servicio. En este caso, utilice los siguientes puntos finales de autorización en función de la región de Bluemix:
  
  EE.UU. sur: 
  ```
  https://mobileclientaccess.ng.bluemix.net/oauth/v2/authorization
   ```
  Londres:
  ``` 
 https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/authorization
   ```
  Sídney:
  ```
 https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/authorization
  ```
2. Cree el URI del servidor de autorizaciones utilizando `response_type("code")`, `client_id` y `redirect_uri` como parámetros de consulta. 
3. Redireccione desde su app web al URI generado.



El ejemplo siguiente recupera los parámetros de la variable `VCAP_SERVICES`, creando el URL y enviando la solicitud de redireccionamiento.

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
  // Si no - redireccione al servidor de autorización
        var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;
        var authorizationEndpoint = mcaCredentials.authorizationEndpoint;
        var clientId = mcaCredentials.clientId;
        var redirectUri = "http://some-server/oauth/callback";
         // El URI de redireccionamiento de la aplicación web

        var redirectUrl = authorizationEndpoint + "?response_type=code";
        redirectUrl += "&client_id=" + clientId;   
        redirectUrl += "&redirect_uri=" + redirectUri;   
  
        res.redirect(redirectUrl);  
  
      } 
  }
  
 ```

   El parámetro `redirect_uri` es el URI para la redirección, después de una autenticación satisfactoria o con error con Facebook.
   

 Una vez que haya redirigido al punto final de autorización, obtendrá un formulario de inicio de sesión desde
Facebook. Una vez que Facebook autorice la identidad del usuario, el servicio de {{site.data.keyword.amashort}} invocará el URI de redireccionamiento de la aplicación web, que suministra el código de concesión como un parámetro de consulta.  
## Obtención de las señales

El siguiente paso consiste en obtener las señales de acceso y de identidad utilizando el código de concesión recibido anteriormente:

 1.  Recupere la señal `tokenEndpoint`, `clientId` y `secret` desde las credenciales de servicio almacenadas en la variable de entorno `VCAP_SERVICES`. 
 
    **Nota:** En caso de que haya utilizado Mobile Client Access antes de que se añadiera el soporte web, es posible que no tenga el punto final de señal en las credenciales de servicio. En este caso, utilice los URL en función de la región de Bluemix: 

    EE.UU. sur: 
    ```
    https://mobileclientaccess.ng.bluemix.net/oauth/v2/token 
     ```
  Londres:
  ```
    https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/token  
     ```
  Sídney:
  ```
    https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/token 
    ```

 1. Envíe una solicitud de publicación a la URI de servidor de señal con el tipo de concesión ("authorization_code"), `clientId`, y el URI de redireccionamiento como parámetros de formulario. Envíe el `clientId` y `secret` como credenciales de autenticación HTTP básicas.
 
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
      redirect_uri: "http://some-server/oauth/callback",
     // El URI de redirección de la aplicación web
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
 
 Tenga en cuenta que el parámetro `redirect_uri` debe coincidir con el `redirect_uri` utilizado para la solicitud de autorización anterior. El valor de parámetro `code` debe ser el código de concesión recibido en la respuesta desde la solicitud de autorización. El código de concesión es válido para 10 minutos, tras los cuales se debe recuperar un código nuevo.

El cuerpo de respuesta contendrá el código de acceso y el ID de señal en formato JWT (https://jwt.io/).

Una vez que tenga acceso y que haya recibido las señales de identidad, puede señalar la sesión web como se indica y, opcionalmente, persistir estas señales.  

##Utilización de la señal de identidad y del acceso obtenido 

La señal de identidad contiene información sobre la identidad del usuario. En caso de la autenticación de Facebook, la señal contendrá toda la información que el usuario esté de acuerdo en compartir, como el nombre completo, el grupo de edad, el URL de la foto de perfil, etc.  

La señal de acceso permite comunicaciones con recursos protegidos por filtros de autorización de {{site.data.keyword.amashort}}, consulte [Protección de recursos](protecting-resources.html).


Para realizar solicitudes en los recursos protegidos, añada una cabecera de autorización a las solicitudes con la estructura siguiente: 

`Authorization=Bearer <accessToken> <idToken>`

**Nota:** 

* El `accessToken` e `idToken` deben estar separados por un espacio en blanco.

* El `idToken` es opcional. En el caso de que no proporcione la señal de identidad, se puede acceder al recurso protegido, pero no recibirá ninguna información sobre el usuario autorizado. 
 



