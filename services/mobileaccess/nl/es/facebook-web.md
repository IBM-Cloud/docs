---

copyright:
  year: 2016, 2017
lastupdated: "2017-01-08"

---

# Habilitación de la autenticación de Facebook para apps de Web
{: #facebook_web}

Utilice Facebook para autenticar usuarios para la app web.

## Antes de empezar
{: #facebook-auth-android-before}
Debe tener lo siguiente:
* Una app web.  
* Una instancia de una aplicación {{site.data.keyword.Bluemix_notm}} que esté protegida por el servicio {{site.data.keyword.amashort}}. Para obtener más información sobre la creación de un programa de fondo {{site.data.keyword.Bluemix_notm}}, consulte [Cómo empezar](index.html).
* Un ID de aplicación de Facebook y un secreto de app. Para obtener más información, consulte [Cómo obtener un ID de aplicación de Facebook desde el portal de desarrolladores de Facebook](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID).


## Configuración de la aplicación de Facebook para su sitio web
Para utilizar Facebook como proveedor de identidad en su sitio web, debe añadir y configurar la plataforma de sitio web en su aplicación de Facebook.

1. Abra la aplicación de Facebook en el portal de desarrolladores de Facebook.
1. Anote el ID de autenticación para su app y secreto de app. Necesitará este valor cuando configure el proyecto web para la autenticación de Facebook.
1. En la página **Configuración**, pulse **Añadir plataforma** y elija **Sitio web**.
1. Guarde los cambios realizados.
1. Pulse **Inicio de sesión de Facebook** en la barra lateral izquierda.
1. Especifique el punto final de devolución de llamada del servidor de autorización en el recuadro **URI de redirección de OAuth válidos**: https://imf-newauthserver.bluemix.net/oauth/{bluemix_app_guid}/callback. Guarde los cambios realizados.




# Configuración de {{site.data.keyword.amashort}} para la autenticación de Facebook
Una vez que tenga el ID de la aplicación de Facebook y el secreto de la app, y que la autenticación de Facebook esté configurada para prestar servicio a clientes web, puede habilitar la autenticación de Facebook en el panel de control de {{site.data.keyword.Bluemix_notm}}.

1. Abra la app en el panel de control de {{site.data.keyword.Bluemix_notm}}.
1. Pulse el icono de {{site.data.keyword.amashort}}. Se cargará el panel de control de {{site.data.keyword.amashort}}.
1. Pulse el icono de Facebook.
1. Especifique el ID de aplicación de Facebook y el secreto de la app, y guarde los cambios.




## Utilización de Mobile Client Access para la autenticación web de Facebook

Para iniciar el proceso de autorización:

1. Redireccione desde su app web al siguiente punto final del servidor de autorización:  https://imf-newauthserver.bluemix.net/oauth/v2/authorization.

1. Añada los siguientes parámetros de consulta:
   ```
    response_type='authorization_code'
    client_id= <bluemix_app_guid>
    redirect_uri= <uri para redireccionar después de recibir el código de autorización>
    scope= 'openid'
    state= <state>
    ```


  El parámetro `state` no se utiliza por ahora y se puede dejar en blanco.
  El parámetro `redirect_uri` es el uri para la redirección después de una autenticación satisfactoria o con error con Facebook.

1. Una vez que haya redirigido al punto final de autorización, obtendrá un formulario de inicio de sesión desde      
   Facebook. Especifique el nombre de usuario y la contraseña para redirigir al `redirect_uri`.
   La respuesta que se obtiene después de la redirección contiene el código de autorización en los parámetros de consulta de la solicitud.

1. Realice una solicitud `POST` para el punto final del elemento de servidor de autorización:

  https://imf-newauthserver.bluemix.net/oauth/v2/token

  con estos parámetros de consulta:
  ```
  grant_type='authorization_code'
  client_id= <guid_app_bluemix>
  code= <código_autorización>
  ```
El parámetro `redirect_uri` debe coincidir con el `redirect_uri` del paso 2.
El valor `code` es el código de autorización recibido en la respuesta al final del paso 3.
Asegúrese de enviar esta solicitud `POST` en el plazo de 10 minutos porque el código de autorización es válido durante 10 minutos como máximo.

  El cuerpo de la respuesta `POST` debería contener el `access_token` y el `id_token` codificado en base64.

## Prueba de autenticación
Ahora puede empezar a realizar solicitudes a los recursos protegidos.
Todas las solicitudes para recursos protegidos deben contener el `access_token` en el campo de cabecera de solicitud de autorización.
