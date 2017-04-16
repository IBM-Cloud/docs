---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configuración de la integración de herramientas
{: #integrations}

Última actualización: 18 de octubre de 2016
{: .last-updated}

Puede configurar integraciones de herramientas que admitan tareas de desarrollo, despliegue y operaciones mientras crea una cadena de herramientas, o bien puede añadir y configurar integraciones de herramientas para personalizar una cadena de herramientas existente.  
{:shortdesc}

**Importante**: En {{site.data.keyword.Bluemix_notm}} Público, las cadenas de herramientas están disponibles únicamente en el sur de EE. UU.

Las integraciones de herramientas que están disponibles para añadirse y configurarse para la cadena de herramientas son distintas en función de si está utilizando cadenas de herramientas en {{site.data.keyword.Bluemix_notm}} Público o {{site.data.keyword.Bluemix_notm}} Dedicado. Si está utilizando cadenas de herramientas en {{site.data.keyword.Bluemix_notm}} Dedicado, las integraciones de herramientas disponibles para usted dependerán de cómo se haya configurado {{site.data.keyword.jazzhub_title}} en el entorno específico.

*Tabla 1. Integraciones de herramientas disponibles para cadenas de herramientas en {{site.data.keyword.Bluemix_notm}} Público y Dedicado*

|Integración de herramientas |Disponible en {{site.data.keyword.Bluemix_notm}} Público	|Disponible en {{site.data.keyword.Bluemix_notm}} Dedicado (dependiente del entorno)|
|:----------|:------------------------------|:------------------|
|{{site.data.keyword.deliverypipeline}} 		|Sí	   	|Sí  		|
|{{site.data.keyword.DRA_short}} 		|Sí		|No			|
|Eclipse Orion {{site.data.keyword.webide}}		|Sí		|Sí			|
|GitHub		|Sí		|Sí		|
|GitHub Enterprise Dedicado			|No		|Sí		|
|Otras herramientas			|Sí		|Sí		|
|PagerDuty			|Sí		|Sí		|
|Sauce Labs		|Sí		|No		|
|Slack			|Sí		|Sí		|

**Consejo**: si desea empezar a desarrollar su propio código en {{site.data.keyword.Bluemix_notm}} Público, configure la integración de herramientas GitHub antes de configurar el {{site.data.keyword.deliverypipeline}}. Si desea empezar a desarrollar su propio código en {{site.data.keyword.Bluemix_notm}} Dedicado, configure la integración de herramientas {{site.data.keyword.ghe_short}} o la integración de herramientas GitHub antes de configurar el {{site.data.keyword.deliverypipeline}}. 


## Configuración del conducto de entrega
{: #deliverypipeline}

El {{site.data.keyword.deliverypipeline}} automatiza el despliegue continuado de los proyectos a través de secuencias de fases que recuperan entradas y ejecutan trabajos, como compilaciones, pruebas y despliegues. 

Configure el {{site.data.keyword.deliverypipeline}} para automatizar la creación, las pruebas y el despliegue automáticos de sus apps: 

1. Si configura la integración de esta herramienta al crear la cadena de herramientas, en la sección Configurable Integrations, pulse **Delivery Pipeline**. En función de la plantilla que utilice, los campos disponibles serán distintos. Revise los valores del campo predeterminado y, si es necesario, realice cambios.
1. Si tiene una cadena de herramientas en {{site.data.keyword.Bluemix_notm}} Público y añade esta integración de herramientas a dicha cadena, en el panel de control DevOps, en la página **Cadenas de herramientas**, pulse la cadena de herramientas para abrir la página Integraciones de herramientas. Como alternativa, en la página Visión general de la aplicación, en el mosaico Continuous Delivery, pulse **Ver cadena de herramientas**. A continuación, pulse **Tool Integrations**. Si utiliza una cadena de herramientas en {{site.data.keyword.Bluemix_notm}} Dedicado, en el Panel de control, en el separador **DEVOPS**, pulse la cadena de herramientas para abrir su página Integraciones de herramientas. Como alternativa, en la esquina superior derecha de la página Visión general de la aplicación, pulse **Ver cadena de herramientas**. A continuación, pulse **Tool Integrations**. 
1. Pulse el botón de adición (+).
1. En la sección Tool Integrations, pulse **Delivery Pipeline**.
1. Especifique un nombre para el nuevo conducto.
1. Si tiene previsto utilizar el conducto para desplegar una interfaz de usuario, seleccione el recuadro de selección **Viewable App**. Todas las apps creadas por el conducto se muestran en la lista **VIEW APP** de la página Tool Integrations de la cadena de herramientas.
1. Pulse **Create Integration** para añadir el {{site.data.keyword.deliverypipeline}} a la cadena de herramientas.
1. Pulse el mosaico para {{site.data.keyword.deliverypipeline}} para ver el conducto y configurarlo. Para obtener información básica sobre cómo configurar un conducto, consulte [Creación y despliegue de conductos (El enlace se abre en una ventana nueva)](../services/DeliveryPipeline/build_deploy.html){: new_window}.

  **Consejo**: si desea activar el conducto al transferir cambios al repositorio (repo) de GitHub o {{site.data.keyword.ghe_short}}, debe configurar GitHub o {{site.data.keyword.ghe_short}} para la cadena de herramientas antes de definir las fases del conducto. Las fases del conducto necesitan los URL Git para los repositorios. Cada fase de conducto puede hacer referencia a un único repositorio de GitHub o {{site.data.keyword.ghe_short}} que esté asociado con la cadena de herramientas. Para obtener instrucciones sobre cómo configurar GitHub, consulte la sección [GitHub](#github). Para obtener instrucciones sobre cómo configurar GitHub Enterprise Dedicado, consulte [Iniciación a {{site.data.keyword.ghe_long}} (El enlace se abre en una ventana nueva)](../services/ghededicated/index.html){: new_window}.
  
1. Opcional: si utiliza una cadena de herramientas en {{site.data.keyword.Bluemix_notm}} Público y desea que Sauce Labs ejecute pruebas en la app, configure el {{site.data.keyword.deliverypipeline}} para añadir el trabajo de pruebas Sauce Labs. Para obtener instrucciones sobre cómo configurar el trabajo de pruebas, consulte [Configuración de un trabajo de pruebas Sauce Labs en el conducto](#config_saucelabs).

### Configuración de un trabajo de pruebas Sauce Labs en el conducto
{: #config_saucelabs}

Antes de configurar un trabajo de pruebas Sauce Labs en el conducto, necesita un conducto de trabajo que incluya fases para crear y desplegar la app, y debe configurar Sauce Labs para su cadena de herramientas. Para obtener instrucciones sobre cómo configurar Sauce Labs, consulte la sección [Sauce Labs](#saucelabs).

Configure el {{site.data.keyword.deliverypipeline}} para añadir un trabajo de pruebas Sauce Labs:

1. Si no tiene ninguna fase que despliegue una versión de pruebas de su app, cree una.
1. En la fase, añada un trabajo de prueba después del trabajo de despliegue. Disponer de estos trabajos en la misma fase permite que accedan al mismo conjunto de propiedades del entorno.   
  ![Trabajo de prueba](images/toolchain_test_job.png) 

1. Configure la fase: 

  a. En el separador **ENVIRONMENT PROPERTIES**, cree tres propiedades: CF_APP_NAME, SAUCE_USERNAME y SAUCE_ACCESS_KEY.
  
  b. Introduzca su nombre de usuario y clave de acceso para Sauce Labs. De este modo, externaliza estos valores para poder utilizarlos en sus pruebas.
  
1. Configure el trabajo de despliegue. En el campo **Deploy Script**, incluya este mandato: `export CF_APP_NAME="$CF_APP"`. Este mandato exporta el nombre de la app como propiedad del entorno.
1. Configure el trabajo de prueba. Los valores de la imagen siguiente son ejemplos. Los campos **Service Instance**, **Target**, **Organization** y **Space** se rellenan con el nombre de usuario de Sauce Labs, la región, la organización y el espacio que se está utilizando.  
![Trabajo de configuración](images/toolchain_configure_job.png)

  a. Para el tipo de prueba, seleccione **Sauce Labs**.
  
  b. Para la instancia de servicio, seleccione el nombre de usuario de Sauce Labs que ha utilizado al configurar Sauce Labs para su cadena de herramientas. 
  
   **Consejo**: para ver el nombre de usuario y la clave de acceso que ha utilizado al configurar Sauce Labs para su cadena de herramientas, pulse **Configurar**. 
  
  c. En el campo **Test Execution Command**, especifique los mandatos que instalan las dependencias necesarias para las pruebas y, a continuación, ejecute las pruebas. Por ejemplo, para una app Node.js, puede introducir estos mandatos:
     ```
     npm install
     node_modules/grunt-cli/bin/grunt test:sauce:parallel
     ```
  
    d. Si desea ver los informes de las pruebas en los registros del trabajo de prueba, seleccione el recuadro de selección **Enable Test Report** y establezca el valor de Test Result File Pattern en `test/*.xml`.
  
1. Pulse **SAVE**. Siempre que se ejecute su conducto, se ejecutarán las pruebas de Sauce Labs.

Para obtener más información, consulte [Conducto de entrega (El enlace se abre en una ventana nueva)](https://www.ibm.com/devops/method/content/deliver/tool_build_and_deploy/){: new_window}.


## Adición de {{site.data.keyword.DRA_short}}
{: #dra}

{{site.data.keyword.DRA_full}} recopila y analiza los resultados de las pruebas de unidad, de las pruebas funcionales y de las herramientas de cobertura de código para determinar si el código cumple los criterios predefinidos en las puertas especificadas del proceso de despliegue. Si el código no cumple o excede los criterios, el despliegue se detiene para evitar la exposición a riesgos. Puede utilizar {{site.data.keyword.DRA_short}} como red de seguridad para el entorno de entrega continuada o como método para implementar y mejorar los estándares de calidad. 

 **Nota**: esta integración de herramientas está preconfigurada. No es necesario configurar ningún parámetro y tampoco es posible modificar la configuración existente.
 
Añada {{site.data.keyword.DRA_short}} para mantener y mejorar la calidad de su código en {{site.data.keyword.Bluemix_notm}} supervisando las implementaciones para identificar los riesgos antes de distribuir la aplicación.

1. Si tiene una cadena de herramientas y añade esta integración de herramienta a dicha cadena, en el panel de control DevOps, en la página **Cadenas de herramientas**, pulse la cadena de herramientas para abrir la página Integraciones de herramientas. Como alternativa, en la página Visión general de la aplicación, en el mosaico Entrega continua, pulse **Ver cadena de herramientas**. A continuación, pulse **Tool Integrations**. 
1. Pulse el botón de adición (+).
1. En la sección Tool Integrations, pulse **Deployment Risk Analytics**. 
1. Pulse **Create Integration**.
1. Pulse el mosaico para {{site.data.keyword.DRA_short}} y, a continuación, complete los primeros pasos: crear criterios, conectar los criterios al conducto y ejecutar el conducto. Para obtener más información, consulte [{{site.data.keyword.DRA_short}} (El enlace se abre en una ventana nueva)](https://www.ibm.com/devops/method/content/deliver/tool_deployment_risk_analytics/){: new_window}.


## Adición de Eclipse Orion {{site.data.keyword.webide}}
{: #webide}

Eclipse Orion {{site.data.keyword.webide}} es un entorno integrado basado en web en el que puede crear, editar, ejecutar, depurar y controlar las tareas de control del código fuente. Puede pasar sin problemas de editar a ejecutar, enviar y desplegar. 

 **Nota**: esta integración de herramientas está preconfigurada. No es necesario configurar ningún parámetro y tampoco es posible modificar la configuración existente.
 
Para completar las tareas de control del código fuente, añada la integración de herramientas Eclipse Orion {{site.data.keyword.webide}}:

1. Si tiene una cadena de herramientas en {{site.data.keyword.Bluemix_notm}} Público y añade esta integración de herramientas a dicha cadena, en el panel de control DevOps, en la página **Cadenas de herramientas**, pulse la cadena de herramientas para abrir la página Integraciones de herramientas. Como alternativa, en la página Visión general de la aplicación, en el mosaico Entrega continua, pulse **Ver cadena de herramientas**. A continuación, pulse **Tool Integrations**. Si utiliza una cadena de herramientas en {{site.data.keyword.Bluemix_notm}} Dedicado, en el Panel de control, en el separador **DEVOPS**, pulse la cadena de herramientas para abrir su página Integraciones de herramientas. Como alternativa, en la esquina superior derecha de la página Visión general de la aplicación, pulse **Ver cadena de herramientas**. A continuación, pulse **Tool Integrations**.
1. Pulse el botón de adición (+).
1. En la sección Tool Integrations, pulse **Eclipse Orion Web IDE**. 
1. Pulse **Create Integration**.
1. Pulse el mosaico para el nuevo Eclipse Orion {{site.data.keyword.webide}}. El espacio de trabajo ya contiene los repositorios de GitHub o {{site.data.keyword.ghe_short}}. Los repositorios que están asociados a la cadena de herramientas actual aparecen resaltados.

Para obtener más información, consulte [Edición de código con Eclipse Orion {{site.data.keyword.webide}} (El enlace se abre en una ventana nueva)](../toolchains/web_ide.html){: new_window}.


## Configuración de GitHub
{: #github}

GitHub es un servicio de alojamiento basado en web para repositorios Git. Puede tener copias locales y remotas de sus repositorios, lo que facilita la colaboración. 

GitHub Issues es una herramienta de seguimiento que mantiene todo su trabajo y sus planificaciones en un mismo lugar. Está integrado con el repositorio de desarrollo de modo que pueda centrarse en las tareas importantes.

Configure GitHub para gestionar el código fuente en la nube:

1. Si configura la integración de esta herramienta mientras crea la cadena de herramientas, siga estos pasos:

 a. En la sección Configurable Integrations, pulse **GitHub**. Si está creando la cadena de herramientas en {{site.data.keyword.Bluemix_notm}} Público y no ha autorizado a {{site.data.keyword.Bluemix_notm}} acceso a GitHub, pulse **Authorize** para ir al sitio web de GitHub. Si no tiene ninguna sesión de GitHub activa, se le solicitará que inicie sesión. Pulse **Authorize Application** para permitir que {{site.data.keyword.Bluemix_notm}} acceda a su cuenta de GitHub. Si tiene una sesión activa de GitHub pero no ha introducido recientemente su contraseña, es posible que se le solicite que introduzca la contraseña de GitHub para confirmarla.
 
 b. Revise las ubicaciones de repositorio de destino predeterminadas para el repositorio de GitHub. Dichos repositorios se clonan a partir del repositorio de ejemplo. Si es necesario, cambie el nombre de los repositorios de destino.
 ![Ubicaciones de repositorio de destino predeterminadas](images/toolchain_github_config.png)
   
1. Si tiene una cadena de herramientas y añade esta integración de herramienta a dicha cadena, en el panel de control DevOps, en la página **Cadenas de herramientas**, pulse la cadena de herramientas para abrir la página Integraciones de herramientas. Como alternativa, en la página Visión general de la aplicación, en el mosaico Entrega continua, pulse **Ver cadena de herramientas**. A continuación, pulse **Tool Integrations**. 
1. Pulse el botón de adición (+).
1. En la sección Tool Integrations, pulse **GitHub**.
1. Si tiene un repositorio de GitHub y desea utilizarlo, escriba el URL. Para el tipo de repositorio, pulse **Link**.
1. Si desea utilizar un repositorio nuevo de GitHub, escriba un nombre para el repositorio de GitHub, escriba el URL del repositorio que está clonando o bifurcando y seleccione el tipo de repositorio: 

 a. Para crear un repositorio vacío, pulse **New**. 
 
 b. Para crear una copia de un repositorio de GitHub, pulse **Clone**.
 
 c. Para bifurcar un repositorio de GitHub de modo que pueda aportar cambios a través de todas las solicitudes de extracción, pulse **Fork**.
 
1. Si desea utilizar GitHub Issues para realizar un seguimiento de los problemas, seleccione el recuadro de selección **Enable GitHub Issues**.
1. Pulse **Create Integration**.
1. Pulse el mosaico del repositorio de GitHub con el que desee trabajar. Se abrirá el sitio web de GitHub, donde puede ver el contenido del repositorio.
 
  **Consejo**: puede utilizar estas herramientas integradas de gestión del código fuente en Eclipse Orion {{site.data.keyword.webide}} para editar el repositorio de GitHub y desplegar una app desde su espacio de trabajo.

1. Si ha habilitado GitHub Issues, pulse el mosaico de GitHub Issues para abrirlo.

Para obtener más información, consulte [GitHub (El enlace se abre en una ventana nueva)](https://www.ibm.com/devops/method/content/code/tool_github/){: new_window} y [GitHub Issues (El enlace se abre en una ventana nueva)](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}.


## Configuración de GitHub Enterprise Dedicado
{: #configghe}

{{site.data.keyword.ghe_long}} es un servicio de alojamiento basado en web para repositorios Git. GitHub Enterprise Dedicado es únicamente para clientes de {{site.data.keyword.Bluemix_notm}} Dedicado. GitHub Issues es una herramienta de seguimiento que mantiene todo su trabajo y sus planificaciones en un mismo lugar. Está integrado con el repositorio de desarrollo de modo que pueda centrarse en las tareas importantes. Para obtener más información sobre GitHub Enterprise Dedicado y GitHub Issues, consulte [Uso de GitHub Enterprise Dedicado (El enlace se abre en una ventana nueva)](../services/ghededicated/index.html){: new_window} y [GitHub Issues (El enlace se abre en una ventana nueva)](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}.

Puede configurar {{site.data.keyword.ghe_short}} como una integración de herramientas de la cadena de herramientas para que pueda gestionar el código fuente en la instancia de [{{site.data.keyword.Bluemix_notm}} Dedicado de la empresa (El enlace se abre en una ventana nueva)](../dedicated/index.html#dedicated){: new_window}.

1. Si configura la integración de esta herramienta mientras crea la cadena de herramientas, siga estos pasos:

 a. Antes de iniciar sesión en GitHub Enterprise Dedicado por primera vez, pida al administrador de región de su empresa que añada su ID de usuario a la instancia de {{site.data.keyword.Bluemix_notm}} Dedicado desde el registro de usuario de la empresa utilizando LDAP. Para obtener información sobre cómo configurar la cuenta de {{site.data.keyword.ghe_short}}, consulte [Uso de GitHub Enterprise Dedicado (El enlace se abre en una ventana nueva)](../services/ghededicated/index.html){: new_window}.
 
 b. En la sección Configurable Integrations, pulse **{{site.data.keyword.ghe_short}}**.    
 
 c. Revise el nombre predeterminado para el nuevo repositorio de {{site.data.keyword.ghe_short}}. Si es necesario, cambie el nombre del repositorio nuevo. La siguiente imagen muestra un ejemplo de un repositorio clonado desde un repositorio de ejemplo. Puede utilizar un repositorio existente o uno nuevo. Para utilizar un repositorio nuevo, puede crear un repositorio vacío, clonarlo o bifurcarlo. 
 ![Ubicaciones de repositorio predeterminado](images/toolchain_ghe_config.png)
   
1. Si tiene una cadena de herramientas en {{site.data.keyword.Bluemix_notm}} Público y añade esta integración de herramientas a dicha cadena, en el panel de control DevOps, en la página **Cadenas de herramientas**, pulse la cadena de herramientas para abrir la página Integraciones de herramientas. Como alternativa, en la página Visión general de la aplicación, en el mosaico Continuous Delivery, pulse **Ver cadena de herramientas**. A continuación, pulse **Tool Integrations**. Si utiliza una cadena de herramientas en {{site.data.keyword.Bluemix_notm}} Dedicado, en el Panel de control, en el separador **DEVOPS**, pulse la cadena de herramientas para abrir su página Integraciones de herramientas. Como alternativa, en la esquina superior derecha de la página Visión general de la aplicación, pulse **Ver cadena de herramientas**. A continuación, pulse **Tool Integrations**.
1. Pulse el botón de adición (+).
1. En la sección Tool Integrations, pulse **{{site.data.keyword.ghe_short}}**.
1. Si tiene un repositorio de {{site.data.keyword.ghe_short}} que desea utilizar, escriba el URL para el repositorio. Para el tipo de repositorio, pulse **Existing**.
1. Si desea utilizar un repositorio nuevo de {{site.data.keyword.ghe_short}}, escriba un nombre para el repositorio, escriba el URL del repositorio que está clonando o bifurcando y seleccione el tipo de repositorio: 

 a. Para crear un repositorio vacío, pulse **New**. 
 
 b. Para crear una copia de un repositorio, pulse **Clone**.
 
 c. Para bifurcar un repositorio de modo que pueda aportar cambios a través de todas las solicitudes de extracción, pulse **Fork**.
 
1. Para utilizar GitHub Issues para realizar un seguimiento de los problemas, seleccione el recuadro de selección **Enable GitHub Issues**.
1. Pulse **Create Integration**.
1. Pulse el mosaico del repositorio de {{site.data.keyword.ghe_short}} con el que desee trabajar. Se abrirá la instancia de [{{site.data.keyword.Bluemix_notm}} Dedicado de la empresa (El enlace se abre en una ventana nueva)](../dedicated/index.html#dedicated){: new_window}, donde puede ver el contenido del repositorio.
 
  **Consejo**: puede utilizar estas herramientas integradas de gestión del código fuente en Eclipse Orion {{site.data.keyword.webide}} para editar el repositorio de {{site.data.keyword.ghe_short}} y desplegar una app desde su espacio de trabajo.

1. Si ha habilitado GitHub Issues, pulse el mosaico de GitHub Issues.

<!-- 8/23/2016: The GHE Dedicated content has been moved to docs-staging/services/ghededicated/index.md -->

## Configuración de una herramienta personalizada (Otras herramientas)
{: #othertool}

Si el equipo utiliza una herramienta no incluida en la lista de integraciones de las cadenas de herramientas, puede integrar una herramienta personalizada. 

Configure una herramienta personalizada para que funcione con otras herramientas de la cadena de herramientas y que esté disponible para el equipo:
1. Si configura la integración de esta herramienta al crear la cadena de herramientas, en la sección Configurable Integrations, pulse **Other Tool**.

1. Si tiene una cadena de herramientas y añade esta integración de herramienta a dicha cadena, en el panel de control DevOps, en la página **Cadenas de herramientas**, pulse la cadena de herramientas para abrir la página Integraciones de herramientas. Como alternativa, en la página Visión general de la aplicación, en el mosaico Entrega continua, pulse **Ver cadena de herramientas**. A continuación, pulse **Tool Integrations**.
1. Pulse el botón de adición (+).
1. En la sección Tool Integrations, pulse **Other Tool**.
1. Escriba el nombre de la herramienta.
1. Seleccione la fase del Ciclo de vida que esté asociada de forma más cercana con la herramienta. La elección de la fase del ciclo de vida determina en qué categoría está listada la herramienta en la página Toolchains Integrations.
1. Añada un URL de icono. El icono aparecerá en la tarjeta de integración de la herramienta.
1. Añada un URL de documentación.
1. Especifique un nombre de instancia de la herramienta. Por ejemplo: My Team Tool.
1. Añada un URL de instancia de herramienta. Pulsar la tarjeta de integración de la herramienta le llevará al URL que liste para la instancia de herramientas.
1. Añada una descripción de la herramienta.
1. (Avanzado) Añada propiedades adicional si es necesario. Por ejemplo, liste cualquier información o atributos necesarios para que la herramienta se integre con otras herramientas en la cadena de herramientas.  
1. Pulse **Create Integration**.

## Configuración de PagerDuty
{: #pagerduty}

PagerDuty integra datos de varios sistemas de supervisión en una única vista. Cuando se produce un problema, PagerDuty se asegura de que el miembro del equipo más adecuado para corregirlo reciba una notificación. Si el miembro del equipo no responde al problema, pueden configurarse sistemas de escalado para pasar el problema a ingenieros o gestores de operaciones secundarios.

Configure PagerDuty para enviar notificaciones cuando se producen errores en la fase de conducto para que pueda corregir los problemas con mayor celeridad y reducir el tiempo de inactividad:

1. Si configura la integración de esta herramienta al crear la cadena de herramientas, en la sección Configurable Integrations, pulse **PagerDuty**.
1. Si tiene una cadena de herramientas y añade esta integración de herramienta a dicha cadena, en el panel de control DevOps, en la página **Cadenas de herramientas**, pulse la cadena de herramientas para abrir la página Integraciones de herramientas. Como alternativa, en la página Visión general de la aplicación, en el mosaico Entrega continua, pulse **Ver cadena de herramientas**. A continuación, pulse **Tool Integrations**. 
1. Pulse el botón de adición (+).
1. En la sección Tool Integrations, pulse **PagerDuty**.
1. Escriba el nombre del sitio de PagerDuty asociado con su cuenta de PagerDuty. Si no tiene ninguna cuenta de PagerDuty, [regístrese en una (El enlace se abre en una ventana nueva)](https://signup.pagerduty.com/accounts/new){: new_window}.
1. Escriba la clave de acceso de API para su cuenta de PagerDuty. Para obtener instrucciones sobre cómo encontrar la clave, consulte [Autenticación de API (El enlace se abre en una ventana nueva)](https://signup.pagerduty.com/accounts/new){: new_window}.
1. Escriba el nombre del servicio PagerDuty.
1. Escriba la dirección de correo electrónico del contacto principal de PagerDuty.
1. Escriba el número de teléfono del contacto principal de PagerDuty.
1. Pulse **Create Integration**.
1. Pulse el mosaico de PagerDuty para ir a pagerduty.com. Puede ver los sucesos asociados con el servicio PagerDuty que ha especificado al configurar la integración de esta herramienta para su cadena de herramientas. 

Para obtener más información, consulte [PagerDuty (El enlace se abre en una ventana nueva)](https://www.ibm.com/devops/method/content/manage/tool_pagerduty/){: new_window}.


## Configuración de Sauce Labs
{: #saucelabs}

Sauce Labs ejecuta pruebas de unidad funcionales. Cuando se configura una suite de pruebas de Sauce Labs como trabajo de pruebas en {{site.data.keyword.deliverypipeline}}, la suite de pruebas puede ejecutar pruebas para la app web o móvil como parte del proceso de entrega continuo. Estas pruebas pueden proporcionar un control de flujo muy valioso para los proyectos, y actuar como pasarelas para evitar el despliegue de código defectuoso.

Configure Sauce Labs para ejecutar pruebas funcionales automatizadas en varios sistemas operativos y navegadores a fin de poder emular el modo en que el usuario puede utilizar un sitio web o una aplicación:

1. Si configura la integración de esta herramienta al crear la cadena de herramientas, en la sección Configurable Integrations, pulse **Sauce Labs**.
1. Si tiene una cadena de herramientas y añade esta integración de herramienta a dicha cadena, en el panel de control DevOps, en la página **Cadenas de herramientas**, pulse la cadena de herramientas para abrir la página Integraciones de herramientas. Como alternativa, en la página Visión general de la aplicación, en el mosaico Entrega continua, pulse **Ver cadena de herramientas**. A continuación, pulse **Tool Integrations**. 
1. Pulse el botón de adición (+).
1. En la sección Tool Integrations, pulse **Sauce Labs**.
1. Escriba el nombre de usuario asociado con su cuenta de Sauce Labs. Puede [encontrar su nombre de usuario en el mensaje de bienvenida de la parte superior de la página de la cuenta de Sauce Labs (El enlace se abre en una ventana nueva)](https://saucelabs.com/account){: new_window}.
1. Escriba la clave de acceso para su cuenta de Sauce Labs. Puede [encontrar la clave en la página de la cuenta de Sauce Labs (El enlace se abre en una ventana nueva)](https://saucelabs.com/account){: new_window}.
1. Pulse **Create Integration**.
1. Pulse el mosaico de Sauce Labs para ir a saucelabs.com y verla actividad de prueba para la cadena de herramientas.

 **Consejo**: si ha añadido un trabajo de pruebas de Sauce Labs al {{site.data.keyword.deliverypipeline}}, puede seleccionar la instancia del servicio.

Para obtener más información, consulte [Sauce Labs (El enlace se abre en una ventana nueva)](https://www.ibm.com/devops/method/content/code/tool_sauce_labs/){: new_window}.


## Configuración de Slack
{: #slack}

**Importante**: las notificaciones que se publican en canales Slack públicos son visibles para todas las personas del equipo. Recuerde que es responsable de todo el contenido que publique.

Slack es un sistema de notificaciones y mensajería en tiempo real y basado en la nube. Slack proporciona una función de chat permanente, que es una alternativa más interactiva que el correo electrónico para facilitar la colaboración del equipo. Puede comunicarse con su equipo en un canal dedicado o en un conjunto de canales directamente relacionados con su trabajo. Asimismo, puede compartir archivos e imágenes a través de los canales o a través de mensajes directos entre dos o más personas. Las comunicaciones en los mensajes directos y en los canales se conservan para poder realizar búsquedas. 

Configure Slack para recibir notificaciones acerca de su cadena de herramientas desde las integraciones de herramientas, como actividades de prueba y de despliegue:

1. Si configura la integración de esta herramienta al crear la cadena de herramientas, en la sección Configurable Integrations, pulse **Slack**.
1. Si tiene una cadena de herramientas y añade esta integración de herramienta a dicha cadena, en el panel de control DevOps, en la página **Cadenas de herramientas**, pulse la cadena de herramientas para abrir la página Integraciones de herramientas. Como alternativa, en la página Visión general de la aplicación, en el mosaico Entrega continua, pulse **Ver cadena de herramientas**. A continuación, pulse **Tool Integrations**.
1. Pulse el botón de adición (+).
1. En la sección Tool Integrations, pulse **Slack**.
1. Escriba la señal de autenticación de API para su cuenta de Slack. Debe utilizar la señal con acceso completo garantizado para autenticarse con Slack. Para obtener instrucciones sobre cómo encontrar la señal, consulte [Autenticación de Slack (El enlace se abre en una ventana nueva)](https://api.slack.com/web#authentication){: new_window}.
1. Escriba el nombre del canal Slack al que desea enviar las notificaciones. Si el canal que intenta especificar no existe, se crea. Si el canal se ha archivado, se reactiva.
1. Pulse **Create Integration**.
1. Pulse el mosaico de Slack. Puede ver toda la actividad de su cadena de herramientas en el canal Slack configurado.

Para obtener más información, consulte [Slack (El enlace se abre en una ventana nueva)](https://www.ibm.com/devops/method/content/culture/tool_slack/){: new_window}.








