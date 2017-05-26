---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-29"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Registro en Bluemix
{: #logging_bmx_ov}

Las funciones de registro de {{site.data.keyword.Bluemix}} están integradas en la plataforma y la recopilación de datos se habilita automáticamente para los recursos de la nube. De forma predeterminada, {{site.data.keyword.Bluemix_notm}} recopila y muestra los registros correspondientes a sus apps, tiempos de ejecución de apps y tiempos de ejecución del sistema en el que se ejecutan dichas apps. 
{:shortdesc}

Puede utilizar las funciones de registro de {{site.data.keyword.Bluemix_notm}} para comprender el comportamiento de la plataforma de nube y los recursos que se ejecutan la misma. No se requiere ninguna instrumentación especial para recopilar la salida estándar y los registros de error estándares. Por ejemplo, puede utilizar registros para proporcionar un seguimiento de auditoría para una aplicación, detectar problemas en un servicio, identificar vulnerabilidades, resolver problemas de despliegues de app y de comportamiento del tiempo de ejecución, detectar problemas en la infraestructura en la que se ejecuta la app, realizar un rastreo de la app entre los componentes de la plataforma de nube y detectar patrones que puede utilizar para tomar el control de acciones que podrían afectar al SLA del servicio.

Cuando ejecuta sus apps en la nube, es posible que no pueda utilizar SSH ni FTP en la infraestructura en la que se ejecutan las apps para acceder a los registros, por ejemplo si ejecuta apps en Cloud Foundry. Por otro lado, puede ejecutar la app en {{site.data.keyword.containershort}}, otro tiempo de ejecución de cálculo disponible en {{site.data.keyword.Bluemix_notm}}, donde puede ejecutar SSH y acceder a los registros. Independientemente del tiempo de ejecución de cálculo, el acceso a los registros resulta crucial y {{site.data.keyword.Bluemix_notm}} proporciona una experiencia común para visualizar y analizar registros en la plataforma en la nube.

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

## Creación de registros para apps de CF
{: #logging_bmx_ov_cf}

{{site.data.keyword.Bluemix_notm}} registra los datos de registro que genera la plataforma Cloud Foundry y las aplicaciones de Cloud Foundry. En los registros puede ver los errores, avisos y mensajes informativos que se generan para la app. Para obtener más información sobre la creación de registros en Cloud Foundry, consulte [Creación de registros para apps de Cloud Foundry en Bluemix](cfapps/logging_cf_apps.html#logging_bluemix_cf_apps). 

## Creación de registros para contenedores
{: #logging_bmx_ov_containers}

{{site.data.keyword.Bluemix_notm}} registra los datos de registro que genera {{site.data.keyword.containershort}}. Para obtener más información sobre el registro en {{site.data.keyword.containershort}}, consulte [Registro correspondiente al servicio IBM Bluemix Container](containers/logging_containers_ov.html#logging_containers_ov).  

**Nota:** Tiene la posibilidad de analizar los registros de contenedores Docker en {{site.data.keyword.Bluemix_notm}} que se despliegan en la infraestructura de nube gestionada de {{site.data.keyword.IBM}}. 

## Análisis de registro en Bluemix
{: #logging_bmx_ov_ui}

En {{site.data.keyword.Bluemix_notm}}, puede ver los registros recientes para su app o la parte más reciente de los registros en tiempo real. 

* Puede ver, filtrar y analizar registros a través de la interfaz de usuario. Para obtener más información, consulte [Análisis de registros desde la consola de Bluemix](logging_view_dashboard.html#analyzing_logs_bmx_ui).

* Puede ver, filtrar y analizar registros mediante la línea de mandatos para gestionar registros mediante programación. Para obtener más información, consulte [Análisis de registros desde la interfaz de línea de mandatos](logging_view_cli.html#analyzing_logs_cli).

## Análisis avanzado de registros con Kibana
{: #logging_bmx_ov_kibana}

En {{site.data.keyword.Bluemix_notm}}, puede utilizar Kibana, una plataforma de visualización y análisis de código abierto, para supervisar, buscar, analizar y visualizar datos en diversos gráficos, como diagramas y tablas. Para obtener más información, consulte [Análisis avanzado de registros con Kibana](kibana4/analyzing_logs_Kibana.html#analyzing_logs_Kibana).


