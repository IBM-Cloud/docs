---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


#Iniciación a {{site.data.keyword.streaminganalyticsshort}}
{: #gettingstarted}

{{site.data.keyword.streaminganalyticsshort}} está basado en {{site.data.keyword.streamsshort}}, una plataforma analítica avanzada que se puede utilizar para introducir, analizar y correlacionar información a medida que llega desde distintos tipos de orígenes de datos en tiempo real. Cuando se crea una instancia del servicio {{site.data.keyword.streaminganalyticsshort}}, se obtiene una instancia propia de {{site.data.keyword.streamsshort}} que se ejecuta en la nube de {{site.data.keyword.Bluemix_short}}, lista para ejecutarse en las aplicaciones de {{site.data.keyword.streamsshort}}.
{:shortdesc}

Puede desplegar sus aplicaciones en una instancia de {{site.data.keyword.streaminganalyticsshort}} que se ejecute en la nube {{site.data.keyword.Bluemix_short}}.

Puede empezar a utilizar {{site.data.keyword.streaminganalyticsshort}} directamente ejecutando las [aplicaciones de inicio](/docs/services/StreamingAnalytics/c_starterapps.html){:new_window}. Si desea profundizar en el uso de sus propias aplicaciones, es necesario un entorno de desarrollo de {{site.data.keyword.streamsshort}} y preparar su SPL para la nube.

Para empezar a utilizar {{site.data.keyword.streaminganalyticsshort}}, siga uno de estos métodos para enviar el paquete de aplicaciones (archivo .sab) asociado con la aplicación SPL o Java™:
* Utilice la consola de {{site.data.keyword.streaminganalyticsshort}}.
* Desarrolle una aplicación {{site.data.keyword.Bluemix_short}} y añádale la aplicación {{site.data.keyword.streamsshort}}. Contrólela utilizando la [API REST de {{site.data.keyword.streaminganalyticsshort}}](https://console.ng.bluemix.net/apidocs/220). Compruebe que la aplicación SPL o Java se ejecute correctamente en el entorno de desarrollo.

Ahora puede utilizar {{site.data.keyword.streaminganalyticsshort}} con otros servicios de {{site.data.keyword.Bluemix_short}}, incluidos {{site.data.keyword.cloudant}} y {{site.data.keyword.messagehub}}. Consulte las [Guías de aprendizaje para la integración con otros servicios de {{site.data.keyword.Bluemix_short}}](/docs/services/StreamingAnalytics/r_integrating_cloudant_rest.html){:new_window} para ver ejemplos que le ayuden a empezar.

Para desarrollar una aplicación {{site.data.keyword.streamsshort}} debe disponer de un entorno de desarrollo de {{site.data.keyword.streamsshort}}. Si no dispone de un entorno de {{site.data.keyword.streamsshort}}, puede descargar {{site.data.keyword.streamsshort}} Quick Start Edition, de forma gratuita desde la [página del producto {{site.data.keyword.streamsshort}}.](https://www.ibm.com/analytics/us/en/technology/stream-computing/#products)

Si no está familiarizado con el desarrollo de aplicaciones {{site.data.keyword.streamsshort}}, hay recursos que le pueden ayudar. Para obtener más información, consulte [{{site.data.keyword.streamsshort}} Knowledge Center.](https://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window}

Si ya tiene una aplicación SPL que se ejecuta localmente, [prepare la aplicación para la nube.](https://developer.ibm.com/streamsdev/docs/getting-spl-application-ready-cloud/){:new_window}

# Enlaces relacionados
{: #rellinks}

## Guías de aprendizaje y ejemplos
{: #samples}
* [Introducción a {{site.data.keyword.streaminganalyticsshort}}](https://developer.ibm.com/streamsdev/docs/streaming-analytics-now-available-bluemix){:new_window}
* [Aplicación de inicio {{site.data.keyword.streaminganalyticsshort}} SDK for Node.js™](http://bit.ly/1iR1bzu){:new_window}
* [Aplicación de inicio {{site.data.keyword.streaminganalyticsshort}} Liberty for Java™](https://developer.ibm.com/streamsdev/docs/bluemix-streaming-analytics-starter-application/){:new_window}
* [Preparación de la aplicación SPL para la nube](https://developer.ibm.com/streamsdev/docs/getting-spl-application-ready-cloud){:new_window}
* [Guía de desarrollo de Bluemix {{site.data.keyword.streaminganalyticsshort}}](https://developer.ibm.com/streamsdev/docs/bluemix-streaming-analytics-development-guide/){:new_window}
* [Más guías de aprendizaje](StreamingAnalytics.html#r_integrating_cloudant_rest){:new_window}


## Referencia de la API
{: #api}
* [{{site.data.keyword.streaminganalyticsshort}} API REST](https://console.ng.bluemix.net/apidocs/220){:new_window}
* [Métricas de {{site.data.keyword.streaminganalyticsshort}} mediante la API REST de {{site.data.keyword.streamsshort}}](https://developer.ibm.com/bluemix/2016/07/25/streaming-analytics-metrics-using-rest-api/){:new_window}

## Entornos de tiempo de ejecución compatibles
{: #buildpacks}
* [Liberty for Java](/docs/runtimes/liberty/index.html#liberty)
* [Node.js](/docs/runtimes/nodejs/index.html#nodejs)

## Enlaces relacionados
{: #general}
* [Documentación de {{site.data.keyword.streamsshort}}](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window}
* [{{site.data.keyword.streamsshort}}Quick
Start Edition](http://www.ibm.com/analytics/us/en/technology/stream-computing/){:new_window}
