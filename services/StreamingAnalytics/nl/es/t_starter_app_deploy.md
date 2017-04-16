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

# Despliegue de aplicaciones de inicio en {{site.data.keyword.Bluemix_short}}
{: #starterapps_deploy}

Puede enviar y desplegar una de las aplicaciones de inicio de {{site.data.keyword.streaminganalyticsshort}} en la nube de {{site.data.keyword.Bluemix_short}}.
{:shortdesc}

Antes de empezar, prepare {{site.data.keyword.Bluemix_short}} para desplegar las aplicaciones de inicio de {{site.data.keyword.streaminganalyticsshort}}:

* [Instale la herramienta de línea de mandatos cf](https://github.com/cloudfoundry/cli/releases).
* Cree una aplicación en {{site.data.keyword.Bluemix_short}}, añada el servicio de {{site.data.keyword.streaminganalyticsshort}} a la aplicación y vuelva a transferir la aplicación:
	* Para desplegar la app de inicio Detección de suceso, cree una aplicación con el tiempo de ejecución de {{site.data.keyword.sdk4node}}.
	* Para desplegar la app de inicio Tráfico en Nueva York, cree una aplicación con el tiempo de ejecución de Liberty for Java™.

Recuerde el nombre que asigna a la aplicación; lo necesitará más adelante.

{{site.data.keyword.streaminganalyticsshort}} proporciona dos aplicaciones de ejemplo para que empiece a utilizar el servicio. 

La aplicación de inicio Detección de suceso analiza los datos relacionados con el tiempo en una secuencia en tiempo real y muestra el estado y los resultados del análisis. La aplicación se escribe en {{site.data.keyword.sdk4node}}. Para obtener más información sobre cómo utilizar la app de inicio Detección de suceso, consulte [Detección de sucesos complejos en una secuencia de datos en tiempo real](https://www.ibm.com/developerworks/library/ba-bluemix-detect-complex-events-from-data-stream-trs/index.html).

La aplicación de inicio Tráfico en Nueva York lee y analiza datos de tráfico desde un sitio web público. La aplicación se escribe en Liberty for Java™. Para obtener más información sobre cómo utilizar la app de inicio Tráfico en Nueva York, consulte [Aplicación de inicio de {{site.data.keyword.streaminganalyticsfull}}](https://developer.ibm.com/streamsdev/docs/bluemix-streaming-analytics-starter-application/). 

Para descargar y desplegar la aplicación de inicio en {{site.data.keyword.Bluemix_short}}:

1. Descargue la aplicación de inicio [Detección de suceso](https://hub.jazz.net/project/streamscloud/EventDetection/overview) o [Tráfico en Nueva York](https://hub.jazz.net/project/streamscloud/NYCTraffic/overview).
2. En la línea de mandatos, vaya al directorio del proyecto.
  <pre><code>cd myapp</code></pre>
 
3. Renombre el directorio del proyecto para que coincida con el nombre asignado a la aplicación en {{site.data.keyword.Bluemix_short}}.
4. Conéctese a {{site.data.keyword.Bluemix_short}}:
  <pre><code>cf api https://api.DomainName</code></pre>
   
5. Inicie sesión en {{site.data.keyword.Bluemix_short}} y defina la organización de destino cuando se solicite:
   <pre><code>cf login</code></pre>
    
6. Despliegue la aplicación:
  <pre><code>cf push myapp</code></pre>
   
7. Vaya a la página de visión general de la aplicación, a la que puede acceder desde el panel de control de {{site.data.keyword.Bluemix_short}}, para comprobar que la aplicación se ha iniciado correctamente.
8. Inicie la aplicación para verla en el navegador. Encontrará el URL de la aplicación (o "ruta") en la página de visión general de la aplicación.

Ahora que la app se está ejecutando, puede ir al panel de control del servicio para ver el estado de la instancia de {{site.data.keyword.streaminganalyticsshort}} y para obtener información para la resolución de problemas. Para acceder al panel de control del servicio, vaya al panel de control de {{site.data.keyword.Bluemix_short}} y haga clic en el mosaico {{site.data.keyword.streaminganalyticsshort}} de la página de visión general de la aplicación.
