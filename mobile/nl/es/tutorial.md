---

copyright:
  years: 2016
lastupdated: "2016-11-22"

---
{:new_window: target="_blank"}

# Guía de aprendizaje del iniciador de código Basic
{: #tutorial}

En la siguiente guía de aprendizaje encontrará los pasos a seguir para crear un proyecto desde el iniciador de código de Basic, incluidas las herramientas que debe tener instaladas y, por lo tanto, los pasos para ejecutar el iniciador en Xcode y Android Studio.


### Instalación de herramientas del desarrollador
{: #dev_tools}

Asegúrese de haber instalado las [herramientas necesarias del desarrollador](get_code.html#prereq-dev-tools){: new_window}.


### Creación de un proyecto desde el iniciador de código de Basic
{: #create_project}

1. Cree un proyecto de panel de control de Mobile en {{site.data.keyword.Bluemix}}.

   1. Desde la página **Guía de inicio** del panel de control de Mobile, pulse **Crear proyecto**.

      De forma alternativa, puede pulsar **Crear proyecto** desde la página **Proyectos**.

   2. Pulse **Iniciadores de código**.

   3. Seleccione **Basic** y pulse **Crear proyecto**.

   4. Especifique el nombre del proyecto. En esta guía de aprendizaje utilizaremos `BasicProject`.
   
   5. Pulse **Crear**.

2. Opcional: Añada capacidad de notificaciones Push.

   1. Pulse **Añadir** para **Notificaciones Push** en la página **Visión general del proyecto**.

      De forma alternativa, puede pulsar **Crear** desde la página **Notificaciones Push**.

   2. Especifique el nombre del servicio y pulse **Crear**.

   3. Para iOS, [configure el Servicio de notificaciones Push de Apple](/docs/services/mobilepush/t_push_provider_ios.html){: new_window}.

   4. Para Android, [configure Firebase Cloud Messaging](/docs/services/mobilepush/t_push_provider_android.html){: new_window}.
   
3. Opcional: Añada capacidad de análisis.

   1. Pulse **Añadir** para **Análisis** en la página **Visión general del proyecto**.

      De forma alternativa, puede pulsar **Crear** desde la página **Análisis**.

   2. Especifique el nombre del servicio y pulse **Crear**.
   
   3. Desactive la **Modalidad de demostración** para ver los datos del análisis después de ejecutar la app.
   
   4. Consulte [Iniciación a {{site.data.keyword.mobileanalytics_short}}](/docs/services/mobileanalytics/index.html){: new_window} para obtener más información sobre cómo configurar el análisis.
  
4. Opcional: Añada capacidad de autenticación.

   1. Pulse **Añadir** para **Autenticación** en la página **Visión general del proyecto**.

      De forma alternativa, puede seleccionar **Crear** en la página **Autenticación**.

   2. Especifique el nombre del servicio y pulse **Crear**.
   
   3. Active **Autenticación**.
   
   4. Seleccione su proveedor de identidad y especifique la información necesaria para configurarlo. Solo puede habilitar un proveedor de identidad.

   5. Consulte [Iniciación a {{site.data.keyword.amashort}}](/docs/services/mobileaccess/index.html){: new_window} para obtener más información sobre cómo configurar la autenticación.

5. Genere el código del proyecto.

   1. Pulse **Obtener código** en la página **Visión general del proyecto** para seleccionar la plataforma y el lenguaje.
   
      Como alternativa, pulse la página **Código**.
      
   2. Para Objective-C, pulse **iOS Obj-C**.

   3. Para Swift, pulse **iOS Swift**.
   
   4. Para Cordova, pulse **Cordova**.

   5. Para Android, pulse **Android**.
   
   6. Cuando se haya generado el código, pulse **Descargar código** para descargar el archivo del proyecto.


### Ejecución del proyecto Objective-C en Xcode
{: #run_obj-c}

1. Extraiga el archivo `BasicProject-ObjC.zip`. 

2. Abra el archivo `README.md` en un visor Markdown para ver los pasos a seguir para configurar el proyecto.

   1. Abra el terminar y vaya a la carpeta del proyecto.
   
      1. Ejecute `pod setup` si tiene que configurar el repositorio de CocoaPods.
      
      2. Ejecute `pod update` si tiene que actualizar los pods existentes.
      
      3. Ejecute `pod install` para instalar los pods necesarios para el proyecto.
      
   2. Abra el espacio de trabajo Xcode `BasicProject.xcworkspace`. 
      
3. Ejecute la app.


### Ejecución del proyecto Swift en Xcode
{: #run_swift}

1. Extraiga el archivo `BasicProject-Swift.zip`. 

2. Abra el archivo `README.md` en un visor Markdown para ver los pasos a seguir para configurar el proyecto.

   1. Abra el terminar y vaya a la carpeta del proyecto.
   
      1. Ejecute `pod setup` si tiene que configurar el repositorio de CocoaPods.
      
      2. Ejecute `pod update` si tiene que actualizar los pods existentes.
      
      3. Ejecute `pod install` para instalar los pods necesarios para el proyecto.
      
   3. Abra el espacio de trabajo Xcode `BasicProject.xcworkspace`. 
      
3. Ejecute la app.


### Ejecución del proyecto Cordova en Xcode
{: #run_cordova_xcode}

1. Extraiga el archivo `BasicProject-Cordova.zip`. 

2. Abra el archivo `README.md` en un visor Markdown para configurar el proyecto.

   1. Abra el proyecto `platforms/ios` en Xcode. 
      
3. Ejecute la app.


### Ejecución del proyecto Cordova en Android Studio
{: #run_cordova_studio}

1. Extraiga el archivo `BasicProject-Cordova.zip`. 

2. Abra el archivo `README.md` en un visor Markdown para configurar el proyecto.

   1. Abra el proyecto `platforms/android` en Android Studio.
      
3. Ejecute la app.


### Ejecución del proyecto Android en Android Studio
{: #run_android}

1. Extraiga el archivo `BasicProject-Android.zip`. 

2. Abra el archivo `README.md` en un visor Markdown para configurar el proyecto.

   1. Abra el proyecto `BasicProject-Android` en Android Studio.
      
3. Ejecute la app.


## Qué hacer a continuación
{: #what_next}

Consulte otras guías de aprendizaje.


### Guías de aprendizaje del Iniciador de IU
{: #tutorials_UI}

* [Guía de aprendizaje: Catálogo de almacenamiento](tutorial_store_catalog.html)


### Guías de aprendizaje del Iniciador de código
{: #tutorials_Code}

* [Guía de aprendizaje - {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [Guía de aprendizaje: Lenguaje Watson](tutorial_watson_language.html)
* [Guía de aprendizaje: Weather](tutorial_weather.html)
