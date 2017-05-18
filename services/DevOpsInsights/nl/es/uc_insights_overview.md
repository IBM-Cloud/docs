---

copyright:
  years: 2017
lastupdated: "2017-03-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Integración de DevOps Insights con IBM UrbanCode Deploy - visión general
{: #uc_insights_overview}

Delivery Insights, una parte de {{site.data.keyword.DRA_short}}, muestra estadísticas de despliegue, métricas e información adicional sobre su instalación IBM UrbanCode Deploy. Por ejemplo, puede mostrar gráficas de duración, éxitos y errores de despliegue, clasificadas por entornos agrupados de forma lógica. {:shortdesc}

Si no tiene una cadena de herramientas o {{site.data.keyword.DRA_short}}, primero debe configurar {{site.data.keyword.DRA_short}}:

1. Desde el catálogo de {{site.data.keyword.Bluemix}}, pulse **{{site.data.keyword.DRA_short}}**, seleccione un plan de precios y, a continuación, pulse **Crear**.
1. Pulse el separador **Gestionar** y, a continuación, bajo **Empezar con Delivery Insights for UrbanCode**, pulse **Empezar aquí**. Delivery Insights creará en un segundo plano una cadena de herramientas para su organización. Las cadenas de herramientas abiertas son conjuntos de integraciones de herramientas y, en este caso, IBM UrbanCode Deploy y {{site.data.keyword.DRA_short}} son parte de su cadena de herramientas. Para obtener más información sobre las cadenas de herramientas, consulte [Cómo trabajar con cadenas de herramientas](../ContinuousDelivery/toolchains_working.html).
1. En la página **Configuración de Delivery Insights**, siga los pasos para configurar DevOps Connect y conectar sus servidores IBM UrbanCode Deploy. 
<!--  1. Set up a system to run DevOps Connect. See [prerequisites](uc_insights_prereqs.html).
  1. Download DevOps Connect, which is provided in a runnable JAR file.
  1. Copy the script from the **Delivery Insights Setup** page and run it. This command starts DevOps Connect with a token that allows it to connect to your organization on {{site.data.keyword.Bluemix}}.
  1. Connect your IBM UrbanCode Deploy servers to DevOps connect. See [Connecting IBM UrbanCode Deploy servers to Delivery Insights](uc_insights_connect_ucd.html). -->


Si ya tiene una cadena de herramientas, siga estos pasos para añadir Delivery Insights:
1. Si todavía no tiene la herramienta {{site.data.keyword.DRA_short}}, añádala a la cadena de herramientas.
1. En la cadena de herramientas, pulse la herramienta {{site.data.keyword.DRA_short}}. 
1. En la página **Configuración de Delivery Insights**, siga los pasos para configurar DevOps Connect y conectar sus servidores IBM UrbanCode Deploy. 

Después de haber configurado Delivery Insights y DevOps Connect, puede mostrar datos de los servidores IBM UrbanCode Deploy en Delivery Insights. Consulte [Conexión de servidores IBM UrbanCode Deploy a Delivery Insights](uc_insights_connect_ucd.html).

<!-- 
For questions or issues, see the [questions forum](https://developer.ibm.com/answers/?community=urbancode).
--> 

![Dos gráficas de datos de demostración de UrbanCode Insights](images/uc_insights_demo_data.gif)

Entre la información que Delivery Insights proporciona, se incluyen: 

- Estadísticas sobre despliegue, incluida la duración del despliegue y el volumen de despliegue a lo largo del tiempo. 
- Estadísticas sobre la tasa de errores de despliegue por aplicación y entorno. 
- Estadísticas sobre el despliegue de componentes, incluida la tase de errores, el tiempo de despliegue y la duración. 

## Visión general de los sistemas

La topología de Delivery Insights incluye una o varias instalaciones locales de IBM UrbanCode Deploy <!-- (and optionally IBM UrbanCode Release) --> y el programa de utilidad DevOps Connect. 

La siguiente gráfica muestra una instalación típica de estos sistemas.

![Visión general de la topología para UrbanCode Insights, incluidos los sistemas locales del cliente e IBM Cloud Services](images/uc_insights_overview_topology_multi_ucd.png)

- Una instalación de **IBM UrbanCode Deploy** proporciona la información sobre los despliegues satisfactorios y erróneos para las métricas. IBM UrbanCode Deploy precisa de un parche para comunicarse con IBM Bluemix DevOps Connect.

<!--
- **IBM UrbanCode Release** is an optional part of the topology. You can use the environment mappings in IBM UrbanCode Release to set logical environments for reports.

-->

- **IBM Bluemix DevOps Connect**, anteriormente conocido por IBM UrbanCode Sync Utility, coordina la comunicación entre las instalaciones locales de IBM UrbanCode Deploy <!-- and IBM UrbanCode Release --> y los servicios alojados por IBM como, por ejemplo, UrbanCode Insights. DevOps Connect utiliza una comunicación HTTPS segura en los servidores locales y señales de autenticación al proporcionar datos a UrbanCode Insights.

  DevOps Connect precisa de plugins para conectarse a otros sistemas en la topología. 

- **Delivery Insights**, parte de {{site.data.keyword.DRA_short}}, proporciona métricas sobre la actividad de despliegue en IBM UrbanCode Deploy, incluidos tiempo de despliegue y tasas de errores de acuerdo a grupos de entornos. Las cuentas de {{site.data.keyword.Bluemix}} controlan las autorizaciones. 
