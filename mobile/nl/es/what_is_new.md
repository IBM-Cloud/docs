---

copyright:
  years: 2016
lastupdated: "2016-10-21"

---
{:new_window: target="_blank"}

# Novedades del panel de control de Mobile
{: #what_is_new}

La actualización de octubre del panel de control de {{site.data.keyword.Bluemix}} Mobile ha introducido los cambios siguientes:

   * Ahora puede añadir prestaciones de Notificaciones Push y Analytics al proyecto directamente desde el panel de control.
   * Ahora están disponibles los [Iniciadores de código](starters.html#Code_Starter).
   * Puede añadir autenticación a sus proyectos que ha creado a partir de un iniciador de código. 
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
