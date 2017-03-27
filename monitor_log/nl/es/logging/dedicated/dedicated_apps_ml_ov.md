---



copyright:

  years: 2016, 2017

lastupdated: "2016-10-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

<!-- audience blue staging only begin -->

# Supervisión y registro para apps de Cloud Foundry en Dedicado y Local
{: #dedicated_apps_ml_ov}


En {{site.data.keyword.Bluemix_dedicated_notm}} y {{site.data.keyword.Bluemix_local_notm:}}, las apps Cloud Foundry se suministran con registro incorporado. Puede revisar los datos que recopilan las apps en la consola de {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

Las apps Cloud Foundry utilizan loggregator de Cloud Foundry para supervisar los registros desde fuera de la app. No es necesario que instale agentes dentro de la app.

## Requisitos de hardware


| **Requisito** |    **1 nodo**     | **3 nodos para la alta disponibilidad** |
|-----------------|-------------------|-------------------|
vCPU | 19 | 57 |
Memoria | 80 GB | 240 GB |
Almacenamiento local | 2,98 TB | 8,94 TB |
{: caption="Table 1. Logging hardware requirements for {{site.data.keyword.Bluemix_local_notm:}}" caption-side="top"}

## Instalación

En {{site.data.keyword.Bluemix}} Dedicado y {{site.data.keyword.Bluemix}} Local, los registros estarán activos para todas las apps de forma predeterminada. Para ver información sobre la lectura de registros estándares, consulte Registro para apps que se ejecutan en Cloud Foundry. Además, el registro avanzado se puede habilitar en los entornos {{site.data.keyword.Bluemix}} Dedicado y {{site.data.keyword.Bluemix}} Local.

## Retención de registros

En las aplicaciones de Cloud Foundry {{site.data.keyword.Bluemix}} Dedicado y {{site.data.keyword.Bluemix}} Local, los datos de registro se almacenan durante 30 días de forma predeterminada.

## Visualización de registros para apps Cloud Foundry en {{site.data.keyword.Bluemix}} Dedicado y {{site.data.keyword.Bluemix}} Local
{: #dedicated_apps_ml_logs_dash}

Puede revisar los registros de las apps que se ejecutan en {{site.data.keyword.Bluemix_notm}} Dedicado y {{site.data.keyword.Bluemix_notm}} Local.
{:shortdesc}

Para ver los registros de una app, siga estos pasos:
1. Seleccione una app en ejecución.
2. Pulse **Registros**. En la vista **Registros** puede ver los registros de la app en ejecución.
4. Pulse el botón **Vista avanzada**. **Vista avanzada** muestra una vista más detallada de los registros mediante Kibana, una herramienta de visualización que utiliza registros y datos con indicación de hora para crear visualizaciones personalizadas. Para obtener más información sobre cómo utilizar la vista avanzada, consulte la documentación de [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html).

Luego puede personalizar un panel de instrumentos de Kibana. Consulte [Personalización de la visualización de registros en un panel de control de Kibana](/docs/containers/monitoringandlogging/container_ml_logs.html#container_ml_dash_logs_custom) para obtener más información.

<!-- audience blue staging only end comment -->
