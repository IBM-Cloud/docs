---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Iniciación a las cadenas de herramientas
{: #toolchains-setup}

Última actualización: 28 de abril de 2016
{: .last-updated}  

Puede crear una cadena de herramientas de dos maneras: utilizando una plantilla para crear una cadena de herramientas o añadiendo una cadena de herramientas a una app. En función de la plantilla o cadena de herramientas que se utilice, la cadena de herramientas puede incluir un repositorio de GitHub (repo) que se llena con código de inicio de la app y un conducto de entrega ya configurado. Cuando se envían los cambios al repositorio de GitHub de la cadena de herramientas, el conducto de entrega crea y despliega automáticamente la app en {{site.data.keyword.Bluemix}}. 
{: shortdesc}  

**Importante**: Esta función es experimental. Es posible que las cadenas de herramientas no sean estables y cambien de modo que no sean compatibles con versiones anteriores. No se recomienda su uso en entornos de producción.
Para utilizar cadenas de herramientas, debe realizar una [solicitud de acceso](https://new-console.ng.bluemix.net/devops?cm_mmc=IBMBluemixGarageMethod-_-MethodSite-_-10-19-15::12-31-18-_-toolchains-welcome-page){: new_window} una sola vez. Las cadenas de herramientas solo están disponibles solo en la región Dallas.


##Creación de una cadena de herramientas a partir de una plantilla   
{: #creating_a_toolchain_from_a_template}

Una vez aprobada la solicitud de acceso a las cadenas de herramientas, puede utilizar una plantilla como punto de partida para crear una cadena de herramientas que incluya un conjunto específico de integraciones de herramientas.

1. En el panel de control de DevOps, en la página **Cadenas de herramientas**, pulse **Crear una cadena de herramientas** para crear su primera cadena de herramientas. Si ya tiene una cadena de herramientas, pulse el botón de adición (+) para crear una cadena de herramientas.
1. Pulse una plantilla de cadena de herramientas. Por ejemplo, para utilizar un ejemplo de tienda en línea para crear la cadena de herramientas, pulse **Cadena de herramientas nativa de la nube para Microservices**. 
1. En la página de creación de cadenas de herramientas, revise el diagrama de la cadena de herramientas que está a punto de crear. El diagrama muestra cada integración de herramientas en la fase del ciclo de vida correspondiente en la cadena de herramientas. El diagrama de la imagen siguiente es un ejemplo. Cuando cree una cadena de herramientas, el diagrama mostrará cada integración de herramientas que forma parte de la cadena de herramientas.
![Diagrama de cadena de herramientas](images/toolchain_diagram.png)

1. Revise la información predeterminada para la configuración de la cadena de herramientas. El nombre de la cadena de herramientas la identifica en {{site.data.keyword.Bluemix}}. Si ya existe una cadena de herramientas con este nombre, o si desea utilizar otro, cambie el nombre de la cadena de herramientas.  
1. Si desea crear la cadena de herramientas antes de configurar integraciones de herramientas, pulse **CREAR** y confirme que desea crear la cadena de herramientas sin integraciones de herramientas. Continúe en la sección [Creación de una cadena de herramientas](#creating_a_toolchain), que describe los pasos que se ejecutan automáticamente para configurar la cadena de herramientas.  
1. Si desea configurar las integraciones de herramientas antes de crear la cadena de herramientas, en la sección Integraciones configurables seleccione las integraciones de herramientas que desee configurar. Para obtener información sobre cómo configurar las integraciones de herramientas, consulte [Configurar integraciones de herramientas](../toolchains/toolchains_integrations.html){: new_window}. 

##Creación de una cadena de herramientas desde una app
{: #creating_a_toolchain_from_an_app}

Una vez aprobada la solicitud para acceder a las cadenas de herramientas, puede crear una cadena de herramientas desde una app. La cadena de herramientas puede admitir tareas continuadas de desarrollo, despliegue, supervisión, etc., y está asociada con su app. Cada app puede estar asociada a una cadena de herramientas. Cuando se envían los cambios al repositorio de GitHub de la cadena de herramientas, el conducto crea y despliega automáticamente la app.  

1. En la página Visión general de la app, en el mosaico Continuous Delivery, pulse **Añadir cadena de herramientas**. Como alternativa, en Bluemix Classic Experience, pulse **AÑADIR GIT**. La app se configura para una entrega continuada desde un nuevo repositorio de GitHub que ya contiene el código de inicio de la app.
1. En la página de creación de cadenas de herramientas, revise el diagrama de la cadena de herramientas que está a punto de crear. El diagrama muestra cada integración de herramientas en la fase del ciclo de vida correspondiente en la cadena de herramientas.
1. Revise la información predeterminada para la configuración de la cadena de herramientas. El nombre de la cadena de herramientas la identifica en {{site.data.keyword.Bluemix}}. Si ya existe una cadena de herramientas con este nombre, o si desea utilizar otro, cambie el nombre de la cadena de herramientas.
1. En la sección Integraciones configurables, seleccione las integraciones de herramientas que desee configurar para su cadena de herramientas. Para obtener información sobre cómo configurar las integraciones de herramientas, consulte [Configurar integraciones de herramientas](../toolchains/toolchains_integrations.html){: new_window}.

## Configuración de una cadena de herramientas
{: #setting_up_a_toolchain}

Si aún no ha creado una cadena de herramientas, pulse **CREAR**. Para configurar la cadena de herramientas, se ejecutan varios pasos automáticamente:

 * Se crea la cadena de herramientas.
 * Si ha configurado la integración de la herramienta Delivery Pipeline, los conductos se activan.
 * Si ha configurado la integración de la herramienta Sauce Labs, la integración de Sauce Labs se configura para añadir trabajos a los conductos y ejecutar pruebas.
 * Si ha configurado la integración de la herramienta PagerDuty, la integración de PagerDuty se configura para enviar notificaciones al canal configurado en Slack. Estas notificaciones indican la aparición de un problema.
 * Si ha configurado la integración de la herramienta Slack, la integración de Slack se configura para enviar notificaciones al canal configurado en Slack. Estas notificaciones indican el progreso del despliegue; por ejemplo, `Connected with Project XYZ`, `Pipeline Configured` y `Stage 'build' started`.
 * Si ha configurado la integración de la herramienta GitHub, el repositorio de ejemplo de GitHub se clona en su cuenta de GitHub.  
 
##Visualización de una cadena de herramientas
{: #viewing_a_toolchain}

Después de configurar la cadena de herramientas y todas las integraciones de herramientas, se abre la página Integraciones de herramientas. 

1. Revise la página para tener una representación visual de la cadena de herramientas para su app.
1. Para acceder a una integración de herramienta de su cadena de herramientas, pulse el mosaico de la herramienta. 
 
 **Consejo**: si tiene más de un repositorio de GitHub, es posible que tenga varios mosaicos para la misma integración de herramienta porque cada repositorio necesita su propio conducto. 
