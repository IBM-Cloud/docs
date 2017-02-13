---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}

# Novedades del panel de control de Mobile
{: #what_is_new}

### Novedad desde: diciembre de 2016
{: #dec-2016}

La actualización de diciembre de 2016 del panel de control de {{site.data.keyword.Bluemix}} Mobile ha introducido los cambios siguientes:

   * Puede eliminar un servicio conectado de un proyecto para que se pueda suprimir y reutilizar con otro proyecto.  
   * Puede añadir un servicio existente a un proyecto. 
   * Puede crear o conectar un servicio CloudantNoSQL existente como origen de datos cuando utilice un iniciador de código. 
   * Si se admite, puede crear o conectar un servicio Object Storage existente como origen de datos para el proyecto. 
   * Puede personalizar el diseño de navegación de la app que cree con un iniciador de IU.  
   

### Novedad desde: noviembre de 2016
{: #nov-2016}

La actualización de noviembre de 2016 del panel de control de {{site.data.keyword.Bluemix}} Mobile ha introducido los cambios siguientes:

   * Ahora puede generar artefactos SDK para proyectos desde la página **Código**. 
   * Ahora se admite Cordova para el iniciador de código de Basic. 
   * Ahora puede [notificar sucesos de red ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](/docs/services/mobileanalytics/sdk.html#network-requests "icono de enlace externo"){: new_window} y [supervisar solicitudes de red ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](/docs/services/mobileanalytics/app-monitoring.html#monitor-network-requests "icono de enlace externo"){: new_window} en la página **Solicitudes de red** de la Consola de {{site.data.keyword.mobileanalytics_short}}. 
   * Ahora puede [exportar datos a dashDB ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](/docs/services/mobileanalytics/app-monitoring.html#dashdb "icono de enlace externo"){: new_window} en la Consola de {{site.data.keyword.mobileanalytics_short}}. 


### Novedad de octubre de 2016
{: #oct-2016}

La actualización de octubre de 2016 del panel de control de {{site.data.keyword.Bluemix_notm}} Mobile ha introducido los cambios siguientes:

   * Ahora puede añadir prestaciones de {{site.data.keyword.mobilepushshort}} y Analytics al proyecto directamente desde el panel de control.
   * Ahora están disponibles los [Iniciadores de código](starters.html#Code_Starter).
   * Puede añadir autenticación a sus proyectos que ha creado a partir de un iniciador de código.
   * Ahora se da soporte a Swift.


#### Analítica
{: #analytics}

   * La modalidad de demostración está habilitada de forma predeterminada al añadir la prestación Analytics. Puede desactivar la modalidad de demostración para ver las analíticas tras ejecutar la aplicación.


#### Creador de IU
{: #ui_builder}

   * Ahora se accede a la prestación **{{site.data.keyword.mobilepushshort}}** desde el proyecto.
   * El separador **Valores del proyecto** se ha redenominado al separador **Valores**.
   * El separador **Autenticación** se ha redenominado al separador **Acceso de usuarios**.


#### Código
{: #code}

   * El código generado de Objective-C y Swift para iOS utiliza ahora CocoaPods para gestionar las dependencias. Esto significa que tiene que instalar CocoaPods. Para instalarlo, ejecute `sudo gem install cocoapods`. Una vez que CocoaPods se haya instalado, ejecute `pod setup` para configurarlo (si aún no se ha configurado). Finalmente, ejecute `pod install` para descargar e instalar las dependencias del proyecto necesarias antes de abrir el archivo `.xcworkspace` en Xcode. Hay detalles adicionales disponibles en el archivo `README.md` en el archivado de código descargado. Consulte sobre las [Herramientas necesarias del desarrollador](get_code.html#prereq-dev-tools) para obtener más información.

Consulte con frecuencia para estar al corriente de las nuevas actualizaciones.
