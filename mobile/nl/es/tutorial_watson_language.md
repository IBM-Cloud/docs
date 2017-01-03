---

copyright:
  years: 2016
lastupdated: "2016-10-21"

---
{:new_window: target="_blank"}

# Guía de aprendizaje: Iniciador de código de lenguaje Watson
{: #tutorial_watson_language}

El Iniciador de código de {{site.data.keyword.Bluemix}} Mobile para el lenguaje Watson muestra los servicios de Text To Speech y de Language Translation de Watson y le proporciona los puntos de integración para cada uno de los servicios de {{site.data.keyword.Bluemix_notm}} Mobile.


## Requisitos
{: #tutorial_requirements}

* Una cuenta de [Bluemix](http://bluemix.net)
* Instancias de servicio de [Language Translator](https://console.{DomainName}/catalog/services/language-translator/) y [Text to Speech](https://console.{DomainName}/catalog/services/text-to-speech/) obtenidas desde el [Catálogo de Bluemix](https://console.{DomainName}/catalog/)


## Guía de inicio
{: #tutorial_gs}

Para comenzar a utilizar rápidamente el Iniciador de código de lenguaje Watson, siga estos pasos:

1. Cree un proyecto de panel de control de Mobile en {{site.data.keyword.Bluemix_notm}}.

   1. Desde la página **Guía de inicio** del panel de control de Mobile, pulse **Crear proyecto**.

      De forma alternativa, puede pulsar **Crear proyecto** desde la página **Proyectos**.

   2. Pulse **Iniciadores de código**.

   3. Seleccione **Lenguaje Watson** y pulse **Crear proyecto**.

   4. Especifique el nombre de proyecto y pulse **Crear**.

2. Opcional: Añada capacidad de notificaciones Push.

   1. Pulse **Añadir** para **Notificaciones Push** en la página **Visión general del proyecto**.

      De forma alternativa, puede pulsar **Crear** desde la página **Notificaciones Push**.

   2. Especifique el nombre del servicio y pulse **Crear**.

   3. Para iOS, [configure el Servicio de notificaciones Push de Apple](/docs/services/mobilepush/t_push_provider_ios.html){: new_window}.

   4. Para Android, [configure Google Cloud Messaging](/docs/services/mobilepush/t_push_provider_android.html){: new_window}.
   
3. Opcional: Añada capacidad de análisis.

   1. Pulse **Añadir** para **Análisis** en la página **Visión general del proyecto**.

      De forma alternativa, puede pulsar **Crear** desde la página **Análisis**.

   2. Especifique el nombre del servicio y pulse **Crear**.
   
   3. Desactive la **Modalidad de demostración** para ver los datos del análisis después de ejecutar la app.

4. Opcional: Añada capacidad de autenticación.

   1. Pulse **Añadir** para **Autenticación** en la página **Visión general del proyecto**.

      De forma alternativa, puede seleccionar **Crear** en la página **Autenticación**.

   2. Especifique el nombre del servicio y pulse **Crear**.
   
   3. Active **Autenticación**.
   
   4. Seleccione su proveedor de identidad y especifique la información necesaria para configurarlo. Solo puede habilitar un proveedor de identidad.

   5. Consulte [Iniciación a Mobile Client Access](/docs/services/mobileaccess/index.html){: new_window} para obtener más información sobre cómo configurar la autenticación.

5. Descargue el proyecto.

   1. Pulse **Código** y seleccione el lenguaje preferido.

   2. Pulse **Descargar código**.

6. Extraiga el archivado y visualice el archivo `README.md` en un visor Markdown para completar la configuración.


## Qué hacer a continuación
{: #tutorial_next}

[Pruébelo.](http://console.{DomainName}/mobile/create-project?starter=512568a1-72db-35c7-b9c4-4f3e3bc89375){: new_window}
