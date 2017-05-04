---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-18"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock: .codeblock}

# Obtener código
{: #Get_Code}

Cuando haya completado la configuración del proyecto con las funciones, podrá descargar el código que le permite ejecutar la aplicación. El proyecto descargado está preconfigurado con las dependencias y las credenciales requeridas de SDK para cada función que configure.

Tendrá que completar las credenciales para servicios que no sean configurables en el proyecto descargado. El archivo `README.md` para el proyecto iniciador contiene instrucciones. Visualice el archivo `README.md` en un visor Markdown para completar la configuración.

## Herramientas necesarias del desarrollador
{: #prereq-dev-tools}

Las siguientes herramientas de desarrollador son necesarias cuando trabaja con código generado desde la {{site.data.keyword.dev_console}} de {{site.data.keyword.Bluemix_notm}}:


### General
{: #general notoc}

* [Homebrew ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](http://brew.sh/)
	* Herramienta de línea de mandatos para ayudar en la instalación de otras herramientas y tiempos de ejecución, como por ejemplo CocoaPods y Carthage, para desarrolladores de Apple.

* [Docker ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://www.docker.com/get-docker)
	* Proyecto de código abierto para ayudar en la ejecución y depuración de aplicaciones en contenedores. Esto solo es necesario para proyectos que no sean móviles.

### {{site.data.keyword.Bluemix_notm}}
{: #bluemix notoc}

* Node.js (tiempos de ejecución Node y npm) para ayudar con la ejecución de {{site.data.keyword.apiconnect_short}} Loopback y otras herramientas de {{site.data.keyword.Bluemix_notm}} Productivity.

	Para ejecutar herramientas {{site.data.keyword.apiconnect_short}} de forma local, utilice 5.x:
	
	```
	$ brew install Node5
	```

* [Herramientas de CLI de Bluemix ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](http://clis.ng.bluemix.net/ui/home.html)

   Herramientas de líneas de mandatos para desplegar los tiempos de ejecución de Cloud Foundry desde una interfaz de línea de mandatos con {{site.data.keyword.Bluemix_notm}}.  

* [{{site.data.keyword.dev_cli_notm}} ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](dev_cli.html)

	Plugin de CLI de {{site.data.keyword.Bluemix_notm}} para crear, probar y desplegar proyectos web y móviles.
	
* [Plugin de generador de SDK ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](sdk_cli.html)

	{{site.data.keyword.Bluemix_notm}} Plugin de CLI para generar SDK desde una definición de la API REST compatible con la [Especificación de Open API ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://www.openapis.org/).

### Android
{: #android notoc}

* [Android Studio 2.2 o superior ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.android.com/studio)
	* Instale el último tiempo de ejecución de [Android 7.0 ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](https://www.android.com/versions/nougat-7-0/).

### iOS
{: #ios notoc}

* [Xcode 8 ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.apple.com/xcode/) (recomendado)

<!-- * Install the latest [iOS 10 ![External link icon](../icons/launch-glyph.svg "External link icon")](http://www.apple.com/ios/ios-10/) runtime.
-->
* Gestor de dependencia de [CocoaPods ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](https://cocoapods.org/) para instalar dependencias del SDK de iOS. Utilice la versión más reciente:

	```
	$ sudo gem install cocoapods --pre
	```
* [Gestor de dependencias de Carthage ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/Carthage/Carthage) para instalar los SDK de {{site.data.keyword.watson}} Developer Cloud.

	```
	$ brew install carthage
	```
