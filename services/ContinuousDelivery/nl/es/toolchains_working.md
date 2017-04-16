---

copyright:
  years: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Cómo trabajar con cadenas de herramientas
{: #toolchains_getting_started}

Última actualización: 17 de Noviembre de 2016
{: .last-updated}  

Una *cadena de herramientas* es un conjunto de integraciones de herramientas que dan soporte a tareas de desarrollo, despliegue, y operaciones. La potencia en conjunto de una cadena de herramientas es superior a la suma de las integraciones de las herramientas individuales.
{: shortdesc}

Las cadenas de herramientas están disponibles en los entornos Público y Dedicado en {{site.data.keyword.Bluemix}}. Una cadena de herramientas se puede crear de dos formas: mediante una plantilla o a partir de una app. En {{site.data.keyword.Bluemix_notm}} Público, las cadenas de herramientas solo están disponibles en la región EE.UU. Sur. 

## Iniciación a las cadenas de herramientas: Público
{: #getting_started_public}

Cada cadena de herramientas está asociada con una organización (org) específica y cualquier usuario que sea miembro de la organización en cuestión puede acceder a las cadenas de herramientas asociadas correspondientes. Para poder crear una cadena de herramientas, asegúrese de que está trabajando en la organización donde desea crear la cadena de herramientas. La organización en la que está trabajando actualmente se muestra en la barra de menús. Para conmutar a otra organización, pulse la organización en la barra de menús y, a continuación, seleccione la organización a la que desea conmutar.

### Creación de una cadena de herramientas a partir de una plantilla   
{: #creating_a_toolchain_from_a_template}

Puede utilizar una plantilla como punto de partida para [crear una cadena de herramientas (el enlace se abre en una nueva ventana)](https://console.ng.bluemix.net/devops/create){: new_window} que incluya un conjunto específico de integraciones de herramientas. Obtenga más información sobre cómo utilizar las plantillas desde el [Método IBM Bluemix Garage (el enlace se abre en una ventana nueva)](https://www.ibm.com/devops/method/category/tools){:new_window}.

1. Inicie una sesión en [{{site.data.keyword.Bluemix_notm}} (el enlace se abre en una ventana nueva)](http://console.ng.bluemix.net){:new_window}. Se abre el panel de control de {{site.data.keyword.Bluemix_notm}}, que muestra una visión general del espacio de {{site.data.keyword.Bluemix_notm}} activo para la org.
1. En el menú de la barra de menús, pulse **Servicios** y luego pulse **DevOps**.
1. En el panel de control de DevOps, en la página **Cadenas de herramientas**, pulse **Crear una cadena de herramientas**. 
1. En la página **Crear una cadena de herramientas**, pulse una plantilla de cadena de herramientas. 
1. Revise el diagrama de la cadena de herramientas que se dispone a crear. El diagrama muestra cada integración de herramientas en la fase del ciclo de vida correspondiente en la cadena de herramientas. El diagrama de la imagen siguiente es un ejemplo. Cuando cree una cadena de herramientas, el diagrama mostrará cada integración de herramientas que forma parte de la cadena de herramientas.
![Diagrama de cadena de herramientas](images/toolchain_diagram.png)

1. Revise la información predeterminada para la configuración de la cadena de herramientas. El nombre de la cadena de herramientas la identifica en {{site.data.keyword.Bluemix_notm}}. Si desea utilizar otro nombre, cambie el nombre de la cadena de herramientas.   
1. En la sección Integraciones configurables, seleccione las integraciones de herramientas que desee configurar para su cadena de herramientas. Algunas integraciones de herramientas no necesitan configuración. Para obtener información sobre cómo configurar las integraciones de herramientas, consulte [Configurar integraciones de herramientas](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Pulse **Crear**. Para configurar la cadena de herramientas, se ejecutan varios pasos automáticamente:

 * Se crea la cadena de herramientas.
 * Si ha configurado la integración de la herramienta Delivery Pipeline, los conductos se crean y se activan.
 * Si ha configurado la integración de la herramienta Sauce Labs, Sauce Labs se configura para añadir trabajos a los conductos y para ejecutar pruebas.
 * Si ha configurado la integración de la herramienta PagerDuty, PagerDuty se configura para enviar notificaciones de alerta al servicio que ha especificado. 
 * Si ha configurado la integración de la herramienta Slack, Slack se configura para enviar notificaciones sobre el estado de despliegue al canal que ha especificado. 
 * Si ha configurado la integración de la herramienta GitHub, el repositorio de ejemplo de GitHub se clona en su cuenta de GitHub.


### Creación de una cadena de herramientas desde una app
{: #creating_a_toolchain_from_an_app}

Puede crear una cadena de herramientas desde una app. La cadena de herramientas puede admitir tareas continuadas de desarrollo, despliegue, supervisión, etc., y está asociada con su app. Cada app puede estar asociada a una cadena de herramientas. Cuando se envían los cambios al repositorio de GitHub de la cadena de herramientas, el conducto crea y despliega automáticamente la app.  

1. En la página Visión general de la app, en el mosaico Continuous Delivery, pulse **Enable**. La app se configura para una entrega continuada desde un nuevo repositorio de GitHub que ya contiene el código de inicio de la app.
1. En la página de creación de cadenas de herramientas, revise el diagrama de la cadena de herramientas que está a punto de crear. El diagrama muestra cada integración de herramientas en la fase del ciclo de vida correspondiente en la cadena de herramientas.
1. Revise la información predeterminada para la configuración de la cadena de herramientas. El nombre de la cadena de herramientas la identifica en {{site.data.keyword.Bluemix_notm}}. Si desea utilizar otro nombre, cambie el nombre de la cadena de herramientas. 
1. En la sección Integraciones configurables, seleccione las integraciones de herramientas que desee configurar para su cadena de herramientas. Algunas integraciones de herramientas no necesitan configuración. Para obtener información sobre cómo configurar las integraciones de herramientas, consulte [Configurar integraciones de herramientas](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Pulse **Crear**. Para configurar la cadena de herramientas, se ejecutan varios pasos automáticamente:

 * Se crea la cadena de herramientas.
 * Si ha configurado la integración de la herramienta Delivery Pipeline, los conductos se crean y se activan.
 * Si ha configurado la integración de la herramienta Sauce Labs, Sauce Labs se configura para añadir trabajos a los conductos y para ejecutar pruebas.
 * Si ha configurado la integración de la herramienta PagerDuty, PagerDuty se configura para enviar notificaciones de alerta al servicio que ha especificado. 
 * Si ha configurado la integración de la herramienta Slack, Slack se configura para enviar notificaciones sobre el estado de despliegue al canal que ha especificado. 
 * Si ha configurado la integración de la herramienta GitHub, el repositorio de ejemplo de GitHub se clona en su cuenta de GitHub.


## Iniciación a las cadenas de herramientas: dedicado
{: #getting_started_dedicated}

Cada cadena de herramientas está asociada con una organización específica y cualquier usuario que sea miembro de la organización en cuestión puede acceder a las cadenas de herramientas asociadas. Para poder crear una cadena de herramientas, pulse el icono **{{site.data.keyword.avatar}}** en la barra de menús para abrir el widget de Cuenta y soporte y ver la organización en la que está trabajando. Si la organización no es la organización en la que desea crear la cadena de herramientas, cambie a otra.

### Creación de una cadena de herramientas a partir de una plantilla   
{: #creating_a_toolchain_from_a_template_dedicated}

Puede utilizar una plantilla como punto de partida para crear una cadena de herramientas que incluya un conjunto específico de integraciones de herramientas.

1. En el panel de control de {{site.data.keyword.Bluemix_notm}}, en el separador **DEVOPS**, pulse el botón de adición (+) para crear una cadena de herramientas.
1. En la página **Crear una cadena de herramientas**, pulse una plantilla de cadena de herramientas.  
1. Revise el diagrama de la cadena de herramientas que se dispone a crear. El diagrama muestra cada integración de herramientas en la fase del ciclo de vida correspondiente en la cadena de herramientas. El diagrama de la imagen siguiente es un ejemplo. Cuando cree una cadena de herramientas, el diagrama mostrará cada integración de herramientas que forma parte de la cadena de herramientas.
![Diagrama de cadena de herramientas dedicada](images/toolchain_dedicated_diagram.png)

1. Revise la información predeterminada para la configuración de la cadena de herramientas. El nombre de la cadena de herramientas la identifica en {{site.data.keyword.Bluemix_notm}}. Si ya existe una cadena de herramientas con este nombre, o si desea utilizar otro, cambie el nombre de la cadena de herramientas.  
1. En la sección Integraciones configurables, seleccione las integraciones de herramientas que desee configurar para su cadena de herramientas. Algunas integraciones de herramientas no necesitan configuración. Para obtener información sobre cómo configurar las integraciones de herramientas, consulte [Configurar integraciones de herramientas](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Pulse **Crear**. Para configurar la cadena de herramientas, se ejecutan varios pasos automáticamente:

 * Se crea la cadena de herramientas.
 * Si ha configurado la integración de la herramienta Delivery Pipeline, los conductos se crean y se activan.
 * Si ha configurado la integración de la herramienta PagerDuty, PagerDuty se configura para enviar notificaciones de alerta al servicio que ha especificado. 
 * Si ha configurado la integración de la herramienta Slack, Slack se configura para enviar notificaciones sobre el estado de despliegue al canal que ha especificado. 
 * Si ha configurado la integración de herramientas de GitHub Enterprise, el repositorio de GitHub Enterprise de ejemplo se clona en su cuenta de GitHub Enterprise.


### Creación de una cadena de herramientas desde una app
{: #creating_a_toolchain_from_an_app_dedicated}

Puede crear una cadena de herramientas desde una app. La cadena de herramientas puede admitir tareas continuadas de desarrollo, despliegue, supervisión, etc., y está asociada con su app. Cada app puede estar asociada a una cadena de herramientas. Cuando se envían los cambios al repositorio de GitHub Enterprise de la cadena de herramientas, el conducto crea y despliega automáticamente la app.  

1. En la esquina superior derecha de la página Visión general de su app, pulse **Añadir cadena de herramientas**. La app se configura para una entrega continuada desde un nuevo repositorio de GitHub Enterprise que ya contiene el código de inicio de la app.
1. En la página de creación de cadenas de herramientas, revise el diagrama de la cadena de herramientas que está a punto de crear. El diagrama muestra cada integración de herramientas en la fase del ciclo de vida correspondiente en la cadena de herramientas.
1. Revise la información predeterminada para la configuración de la cadena de herramientas. El nombre de la cadena de herramientas la identifica en {{site.data.keyword.Bluemix_notm}}. Si ya existe una cadena de herramientas con este nombre, o si desea utilizar otro, cambie el nombre de la cadena de herramientas.
1. En la sección Integraciones configurables, seleccione las integraciones de herramientas que desee configurar para su cadena de herramientas. Algunas integraciones de herramientas no necesitan configuración. Para obtener información sobre cómo configurar las integraciones de herramientas, consulte [Configurar integraciones de herramientas](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Pulse **Crear**. Para configurar la cadena de herramientas, se ejecutan varios pasos automáticamente:

 * Se crea la cadena de herramientas.
 * Si ha configurado la integración de la herramienta Delivery Pipeline, los conductos se crean y se activan.
 * Si ha configurado la integración de la herramienta PagerDuty, PagerDuty se configura para enviar notificaciones de alerta al servicio que ha especificado. 
 * Si ha configurado la integración de la herramienta Slack, Slack se configura para enviar notificaciones sobre el estado de despliegue al canal que ha especificado. 
 * Si ha configurado la integración de herramientas de GitHub Enterprise, el repositorio de GitHub Enterprise de ejemplo se clona en su cuenta de GitHub Enterprise.


## Visualización de una cadena de herramientas
{: #viewing_a_toolchain}

Una vez que se ha configurado la cadena de herramientas y sus integraciones de herramientas, es posible obtener una representación visual de la cadena de herramientas.

* Si utiliza {{site.data.keyword.Bluemix_notm}} público, en el panel de control de DevOps, en la página **Cadenas de herramientas**, pulse una cadena de herramientas para abrir la página Visión general correspondiente. Como alternativa, en la página Visión general de la aplicación, en el mosaico Entrega continua, pulse **Ver cadena de herramientas**. A continuación, pulse **Visión general**. 
   
* Si utiliza {{site.data.keyword.Bluemix_notm}} dedicado, en el panel de control, separador **DEVOPS**, haga clic en la cadena de herramientas para abrir la página Integraciones de herramientas correspondiente. Si lo prefiere, en la esquina superior derecha de la página Visión general de la app, pulse **Ver cadena de herramientas**.

* Para acceder a una integración de herramientas de su cadena de herramientas, pulse el mosaico de la herramienta. 
 
 **Consejo**: si tiene más de un repositorio de GitHub o GitHub, puede tener más de un mosaico para la misma integración de herramientas porque cada repositorio se representa mediante su propio mosaico.


# Enlaces relacionados
{: #rellinks}

## Guías de aprendizaje y ejemplos
{: #samples}

* [Crear y utilizar su primera cadena de herramientas (el enlace se abre en una nueva ventana)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_flow){:new_window}
* [Crear una cadena de herramientas personalizada (el enlace se abre en una nueva ventana)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_custom){:new_window}
* [Crear una aplicación con tres microservicios (el enlace se abre en una nueva ventana)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_microservices){:new_window}
* [Crear una cadena de herramientas desde una plantilla en {{site.data.keyword.Bluemix_notm}} Dedicado (Beta) (el enlace se abre en una nueva ventana)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_template_flow){:new_window}
* [Crear una cadena de herramientas desde una app en {{site.data.keyword.Bluemix_notm}} Dedicado (Beta) (el enlace se abre en una nueva ventana)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_app_flow){:new_window}

## Enlaces relacionados
{: #general}

* [Cadena de herramientas de microservicios (el enlace se abre en una nueva ventana)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Cadena de herramientas simple (el enlace se abre en una nueva ventana)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [Método IBM Bluemix Garage (el enlace se abre en una ventana nueva)](https://www.ibm.com/devops/method){:new_window}
