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

#Despliegue de aplicaciones de {{site.data.keyword.streamsshort}} en la nube
{: #t_deploytocloud}

Puede desplegar sus aplicaciones de {{site.data.keyword.streamsshort}} en una instancia de {{site.data.keyword.streaminganalyticsshort}} que se ejecute en la nube {{site.data.keyword.Bluemix_short}}.
{:shortdesc}

Las aplicaciones de {{site.data.keyword.streamsshort}} se escriben en {{site.data.keyword.streamsshort}} Processing Language (SPL) en un entorno {{site.data.keyword.streamsshort}}. {{site.data.keyword.streamsshort}} también soporta varios kits de desarrollo de Java™ que se pueden utilizar para desarrollar las aplicaciones. Para obtener más información sobre el soporte Java en {{site.data.keyword.streamsshort}}, consulte [Kits de desarrollo Java soportados para el desarrollo de aplicaciones](https://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-prerequisites-java-supported-sdks.html){:new_window}. 
{{site.data.keyword.streaminganalyticsshort}} no incluye ningún entorno de desarrollo de {{site.data.keyword.streamsshort}} en la nube, pero puede desplegar las aplicaciones que desarrolle localmente en la nube.

Antes de empezar, inhabilite el bloqueador de ventanas emergentes del navegador para visualizar la consola de Streaming Analytics.

Para desplegar las aplicaciones de {{site.data.keyword.streamsshort}} en la nube:

1. Configure un entorno de {{site.data.keyword.streamsshort}} para desarrollar y probar la aplicación. 

	Si no dispone del entorno de desarrollo de {{site.data.keyword.streamsshort}}, puede descargar {{site.data.keyword.streamsshort}} Quick Start Edition, de forma gratuita. Vaya a la [página del producto IBM Streams](http://www.ibm.com/analytics/us/en/technology/stream-computing/){:new_window} y pulse **Descargar la instalación de software nativa**.

2. Desarrolle su aplicación SPL o Java en su entorno de {{site.data.keyword.streamsshort}} utilizando Streams Studio o las herramientas de las líneas de mandato.
3. Compruebe que la aplicación SPL o Java se ejecute correctamente en el entorno de desarrollo.
4. Envíe el paquete de aplicaciones (archivo .sab) asociado con la aplicación SPL o Java a su instancia de servicio en la nube utilizando uno de los siguientes métodos:
	* Utilice la consola {{site.data.keyword.streaminganalyticsshort}} para enviar el paquete de aplicaciones.
    * Desarrolle una aplicación {{site.data.keyword.Bluemix_short}} y añádale la aplicación {{site.data.keyword.streamsshort}}. Contrólela utilizando la API REST de {{site.data.keyword.streaminganalyticsshort}}.

Ahora su aplicación está desplegada en la nube. Puede supervisar su aplicación utilizando el servicio de {{site.data.keyword.streaminganalyticsshort}}. También puede enviar más de una aplicación SPL o Java (archivos .sab) a su instancia de servicio. Puede enviar tantas aplicaciones como desee.
