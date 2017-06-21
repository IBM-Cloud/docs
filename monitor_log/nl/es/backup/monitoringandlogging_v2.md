---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-14"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Supervisión y registro
{: #monitoringandlogging}

{{site.data.keyword.Bluemix}} es una plataforma de computación de {{site.data.keyword.IBM_notm}} en la nube para compilar, ejecutar y gestionar apps y servicios. {{site.data.keyword.Bluemix_notm}} combina una plataforma como servicio (PaaS) con una infraestructura como servicio (IaaS). Además, {{site.data.keyword.Bluemix_notm}} tiene un catálogo enriquecido de servicios de nube que se pueden integrar fácilmente con una PaaS e IaaS para crear aplicaciones empresariales rápidamente. {{site.data.keyword.Bluemix_notm}} incluye servicios integrados de supervisión y creación de registros en toda la plataforma. 
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} ofrece servicios de supervisión y creación de registros a lo largo de los distintos servicios de computación como, por ejemplo, Cloud Foundry y {{site.data.keyword.containershort}}. Puede desarrollar, ejecutar y gestionar aplicaciones en cualquier entorno de ejecución de computación sin la complejidad de tener que crear y mantener la infraestructura que se suele asociar al desarrollo y puesta en marcha de una app. 

**Nota:** Las funcionalidades de supervisión y creación de registros están disponibles en la región US South y en la región United Kingdom.

Puede utilizar las funciones de supervisión de {{site.data.keyword.Bluemix_notm}} para recopilar y calcular automáticamente medidas clave del entorno y las aplicaciones. No se requiere ninguna instrumentación especial para recopilar medidas. Por ejemplo, puede utilizar la información que proporcionan las medidas de rendimiento para supervisar la forma en que se ejecuta un servicio en la nube, detectar cuellos de botella de recursos y supervisar el acuerdo de nivel de servicio (SLA). Por ejemplo, al analizar los datos de rendimiento de un servicio, puede detectar situaciones que pueden dar lugar a un cuello de botella del recurso, lo que afectaría al SLA de servicio de los clientes. Al emprender una acción temprana, puede evitar situaciones que podrían perjudicar a su negocio.  

Puede utilizar las funciones de registro de {{site.data.keyword.Bluemix_notm}} para comprender el comportamiento de la plataforma de nube y los recursos que se ejecutan la misma. No se requiere ninguna instrumentación especial para recopilar la salida estándar y los registros de error estándares. Por ejemplo, puede utilizar registros para proporcionar un seguimiento de auditoría para una aplicación, detectar problemas en un servicio, identificar vulnerabilidades, resolver problemas de despliegues de app y de comportamiento del tiempo de ejecución, detectar problemas en la infraestructura en la que se ejecuta la app, realizar un rastreo de la app entre los componentes de la plataforma de nube y detectar patrones que puede utilizar para tomar el control de acciones que podrían afectar al SLA del servicio.

