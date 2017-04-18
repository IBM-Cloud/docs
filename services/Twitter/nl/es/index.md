---

copyright:
  years: 2016
lastupdated: "2016-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Iniciación a Insights for Twitter {: #insights_twitter_overview}

Utilice
{{site.data.keyword.twitterfull}}
para incorporar contenido de Twitter procedente de flujos
[Decahose](http://support.gnip.com/gnip2.0/){: new_window} o [PowerTrack](http://support.gnip.com/apis/powertrack2.0/){: new_window} a las aplicaciones {{site.data.keyword.Bluemix}}.
{:shortdesc}

Para empezar a utilizar {{site.data.keyword.twittershort}}, primero cree la aplicación web de  Bluemix con un tiempo de ejecución como Liberty for Java y, a continuación, añada el servicio {{site.data.keyword.twittershort}} a la app. Cuando el servicio de {{site.data.keyword.twittershort}} se enlaza a la app, la instancia de servicio se suministra con credenciales exclusivas. La app utiliza estas credenciales con las API REST para buscar y consumir contenido Twitter.  Siga estos pasos para recuperar las credenciales de VCAP_SERVICES e integrar la instancia de servicio con la app.

1. Vaya a la página de descripción general de la aplicación.
2. Vaya a la sección **Variables de entorno**. Se visualiza la información `VCAP_SERVICES` para cada uno de los servicios.
3. Anote los valores de nombre de usuario y contraseña desde el servicio {{site.data.keyword.twittershort}}. Para probar las operaciones en la documentación de referencia de API REST, deberá especificar estas credenciales. Por ejemplo, `VCAP_SERVICES` se parece al siguiente fragmento de código:

```
{  
   "twitterinsights": [    
     {      
      "name": "IBM Insights for Twitter-x3",
      "label": "twitterinsights",
      "plan": "Free",
      "credentials": {
         "port": "443",
         "username": "fa7fed4b86baa0ec3e48e96b29cd2a03",
         "host": "cdeservice.mybluemix.net",
         "password": "7cunxw29",
         "url": "https://fa7fed4b86baa0ec3e48e96b29cd2a03:7cunxw29@cdeservice.mybluemix.net"
      }
     }  
   ]
}
```

# rellinks
{: #rellinks}
## ejemplos
{: #samples}
* [Demo de búsqueda de decahose interactiva](https://cdetestapp.mybluemix.net/){: new_window}
* [developerWorks: Guía de aprendizaje y código fuente para la demo de búsqueda de decahose](http://www.ibm.com/developerworks/cloud/library/cl-twitter-search-insights-bluemix-trs/index.html){: new_window}
* [Análisis de los datos de taquilla de "El francotirador" (YouTube)](https://www.youtube.com/watch?v=Gfk5quglXvI){: new_window}
* [Places Insights hands-on lab](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}

## api
{: #api}
* [API REST](https://cdeservice.{APPDomain}/rest-api/){: new_window}

## tiempos de ejecución compatibles
{: #buildpacks}
* [Ir](https://console.{DomainName}/docs/runtimes/go/index.html){: new_window}
* [Liberty for Java](https://console.{DomainName}/docs/runtimes/liberty/index.html){: new_window}
* [Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html){: new_window}
* [PHP](https://console.{DomainName}/docs/runtimes/php/index.html){: new_window}
* [Python](https://console.{DomainName}/docs/runtimes/python/index.html){: new_window}
* [Ruby](https://console.{DomainName}/docs/runtimes/ruby/index.html){: new_window}
* [Swift](https://console.{DomainName}/docs/runtimes/swift/index.html){: new_window}
* [Tomcat](https://console.{DomainName}/docs/runtimes/tomcat/index.html){: new_window}

## general
{: #general}
* [Novedades en {{site.data.keyword.Bluemix_notm}} Services](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){: new_window}
* [Adición de un servicio a la aplicación](../reqnsi.html){: new_window}
* [Desarrollo completo](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [{{site.data.keyword.Bluemix_notm}} Hoja de precios](https://console.{DomainName}/pricing/){: new_window}
* [{{site.data.keyword.Bluemix_notm}} Requisitos previos de ](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}

