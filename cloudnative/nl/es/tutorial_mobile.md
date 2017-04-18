---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Guía de aprendizaje del iniciador Mobile Basic
{: #tutorial}

En la siguiente guía de aprendizaje encontrará los pasos a seguir para crear un proyecto desde el iniciador Mobile Basic, incluidas las herramientas que debe tener instaladas y, por lo tanto, los pasos para ejecutar el proyecto en Xcode y Android Studio.


## Instalación de herramientas del desarrollador
{: #dev_tools}

Asegúrese de haber instalado las [herramientas de desarrollador necesarias ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](get_code.html#prereq-dev-tools){: new_window}.


## Creación de un proyecto mediante la {{site.data.keyword.dev_console}}
{: #create-devex}

1. Cree un proyecto de {{site.data.keyword.dev_console}} en {{site.data.keyword.Bluemix}}.

   1. Desde la página **Cómo empezar** en la {{site.data.keyword.dev_console}}, pulse **Crear proyecto**.

      De forma alternativa, puede pulsar **Crear proyecto** desde la página **Proyectos**.

   2. Seleccione **Aplicación móvil** y pulse **Siguiente**.

   3. Seleccione **Basic** y pulse **Siguiente**.

   4. Especifique el nombre del proyecto. En esta guía de aprendizaje, utilizaremos `MobileBasicProject`.

   5. Seleccione su plataforma. En esta guía de aprendizaje, utilizaremos `Swift`.
   
   6. Pulse **Crear**.

2. Opcional: Añada capacidad de autenticación.

   1. Pulse **Añadir** para **Autenticación** en la página **Visión general del proyecto**.

      De forma alternativa, puede seleccionar **Crear** o **Añadir existente** en la página **Prestaciones > Authentication**.

   2. Especifique el nombre del servicio y pulse **Crear**.
   
   3. Active **Autenticación**.
   
   4. Seleccione su proveedor de identidad y especifique la información necesaria para configurarlo. Solo puede habilitar un proveedor de identidad.
   
   5. Consulte [Configuración de los proveedores de identidad} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](/docs/services/appid/identity-providers.html){: new_window} para obtener más información sobre cómo configurar Authentication.

3. Opcional: Añada capacidad de análisis.

   1. Pulse **Añadir** para **Análisis** en la página **Visión general del proyecto**.

      De forma alternativa, pulse **Crear** o **Añadir existente** desde la página **Prestaciones > Analytics**.

   2. Especifique el nombre del servicio y pulse **Crear**.
   
   3. Desactive la **Modalidad de demostración** para ver los datos del análisis después de ejecutar la app.
   
   4. Consulte [Iniciación a {{site.data.keyword.mobileanalytics_short}} ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](/docs/services/mobileanalytics/index.html){: new_window} para obtener más información sobre cómo configurar Analytics.

4. Opcional: Añada la función de {{site.data.keyword.mobilepushshort}}.

   1. Pulse **Añadir** para **{{site.data.keyword.mobilepushshort}}** en la página **Visión general del proyecto**.

      De forma alternativa, pulse **Crear** o **Añadir existente** desde la página **Prestaciones > {{site.data.keyword.mobilepushshort}}**.

   2. Especifique el nombre del servicio y pulse **Crear**.

   3. Para iOS, [configure el servicio de notificación Push de Apple ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](/docs/services/mobilepush/t_push_provider_ios.html){: new_window}.

   4. Para Android, [configure Firebase Cloud Messaging ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](/docs/services/mobilepush/t_push_provider_android.html){: new_window}.

5. Opcional: Añada la capacidad de Datos.

   1. Pulse **Ver** para **Datos** en la página **Visión general del proyecto**.

      De forma alternativa, puede seleccionar **Crear** en la página **Datos**.
      
   2. Elija **{{site.data.keyword.cloudant_short_notm}}** o **{{site.data.keyword.objectstorageshort}}**.

   3. Especifique el nombre del servicio y pulse **Crear**.

   4. Consulte [Iniciación a {{site.data.keyword.cloudant_short_notm}} ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](/docs/services/Cloudant/index.html){: new_window} para obtener más información sobre cómo configurar {{site.data.keyword.cloudant_short_notm}}.

   5. Consulte [Iniciación a {{site.data.keyword.objectstorageshort}} ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](/docs/services/ObjectStorage/index.html){: new_window} para obtener más información sobre cómo configurar {{site.data.keyword.objectstorageshort}}.

6. Genere el código del proyecto.

   1. Pulse **Obtener el código** en la página **Visión general del proyecto** para seleccionar el lenguaje.
   
      Como alternativa, pulse la página **Código**.
      
   2. Pulse **Generar Swift**.
   
   3. Cuando se haya generado el código, pulse **Descargar Swift** para descargar el archivo del proyecto.

7. Opcional: [Actualización del proyecto](project_overview_page.html#update_language) para generar un nuevo lenguaje.


## Creación de un proyecto mediante {{site.data.keyword.dev_cli_notm}}
{: #create-cli}

1. Asegúrese de haber instalado [{{site.data.keyword.dev_cli_short}}](dev_cli.html).

2. En la solicitud de terminal, vaya al directorio local que prefiera y ejecute el siguiente mandato.

	```
	bx dev create
	```
	{: codeblock}
	
3. Proporcione los siguientes valores cuando se le solicite:

	* Seleccione un patrón: 2 (para Móvil)
	* Seleccione un iniciador: 1 (para Basic)
	* Seleccione una plataforma: 3 (para iOS Swift)
	* Especifique un nombre para el proyecto: `MobileBasicProjectCLI`

4. Si desea añadir servicios al proyecto, escriba `y` en la solicitud de preguntas y responda el resto de las preguntas.

5. Cuando `MobileBasicProjectCLI` se haya guardado correctamente, vaya a la carpeta `MobileBasicProjectCLI/MobileBasicProjectCLI-Swift`.


## Ejecución del proyecto Swift en Xcode
{: #run_swift}

1. Extraiga el archivo `MobileBasicProject-Swift.zip`.

2. Abra el archivo `README.md` en un visor Markdown para ver los pasos a seguir para configurar el proyecto.

   1. Abra el terminar y vaya a la carpeta del proyecto.
   
      1. Ejecute `pod setup` si tiene que configurar el repositorio de CocoaPods.
      
      2. Ejecute `pod update` si tiene que actualizar los pods existentes.
      
      3. Ejecute `pod install` para instalar los pods necesarios para el proyecto.
      
   3. Abra el espacio de trabajo Xcode `BasicProject.xcworkspace`.
      
3. Ejecute la app.


## Ejecución del proyecto Cordova en Xcode
{: #run_cordova_xcode}

1. Extraiga el archivo `MobileBasicProject-Cordova.zip`.

2. Abra el archivo `README.md` en un visor Markdown para configurar el proyecto.

   1. Abra el proyecto `platforms/ios` en Xcode.
      
3. Ejecute la app.


## Ejecución del proyecto Cordova en Android Studio
{: #run_cordova_studio}

1. Extraiga el archivo `BasicProject-Cordova.zip`.

2. Abra el archivo `README.md` en un visor Markdown para configurar el proyecto.

   1. Abra el proyecto `platforms/android` en Android Studio.
      
3. Ejecute la app.


## Ejecución del proyecto Android en Android Studio
{: #run_android}

1. Extraiga el archivo `MobileBasicProject-Android.zip`.

2. Abra el archivo `README.md` en un visor Markdown para configurar el proyecto.

   1. Abra el proyecto `BasicProject-Android` en Android Studio.
      
3. Ejecute la app.
