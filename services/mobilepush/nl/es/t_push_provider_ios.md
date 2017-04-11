---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configuración de credenciales para APNs
{: #create-push-credentials-apns}
Última actualización: 16 de enero de 2017
{: .last-updated}

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


##Registrar un ID de App
{: #create-push-credentials-apns-register}


El ID de app (el identificador de paquete) es un identificador exclusivo que identifica una aplicación específica. Cada aplicación requiere un ID de app. Los servicios como {{site.data.keyword.mobilepushshort}} se configuran en el ID de la app.

1. Asegúrese de tener una cuenta de [desarrolladores de Apple ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://developer.apple.com/){: new_window}.
2. Vaya al portal de [desarrolladores de Apple ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://developer.apple.com){: new_window}, pulse **Centro de miembros** y seleccione **Certificados, identificadores y perfiles**.
3. Vaya a la sección **Registro de ID de app** de la [Biblioteca de desarrolladores de Apple ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html#//apple_ref/doc/uid/TP40012582-CH30-SW991){: new_window} y siga las instrucciones para registrar el ID de la app.

Al registrar un ID de App, seleccione las opciones siguientes:

* Notificaciones push
![Servicios de aplicaciones](images/appID_appservices_enablepush.jpg)
* Sufijo de ID explícito
![ID explícito](images/appID_bundleID.jpg)
4. Crear un certificado SSL de APNs de desarrollo y distribución.

##Crear un certificado SSL de APNs de desarrollo y distribución
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


##Creación de un perfil de suministro de desarrollo
{: #create-push-credentials-dev-profile}

El perfil de suministro funciona con el ID de App para determinar qué dispositivos pueden instalar y ejecutar la app y a qué servicios puede acceder la app. Para cada ID de App, cree dos perfiles de suministro: uno para desarrollo y otro para distribución. Xcode utiliza el perfil de suministro de desarrollo para determinar qué desarrolladores están permitidos para crear la aplicación y qué dispositivos están permitidos para probarse en la aplicación.

Asegúrese de que ha registrado un ID de App, de que lo ha habilitado para el servicio de {{site.data.keyword.mobilepushshort}} y de que lo ha configurado para utilizar un certificado SSL de APNs de desarrollo y producción.

Cree un perfil de suministro de desarrollo, como se indica a continuación:

1. Vaya al portal de [desarrolladores de Apple ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://developer.apple.com){: new_window}, pulse **Centro de miembros** y seleccione **Certificados, identificadores y perfiles**.
2. Vaya a la [Biblioteca de desarrolladores de Mac ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html#//apple_ref/doc/uid/TP40012582-CH30-SW62site){: new_window}, desplácese hasta la sección **Creación de perfiles de suministro de desarrollo** y siga las instrucciones para crear un perfil de desarrollo.
**Nota**: Al configurar un perfil de suministro de desarrollo, seleccione las opciones siguientes:
	* **Desarrollo de apps de iOS**
	* **Para aplicaciones iOS y watchOS**



##Creación de un perfil de suministro de distribución del almacén
{: #create-push-credentials-apns-distribute_profile}

Utilice el perfil de suministro del almacén para enviar la app para su distribución a la App Store.

1. Vaya al portal de [desarrolladores de Apple ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://developer.apple.com){: new_window}, pulse **Centro de miembros** y seleccione **Certificados, identificadores y perfiles**.
2. Efectúe una doble pulsación en el perfil de suministro descargado para instalarlo en Xcode.

##Configuración de APNs en el panel de control de {{site.data.keyword.mobilepushshort}}
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
