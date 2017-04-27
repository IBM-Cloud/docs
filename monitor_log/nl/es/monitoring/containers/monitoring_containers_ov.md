---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-08"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Supervisión del servicio IBM Bluemix Container
{: #monitoring_bmx_containers_ov}

En {{site.data.keyword.Bluemix}}, las métricas de contenedor se recopilan automáticamente desde fuera del contenedor, sin tener que instalar y mantener agentes dentro del contenedor.
{:shortdesc}

Los agentes que están dentro del contenedor pueden sufrir importantes sobrecargas y tiempos de configuración para instancias en la nube ligeras y breves y grupos de escalado automático, en los que los contenedores
pueden crearse y destruirse rápidamente. Este método externo de recopilación de datos elimina estos problemas
y la tarea de supervisión por parte de los usuarios.

Un proceso que se ejecuta en el host efectúa una supervisión sin agentes para obtener métricas. Este proceso, que también se denomina rastreador, recopila constantemente las métricas siguientes de todos los contenedores de forma predeterminada:

* CPU
* Memoria
* Información de red

Los datos de métricas se recopilan en Graphite y se muestran en la IU de {{site.data.keyword.Bluemix_notm}} y en Grafana. 

Puede iniciar Grafana desde la IU de {{site.data.keyword.Bluemix_notm}} o directamente desde un navegador. Para obtener más información, consulte [Análisis de métricas en Grafana](../grafana/monitoring_analyzing_metrics_grafana.html#analyzing_metrics_grafana).

La información de contabilidad de grupos y los convenios de Docker sirven como mecanismo básico para recopilar datos de supervisión.

**Retención de métricas**

Se recopila hasta un punto de datos por minuto. Las métricas de contenedor que no se hayan grabado en
un plazo de 7 días se suprimirán. 
    
**Ordenación de métricas**

Los datos se muestran y ordenan según el ID del contenedor.  

Desde la línea de mandatos, puede ejecutar el mandato `cf ic ps` para ver una lista de los ID de contenedor de los contenedores del registro de imágenes privado de {{site.data.keyword.Bluemix_notm}}. 

