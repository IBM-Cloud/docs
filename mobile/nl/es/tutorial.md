---

copyright:
  years: 2016
lastupdated: "2016-10-21"

---
{:new_window: target="_blank"}

# Guía de aprendizaje del iniciador de código de {{site.data.keyword.visualrecognitionshort}}
{: #tutorial}

En la siguiente guía de aprendizaje encontrará los pasos a seguir para crear un proyecto desde el iniciador de código de {{site.data.keyword.visualrecognitionshort}}, incluidas las herramientas que debe tener instaladas y, por lo tanto, los pasos para ejecutar el iniciador en Xcode y Android Studio.


### Instalación de herramientas del desarrollador
{: #dev_tools}

Asegúrese de haber instalado las [herramientas necesarias del desarrollador](get_code.html#prereq-dev-tools){: new_window}.


### Creación de un proyecto desde el iniciador de código de {{site.data.keyword.visualrecognitionshort}}
{: #create_project}

1. Cree un proyecto de panel de control de Mobile en {{site.data.keyword.Bluemix}}.

   1. Desde la página **Guía de inicio** del panel de control de Mobile, pulse **Crear proyecto**.

      De forma alternativa, puede pulsar **Crear proyecto** desde la página **Proyectos**.

   2. Pulse **Iniciadores de código**.

   3. Seleccione **Reconocimiento visual** y pulse **Crear proyecto**.

   4. Especifique el nombre del proyecto. En esta guía de aprendizaje utilizaremos `VisualRecognitionProject`.
   
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
      
   2. Para iOS, pulse **iOS Swift**.
   
   3. Para Android, pulse **Android**.
   
   4. Cuando se haya generado el código, pulse **Descargar código** para descargar el archivo del proyecto. 


### Ejecución del proyecto en Xcode
{: #run_xcode}

1. Extraiga el archivo `VisualRecognitionProject-Swift.zip`. 

2. Abra el archivo `README.md` en un visor Markdown para ver los pasos a seguir para configurar el proyecto. 

   1. Cree su instancia de servicio de [{{site.data.keyword.visualrecognitionshort}}](https://console.{DomainName}/catalog/services/visual-recognition/){: new_window}. 
   
   2. Abra el terminar y vaya a la carpeta del proyecto. 
   
      1. Ejecute `pod setup` si tiene que configurar el repositorio de CocoaPods. 
      
      2. Ejecute `pod update` si tiene que actualizar los pods existentes. 
      
      3. Ejecute `pod install` para instalar los pods necesarios para el proyecto. 
      
      4. Ejecute `carthage update --platform iOS` para crear las dependencias e infraestructura que utilizará el SDK iOS de {{site.data.keyword.ibmwatson}} Developer Cloud. 
      
   3. Abra el espacio de trabajo Xcode `VisualRecognitionProject.xcworkspace`. 
   
   4. Añada las credenciales de servicio de {{site.data.keyword.visualrecognitionshort}}. 
   
      1. Copie el archivo `api_key` de las credenciales de servicio de {{site.data.keyword.visualrecognition}}. 
      
      2. Pegue el archivo `api_key` en la clave `VisualRecognitionAPIKey` en el archivo `WatsonCredentials.plist`. 
      
3. Ejecute la app.


### Ejecución del proyecto en Android Studio
{: #run_studio}

1. Extraiga el archivo `VisualRecognitionProject-Android.zip`. 

2. Abra el archivo `README.md` en un visor Markdown para configurar el proyecto. 

   1. Cree su instancia de servicio de [{{site.data.keyword.visualrecognitionshort}}](https://console.{DomainName}/catalog/services/visual-recognition/){: new_window}. 
   
      Sáltese este paso si ya tiene una instancia de servicio de {{site.data.keyword.visualrecognitionshort}}. 
   
   2. Abra el proyecto `VisualRecognitionProject-Android` en Android Studio.
   
   4. Añada las credenciales de servicio de {{site.data.keyword.visualrecognitionshort}}. 
   
      1. Copie el archivo `api_key` de las credenciales de servicio de {{site.data.keyword.visualrecognition}}. 
      
      2. Pegue el archivo `api_key` en la clave `watson_visual_recognition_api_key` en el archivo `res/values/watson_credentials.xml`. 
      
3. Ejecute la app.


## Qué hacer a continuación
{: #what_next}

Consulte otras guías de aprendizaje. 


### Guías de aprendizaje del Iniciador de IU
{: #tutorials_UI}

* [Guía de aprendizaje: Catálogo de almacenamiento](tutorial_store_catalog.html)


### Guías de aprendizaje del Iniciador de código
{: #tutorials_Code}

* [Guía de aprendizaje: Lenguaje Watson](tutorial_watson_language.html)
* [Guía de aprendizaje: Weather](tutorial_weather.html)
