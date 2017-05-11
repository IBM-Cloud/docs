---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-4"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Acerca de la entrega continua  
{: #cd_about}  

Con {{site.data.keyword.contdelivery_full}} puede crear, probar y entregar aplicaciones mediante las herramientas más utilizadas de la industria y prácticas de DevOps.
{:shortdesc}

El servicio {{site.data.keyword.contdelivery_short}} da soporte a los flujos de trabajo de DevOps: 

 * Puede crear [cadenas de herramientas](/docs/services/ContinuousDelivery/toolchains_about.html){: new_window} abiertas integradas de DevOps para habilitar las integraciones de herramientas que dan soporte a las tareas de desarrollo, despliegue y operaciones. 

  Una cadena de herramientas es un conjunto integrado de herramientas que puede utilizar para desarrollar, crear, desplegar, prueba y gestionar aplicaciones de forma colaborativa. Puede crear cadenas de herramientas que incluyan servicios de {{site.data.keyword.Bluemix_notm}}, herramientas de código abierto y herramientas de otros proveedores, como por ejemplo GitHub, PagerDuty y Slack, que facilitan el desarrollo y la gestión de operaciones. 

 * Entrega continua mediante [conductos](/docs/services/ContinuousDelivery/pipeline_about.html){: new_window} automatizados.

  Automatice compilaciones, pruebas de unidad, despliegues y más. Cree, pruebe y despliegue de manera repetitiva con una mínima intervención humana. Esté listo para pasar a producción en cualquier momento.

 * Edite y envíe el código desde cualquier lugar utilizando el [IDE basado en web](/docs/services/ContinuousDelivery/web_ide.html){: new_window}. 

  Cree, edite, ejecute, depure y complete tareas de control de código fuente en GitHub. Puede pasar fácilmente de editar el código a desplegarlo en producción. 

 * Mejore la calidad mediante [{{site.data.keyword.DRA_short}}](/docs/services/ContinuousDelivery/di_working.html){: new_window}.

  Comprenda la dinámica de su equipo a medida que desarrolla y entrega el código. Sepa cómo interactúan los usuarios con la aplicación. Revise los datos para ayudarle a gestionar las operaciones de la aplicación.


## Disponibilidad de la cadena de herramientas en Bluemix público en comparación con Bluemix dedicado
{: #public_and_dedicated}

{{site.data.keyword.Bluemix_notm}} público es una plataforma basada en la nube de estándares abiertos con la que puede crear, ejecutar y gestionar aplicaciones a las que accede [http://bluemix.net ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://bluemix.net){:new_window}. {{site.data.keyword.Bluemix_notm}} dedicado ofrece las funciones de {{site.data.keyword.Bluemix_notm}} en un entorno SoftLayer dedicado conectado de forma segura tanto al entorno de {{site.data.keyword.Bluemix_notm}} público como a la red. Es posible que el entorno {{site.data.keyword.Bluemix_notm}} dedicado de la empresa no contenga las mismas integraciones de herramientas que el sitio de {{site.data.keyword.Bluemix_notm}} público. 

Para la gestión de código fuente y el seguimiento de problemas, {{site.data.keyword.Bluemix_notm}} público suele utilizar github.com. {{site.data.keyword.Bluemix_notm}} dedicado también puede utilizar github.com, aunque normalmente utiliza {{site.data.keyword.ghe_short}} instalado por la empresa o gestionado por IBM. 

{{site.data.keyword.contdelivery_short}} está disponible en {{site.data.keyword.Bluemix_notm}} público y en {{site.data.keyword.Bluemix_notm}} dedicado. Las cadenas de herramientas difieren en función de si utiliza {{site.data.keyword.contdelivery_short}} en {{site.data.keyword.Bluemix_notm}} público o en {{site.data.keyword.Bluemix_notm}} dedicado. 

|Cadenas de herramientas |{{site.data.keyword.Bluemix_notm}} público	|{{site.data.keyword.Bluemix_notm}} dedicado |
|:----------|:------------------------------|:------------------|
|Integraciones de herramientas  		|Para ver una lista de las integraciones de herramientas admitidas, consulte [Configurar integraciones de herramientas](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}. 		|Las integraciones de herramientas disponibles dependen de cómo se haya configurado {{site.data.keyword.contdelivery_short}} en el entorno. 			|
|Creación de una cadena de herramientas a partir de una plantilla		|Inicie la sesión en [{{site.data.keyword.Bluemix_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://console.ng.bluemix.net/devops){:new_window}		|Inicie la sesión en el entorno dedicado en {{site.data.keyword.Bluemix_notm}}. 			|
|Creación de una cadena de herramientas desde una app		|La app se configura para una entrega continuada desde un nuevo repositorio de GitHub que ya contiene el código de inicio de la app.		|La app se configura para una entrega continua desde un nuevo repositorio de GitHub o GitHub Enterprise que ya contiene el código de inicio de la app.		|  
|Regiones de despliegue de conducto de entrega		|Todas las regiones de {{site.data.keyword.Bluemix_notm}} público están disponibles para los trabajos de despliegue de Cloud Foundry.  		|La región de {{site.data.keyword.Bluemix_notm}} dedicado está disponible. Otras regiones dedicadas o locales dentro de la misma cuenta de cliente también pueden estar disponibles en función de cómo se haya configurado {{site.data.keyword.contdelivery_short}} en el entorno específico.		|
|Trabajos de despliegue de conducto de entrega		|Todos los [tipos de trabajos](/docs/services/ContinuousDelivery/pipeline_about.html#deliverypipeline_jobs) están disponibles.		|Los tipos de trabajos que dependen de servicios de {{site.data.keyword.Bluemix_notm}} que no estén instalados en el entorno dedicado pueden no estar disponibles. Por ejemplo, los tipos de trabajos de despliegue y compilación de contenedores pueden no estar disponibles en entornos que no tengan el servicio {{site.data.keyword.Bluemix_notm}} Container.	|
{: caption="Table 1. Differences between toolchains on {{site.data.keyword.Bluemix_notm}} dedicado y {{site.data.keyword.Bluemix_notm}} público" caption-side="top"}


## Plantillas de cadenas de herramientas
{: #templates}

Puede utilizar una plantilla como punto de partida para [crear una cadena de herramientas ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/devops/create){: new_window}. Las plantillas de cadenas de herramientas incluyen conjuntos específicos de integraciones de herramientas que admiten tareas de desarrollo, despliegue y operaciones. 

**Consejo**: Es posible que el entorno {{site.data.keyword.Bluemix_notm}} dedicado de la empresa no contenga las mismas plantillas de cadenas de herramientas que el sitio de {{site.data.keyword.Bluemix_notm}} público. Las plantillas de cadenas de herramientas que están disponibles tanto en {{site.data.keyword.Bluemix_notm}} público como en {{site.data.keyword.Bluemix_notm}} dedicado pueden contener un conjunto distinto de integraciones de herramientas en {{site.data.keyword.Bluemix_notm}} dedicado. 

Algunas plantillas de cadenas de herramientas incluyen integraciones que forman parte del servicio {{site.data.keyword.contdelivery_short}}. Si su organización aún no tiene ninguna instancia de dicho servicio, cuando pulse **Crear** para crear la cadena de herramientas, el servicio se añadirá automáticamente de forma gratuita. Para obtener más información y ver las condiciones, consulte el [Catálogo de Bluemix ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/catalog/services/continuous-delivery/){:new_window}.

Las plantillas de cadenas de herramientas de microservicios despliegan una app con las API de catálogo y de pedidos que se han copiado en un almacén de Cloudant. Como parte del despliegue de la app, se crea una instancia del servicio Cloudant sin coste alguno. Para obtener más información y ver las condiciones, consulte el [Catálogo de Bluemix ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/catalog/services/cloudant-nosql-db/){:new_window}.

|Plantilla  |Descripción	|
|:----------|:------------------------------|
|[Cadena de herramientas de guía de aprendizaje del método Garage nativo de la nube ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fcloud-native-toolchain-tutorial){:new_window} 		|Esta cadena de herramientas muestra prácticas de DevOps integradas en el método Garage. La cadena de herramientas está preconfigurada para entrega continua, control de código fuente, automatización de pruebas y para supervisión y operaciones automatizadas. Se suministra con una app de ejemplo escrita en Node.js Express 4, que puede ampliar.  		|
|[Cadena de herramientas de microservicios con {{site.data.keyword.DRA_short}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Ftoolchain-demo){:new_window} 		|Con esta cadena de herramientas nativa de la nube puede utilizar una muestra para crear un almacén en línea compuesto por tres microservicios: una API de catálogo, una API de pedidos y una IU que realiza llamadas a ambas API. La cadena de herramientas está preconfigurada para entrega continua, control de código fuente, pruebas funcionales, seguimiento de problemas, edición en línea y notificación de alertas.  		|
|[Cadena de herramientas de microservicios con {{site.data.keyword.DRA_short}} (v2) ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fmicroservices-toolchain-hosted){:new_window} 		|Con esta cadena de herramientas nativa de la nube puede utilizar una muestra para crear un almacén en línea compuesto por tres microservicios: una API de catálogo, una API de pedidos y una IU que realiza llamadas a ambas API. La cadena de herramientas está preconfigurada para entrega continua, control de código fuente, pruebas funcionales, seguimiento de problemas, edición en línea y notificación de alertas.  		|
|[Cadena de herramientas de contenedor seguro ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsecure-container-toolchain){:new_window} 		|Con esta cadena de herramientas puede desarrollar y desplegar una app de contenedor Docker segura. De forma predeterminada, la cadena de herramientas utiliza una app Node.js "Hello World" de ejemplo, pero puede enlazar en su lugar con su propio repositorio GitHub. La cadena de herramientas está preconfigurada para entrega continua con Vulnerability Advisor, control de código fuente, seguimiento de problemas y edición en línea.  		|
|[Cadena de herramientas simple de Cloud Foundry ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsimple-toolchain){:new_window}		|Con esta cadena de herramientas puede desarrollar y desplegar una app de Cloud Foundry. De forma predeterminada, esta cadena de herramientas utiliza una app Node.js "Hello world" de ejemplo, pero puede enlazar en su lugar con su propio repositorio GitHub. La cadena de herramientas está preconfigurada para entrega continua, control de código fuente, seguimiento de problemas y edición en línea.  		|
|[Cadena de herramientas simple de Cloud Foundry (v2) ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsimple-toolchain-hosted){:new_window}	|Con esta cadena de herramientas puede desarrollar y desplegar una app de Cloud Foundry. De forma predeterminada, esta cadena de herramientas clona una app Node.js "Hello world" de ejemplo en un repositorio Git alojado por IBM, que luego puede modificar. La cadena de herramientas está preconfigurada para entrega continua, control de código fuente, seguimiento de problemas y edición en línea.  		|
|[Cadena de herramientas simple de Cloud Foundry con {{site.data.keyword.DRA_short}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdra-toolchain-demo){:new_window}		|Con esta cadena de herramientas nativa de la nube puede utilizar {{site.data.keyword.DRA_short}} para llevar a cabo el despliegue de una app sencilla de Cloud Foundry. De forma predeterminada, esta cadena de herramientas utiliza una app de meteorología Node.js, pero puede enlazar con su propio repositorio GitHub.  		|
|[Cadena de herramientas simple de Container ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsimple-container-toolchain){:new_window}		|Con esta cadena de herramientas puede desarrollar y desplegar una app de contenedor Docker. De forma predeterminada, la cadena de herramientas utiliza una app Node.js "Hello World" de ejemplo, pero puede enlazar en su lugar con su propio repositorio GitHub. La cadena de herramientas está preconfigurada para entrega continua, control de código fuente, seguimiento de problemas y edición en línea.  		|
|[Delivery Insights con despliegue de IBM UrbanCode ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdeliveryinsights-toolchain){:new_window}		|Con esta cadena de herramientas puede ver métricas de despliegue con IBM UrbanCode Deploy. Habilite esta cadena de herramientas para comunicarse con IBM UrbanCode Deploy mediante la descarga y configuración de DevOps Connect desde la página Valores de {{site.data.keyword.DRA_short}}. 		|
|[Deployment Risk Analytics con GitHub y Jenkins ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdevopsinsights-toolchain){:new_window}		|Con esta cadena de herramientas puede ver detalles del proceso Jenkins para la integración y entrega continua. Puede configurar el servidor Jenkins para que envíe datos a {{site.data.keyword.DRA_short}} cuando Jenkins ejecuta los trabajos. También puede implementar mejoras en la calidad para bloquear despliegues en función de políticas. Puede ver los resultados en el panel de control de Deployment Risk de {{site.data.keyword.DRA_short}}. Si configura un repositorio GitHub para indicar el repositorio de origen que utiliza Jenkins, puede cambiar el nivel de rastreo.   		|
|[Developer Insights y Team Dynamics con GitHub y JIRA ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdevteaminsights-toolchain){:new_window}		|Con esta cadena de herramientas, puede explorar el riesgo de despliegue de un proyecto y utilizar un análisis de codificación social para comprender los patrones de interacción entre los desarrolladores. Puede analizar el código fuente de GitHub junto con problemas de GitHub, problemas de JIRA o ambos. Utilice Developer Insights para identificar los archivos muy propensos a errores y para ver si el proyecto cumple con las prácticas de DevOps. El análisis de codificación social en Team Dynamics identifica el nivel de interacción entre miembros del equipo para que el equipo pueda solucionar las prácticas improductivas. 		|
|[Cree su propia cadena de herramientas ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fempty-toolchain){:new_window}		|Esta cadena de herramientas no tiene herramientas preconfiguradas. Si ya está familiarizado con las cadenas de herramientas, puede configurar su propia cadena de herramientas. 		|
{: caption="Table 2. Toolchain templates" caption-side="top"}
