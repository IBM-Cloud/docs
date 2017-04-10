---

copyright:
  years: 2017
lastupdated: "2017-03-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Configuración de los proveedores de identidad
{: #setting-up-idp}

Puede configurar Facebook, Google o ambos para autenticar las aplicaciones y autorizar el acceso a recursos de fondo protegidos.
{:shortdesc}


## Facebook
{: #facebook}

Configure el servicio de {{site.data.keyword.appid_short}} para utilizar Facebook como proveedor de identidad.

<!--- ### Sequence diagram
{: #facebook-sequence-diagram}--->

### Obtención de un ID de app y secreto de Facebook
{: #getting-facebook-appid}

Para utilizar Facebook como proveedor de identidad en sus apps web o móviles, debe añadir y configurar la plataforma de sitio web en su aplicación de Facebook.

1. Inicie sesión en su cuenta en el sitio Facebook for Developers. Para obtener información sobre cómo crear una nueva app de Facebook, consulte <a href="https://developers.facebook.com/docs/apps/register" target="_blank">Creación de una aplicación <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.
2. Anote el ID y el secreto de la app de Facebook. Necesitará estos valores para configurar el proyecto web para la autenticación en el panel de control de servicio.
3. Añada la plataforma web y especifique el URL del sitio.
4. En la lista de productos, seleccione **Inicio de sesión de Facebook **.
5. En el campo URL de redirección de OAuth válidos, especifique el URL de punto final de devolución de llamada del servidor de autorización. Puede añadir este valor después de configurar el servicio de {{site.data.keyword.appid_short_notm}} en los pasos siguientes.
6. Pulse **Guardar cambios**.

### Configuración de {{site.data.keyword.appid_short_notm}} para la autenticación de Facebook
{: #configuring-facebook-appid}

Una vez que tenga el ID y secreto de la app de Facebook, y que la app de Facebook for Developers esté configurada para prestar servicio a los clientes web, puede editar la autenticación de Facebook en el panel de control del servicio.

1. Desde el separador **Gestionar** del panel de control del servicio, seleccione **Facebook** y pulse **Editar**.
2. Especifique el ID y el secreto de la app de Facebook que ha obtenido del sitio web de Facebook for Developers.
3. Copie el URI que está en el campo **URI de redirección para Facebook for Developers**. Copie el URI en el campo **URI de redirección de OAuth válido** en la sección **Inicio de sesión de Facebook** del portal de desarrolladores de Facebook.
4. Pulse **Guardar**.
5. Opcional: para configurar la autenticación para apps web, especifique el URI de redirección en los URI de redirección de la aplicación web. Este valor está determinado por el desarrollador y se utiliza para acceder al URI de redirección una vez completado el proceso de autorización.


## Google
{: #google}

Configure el servicio de {{site.data.keyword.appid_short_notm}} para utilizar Google como proveedor de identidad.

<!--- ### Sequence diagram
{: #google-sequence-diagram}--->

### Obtención de un ID de cliente y secreto de Google
{: #google-client-id}

Para utilizar Google como proveedor de identidad, obtenga un ID de cliente y secreto de Google y cree un proyecto en Google Developer Console.

1. Abra la aplicación de Google en la consola del desarrollador de Google.
2. Añada la API de Google+.
3. Cree credenciales mediante OAuth. En el campo **Tipo de aplicación**, seleccione **Aplicación web**. En el campo **URI de redirección autorizados**, especifique el URI de redirección de ID de app. Puede obtener el URI de autorización de redirección de ID de app desde la pantalla de configuración de Google del panel de control del servicio.
4. Guarde los cambios. Anote el ID de cliente y secreto de Google.




### Configuración de {{site.data.keyword.appid_short_notm}} para la autenticación de Google
{: #google-client-appid}

Una vez que tenga el cliente y secreto de Google, y la consola de Google Developers esté configurada para prestar servicio a los clientes web, puede editar la autenticación de Google en el panel de control del servicio.

1. Desde el separador **Gestionar** del panel de control del servicio, seleccione **Google** y pulse **Editar**.
3. Especifique el ID de cliente y el secreto de Google que ha obtenido de la consola de Google Developers.
4. Copie el URI que está en el campo **URI de redirección para Google for Developers**. Copie el URI en el campo **URI de redirección autorizados** que se encuentra en **Restricciones** en la sección **ID de cliente para la aplicación web** del portal de desarrolladores de Google.
5. Pulse **Guardar**.
6. Opcional: para configurar la autenticación para apps web, especifique el URI de redirección en el campo URI de redirección de la aplicación web. Este valor se determina por parte del desarrollador y el que se utiliza para acceder a la redirección URI después de la autorización proceso se completa.



<!---[## Bring your own OAuth2/OIDC identity provider
{: #oauth2}

### About
{: #oauth2-about}
### Sequence diagram
{: #oauth2-sequence-diagram}
### Configuring AppID for BYOIDP OAuth2 authentication
{: #oauth2-appid} SHAWNA: Is this Interconnect?]--->
