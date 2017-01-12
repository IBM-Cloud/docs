---

copyright:
  years: 2016
lastupdated: "2016-11-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Iniciación a {{site.data.keyword.DRA_short}} (experimental)
{: #gettingstarted}

Utilice {{site.data.keyword.DRA_full}} para identificar riesgos en sus compilaciones y despliegues.
{:shortdesc}

{{site.data.keyword.DRA_short}} agrega y analiza los resultados de pruebas de unidad, pruebas funcionales y herramientas de cobertura de código para determinar si el código cumple las políticas predefinidas en las puertas especificadas del proceso de despliegue. Si el código no cumple o supera una política, el despliegue se detiene para impedir que se liberen cambios arriesgados. Puede utilizar {{site.data.keyword.DRA_short}} como red de seguridad para su entorno de entrega continua, como método para implementar y mejorar con el tiempo los estándares de calidad y como una herramienta de visualización de datos para ayudarle a comprender el estado de salud de su proyecto.

{{site.data.keyword.DRA_short}} es una oferta experimental y se proporciona tal cual únicamente para finalidades de desarrollo y experimentación. Para utilizar {{site.data.keyword.DRA_short}}, añádalo a cualquier cadena de herramientas que utilice {{site.data.keyword.deliverypipeline}}.

{: #catalog}
Para acceder a la interfaz de usuario de {{site.data.keyword.DRA_short}}, realice los pasos siguientes dese una cadena de herramientas existente:

1. Pulse el botón **Añadir una herramienta**.

2. Pulse **{{site.data.keyword.DRA_short}}**.

3. Pulse **Crear integración**.

4. Pulse el mosaico **{{site.data.keyword.DRA_short}}**.

5. Complete la configuración con las tareas restantes:

	1. [Configure su integración con {{site.data.keyword.deliverypipeline}}](./pipeline_integration.html).
	2. Ejecute el conducto y [revise los paneles de control de {{site.data.keyword.deliverypipeline}}](./pipeline_decision_reports.html).
	3. [Defina políticas](./create_criteria.html) que {{site.data.keyword.DRA_short}} debe gestionar.
	4. Ejecute el conducto de nuevo para comprobar que el proyecto cumple las políticas.


# Enlaces relacionados
{: #rellinks}

## Guías de aprendizaje y ejemplos
{: #samples}

* [Utilización de análisis para evaluar la probabilidad despliegues correctos](https://www.ibm.com/devops/method/content/deliver/tool_deployment_risk_analytics/){:new_window}

## Enlaces relacionados
{: #general}

* [Iniciación a las cadenas de herramientas](https://new-console.ng.bluemix.net/docs/toolchains/toolchains_overview.html){:new_window}
* [Iniciación a Delivery Pipeline](https://new-console.ng.bluemix.net/docs/services/DeliveryPipeline/index.html){:new_window}
* [Hoja de precios de IBM Bluemix](https://new-console.ng.bluemix.net/pricing/){:new_window}
* [Requisitos previos de IBM Bluemix](https://developer.ibm.com/bluemix/support/?cm_mc_uid=96503159749414585876298&cm_mc_sid_50200000=1462802909#prereqs){:new_window}
