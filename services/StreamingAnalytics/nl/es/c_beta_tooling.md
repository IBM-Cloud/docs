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

#Herramientas de desarrollo y entorno
{: #c_beta_tooling}


Estas consideraciones se aplican a las herramientas y al entorno que se utiliza para desarrollar aplicaciones para {{site.data.keyword.streaminganalyticsshort}}.
{:shortdesc}


* {{site.data.keyword.streaminganalyticsshort}} no incluye ningún entorno de desarrollo de {{site.data.keyword.streamsshort}} en la nube o en Streams Studio en la nube. Desarrolle las aplicaciones en un entorno {{site.data.keyword.streamsshort}} localmente y envíelas como paquetes de aplicaciones. Si no dispone del entorno de desarrollo, puede descargar {{site.data.keyword.streamsshort}} Quick Start Edition, de forma gratuita desde la página del producto [{{site.data.keyword.streamsshort}}](https://www.ibm.com/analytics/us/en/technology/stream-computing/#products).
* Compile el paquete de aplicación en un entorno Red Hat Enterprise Linux 6.5, o una versión de CentOS equivalente, para garantizar la compatibilidad.
* En el entorno de desarrollo de {{site.data.keyword.streamsshort}}, defina la variable de entorno `JAVA_HOME` en $STREAMS_INSTALL/java.
