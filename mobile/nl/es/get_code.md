---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock: .codeblock}

# Obtener código
{: #Get_Code}

Cuando haya completado la configuración del proyecto móvil con las funciones, podrá descargar el código que le permite ejecutar el mismo en Xcode o Android Studio. El proyecto descargado está preconfigurado con las dependencias y las credenciales requeridas de SDK para cada función que configure.

Tendrá que completar las credenciales para servicios que no sean configurables en el proyecto descargado. El archivo `README.md` para el proyecto iniciador contiene instrucciones. Visualice el archivo `README.md` en un visor Markdown para completar la configuración.

### Herramientas necesarias del desarrollador
{: #prereq-dev-tools}

Las siguientes herramientas de desarrollador son necesarias cuando trabaja con código generado desde el panel de control de {{site.data.keyword.Bluemix_notm}} Mobile:

#### Android
* [Android Studio 2.2 ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](https://developer.android.com/studio "icono de enlace externo")
	* Instale la última versión del tiempo de ejecución de [Android 7.0 ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](https://www.android.com/versions/nougat-7-0/ "icono de enlace externo"). 

#### iOS
* [Xcode 8.0 ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](https://developer.apple.com/xcode/ "icono de enlace externo") (recomendado)
	* Instale la última versión del tiempo de ejecución de [iOS 10 ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](http://www.apple.com/ios/ios-10/ "icono de enlace externo"). 
* [Homebrew ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](http://brew.sh/ "icono de enlace externo")
	* Herramienta de línea de mandatos para ayudar en la instalación de otras herramientas y tiempos de ejecución, como por ejemplo CocoaPods y Carthage, para desarrolladores de Apple.
* Gestor de dependencias de [CocoaPods ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](https://cocoapods.org/ "icono de enlace externo") para instalar dependencias de iOS SDK. Utilice la versión más reciente:

	```
	$ sudo gem install cocoapods --pre
	```
* Gestor de dependencias de [Carthage ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](https://github.com/Carthage/Carthage "icono de enlace externo") para instalar los SDK de Watson Developer Cloud. 

	```
	$ brew install carthage
	```

#### {{site.data.keyword.Bluemix_notm}}
* NodeJS (tiempos de ejecución de Node y NPM) para ayudar con la ejecución de API Connect Loopback y de otras herramientas de Bluemix Productivity.

	Para ejecutar las herramientas de API Connect de forma local, utilice Node 5.x:
	```
	$ brew install Node5
	```

* [Herramientas de CLI de Bluemix ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](http://clis.ng.bluemix.net/ui/home.html "icono de enlace externo").
Herramientas de líneas de mandatos para desplegar de forma sencilla los tiempos de ejecución de Cloud Foundry desde una interfaz de línea de mandatos con Bluemix.  
