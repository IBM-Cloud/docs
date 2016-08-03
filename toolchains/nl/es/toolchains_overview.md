---

copyright:
  years: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Iniciación a las cadenas de herramientas (experimental)
{: #toolchains_getting_started}

*Última actualización: 8 de junio de 2016*
{: .last-updated}  

Una cadena de herramientas es un conjunto de integraciones de herramientas que admiten tareas de desarrollo, despliegue y operaciones. La potencia en conjunto de una cadena de herramientas es superior a la suma de las integraciones de las herramientas individuales.
{: shortdesc}

Una cadena de herramientas se puede crear de dos formas: mediante una plantilla o a partir de una app. En función de la plantilla o cadena de herramientas que se utilice, es posible que la cadena de herramientas incluya un repositorio de GitHub que contenga código de inicio de la app y un conducto de entrega ya configurado. Cuando se envían los cambios al repositorio de GitHub de la cadena de herramientas, el conducto de entrega crea y despliega automáticamente la app en {{site.data.keyword.Bluemix}}.

Como punto de partida, puede utilizar una plantilla de cadena de herramientas para utilizar una cadena de herramientas que tenga un conjunto específico de integraciones de herramientas o bien una cadena de herramientas vacía a la que puede añadir integraciones de herramientas. 

**Importante**: esta capacidad es experimental. Es posible que las cadenas de herramientas no sean estables y que cambien de tal modo que no sean compatibles con versiones anteriores. No se recomienda su uso en entornos de producción. Para utilizar cadenas de herramientas, debe realizar una [solicitud única de acceso](https://new-console.ng.bluemix.net/devops?cm_mmc=IBMBluemixGarageMethod-_-MethodSite-_-10-19-15::12-31-18-_-toolchains-welcome-page){: new_window}. Las cadenas de herramientas están disponibles únicamente en el sur de EE. UU. 


##Creación de una cadena de herramientas a partir de una plantilla   
{: #creating_a_toolchain_from_a_template}

Una vez que se haya aprobado su solicitud para acceder a cadenas de herramientas, puede utilizar una plantilla como punto de partida para crear una cadena de herramientas que incluya un conjunto específico de integraciones de herramientas. 

1. En el panel de control de DevOps, en la pestaña **Toolchains**, pulse **Create a Toolchain** para crear su primera cadena de herramientas. Si ya tiene una cadena de herramientas, pulse el botón de adición (+) para crear otra. 
1. Pulse la plantilla de la cadena de herramientas. Por ejemplo, para utilizar un ejemplo de tienda en línea para crear la cadena de herramientas, pulse **Microservices Toolchain**. 
1. En la página de creación de la cadena de herramientas, revise el diagrama de la cadena de herramientas que se dispone a crear. El diagrama muestra cada integración de herramienta en su fase de ciclo en la cadena de herramientas. El diagrama de la imagen siguiente es un ejemplo. Al crear una cadena de herramientas, el diagrama muestra cada una de las integraciones de herramienta que forma parte de la cadena de herramientas.
![Diagrama de cadena de herramientas](images/toolchain_diagram.png)

1. Revise la información predeterminada para la configuración de la cadena de herramientas. El nombre de la cadena de herramientas la identifica en {{site.data.keyword.Bluemix}}. Si ya tiene una cadena de herramientas con dicho nombre, o si desea utilizar otro nombre, cambie el nombre de la cadena de herramientas   
1. En la sección Configurable Integrations, seleccione cada una de las integraciones de herramienta para las que desee configurar su cadena de herramientas. Para obtener información sobre cómo configurar las integraciones de herramienta, consulte [Configurar integraciones de herramienta](../toolchains/toolchains_integrations.html){: new_window}.
1. Pulse **Create**. Para configurar la cadena de herramientas, se ejecutan varios pasos automáticamente: 

 * Se crea la cadena de herramientas. 
 * Si ha configurado la integración de la herramienta Delivery Pipeline, los conductos se activan. 
 * Si ha configurado la integración de la herramienta Sauce Labs, la integración de Sauce Labs se configura para añadir trabajos a los conductos y ejecutar pruebas. 
 * Si ha configurado la integración de la herramienta PagerDuty, la integración de PagerDuty se configura para enviar notificaciones al canal configurado en Slack. Estas notificaciones indican cuándo se produce el problema. 
 * Si ha configurado la integración de la herramienta Slack, la integración de Slack se configura para enviar notificaciones al canal configurado en Slack. Estas notificaciones indican el progreso del despliegue; por ejemplo, `Connected with Project XYZ`, `Pipeline Configured` y `Stage 'build' started`.
 * S ha configurado la integración de la herramienta GitHub, el repositorio de ejemplo de GitHub se clona en su cuenta de GitHub. 


##Creación de una cadena de herramientas a partir de una app
{: #creating_a_toolchain_from_an_app}

Una vez que se haya aprobado su solicitud para acceder a cadenas de herramientas, puede crear una cadena de herramientas a partir de su app. La cadena de herramientas puede admitir tareas continuadas de desarrollo, despliegue, supervisión, etc., y está asociada con su app. Cada app puede asociarse a una cadena de herramientas. Cuando se envían los cambios al repositorio de GitHub de la cadena de herramientas, el conducto crea y despliega automáticamente la app.   

1. En la página de visión general de la app, en el titulo Continuous Delivery, pulse **Add Toolchain**. Como alternativa, en Bluemix Classic Experience, pulse **ADD GIT**. La app se configura para una entrega continuada desde un nuevo repositorio de GitHub que ya contiene el código de inicio de la app. 
1. En la página de creación de la cadena de herramientas, revise el diagrama de la cadena de herramientas que se dispone a crear. El diagrama muestra cada integración de herramienta en su fase de ciclo en la cadena de herramientas. 
1. Revise la información predeterminada para la configuración de la cadena de herramientas. El nombre de la cadena de herramientas la identifica en {{site.data.keyword.Bluemix}}. Si ya tiene una cadena de herramientas con dicho nombre, o si desea utilizar otro nombre, cambie el nombre de la cadena de herramientas 
1. En la sección Configurable Integrations, seleccione cada una de las integraciones de herramienta para las que desee configurar su cadena de herramientas. Para obtener información sobre cómo configurar las integraciones de herramienta, consulte [Configurar integraciones de herramienta](../toolchains/toolchains_integrations.html){: new_window}.
1. Pulse **Create**. Para configurar la cadena de herramientas, se ejecutan varios pasos automáticamente: 

 * Se crea la cadena de herramientas. 
 * Si ha configurado la integración de la herramienta Delivery Pipeline, los conductos se activan. 
 * Si ha configurado la integración de la herramienta Sauce Labs, la integración de Sauce Labs se configura para añadir trabajos a los conductos y ejecutar pruebas. 
 * Si ha configurado la integración de la herramienta PagerDuty, la integración de PagerDuty se configura para enviar notificaciones al canal configurado en Slack. Estas notificaciones indican cuándo se produce el problema. 
 * Si ha configurado la integración de la herramienta Slack, la integración de Slack se configura para enviar notificaciones al canal configurado en Slack. Estas notificaciones indican el progreso del despliegue; por ejemplo, `Connected with Project XYZ`, `Pipeline Configured` y `Stage 'build' started`.
 * S ha configurado la integración de la herramienta GitHub, el repositorio de ejemplo de GitHub se clona en su cuenta de GitHub. 

 
##Visualización de una cadena de herramientas
{: #viewing_a_toolchain}

Una ve que se ha configurado la cadena de herramientas y todas las integraciones de herramientas, es posible obtener una representación visual de la cadena de herramientas en la página Tool Integrations. 

1. En el panel de control de DevOps, en la pestaña **Toolchains**, pulse una cadena de herramientas para abrir la página Tool Integrations correspondiente. Como alternativa, en la página de visión general de la app, en el título Continuous Delivery, pulse **View Toolchain** y, a continuación, pulse **Tool Integrations**.
1. Revise la página para obtener una representación visual de la cadena de herramientas. 
1. Para acceder a una integración de herramienta de su cadena de herramientas, puse el título de la herramienta.  
 
 **Consejo**: si tiene más de un repositorio de GitHub, es posible que tenga varios títulos para la misma integración de herramienta porque cada repositorio necesita su propio conducto. 


 <!-- The toolchain in the following image is an example. When you create your own toolchain, the visual representation of the toolchain shows the tool integrations that you configure.
![Sample toolchain](images/toolchain.png) -->


# Enlaces relacionados
{: #rellinks}

## Tutoriales y ejemplos
{: #samples}

* [Crear una aplicación con tres microservicios](https://www.ibm.com/devops/method/tutorials/tutorial_microservices_part1){:new_window}

## Enlaces relacionados
{: #general}

* [Cadena de herramientas de microservicios (experimental)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Cadena de herramientas simple (experimental)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [Método Garage de IBM&reg; Bluemix&reg;](https://www.ibm.com/devops/method){:new_window}
