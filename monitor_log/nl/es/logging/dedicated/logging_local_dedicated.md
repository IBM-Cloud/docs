---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Registro para apps CF en Dedicado y Local
{: #hybrid_apps_logs_ov}

En {{site.data.keyword.Bluemix_dedicated_notm}} y {{site.data.keyword.Bluemix_local_notm}}, las apps Cloud Foundry se suministran con registro incorporado. Puede revisar los datos que recopilan las apps en la consola de {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

Las apps Cloud Foundry utilizan loggregator de Cloud Foundry para supervisar los registros desde fuera de la app. No es necesario que instale agentes dentro de la app.

## Requisitos de hardware


| **Requisito** |    **1 nodo**     | **3 nodos para la alta disponibilidad** |
|-----------------|-------------------|-------------------|
| vCPU | 19 | 57 |
| Memoria | 80 GB | 240 GB |
| Almacenamiento local | 2,98 TB | 8,94 TB |
{: caption="Table 2. Logging hardware requirements for {{site.data.keyword.Bluemix_local_notm}}" caption-side="top"}

## Instalación

En {{site.data.keyword.Bluemix_dedicated_notm}} y {{site.data.keyword.Bluemix_local_notm}}, los registros están activos para todas de apps de forma predeterminada. Para obtener más información sobre cómo leer los registros estándares, consulte [Registro de apps que se ejecutan en Cloud Foundry](../logging_cf_apps.html#logging_bluemix_cf_apps). Además, el registro avanzado se puede habilitar en los entornos {{site.data.keyword.Bluemix_dedicated_notm}} y {{site.data.keyword.Bluemix_local_notm}}.

* Para confirmar que el registro avanzado está habilitado en los entornos {{site.data.keyword.Bluemix_dedicated_notm}} entornos y {{site.data.keyword.Bluemix_local_notm}}, siga los pasos del apartado [Visualización de registros](#hybrid_apps_logs_dash). Si no tiene el botón **Vista avanzada**, significa que esta función no está habilitada.

* Para añadir el registro avanzada al entorno, siga los pasos de la documentación de [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) o de [{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local).

## Retención de registros

En las apps de {{site.data.keyword.Bluemix_dedicated_notm}} y {{site.data.keyword.Bluemix_local_notm}} Cloud Foundry, los datos de registro se almacenan durante 30 días de forma predeterminada.

## Visualización de registros para apps Cloud Foundry en Dedicado y Local
{: #hybrid_apps_logs_dash}

Puede revisar los registros de las apps que ejecutan en {{site.data.keyword.Bluemix_dedicated_notm}} y {{site.data.keyword.Bluemix_local_notm}}.
{:shortdesc}

Para ver los registros de una app, siga estos pasos:
1. Seleccione una app en ejecución.
2. Pulse **Registros**. En la vista **Registros** puede ver los registros de la app en ejecución.
4. Pulse el botón **Vista avanzada**. **Vista avanzada** muestra una vista más detallada de los registros mediante Kibana, una herramienta de visualización que utiliza registros y datos con indicación de hora para crear visualizaciones personalizadas. Para obtener más información sobre cómo utilizar la vista avanzada, consulte la documentación de [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html).

Luego puede personalizar un panel de instrumentos de Kibana. Consulte [Análisis de registros en Kibana](../logging_view_kibana3.html#analyzing_logs_Kibana3) para obtener más información.
