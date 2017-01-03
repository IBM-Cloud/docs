---

copyright:
  years: 2016
lastupdated: "2016-12-01"

---
{:new_window: target="_blank"}

# Novedades del panel de control de Mobile
{: #what_is_new}


### Novedad desde: noviembre de 2016
{: #nov-2016}

La actualización de noviembre de 2016 del panel de control de {{site.data.keyword.Bluemix}} Mobile ha introducido los cambios siguientes:

   * Ahora puede generar artefactos SDK para proyectos desde la página **Código**. 
   * Ahora se admite Cordova para el iniciador de código de Basic. 
   * Ahora puede [notificar sucesos de red](/docs/services/mobileanalytics/sdk.html#network-requests){: new_window} y [supervisar solicitudes de red](/docs/services/mobileanalytics/app-monitoring.html#monitor-network-requests){: new_window} en la página **Solicitudes de red** de la consola de {{site.data.keyword.mobileanalytics_short}}. 
   * Ahora puede [exportar datos a dashDB](/docs/services/mobileanalytics/app-monitoring.html#dashdb){: new_window} en la consola de {{site.data.keyword.mobileanalytics_short}}. 


### Novedad de octubre de 2016
{: #oct-2016}

La actualización de octubre de 2016 del panel de control de {{site.data.keyword.Bluemix_notm}} Mobile ha introducido los cambios siguientes:

   * Ahora puede añadir prestaciones de Notificaciones Push y Analytics al proyecto directamente desde el panel de control.
   * Ahora están disponibles los [Iniciadores de código](starters.html#Code_Starter).
   * Puede añadir autenticación a sus proyectos que ha creado a partir de un iniciador de código.
   * Ahora se da soporte a Swift.


#### Analítica
{: #analytics}

   * La modalidad de demostración está habilitada de forma predeterminada al añadir la prestación Analytics. Puede desactivar la modalidad de demostración para ver las analíticas tras ejecutar la aplicación.


#### Creador de IU
{: #ui_builder}

   * Ahora se accede a la prestación de **Notificaciones Push** desde el proyecto.
   * El separador **Valores del proyecto** se ha redenominado al separador **Valores**.
   * El separador **Autenticación** se ha redenominado al separador **Acceso de usuarios**.


#### Código
{: #code}

   * El código generado de Objective-C y Swift para iOS utiliza ahora CocoaPods para gestionar las dependencias. Esto significa que tiene que instalar CocoaPods. Para instalarlo, ejecute `sudo gem install cocoapods`. Una vez que CocoaPods se haya instalado, ejecute `pod setup` para configurarlo (si aún no se ha configurado). Finalmente, ejecute `pod install` para descargar e instalar las dependencias del proyecto necesarias antes de abrir el archivo `.xcworkspace` en Xcode. Hay detalles adicionales disponibles en el archivo `README.md` en el archivado de código descargado. Consulte sobre [Prerequisite Developer Tools](get_code.html#prereq-dev-tools) para obtener más información.

Consulte con frecuencia para estar al corriente de las nuevas actualizaciones.
