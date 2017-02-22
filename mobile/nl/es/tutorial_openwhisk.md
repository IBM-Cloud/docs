---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Guía de aprendizaje del iniciador de {{site.data.keyword.openwhisk_short}}
{: #tutorial}

En la siguiente guía de aprendizaje encontrará los pasos a seguir para crear un proyecto desde el iniciador de código de {{site.data.keyword.openwhisk_short}}, incluidas las herramientas que debe tener instaladas y, por lo tanto, los pasos para ejecutar el iniciador en Xcode y Android Studio.


### Instalación de herramientas del desarrollador
{: #dev_tools}

Asegúrese de haber instalado las [herramientas de desarrollador necesarias ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](get_code.html#prereq-dev-tools "icono de enlace externo"){: new_window}.


### Creación de un proyecto desde el iniciador de código de {{site.data.keyword.openwhisk_short}}
{: #create_project}

1. Cree un proyecto de panel de control de Mobile en {{site.data.keyword.Bluemix}}.

   1. Desde la página **Guía de inicio** del panel de control de Mobile, pulse **Crear proyecto**.

      De forma alternativa, puede pulsar **Crear proyecto** desde la página **Proyectos**.

   2. Pulse **Iniciadores de código**.

   3. Seleccione **{{site.data.keyword.openwhisk_short}}** y pulse **Crear proyecto**.

   4. Especifique el nombre del proyecto. En esta guía de aprendizaje utilizaremos `{{site.data.keyword.openwhisk_short}}Project`.
   
   5. Pulse **Crear**.

2. Opcional: Añada la función de {{site.data.keyword.mobilepushshort}}. 

   **Nota**: si desea ejecutar `pushAction`, debe añadir y configurar {{site.data.keyword.mobilepushshort}}.

   1. Pulse **Añadir** para **{{site.data.keyword.mobilepushshort}}** en la página **Visión general del proyecto**.

      De forma alternativa, puede pulsar **Crear** desde la página **{{site.data.keyword.mobilepushshort}}**. 

   2. Especifique el nombre del servicio y pulse **Crear**.

   3. Para iOS, [configure el servicio de notificación Push de Apple ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](/docs/services/mobilepush/t_push_provider_ios.html "icono de enlace externo"){: new_window}.

   4. Para Android, [configure Firebase Cloud Messaging ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](/docs/services/mobilepush/t_push_provider_android.html "icono de enlace externo"){: new_window}.
   
3. Opcional: Añada capacidad de análisis.

   1. Pulse **Añadir** para **Análisis** en la página **Visión general del proyecto**.

      De forma alternativa, puede pulsar **Crear** desde la página **Análisis**.

   2. Especifique el nombre del servicio y pulse **Crear**.
   
   3. Desactive la **Modalidad de demostración** para ver los datos del análisis después de ejecutar la app.
   
   4. Consulte [Iniciación a {{site.data.keyword.mobileanalytics_short}} ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](/docs/services/mobileanalytics/index.html "icono de enlace externo"){: new_window} para obtener más información sobre cómo configurar Analytics.
  
4. Opcional: Añada capacidad de autenticación.

   1. Pulse **Añadir** para **Autenticación** en la página **Visión general del proyecto**.

      De forma alternativa, puede seleccionar **Crear** en la página **Autenticación**.

   2. Especifique el nombre del servicio y pulse **Crear**.
   
   3. Active **Autenticación**.
   
   4. Seleccione su proveedor de identidad y especifique la información necesaria para configurarlo. Solo puede habilitar un proveedor de identidad.

   5. Consulte [Iniciación a {{site.data.keyword.amashort}} ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](/docs/services/mobileaccess/index.html "icono de enlace externo"){: new_window} para obtener más información sobre cómo configurar la autenticación. 

5. Genere el código del proyecto.

   1. Pulse **Obtener código** en la página **Visión general del proyecto** para seleccionar la plataforma y el lenguaje.
   
      Como alternativa, pulse la página **Código**.

   2. Para Swift, pulse **iOS Swift**.
   
   3. Para Android, pulse **Android**.
   
   4. Cuando se haya generado el código, pulse **Descargar código** para descargar el archivo del proyecto.


### Ejecución del proyecto Swift en Xcode
{: #run_swift}

1. Extraiga el archivo `{{site.data.keyword.openwhisk_short}}Project-Swift.zip`.

2. Abra el archivo `README.md` en un visor Markdown para ver los pasos a seguir para configurar el proyecto.

   1. Abra el terminar y vaya a la carpeta del proyecto.
   
      1. Ejecute `pod setup` si tiene que configurar el repositorio de CocoaPods.
      
      2. Ejecute `pod update` si tiene que actualizar los pods existentes.
      
      3. Ejecute `pod install` para instalar los pods necesarios para el proyecto.
      
   3. Abra el espacio de trabajo Xcode `{{site.data.keyword.openwhisk_short}}Project.xcworkspace`.

   4. Si desea ejecutar `pushAction`, debe configurar {{site.data.keyword.mobilepush}}.
      
3. Ejecute la app.


### Ejecución del proyecto Android en Android Studio
{: #run_android}

1. Extraiga el archivo `{{site.data.keyword.openwhisk_short}}Project-Android.zip`. 

2. Abra el archivo `README.md` en un visor Markdown para configurar el proyecto.

   1. Abra el proyecto `{{site.data.keyword.openwhisk_short}}Project-Android` en Android Studio.

   2. Si desea ejecutar `pushAction`, debe configurar {{site.data.keyword.mobilepush}}.
      
3. Ejecute la app.


## Qué hacer a continuación
{: #what_next}

Consulte otras guías de aprendizaje.


### Guías de aprendizaje del Iniciador de IU
{: #tutorials_UI}

* [Guía de aprendizaje: Catálogo de almacenamiento](tutorial_store_catalog.html)


### Guías de aprendizaje del Iniciador de código
{: #tutorials_Code}

* [Guía de aprendizaje: Basic](tutorial.html)
* [Guía de aprendizaje: Cloudant Sync](tutorial_cloudant_synd.html)
* [Guía de aprendizaje: {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [Guía de aprendizaje: Lenguaje Watson](tutorial_watson_language.html)
* [Guía de aprendizaje: Weather](tutorial_weather.html)
