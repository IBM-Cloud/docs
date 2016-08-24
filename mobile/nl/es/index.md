---

copyright:
  years: 2016

---
{:new_window: target="_blank"}

# Creación de proyectos móviles desde el panel de control de Mobile
{: #mobile}
*Última actualización: 18 de julio de 2016*
{: .last-updated}

Con los servicios de {{site.data.keyword.Bluemix}} Mobile, puede incorporar servicios de nube integrados, gestionados y escalables a las aplicaciones móviles sin intervención de TI. Céntrese en crear sus apps para móvil en lugar de en solucionar la complejidad de gestionar la infraestructura de fondo.

El panel de control de Mobile proporciona una experiencia integrada en {{site.data.keyword.Bluemix_notm}}. Puede crear nuevos proyectos móviles de forma sencilla desde dentro del panel de control. Con la vista **Proyectos**, puede gestionar todos los proyectos en un lugar. La vista **Servicios** muestra las instancias del servicio móvil existentes.

Para ver el panel de control de Mobile, pulse la categoría **Mobile** desde el inicio de {{site.data.keyword.Bluemix_notm}}.
<img src="images/mobile_dashboard.jpg" alt="Inicio de {{site.data.keyword.Bluemix_notm}}">

Para comenzar, pulse **Proyecto nuevo** desde la vista **Proyectos** del panel de control de Mobile.

## Visión general de los servicios de {{site.data.keyword.Bluemix_notm}} Mobile
{: #mobile_services_overview}

En la tabla siguiente se describen los servicios de {{site.data.keyword.Bluemix_notm}} Mobile disponibles. Puede utilizar los servicios individuales desde el catálogo de {{site.data.keyword.Bluemix_notm}}, o puede integrarlos en el proyecto móvil.

<table summary="Esta tabla describe los servicios de {{site.data.keyword.Bluemix_notm}} Mobile y proporciona enlaces a la documentación del servicio">
<caption>Tabla 1. Servicios de {{site.data.keyword.Bluemix_notm}} Mobile</caption>
<th>Servicio de {{site.data.keyword.Bluemix_notm}} Mobile</th>
<th>Descripción</th>
<tr>
<td> <img src="images/mobile_analytics_icon.png" alt="Icono de {{site.data.keyword.mobileanalytics_short}}"><br/><b>{{site.data.keyword.mobileanalytics_short}} (Experimental)</b></td>
<td valign="top">Utilice el servicio de {{site.data.keyword.mobileanalytics_full}} para medir el estado, el comportamiento y el contexto de las aplicaciones móviles, de los usuarios móviles y de los dispositivos móviles.<br/><br/>
Consulte más información sobre el funcionamiento de este servicio en la documentación de <a href="../services/mobileanalytics/index.html" alt="Enlace de documentación de {{site.data.keyword.mobileanalytics_short}}">{{site.data.keyword.mobileanalytics_short}}</a>.
</td>
</tr>
<tr>
<td><img src="images/catalog_icons-05.png" alt="Icono de servicio de {{site.data.keyword.amashort}}"><br/><b>{{site.data.keyword.amashort}}</b></td>
<td valign="top">Utilice el servicio de {{site.data.keyword.amafull}} para añadir funcionalidad de seguridad a la aplicación móvil. Puede configurar la autenticación del cliente y los proveedores de identidad para que los usuarios puedan iniciar sesión en la app con sus cuentas existentes de Google o Facebook.<br/><br/>
Obtenga más información sobre el funcionamiento de este servicio en la documentación de <a href="../services/mobileaccess/index.html" alt="Enlace de documentación de {{site.data.keyword.amashort}}">{{site.data.keyword.amashort}}</a>.</td>
</tr>
<tr>
<td><img src="images/MFPFoundation_icon.png" alt="Icono de servicio de {{site.data.keyword.mobilefoundation_short}}"><br/> <b>{{site.data.keyword.mobilefoundation_short}}</b></td>
<td valign="top">Utilice el servicio de {{site.data.keyword.mobilefoundation_long}} para configurar de forma rápida un entorno de {{site.data.keyword.mfp_full}} desde el que puede desarrollar, probar y hacer funcionar las aplicaciones móviles empresariales.<br/><br/>
Consulte más información sobre el funcionamiento de este servicio en la documentación de <a href="../services/mobilefoundation/index.html" alt="Enlace de documentación de {{site.data.keyword.mobilefoundation_short}}">{{site.data.keyword.mobilefoundation_short}}</a>.</td>
</tr>
<tr>
<td><img src="images/mqa_icon.png" alt="Icono de servicio de {{site.data.keyword.mqa}}"><br/><b>{{site.data.keyword.mqa}}</b></td>
<td valign="top">Utilice el servicio de {{site.data.keyword.mqafull}} para descubrir y configurar servicios móviles de calidad para las apps. Puede ver medidas de calidad de alto nivel para sus apps para móvil a fin de obtener una visión general de los problemas de las apps con las que trabaja. Estas medidas incluyen información sobre bloqueos, errores, comentarios de usuarios y opinión general de los usuarios. Al visualizar esta información para las apps, puede determinar si desea investigar en mayor profundidad problemas específicos.<br/><br/>
Consulte más información sobre el funcionamiento de este servicio en la documentación de <a href="../services/MobileQualityAssurance/index.html" alt="Enlace de documentación de {{site.data.keyword.mqa}}">{{site.data.keyword.mqa}}</a>.</td>
</tr>
<tr>
<td><img src="images/catalog_icons-09.png" alt="Icono de servicio de Notificaciones push"><br/><b>{{site.data.keyword.mobilepushshort}}</b></td>
<td valign="top">Utilice el servicio de {{site.data.keyword.mobilepushfull}} para enviar y gestione notificaciones push móviles que estén pensadas para las plataformas iOS y Android. Este servicio gestiona la correlación de los usuarios de aplicaciones en sus dispositivos, plataforma de dispositivos, y maneja la asignación de notificaciones push en los dispositivos. Con este servicio, puede enviar difusiones, unicasts (en función del userID, deviceID), y etiquetas (o temas) basados en notificaciones push a sus usuarios de aplicación móvil.<br/><br/>
Consulte más información sobre el funcionamiento de este servicio en la documentación de <a href="../services/mobilepush/index.html" alt="Enlace de documentación de {{site.data.keyword.mobilepushshort}}">{{site.data.keyword.mobilepushshort}}</a>.</td>
</table>

## Integración de servicios móviles
{: #services_integration}
Puede integrar los servicios existentes de {{site.data.keyword.Bluemix_notm}} Mobile, como por ejemplo {{site.data.keyword.mobilepushshort}} y {{site.data.keyword.cloudant}}, en el proyecto.

#### Integración de {{site.data.keyword.mobilepushshort}}
{: #push_integration}

Para integrar el servicio existente de {{site.data.keyword.mobilepushshort}}, siga estos pasos:

1. Pulse la instancia de servicio de {{site.data.keyword.mobilepushshort}}.
2. Pulse **Opciones móviles** y copie los valores **Ruta** y **AppGuid**.

   **Nota**: El servicio de {{site.data.keyword.mobilepushshort}} debe estar enlazado a una app para ver **Opciones móviles**.

3. Vuelva a la vista **Proyectos** del panel de control de Mobile.
4. Pulse en el proyecto para editarlo.
5. Pulse **Enviar por push** y habilite las notificaciones.
6. Proporcione el valor **AppGuid** que ha copiado anteriormente en el **ID de app**.
7. Proporcione el valor **Ruta** que ha copiado anteriormente en el **URL de ruta de app**.

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


# Enlaces relacionados
{: #rellinks}

<!-- links to internal services don't work
## {{site.data.keyword.Bluemix_notm}} Mobile services
{: #general}
* [Mobile Analytics (Experimental)](../services/mobileanalytics/index.html){: new_window}
* [Mobile Client Access](../services/mobileaccess/index.html){: new_window}
* [Mobile Foundation](../services/mobilefoundation/index.html){: new_window}
* [Mobile Quality Assurance)](../services/MobileQualityAssurance/index.html){: new_window}
* [Push Notifications](../services/mobilepush/index.html){: new_window}
-->

## Publicaciones del blog
{: #general}
* [Publicación del blog: Introducción del panel de control de Bluemix Mobile](https://developer.ibm.com/bluemix/2016/07/08/new-bluemix-mobile-dashboard/){: new_window}
* [Publicación del blog: Bluemix Mobile, Parte 1: Creación de una aplicación Store Catalog](https://developer.ibm.com/bluemix/2016/07/13/bluemix-mobile-creating-store-catalog-app-part1/){: new_window}
* [Publicación del blog: Bluemix Mobile, Parte 2: Integración de programa de fondo de Bluemix personalizado en la app Store Catalog](https://developer.ibm.com/bluemix/2016/07/14/bluemix-mobile-integrating-custom-backend-part2/){: new_window}

## Guías de aprendizaje y ejemplos
{: #samples}
* [Backend móvil para Bluemix](https://github.com/ibm-bluemix-mobile-services/mobiledashboard-storecatalog-backend){: new_window}
