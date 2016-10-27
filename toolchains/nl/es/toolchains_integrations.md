---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configuración de integraciones de herramientas
{: #integrations}

Última actualización: 13 de septiembre de 2016
{: .last-updated}

Puede configurar integraciones de herramientas que soporten tareas de desarrollo, despliegue y operaciones mientras crea una cadena de herramientas, o bien puede añadir y configurar integraciones de herramientas para personalizar una cadena de herramientas existente.  
{:shortdesc}

**Importante**: esta funcionalidad es experimental. Las cadenas de herramientas pueden no ser estables y es posible que cambien de modo que no sean compatibles con versiones anteriores. No se recomienda utilizarlas en entornos de producción. En {{site.data.keyword.Bluemix_notm}} público, las cadenas de herramientas están disponibles solo en la región EE.UU. sur.

Las integraciones de herramientas que están disponibles para añadirse y configurarse para su cadena de herramientas varían en función de si las cadenas de herramientas se utilizan en {{site.data.keyword.Bluemix_notm}} público o {{site.data.keyword.Bluemix_notm}} dedicado.

*Tabla 1. Integraciones de herramientas disponibles para cadenas de herramientas en {{site.data.keyword.Bluemix_notm}} público y dedicado*

|Integración de herramientas |Disponible en {{site.data.keyword.Bluemix_notm}} público	|Disponible en {{site.data.keyword.Bluemix_notm}} dedicado|
|:----------|:------------------------------|:------------------|
|{{site.data.keyword.deliverypipeline}} 		|Sí	   	|Sí  		|
|{{site.data.keyword.DRA_short}} 		|Sí		|No			|
|Eclipse Orion {{site.data.keyword.webide}}		|Sí		|Sí			|
|GitHub		|Sí		|No		|
|Dedicated GitHub Enterprise			|No		|Sí		|
|PagerDuty			|Sí		|No		|
|Sauce Labs		|Sí		|No		|
|Slack			|Sí		|No		|

**Consejo**: si desea empezar a desarrollar con su código fuente en {{site.data.keyword.Bluemix_notm}} público, configure la integración de herramientas en GitHub antes de configurar {{site.data.keyword.deliverypipeline}}. Si desea empezar a desarrollar con su código en {{site.data.keyword.Bluemix_notm}} dedicado, configure la integración de herramientas de {{site.data.keyword.ghe_short}} antes de configurar {{site.data.keyword.deliverypipeline}}. 


## Configuración del conducto de entrega
{: #deliverypipeline}

El {{site.data.keyword.deliverypipeline}} automatiza el despliegue continuado de los proyectos a través de secuencias de fases que recuperan entradas y ejecutan trabajos, como compilaciones, pruebas y despliegues. 

Configure el {{site.data.keyword.deliverypipeline}} para automatizar la creación, las pruebas y el despliegue automáticos de sus apps: 

1. Si configura la integración de esta herramienta al crear la cadena de herramientas, en la sección Configurable Integrations, pulse **Delivery Pipeline**. En función de la plantilla que utilice, los campos disponibles serán distintos. Revise los valores del campo predeterminado y, si es necesario, realice cambios.
1. Si tiene una cadena de herramientas en {{site.data.keyword.Bluemix_notm}} público y le está añadiendo esta integración de herramientas, en el panel de instrumentos de DevOps, en el separador **Cadenas de herramientas**, pulse la cadena de herramientas para abrir la página Integraciones de herramientas correspondiente. Si lo prefiere, en la página Visión general de la app, mosaico Entrega continua, pulse **Ver cadena de herramientas**. A continuación, pulse **Integraciones de herramientas**. Si está utilizando una cadena de herramientas en {{site.data.keyword.Bluemix_notm}} dedicado, en el panel de control, en la pestaña **DEVOPS**, pulse la cadena de herramientas para abrir la página Integraciones de herramientas correspondiente.Si lo prefiere, en la esquina superior derecha de la página Visión general de la app, pulse **Ver cadena de herramientas**. A continuación, pulse **Integraciones de herramientas**. 
1. Pulse el botón de adición (+).
1. En la sección Tool Integrations, pulse **Delivery Pipeline**.
1. Especifique un nombre para el nuevo conducto.
1. Si tiene previsto utilizar un conducto para desplegar una interfaz de usuario, marque el recuadro de selección **App visibles**. Todas las apps creadas por el conducto se muestran en la lista **VIEW APP** de la página Tool Integrations de la cadena de herramientas.
1. Pulse **Create Integration** para añadir el {{site.data.keyword.deliverypipeline}} a la cadena de herramientas.
1. Pulse el mosaico de {{site.data.keyword.deliverypipeline}} para ver el conducto y configurarlo. Para obtener información básica sobre como configurar un conducto, consulte [Creación y despliegue de conductos](../services/DeliveryPipeline/build_deploy.html){: new_window}.

  **Consejo**: si desea activar el conducto al transferir cambios a GitHub o al repositorio de {{site.data.keyword.ghe_short}}, debe configurar GitHub o {{site.data.keyword.ghe_short}} para la cadena de herramientas antes de definir las fases del conducto.
Las fases del conducto necesitan los URL Git para el repositorio. Cada fase de conducto puede hacer referencia a un único GitHub o repositorio de {{site.data.keyword.ghe_short}} que esté asociado con la cadena de herramientas. Para obtener instrucciones sobre la configuración de GitHub, consulte la sección [GitHub](#github). Para obtener más información sobre la configuración de Dedicated GitHub Enterprise, consulte [Iniciación a {{site.data.keyword.ghe_long}}](../services/ghededicated/index.html){: new_window}.
  
1. Opcional: si está utilizando una cadena de herramientas en {{site.data.keyword.Bluemix_notm}} público y desea que Sauce Labs ejecute pruebas en su app, configure el {{site.data.keyword.deliverypipeline}} para añadir un trabajo de prueba de Sauce Labs. Para obtener instrucciones sobre cómo configurar el trabajo de pruebas, consulte [Configuración de un trabajo de pruebas Sauce Labs en el conducto](#config_saucelabs).

### Configuración de un trabajo de pruebas Sauce Labs en el conducto
{: #config_saucelabs}

Antes de configurar un trabajo de pruebas Sauce Labs en el conducto, necesita un conducto de trabajo que incluya fases para crear y desplegar la app, y debe configurar Sauce Labs para su cadena de herramientas. Para obtener instrucciones sobre cómo configurar Sauce Labs, consulte la sección [Sauce Labs](#saucelabs).

Configure el {{site.data.keyword.deliverypipeline}} para añadir un trabajo de pruebas Sauce Labs:

1. Si no tiene ninguna fase que despliegue una versión de pruebas de su app, cree una.
1. En la fase, añada un trabajo de prueba después del trabajo de despliegue. Disponer de estos trabajos en la misma fase permite que accedan al mismo conjunto de propiedades del entorno.
![Trabajo de prueba](images/toolchain_test_job.png) 

1. Configure la fase: 

  a. En la pestaña **ENVIRONMENT PROPERTIES**, cree tres propiedades: CF_APP_NAME, SAUCE_USERNAME y SAUCE_ACCESS_KEY.
  
  b. Introduzca su nombre de usuario y clave de acceso para Sauce Labs. De este modo, externaliza estos valores para poder utilizarlos en sus pruebas.
  
1. Configure el trabajo de despliegue. En el campo **Deploy Script**, incluya este mandato: `export CF_APP_NAME="$CF_APP"`. Este mandato exporta el nombre de la app como propiedad del entorno.
1. Configure el trabajo de prueba. Los valores de la siguiente imagen son ejemplos. Los campos **Service Instance**, **Target**, **Organization** y **Space** se rellenan con el nombre de usuario de Sauce Labs, la región, la organización y el espacio que se está utilizando actualmente.
![Trabajo de configuración](images/toolchain_configure_job.png)

  a. Para el tipo de prueba, seleccione **Sauce Labs**.
  
  b. Para la instancia de servicio, seleccione el nombre de usuario de Sauce Labs que ha utilizado al configurar Sauce Labs para su cadena de herramientas. 
  
   **Consejo**: para ver el nombre de usuario y la clave de acceso que ha utilizado al configurar Sauce Labs para su cadena de herramientas, pulse **Configurar**. 
  
  c. En el campo **Test Execution Command**, especifique los mandatos que instalan las dependencias necesarias para las pruebas y, a continuación, ejecute las pruebas. Por ejemplo para una app Node.js, podría especificar los siguientes mandatos:
     ```
     npm install
     node_modules/grunt-cli/bin/grunt test:sauce:parallel
     ```
  
    d. Si desea ver los informes de prueba en los registros del trabajo de prueba, seleccione la casilla **Habilitar informe de prueba** y establezca el patrón de archivo de resultados de prueba en `test/*.xml`.
  
1. Pulse **GUARDAR**. Cuando se ejecute el conducto, se ejecutarán las pruebas de Sauce Labs.

Para obtener más información, consulte [Delivery Pipeline](https://www.ibm.com/devops/method/content/deliver/tool_build_and_deploy/){: new_window}.


## Adición de {{site.data.keyword.DRA_short}}
{: #dra}

{{site.data.keyword.DRA_full}} recopila y analiza los resultados de pruebas de unidad, pruebas funcionales y herramientas de cobertura de código para determinar si el código cumple los criterios predefinidos en las puertas especificadas del proceso de despliegue. Si el código no cumple o supera los criterios, el despliegue se detiene para evitar la exposición a riesgos. Puede utilizar {{site.data.keyword.DRA_short}} como red de seguridad para su entorno de entrega continua o como método para implementar y mejorar los estándares de calidad. 

 **Nota**: esta integración de herramientas está preconfigurada. No se requieren otros parámetros de configuración y no se puede volver a configurar.
 
Añada {{site.data.keyword.DRA_short}} para mantener y mejorar la calidad del código en {{site.data.keyword.Bluemix_notm}} supervisando los despliegues para identificar los riesgos antes de que se propaguen.

1. Si tiene una cadena de herramientas y le está añadiendo esta integración de herramientas, en el panel de instrumentos de DevOps, en el separador **Cadenas de herramientas**, pulse la cadena de herramientas para abrir la página Integraciones de herramientas correspondiente. Si lo prefiere, en la página Visión general de la app, mosaico Entrega continua, pulse **Ver cadena de herramientas**. A continuación, pulse **Integraciones de herramientas**. 
1. Pulse el botón de adición (+).
1. En la sección Integraciones de herramientas, pulse **Deployment Risk Analytics**. 
1. Pulse **Crear integración**.
1. Pulse el mosaico de {{site.data.keyword.DRA_short}} y complete los pasos de iniciación: crear criterios, conectar los criterios con el conducto y ejecutar el conducto. Para obtener más información, consulte [{{site.data.keyword.DRA_short}}](https://www.ibm.com/devops/method/content/deliver/tool_deployment_risk_analytics/){: new_window}.


## Adición de Eclipse Orion {{site.data.keyword.webide}}
{: #webide}

El entorno Eclipse Orion {{site.data.keyword.webide}} es un entorno basado en web integrado donde se pueden crear, editar, ejecutar, depurar y completar tareas de control de origen. Puede cambiar sin problemas entre la edición, la ejecución, el envío y el despliegue. 

 **Nota**: esta integración de herramientas está preconfigurada. No se requieren otros parámetros de configuración y no se puede volver a configurar.
 
Para completar las tareas de control de origen, añada la integración de la herramienta Eclipse Orion {{site.data.keyword.webide}}:

1. Si tiene una cadena de herramientas en {{site.data.keyword.Bluemix_notm}} público y le está añadiendo esta integración de herramientas, en el panel de instrumentos de DevOps, en el separador **Cadenas de herramientas**, pulse la cadena de herramientas para abrir la página Integraciones de herramientas correspondiente. Si lo prefiere, en la página Visión general de la app, mosaico Entrega continua, pulse **Ver cadena de herramientas**. A continuación, pulse **Integraciones de herramientas**. Si está utilizando una cadena de herramientas en {{site.data.keyword.Bluemix_notm}} dedicado, en el panel de control, en la pestaña **DEVOPS**, pulse la cadena de herramientas para abrir la página Integraciones de herramientas correspondiente.Si lo prefiere, en la esquina superior derecha de la página Visión general de la app, pulse **Ver cadena de herramientas**. A continuación, pulse **Integraciones de herramientas**.
1. Pulse el botón de adición (+).
1. En la sección Integraciones de herramientas, pulse **Eclipse Orion Web IDE**. 
1. Pulse **Crear integración**.
1. Pulse el mosaico del nuevo Eclipse Orion {{site.data.keyword.webide}}. El espacio de trabajo ya contiene los repositorios de GitHub o {{site.data.keyword.ghe_short}}. Los repositorios que están asociados con la cadena de herramientas actual están resaltados.

Para obtener más información, consulte [Edición de código con Eclipse Orion {{site.data.keyword.webide}}](../toolchains/web_ide.html){: new_window}.


## Configuración de GitHub
{: #github}

GitHub es un servicio de alojamiento basado en web para repositorios Git. Puede tener tanto copias locales como remotas de sus repositorios, lo cual facilita la colaboración. 

GitHub Issues es una herramienta de rastreo que conserva en un único lugar su trabajo y sus planes. Se integra con el repositorio de desarrollo de forma que se pueda centrar en tareas importantes.

Configure GitHub para gestionar el código fuente en la nube:

1. Si está configurando esta integración de herramientas a medida que crea la cadena de herramientas, siga estos pasos:

 a. En la sección Configurable Integrations, pulse **GitHub**. Si no ha autorizado a {{site.data.keyword.Bluemix_notm}} el acceso a GitHub, pulse **Autorizar** para ir al sitio web de GitHub. Si no tiene ninguna sesión de GitHub activa, se le solicitará que inicie sesión. Pulse **Autorizar aplicación** para permitir a {{site.data.keyword.Bluemix_notm}} el acceso a la cuenta de GitHub. Si tiene una sesión de GitHub activa, pero no ha introducido la contraseña recientemente, es posible que se le solicite la contraseña de GitHub para confirmar.
 
 b. Revise las ubicaciones del repositorio de destino predeterminadas de los repositorios de GitHub. Estos repositorios se clonan a partir de los repositorios de ejemplo. Si es necesario, cambie los nombres de los repositorios de destino.
![Ubicaciones del repositorio de destino predeterminado](images/toolchain_github_config.png)
   
1. Si tiene una cadena de herramientas y le está añadiendo esta integración de herramientas, en el panel de instrumentos de DevOps, en el separador **Cadenas de herramientas**, pulse la cadena de herramientas para abrir la página Integraciones de herramientas correspondiente. Si lo prefiere, en la página Visión general de la app, mosaico Entrega continua, pulse **Ver cadena de herramientas**. A continuación, pulse **Integraciones de herramientas**. 
1. Pulse el botón de adición (+).
1. En la sección Integraciones de herramientas, pulse **GitHub**.
1. Si tiene un repositorio de GitHub y desea utilizarlo, escriba el URL. Para el tipo de repositorio, pulse **Enlace**.
1. Si desea utilizar un repositorio nuevo de GitHub, escriba un nombre para el repositorio de GitHub, escriba el URL del repositorio que está clonando o bifurcando y seleccione el tipo de repositorio: 

 a. Para crear un repositorio vacío, pulse **Nuevo**. 
 
 b. Para crear una copia de un repositorio de GitHub, pulse **Clonar**.
 
 c. Para bifurcar un repositorio de GitHub de forma que pueda aportar cambios a través de solicitudes de extracción, pulse **Bifurcar**.
 
1. Si desea utilizar GitHub's Issues para realizar un seguimiento de problemas, seleccione la casilla **Habilitar GitHub Issues**.
1. Pulse **Crear integración**.
1. Pulse el mosaico del repositorio de GitHub con el que desee trabajar. El sitio web de GitHub se abre y muestra el contenido del repositorio.
 
  **Consejo**: puede utilizar las herramientas de gestión de código fuente integrado en Eclipse Orion {{site.data.keyword.webide}} para editar el repositorio de GitHub y desplegar una aplicación desde el espacio de trabajo.

1. Si ha habilitado GitHub Issues, pulse el mosaico de GitHub Issues para abrirlo.

Para obtener más información, consulte [GitHub](https://www.ibm.com/devops/method/content/code/tool_github/){: new_window} y [GitHub Issues](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}.


## Configuración de Dedicated GitHub Enterprise
{: #configghe}

{{site.data.keyword.ghe_long}} es un servicio de alojamiento basado en web local para repositorios Git. Dedicated GitHub Enterprise es de uso exclusivo para los clientes de {{site.data.keyword.Bluemix_notm}} dedicado. GitHub Issues es una herramienta de rastreo que conserva en un único lugar su trabajo y sus planes. Se integra con el repositorio de desarrollo de forma que se pueda centrar en tareas importantes. Para obtener más información sobre Dedicated GitHub Enterprise y GitHub Issues, consulte [Uso de Dedicated GitHub Enterprise](../services/ghededicated/index.html){: new_window} y [GitHub Issues](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}.

Puede configurar {{site.data.keyword.ghe_short}} como una integración de herramientas en su cadena de herramientas para poder gestionar el código fuente en la instancia de [{{site.data.keyword.Bluemix_notm}} dedicado](../dedicated/index.html#dedicated){: new_window} de su empresa.

1. Si está configurando esta integración de herramientas a medida que crea la cadena de herramientas, siga estos pasos:

 a. Antes de iniciar sesión en Dedicated GitHub Enterprise por primera vez, solicite al administrador de su zona de la empresa que añada su ID de usuario a la instancia de {{site.data.keyword.Bluemix_notm}} dedicado desde el registro de usuarios de la compañía utilizando LDAP. Para obtener más información sobre la configuración de la cuenta de {{site.data.keyword.ghe_short}}, consulte [Uso de Dedicated GitHub Enterprise](../services/ghededicated/index.html){: new_window}.
 
 b. En la sección Configurable Integrations, pulse **{{site.data.keyword.ghe_short}}**.    
 
 c. Revise el nombre predeterminado del nuevo repositorio de {{site.data.keyword.ghe_short}}. Si es necesario, cambie el nombre del repositorio nuevo.
La siguiente imagen muestra un ejemplo de un repositorio clonado a partir de un repositorio de ejemplo. Puede utilizar un repositorio existente o uno nuevo. Para utilizar un repositorio nuevo, puede crear un repositorio vacío, clonar un repositorio o bifurcar un repositorio. ![Ubicaciones del repositorio predeterminado](images/toolchain_ghe_config.png)
   
1. Si tiene una cadena de herramientas en {{site.data.keyword.Bluemix_notm}} público y le está añadiendo esta integración de herramientas, en el panel de instrumentos de DevOps, en el separador **Cadenas de herramientas**, pulse la cadena de herramientas para abrir la página Integraciones de herramientas correspondiente. Si lo prefiere, en la página Visión general de la app, mosaico Entrega continua, pulse **Ver cadena de herramientas**. A continuación, pulse **Integraciones de herramientas**. Si está utilizando una cadena de herramientas en {{site.data.keyword.Bluemix_notm}} dedicado, en el panel de control, en la pestaña **DEVOPS**, pulse la cadena de herramientas para abrir la página Integraciones de herramientas correspondiente.Si lo prefiere, en la esquina superior derecha de la página Visión general de la app, pulse **Ver cadena de herramientas**. A continuación, pulse **Integraciones de herramientas**.
1. Pulse el botón de adición (+).
1. En la sección Integraciones de herramientas, pulse **{{site.data.keyword.ghe_short}}**.
1. Si tiene un repositorio de {{site.data.keyword.ghe_short}} y desea utilizarlo, escriba el URL correspondiente. Para el tipo de repositorio, pulse **Existente**.
1. Si desea utilizar un nuevo repositorio de {{site.data.keyword.ghe_short}}, escriba un nombre para el repositorio, escriba el URL del repositorio que está clonando o bifurcando y seleccione el tipo de repositorio: 

 a. Para crear un repositorio vacío, pulse **Nuevo**. 
 
 b. Para crear una copia de un repositorio, pulse **Clonar**.
 
 c. Para bifurcar un repositorio de forma que pueda aportar cambios a través de solicitudes de extracción, pulse **Bifurcar**.
 
1. Para utilizar GitHub Issues para realizar un seguimiento de problemas, seleccione la casilla **Habilitar GitHub Issues**.
1. Pulse **Crear integración**.
1. Pulse el mosaico del repositorio de {{site.data.keyword.ghe_short}} con el que desee trabajar. Se abrirá la instancia de [{{site.data.keyword.Bluemix_notm}} dedicado](../dedicated/index.html#dedicated){: new_window} de su compañía, donde podrá ver el contenido del repositorio.
 
  **Consejo**: puede utilizar las herramientas de gestión de código fuente integrado en Eclipse Orion {{site.data.keyword.webide}} para editar el repositorio de {{site.data.keyword.ghe_short}} y desplegar una aplicación desde el espacio de trabajo.

1. Si ha habilitado GitHub Issues, pulse el mosaico de GitHub Issues.

<!-- 8/23/2016: The GHE Dedicated content has been moved to docs-staging/services/ghededicated/index.md -->

## Configuración de PagerDuty
{: #pagerduty}

PagerDuty integra datos de varios sistemas de supervisión en una única vista. Cuando se produce un problema, PagerDuty garantiza que el miembro del equipo que está más capacitado para arreglarlo en ese momento reciba una notificación. Si el miembro del equipo no responde al problema, se pueden configurar escalados para direccionarlo a ingenieros o gestores de operaciones secundarios.

Configure PagerDuty para que envíe notificaciones cuando se produzcan anomalías en la etapa de conducto de manera que se puedan solucionar los problemas más rápidamente y reducir el tiempo de inactividad:

1. Si está configurando esta integración de herramientas a medida que crea la cadena de herramientas, en la sección Configurable Integrations, pulse **PagerDuty**.
1. Si tiene una cadena de herramientas y le está añadiendo esta integración de herramientas, en el panel de instrumentos de DevOps, en el separador **Cadenas de herramientas**, pulse la cadena de herramientas para abrir la página Integraciones de herramientas correspondiente. Si lo prefiere, en la página Visión general de la app, mosaico Entrega continua, pulse **Ver cadena de herramientas**. A continuación, pulse **Integraciones de herramientas**. 
1. Pulse el botón de adición (+).
1. En la sección Integraciones de herramientas, pulse **PagerDuty**
1. Escriba el nombre de sitio de PagerDuty que está asociado a su cuenta de PagerDuty. Si no tiene cuenta de PagerDuty, [regístrese para obtener una](https://signup.pagerduty.com/accounts/new){: new_window}.
1. Escriba la clave de acceso de API para su cuenta de PagerDuty. Para obtener instrucciones sobre cómo encontrar la clave, consulte [Autenticación de API](https://signup.pagerduty.com/accounts/new){: new_window}.
1. Escriba el nombre del servicio PagerDuty.
1. Escriba la dirección de correo electrónico del contacto principal de PagerDuty.
1. Escriba el número de teléfono del contacto principal de PagerDuty.
1. Pulse **Crear integración**.
1. Pulse el mosaico de PagerDuty para ir a pagerduty.com. Puede ver los sucesos que están asociados con el servicio PagerDuty especificado al configurar esta integración de herramientas para la cadena de herramientas. 

Para obtener más información, consulte [PagerDuty](https://www.ibm.com/devops/method/content/manage/tool_pagerduty/){: new_window}.


## Configuración de Sauce Labs
{: #saucelabs}

Sauce Labs ejecuta pruebas de unidad funcional. Cuando se configura una suite de pruebas de Sauce Labs como trabajo de pruebas en {{site.data.keyword.deliverypipeline}}, la suite de pruebas puede ejecutar pruebas para la app web o móvil como parte del proceso de entrega continuo. Estas pruebas pueden proporcionar un control de flujo muy valioso para los proyectos, y actuar como pasarelas para evitar el despliegue de código defectuoso.

Configure Sauce Labs para ejecutar pruebas funcionales automatizadas en varios sistemas operativos y navegadores a fin de poder emular el modo en que el usuario puede utilizar un sitio web o una aplicación:

1. Si configura la integración de esta herramienta al crear la cadena de herramientas, en la sección Configurable Integrations, pulse **Sauce Labs**.
1. Si tiene una cadena de herramientas y le está añadiendo esta integración de herramientas, en el panel de instrumentos de DevOps, en el separador **Cadenas de herramientas**, pulse la cadena de herramientas para abrir la página Integraciones de herramientas correspondiente. Si lo prefiere, en la página Visión general de la app, mosaico Entrega continua, pulse **Ver cadena de herramientas**. A continuación, pulse **Integraciones de herramientas**. 
1. Pulse el botón de adición (+).
1. En la sección Tool Integrations, pulse **Sauce Labs**.
1. Escriba el nombre de usuario que está asociado a su cuenta de Sauce Labs. Puede [encontrar su nombre de usuario en el mensaje de bienvenida de la parte superior de la página de la cuenta de Sauce Labs](https://saucelabs.com/account){: new_window}.
1. Escriba la clave de acceso de su cuenta de Sauce Labs. [Encontrara la clave en la esquina inferior izquierda de la página de la cuenta de Sauce Labs](https://saucelabs.com/account){: new_window}.
1. Pulse **Crear integración**.
1. Pulse el título de Sauce Labs para ir a saucelabs.com y verla actividad de prueba para la cadena de herramientas.

 **Consejo**: si ha añadido un trabajo de pruebas de Sauce Labs al {{site.data.keyword.deliverypipeline}}, puede seleccionar la instancia del servicio.

Para obtener más información, consulte [Sauce Labs](https://www.ibm.com/devops/method/content/code/tool_sauce_labs/){: new_window}.


## Configuración de Slack
{: #slack}

**Importante**: las notificaciones que se publican en canales Slack públicos son visibles para todas las personas del equipo. Recuerde que es responsable de todo el contenido que publique.

Slack es un sistema de notificaciones y mensajería en tiempo real y basado en la nube. Slack proporciona una función de chat permanente, que es una alternativa más interactiva que el correo electrónico para facilitar la colaboración del equipo. Puede comunicarse con su equipo en un canal dedicado o en un conjunto de canales directamente relacionados con su trabajo. Asimismo, puede compartir archivos e imágenes a través de los canales o a través de mensajes directos entre dos o más personas. Las comunicaciones en los mensajes directos y en los canales se conservan para poder realizar búsquedas. 

Configure Slack para recibir notificaciones acerca de su cadena de herramientas desde las integraciones de herramientas, como actividades de prueba y de despliegue:

1. Si configura la integración de esta herramienta al crear la cadena de herramientas, en la sección Configurable Integrations, pulse **Slack**.
1. Si tiene una cadena de herramientas y le está añadiendo esta integración de herramientas, en el panel de instrumentos de DevOps, en el separador **Cadenas de herramientas**, pulse la cadena de herramientas para abrir la página Integraciones de herramientas correspondiente. Si lo prefiere, en la página Visión general de la app, mosaico Entrega continua, pulse **Ver cadena de herramientas**. A continuación, pulse **Integraciones de herramientas**.
1. Pulse el botón de adición (+).
1. En la sección Tool Integrations, pulse **Slack**.
1. Escriba la señal de autenticación de la API de la cuenta de Slack. Debe utilizar la señal con acceso completo garantizado para autenticarse con Slack. Para obtener instrucciones sobre cómo encontrar la señal, consulte [Configuración de Slack](https://api.slack.com/web#authentication){: new_window}.
1. Escriba el nombre del canal Slack al que desea enviar las notificaciones. Si el canal que intenta especificar no existe, se crea. Si el canal se ha archivado, se reactiva.
1. Pulse **Crear integración**.
1. Pulse el mosaico de Slack. Puede ver toda la actividad de su cadena de herramientas en el canal Slack configurado.

Para obtener más información, consulte [Slack](https://www.ibm.com/devops/method/content/culture/tool_slack/){: new_window}.
