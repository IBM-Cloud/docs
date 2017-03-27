---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Supervisión en Bluemix
{: #monitoring_bmx_ov}

De forma predeterminada, {{site.data.keyword.Bluemix_notm}} recopila y muestra medidas de rendimiento correspondientes a uso de CPU, utilización de memoria y E/S de red. Estas medidas ofrecen información sobre el rendimiento de recursos individuales de la nube. Puede supervisar el rendimiento de estos recursos en el entorno de red mediante la IU de {{site.data.keyword.Bluemix_notm}}. Puede ver datos casi en tiempo real y datos históricos.
{:shortdesc}

Puede utilizar las funciones de supervisión de {{site.data.keyword.Bluemix_notm}} para recopilar y calcular automáticamente medidas clave del entorno y las aplicaciones. No se requiere ninguna instrumentación especial para recopilar medidas. Por ejemplo, puede utilizar la información que proporcionan las medidas de rendimiento para supervisar la forma en que se ejecuta un servicio en la nube, detectar cuellos de botella de recursos y supervisar el acuerdo de nivel de servicio (SLA). Al analizar los datos de rendimiento de un servicio, puede detectar situaciones que pueden dar lugar a un cuello de botella del recurso, lo que afectaría al SLA de servicio de los clientes. Al emprender una acción temprana, puede evitar situaciones que podrían perjudicar a su negocio.  

También puede configurar y supervisar más medidas de rendimiento. Puede visualizar y analizar estas medidas fuera de {{site.data.keyword.Bluemix_notm}}. Por ejemplo, puede utilizar Grafana para supervisar más medidas al ejecutar una app en {{site.data.keyword.containershort}}. Puede personalizar paneles de control por instancia de contenedor o por espacio donde visualiza a y analiza los datos de rendimiento.

![Vista de supervisión de Grafana de un contenedor que se ejecuta en {{site.data.keyword.Bluemix_notm}}](images/monitoring_default_container_grafana_view.jpg)

Puede utilizar las funciones de supervisión de la plataforma {{site.data.keyword.Bluemix_notm}} para:

* Tener una mejor perspectiva de las operaciones de la aplicación (por ejemplo, detectar los posibles cuellos de botella o cuando se deben efectuar actualizaciones).
* Definir tendencias que puede utilizar para planificar futuros requisitos de una app en la plataforma de nube.

Para obtener más información sobre la supervisión de apps que se ejecutan en Cloud Foundry, consulte [Supervisión de apps que se ejecutan en Cloud Foundry](monitoring_cf_apps.html#monitoring_bluemix_apps).

Para obtener más información sobre la supervisión en {{site.data.keyword.containershort}}, consulte [Supervisión en {{site.data.keyword.containershort}}](/docs/containers/monitoringandlogging/container_ml_monitor.html#container_ml_monitor).   

