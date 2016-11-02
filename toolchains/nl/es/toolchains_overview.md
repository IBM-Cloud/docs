---

copyright:
  years: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Iniciación a las cadenas de herramientas (Experimental)
{: #toolchains_getting_started}

Última actualización: 17 de agosto de 2016
{: .last-updated}  

Las cadenas de herramientas están disponibles en los entornos públicos y dedicados en {{site.data.keyword.Bluemix}}. Puede crear una cadena de herramientas de dos maneras: utilizando una plantilla para crear la cadena de herramientas o creando una cadena de herramientas desde una app.
{: shortdesc}

**Importante**: esta funcionalidad es experimental. Las cadenas de herramientas pueden no ser estables y es posible que cambien de modo que no sean compatibles con versiones anteriores. No se recomienda utilizarlas en entornos de producción. En {{site.data.keyword.Bluemix_notm}} público, las cadenas de herramientas están disponibles solo en la región EE.UU. sur.


##Iniciación a las cadenas de herramientas: público
{: #getting_started_public}

Cada cadena de herramientas está asociada con una organización (org) específica y cualquier usuario que sea miembro de la organización en cuestión puede acceder a las cadenas de herramientas asociadas correspondientes. Antes de crear una cadena de herramientas, asegúrese de estar trabajando en la organización donde sea crear la cadena de herramientas. Para cambiar a otra organización, pulse el icono **{{site.data.keyword.avatar}}** ![icono Avatar](../icons/i-avatar-icon.svg) en la barra de menús para abrir el widget Cuenta y soporte.

###Creación de una cadena de herramientas a partir de una plantilla   
{: #creating_a_toolchain_from_a_template}

Puede utilizar una plantilla como punto de partida para crear una cadena de herramientas que incluya un conjunto específico de integraciones de herramientas.

1. Si está creando su primera cadena de herramientas, asegúrese de que las cadenas de herramientas estén habilitadas en su organización:
   1. Abra el panel de instrumentos de DevOps y pulse la pestaña **Cadenas de herramientas**.
   2. Si se muestra el botón **Habilitar cadenas de herramientas**, púlselo y siga las instrucciones para crear la cadena de herramientas.
   3. Si no se muestra el botón **Habilitar cadenas de herramientas**, significa que las cadenas de herramientas ya están habilitadas. Continúe con el paso 2. 
1. En el panel de control de DevOps, pestaña **Cadenas de herramientas**, pulse el botón de adición (+) para crear una cadena de herramientas.
1. Pulse una plantilla de cadena de herramientas. Por ejemplo, para utilizar un ejemplo de almacén en línea para crear la cadena de herramientas, pulse **Cadena de herramientas de microservicios**. 
1. En la página de creación de cadenas de herramientas, revise el diagrama de la cadena de herramientas que está a punto de crear. El diagrama muestra cada integración de herramientas en la fase del ciclo de vida correspondiente en la cadena de herramientas. El diagrama de la siguiente imagen es un ejemplo. Cuando cree una cadena de herramientas, el diagrama mostrará cada integración de herramientas que forma parte de la cadena de herramientas.
![Diagrama Cadena de herramientas](images/toolchain_diagram.png)

1. Revise la información predeterminada para los valores de la cadena de herramientas. El nombre de la cadena de herramientas la identifica en {{site.data.keyword.Bluemix_notm}}. Si ya existe una cadena de herramientas con el mismo nombre, o si desea utilizar otro, cambie el nombre de la cadena de herramientas.  
1. En la sección Configurable Integrations, seleccione las integraciones de herramientas que desee configurar para su cadena de herramientas.Algunas integraciones de herramientas no requieren ninguna configuración. Para obtener más información sobre las integraciones de herramientas, consulte [Configuración de integraciones de herramientas](../toolchains/toolchains_integrations.html){: new_window}.
1. Pulse **Crear**.  Para configurar la cadena de herramientas, se ejecutan varios pasos automáticamente:

 * Se crea la cadena de herramientas.
 * Si ha configurado la integración de herramientas de Delivery Pipeline, se desencadenan los conductos.
 * Si ha configurado la integración de herramientas de Sauce Labs, se configura la integración de Sauce Labs para añadir trabajos a los conductos y ejecutar pruebas.
 * Si ha configurado la integración de herramientas de PagerDuty, se configura la integración de PagerDuty para enviar notificaciones al canal configurado en Slack. Estas notificaciones indican la aparición de un problema.
 * Si ha configurado la integración de herramientas de Slack, se configura la integración de Slack para enviar notificaciones al canal configurado en Slack. Estas notificaciones indican el progreso del despliegue; por ejemplo, `Connected with Project XYZ`, `Pipeline Configured` y `Stage 'build' started`.
 * Si ha configurado la integración de herramientas de GitHub, el repositorio de GitHub de ejemplo se clona en su cuenta de GitHub.


###Creación de una cadena de herramientas desde una app
{: #creating_a_toolchain_from_an_app}

Puede crear una cadena de herramientas desde su app. La cadena de herramientas puede soportar tareas continuas de desarrollo, despliegue, supervisión, etc. y está asociada con su app. Cada app se puede asociar con una cadena de herramientas. Cuando se envían los cambios al repositorio de GitHub de la cadena de herramientas, el conducto crea y despliega automáticamente la app.  

1. Si está creando su primera cadena de herramientas, asegúrese de que las cadenas de herramientas estén habilitadas en su organización:
   1. Abra el panel de instrumentos de DevOps y pulse la pestaña **Cadenas de herramientas**.
   2. Si se muestra el botón **Habilitar cadenas de herramientas**, púlselo y siga las instrucciones para crear la cadena de herramientas.
   3. Si no se muestra el botón **Habilitar cadenas de herramientas**, significa que las cadenas de herramientas ya están habilitadas. Continúe con el paso 2. 
1. En la página Visión general de la app, mosaico Entrega continua, pulse **Añadir cadena de herramientas**. Si lo prefiere, en {{site.data.keyword.Bluemix_notm}} Classic Experience, en la esquina superior derecha de la página Visión general de la app, pulse **Añadir cadena de herramientas**. Su app se ha configurado para entrega continua desde un nuevo repositorio de GitHub que se llena con código de inicio de la app.
1. En la página de creación de cadenas de herramientas, revise el diagrama de la cadena de herramientas que está a punto de crear. El diagrama muestra cada integración de herramientas en la fase del ciclo de vida correspondiente en la cadena de herramientas. 
1. Revise la información predeterminada para los valores de la cadena de herramientas. El nombre de la cadena de herramientas la identifica en {{site.data.keyword.Bluemix_notm}}. Si ya existe una cadena de herramientas con el mismo nombre, o si desea utilizar otro, cambie el nombre de la cadena de herramientas.
1. En la sección Configurable Integrations, seleccione las integraciones de herramientas que desee configurar para su cadena de herramientas.Algunas integraciones de herramientas no requieren ninguna configuración. Para obtener más información sobre las integraciones de herramientas, consulte [Configuración de integraciones de herramientas](../toolchains/toolchains_integrations.html){: new_window}.
1. Pulse **Crear**.  Para configurar la cadena de herramientas, se ejecutan varios pasos automáticamente:

 * Se crea la cadena de herramientas.
 * Si ha configurado la integración de herramientas de Delivery Pipeline, se desencadenan los conductos.
 * Si ha configurado la integración de herramientas de Sauce Labs, se configura la integración de Sauce Labs para añadir trabajos a los conductos y ejecutar pruebas.
 * Si ha configurado la integración de herramientas de PagerDuty, se configura la integración de PagerDuty para enviar notificaciones al canal configurado en Slack. Estas notificaciones indican la aparición de un problema.
 * Si ha configurado la integración de herramientas de Slack, se configura la integración de Slack para enviar notificaciones al canal configurado en Slack. Estas notificaciones indican el progreso del despliegue; por ejemplo, `Connected with Project XYZ`, `Pipeline Configured` y `Stage 'build' started`.
 * Si ha configurado la integración de herramientas de GitHub, el repositorio de GitHub de ejemplo se clona en su cuenta de GitHub.


##Iniciación a las cadenas de herramientas: dedicado
{: #getting_started_dedicated}

Cada cadena de herramientas está asociada con una organización (org) específica y cualquier usuario que sea miembro de la organización en cuestión puede acceder a las cadenas de herramientas asociadas correspondientes. Antes de crear una cadena de herramientas, pulse el icono **{{site.data.keyword.avatar}}** ![icono de Avatar](../icons/i-avatar-icon.svg) en la barra de menús para abrir el widget Cuenta y soporte y ver la organización en la que está trabajando. Si la organización no es la organización en la que desea crear la cadena de herramientas, cambie a otra.

###Creación de una cadena de herramientas a partir de una plantilla   
{: #creating_a_toolchain_from_a_template_dedicated}

Puede utilizar una plantilla como punto de partida para crear una cadena de herramientas que incluya un conjunto específico de integraciones de herramientas.

1. Si está creando su primera cadena de herramientas, asegúrese de que las cadenas de herramientas estén habilitadas en su organización:
   1. Abra el panel de instrumentos de DevOps y pulse la pestaña **Cadenas de herramientas**.
   2. Si se muestra el botón **Habilitar cadenas de herramientas**, púlselo y siga las instrucciones para crear la cadena de herramientas.
   3. Si no se muestra el botón **Habilitar cadenas de herramientas**, significa que las cadenas de herramientas ya están habilitadas. Continúe con el paso 2.
1. En el panel de control de {{site.data.keyword.Bluemix_notm}}, en la pestaña **DEVOPS**, pulse el botón de adición (+) para crear una cadena de herramientas.
1. Pulse una plantilla de cadena de herramientas. Por ejemplo, para crear una cadena de herramientas simple para desplegar una nueva aplicación de Cloud Foundry, pulse **Cadena de herramientas simple de Cloud Foundry**. 
1. En la página de creación de cadenas de herramientas, revise el diagrama de la cadena de herramientas que está a punto de crear. El diagrama muestra cada integración de herramientas en la fase del ciclo de vida correspondiente en la cadena de herramientas. El diagrama de la siguiente imagen es un ejemplo. Cuando cree una cadena de herramientas, el diagrama mostrará cada integración de herramientas que forma parte de la cadena de herramientas.
![Diagrama de cadena de herramientas dedicada](images/toolchain_dedicated_diagram.png)

1. Revise la información predeterminada para los valores de la cadena de herramientas. El nombre de la cadena de herramientas la identifica en {{site.data.keyword.Bluemix_notm}}. Si ya existe una cadena de herramientas con el mismo nombre, o si desea utilizar otro, cambie el nombre de la cadena de herramientas.  
1. En la sección Configurable Integrations, seleccione las integraciones de herramientas que desee configurar para su cadena de herramientas.Algunas integraciones de herramientas no requieren ninguna configuración. Para obtener más información sobre las integraciones de herramientas, consulte [Configuración de integraciones de herramientas](../toolchains/toolchains_integrations.html){: new_window}.
1. Pulse **Crear**.  Para configurar la cadena de herramientas, se ejecutan varios pasos automáticamente:

 * Se crea la cadena de herramientas.
 * Si ha configurado la integración de herramientas de Delivery Pipeline, se desencadenan los conductos.
 * Si ha configurado la integración de herramientas de GitHub Enterprise, el repositorio de GitHub Enterprise de ejemplo se clona en su cuenta de GitHub Enterprise.


###Creación de una cadena de herramientas desde una app
{: #creating_a_toolchain_from_an_app_dedicated}

Puede crear una cadena de herramientas desde su app. La cadena de herramientas puede soportar tareas continuas de desarrollo, despliegue, supervisión, etc. y está asociada con su app. Cada app se puede asociar con una cadena de herramientas. Cuando se envían los cambios al repositorio de GitHub Enterprise de la cadena de herramientas, el conducto crea y despliega automáticamente la app.  

1. Si está creando su primera cadena de herramientas, asegúrese de que las cadenas de herramientas estén habilitadas en su organización:
   1. Abra el panel de instrumentos de DevOps y pulse la pestaña **Cadenas de herramientas**.
   2. Si se muestra el botón **Habilitar cadenas de herramientas**, púlselo y siga las instrucciones para crear la cadena de herramientas.
   3. Si no se muestra el botón **Habilitar cadenas de herramientas**, significa que las cadenas de herramientas ya están habilitadas. Continúe con el paso 2. 
1. En la esquina superior derecha de la página Visión general de su app, pulse **Añadir cadena de herramientas**. Su app se ha configurado para entrega continua desde un nuevo repositorio de GitHub Enterprise que se llena con código de inicio de la app.
1. En la página de creación de cadenas de herramientas, revise el diagrama de la cadena de herramientas que está a punto de crear. El diagrama muestra cada integración de herramientas en la fase del ciclo de vida correspondiente en la cadena de herramientas. 
1. Revise la información predeterminada para los valores de la cadena de herramientas. El nombre de la cadena de herramientas la identifica en {{site.data.keyword.Bluemix_notm}}. Si ya existe una cadena de herramientas con el mismo nombre, o si desea utilizar otro, cambie el nombre de la cadena de herramientas.
1. En la sección Configurable Integrations, seleccione las integraciones de herramientas que desee configurar para su cadena de herramientas.Algunas integraciones de herramientas no requieren ninguna configuración. Para obtener más información sobre las integraciones de herramientas, consulte [Configuración de integraciones de herramientas](../toolchains/toolchains_integrations.html){: new_window}.
1. Pulse **Crear**.  Para configurar la cadena de herramientas, se ejecutan varios pasos automáticamente:

 * Se crea la cadena de herramientas.
 * Si ha configurado la integración de herramientas de Delivery Pipeline, se desencadenan los conductos.
 * Si ha configurado la integración de herramientas de GitHub Enterprise, el repositorio de GitHub Enterprise de ejemplo se clona en su cuenta de GitHub Enterprise.


##Visualización de una cadena de herramientas
{: #viewing_a_toolchain}

Cuando haya configurado la cadena de herramientas y las integraciones de herramientas correspondientes, puede ver una representación visual de la cadena de herramientas en la página Integraciones de herramientas.

* Si utiliza {{site.data.keyword.Bluemix_notm}} público, en el panel de control de DevOps, en la pestaña **Cadenas de herramientas**, pulse una cadena de herramientas para abrir la página Integraciones de herramientas correspondiente. Si lo prefiere, en la página Visión general de la app, mosaico Entrega continua, pulse **Ver cadena de herramientas**. A continuación, pulse **Integraciones de herramientas**. 
   
* Si utiliza {{site.data.keyword.Bluemix_notm}} dedicado, en el panel de control, separador **DEVOPS**, haga clic en la cadena de herramientas para abrir la página Integraciones de herramientas correspondiente. Si lo prefiere, en la esquina superior derecha de la página Visión general de la app, pulse **Ver cadena de herramientas**.

* Para acceder a una integración de herramientas de su cadena de herramientas, pulse el mosaico de la herramienta. 
 
 **Consejo**: si tiene más de un repositorio de GitHub o GitHub, puede tener más de un mosaico para la misma integración de herramientas porque cada repositorio se representa mediante su propio mosaico.


 <!-- The toolchain in the following image is an example. When you create your own toolchain, the visual representation of the toolchain shows the tool integrations that you configure.
![Sample toolchain](images/toolchain.png) -->


# Enlaces relacionados
{: #rellinks}

## Guías de aprendizaje y ejemplos
{: #samples}

* [Crear una aplicación con tres microservicios](https://www.ibm.com/devops/method/tutorials/tutorial_microservices_part1){:new_window}
* [Crear una cadena de herramientas desde una plantilla en {{site.data.keyword.Bluemix_notm}} dedicado (Experimental)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_template_flow){:new_window}
* [Crear una cadena de herramientas desde una app en {{site.data.keyword.Bluemix_notm}} dedicado (Experimental)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_app_flow){:new_window}

## Enlaces relacionados
{: #general}

* [Cadena de microservicios (Experimental)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Cadena de herramientas simple (Experimental)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM Bluemix Garage Method](https://www.ibm.com/devops/method){:new_window}
