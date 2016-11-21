---

copyright:
  years: 2016
lastupdated: "2016-10-18"

---
{:new_window: target="_blank"}

# Novedades del panel de control de Mobile
{: #what_is_new}

Última actualización: 18 de octubre de 2016
{: .last-updated}

La actualización de octubre del panel de control de {{site.data.keyword.Bluemix}} Mobile ha introducido los cambios siguientes:

   * Ahora puede añadir prestaciones de Notificaciones Push y Analytics al proyecto directamente desde el panel de control.
   * Ahora están disponibles los [Iniciadores de código](starters.html#Code_Starter).
   * Ahora se da soporte a Swift.


### Analítica
{: #analytics}

   * La modalidad de demostración está habilitada de forma predeterminada al añadir la prestación Analytics. Puede desactivar la modalidad de demostración para ver las analíticas tras ejecutar la aplicación.


### Creador de IU
{: #ui_builder}

   * Ahora se accede a la prestación de **Notificaciones Push** desde el proyecto.
   * El separador **Valores del proyecto** se ha redenominado al separador **Valores**.
   * El separador **Autenticación** se ha redenominado al separador **Acceso de usuarios**.


### Código
{: #code}

   * El código generado de Objective-C y Swift para iOS utiliza ahora CocoaPods para gestionar las dependencias. Esto significa que tiene que instalar CocoaPods. Para instalarlo, ejecute `sudo gem install cocoapods`. Una vez que CocoaPods se haya instalado, ejecute `pod setup` para configurarlo (si aún no se ha configurado). Finalmente, ejecute `pod install` para descargar e instalar las dependencias del proyecto necesarias antes de abrir el archivo `.xcworkspace` en Xcode. Hay detalles adicionales disponibles en el archivo `README.md` en el archivado de código descargado. Consulte sobre [Prerequisite Developer Tools](get_code.html#prereq-dev-tools) para obtener más información.

Consulte con frecuencia para estar al corriente de las nuevas actualizaciones.


# Enlaces relacionados
{: #rellinks}

<!-- links to internal services don't work
## {{site.data.keyword.Bluemix_notm}} Mobile services
{: #general}
* [Mobile Analytics (Beta)](../services/mobileanalytics/index.html){: new_window}
* [Mobile Client Access](../services/mobileaccess/index.html){: new_window}
* [Mobile Foundation](../services/mobilefoundation/index.html){: new_window}
* [Mobile Quality Assurance)](../services/MobileQualityAssurance/index.html){: new_window}
* [Push Notifications](../services/mobilepush/index.html){: new_window}
-->

## Publicaciones del blog
{: #general}
* [Publicación del blog: Introducción del panel de control de Bluemix Mobile](https://developer.ibm.com/bluemix/2016/07/08/new-bluemix-mobile-dashboard/){: new_window}
* [Publicación del blog: Introducción de la siguiente generación del panel de control de Bluemix Mobile](https://ibm.com/blogs/bluemix/2016/10/introducing-the-next-generation-of-the-bluemix-mobile-dashboard/){: new_window}
* [Publicación del blog: Introducción de Bluemix Mobile Code Starters](https://www.ibm.com/blogs/bluemix/2016/10/rapid-dev-with-mobile-code-starters/){: new_window}
* [Publicación del blog: Bluemix Mobile, Parte 1: Creación de una aplicación Store Catalog](https://developer.ibm.com/bluemix/2016/07/13/bluemix-mobile-creating-store-catalog-app-part1/){: new_window}
* [Publicación del blog: Bluemix Mobile, Parte 2: Integración de programa de fondo de Bluemix personalizado en la app Store Catalog](https://developer.ibm.com/bluemix/2016/07/14/bluemix-mobile-integrating-custom-backend-part2/){: new_window}

## Guías de aprendizaje y ejemplos
{: #samples}
* [Backend móvil para Bluemix](https://github.com/ibm-bluemix-mobile-services/mobiledashboard-storecatalog-backend){: new_window}
