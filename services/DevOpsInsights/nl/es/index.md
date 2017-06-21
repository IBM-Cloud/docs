---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Iniciación a DevOps Insights (Beta)
{: #gettingstarted}

{{site.data.keyword.DRA_full}} aplica analíticas de despliegue, equipos y desarrolladores a los proyectos DevOps. Utilícelas para conocer en qué medida su equipo sigue los procedimientos de desarrollador y de DevOps, para gestionar el riesgo en su codebase y para imponer de forma automática estándares de calidad en proyectos de entrega continua.
{:shortdesc}

{{site.data.keyword.DRA_short}} consta de varios grupos de funcionalidades:

   * Developer Insights proporciona una forma averiguar la madurez del desarrollo de un proyecto. Permite identificar los archivos más propensos a contener errores y obtener una vista de conformidad del proyecto con relación a los procedimientos de desarrollador.

   * Team Dynamics utiliza análisis de codificación social para ayudarle a comprender cómo colabora entre sí el equipo y cómo puede hacerlo mejor.

   * Deployment Risk es como una red de seguridad para la entrega continua. Analiza los resultados de pruebas de unidad, pruebas funcionales, exploraciones de código y herramientas de cobertura de código en puertas concretas en su proceso de despliegue e impide que se liberen cambios peligrosos.

   * Delivery Insights muestra estadísticas de despliegue, métricas e información adicional sobre su instalación IBM UrbanCode Deploy. Por ejemplo, puede mostrar gráficas de duración, éxitos y errores de despliegue, clasificadas por entornos agrupados de forma lógica. Consulte [Integración de DevOps Insights con IBM UrbanCode Deploy](/docs/services/DevOpsInsights/uc_insights_overview.html).

{{site.data.keyword.DRA_short}} es una integración en el catálogo de cadenas de herramientas abiertas de Bluemix. Para obtener más información sobre las cadenas de herramientas, consulte [Cómo trabajar con cadenas de herramientas](/docs/services/ContinuousDelivery/toolchains_working.html).

Para utilizar {{site.data.keyword.DRA_short}}, deberá añadirlo a una cadena de herramientas. Muchas cadenas de herramientas ya incluyen a {{site.data.keyword.DRA_short}}. Asegúrese también de [añadirlo a su organización de {{site.data.keyword.Bluemix_notm}} como un servicio](/docs/services/reqnsi.html) de forma que pueda ver información sobre {{site.data.keyword.DRA_short}} y acceder desde su panel de control de {{site.data.keyword.Bluemix_notm}} a algunas de las plantillas de cadena de herramientas que lo incluyen.  

## Adición de DevOps Insights a una cadena de herramientas
{: #catalog}

{{site.data.keyword.DRA_short}} es parte de {{site.data.keyword.contdelivery_short}}. {{site.data.keyword.DRA_short}} se puede añadir a cualquier cadena de herramientas seleccionándolo desde el catálogo de integración de herramientas.

{{site.data.keyword.DRA_short}} también es parte de muchas plantillas de cadena de herramientas. Si crea una cadena de herramientas a partir de una plantilla que incluye {{site.data.keyword.DRA_short}}, asegúrese de que {{site.data.keyword.DRA_short}} se establece en **Avanzado**. A continuación, cree la cadena de herramientas y vaya a [Utilización de Insights](/docs/services/DevOpsInsights/index.html#using).

Para añadir {{site.data.keyword.DRA_short}} a una cadena de herramientas:

1. Pulse **Añadir una herramienta**.

2. Pulse **{{site.data.keyword.DRA_short}}**.

3. Pulse **Crear integración**.

{{site.data.keyword.DRA_short}} está ahora disponible en la página Visión general de la cadena de herramientas. Automáticamente se exploran los datos de su repositorio y sistema de seguimiento de problemas. 

## Utilización de DevOps Insights
{: #using}

Si su cadena de herramientas incluye GitHub, GitLab, o JIRA, {{site.data.keyword.DRA_short}} proporciona de forma automática información sobre su codebase y del equipo después de una recopilación y análisis de los datos iniciales. Si su cadena de herramientas no incluye ninguna de estas integraciones, añada una de ellas y, a continuación, siga estos pasos:

1. Desde la página visión general de la cadena de herramientas, pulse **{{site.data.keyword.DRA_short}}**.

2. Pulse **Team Dynamics** o **Developer Insights** y, a continuación, seleccione una categoría de datos.  

3. Explore los datos del proyecto mediante la visualización de los paneles de control en la categoría de datos. Si desea saber más sobre un gráfico o lo que puede hacer con su información, pulse **Information** o **Instrucciones**.

Después de explorar Team Dynamics y Developer Insights, [configure Deployment Risk](/docs/services/DevOpsInsights/insights_risk.html) que le ayudará en el cumplimiento de calidad de código deseada. Deployment Risk es compatible tanto con los conductos de {{site.data.keyword.contdelivery_short}} como con Jenkins.   
