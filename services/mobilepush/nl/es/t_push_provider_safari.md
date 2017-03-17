---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configuración de credenciales para navegadores web
{: #configure-credential-for-browsers}
Última actualización: 11 de enero de 2017
{: .last-updated}

El servicio IBM {{site.data.keyword.mobilepushshort}} amplía sus funciones para enviar notificaciones al navegador. 

El servicio {{site.data.keyword.mobilepushshort}} necesita el URL del sitio web o el nombre del dominio del sitio web para identificar las solicitudes que se deben permitir. Una instancia de servicio de {{site.data.keyword.mobilepushshort}} solo admite un nombre de dominio. Por lo tanto, asegúrese de que se haya establecido el mismo valor para Chrome, Firefox y Safari. 

Los navegadores Chrome y Safari necesitan configuración adicional para push we,. Necesitaría una clave de API de FCM, ya que se utiliza un punto final FCM para distribuir mensajes en Chrome. Para obtener una clave de API de FCM, consulte [Configuración de credenciales para FCM](t_push_provider_android.html).



##Configuración para push web de Chrome y Firefox 
{: #config-chrome-firefox}

1. En el panel de control de Push, seleccione **Configurar**.
2. Seleccione el separador Web.
	![Configuraciones de push web](images/webpush_configure.jpg)
3. Configure la clave de la API de FCM/GCM y el URL del sitio web que se registrará para la recepción de notificaciones por push.
4. Pulse **Guardar**.
5. Pasos siguientes. [Habilitación de notificaciones para navegadores Google Chrome y Mozilla Firefox](c_enable_push.html).


## Configuración de push web de Safari 
{: #configure-safari}

La versión admitida para el servicio de {{site.data.keyword.mobilepushshort}} en Safari es 10.0. Debe generar un certificado a través de su cuenta de Apple Developer para poder configurar el navegador para que reciba notificaciones.

### Generación de un certificado
{: #certificate-generation}

Asegúrese de disponer de una cuenta de desarrollador de Apple. Tiene que registrar un Push ID del sitio web y generar un certificado para configurar Safari para que reciba notificaciones. Comience siguiendo estos pasos.

1. En el centro Apple Developer Member, pulse **Certificados, ID y Perfiles**. 
2. Pulse **Identificadores** y luego **ID Push del sitio web**.
3. Elija crear una nueva entrada seleccionando el icono del signo más.
  ![Panel de control de Push](images/safari_1.jpg)

4. En el panel Registrar ID Push del sitio web, especifique una descripción adecuada del ID Push del sitio web y un ID identificador. Se recomienda que esté en formato de nombre de dominio invertido, comenzando por 'web'. Por ejemplo: web.com.example.dailyweatherreports.
5. Registre el ID Push del sitio web. Ahora tiene el ID Push del sitio web 
6. Seleccione **Editar** para crear un certificado que se utilizará para el ID Push del sitio web.
7. En la ventana Asistente de certificados para la información sobre certificados, especifique su ID de correo electrónico y un nombre común. Deje en blanco la dirección de correo electrónico de la entidad emisora de certificados.
8. Pulse **Guardar en disco** y seleccione **Continuar**.
9. Guarde el certificado en una carpeta adecuada.
10. Seleccione el `.certSigningRequest` creado en el disco cuando se le solicite en el asistente para generar el certificado. Asegúrese de que descarga el certificado push del sitio web creado en el formato `.cer`.
11. Abra el Certificado en la herramienta KeyChain Access. Pulse con el botón derecho del ratón y exporte como certificado p12. Anote la contraseña que se facilita durante la generación del certificado p12.


### Configuración para notificaciones
  {: #configuration-notification}
 
Tras generar el certificado, puede configurar el servicio para enviar notificaciones a Safari. 

Complete los pasos:

1. En el panel de control de servicio de Notificaciones Push, **pulse Configurar**. 
2. Seleccione el separador Web. 
3. En la sección Push de Safari, actualice el formulario con la información necesaria. 
	- **Nombre del sitio web**: Este es el nombre que ha facilitado en el Centro de notificaciones.
	- **ID Push del sitio web**: Actualice con la serie de dominio invertido para el ID Push del sitio web. Por ejemplo, web.com.ejemplo.www.
	- **URL del sitio web**: Proporcione el URL del sitio web que debería estar suscrito a notificaciones push. Por ejemplo, https://www.ejemplo.com.
	- **Dominios permitidos**: Este es un parámetro opcional. Es la lista de sitios web que solicita permiso del usuario. Asegúrese de que las URL sean valores separados por coma. Tenga en cuenta que el valor del URL del sitio web se utilizará si no se proporciona. 
	- **Serie de formato de URL**: El URL a resolver cuando se pulse la notificación. Por ejemplo, ["https://www.ejemplo.com"]. Asegúrese de que el URL utilice el esquema http o https.
	- **Certificado Push web de Safari**: Cargue el certificado .p12 y proporcione la contraseña.
4. Pulse **Guardar**.	

![Panel de control de Push](images/push_configure_safari.jpg)	

Ya tiene configurado el envío de notificaciones push para el navegador Safari.

	
