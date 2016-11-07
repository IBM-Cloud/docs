---

copyright:
  years: 2016
lastupdated: "2016-10-13"

---
{:new_window: target="_blank"}

# Guía de aprendizaje: Iniciador de código de lenguaje Watson
{: #tutorial_watson_language}

Última actualización: 13 de octubre de 2016
{: .last-updated}

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

2. Opcional: Añada Notificaciones Push.

   1. Pulse **Añadir** para **Notificaciones Push** en la página **Visión general del proyecto**.

      De forma alternativa, puede pulsar **Crear** desde la página **Notificaciones Push**.

   2. Especifique el nombre del servicio y pulse **Crear**.

   3. Para iOS, [configure el Servicio de notificaciones Push de Apple](../services/mobilepush/t_push_provider_ios.html){: new_window}.

   4. Para Android, [configure Google Cloud Messaging](../services/mobilepush/t_push_provider_android.html){: new_window}.

3. Opcional: Añada otros servicios.

   1. Pulse **Añadir** para el servicio en la página **Visión general del proyecto**.

   2. Especifique el nombre del servicio y pulse **Crear**.

   3. Siga las instrucciones del servicio para configurarlo.

4. Descargue el proyecto.

   1. Pulse **Código** y seleccione el lenguaje preferido.

   2. Pulse **Descargar código**.

5. Extraiga el archivado y visualice el archivo `README.md` en un visor Markdown para completar la configuración.


## Qué hacer a continuación
{: #tutorial_next}

[Pruébelo.](http://new-console.{DomainName}/mobile/create-project?starter=512568a1-72db-35c7-b9c4-4f3e3bc89375){: new_window}


# Enlaces relacionados
{: #rellinks}

<!-- links to internal services don't work
## {{site.data.keyword.Bluemix_notm}} Mobile services
{: #general}
* [Mobile Analytics (Beta)](../services/mobileanalytics/index.html){: new_window}
* [Mobile Client Access](../services/mobileaccess/index.html){: new_window}
* [Mobile Foundation](../services/mobilefoundation/index.html){: new_window}
* [Mobile Quality Assurance)](../services/MobileQualityAssurance/index.html){: new_window}
* [Push Notifications](../services/mobilepush/index.html){: new_window}
-->

## Publicaciones del blog
{: #general}
* [Publicación del blog: Introducción del panel de control de Bluemix Mobile](https://developer.ibm.com/bluemix/2016/07/08/new-bluemix-mobile-dashboard/){: new_window}
* [Publicación del blog: Introducción de la siguiente generación del panel de control de Bluemix Mobile](https://ibm.event.ibm.com/blogs/bluemix/2016/10/introducing-the-next-generation-of-the-bluemix-mobile-dashboard/){: new_window}
* [Publicación del blog: Introducción de Bluemix Mobile Code Starters](https://www.ibm.com/blogs/bluemix/2016/10/rapid-dev-with-mobile-code-starters/){: new_window}
* [Publicación del blog: Bluemix Mobile, Parte 1: Creación de una aplicación Store Catalog](https://developer.ibm.com/bluemix/2016/07/13/bluemix-mobile-creating-store-catalog-app-part1/){: new_window}
* [Publicación del blog: Bluemix Mobile, Parte 2: Integración de programa de fondo de Bluemix personalizado en la app Store Catalog](https://developer.ibm.com/bluemix/2016/07/14/bluemix-mobile-integrating-custom-backend-part2/){: new_window}

## Guías de aprendizaje y ejemplos
{: #samples}
* [Backend móvil para Bluemix](https://github.com/ibm-bluemix-mobile-services/mobiledashboard-storecatalog-backend){: new_window}
