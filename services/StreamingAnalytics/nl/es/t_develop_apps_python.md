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

# Desarrollo de aplicaciones Python para {{site.data.keyword.streaminganalyticsshort}}
{: #t_develop_apps_python}

Ahora puede desarrollar aplicaciones Python en IBM Data Science Experience (DSX) o en un entorno de desarrollo Python local y desplegarlas en {{site.data.keyword.streaminganalyticsshort}}.
{:shortdesc}

Desarrolle y despliegue sus aplicaciones Python en la nube de {{site.data.keyword.Bluemix_short}} utilizando el servicio {{site.data.keyword.streaminganalyticsshort}} y uno de estos métodos: 


## Desarrollo de aplicaciones Streams Python en DSX
{: #t_develop_python_dsx}

Si no dispone de un entorno de desarrollo Python, el modo más sencillo de comenzar consiste en utilizar nuestros cuadernos en DSX y crear aplicaciones Python para el servicio {{site.data.keyword.streaminganalyticsshort}}. Estos cuadernos muestran los pasos a seguir y ejemplos de código para crear y desplegar aplicaciones Python de ejemplo para el servicio {{site.data.keyword.streaminganalyticsshort}} dentro del entorno DSX Python: 

* [Hello World!](https://apsportal.ibm.com/exchange/public/entry/view/9fc33ce7301f10e21a9f92039ca9c6e8): Cree una sencilla aplicación Hello World! para empezar a trabajar y desplegar la aplicación en una instancia del servicio {{site.data.keyword.streaminganalyticsshort}}. 

* [Healthcare Demo](https://apsportal.ibm.com/exchange/public/entry/view/9fc33ce7301f10e21a9f92039cad29a6): Cree una aplicación que ingiera y analice datos de secuencias (streaming) desde un canal de información y luego visualice los datos en el cuaderno. Finalmente, envíe esta aplicación a la instancia del servicio {{site.data.keyword.streaminganalyticsshort}}. 

* [Neural Net Demo](https://apsportal.ibm.com/exchange/public/entry/view/9fc33ce7301f10e21a9f92039ca60bb7): Cree un conjunto de datos de ejemplo, cree un modelo para los datos de ejemplo, utilice dicho modelo en una aplicación de streaming, visualice los datos de streaming y finalmente envíe la aplicación streaming al servicio {{site.data.keyword.streaminganalyticsshort}}. 

## Desarrollo de aplicaciones en el entorno Python local
 {: #t_develop_python_api}

 La [API de aplicación de {{site.data.keyword.streamsshort}} Python](http://ibmstreams.github.io/streamsx.documentation/docs/python/python-appapi-devguide/#50-api-features), que se incluye en el paquete streamsx, le permite crear aplicaciones de proceso de secuencias utilizando clases y funciones que se pueden llamar desde Python. Utilice la API de aplicación de Python y luego defina y envíe la aplicación al servicio. 

Comience siguiendo los pasos de la guía de aprendizaje [Desarrollo para el servicio {{site.data.keyword.streaminganalyticsshort}}](http://ibmstreams.github.io/streamsx.documentation/docs/python/1.6/python-appapi-devguide-2a/index.html) para crear una aplicación de ejemplo en el entorno Python local y despliéguela en el servicio {{site.data.keyword.streaminganalyticsshort}}. 
