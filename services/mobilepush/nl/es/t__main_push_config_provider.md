
---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configuración de credenciales para un proveedor de notificaciones
{: #create-push-credentials}
Última actualización: 12 de abril de 2017
{: .last-updated}

Para configurar el servicio {{site.data.keyword.mobilepushshort}}, obtenga las credenciales necesarias del proveedor de notificaciones push, que puede ser Firebase Cloud Messaging (FCM) o el servicio de notificaciones Push de Apple (APNs) para dispositivos móviles.  

Puede configurar {{site.data.keyword.mobilepushshort}} mediante el panel de control de **IBM Bluemix Services** o mediante las [API REST ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://mobile.{DomainName}/imfpush/){: new_window}.


## Configuración de credenciales para FCM
{: #create-push-enable-gcm}

Firebase Cloud Messaging (FCM) es la pasarela utilizada para entregar notificaciones push a dispositivos Android y Google Chrome. FCM es la nueva versión de Google Cloud Messaging (GCM). Para configurar el servicio {{site.data.keyword.mobilepushshort}} en el panel de control, debe obtener credenciales de FCM. Asegúrese de que utiliza las configuraciones de FCM para nuevas apps. Las apps existentes seguirán funcionando con las configuraciones de GCM.

### Cómo obtener el ID de remitente y la clave de la API
{: #android-senderid-apikey}

La clave de la API se almacena de forma segura y la utiliza el servicio {{site.data.keyword.mobilepushshort}} para conectarse al servidor de FCM y el ID de remitente (número de proyecto) lo utilizará el SDK de Android y el SDK de JS para Google Chrome y Mozilla Firefox en el lado de cliente. 

Para configurar el FCM, genere la clave de API y el ID de remitente y siga estos pasos:

1. Visite la [Consola de Firebase ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://console.firebase.google.com/?pli=1){: new_window}.
2. Seleccione **Crear nuevo proyecto**. 
3. En la ventana Crear un proyecto, proporcione un nombre de proyecto, elija un país/región y pulse **Crear proyecto**.
3. En el panel de navegación, pulse el icono Valores y seleccione **Valores del proyecto**.
4. Seleccione el separador Cloud Messaging para generar una Clave de API de servidor y un ID de remitente.

### Configuración del servicio de notificacions push para Android y las apps y extensiones de Chrome
{: #setup-push-android}

**Nota:** Necesitará la Clave de la API de FCM/GCM y el ID del remitente (número de proyecto).

1. Abra el panel de control de Bluemix y pulse la instancia del servicio {{site.data.keyword.mobilepushfull}} que ha creado para abrir su panel de control. Se mostrará el panel de control de Push. Para configurar un servicio {{site.data.keyword.mobilepushshort}} desenlazado para Android, seleccione el icono de Servicio {{site.data.keyword.mobilepushshort}} desenlazado para abrir el panel de control del servicio {{site.data.keyword.mobilepushshort}}. 

![Panel de control de Push](images/push_unbound.jpg)

2. Pulse el botón **Configurar Push** para configurar las credenciales de FCM/GCM para aplicaciones de Android y apps y extensiones de Google Chrome.
3. En la página **Configuración**, para Android, vaya al separador **Mobile** y configure el ID del remitente (número de proyecto de GCM) y la Clave de la API. Para las apps y extensiones de Google Chrome, vaya al separador **Web** y configure el ID del remitente (número de proyecto de FCM/GCM) y la Clave de la API adecuadamente.
4. Pulse **Guardar**.
5. Pasos siguientes. [Habilitación de notificaciones para Android](c_enable_push.html) o [Habilitación de notificaciones para apps y extensiones de Google Chrome](c_web_extensions.html).


## Configuración de credenciales para APNs
{: #create-push-credentials-apns}

El servicio de notificaciones push de Apple (APNs) permite a los desarrolladores de aplicaciones enviar
notificaciones remotas desde la instancia del servicio {{site.data.keyword.mobilepushshort}} en Bluemix (el proveedor) en dispositivos y aplicaciones de iOS. Los mensajes se envían a una aplicación de destino del dispositivo. 

Obtenga y configure las credenciales de APNs. Los certificados de APNs se gestionan de forma segura mediante el servicio {{site.data.keyword.mobilepushshort}} y se utilizan para conectarse al servidor APNs como proveedor.

<!-- 1. Obtain an [Apple Developers ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.apple.com/){: new_window} account.-->

<!--2. [Register an App ID](#create-push-credentials-apns-register)
3. [Create a development and distribution APNs SSL certificate](#create-push-credentials-apns-ssl)
4. [Create a development provisioning profile](#create-push-credentials-dev-profile)
5. [Create a store distribution provisioning profile](#create-push-credentials-apns-distribute_profile)
6. [Creating .p12 push certificate file for Bluemix push](#create-p12-push-certificate-file-for-Bluemix-push)
7. [Set up APNs on the Push Dashboard](#create-push-credentials-apns-dashboard)
-->


### Registrar un ID de App
{: #create-push-credentials-apns-register}


El ID de app (el identificador de paquete) es un identificador exclusivo que identifica una aplicación específica. Cada aplicación requiere un ID de app. Los servicios como {{site.data.keyword.mobilepushshort}} se configuran en el ID de la app.

1. Asegúrese de tener una cuenta de [desarrolladores de Apple ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://developer.apple.com/){: new_window}.
2. Vaya al portal de [desarrolladores de Apple ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://developer.apple.com){: new_window}, pulse **Centro de miembros** y seleccione **Certificados, identificadores y perfiles**.
3. Vaya a la sección **Registro de ID de app** de la [Biblioteca de desarrolladores de Apple ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html#//apple_ref/doc/uid/TP40012582-CH30-SW991){: new_window} y siga las instrucciones para registrar el ID de la app.

Al registrar un ID de App, seleccione las opciones siguientes:

* Notificaciones push
![Servicios de apps](images/appID_appservices_enablepush.jpg)
* Sufijo de ID explícito
![ID explícito](images/appID_bundleID.jpg)
4. Crear un certificado SSL de APNs de desarrollo y distribución.

### Crear un certificado SSL de APNs de desarrollo y distribución
{: #create-push-credentials-apns-ssl}

Para poder obtener un certificado de APNs, debe generar en primer lugar una solicitud de firma de certificado (CSR) y enviarla a Apple, la entidad emisora de certificados (CA). La CSR contiene información que identifica a la empresa y a la clave pública y privada que utilice para firmar las notificaciones push de Apple. A continuación, genere el certificado SSL en el Portal de desarrollador de iOS. El certificado, junto con su clave pública y privada, se almacena en el Acceso de cadena de claves.

<!-- ###Before you begin -->
<!-- {: before-you-begin-certificate} -->

<!--[Register an App ID](#create-push-credentials-apns-register)-->

Puede utilizar APNs de dos maneras: 

* La modalidad de pruebas durante el desarrollo y la prueba.
* La modalidad de producción al distribuir aplicaciones mediante App Store (u otros mecanismos de distribución de empresa).

Debe obtener certificados independientes para los entornos de desarrollo y de distribución. Los certificados están asociados con un ID de App para la app que es el destinatario de las notificaciones remotas. Para la producción, puede crear un máximo de dos certificados. Bluemix utiliza los certificados para establecer una conexión SSL con APNs.

<!-- Create a development and distribution SSL certificate. -->

1. Vaya al sitio web de [desarrolladores de Apple ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://developer.apple.com){: new_window}, pulse **Centro de miembros** y seleccione **Certificados, identificadores y perfiles**.
2. En el área **Identificadores**, pulse **ID de app**.
3. Desde la lista de ID de App, seleccione el ID de App <!--newly created--> y, a continuación, seleccione **Configuración**.
4. En el área **Notificaciones Push**, cree un certificado SSL de desarrollo y, a continuación, un certificado SSL de producción.

	![Certificados SSL de notificación Push](images/certificate_createssl.jpg)

5. Cuando se muestre la pantalla **Acerca de la creación de una solicitud de firma de certificado (CSR)**, inicie la aplicación **Acceso de cadena de claves** en el Mac para crear una Solicitud de firma de certificado (CSR).
6. En el menú, seleccione **Acceso de cadena de claves > Asistente de certificado > Solicitud de un certificado a partir de una entidad emisora de certificados…** 
7. En **Información del certificado**, especifique la dirección de correo electrónico asociada con la cuenta de Desarrollador de apps y un nombre común. Otorgue un nombre significativo que le ayude a identificar si es un certificado para desarrollo (pruebas) o distribución (producción); por ejemplo, *sandbox-apns-certificate* o *production-apns-certificate*.
8. Seleccione **Guardado en disco** para descargar el archivo `.certSigningRequest` en su escritorio y, a continuación, pulse **Continuar**.
9. En la opción de menú **Guardar como**, asigne `.certSigningRequest` al archivo y pulse **Guardar**.
10. Pulse **Hecho**. Ahora tiene un CSR.
11. Vuelva a la ventana **Acerca de la creación de una solicitud de firma de certificado (CSR)** y haga clic en **Continuar**. 
12. Desde la pantalla **Generar**, pulse **Elegir archivo...** y seleccione el archivo CSR que ha guardado en el escritorio. Luego, pulse **Generar**.
	![Generar certificado](images/generate_certificate.jpg)
13. Cuando el certificado esté listo, pulse **Hecho**.
14. En la pantalla **Notificaciones Push**, pulse **Descargar** para descargar el certificado y, a continuación, pulse **Hecho**. 
	![Descargar certificado](images/certificate_download.jpg)
15. En el Mac, vaya a **Acceso de cadena de claves > Mis certificados**, y ubique el certificado recién instalado. Efectúe una doble pulsación en el certificado para instalarlo en el Acceso de cadena de claves.
16. Seleccione el certificado y la clave privada y, a continuación, seleccione **Exportar** para convertir el certificado en el formato de intercambio de información personal (formato `.p12`).
	![Exportar certificado y claves](images/keychain_export_key.jpg)
17. En el campo **Guardar como**, escriba un nombre significativo para el certificado. Por ejemplo, `sandbox_apns.p12_certifcate` o `production_apns.p12`; luego pulse **Guardar**.
	![Exportar certificado y claves](images/certificate_p12v2.jpg)
18. En el campo **Escriba una contraseña**, especifique una contraseña para proteger los elementos exportados y, a continuación, pulse **Aceptar**. Puede utilizar esta contraseña para configurar los valores de APNs en el panel de control de Push.{: #step18}
	![Exportar certificado y claves](images/export_p12.jpg)
19. **Key Access.app** le solicita que exporte su clave desde la pantalla **Cadena de claves**. Especifique la contraseña de administración para Mac para permitir al sistema exportar estos elementos y, a continuación, seleccione la opción **Permitir siempre**. Se generará un certificado `.p12` en el escritorio.


### Creación de un perfil de suministro de desarrollo
{: #create-push-credentials-dev-profile}

El perfil de suministro funciona con el ID de App para determinar qué dispositivos pueden instalar y ejecutar la app y a qué servicios puede acceder la app. Para cada ID de App, cree dos perfiles de suministro: uno para desarrollo y otro para distribución. Xcode utiliza el perfil de suministro de desarrollo para determinar qué desarrolladores están permitidos para crear la aplicación y qué dispositivos están permitidos para probarse en la aplicación.

Asegúrese de que ha registrado un ID de App, de que lo ha habilitado para el servicio de {{site.data.keyword.mobilepushshort}} y de que lo ha configurado para utilizar un certificado SSL de APNs de desarrollo y producción.

Cree un perfil de suministro de desarrollo, como se indica a continuación:

1. Vaya al portal de [desarrolladores de Apple ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://developer.apple.com){: new_window}, pulse **Centro de miembros** y seleccione **Certificados, identificadores y perfiles**.
2. Vaya a la [Biblioteca de desarrolladores de Mac ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html#//apple_ref/doc/uid/TP40012582-CH30-SW62site){: new_window}, desplácese hasta la sección **Creación de perfiles de suministro de desarrollo** y siga las instrucciones para crear un perfil de desarrollo.
**Nota**: Al configurar un perfil de suministro de desarrollo, seleccione las opciones siguientes:
	* **Desarrollo de apps de iOS**
	* **Para apps iOS y watchOS**


### Creación de un perfil de suministro de distribución del almacén
{: #create-push-credentials-apns-distribute_profile}

Utilice el perfil de suministro del almacén para enviar la app para su distribución a la App Store.

1. Vaya al portal de [desarrolladores de Apple ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://developer.apple.com){: new_window}, pulse **Centro de miembros** y seleccione **Certificados, identificadores y perfiles**.
2. Efectúe una doble pulsación en el perfil de suministro descargado para instalarlo en Xcode.

### Configuración de APNs en el Panel de control de notificaciones Push
{: #create-push-credentials-apns-dashboard}

Para utilizar el servicio {{site.data.keyword.mobilepushshort}} para enviar notificaciones, cargue los certificados SSL necesarios para el servicio de Notificaciones Push de Apple (APNs). También se puede utilizar la API REST para subir un certificado de APNs.

<!-- Get your development and production APNs SSL certificate and the password associated with each type of certificate. For information, see Creating and configuring push credentials for APNs.-->

Los certificados necesarios para APNs son los certificados `.p12`. Estos certificados contienen la clave privada y certificados SSL que son necesarios para crear y publicar la aplicación. Debe generar los certificados desde el Centro de miembros del sitio web Desarrollador de Apple (es necesaria una cuenta válida de desarrollador de Apple). Los certificados independientes son necesarios para el entorno de desarrollo (pruebas) y el entorno de producción (distribución).

**Nota**: Después de que el archivo `.cer` se encuentre en el acceso de cadena de claves, expórtelo al sistema para crear un certificado `.p12`.

Para obtener más información sobre cómo utilizar APNs, consulte en la [Biblioteca de desarrolladores de iOS la guía de programación de notificaciones push y locales ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ProvisioningDevelopment.html#//apple_ref/doc/uid/TP40008194-CH104-SW4){: new_window}.

Para configurar APNs en el panel de control de servicios de notificación push, siga estos pasos:

1. Seleccione **Configurar** en el panel de control de servicios de notificación push.
2. Elija la opción **Móvil** para actualizar la información del formulario **Credenciales push de APNs**.
3. Seleccione **Recinto de seguridad** (desarrollo) o **Producción** (distribución) según convenga y cargue los certificados `p.12` que ha creado en el [paso](#step18) anterior.
  ![Panel de control Establecer notificaciones push](images/wizard.jpg)
3. En el campo **Contraseña**, especifique la contraseña asociada con el archivo de certificado `.p12` y, a continuación, pulse **Guardar**.

Después de subir los certificados satisfactoriamente con una contraseña válida, inicie el envío de notificaciones.

## Configuración de credenciales para navegadores web
{: #configure-credential-for-browsers}

El servicio IBM {{site.data.keyword.mobilepushshort}} amplía sus funciones para enviar notificaciones al navegador. 

El servicio {{site.data.keyword.mobilepushshort}} necesita el URL del sitio web o el nombre del dominio del sitio web para identificar las solicitudes que se deben permitir. Una instancia de servicio de {{site.data.keyword.mobilepushshort}} solo admite un nombre de dominio. Por lo tanto, asegúrese de que se haya establecido el mismo valor para Chrome, Firefox y Safari. 

Los navegadores Chrome y Safari necesitan configuración adicional para push we,. Necesitaría una clave de API de FCM, ya que se utiliza un punto final FCM para distribuir mensajes en Chrome. 


### Configuración para push web de Chrome y Firefox 
{: #config-chrome-firefox}

1. En el panel de control de Push, seleccione **Configurar**.
2. Seleccione el separador Web.
	![Configuraciones de push web](images/webpush_configure.jpg)
3. Configure la clave de la API de FCM/GCM y el URL del sitio web que se registrará para la recepción de notificaciones por push.
4. Pulse **Guardar**.
5. Pasos siguientes. [Habilitación de notificaciones para navegadores Google Chrome y Mozilla Firefox](c_chrome_firefox_enable.html).


### Configuración de push web de Safari 
{: #configure-safari}

La versión admitida para el servicio de {{site.data.keyword.mobilepushshort}} en Safari es 10.0. Debe generar un certificado a través de su cuenta de Apple Developer para poder configurar el navegador para que reciba notificaciones.

#### Generación de un certificado
{: #certificate-generation}

Asegúrese de disponer de una cuenta de desarrollador de Apple. Tiene que registrar un Push ID del sitio web y generar un certificado para configurar Safari para que reciba notificaciones. Comience siguiendo estos pasos.

1. En el centro Apple Developer Member, pulse **Certificados, ID y Perfiles**. 
2. Pulse **Identificadores** y luego **ID Push del sitio web**.
3. Elija crear una nueva entrada seleccionando el icono del signo más.
  ![Panel de control de Push](images/safari_1.jpg)

4. En el panel Registrar ID Push del sitio web, especifique una descripción adecuada del ID Push del sitio web y un ID identificador. Se recomienda que esté en formato de nombre de dominio invertido, comenzando por `web`. Por ejemplo: `web.com.example.dailyweatherreports`.
5. Registre el ID Push del sitio web. Ahora tiene el ID Push del sitio web 
6. Seleccione **Editar** para crear un certificado que se utilizará para el ID Push del sitio web.
7. En la ventana Asistente de certificados para la información sobre certificados, especifique su ID de correo electrónico y un nombre común. Deje en blanco la dirección de correo electrónico de la entidad emisora de certificados.
8. Pulse **Guardar en disco** y seleccione **Continuar**.
9. Guarde el certificado en una carpeta adecuada.
10. Seleccione el `.certSigningRequest` creado en el disco cuando se le solicite en el asistente para generar el certificado. Asegúrese de que descarga el certificado push del sitio web creado en el formato `.cer`.
11. Abra el Certificado en la herramienta KeyChain Access. Pulse con el botón derecho del ratón y exporte como certificado p12. Anote la contraseña que se facilita durante la generación del certificado p12.


#### Configuración para notificaciones
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
