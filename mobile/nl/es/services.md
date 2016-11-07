---

copyright:
  years: 2016
lastupdated: "2016-10-18"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock: .codeblock}

# Servicios
{: #services}

Última actualización: 18 de octubre de 2016
{: .last-updated}

Desde la vista **Servicios** del panel de control de {{site.data.keyword.Bluemix}} Mobile, puede ver los servicios existentes o crear nuevos servicios. El panel de control de Mobile proporciona una única ubicación para ver todos los servicios de Bluemix gestionados por proyectos.  

Si suprime servicios desde la vista **Servicios**, desconectará el servicio del proyecto con el que está asociado. Cree una nueva instancia de servicio si desea volver a conectar el servicio al proyecto.

## Visión general de los servicios de {{site.data.keyword.Bluemix_notm}} Mobile
{: #mobile_services_overview}

En la tabla siguiente se describen los servicios de {{site.data.keyword.Bluemix_notm}} Mobile. Puede utilizar los servicios individuales desde el catálogo de {{site.data.keyword.Bluemix_notm}}, o puede integrarlos en el proyecto móvil.

<table summary="Esta tabla describe los servicios de {{site.data.keyword.Bluemix_notm}} Mobile y proporciona enlaces a la documentación del servicio">
<caption>Tabla 1. Servicios de {{site.data.keyword.Bluemix_notm}} Mobile</caption>
<th>Servicio de {{site.data.keyword.Bluemix_notm}} Mobile</th>
<th>Descripción</th>
<tr>
<td> <img src="images/mobile_analytics_icon.png" alt="Icono de {{site.data.keyword.mobileanalytics_short}}"><br/>{{site.data.keyword.mobileanalytics_short}} (Beta)</td>
<td valign="top">Utilice el servicio de {{site.data.keyword.mobileanalytics_full}} para ver cómo están funcionando las aplicaciones móviles y cómo se están utilizando.<br/><br/>
Consulte más información sobre el funcionamiento de este servicio en la documentación de <a href="../services/mobileanalytics/index.html" alt="Enlace de documentación de {{site.data.keyword.mobileanalytics_short}}">{{site.data.keyword.mobileanalytics_short}}</a>.
</td>
</tr>
<tr>
<td><img src="images/authentication_icon
.png" alt="Icono de servicio de {{site.data.keyword.amashort}}"><br/>{{site.data.keyword.amashort}}</td>
<td valign="top">Utilice el servicio de {{site.data.keyword.amafull}} para añadir funcionalidad de seguridad a la aplicación móvil. Puede configurar la autenticación del cliente y los proveedores de identidad para que los usuarios puedan iniciar sesión en la app con sus cuentas existentes de Google o Facebook.<br/><br/>
Obtenga más información sobre el funcionamiento de este servicio en la documentación de <a href="../services/mobileaccess/index.html" alt="Enlace de documentación de {{site.data.keyword.amashort}}">{{site.data.keyword.amashort}}</a>.</td>
</tr>
<tr>
<td><img src="images/MFPFoundation_icon.png" alt="icono del servicio {{site.data.keyword.mobilefoundation_short}}"><br/> {{site.data.keyword.mobilefoundation_short}}</td>
<td valign="top">Utilice el servicio de {{site.data.keyword.mobilefoundation_long}} para configurar de forma rápida un entorno de {{site.data.keyword.mfp_full}} desde el que puede desarrollar, probar y hacer funcionar las aplicaciones móviles empresariales.<br/><br/>
Consulte más información sobre el funcionamiento de este servicio en la documentación de <a href="../services/mobilefoundation/index.html" alt="Enlace de documentación de {{site.data.keyword.mobilefoundation_short}}">{{site.data.keyword.mobilefoundation_short}}</a>.</td>
</tr>
<tr>
<td><img src="images/mqa_icon.png" alt="icono de servicio {{site.data.keyword.mqa}}"><br/>{{site.data.keyword.mqa}}</td>
<td valign="top">Utilice el servicio de {{site.data.keyword.mqafull}} para descubrir y configurar servicios móviles de calidad para las apps. Puede ver medidas de calidad de alto nivel para sus apps para móvil a fin de obtener una visión general de los problemas de las apps con las que trabaja. Estas medidas incluyen información sobre bloqueos, errores, comentarios de usuarios y opinión general de los usuarios. Al visualizar esta información para las apps, puede determinar si desea investigar en mayor profundidad problemas específicos.<br/><br/>
Consulte más información sobre el funcionamiento de este servicio en la documentación de <a href="../services/MobileQualityAssurance/index.html" alt="Enlace de documentación de {{site.data.keyword.mqa}}">{{site.data.keyword.mqa}}</a>.</td>
</tr>
<tr>
<td><img src="images/push_icon.png" alt="Icono de servicio de Notificaciones push"><br/>{{site.data.keyword.mobilepushshort}}</td>
<td valign="top">Utilice el servicio de {{site.data.keyword.mobilepushfull}} para enviar y gestione notificaciones push móviles que estén pensadas para las plataformas iOS y Android. Este servicio gestiona la correlación de los usuarios de aplicaciones en sus dispositivos, plataforma de dispositivos, y maneja la asignación de notificaciones push en los dispositivos. Con este servicio, puede enviar difusiones, unicasts (en función del userID, deviceID), y etiquetas (o temas) basados en notificaciones push a sus usuarios de aplicación móvil.<br/><br/>
Consulte más información sobre el funcionamiento de este servicio en la documentación de <a href="../services/mobilepush/index.html" alt="Enlace de documentación de {{site.data.keyword.mobilepushshort}}">{{site.data.keyword.mobilepushshort}}</a>.</td>
</table>

## Integración de servicios móviles
{: #services_integration}
Puede integrar los servicios existentes de {{site.data.keyword.Bluemix_notm}} Mobile, como por ejemplo {{site.data.keyword.cloudant}}, en el proyecto.


#### Integración de {{site.data.keyword.cloudant}}
{: #cloudant_integration}

Para integrar el servicio existente de {{site.data.keyword.cloudant}}, siga estos pasos:

1. Pulse la instancia de servicio de {{site.data.keyword.cloudant}}.
2. Pulse **INICIAR**.
3. En la vista **Bases de datos**, pulse el nombre de la Base de datos.
4. Pulse **API** y copie el valor **Clave de API** en el nombre de la base de datos.

   **Nota**: No copie el contenido en el nombre de la base de datos.

5. Pulse **Permisos** > **Generar clave de API** y copie los valores **Clave** y **Contraseña**.
6. Vuelva a la vista **Proyectos** del panel de control de Mobile.
7. Pulse en el proyecto para editarlo.
8. Pulse **Datos** > **+ Origen de datos** > **Cloudant** y proporcione el nombre de origen de los datos y pulse **Añadir**.
9. Pulse **Configuración de Cloudant**.
10. Proporcione el valor **Clave de API** que ha copiado anteriormente en el **URL de API**.
11. Proporcione el valor **Clave** que ha copiado anteriormente en **Usuario**.
12. Proporcione el valor **Contraseña** que ha copiado anteriormente en **Contraseña**.
13. Pulse **Aceptar**.
