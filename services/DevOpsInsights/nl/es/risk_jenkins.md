---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Integración con proyectos Jenkins de formato libre

Después de añadir {{site.data.keyword.DRA_full}} a una cadena de herramientas abierta y de definir las políticas que supervisa, puede integrarla con un proyecto Jenkins de formato libre. Los proyectos Jenkins de formato libre se configuran y administran desde la interfaz web de Jenkins.  

El plugin IBM Cloud DevOps para Jenkins integra proyectos Jenkins con cadenas de herramientas. Una *cadena de herramientas* es un conjunto de integraciones de herramientas que dan soporte a tareas de desarrollo, despliegue, y operaciones. El poder colectivo de una cadena de herramientas es mayor que la suma de sus integraciones de herramientas individuales. Las cadenas de herramientas abiertas son parte del servicio {{site.data.keyword.contdelivery_full}}. Para obtener más información sobre el servicio {{site.data.keyword.contdelivery_short}}, consulte [su documentación](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/cd_about.html).

Después de instalar el plugin IBM Cloud DevOps, puede publicar los resultados de las pruebas en {{site.data.keyword.DRA_short}}, añadir puertas de calidad automatizadas y realizar un seguimiento del riesgo del despliegue. También puede enviar notificaciones de trabajos a otras herramientas en su cadena de herramientas como, por ejemplo, Slack y PagerDuty. Para ayudarle en el seguimiento de despliegues, la cadena de herramientas puede añadir mensajes de despliegue a confirmaciones Git y los correspondientes problemas Git o JIRA relacionados. También puede ver los despliegues en la página Conexiones de la cadena de herramientas.  

El plugin proporciona una interfaz de línea de mandatos y las acciones posteriores a la compilación para dar soporte a la integración. {{site.data.keyword.DRA_short}} agrega y analiza los resultados de pruebas de unidad, pruebas funcionales, herramientas de cobertura de código, exploraciones de código de seguridad estático y exploraciones de código de seguridad dinámico para determinar si el código cumple las políticas predefinidas en las puertas especificadas del proceso de despliegue. Si el código no cumple o supera una política, el despliegue se detiene para impedir que se liberen cambios arriesgados. Puede utilizar {{site.data.keyword.DRA_short}} como red de seguridad para su entorno de entrega continua, como método para implementar y mejorar con el tiempo los estándares de calidad y como una herramienta de visualización de datos para ayudarle a comprender el estado de salud de su proyecto.

