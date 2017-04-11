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

#Envío por push de la aplicación de inicio a {{site.data.keyword.Bluemix_short}}
{: #pushing_starter_app}


 
Despliegue la aplicación de inicio y aprenda rápidamente a utilizar el servicio
{{site.data.keyword.geospatialshort_Geospatial}}:{:shortdesc}

1. Si aún no lo ha hecho, [instale la herramienta de línea de mandatos cf](docs/starters/install_cli.html).
2. [Obtenga el código](https://hub.jazz.net/project/streamscloud/geo-starter/overview) de la aplicación de inicio {{site.data.keyword.geospatialshort_Geospatial}}. 
3. Renombre el directorio que contiene los archivos de aplicación para que coincida con el nombre que ha asignado a la aplicación en {{site.data.keyword.Bluemix_short}}. Por ejemplo, si la aplicación se denomina myapp, cambie el nombre del directorio myapp.
4. En la línea de mandatos, cambie al directorio renombrado.
<pre><code>cd myapp</code></pre>
5. Conéctese a {{site.data.keyword.Bluemix_short}}:
<pre><code>cf api https://api.DomainName</code></pre>
6. Inicie la sesión en {{site.data.keyword.Bluemix_short}}, establezca la organización de destino cuando se le solicite y despliegue la aplicación.
<pre><code>
cf login
cf push myapp
</code></pre>

##Qué hacer a continuación

* Vaya a la página de visión general de la aplicación, a la que puede acceder desde el panel de control de {{site.data.keyword.Bluemix_short}}, para comprobar que la aplicación se ha iniciado correctamente.
* Inicie la aplicación para verla en el navegador. Encontrará el URL de la aplicación (o "route") en la página de visión general de la aplicación. La página web de la aplicación de ejemplo muestra información sobre el estado de las llamadas a la API REST en el código de la aplicación y los sucesos que {{site.data.keyword.geospatialshort_Geospatial}} detecta.
