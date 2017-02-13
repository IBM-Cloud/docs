---

copyright:
  year: 2016, 2017
lastupdated: "2017-01-08"

---

# Habilitación de la autenticación de Google para apps de web
{: #google-auth-web}

Utilice el inicio de sesión de Google para autenticar usuarios para la app web.


## Antes de empezar
{: #before-you-begin}

Debe tener lo siguiente:
* Una app web.
* Una instancia de una aplicación {{site.data.keyword.Bluemix_notm}} que esté protegida por el servicio {{site.data.keyword.amashort}}. Para obtener más información sobre la creación de un programa de fondo {{site.data.keyword.Bluemix_notm}}, consulte [Cómo empezar](index.html).

## Configuración de la aplicación de Google para su sitio web
Para empezar a utilizar Google como proveedor de identidad, cree un proyecto en [Google Developer Console](https://console.developers.google.com). Parte de la creación de un proyecto consiste en obtener un ID y un secreto de cliente de Google. El ID de cliente y el secreto de Google son los únicos identificadores para la aplicación utilizados por la autenticación de Google y se necesitan para configurar la aplicación {{site.data.keyword.Bluemix_notm}}.

1. Cree un proyecto utilizando la API de Google+.
1. Cree credenciales mediante **OAuth**. Para crear las credenciales, debe hacer lo siguiente:
    * Seleccionar el tipo de aplicación **Aplicación web**.
    * Proporcionar el valor de **URI de redirección autorizados**:

     https://imf-newauthserver.bluemix.net/oauth/{guid_app_bluemix}/callback
1. Complete el proceso de creación de credenciales y tome nota del ID y del secreto del cliente Google.


## Configuración de {{site.data.keyword.amashort}} para la autenticación de Google
Una vez que ya tenga el ID de aplicación y el secreto de Google puede habilitar la autenticación de Google en el panel de control de {{site.data.keyword.amashort}}.

1. Abra la app en el panel de control de {{site.data.keyword.Bluemix_notm}}.
1. Pulse el icono de {{site.data.keyword.amashort}}. Se cargará el panel de control de {{site.data.keyword.amashort}}.
1. Pulse el icono de Google.
1. Especifique el ID de cliente y el secreto de Google y guarde los cambios.


## Utilización de {{site.data.keyword.amashort}} para la autenticación web de Google
Para iniciar el proceso de autorización:

1. Redireccione desde su app web al siguiente punto final del servidor de autorización:  
  https://imf-newauthserver.bluemix.net/oauth/v2/authorization

  con estos parámetros de consulta:
	```
   response_type='authorization_code'
   client_id= <guid_app_bluemix>
   redirect_uri= <uri que desea devolver después de obtener un código de concesión>
   scope= ‘openid’
   state= <estado>
	```

  El parámetro `state` no se utiliza por ahora y se puede dejar en blanco.

  El uri del parámetro `redirect_uri` es la redirección después de una autenticación correcta o con error de Google.
  La respuesta que se obtiene después de la redirección contiene el código de autorización en los parámetros de consulta de la solicitud.
1. Realice una solicitud `POST` para el punto final del elemento de servidor de autorización:

 https://imf-newauthserver.bluemix.net/oauth/v2/token


  con estos parámetros de consulta:

	```
  	grant_type=’authorization_code’
    client_id= < guid_app_bluemix>
    redirect_uri= <uri_redirección>
    code= <código_autorización>
	```
  El parámetro `redirect_uri` debe coincidir con el `redirect_uri` del paso 1 y el valor de `<authorization code>` se recibe de la respuesta.
  Asegúrese de enviar esta solicitud `POST` en el plazo de 10 minutos porque el código de concesión es válido durante 10 minutos como máximo.

El cuerpo de la respuesta `POST` debería contener el `access_token` y el `id_token` codificado en base64.

## Prueba de autenticación

Ahora puede empezar a realizar solicitudes a los recursos protegidos.
Todas las solicitudes a recursos protegidos deben contener el elemento de acceso en el campo de cabecera de solicitud de autorización.
