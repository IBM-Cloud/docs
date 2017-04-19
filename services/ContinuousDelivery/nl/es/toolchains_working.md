---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-7"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Creación de cadenas de herramientas
{: #toolchains_getting_started}

Una *cadena de herramientas* es un conjunto de integraciones de herramientas que dan soporte a tareas de desarrollo, despliegue, y operaciones. La potencia en conjunto de una cadena de herramientas es superior a la suma de las integraciones de las herramientas individuales.
{: shortdesc}

Las cadenas de herramientas abiertas están disponibles en los entornos Público y Dedicado en {{site.data.keyword.Bluemix}}. Una cadena de herramientas se puede crear de dos formas: mediante una plantilla o a partir de una app. En {{site.data.keyword.Bluemix_notm}} público, las cadenas de herramientas están disponibles solo en la región EE.UU. sur.


Cada cadena de herramientas está asociada con una organización (org) específica y cualquier usuario que sea miembro de la organización se puede añadir a la lista de control de accesos correspondiente a las cadenas de herramientas asociadas. Para obtener más información sobre el control de accesos para cadenas de herramientas, consulte [Gestión del acceso](/docs/services/ContinuousDelivery/toolchains_using.html#managing_access){: new_window}. Para poder crear una cadena de herramientas, asegúrese de que está trabajando en la organización donde desea crear la cadena de herramientas. La organización en la que está trabajando se muestra en la barra de menús. Para conmutar a otra organización, pulse la organización en la barra de menús y seleccione la organización a la que desea conmutar.


##Creación de una cadena de herramientas a partir de una plantilla   
{: #creating_a_toolchain_from_a_template}

Puede utilizar una plantilla como punto de partida para [crear una cadena de herramientas ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/devops/create){: new_window} que incluya un conjunto específico de integraciones de herramientas. Obtenga más información sobre cómo utilizar las plantillas en el [Método IBM Cloud Garage ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/devops/method/category/tools){:new_window}.

1. Si utiliza {{site.data.keyword.Bluemix_notm}} público, inicie la sesión en [{{site.data.keyword.Bluemix_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://console.ng.bluemix.net){:new_window}.
1. Si utiliza {{site.data.keyword.Bluemix_notm}} dedicado, inicie la sesión en el entorno dedicado en {{site.data.keyword.Bluemix_notm}}.
1. En el menú de la barra de menús, pulse **Servicios** y luego pulse **DevOps**.
1. En el panel de control de DevOps, en la página **Cadenas de herramientas**, pulse **Crear una cadena de herramientas**. 
1. En la página **Crear una cadena de herramientas**, pulse una plantilla de cadena de herramientas. 
1. Revise el diagrama de la cadena de herramientas que se dispone a crear. El diagrama muestra cada integración de herramientas en la fase del ciclo de vida correspondiente en la cadena de herramientas.

 **Consejo**: Algunas de las plantillas de cadena de herramientas tienen varias instancias de una integración de herramientas. Por ejemplo, la plantilla de la cadena de herramientas de microservicios de {{site.data.keyword.Bluemix_notm}} público contiene tres instancias de GitHub y tres instancias de Delivery Pipeline, una para cada uno de los tres microservicios. 

 El diagrama de la imagen siguiente es un ejemplo. Cuando cree una cadena de herramientas, el diagrama mostrará cada integración de herramientas que forma parte de la cadena de herramientas.
![Diagrama de cadena de herramientas](images/toolchain_diagram.png)

1. Revise la información predeterminada para la configuración de la cadena de herramientas. El nombre de la cadena de herramientas la identifica en {{site.data.keyword.Bluemix_notm}}. Si desea utilizar otro nombre, cambie el nombre de la cadena de herramientas.   
1. En la sección Integraciones de herramientas, seleccione las integraciones de herramientas que desee configurar para su cadena de herramientas. Algunas integraciones de herramientas no necesitan configuración. Para obtener información sobre cómo configurar las integraciones de herramientas, consulte [Configurar integraciones de herramientas](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Pulse **Crear**. Para configurar la cadena de herramientas, se ejecutan varios pasos automáticamente. Las integraciones de herramientas que se configuran varían en función de la plantilla de cadena de herramientas que haya seleccionado y de si utiliza {{site.data.keyword.Bluemix_notm}} público o {{site.data.keyword.Bluemix_notm}} dedicado. Por ejemplo, si crea una cadena de herramientas de microservicios en {{site.data.keyword.Bluemix_notm}} público, se ejecutan estos pasos: 

 * Se crea la cadena de herramientas.
 * Si ha configurado Delivery Pipeline, los conductos se crean y se activan.
 * Si ha configurado Sauce Labs, la cadena de herramientas se configura para añadir trabajos de prueba de Sauce Labs a los conductos. 
 * Si ha configurado PagerDuty, la cadena de herramientas se configura para enviar notificaciones de alerta al servicio de PagerDuty que ha especificado. 
 * Si ha configurado Slack, la cadena de herramientas se configura para enviar notificaciones sobre el estado de despliegue al canal Slack que ha especificado. 
 * Si ha configurado la integración de una herramienta de código fuente como GitHub, el repositorio de ejemplo de GitHub se clona en su cuenta de GitHub.


##Creación de una cadena de herramientas desde una app
{: #creating_a_toolchain_from_an_app}

Puede crear una cadena de herramientas desde su app. La cadena de herramientas puede admitir tareas continuadas de desarrollo, despliegue, supervisión, etc., y está asociada con su app. Cada app puede asociarse a una cadena de herramientas. Cuando se envían los cambios al repositorio de GitHub o {{site.data.keyword.ghe_short}} de la cadena de herramientas, el conducto crea y despliega automáticamente la app.  

1. En la página Visión general de la app, en la tarjeta de entrega continua, pulse **Habilitar**. Si utiliza {{site.data.keyword.Bluemix_notm}} público, la app se configura para una entrega continua desde un nuevo repositorio de GitHub que ya contiene el código de inicio de la app. Si utiliza {{site.data.keyword.Bluemix_notm}} dedicado, la app se configura para una entrega continua desde un nuevo repositorio de GitHub o {{site.data.keyword.ghe_short}} que ya contiene el código de inicio de la app. 
1. En la página de creación de cadenas de herramientas, revise el diagrama de la cadena de herramientas que está a punto de crear. El diagrama muestra cada integración de herramientas en la fase del ciclo de vida correspondiente en la cadena de herramientas.
1. Revise la información predeterminada para la configuración de la cadena de herramientas. El nombre de la cadena de herramientas la identifica en {{site.data.keyword.Bluemix_notm}}. Si desea utilizar otro nombre, cambie el nombre de la cadena de herramientas. 
1. En la sección Integraciones de herramientas, seleccione las integraciones de herramientas que desee configurar para su cadena de herramientas. Algunas integraciones de herramientas no necesitan configuración. Para obtener información sobre cómo configurar las integraciones de herramientas, consulte [Configurar integraciones de herramientas](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Pulse **Crear**. Para configurar la cadena de herramientas, se ejecutan varios pasos automáticamente. Las integraciones de herramientas que se configuran dependen de si utiliza cadenas de herramientas en {{site.data.keyword.Bluemix_notm}} Público o {{site.data.keyword.Bluemix_notm}} Dedicado. Por ejemplo, si crea una cadena de herramientas a partir de una app en {{site.data.keyword.Bluemix_notm}} público, se ejecutan estos pasos: 

 * Se crea la cadena de herramientas.
 * Si ha configurado Delivery Pipeline, los conductos se crean y se activan.
 * Si ha configurado GitHub, el repositorio de ejemplo de GitHub se clona en su cuenta de GitHub.


##Visualización de una cadena de herramientas
{: #viewing_a_toolchain}

Una vez que se ha configurado la cadena de herramientas y sus integraciones de herramientas, es posible obtener una representación visual de la cadena de herramientas.

1. En el panel de control de DevOps, en la página **Cadenas de herramientas**, pulse sobre la cadena de herramientas para abrir la página Visión general correspondiente. Como alternativa, en la página Visión general de la app, en la tarjeta de Entrega continua, pulse **Ver cadena de herramientas**. A continuación, pulse **Visión general**.
2. Para acceder a una integración de herramienta de su cadena de herramientas, pulse la herramienta.

 **Consejo**: si tiene más de un repositorio de GitHub, {{site.data.keyword.ghe_short}} o Git, puede tener varias tarjetas para la misma integración de herramientas porque cada repositorio se representa mediante su propia tarjeta. Si tiene más de un conducto, puede tener varias tarjetas para la misma integración de herramientas porque cada conducto se representa mediante su propia tarjeta. Por ejemplo, cuando se crea una cadena de herramientas de microservicios, cada uno de los tres microservicios tiene su propio repositorio GitHub, {{site.data.keyword.ghe_short}} o Git y su propio conducto.
