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

# Guía de aprendizaje del iniciador de código de Cloudant Sync
{: #tutorial}

En la siguiente guía de aprendizaje encontrará los pasos a seguir para crear un proyecto desde el iniciador de código de Cloudant Sync, incluidas las herramientas que debe tener instaladas y, por lo tanto, los pasos para ejecutar el iniciador en Android Studio.


### Instalación de herramientas del desarrollador
{: #dev_tools}

Asegúrese de haber instalado las [herramientas de desarrollador necesarias ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](get_code.html#prereq-dev-tools "icono de enlace externo"){: new_window}.


### Creación de un proyecto desde el iniciador de código de Cloudant Sync 
{: #create_project}

1. Cree un proyecto de panel de control de Mobile en {{site.data.keyword.Bluemix}}.

   1. Desde la página **Guía de inicio** del panel de control de Mobile, pulse **Crear proyecto**.

      De forma alternativa, puede pulsar **Crear proyecto** desde la página **Proyectos**.

   2. Pulse **Iniciadores de código**.

   3. Seleccione **Cloudant Sync** y pulse **Crear proyecto**.

   4. Especifique el nombre del proyecto. En esta guía de aprendizaje utilizaremos `CloudantSyncProject`.
   
   5. Pulse **Crear**.

2. Añada capacidad de datos. Puede crear una nueva instancia del servicio {{site.data.keyword.cloudant}} o añadir una instancia del servicio existente. 

   1. Pulse **Ver** en el mosaico **Datos** de la página **Visión general del proyecto**. 

      Como alternativa, puede pulsar **Crear** o **Añadir existente** y luego **Base de datos Cloudant NoSQL** en la página **Datos**. 
      
   2. Opcional: si ha elegido crear una nueva instancia de servicio, escriba el nombre del servicio y pulse **Crear**.

   3. Opcional: si ha elegido añadir una instancia de servicio existente, seleccione la instancia del servicio en la lista y pulse **Añadir existente**.

   4. Pulse el icono **Menú** en el mosaico de servicios y seleccione **Iniciar...** para iniciar la instancia de servicio. 

      1. Pulse **INICIAR** para iniciar la consola de {{site.data.keyword.cloudant}}. 

      2. Pulse **Crear base de datos**, escriba el nombre de la base de datos y pulse **Crear**.

      3. Pulse el icono **+** que hay junto a **Todos los documentos** para añadir documentos. 

3. Opcional: Añada la función de {{site.data.keyword.mobilepushshort}}. 

   1. Pulse **Añadir** para **{{site.data.keyword.mobilepushshort}}** en la página **Visión general del proyecto**.

      De forma alternativa, puede pulsar **Crear** desde la página **{{site.data.keyword.mobilepushshort}}**. 

   2. Especifique el nombre del servicio y pulse **Crear**.

   3. Para Android, [configure Firebase Cloud Messaging ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](/docs/services/mobilepush/t_push_provider_android.html "icono de enlace externo"){: new_window}.
   
4. Opcional: Añada capacidad de análisis.

   1. Pulse **Añadir** para **Análisis** en la página **Visión general del proyecto**.

      De forma alternativa, puede pulsar **Crear** desde la página **Análisis**.

   2. Especifique el nombre del servicio y pulse **Crear**.
   
   3. Desactive la **Modalidad de demostración** para ver los datos del análisis después de ejecutar la app.
   
   4. Consulte [Iniciación a {{site.data.keyword.mobileanalytics_short}} ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](/docs/services/mobileanalytics/index.html "icono de enlace externo"){: new_window} para obtener más información sobre cómo configurar Analytics.
  
5. Opcional: Añada capacidad de autenticación.

   1. Pulse **Añadir** para **Autenticación** en la página **Visión general del proyecto**.

      De forma alternativa, puede seleccionar **Crear** en la página **Autenticación**.

   2. Especifique el nombre del servicio y pulse **Crear**.
   
   3. Active **Autenticación**.
   
   4. Seleccione su proveedor de identidad y especifique la información necesaria para configurarlo. Solo puede habilitar un proveedor de identidad.

   5. Consulte [Iniciación a {{site.data.keyword.amashort}} ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](/docs/services/mobileaccess/index.html "icono de enlace externo"){: new_window} para obtener más información sobre cómo configurar la autenticación. 

6. Genere el código del proyecto.

   1. Pulse **Obtener código** en la página **Visión general del proyecto** para seleccionar la plataforma y el lenguaje.
   
      Como alternativa, pulse la página **Código**.
      
   2. Para Android, pulse **Android**.
   
   3. Cuando se haya generado el código, pulse **Descargar código** para descargar el archivo del proyecto.


### Ejecución del proyecto Android en Android Studio
{: #run_android}

1. Extraiga el archivo `CloudantSyncProject-Android.zip`. 

2. Abra el archivo `README.md` en un visor Markdown para configurar el proyecto.

   1. Abra el proyecto `CloudantSyncProject-Android` en Android Studio.

   2. Añada las credenciales de Cloudant. 

      1. En la página **Datos**, pulse el icono **Menú** en el mosaico de servicios y seleccione **Iniciar...** para iniciar la instancia de servicio. 

         1. Pulse **INICIAR** para iniciar la consola de {{site.data.keyword.cloudant}}. 

         2. Pulse el nombre de la base de datos y pulse **Permisos**.

         3. Escriba el nombre de la base de datos en la serie `cloudant_dbname` del archivo `res/values/cloudant_credentials.xml`. 

         4. Pulse **Generar clave de API**.

             1. Copie el valor **Clave** y péguelo en la serie `cloudant_api_key` del archivo `res/values/cloudant_credentials.xml`. 

             2. Copie el valor **Contraseña** y péguelo en la serie `cloudant_api_password` del archivo `res/values/cloudant_credentials.xml`. 

             3. Seleccione el permiso **_admin**. 
      
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
* [Guía de aprendizaje: {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [Guía de aprendizaje: {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [Guía de aprendizaje: Lenguaje Watson](tutorial_watson_language.html)
* [Guía de aprendizaje: Weather](tutorial_weather.html)
