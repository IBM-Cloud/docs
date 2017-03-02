---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#{{site.data.keyword.geospatialshort_Geospatial}} resolución de problemas 
{: #ts_geospatial}


Obtenga las respuestas a algunas preguntas comunes sobre el uso de {{site.data.keyword.geospatialshort_Geospatial}} en {{site.data.keyword.Bluemix_short}}.
{:shortdesc}

##Cuando detengo mi app, el servicio sigue supervisando regiones
{: #stop-monitoring}


El hecho de detener la app no detiene automáticamente {{site.data.keyword.geospatialshort_Geospatial}}.
{:shortdesc}


Ha detenido la aplicación que utiliza {{site.data.keyword.geospatialshort_Geospatial}}, pero ve en el panel de control de administración de servicios que el servicio sigue supervisando las regiones que ha especificado en la app.
{: tsSymptoms}


Si detiene la aplicación, la instancia del servicio {{site.data.keyword.geospatialshort_Geospatial}} sigue ejecutándose. El servicio sigue supervisando regiones hasta que detenga el servicio, independientemente de si la app se está ejecutando. 
{: tsCauses}


Detenga {{site.data.keyword.geospatialshort_Geospatial}} desde el panel de control de administración de servicios. También puede modificar la app para detener el servicio mediante la API REST y luego enviar los cambios de nuevo a {{site.data.keyword.Bluemix_short}}.
{: tsResolve}

##El servicio supervisa regiones que no he especificado en mi app
{: #unspecified-region}



Si tiene más de una aplicación enlazada a la misma instancia de servicio, es posible que otra aplicación haya añadido estas regiones.
{:shortdesc}



Cuando consulte la instancia de {{site.data.keyword.geospatialshort_Geospatial}} en el panel de control de administración de servicios, verá que está supervisando más regiones de las que ha especificado en una de sus apps.
{: tsSymptoms}

Una sola instancia de {{site.data.keyword.geospatialshort_Geospatial}} supervisa las regiones de todas las apps enlazadas a la misma. Esto significa que cuando consulte el servicio en el panel de control de administración, verá información correspondiente a las regiones especificadas por todas sus apps.
{: tsCauses}

Para que {{site.data.keyword.geospatialshort_Geospatial}} deje de supervisar ciertas regiones:

1. Detener el servicio.
2. Modifique la app o apps para eliminar dichas regiones.
3. Envíe la app o apps de nuevo a {{site.data.keyword.Bluemix_short}}.
{: tsResolve}


##Resolución de problemas desde el panel de control de administración de servicios
{: #dashboard}

Cuando resuelva los problemas de la aplicación, deseará ir al panel de control de administración de servicios para ver el estado de la instancia del servicio. Si no está procesando datos, es posible que pueda solucionar el problema deteniendo y volviendo a iniciar el servicio.
{:shortdesc}

El estado de la instancia del servicio {{site.data.keyword.geospatialshort_Geospatial}} es independiente del estado de la aplicación y se pueden enlazar varias aplicaciones a la misma instancia de servicio. 

El panel de control de administración de servicios ofrece información sobre el estado de {{site.data.keyword.geospatialshort_Geospatial}}, no sobre las aplicaciones enlazadas al mismo. Los estados separados de la instancia de servicio y de la aplicación o aplicaciones significan que si detiene la aplicación, la instancia del servicio {{site.data.keyword.geospatialshort_Geospatial}} continúa ejecutándose. El servicio sigue supervisando las regiones que ha elegido hasta que las elimina, independientemente de si la app se está ejecutando o no.
