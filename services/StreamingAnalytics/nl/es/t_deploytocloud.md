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

# Despliegue de aplicaciones de {{site.data.keyword.streamsshort}} en la nube
{: #t_deploytocloud}

Puede desplegar sus aplicaciones de {{site.data.keyword.streamsshort}} en una instancia de {{site.data.keyword.streaminganalyticsshort}} que se ejecute en la nube {{site.data.keyword.Bluemix_short}}.
{:shortdesc}

Las aplicaciones de {{site.data.keyword.streamsshort}} se escriben en {{site.data.keyword.streamsshort}} Processing Language (SPL), SPL, Java, Scala o Python en un entorno {{site.data.keyword.streamsshort}}. Ahora puede desarrollar aplicaciones Streams Python sin un entorno {{site.data.keyword.streamsshort}}. Consulte el apartado sobre [Desarrollo de aplicaciones {{site.data.keyword.streamsshort}} Python para la nube](docs/services/StreamingAnalytics/t_deploytocloud.html#t_deploypython)


{{site.data.keyword.streaminganalyticsshort}} no incluye ningún entorno de desarrollo de {{site.data.keyword.streamsshort}} en la nube, pero puede desplegar las aplicaciones que desarrolle localmente en la nube.

Antes de empezar, inhabilite el bloqueador de ventanas emergentes del navegador para visualizar la consola de {{site.data.keyword.streaminganalyticsshort}}. 

Para desplegar las aplicaciones de {{site.data.keyword.streamsshort}} en la nube:

1. Configure un entorno de desarrollo para desarrollar y probar la aplicación.

	Si desea utilizar un entorno {{site.data.keyword.streamsshort}}, puede descargar {{site.data.keyword.streamsshort}} Quick Start Edition de forma gratuita. Vaya a la [página del producto IBM Streams](http://www.ibm.com/analytics/us/en/technology/stream-computing/){:new_window} y pulse **Descargar la instalación de software nativa**.

2. Desarrolle su aplicación de streaming en el entorno de desarrollo. En el entorno de desarrollo {{site.data.keyword.streamsshort}}, puede utilizar Streams Studio o herramientas de línea de mandatos para desarrollar su aplicación. 

3. Compruebe que la aplicación de streaming se ejecute correctamente en el entorno de aplicación. **Nota:** Debe compilar su aplicación en un sistema operativo Red Hat Enterprise Linux (RHEL) 6.5 o una versión de CentOS equivalente utilizando procesadores Intel. 

4. Envíe el paquete de aplicaciones (archivo .sab) asociado con la aplicación SPL, Java, Scala o Python a su instancia de servicio en la nube utilizando uno de los siguientes métodos:
	* Utilice la consola {{site.data.keyword.streaminganalyticsshort}} para enviar el paquete de aplicaciones.
  * Cree una aplicación {{site.data.keyword.Bluemix_short}} y añádale la aplicación {{site.data.keyword.streamsshort}}. Contrólela utilizando la API REST de {{site.data.keyword.streaminganalyticsshort}}.

Ahora su aplicación está desplegada en la nube. Puede supervisar su aplicación utilizando el servicio de {{site.data.keyword.streaminganalyticsshort}}. También puede enviar más de una aplicación (archivos .sab) a su instancia de servicio. Puede enviar tantas aplicaciones como desee.

{{site.data.keyword.streamsshort}} también soporta varios kits de desarrollo de Java™ que se pueden utilizar para desarrollar las aplicaciones. Para obtener más información sobre el soporte Java en {{site.data.keyword.streamsshort}}, consulte [Kits de desarrollo Java soportados para el desarrollo de aplicaciones](https://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-prerequisites-java-supported-sdks.html){:new_window}.

## Despliegue de aplicaciones de {{site.data.keyword.streamsshort}} Python en la nube
{: #t_deploypython}

Despliegue sus aplicaciones {{site.data.keyword.streamsshort}} Python en un servicio {{site.data.keyword.streaminganalyticsshort}} que se ejecute en la nube {{site.data.keyword.Bluemix_short}}.
No es necesario que disponga de una instalación de {{site.data.keyword.streamsshort}}.
{:shortdesc}

La [API de la aplicación {{site.data.keyword.streamsshort}} Python](http://ibmstreams.github.io/streamsx.documentation/docs/python/python-appapi-devguide/#50-api-features), que se incluye en el paquete streamsx, le permite desplegar sus aplicaciones Python en el servicio {{site.data.keyword.streaminganalyticsshort}}. Consulte la guía de aprendizaje [Desarrollo para el servicio {{site.data.keyword.streaminganalyticsshort}}](http://ibmstreams.github.io/streamsx.documentation/docs/python/1.6/python-appapi-devguide-2a/index.html) para ver un ejemplo de cómo crear y desplegar una aplicación Python sencilla para el servicio {{site.data.keyword.streaminganalyticsshort}}. 

IBM Data Science Experience (DSX) también permite el envío de aplicaciones Python en cuadernos interactivos Jupyter. Para obtener más información, consulte el tema sobre [Desarrollo de aplicaciones Python para {{site.data.keyword.streaminganalyticsshort}}](/docs/services/StreamingAnalytics/t_develop_apps_python.html).