## Supervisión de recursos de infraestructura de computación
{: #monitoring_sl_ov}

Cada servidor de {{site.data.keyword.Bluemix_notm}} incluye funcionalidades de supervisión e informes fácilmente entendibles que siempre están disponibles. Para obtener más información, consulte [Supervisión de la infraestructura e informes ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](https://www.ibm.com/cloud-computing/bluemix/infrastructure-monitoring){: new_window}.


## Supervisión en {{site.data.keyword.Bluemix}} para servicios de computación
{: #monitoring_bmx_ov}

De forma predeterminada, {{site.data.keyword.Bluemix_notm}} recopila y muestra medidas de rendimiento correspondientes a uso de CPU, utilización de memoria y E/S de red. Estas medidas ofrecen información sobre el rendimiento de recursos individuales de la nube. Puede supervisar el rendimiento de estos recursos en el entorno de red mediante la IU de {{site.data.keyword.Bluemix_notm}}. Puede ver datos casi en tiempo real y datos históricos. 

También puede configurar y supervisar más medidas de rendimiento. Puede visualizar y analizar estas medidas fuera de {{site.data.keyword.Bluemix_notm}}. Por ejemplo, puede utilizar Grafana para supervisar más medidas al ejecutar una app en {{site.data.keyword.containershort}}. Puede personalizar paneles de control por instancia de contenedor o por espacio donde visualiza a y analiza los datos de rendimiento.

![Vista de supervisión de Grafana en un contenedor ejecutándose en {{site.data.keyword.Bluemix_notm}}](images/monitoring_default_container_grafana_view.jpg)

Puede utilizar las funciones de supervisión de la plataforma {{site.data.keyword.Bluemix_notm}} para:

* Tener una mejor perspectiva de las operaciones de la aplicación (por ejemplo, detectar los posibles cuellos de botella o cuando se deben efectuar actualizaciones).
* Definir tendencias que puede utilizar para planificar futuros requisitos de una app en la plataforma de nube.

Para obtener más información sobre la supervisión de apps que se ejecutan en Cloud Foundry, consulte [Supervisión de apps que se ejecutan en Cloud Foundry](monitoring_cf_apps.html#monitoring_bluemix_apps).

Para obtener más información sobre la supervisión en {{site.data.keyword.containershort}}, consulte [Supervisión en {{site.data.keyword.containershort}}](/docs/containers/monitoringandlogging/container_ml_monitor.html#container_ml_monitor).   

## Creación de registros en {{site.data.keyword.Bluemix}}
{: #logging_bmx_ov}

Las funciones de registro de {{site.data.keyword.Bluemix_notm}} están integradas en la plataforma y la recopilación de datos se habilita automáticamente para los recursos de la nube. De forma predeterminada, {{site.data.keyword.Bluemix_notm}} recopila y muestra los registros correspondientes a sus apps, tiempos de ejecución de apps y tiempos de ejecución del sistema en el que se ejecutan dichas apps. 

Cuando ejecuta sus apps en la nube, es posible que no pueda utilizar SSH ni FTP en la infraestructura en la que se ejecutan las apps para acceder a los registros, por ejemplo si ejecuta apps en Cloud Foundry. Por otro lado, puede ejecutar la app en {{site.data.keyword.containershort}}, otro tiempo de ejecución de cálculo disponible en {{site.data.keyword.Bluemix_notm}}, donde puede ejecutar SSH y acceder a los registros. Independientemente del tiempo de ejecución de cálculo, el acceso a los registros resulta crucial y {{site.data.keyword.Bluemix_notm}} proporciona una experiencia común para visualizar y analizar registros en la plataforma en la nube.

{{site.data.keyword.Bluemix_notm}} registra los datos de registro que genera la plataforma Cloud Foundry y las aplicaciones de Cloud Foundry. En los registros puede ver los errores, avisos y mensajes informativos que se generan para la app. Para obtener más información sobre la creación de registros en Cloud Foundry, consulte [Creación de registros para apps de Cloud Foundry en {{site.data.keyword.Bluemix}}](logging_cf_apps.html#logging_bluemix_cf_apps).

{{site.data.keyword.Bluemix_notm}} registra los datos de registro que genera {{site.data.keyword.containershort}}. Para obtener información sobre la creación de registros en {{site.data.keyword.containershort}}, consulte [Creación de registros en {{site.data.keyword.containershort}}](/docs/containers/monitoringandlogging/container_ml_logs.html#container_ml_logs).   


Con la función de registro que proporciona {{site.data.keyword.Bluemix_notm}}, puede:

* Obtener una perspectiva de los recursos de la nube y sobre su rendimiento y ejecución.
* Definir tendencias que le ayuden a identificar escenarios que requieran su intervención.
* Definir seguimientos de datos para una app que puede, por ejemplo, utilizar para la auditoría.
* Reducir el tiempo y esfuerzo necesarios para localizar y solucionar cualquier problema de una app. 
* Supervisar el despliegue de sus apps en la plataforma de nube.
* Detectar cuándo un servicio o una app está inactivo o se ha colgado.
* Realizar un seguimiento de la ejecución y del flujo de datos de una aplicación.
* Identificar vulnerabilidades de una app.
* Detectar problemas de la infraestructura.
* Detectar problemas del tiempo de ejecución de una app.


