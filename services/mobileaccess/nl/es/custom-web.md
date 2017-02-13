---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-08"

---

# Autenticación personalizada de la app web
{: #custom-web}

Añadir autenticación personalizada a la app web

## Antes de empezar
{: #before-you-begin}

Debe tener lo siguiente:
* Una app web con un punto final `/apps/:Guid/<RealmName>/handleChallengeAnswer`, que devuelve la identidad del usuario después de una autenticación correcta. La estructura JSON de la identidad debe ser de este modo:

   ```json
  userIdentity: {
  userName: <nombre_usuario>,
  displayName: <nombre_visualización>;
 };
```
* Una instancia de una aplicación {{site.data.keyword.Bluemix_notm}} que esté protegida por el servicio {{site.data.keyword.amashort}}. Para obtener más información sobre la creación de un programa de fondo {{site.data.keyword.Bluemix_notm}}, consulte [Cómo empezar](index.html).



## Configuración de una app {{site.data.keyword.amashort}} para autenticación personalizada


1. Abra la app en el panel de control de {{site.data.keyword.Bluemix_notm}}.
1. Pulse el icono de {{site.data.keyword.amashort}}. Se cargará el panel de control de {{site.data.keyword.amashort}}.
1. Pulse el icono de Personalizado.
1. Especifique **custom realm**, **custom identity provider url** y **redirect_uri**. Pulse Guardar.

## Utilización de {{site.data.keyword.amashort}} para la autenticación web personalizada

Para iniciar el proceso de autorización:

1. Redireccione desde su app web al siguiente punto final del servidor de autorización:

    https://imf-newauthserver.bluemix.net/oauth/v2/authorization

  con estos parámetros de consulta:
   ```
   response_type=’authorization_code’
   client_id= <bluemix\_app\_guid>
   redirect_uri= <uri para redirección después de obtener código de autorización>
   scope= ‘openid’
   state= <estado>
   ```

    El parámetro `state` no se utiliza por ahora y puede dejarlo en blanco.

    El parámetro `redirect_uri` determina la redirección después de una autenticación satisfactoria o errónea del proveedor de identidades personalizadas.

1. Una vez que haya redirigido al punto final de autorización, obtendrá un formulario de inicio de sesión. Especifique el nombre de usuario y la contraseña para iniciar la autenticación ante el proveedor de identidad y una redirección a `redirect_uri`.
La respuesta devuelta después de una autenticación satisfactoria contiene el código de autorización en los parámetros de consulta de la solicitud.

4. Realice una solicitud `POST` para el punto final del elemento de servidor de autorización:

 https://imf-newauthserver.bluemix.net/*oauth/v2/token

 con estos parámetros de consulta:
 ```
 grant_type = 'authorization_code'
 client_id = <guid_app_bluemix>
 redirect_uri = <uri_redirección>
 code = <código_autorización>
 ```
  El parámetro `redirect_uri` debe coincidir con el `redirect_uri` del paso 1. El código de autorización lo devuelve la solicitud del paso 2.

  Asegúrese de enviar esta solicitud `POST` en el plazo de 10 minutos porque el código de concesión es válido durante 10 minutos como máximo.

El cuerpo de la respuesta `POST` contiene el *access_token* y el *id_token* codificado en base64.

## Prueba de autenticación


Ahora puede empezar a realizar solicitudes a los recursos protegidos.
Todas las solicitudes a recursos protegidos deben contener el `access_token`.
Envíe el elemento de acceso en el campo del encabezado `the-Authorization-request`.
