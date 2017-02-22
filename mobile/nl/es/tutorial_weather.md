---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}

# Guía de aprendizaje: Iniciador de código de Weather
{: #tutorial_weather}

El Iniciador de código de {{site.data.keyword.Bluemix}} Mobile para Weather muestra un proyecto de aprendizaje para comenzar a trabajar con Weather, utilizando Swift e incluye puntos de integración de Push y Analytics.


## Requisitos
{: #tutorial_requirements}

* Una cuenta de [Bluemix ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](http://bluemix.net "icono de enlace externo")
* Una instancia de servicio de [Weather Company Data ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](https://console.{DomainName}/catalog/services/weather-company-data/ "icono de enlace externo") obtenida del [Catálogo de Bluemix ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](https://console.{DomainName}/catalog/ "icono de enlace externo")


## Guía de inicio
{: #tutorial_gs}

Para comenzar a utilizar rápidamente el Iniciador de código de Weather, siga estos pasos:

1. Cree un proyecto de panel de control de Mobile en {{site.data.keyword.Bluemix_notm}}.

   1. Desde la página **Guía de inicio** del panel de control de Mobile, pulse **Crear proyecto**.

      De forma alternativa, puede pulsar **Nuevo proyecto** desde la página **Proyectos**.

   2. Pulse **Iniciadores de código**.

   3. Seleccione **Weather** y pulse **Crear proyecto**.

   4. Especifique el nombre de proyecto y pulse **Crear**.

2. Opcional: Añada la función de {{site.data.keyword.mobilepushshort}}. 

   1. Pulse **Añadir** para **{{site.data.keyword.mobilepushshort}}** en la página **Visión general del proyecto**.

      De forma alternativa, puede pulsar **Crear** desde la página **{{site.data.keyword.mobilepushshort}}**. 

   2. Especifique el nombre del servicio y pulse **Crear**.

   3. Para iOS, [configure el servicio de notificación Push de Apple ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](/docs/services/mobilepush/t_push_provider_ios.html "icono de enlace externo"){: new_window}.

   4. Para Android, [configure Google Cloud Messaging ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](/docs/services/mobilepush/t_push_provider_android.html "icono de enlace externo"){: new_window}.
   
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

   5. Consulte [Iniciación a Mobile Client Access ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](/docs/services/mobileaccess/index.html "icono de enlace externo"){: new_window} para obtener más información sobre cómo configurar la autenticación. 

5. Descargue el proyecto.

   1. Pulse **Código** y seleccione el lenguaje preferido.

   2. Pulse **Descargar código**.

5. Extraiga el archivado y siga las instrucciones del archivo `README.md`.


## Qué hacer a continuación
{: #tutorial_next}

[¡Pruébelo!![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](http://console.{DomainName}/mobile/create-project?starter=fad1d49e-f7b6-3aff-9b53-14673fca4399 "icono de enlace externo"){: new_window}


### Guías de aprendizaje del Iniciador de IU
{: #tutorials_UI}

* [Guía de aprendizaje: Catálogo de almacenamiento](tutorial_store_catalog.html)


### Guías de aprendizaje del Iniciador de código
{: #tutorials_Code}

* [Guía de aprendizaje: Basic](tutorial.html)
* [Guía de aprendizaje: Cloudant Sync](tutorial_cloudant_synd.html)
* [Guía de aprendizaje: {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [Guía de aprendizaje: {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [Guía de aprendizaje: Lenguaje Watson](tutorial_watson_language.html)
