---

copyright:
  years: 2016
lastupdated: "2016-10-13"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock: .codeblock}

# Obtener código
{: #Get_Code}

Cuando haya completado la configuración del proyecto móvil con las funciones Push, Analytics y Authentication, podrá descargar el código que le permite ejecutar el mismo en Xcode o Android Studio. El proyecto descargado está preconfigurado con las dependencias y las credenciales requeridas de SDK para cada función que configure.

Tendrá que completar las credenciales para servicios que no sean configurables en el proyecto descargado. El archivo `README.md` para el proyecto iniciador contiene instrucciones. Visualice el archivo `README.md` en un visor Markdown para completar la configuración.

### Prerequisite Developer Tools
{: prereq-dev-tools}

Las siguientes herramientas de desarrollador son necesarias cuando trabaja con código generado desde el panel de control de {{site.data.keyword.Bluemix_notm}} Mobile:

#### Android
* [Android Studio 2.2](https://developer.android.com/studio)
	* Instale el tiempo de ejecución más reciente de [Android 7.0](https://www.android.com/versions/nougat-7-0/).

#### iOS
* Xcode 8.0 (recomendado)
	* Instale el tiempo de ejecución más reciente de [iOS 10](http://www.apple.com/ios/ios-10/).
* [Homebrew](http://brew.sh/)
	* Herramienta de línea de mandatos para ayudar en la instalación de otras herramientas y tiempos de ejecución, como por ejemplo CocoaPods y Carthage, para desarrolladores de Apple.
* Gestor de dependencia de [CocoaPods](https://cocoapods.org/) para instalar dependencias de SDK de iOS. Utilice la versión más reciente:

	```
	$ sudo gem install cocoapods --pre
	```
* Gestor de dependencia de [Carthage](https://github.com/Carthage/Carthage) para instalar los SDK de Watson Developer Cloud.

	```
	$ brew install carthage
	```

#### {{site.data.keyword.Bluemix_notm}}
* NodeJS (tiempos de ejecución de Node y NPM) para ayudar con la ejecución de API Connect Loopback y de otras herramientas de Bluemix Productivity.

	Para ejecutar las herramientas de API Connect de forma local, utilice Node 5.x:
	```
	$ brew install Node5
	```

* [Bluemix CLI Tools](http://clis.ng.bluemix.net/ui/home.html).
Herramientas de líneas de mandatos para desplegar de forma sencilla los tiempos de ejecución de Cloud Foundry desde una interfaz de línea de mandatos con Bluemix.  
