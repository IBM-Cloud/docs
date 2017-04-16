---

copyright:
  years: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Iniciación a {{site.data.keyword.contdelivery_short}}
{: #cd_getting_started}

Última actualización: 18 de noviembre de 2016
{: .last-updated}  

Puede adoptar un enfoque DevOps mediante {{site.data.keyword.contdelivery_full}}, que incluye cadenas de herramientas que automatizan la creación y despliegue de aplicaciones. Puede empezar creando una sencilla cadena de herramientas que dé soporte a las tareas de desarrollo, despliegue y operaciones.
{: shortdesc}

Después de crear una instancia de {{site.data.keyword.contdelivery_short}} seleccionando su mosaico de servicios en el catálogo de {{site.data.keyword.Bluemix_notm}}, puede elegir cómo desea empezar a trabajar con el servicio. ![Página de bienvenida de entrega continua](images/cd_landing_page.png)

 * Para empezar a trabajar y a desplegar rápidamente la aplicación utilizando un conducto automatizado, en la sección "Inicio con un conducto" pulse **[Empezar aquí](#starting_with_a_pipeline)**. Luego podrá añadir más herramientas.  
 * Para crear y configurar una cadena de herramientas de entrega continua a partir de una plantilla, en la sección "Inicio desde una plantilla de cadena de herramientas" pulse **[Empezar aquí](#starting_from_a_toolchain_template)**. La cadena de herramientas integra herramientas para la planificación, despliegue de conductos y gestión de aplicaciones. Siempre puede añadir o eliminar herramientas de sus cadenas de herramientas.
 * Si ya tiene cadenas de herramientas, en la sección "Inicio desde una plantilla de cadena de herramientas" pulse **Ver sus cadenas de herramientas**. Para obtener más información sobre cómo trabajar con cadenas de herramientas, consulte el apartado sobre [Utilización de cadenas de herramientas en Bluemix público](/docs/services/ContinuousDelivery/toolchains_using.html){: new_window}.

## Inicio con un conducto
{: #starting_with_a_pipeline}

Los conductos automatizan las compilaciones, despliegues y más. Para empezar con un conducto automatizado, seleccione una plantilla y especifique la ubicación del repositorio GitHub (repositorio).

Para [crear un conducto (el enlace se abre en una nueva ventana)](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window} configurado para desplegar una aplicación Cloud Foundry, siga estos pasos: 

1. Pulse **Cloud Foundry**.
1. Si desea utilizar otro nombre para el conducto, cambie el nombre predeterminado. El nombre del conducto lo identifica en {{site.data.keyword.Bluemix_notm}}.  
1. Si desea utilizar otro nombre para la aplicación, cambie el nombre predeterminado. El nombre de la aplicación la identifica en {{site.data.keyword.Bluemix_notm}}. Este es el nombre de la aplicación en la que se despliega el conducto.  
1. Si no tiene una cadena de herramientas, se crea automáticamente una cadena de herramientas con un nombre predeterminado. Si desea utilizar otro nombre para la cadena de herramientas, cámbiele el nombre. Los conductos se gestionan mediante cadenas de herramientas. Con la cadena de herramientas, puede ampliar las prestaciones del conducto integrándolo con otras herramientas y servicios.  

 **Consejo**: Los conductos y las cadenas de herramientas pertenecen a las organizaciones (orgs). Si pertenece a una org que tiene cadenas de herramientas, puede utilizar dichas cadenas de herramientas aunque no las haya creado. 
 
1. Seleccione la cadena de herramientas que desea utilizar o escriba un nombre para la nueva cadena de herramientas que desea crear.
1. Especifique la ubicación del repositorio GitHub.

 **Sugerencia**: si no tiene autorización de {{site.data.keyword.Bluemix_notm}} para acceder a GitHub, se le solicitará que pulse **Autorizar** para ir al sitio web de GitHub. Si no tiene ninguna sesión de GitHub activa, se le solicitará que inicie sesión. Pulse **Autorizar aplicación** para permitir que {{site.data.keyword.Bluemix_notm}} acceda a su cuenta de GitHub. Si tiene una sesión activa de GitHub pero no ha introducido recientemente su contraseña, es posible que se le solicite que introduzca la contraseña de GitHub para confirmarla.

   * Si tiene un repositorio de GitHub y desea utilizarlo, seleccione **Enlazar** para el tipo de repositorio. Busque la ubicación del repositorio o seleccione el repositorio en la lista de repositorios disponibles.
   
   * Si desea crear un repositorio GitHub vacío, seleccione **Nuevo** para el tipo de repositorio. Escriba un nombre para el repositorio.
   
   * Si desea crear un clon de un repositorio GitHub, seleccione **Copiar** para el tipo de repositorio. Busque la ubicación del repositorio o seleccione el repositorio en la lista de repositorios disponibles.
   
   * Si desea bifurcar un repositorio GitHub de forma que pueda aportar cambios a través de solicitudes de extracción, seleccione **Bifurcar**.Busque la ubicación del repositorio o seleccione el repositorio en la lista de repositorios disponibles.
 
1. Pulse **Crear**. El conducto se crea, se configura y se visualiza en la página Visión general de la cadena de herramientas. ![Mosaico de conductos](images/cd_pipeline.png)
 
Para crear un [conducto vacío (el enlace se abre en una ventana nueva)](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window} sin etapas preconfiguradas:

1. Pulse **Personalizado**.
1. Si desea utilizar otro nombre para el conducto, cambie el nombre predeterminado. El nombre del conducto lo identifica en {{site.data.keyword.Bluemix_notm}}.  
1. Si no tiene una cadena de herramientas, se crea automáticamente una cadena de herramientas con un nombre predeterminado. Si desea utilizar otro nombre para la cadena de herramientas, cámbiele el nombre. Los conductos se gestionan mediante cadenas de herramientas. Con la cadena de herramientas, puede ampliar las prestaciones del conducto integrándolo con otras herramientas y servicios. 
1. Seleccione la cadena de herramientas que desea utilizar o escriba un nombre para la nueva cadena de herramientas que desea crear.
1. Pulse **Crear**. Se crea un conducto vacío y se representa como un mosaico en la página Visión general de la cadena de herramientas.

## Inicio desde una plantilla de cadena de herramientas
{: #starting_from_a_toolchain_template}

Para crear y configurar una cadena de herramientas de entrega continua desde una plantilla de [ (el enlace se abre en una nueva ventana)](https://console.ng.bluemix.net/devops/create){: new_window}:

1. En la página **Crear una cadena de herramientas**, pulse una plantilla de cadena de herramientas.   
1. Revise el diagrama de la cadena de herramientas que se dispone a crear. El diagrama muestra cada integración de herramientas en la fase del ciclo de vida correspondiente en la cadena de herramientas. El diagrama de la imagen siguiente es un ejemplo. Cuando cree una cadena de herramientas, el diagrama mostrará cada integración de herramientas que forma parte de la cadena de herramientas.
![Toolchain_diagram](images/toolchain_diagram.png)
1. Revise la información predeterminada para la configuración de la cadena de herramientas. El nombre de la cadena de herramientas la identifica en {{site.data.keyword.Bluemix_notm}}. Si desea utilizar otro nombre, cambie el nombre de la cadena de herramientas. 
1. En la sección Integraciones configurables, seleccione las integraciones de herramientas que desee configurar para su cadena de herramientas. Algunas integraciones de herramientas no necesitan configuración. Para obtener información sobre cómo configurar las integraciones de herramientas, consulte [Configurar integraciones de herramientas](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}.
1. Pulse **Crear**. Para configurar la cadena de herramientas, se ejecutan varios pasos automáticamente:

 * Se crea la cadena de herramientas.
 * Si ha configurado la integración de la herramienta Delivery Pipeline, los conductos se crean y se activan.
 * Si ha configurado la integración de la herramienta Sauce Labs, Sauce Labs se configura para añadir trabajos a los conductos y para ejecutar pruebas.
 * Si ha configurado la integración de la herramienta PagerDuty, PagerDuty se configura para enviar notificaciones de alerta al servicio que ha especificado.  
 * Si ha configurado la integración de la herramienta Slack, Slack se configura para enviar notificaciones sobre el estado de despliegue al canal que ha especificado.  
 * Si ha configurado la integración de la herramienta GitHub, el repositorio de ejemplo de GitHub se clona en su cuenta de GitHub. 

# Enlaces relacionados
{: #rellinks}

## Guías de aprendizaje y ejemplos
{: #samples}

* [Crear y utilizar su primera cadena de herramientas (el enlace se abre en una nueva ventana)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_flow){:new_window}
* [Crear una cadena de herramientas personalizada (el enlace se abre en una nueva ventana)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_custom){:new_window}
* [Crear una aplicación con tres microservicios (el enlace se abre en una nueva ventana)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_microservices){:new_window}

## Enlaces relacionados
{: #general}

* [Cadena de herramientas de microservicios (el enlace se abre en una nueva ventana)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [Cadena de herramientas simple (el enlace se abre en una nueva ventana)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [Método IBM Bluemix Garage (el enlace se abre en una ventana nueva)](https://www.ibm.com/devops/method){:new_window}