## Requisitos previos
{: #jenkins_prerequisites}

Debe tener acceso a un servidor que ejecute un proyecto Jenkins. 

## Creación de una cadena de herramientas
{: #jenkins_create}

Antes de poder integrar {{site.data.keyword.DRA_short}} con un proyecto Jenkins, debe crear una cadena de herramientas. 

1. Para crear una cadena de herramientas, vaya a la página [Crear una cadena de herramientas](https://console.ng.bluemix.net/devops/create) y siga las instrucciones en dicha página. 

2. Después de crear la cadena de herramientas, añada {{site.data.keyword.DRA_short}} a la misma. Consulte la [documentación de {{site.data.keyword.DRA_short}}](https://console.ng.bluemix.net/docs/services/DevOpsInsights/index.html) para obtener más información.  

## Instalación del plugin
{: #jenkins_install}

Primero, descargue el plugin desde {{site.data.keyword.DRA_short}}.  

1. En la página de Visión general de la cadena de herramientas, pulse **DevOps Insights**.

2. Pulse **Valores** y, a continuación, **Configuración del plugin Jenkins**.
3. Siga las instrucciones de la página para descargar el plugin.

A continuación, instale el plugin en el servidor Jenkins.


1. Pulse **Gestionar Jenkins &gt; Gestionar plugins** y pulse el separador **Avanzado**. 
2. Pulse **Elegir archivo** y seleccione el archivo de instalación del plugin IBM Cloud DevOps.  
3. Pulse **Cargar**.
4. Reinicie Jenkins y verifique se ha instalado el plugin.

## Configuración de trabajos de Jenkins para el panel de control de Deployment Risk 
{: #jenkins_configure}

Después de que el plugin esté instalado, puede integrar {{site.data.keyword.DRA_short}} en su proyecto Jenkins.  

Siga estos pasos para utilizar los paneles de control y las puertas de Deployment Risk en su proyecto. 

1. Abra la configuración de los trabajos que tenga como, por ejemplo, los de compilación, prueba o despliegue. 

2. Añada una acción posterior a la compilación para el tipo correspondiente: 

   * Para trabajos de compilación, utilice **Publicar información de compilación para IBM Cloud DevOps**.
   
   * Para trabajos de prueba, utilice **Publicar información de resultados de prueba para IBM Cloud DevOps**.
   
   * Para trabajos de despliegue, utilice **Publicar información de despliegue para IBM Cloud DevOps**.
   
3. Complete los campos necesarios. Estos variarán según el tipo de trabajo.  

   * Desde la lista de **Credenciales**, seleccione su ID de {{site.data.keyword.Bluemix_notm}} y su contraseña. Si no están guardados en Jenkins, pulse **Añadir** para añadirlos y guardarlos. Pruebe su conexión con {{site.data.keyword.Bluemix_notm}} pulsando **Probar conexión**.
   
   * En el campo **Nombre de trabajo de compilación**, especifique el nombre del trabajo exactamente como aparece en Jenkins. Si la compilación se realiza con el trabajo de prueba, deje este campo vacío. Si el trabajo de compilación se realiza fuera de Jenkins, seleccione el recuadro de selección **Las compilaciones se realizan fuera de Jenkins** y especifique el número de compilación y el URL de compilación. 
   
   * Para el entorno, si las pruebas se ejecutan en la etapa de compilación, seleccione sólo el entorno de compilación. Si las pruebas se ejecutan en la etapa de despliegue, seleccione el entorno de despliegue y especifique el nombre del entorno. Se da soporte a dos valores: `STAGING` y `PRODUCTION`.
   
   * Para el campo **Ubicación del archivo de resultados**, especifique la ubicación del archivo de resultados. Si la prueba no genera ningún archivo de resultados, deje este campo vacío. El plugin sube un archivo de resultados predeterminado que se basa en el estado del trabajo de la prueba actual. 

   Estas imágenes muestran configuraciones de ejemplo: 
   
   ![Subir información de compilación](images/Upload-Build-Info.png "Publicar información de compilación para DRA") *Publicar información de compilación*
   
   ![Subir resultados de pruebas](images/Upload-Test-Result.png "Publicar resultados de pruebas para DRA") *Publicar resultados de pruebas*
   
   ![Subir información de despliegue](images/Upload-Deployment-Info.png "Publicar información de despliegue para DRA")
   *Publicar información de despliegue*

4. Si desea utilizar las puertas de políticas de {{site.data.keyword.DRA_short}} para controlar un trabajo de despliegue en la corriente, añada una acción posterior a la compilación, **Puerta IBM Cloud DevOps**. Elija una política y especifique el ámbito de los resultados de las pruebas. Para permitir que las puertas de políticas impidan el flujo de despliegues en la corriente, seleccione el recuadro de selección **Definir como errónea la compilación en base a las reglas de política**. La siguiente imagen muestra una configuración de ejemplo: 

    ![Puerta de DevOps Insights](images/DRA-Gate.png "Puerta de DevOps Insights")

5. Ejecute su trabajo de compilación de Jenkins. 

6. Visualice el panel de control de Deployment Risk. Vaya a [IBM Bluemix DevOps](https://console.ng.bluemix.net/devops), seleccione su cadena de herramientas y pulse **DevOps Insights**.

El panel de control de Deployment Risk se basa en la presencia de una puerta después un trabajo de despliegue en el entorno de transferencia. Si desea utilizar el panel de control, asegúrese de que tiene una puerta después de realizar el despliegue en el entorno de transferencia y antes de realizar el despliegue en un entorno de producción. 
    
## Configuración de notificaciones
{: #jenkins_notifications}

Tiene la posibilidad de configurar los trabajos de Jenkins para que envíen notificaciones a herramientas como, por ejemplo, Slack o PagerDuty siguiendo las instrucciones en la [documentación de Bluemix](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/toolchains_integrations.html#jenkins).

Este ejemplo muestra cómo configurar `ICD_WEBHOOK_URL` para configuraciones de trabajos: ![Establecer el parámetro ICD_WEBHOOK_URL](images/Set-Parameterized-Webhook.png "Establecer un webhook parametrizado")

Este ejemplo muestra cómo configurar acciones posteriores a la compilación para notificaciones de trabajo: ![Acciones posteriores a la compilación para notificaciones webhook](images/PostBuild-WebHookNotification.png "Configurar notificaciones webhook en acciones posteriores a la compilación")   
