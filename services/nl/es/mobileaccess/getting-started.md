---

copyright:
  años: 2015, 2016

---

# Cómo empezar
{: #getting-started}
Para empezar con {{site.data.keyword.amashort}}, puede añadir el servicio de {{site.data.keyword.amashort}} a una aplicación existente de {{site.data.keyword.Bluemix}} o bien puede crear una nueva app con el contenedor modelo.  

## Creación de una instancia del servicio de {{site.data.keyword.amashort}}
{: #service-instance}

Puede crear una nueva instancia de un servicio de {{site.data.keyword.amashort}} desde el catálogo de {{site.data.keyword.Bluemix}}.  Si no utiliza el contenedor modelo para crear un programa de fondo móvil, debe configurar el SDK del servidor en un programa de fondo existente.


  * **Nueva app**: las instrucciones de las siguientes secciones describen cómo crear una nueva app que crea un programa de fondo móvil y se protege con el SDK del servidor de {{site.data.keyword.amashort}}. Haga clic en el contenedor modelo de **MobileFirst Services Starter** para crear una aplicación nueva con el servicio de {{site.data.keyword.amashort}}.
  * **App existente**: pulse el icono {{site.data.keyword.amashort}} y cree una nueva instancia de servicio que esté enlazada a una aplicación existente. Para configurar el SDK del servidor en la app existente, consulte [Protección de recursos de nube](protecting-resources.html).


## Creación de un programa de fondo móvil con el contenedor modelo de MobileFirst Services Starter
{: #create-backend}
Cuando utilice MobileFirst Services Starter, obtendrá una instancia de un tiempo de ejecución Node.js que se ejecuta en IBM {{site.data.keyword.Bluemix_notm}} para implementar la lógica del programa de fondo móvil. Un conjunto de servicios móviles principales que proporcionan seguridad, datos, envíos por push y funciones de supervisión están enlazados a esa app Node.js. Tras crear la app Node.js de {{site.data.keyword.Bluemix_notm}}, puede configurar el entorno de desarrollo y empezar a utilizar los SDK de {{site.data.keyword.Bluemix_notm}} Mobile Services. Puede utilizar los SDK para acceder a los servicios que están enlazados a la app de nube con sencillas llamadas API.

1. En el catálogo de {{site.data.keyword.Bluemix_notm}}, vaya a la sección **Contenedores modelo** y haga clic en **MobileFirst Services Starter**.
1. Añada información sobre el programa de fondo móvil, incluido el espacio, nombre, host y plan de servicio.
1. Haga clic en **CREAR**.



## Próximos pasos
{: #next-steps}
Varios puntos finales de la aplicación Node.js que ha creado con el contenedor modelo estarán protegidos con {{site.data.keyword.amashort}}. Para obtener más información sobre la aplicación de fondo móvil predeterminada, consulte [bms-hellotodo-strongloop](https://github.com/ibm-bluemix-mobile-services/bms-hellotodo-strongloop).

Puede configurar la app móvil para que utilice el SDK de {{site.data.keyword.amashort}}.  Después de configurar el SDK, podrá empezar a configurar la autenticación y supervisión de la app.  Siga las instrucciones de la plataforma de desarrollo móvil:

* [Android](getting-started-android.html)
* [iOS (SDK de Swift)](getting-started-ios.html)
* [iOS (SDK de Objective-C)](getting-started-ios.html)
* [Cordova](getting-started-cordova.html)
