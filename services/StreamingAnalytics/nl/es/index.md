---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-13"

---

<!-- Attribute definitions -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Iniciación a {{site.data.keyword.streaminganalyticsshort}}
{: #gettingstarted}

{{site.data.keyword.streaminganalyticsshort}} está basado en {{site.data.keyword.streamsshort}}, una plataforma analítica avanzada que se puede utilizar para introducir, analizar y correlacionar información a medida que llega desde distintos tipos de orígenes de datos en tiempo real. Cuando se crea una instancia del servicio {{site.data.keyword.streaminganalyticsshort}}, se obtiene una instancia propia de {{site.data.keyword.streamsshort}} que se ejecuta en la nube de {{site.data.keyword.Bluemix_short}}, lista para ejecutarse en las aplicaciones de {{site.data.keyword.streamsshort}}.
{:shortdesc}

Puede empezar a utilizar {{site.data.keyword.streaminganalyticsshort}} directamente ejecutando las [aplicaciones de inicio](/docs/services/StreamingAnalytics/c_starterapps.html){:new_window}. 

Para empezar a utilizar {{site.data.keyword.streaminganalyticsshort}}, siga uno de estos métodos para enviar el paquete de aplicaciones (archivo .sab) asociado con la aplicación SPL, Java™, Python o Scala Streams: 
* Utilice el botón **Enviar trabajo** de la consola de {{site.data.keyword.streaminganalyticsshort}}.
* Desarrolle una aplicación {{site.data.keyword.Bluemix_short}} y añádale la aplicación {{site.data.keyword.streamsshort}}. Contrólela utilizando la [API REST de {{site.data.keyword.streaminganalyticsshort}}](https://console.ng.bluemix.net/apidocs/220).


Utilice {{site.data.keyword.streaminganalyticsshort}} con otros servicios de {{site.data.keyword.Bluemix_short}}, incluidos {{site.data.keyword.cloudant}} y {{site.data.keyword.messagehub}}. Consulte las [Guías de aprendizaje para la integración con otros servicios de {{site.data.keyword.Bluemix_short}}](/docs/services/StreamingAnalytics/r_integrating_cloudant_rest.html){:new_window} para ver ejemplos que le ayuden a empezar.

Si desea profundizar en el uso de sus propias aplicaciones, puede obtener un entorno de desarrollo de {{site.data.keyword.streamsshort}} y debe preparar su aplicación para la nube. Si no dispone de un entorno de {{site.data.keyword.streamsshort}}, puede descargar {{site.data.keyword.streamsshort}} Quick Start Edition, de forma gratuita desde la [página del producto {{site.data.keyword.streamsshort}}.](https://www.ibm.com/analytics/us/en/technology/stream-computing/#products)

Si no está familiarizado con el desarrollo de aplicaciones {{site.data.keyword.streamsshort}}, hay recursos que le pueden ayudar. Para obtener más información, consulte [{{site.data.keyword.streamsshort}} Knowledge Center.](https://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window}

Si ya tiene una aplicación SPL que se ejecuta localmente, [prepare la aplicación para la nube.](https://developer.ibm.com/streamsdev/docs/getting-spl-application-ready-cloud/){:new_window}

**Nota:** Debe compilar sus aplicaciones en un sistema operativo Red Hat Enterprise Linux (RHEL) 6.5 o una versión de CentOS equivalente utilizando procesadores Intel. 

## Apps {{site.data.keyword.streamsshort}} Python para {{site.data.keyword.streaminganalyticsshort}}
{: #gettingstarted_py notoc}

Ahora puede crear apps Streams en un entorno Python, como IBM Data Science Experience (DSX), y enviar estas a la instancia de {{site.data.keyword.streaminganalyticsshort}} para que se desplieguen en la nube de Bluemix. Ya no necesita instalar {{site.data.keyword.streamsshort}} de forma local para compilar y desplegar una app Streams Python. 

Comience a crear apps Streams Python de ejemplo utilizando cuadernos Jupyter en DSX y envíe estas apps a la instancia del servicio directamente desde DSX. Para obtener más información, consulte el apartado sobre [Desarrollo de apps Streams Python en DSX](/docs/services/StreamingAnalytics/t_develop_apps_python.html#t_develop_python_dsx).

{{site.data.keyword.streaminganalyticsshort}} también da soporte al despliegue de apps Streams desde su entorno Python local. Debe utilizar la [API de la aplicación {{site.data.keyword.streamsshort}} Python](http://ibmstreams.github.io/streamsx.documentation/docs/python/python-appapi-devguide/#50-api-features), que se incluye en el paquete streamsx, para desarrollar sus apps Streams Python localmente y enviarlas a la instancia del servicio. Para empezar, siga los pasos de la guía de aprendizaje [Desarrollo para el servicio {{site.data.keyword.streaminganalyticsshort}}](http://ibmstreams.github.io/streamsx.documentation/docs/python/1.6/python-appapi-devguide-2a/index.html). 
