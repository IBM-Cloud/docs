---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-11"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock: .codeblock}

# Servicios
{: #services}

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
<td> <img src="images/mobile_analytics_icon.png" alt="Icono de {{site.data.keyword.mobileanalytics_short}}"><br/>{{site.data.keyword.mobileanalytics_short}}</td>
<td valign="top">Utilice el servicio {{site.data.keyword.mobileanalytics_full}} para ver información sobre el funcionamiento de las apps para móvil y cómo sel utilizan.<br/><br/>
Encontrará más información sobre el funcionamiento de este servicio en la <a href="/docs/services/mobileanalytics/index.html" alt="enlace a la documentación de {{site.data.keyword.mobileanalytics_short}}">documentación de {{site.data.keyword.mobileanalytics_short}}</a>.
</td>
</tr>
<tr>
<td><img src="images/authentication_icon
.png" alt="Icono del servicio {{site.data.keyword.amashort}}"><br/>{{site.data.keyword.amashort}}</td>
<td valign="top">Utilice el servicio {{site.data.keyword.amafull}} para incorporar funciones de seguridad a la app para móvil. Puede configurar la autenticación de clientes y proveedores de identidad para que los usuarios puedan iniciar una sesión en la app con sus cuentas existentes de Google o Facebook.<br/><br/>
Encontrará más información sobre el funcionamiento de este servicio en la <a href="/docs/services/mobileaccess/index.html" alt="enlace a la documentación de {{site.data.keyword.amashort}}">documentación de {{site.data.keyword.amashort}}</a>.</td>
</tr>
<tr>
<td><img src="images/MFPFoundation_icon.png" alt="Icono del servicio {{site.data.keyword.mobilefoundation_short}}"><br/> {{site.data.keyword.mobilefoundation_short}}</td>
<td valign="top">Utilice el servicio {{site.data.keyword.mobilefoundation_long}} para configurar de forma rápida un entorno de {{site.data.keyword.mfp_full}} en el que puede desarrollar, probar y trabajar con apps para móvil de la empresa.<br/><br/> Encontrará más información sobre el funcionamiento de este servicio en la <a href="/docs/services/mobilefoundation/index.html" alt="enlace a la documentación de {{site.data.keyword.mobilefoundation_short}}">documentación de {{site.data.keyword.mobilefoundation_short}}</a>.</td>
</tr>
<tr>
<td><img src="images/mqa_icon.png" alt="Icono del servicio {{site.data.keyword.mqa}}"><br/>{{site.data.keyword.mqa}}</td>
<td valign="top">Utilice el servicio {{site.data.keyword.mqafull}} para descubrir y configurar servicios móviles de calidad para las apps. Puede ver medidas de calidad de alto nivel para sus apps para móvil a fin de obtener una visión general de los problemas de las apps con las que trabaja. Estas medidas incluyen información sobre bloqueos, errores, comentarios de usuarios y opinión general de los usuarios. Consultando esta información sobre sus apps, puede determinar si debe investigar más a fondo determinados problemas.<br/><br/>
Encontrará más información sobre el funcionamiento de este servicio en la <a href="/docs/services/MobileQualityAssurance/index.html" alt="enlace a la documentación de {{site.data.keyword.mqa}}">documentación de {{site.data.keyword.mqa}}</a>.</td>
</tr>
<tr>
<td><img src="images/push_icon.png" alt="Icono del servicio {{site.data.keyword.mobilepushshort}}"><br/>{{site.data.keyword.mobilepushshort}}</td>
<td valign="top">El servicio {{site.data.keyword.mobilepushfull}} proporciona una plataforma unificada para enviar y gestionar notificaciones push móviles y de web que están pensadas para varias plataformas.
<br/><br/>
El servicio {{site.data.keyword.mobilepushshort}} gestiona la correlación de los usuarios de aplicaciones con sus dispositivos, plataforma de dispositivos y navegadores y maneja la asignación a los mismos de notificaciones push. Puede enviar difusiones, difusiones únicas (en función del ID de dispositivo y del ID de usuario) y etiquetas (o temas) como notificaciones push a sus usuarios de aplicaciones móviles y de navegador web. También puede utilizar las API SDK y REST para desarrollar aplicaciones de cliente.
<br/><br/>
Encontrará más información sobre el funcionamiento de este servicio en la <a href="/docs/services/mobilepush/index.html" alt="enlace a la documentación de {{site.data.keyword.mobilepushshort}}">documentación de {{site.data.keyword.mobilepushshort}}</a>.</td>
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
