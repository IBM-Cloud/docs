---

copyright:
  years: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Iniciación a las cadenas de herramientas (Beta)
{: #toolchains_getting_started}

Última actualización: 7 de octubre de 2016
{: .last-updated}  

Las cadenas de herramientas están disponibles en los entornos Público y Dedicado en {{site.data.keyword.Bluemix}}. Una cadena de herramientas se puede crear de dos formas: mediante una plantilla o a partir de una app. En {{site.data.keyword.Bluemix_notm}} Público, las cadenas de herramientas están disponibles únicamente en el sur de EE. UU.
{: shortdesc}

##Iniciación a las cadenas de herramientas: Público
{: #getting_started_public}

**Nota:** Asegúrese de que está trabajando en la experiencia de New Bluemix comprobando el banner superior.

 * Si ve un mensaje sobre probar el nuevo Bluemix, estará trabajando en la experiencia de Classic Bluemix. Pulse el enlace para abrir la experiencia de New Bluemix.
 * Si no ve dicho mensaje, ya estará trabajando en la experiencia de New Bluemix.

Cada cadena de herramientas está asociada con una organización (org) específica y cualquier usuario que sea miembro de dicha organización puede acceder a las cadenas de herramientas asociadas. Para poder crear una cadena de herramientas, asegúrese de que está trabajando en la organización donde desea crear la cadena de herramientas. La organización en la que está trabajando actualmente se muestra en la barra de menús. Para conmutar a otra organización, pulse la organización en la barra de menús y, a continuación, seleccione la organización a la que desea conmutar.

###Creación de una cadena de herramientas a partir de una plantilla   
{: #creating_a_toolchain_from_a_template}

Puede utilizar una plantilla como punto de partida para crear una cadena de herramientas que incluya un conjunto específico de integraciones de herramientas.

1. Si está creando su primera cadena de herramientas, asegúrese de que las cadenas de herramientas estén habilitadas en su organización:
   1. Abra el panel de control de DevOps y pulse la página **Toolchains**.
   2. Si se muestra el botón **Enable Toolchains**, púlselo y siga las solicitudes para crear la cadena de herramientas.
   3. Si no se muestra el botón **Enable Toolchains**, las cadenas de herramientas ya estarán habilitadas. Continúe con el paso 2.
1. En el panel de control de DevOps, en la página **Toolchains**, pulse el botón add (+) para crear una cadena de herramientas.
1. Pulse la plantilla de la cadena de herramientas. Por ejemplo, para utilizar un ejemplo de tienda en línea para crear la cadena de herramientas, pulse **Microservices toolchain**. 
1. En la página de creación de la cadena de herramientas, revise el diagrama de la cadena de herramientas que se dispone a crear. El diagrama muestra cada integración de herramienta en su fase de ciclo en la cadena de herramientas. El diagrama de la imagen siguiente es un ejemplo. Al crear una cadena de herramientas, el diagrama muestra cada una de las integraciones de herramienta que forma parte de la cadena de herramientas.
![Diagrama de cadena de herramientas](images/toolchain_diagram.png)

1. Revise la información predeterminada para la configuración de la cadena de herramientas. El nombre de la cadena de herramientas la identifica en {{site.data.keyword.Bluemix_notm}}. Si ya tiene una cadena de herramientas con dicho nombre, o si desea utilizar otro nombre, cambie el nombre de la cadena de herramientas.  
1. En la sección Configurable Integrations, seleccione cada una de las integraciones de herramienta para las que desee configurar su cadena de herramientas. Algunas integraciones de herramientas no necesitan configuración. Para obtener información sobre cómo configurar las integraciones de herramientas, consulte [Configurar integraciones de herramientas (El enlace se abre en una ventana nueva)](../toolchains/toolchains_integrations.html){: new_window}.
1. Pulse **Create**.  Para configurar la cadena de herramientas, se ejecutan varios pasos automáticamente:

 * Se crea la cadena de herramientas.
 * Si ha configurado la integración de la herramienta Delivery Pipeline, los conductos se activan.
 * Si ha configurado la integración de la herramienta Sauce Labs, la integración de Sauce Labs se configura para añadir trabajos a los conductos y ejecutar pruebas.
 * Si ha configurado la integración de la herramienta PagerDuty, la integración de PagerDuty se configura para enviar notificaciones al canal configurado en Slack. Estas notificaciones indican cuándo se produce el problema.
 * Si ha configurado la integración de la herramienta Slack, la integración de Slack se configura para enviar notificaciones al canal configurado en Slack. Estas notificaciones indican el progreso del despliegue; por ejemplo, `Connected with Project XYZ`, `Pipeline Configured` y `Stage 'build' started`.
 * Si ha configurado la integración de la herramienta GitHub, el repositorio de ejemplo de GitHub se clona en su cuenta de GitHub.


###Creación de una cadena de herramientas a partir de una app
{: #creating_a_toolchain_from_an_app}

Puede crear una cadena de herramientas desde la app. La cadena de herramientas puede admitir tareas continuadas de desarrollo, despliegue, supervisión, etc., y está asociada con su app. Cada app puede asociarse a una cadena de herramientas. Cuando se envían los cambios al repositorio de GitHub de la cadena de herramientas, el conducto crea y despliega automáticamente la app.  

1. Si está creando su primera cadena de herramientas, asegúrese de que las cadenas de herramientas estén habilitadas en su organización:
   1. Abra el panel de control de DevOps y pulse la página **Toolchains**.
   2. Si se muestra el botón **Enable Toolchains**, púlselo y siga las solicitudes para crear la cadena de herramientas.
   3. Si no se muestra el botón **Enable Toolchains**, las cadenas de herramientas ya estarán habilitadas. Continúe con el paso 2.
1. En la página Visión general de la app, en el mosaico Continuous Delivery, pulse **Enable**. Como alternativa, en {{site.data.keyword.Bluemix_notm}} Classic Experience, en la esquina superior derecha de la página Visión general de la app, pulse **Añadir cadena de herramientas**. La app se configura para una entrega continuada desde un nuevo repositorio de GitHub que ya contiene el código de inicio de la app.
1. En la página de creación de la cadena de herramientas, revise el diagrama de la cadena de herramientas que se dispone a crear. El diagrama muestra cada integración de herramienta en su fase de ciclo en la cadena de herramientas.
1. Revise la información predeterminada para la configuración de la cadena de herramientas. El nombre de la cadena de herramientas la identifica en {{site.data.keyword.Bluemix_notm}}. Si ya tiene una cadena de herramientas con dicho nombre, o si desea utilizar otro nombre, cambie el nombre de la cadena de herramientas.
1. En la sección Configurable Integrations, seleccione cada una de las integraciones de herramienta para las que desee configurar su cadena de herramientas. Algunas integraciones de herramientas no necesitan configuración. Para obtener información sobre cómo configurar las integraciones de herramientas, consulte [Configurar integraciones de herramientas (El enlace se abre en una ventana nueva)](../toolchains/toolchains_integrations.html){: new_window}.
1. Pulse **Create**.  Para configurar la cadena de herramientas, se ejecutan varios pasos automáticamente:

 * Se crea la cadena de herramientas.
 * Si ha configurado la integración de la herramienta Delivery Pipeline, los conductos se activan.
 * Si ha configurado la integración de la herramienta Sauce Labs, la integración de Sauce Labs se configura para añadir trabajos a los conductos y ejecutar pruebas.
 * Si ha configurado la integración de la herramienta PagerDuty, la integración de PagerDuty se configura para enviar notificaciones al canal configurado en Slack. Estas notificaciones indican cuándo se produce el problema.
 * Si ha configurado la integración de la herramienta Slack, la integración de Slack se configura para enviar notificaciones al canal configurado en Slack. Estas notificaciones indican el progreso del despliegue; por ejemplo, `Connected with Project XYZ`, `Pipeline Configured` y `Stage 'build' started`.
 * Si ha configurado la integración de la herramienta GitHub, el repositorio de ejemplo de GitHub se clona en su cuenta de GitHub.


##Iniciación a las cadenas de herramientas: Dedicado
{: #getting_started_dedicated}

Cada cadena de herramientas está asociada con una organización (org) específica y cualquier usuario que sea miembro de dicha organización puede acceder a las cadenas de herramientas asociadas. Para poder crear una cadena de herramientas, pulse el icono **{{site.data.keyword.avatar}}** ![Icono de avatar](../icons/i-avatar-icon.svg) en la barra de menús para abrir el widget de Cuenta y soporte y ver la organización en la que está trabajando. Si dicha organización no es la misma en la que desea crear la cadena de herramientas, conmute a otra organización.

###Creación de una cadena de herramientas a partir de una plantilla   
{: #creating_a_toolchain_from_a_template_dedicated}

Puede utilizar una plantilla como punto de partida para crear una cadena de herramientas que incluya un conjunto específico de integraciones de herramientas.

1. Si está creando su primera cadena de herramientas, asegúrese de que las cadenas de herramientas estén habilitadas en su organización:
   1. Abra el panel de control de DevOps y pulse el separador **Toolchains**.
   2. Si se muestra el botón **Enable Toolchains**, púlselo y siga las solicitudes para crear la cadena de herramientas.
   3. Si no se muestra el botón **Enable Toolchains**, las cadenas de herramientas ya estarán habilitadas. Continúe con el paso 2.
1. En el panel de control de {{site.data.keyword.Bluemix_notm}}, en el separador **DEVOPS**, pulse el botón add (+) para crear una cadena de herramientas.
1. Pulse la plantilla de la cadena de herramientas. Por ejemplo, para crear una cadena de herramientas simple para desplegar una nueva app de Cloud Foundry, pulse **Cadena de herramientas simple de Cloud Foundry**. 
1. En la página de creación de la cadena de herramientas, revise el diagrama de la cadena de herramientas que se dispone a crear. El diagrama muestra cada integración de herramienta en su fase de ciclo en la cadena de herramientas. El diagrama de la imagen siguiente es un ejemplo. Al crear una cadena de herramientas, el diagrama muestra cada una de las integraciones de herramienta que forma parte de la cadena de herramientas.
![Diagrama de cadena de herramientas dedicada](images/toolchain_dedicated_diagram.png)

1. Revise la información predeterminada para la configuración de la cadena de herramientas. El nombre de la cadena de herramientas la identifica en {{site.data.keyword.Bluemix_notm}}. Si ya tiene una cadena de herramientas con dicho nombre, o si desea utilizar otro nombre, cambie el nombre de la cadena de herramientas.  
1. En la sección Configurable Integrations, seleccione cada una de las integraciones de herramienta para las que desee configurar su cadena de herramientas. Algunas integraciones de herramientas no necesitan configuración. Para obtener información sobre cómo configurar las integraciones de herramientas, consulte [Configurar integraciones de herramientas (El enlace se abre en una ventana nueva)](../toolchains/toolchains_integrations.html){: new_window}.
1. Pulse **Create**.  Para configurar la cadena de herramientas, se ejecutan varios pasos automáticamente:

 * Se crea la cadena de herramientas.
 * Si ha configurado la integración de la herramienta Delivery Pipeline, los conductos se activan.
 * Si ha configurado la integración de herramientas de GitHub Enterprise, el repositorio de ejemplo de GitHub Enterprise se clona en su cuenta de GitHub Enterprise.


###Creación de una cadena de herramientas a partir de una app
{: #creating_a_toolchain_from_an_app_dedicated}

Puede crear una cadena de herramientas desde la app. La cadena de herramientas puede admitir tareas continuadas de desarrollo, despliegue, supervisión, etc., y está asociada con su app. Cada app puede asociarse a una cadena de herramientas. Cuando se envían los cambios al repositorio de GitHub Enterprise de la cadena de herramientas, el conducto crea y despliega automáticamente la app.  

1. Si está creando su primera cadena de herramientas, asegúrese de que las cadenas de herramientas estén habilitadas en su organización:
   1. Abra el panel de control de DevOps y pulse el separador **Toolchains**.
   2. Si se muestra el botón **Enable Toolchains**, púlselo y siga las solicitudes para crear la cadena de herramientas.
   3. Si no se muestra el botón **Enable Toolchains**, las cadenas de herramientas ya estarán habilitadas. Continúe con el paso 2.
1. En la esquina superior derecha de la página Visión general de la aplicación, pulse **Añadir cadena de herramientas**. La app se configura para una entrega continuada desde un nuevo repositorio de GitHub Enterprise que ya contiene el código de inicio de la app.
1. En la página de creación de la cadena de herramientas, revise el diagrama de la cadena de herramientas que se dispone a crear. El diagrama muestra cada integración de herramienta en su fase de ciclo en la cadena de herramientas.
1. Revise la información predeterminada para la configuración de la cadena de herramientas. El nombre de la cadena de herramientas la identifica en {{site.data.keyword.Bluemix_notm}}. Si ya tiene una cadena de herramientas con dicho nombre, o si desea utilizar otro nombre, cambie el nombre de la cadena de herramientas.
1. En la sección Configurable Integrations, seleccione cada una de las integraciones de herramienta para las que desee configurar su cadena de herramientas. Algunas integraciones de herramientas no necesitan configuración. Para obtener información sobre cómo configurar las integraciones de herramientas, consulte [Configurar integraciones de herramientas (El enlace se abre en una ventana nueva)](../toolchains/toolchains_integrations.html){: new_window}.
1. Pulse **Create**.  Para configurar la cadena de herramientas, se ejecutan varios pasos automáticamente:

 * Se crea la cadena de herramientas.
 * Si ha configurado la integración de la herramienta Delivery Pipeline, los conductos se activan.
 * Si ha configurado la integración de herramientas de GitHub Enterprise, el repositorio de ejemplo de GitHub Enterprise se clona en su cuenta de GitHub Enterprise.


##Visualización de una cadena de herramientas
{: #viewing_a_toolchain}

Una vez que se ha configurado la cadena de herramientas y sus integraciones de herramientas, es posible obtener una representación visual de la cadena de herramientas en la página Tool Integrations.

* Si utiliza {{site.data.keyword.Bluemix_notm}} Público, en el panel de control DevOps, en la página **Toolchains**, pulse una cadena de herramientas para abrir su página Tool Integrations. Como alternativa, en la página Visión general de la aplicación, en el mosaico Entrega continua, pulse **Ver cadena de herramientas**. A continuación, pulse **Tool Integrations**. 
   
* Si utiliza {{site.data.keyword.Bluemix_notm}} Dedicado, en el Panel de control, en el separador **DEVOPS**, pulse la cadena de herramientas para abrir su página Tool Integrations. Como alternativa, en la esquina superior derecha de la página Visión general de la aplicación, pulse **Ver cadena de herramientas**.

* Para acceder a una integración de herramienta de su cadena de herramientas, pulse el mosaico de la herramienta. 
 
 **Consejo**: si tiene más de un repositorio de GitHub o GitHub Enterprise, es posible que tenga varios mosaicos para la misma integración de herramienta porque cada repositorio está representado por su propio mosaico.


 <!-- The toolchain in the following image is an example. When you create your own toolchain, the visual representation of the toolchain shows the tool integrations that you configure.
![Sample toolchain](images/toolchain.png) -->


# Enlaces relacionados
{: #rellinks}

## Guías de aprendizaje y ejemplos
{: #samples}

* [Crear una aplicación con tres microservicios (Beta) (El enlace se abre en una ventana nueva)](https://www.ibm.com/devops/method/tutorials/tutorial_microservices_part1){:new_window}
* [Crear una cadena de herramientas desde una plantilla en {{site.data.keyword.Bluemix_notm}} Dedicado (Beta) (El enlace se abre en una ventana nueva)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_template_flow){:new_window}
* [Crear una cadena de herramientas desde una app en {{site.data.keyword.Bluemix_notm}} Dedicado (Beta) (El enlace se abre en una ventana nueva)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_app_flow){:new_window}

## Enlaces relacionados
{: #general}

* [Cadena de herramientas de microservicios (Beta) (El enlace se abre en una ventana nueva)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Cadena de herramientas simple (Beta) (El enlace se abre en una ventana nueva)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM Bluemix Garage Method (El enlace se abre en una ventana nueva)](https://www.ibm.com/devops/method){:new_window}
