---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Preparación de MQA con una app de Cordova (en desuso)
{: #instrumentcord}

Para utilizar {{site.data.keyword.mqafull}} con la app de Cordova, debe descargar el SDK y prepararlo realizando algunos cambios mediante la interfaz de línea de mandatos.
{: shortdesc}

Para poder preparar una app con {{site.data.keyword.mqa}}, debe tener una cuenta de {{site.data.keyword.Bluemix}} y la versión correctamente instalada del entorno de desarrollo para las plataformas de la app que está preparando.

Para preparar {{site.data.keyword.mqa}} para que funcione con la app de Cordova, lleve a cabo las siguientes tareas:

1. Añada los permisos necesarios y el SDK descargado al proyecto de Cordova.

	1. Abra un indicador de mandatos y vaya al directorio que contiene los archivos de proyecto.

	2. Añada el plug-in de {{site.data.keyword.mqa}} al proyecto de Cordova realizando los pasos siguientes, en función de su entorno:

		**Importante**: Si está utilizando Xcode 7.x en iOS 9, debe establecer el valor Habilitar Bitcode en No en la Configuración de creación de Xcode. Puede cambiar este valor abriendo Xcode con el archivo de proyecto .xcodeproj de Cordova, que se encuentra en la carpeta platform\iPhone.

		* IBM MobileFirst™ Platform Foundation Versión 7.1:

			1. Escriba el siguiente mandato para instalar el plugin de {{site.data.keyword.mqa}}:

				```
				mfp cordova plugin add plugin_location
				```
				{: codeblock}

			Donde *plugin_location* es la vía de acceso al directorio del plug-in extraído de {{site.data.keyword.mqa}} que ha descargado.

			2. Si la app se ejecuta en Android, cambie el nombre del archivo `project_name/app_name/platforms/android/custom_rules.xml` a `custom_rules.xml.bak`.

		* Apache Cordova anterior a la versión 4.0:
			1. Escriba el siguiente mandato para instalar el plugin de {{site.data.keyword.mqa}}:

				```
				cordova plugin add plugin_location
				```
				{: codeblock}

			Donde *plugin_location* es la vía de acceso al directorio del plug-in extraído de {{site.data.keyword.mqa}} que ha descargado.

			2. Escriba el siguiente mandato para añadir un plugin necesario adicional:

				```
				cordova plugin add cordova-plugin-device
				```
				{: codeblock}

			3. Si la app se ejecuta en Android, cambie el nombre del archivo `project_name/app_name/platforms/android/custom_rules.xml` a `custom_rules_bak.xml`.

		* Apache Cordova versión 4.0, o posterior:

			1. Escriba el siguiente mandato:

				```
				cordova plugin add plugin_location
				```
				{: codeblock}

			Donde *plugin_location* es la vía de acceso al directorio del plug-in extraído de Cordova de {{site.data.keyword.mqa}} que ha descargado.

			2. Escriba el siguiente mandato para añadir un plugin necesario adicional:

				```
				cordova plugin add cordova-plugin-device
				```
				{: codeblock}

2. Inicie una sesión nueva de {{site.data.keyword.mqa}} con cada inicio de sesión.

	1. Abra el archivo `index.js` que se encuentra en el directorio siguiente: `your_project_name\www\js`.

	2. Añada la función y los parámetros siguientes dentro de la función `onDeviceReady()` que se encuentra en el archivo `index.js`. Coloque la función antes del corchete de cierre de la función.

	Restricción: Para una app que ya se encuentre preparada para Mobile Quality Assurance utilizando una versión anterior del plug-in para que Cordova utilice las características incluidas en el plug-in de Mobile Quality Assurance para Cordova versión 3.0.18, y posterior, debe volver a generar y sustituir la clave de app. Para obtener más información sobre cómo volver a generar la clave de app, consulte Gestión de configuración de la app. Las claves de app que se generaron antes de febrero de 2016 siguen funcionando con el plug-in antiguo, pero ya no funcionarán cuando actualice el plug-in a la versión 3.0.18, o posterior.

		```
		MQA.startNewSession(
			{
				mode: "QA",
				// o mode: "MARKET" para modo de producción.
			android: {
				appKey: "your_MQA_Android_appKey" ,
				notificationsEnabled: true},
			ios: {
				appKey: "your_MQA_iOS_appKey" ,
				screenShotsFromGallery: true,}
			},
			{
			success: function () {console.log("Session
			   Started successfully");},
			error: function (string) { console.log("Session
			   error" + string);}
			}
			);
		```
		{: codeblock}

	3. Continúe con los pasos de [Iniciación a {{site.data.keyword.mqa}}](index.html).



# Enlaces relacionados
{: #rellinks notoc}

## Enlaces relacionados
{: #general notoc}
* [Iniciación a {{site.data.keyword.mqa}}](index.html){:new_window}
