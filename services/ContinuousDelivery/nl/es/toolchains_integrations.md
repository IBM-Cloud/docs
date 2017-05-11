---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}    

# Configuración de la integración de herramientas
{: #integrations}

Puede configurar integraciones de herramientas que admitan tareas de desarrollo, despliegue y operaciones mientras crea una cadena de herramientas abierta, o bien puede añadir y configurar integraciones de herramientas para personalizar una cadena de herramientas existente.  
{:shortdesc}

**Importante**: En {{site.data.keyword.Bluemix_notm}} Público, las cadenas de herramientas están disponibles únicamente en el sur de EE. UU.

Las integraciones de herramientas que están disponibles para añadirse y configurarse para la cadena de herramientas son distintas en función de si está utilizando cadenas de herramientas en {{site.data.keyword.Bluemix_notm}} Público o {{site.data.keyword.Bluemix_notm}} Dedicado. Si está utilizando cadenas de herramientas en {{site.data.keyword.Bluemix_notm}} Dedicado, las integraciones de herramientas disponibles para usted dependerán de cómo se haya configurado {{site.data.keyword.contdelivery_full}} en el entorno específico.

|Integración de herramientas |Disponible en {{site.data.keyword.Bluemix_notm}} Público	|Disponible en {{site.data.keyword.Bluemix_notm}} Dedicado (dependiente del entorno)|
|:----------|:------------------------------|:------------------|
|{{site.data.keyword.alertnotificationshort}}		|Sí		|No		|
|Artifactory		|Sí		|No		|
|Supervisión de disponibilidad		|Sí		|No		|
|Gestión de sucesos de nube		|Sí		|No		|
|{{site.data.keyword.deliverypipeline}} 		|Sí	   	|Sí  		|
|{{site.data.keyword.DRA_short}} 		|Sí		|No			|
|Eclipse Orion {{site.data.keyword.webide}}		|Sí		|Sí			|
|Repos Git y seguimiento problemas	|Sí		|No		|
|GitHub y problemas		|Sí		|Sí		|
|{{site.data.keyword.ghe_short}} dedicado y problemas			|No		|Sí		|
|Jenkins		|Sí		|No		|
|JIRA		|Sí		|No		|
|Nexus			|Sí		|No		|
|Otras herramientas			|Sí		|Sí		|
|PagerDuty			|Sí		|Sí		|
|Sauce Labs		|Sí		|No		|
|Slack			|Sí		|Sí		|
{: caption="Table 1. Tool integrations available for toolchains on {{site.data.keyword.Bluemix_notm}} Público y Dedicado" caption-side="top"}

**Consejo**: si desea empezar a desarrollar su propio código en {{site.data.keyword.Bluemix_notm}} Público, configure la integración de herramientas GitHub y la integración de la herramienta de seguimiento de problemas antes de configurar el {{site.data.keyword.deliverypipeline}}. Si desea empezar a desarrollar su propio código en {{site.data.keyword.Bluemix_notm}} Dedicado, configure la integración de herramientas {{site.data.keyword.ghe_short}} o la integración de herramientas GitHub antes de configurar el {{site.data.keyword.deliverypipeline}}.


## Configuración de Alert Notification (experimental)
{: #alertnotification}

{{site.data.keyword.alertnotificationfull}} es una solución híbrida basada en la nube que puede utilizar para centralizar y simplificar la estrategia de notificaciones. Funciona con otras aplicaciones en la nube y locales. Las alertas se reenvían a {{site.data.keyword.alertnotificationshort}} utilizando una API RESTful segura. 

Configure {{site.data.keyword.alertnotificationshort}} de modo que reciba notificaciones sobre problemas durante el proceso de DevOps. 

### Requisitos previos

1. Si no tiene una cuenta de {{site.data.keyword.alertnotificationshort}}, regístrese para obtener una: 

 a. Abra la página de [IBM {{site.data.keyword.alertnotificationshort}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/us-en/marketplace/alert-notification){: new_window} en IBM Marketplace.

 b. Adquiera una suscripción o regístrese para una prueba gratuita de 90 días.

1. Una vez configurada la cuenta de {{site.data.keyword.alertnotificationshort}}, abra [Mi panel de control de IBM ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://myibm.ibm.com/dashboard/){: new_window}.
1. Junto a IBM {{site.data.keyword.alertnotificationshort}}, pulse **Iniciar**.
1. Pulse **Gestionar claves de API** y pulse **Crear clave de API**.
1. En el campo **Crear clave de API**, escriba una descripción. 
1. Pulse **Generar**. Se muestra la información de la nueva clave de API, incluido el nombre y la contraseña. Necesita esta información para la configuración de la integración de la herramienta, de modo que mantenga abierta la ventana Nueva clave de API. Por motivos de seguridad, no puede recuperar posteriormente la contraseña de la clave de API. 

### Configuración de Alert Notification

1. Si configura la integración de esta herramienta al crear la cadena de herramientas, en la sección Integraciones configurables, pulse **{{site.data.keyword.alertnotificationshort}}**. 
1. Si tiene una cadena de herramientas y le está añadiendo esta integración de herramientas, en el panel de instrumentos de DevOps, en la página **Cadenas de herramientas**, pulse la cadena de herramientas para abrir su página Visión general. Como alternativa, en la página Visión general de la app, en la tarjeta de Entrega continua, pulse **Ver cadena de herramientas**. A continuación, pulse **Visión general**.  

 a. Pulse **Añadir una herramienta**.

 b. En la sección Integraciones de herramientas, pulse **{{site.data.keyword.alertnotificationshort}}**.

1. Escriba el URL para la API de {{site.data.keyword.alertnotificationshort}} que desea utilizar. Encontrará el URL en la página Gestionar claves de API del servicio {{site.data.keyword.alertnotificationshort}}; por ejemplo, `https://ibmnotifybm.mybluemix.net/api/alerts/v1`.
1. Escriba el nombre de la clave de API correspondiente a {{site.data.keyword.alertnotificationshort}}. Encontrará el nombre de clave de API en la ventana Nueva clave de API. 
1. Escriba la contraseña que {{site.data.keyword.alertnotificationshort}} ha generado para la clave de API. Encontrará la contraseña de clave de API en la ventana Nueva clave de API. 
1. Pulse **Crear integración**.
1. En la cadena de herramientas, pulse **{{site.data.keyword.alertnotificationshort}}**.

Para obtener más información, consulte [IBM {{site.data.keyword.alertnotificationshort}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/devops/method/content/manage/tool_alert_notification/){: new_window}.


## Configuración de Artifactory
{: #artifactory}

Configure el gestor de repositorios Artifactory para que guarde los artefactos de compilación en el repositorio de Artifactory (repositorio):

1. Si configura la integración de esta herramienta al crear la cadena de herramientas, en la sección Integraciones configurables, pulse **Artifactory**.
1. Si tiene una cadena de herramientas y le está añadiendo esta integración de herramientas, en el panel de instrumentos de DevOps, en la página **Cadenas de herramientas**, pulse la cadena de herramientas para abrir su página Visión general. Como alternativa, en la página Visión general de la app, en la tarjeta de Entrega continua, pulse **Ver cadena de herramientas**. A continuación, pulse **Visión general**.  

 a. Pulse **Añadir una herramienta**.

 b. En la sección Integraciones de herramientas, pulse **Artifactory**. 

1. Escriba el URL del repositorio de Artifactory que desea abrir al pulsar la tarjeta Artifactory. 
1. Seleccione el tipo de repositorio con el que desea conectar. 
1. Si utiliza un registro Artifactory npm, siga estos pasos:

 un. Escriba la dirección de correo electrónico asociada al registro.

 b. Escriba la señal de autenticación asociada al registro.

 c. Escriba el URL del repositorio de release de Artifactory, que es el registro privado del servidor de Artifactory. 

 d. Escriba el URL del registro de duplicación o público que utiliza para combinar varios registros npm públicos y privados. Por ejemplo, este URL podría ser el URL del registro virtual en el servidor de Artifactory que puede acceder tanto al registro privado como a la memoria caché del registro global de npm. 

1. Si utiliza un repositorio Artifactory Maven, siga estos pasos:

 a. Escriba el ID de usuario asociada al repositorio. 

 b. Escriba la contraseña asociada al repositorio. 

 c. Escriba el URL del repositorio de release de Artifactory, que es el repositorio de release privado del servidor de Artifactory. 

 d. Escriba el URL del repositorio de instantáneas de Artifactory, que es el repositorio de instantáneas privado del servidor de Artifactory. 

 e. Escriba el URL del repositorio de duplicación o público que utiliza para combinar varios repositorios Maven públicos y privados. Por ejemplo, este URL podría ser el URL del repositorio virtual en el servidor de Artifactory que puede acceder tanto al repositorio privado como a la memoria caché del repositorio central de Maven.

1. Pulse **Crear integración**.
1. Pulse la tarjeta correspondiente al repositorio de Artifactory con el que desee trabajar. Se abrirá el sitio web de Artifactory, donde puede ver el contenido del repositorio.
1. Opcional: si utiliza una cadena de herramientas en {{site.data.keyword.Bluemix_notm}} Público y desea crear la app utilizando Artifactory con npm, configure el conducto para añadir un trabajo de compilación de npm. Para obtener instrucciones sobre cómo configurar el trabajo de creación, consulte [Configuración de un trabajo de compilación de npm de Artifactory en el conducto](#config_artifactory_npm).
1. Opcional: si utiliza una cadena de herramientas en {{site.data.keyword.Bluemix_notm}} Público y desea crear la app utilizando Artifactory con Maven, configure el conducto para añadir un trabajo de compilación de Maven. Para obtener instrucciones sobre cómo configurar el trabajo de compilación, consulte [Configuración de un trabajo de compilación de Maven de Artifactory en el conducto](#config_artifactory_maven).

### Configuración de un trabajo de compilación de npm de Artifactory en el conducto
{: #config_artifactory_npm}

Antes de configurar un trabajo de compilación de npm en el conducto, necesita un conducto en funcionamiento que pueda utilizar para crear el repositorio SCM como entrada y debe configurar Artifactory Labs para su cadena de herramientas. Para obtener instrucciones sobre cómo configurar Artifactory, consulte la sección [Artifactory](#artifactory). 

Configure el {{site.data.keyword.deliverypipeline}} para añadir un trabajo de compilación de npm: 

1. Cree una etapa y establezca la entrada al repositorio SCM adecuado.
1. En la etapa, añada un trabajo de trabajo de compilación. 
1. Configure el trabajo de compilación: ![Trabajo de compilación de npm](images/artifactory_npm_job.png)

  a. Para el tipo de compilador, seleccione **Compilación de NPM**.

  b. Si ha configurado varias instancias de la integración de herramientas de Artifactory, escriba el nombre de la integración de herramientas de Artifactory para la que desea configurar el trabajo de compilación. 

  c. Para el tipo de integración de herramientas, seleccione **Artifactory**.

  d. Para el mandato de compilación, escriba los mandatos para crear el módulo npm o publicarlo en el registro. En este ejemplo se muestran los mandatos para crear el módulo o publicarlo.
     ```
     npm install
     # or
     npm publish --registry "${NPM_RELEASE_URL}"
     ```
  **Consejo**: Encontrará el URL y las credenciales de usuario que ha utilizado para conectar con el registro en los valores de configuración correspondientes a la integración de herramientas de Artifactory.
  e. Si el trabajo de compilación publica en el registro de Artifactory y el formato de su versión del módulo de nodo es `x.y.z-SNAPSHOT.w`, marque el recuadro de selección **Incrementar versión del módulo de instantánea**.  El trabajo de compilación actualiza automáticamente la versión del módulo antes de que el trabajo publique en el registro de Artifactory. El trabajo selecciona la versión más alta del módulo a partir del registro de npm y el archivo `package.json` local e incrementa la versión del módulo utilizando semver. El trabajo de compilación no envía los cambios al repositorio SCM.

1. Pulse **GUARDAR**. Siempre que se ejecute el conducto, este trabajo de compilación utilizará la información de configuración de la integración de herramientas de Artifactory para conectar con el registro de npm. 

### Configuración de un trabajo de compilación de Maven de Artifactory en el conducto
{: #config_artifactory_maven}

Antes de configurar un trabajo de compilación de Maven en el conducto, necesita un conducto en funcionamiento que pueda utilizar para crear el repositorio SCM como entrada y debe configurar Artifactory para su cadena de herramientas. Para obtener instrucciones sobre cómo configurar Artifactory, consulte la sección [Artifactory](#artifactory). 

Configure {{site.data.keyword.deliverypipeline}} para añadir un trabajo de compilación de Maven: 

1. Cree una etapa y establezca la entrada al repositorio SCM adecuado.
1. En la etapa, añada un trabajo de trabajo de compilación. 
1. Configure el trabajo de compilación: ![Trabajo de compilación de Maven](images/artifactory_maven_job.png)

  a. Para el tipo de compilador, seleccione **Compilación de Maven**.

  b. Si ha configurado varias instancias de la integración de herramientas de Artifactory, escriba el nombre de la integración de herramientas de Artifactory para la que desea configurar el trabajo de compilación de Maven. 

  c. Para el tipo de integración de herramientas, seleccione **Artifactory**.

  d. Para el mandato de compilación, escriba los mandatos para crear el módulo Maven o publicarlo en el registro de instantáneas. En este ejemplo se muestran los mandatos para crear el módulo o publicarlo en un registro de instantáneas.
     ```
     mvn -B clean package
     # or
     mvn -DaltDeploymentRepository="snapshots::default::${MAVEN_SNAPSHOT_URL}" deploy
     ```
  **Consejo**: Encontrará el URL y las credenciales de usuario que ha utilizado para conectar con el registro en los valores de configuración correspondientes a la integración de herramientas de Artifactory.
1. Pulse **GUARDAR**. Siempre que se ejecute el conducto, este trabajo de compilación utilizará la información de configuración de la integración de herramientas de Artifactory para conectar con el registro de Maven. 

Para obtener más información, consulte [Artifactory ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/devops/method/content/code/tool_artifactory/){: new_window}.


## Adición de supervisión de disponibilidad
{: #availabilitymonitoring}

{{site.data.keyword.prf_hublong}} aísla problemas, identifica patrones y mejora el rendimiento antes de que los usuarios se vean afectados. Puede probar la app desde ubicaciones de todo el mundo, integrar con conductos de entrega y obtener perspectivas sobre cómo optimizar el código continuamente. 

**Nota**: esta integración de herramientas está preconfigurada y no requiere ningún parámetro de configuración. No puede volver a configurar esta integración de herramientas.

Para probar, supervisar y mejorar el estado de la appa medida que la crea, añada la integración de herramientas de {{site.data.keyword.prf_hubshort}}: 

1. Si tiene una cadena de herramientas y le está añadiendo esta integración de herramientas, en el panel de instrumentos de DevOps, en la página Cadenas de herramientas, pulse la cadena de herramientas para abrir su página Visión general. Si lo prefiere, en la página Visión general de la app, en la tarjeta de Entrega continua, pulse **Ver cadena de herramientas** y luego **Visión general**.

 a. Pulse **Añadir una herramienta**.

 b. En la sección Integraciones de herramientas, pulse **{{site.data.keyword.prf_hubshort}}**.

1. Pulse **Crear integración**.
1. Pulse **{{site.data.keyword.prf_hubshort}}** para abrir el panel de control de {{site.data.keyword.prf_hubshort}}, seleccione una app y configure la supervisión para la app.

Para obtener más información, consulte [{{site.data.keyword.prf_hublong}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/devops/method/content/manage/tool_bluemix_availability_monitoring/){: new_window}.


## Adición de gestión de sucesos de nube (experimental)
{: #cloudeventmanagement}

{{site.data.keyword.evtmgt_full}} proporciona una vista consolidada de los problemas que se producen con los servicios, las aplicaciones y la infraestructura. Puede configurar un sistema de gestión de incidentes en tiempo real para resolver los problemas de forma más eficiente.

**Nota:** esta integración de herramientas está preconfigurada y no requiere ningún parámetro de configuración. No puede volverla a configurar.


Para ayudar al equipo de DevOps a alcanzar un estado operativo fiable, calidad de servicio y mejora continua de objetivos, añada la función de gestión de sucesos de nube (Cloud Event Management) a su cadena de herramientas:

1. En el panel de control de DevOps, pulse la página Cadenas de herramientas a la que desea añadir la gestión de sucesos de nube. Si lo prefiere, en la página Visión general de la app, en la tarjeta de Entrega continua, pulse **Ver cadena de herramientas** y luego **Visión general**.

 a. Pulse **Añadir una herramienta**.

 b. En la sección Integraciones de herramientas, pulse **Gestión de sucesos de nube**. 

1. Pulse **Crear integración**.
1. En la cadena de herramientas, pulse cualquiera de las siguientes tarjetas de herramientas: 

 * **Gestión de sucesos de nube** para empezar a trabajar con la gestión de sucesos de nube. 

 * **{{site.data.keyword.alertnotificationshort}}** para crear políticas que determinen cuándo recibirán los usuarios notificaciones de incidencias.

 * **Automatización de Runbook** para gestionar el catálogo de runbooks en la herramienta Cloud Event Management.


## Configuración de Delivery Pipeline
{: #deliverypipeline}

{{site.data.keyword.deliverypipeline}} automatiza el despliegue continuado de los proyectos a través de secuencias de fases que recuperan entradas y ejecutan trabajos, como compilaciones, pruebas y despliegues.

Configure {{site.data.keyword.deliverypipeline}} para automatizar la creación, las pruebas y el despliegue automáticos de sus apps:

1. Si configura la integración de esta herramienta al crear la cadena de herramientas, en la sección Integraciones configurables, pulse **{{site.data.keyword.deliverypipeline}}**. En función de la plantilla que utilice, los campos disponibles serán distintos. Revise los valores del campo predeterminado y, si es necesario, realice cambios.
1. Si tiene una cadena de herramientas y le está añadiendo esta integración de herramientas, en el panel de instrumentos de DevOps, en la página **Cadenas de herramientas**, pulse la cadena de herramientas para abrir su página Visión general. Si lo prefiere, en la página Visión general de la app, en la tarjeta de Entrega continua, pulse **Ver cadena de herramientas** y luego **Visión general**.

 a. Pulse **Añadir una herramienta**.

 b. En la sección Integraciones de herramientas, pulse **{{site.data.keyword.deliverypipeline}}**.

1. Especifique un nombre para el nuevo conducto.
1. Si tiene previsto utilizar el conducto para desplegar una interfaz de usuario, seleccione el recuadro de selección **Mostrar apps en el menú VER APP**. Todas las apps creadas por el conducto se muestran en la lista **Ver app** de la página de visión general de la cadena de herramientas.
1. Pulse **Crear integración** para añadir el {{site.data.keyword.deliverypipeline}} a la cadena de herramientas.
1. Pulse **{{site.data.keyword.deliverypipeline}}** para ver el conducto y configurarlo. Para obtener información básica sobre cómo configurar un conducto, consulte [Creación y despliegue de conductos](/docs/services/ContinuousDelivery/pipeline_build_deploy.html){: new_window}.

  **Consejo**: Si desea activar el conducto cuando envíe cambios a GitHub, {{site.data.keyword.ghe_short}} o al repositorio Git (repo), debe configurar GitHub, {{site.data.keyword.ghe_short}} o Git Repos and Issue Tracking para la cadena de herramientas antes de definir las etapas para el conducto. Las etapas del conducto necesitan los URL Git para los repositorios. Cada etapa de conducto puede hacer referencia a un único repositorio de GitHub, {{site.data.keyword.ghe_short}} o Git que esté asociado con la cadena de herramientas. Para obtener instrucciones sobre cómo configurar GitHub, consulte la sección [GitHub](#github). Para obtener instrucciones sobre cómo configurar {{site.data.keyword.ghe_short}}, consulte [Iniciación a {{site.data.keyword.ghe_long}}](/docs/services/ghededicated/index.html){: new_window}. Para obtener instrucciones para configurar Git Repos and Issue Tracking, consulte la sección [Git Repos and Issue Tracking](##gitbluemix).     

  **Nota:** Si no tiene privilegios de administrador para el repositorio GitHub o GitHub Enterprise ni privilegios de Maestro o de Propietario sobre el repositorio de Git Repos and Issue Tracking con el que va a enlazar, la integración se verá limitada porque no podrá utilizar un webhook. Los webhooks se necesitan para activar automáticamente un conducto cuando se envía una confirmación al repositorio. Sin un webhook, debe iniciar los conductos manualmente.

1. Opcional: si utiliza una cadena de herramientas en {{site.data.keyword.Bluemix_notm}} Público y desea que Sauce Labs ejecute pruebas en la app, configure el {{site.data.keyword.deliverypipeline}} para añadir el trabajo de pruebas Sauce Labs. Para obtener instrucciones sobre cómo configurar el trabajo de pruebas, consulte [Configuración de un trabajo de pruebas Sauce Labs en el conducto](#config_saucelabs).

### Configuración de un trabajo de pruebas Sauce Labs en el conducto
{: #config_saucelabs}

Antes de configurar un trabajo de pruebas Sauce Labs en el conducto, necesita un conducto de trabajo que incluya fases para crear y desplegar la app, y debe configurar Sauce Labs para su cadena de herramientas. Para obtener instrucciones sobre cómo configurar Sauce Labs, consulte la sección [Sauce Labs](#saucelabs).

Configure el {{site.data.keyword.deliverypipeline}} para añadir un trabajo de pruebas Sauce Labs:

1. Si no tiene ninguna etapa que despliegue una versión de pruebas de su app, cree una.
1. En la etapa, añada un trabajo de prueba después del trabajo de despliegue. Disponer de estos trabajos en la misma etapa permite que accedan al mismo conjunto de propiedades del entorno.
     
  ![Trabajo de prueba](images/toolchain_test_job.png)

1. Configure la fase:

  a. En el separador **PROPIEDADES DE ENTORNO**, cree tres propiedades: CF_APP_NAME, SAUCE_USERNAME y SAUCE_ACCESS_KEY.

  b. Introduzca su nombre de usuario y clave de acceso para Sauce Labs. De este modo, externaliza estos valores para poder utilizarlos en sus pruebas.

1. Configure el trabajo de despliegue. En el campo **Desplegar script**, incluya este mandato: `export CF_APP_NAME="$CF_APP"`. Este mandato exporta el nombre de la app como propiedad del entorno.
1. Configure el trabajo de prueba. Los valores de la imagen siguiente son ejemplos. Los campos **Instancia de servicio**, **Destino**, **Organización** y **Espacio** se rellenan con el nombre de usuario de Sauce Labs, la región, la organización y el espacio que se está utilizando.
  
![Trabajo de configuración](images/toolchain_configure_job.png)

  a. Para el tipo de prueba, seleccione **Sauce Labs**.

  b. Para la instancia de servicio, seleccione el nombre de usuario de Sauce Labs que ha utilizado al configurar Sauce Labs para su cadena de herramientas.

   **Consejo**: para ver el nombre de usuario y la clave de acceso que ha utilizado al configurar Sauce Labs para su cadena de herramientas, pulse **Configurar**.

  c. En el campo **Probar mandato de ejecución**, especifique los mandatos que instalan las dependencias necesarias para las pruebas y, a continuación, ejecute las pruebas. Por ejemplo, para una app Node.js, puede introducir estos mandatos:
     ```
     npm install
     node_modules/grunt-cli/bin/grunt test:sauce:parallel
     ```

    d. Si desea ver los informes de las pruebas en los registros del trabajo de prueba, seleccione el recuadro de selección **Habilitar informe de prueba** y establezca el valor de Probar patrón de archivo de resultado en `test/*.xml`.

1. Pulse **GUARDAR**. Siempre que se ejecute su conducto, se ejecutarán las pruebas de Sauce Labs.

Para obtener más información, consulte [Delivery Pipeline ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/devops/method/content/deliver/tool_delivery_pipeline/){: new_window}.


## Adición de DevOps Insights (Beta)
{: #dra}

{{site.data.keyword.DRA_full}} recopila y analiza los resultados de las pruebas de unidad, de las pruebas funcionales y de las herramientas de cobertura de código para determinar si el código cumple los criterios predefinidos en las puertas especificadas del proceso de despliegue. Si el código no cumple o excede los criterios, el despliegue se detiene para evitar la exposición a riesgos. Puede utilizar {{site.data.keyword.DRA_short}} como red de seguridad para el entorno de entrega continuada o como método para implementar y mejorar los estándares de calidad.

 **Nota**: esta integración de herramientas solo está disponible en {{site.data.keyword.Bluemix_notm}} público. Está preconfigurada y no requiere ningún parámetro de configuración. No puede volver a configurar esta integración de herramientas.

Añada {{site.data.keyword.DRA_short}} para mantener y mejorar la calidad de su código en {{site.data.keyword.Bluemix_notm}} supervisando las implementaciones para identificar los riesgos antes de distribuir la app.

1. Si tiene una cadena de herramientas y le está añadiendo esta integración de herramientas, en el panel de instrumentos de DevOps, en la página **Cadenas de herramientas**, pulse la cadena de herramientas para abrir su página Visión general. Si lo prefiere, en la página Visión general de la app, en la tarjeta de Entrega continua, pulse **Ver cadena de herramientas** y luego **Visión general**.

 a. Pulse **Añadir una herramienta**.

 b. En la sección Integraciones de herramientas, pulse **{{site.data.keyword.DRA_short}}**.

1. Pulse **Crear integración**.
1. Pulse **{{site.data.keyword.DRA_short}}** y, a continuación, complete los primeros pasos: crear criterios, conectar los criterios al conducto y ejecutar el conducto. 

Para obtener más información, consulte [{{site.data.keyword.DRA_short}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/devops/method/content/learn/tool_devops_insights/){: new_window}.


## Adición del IDE Eclipse Orion Web
{: #webide}

Eclipse Orion {{site.data.keyword.webide}} es un entorno integrado basado en web en el que puede crear, editar, ejecutar, depurar y controlar las tareas de control del código fuente. Puede pasar sin problemas de editar a ejecutar, enviar y desplegar.

 **Nota**: esta integración de herramientas está preconfigurada. No es necesario configurar ningún parámetro y tampoco es posible modificar la configuración existente.

Para completar las tareas de control del código fuente, añada la integración de herramientas Eclipse Orion {{site.data.keyword.webide}}:

1. Si tiene una cadena de herramientas y le está añadiendo esta integración de herramientas, en el panel de instrumentos de DevOps, en la página **Cadenas de herramientas**, pulse la cadena de herramientas para abrir su página Visión general. Si lo prefiere, en la página Visión general de la app, en la tarjeta de Entrega continua, pulse **Ver cadena de herramientas** y luego **Visión general**.

 a. Pulse **Añadir una herramienta**.

 b. En la sección Integraciones de herramientas, pulse **Eclipse Orion Web IDE**.

1. Pulse **Crear integración**.
1. Pulse **Eclipse Orion {{site.data.keyword.webide}}**. El espacio de trabajo ya contiene los repositorios de GitHub o {{site.data.keyword.ghe_short}}. Los repositorios que están asociados a la cadena de herramientas actual aparecen resaltados.

Para obtener más información, consulte [Edición de código con Eclipse Orion {{site.data.keyword.webide}}](/docs/services/ContinuousDelivery/web_ide.html){: new_window} y [Eclipse Orion {{site.data.keyword.webide}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/devops/method/content/code/tool_eclipse_orion_web_ide/){: new_window}.


## Configuración de Git Repos and Issue Tracking (experimental)
{: #gitbluemix}

La integración de la herramienta Git Repos and Issue Tracking se basa en GitLab Community Edition, que es un servicio de alojamiento basado en web para repositorios Git. Puede tener copias locales y remotas de sus repositorios. Para obtener más información, consulte [Git Repos and Issue Tracking (experimental)![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://git.ng.bluemix.net/help){:new_window}.

Si configura Git Repos and Issue Tracking mientras crea la cadena de herramientas, siga estos pasos:    

1. En la sección Integraciones configurables, pulse **Git Repos and Issue Tracking**. 
1. Revise las ubicaciones de destino predeterminadas para el repositorio Git. Dichos repositorios se clonan a partir del repositorio de ejemplo. Si es necesario, cambie el nombre de los repositorios de destino.
 

Si tiene una cadena de herramientas y le está añadiendo Git Repos and Issue Tracking, siga estos pasos:    

1. En el panel de control de DevOps, en la página **Cadenas de herramientas**, pulse sobre la cadena de herramientas para abrir la página Visión general correspondiente. Si lo prefiere, en la página Visión general de la app, en la tarjeta de Entrega continua, pulse **Ver cadena de herramientas** y luego **Visión general**.
1. Pulse **Añadir una herramienta**.
1. En la sección Integraciones de herramientas, pulse **Git Repos and Issue Tracking**. 
1. Seleccione un tipo de repositorio:
     

  a. Para crear un repositorio vacío, seleccione **Nuevo** para el tipo de repositorio y escriba un nombre de repositorio.     
  b. Para bifurcar un repositorio Git de modo que pueda aportar cambios a través de solicitudes de fusión, pulse **Bifurcar** para el tipo de repositorio.Escriba el URL del repositorio de origen.    
  c. Para crear una copia de un repositorio Git, pulse **Clonar** para el tipo de repositorio. Escriba un nuevo nombre de repositorio y el URL del repositorio de origen.      
  d. Si tiene un repositorio Git y desea utilizarlo, pulse **Existente** para el tipo de repositorio. Escriba el URL.    

1. Si desea utilizar la aplicación Issues para realizar un seguimiento de los problemas, marque el recuadro de selección **Habilitar Issues**.
1. Si desea realizar un seguimiento del despliegue de cambios en el código mediante la creación de etiquetas y comentarios en las confirmaciones, y etiquetas y comentarios en los problemas a los que hacen referencia las confirmaciones, marque el recuadro de selección **Hacer un seguimiento del despliegue cambios de código**. Para obtener más información, consulte [Seguimiento de dónde se despliega el código con cadenas de herramientas ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/blogs/bluemix/2017/03/track-code-deployed-toolchains/){:new_window}.
1. Pulse **Crear integración**.
1. Pulse la tarjeta correspondiente al repositorio Git con el que desee trabajar. Se abrirá la página de visión general del proyecto.     

**Nota:** Si no tiene privilegios de Maestro o de Propietario sobre el repositorio con el que va a enlazar, la integración se verá limitada porque no podrá utilizar un webhook. Los webhooks se necesitan para activar automáticamente un conducto cuando se envía una confirmación al repositorio. Sin un webhook, debe iniciar los conductos manualmente.


## Configuración de GitHub and Issues
{: #github}

GitHub es un servicio de alojamiento basado en web para repositorios Git. Puede tener copias locales y remotas de sus repositorios, lo que facilita la colaboración.

GitHub
Issues es una herramienta de seguimiento que mantiene todo su trabajo y sus planificaciones en un mismo lugar. Está integrado con el repositorio de desarrollo de modo que pueda centrarse en las tareas importantes.

Configure GitHub para gestionar el código fuente en la nube:

1. Si configura la integración de esta herramienta mientras crea la cadena de herramientas, siga estos pasos:

 a. En la sección Integraciones configurables, pulse **GitHub**. Si está creando la cadena de herramientas en {{site.data.keyword.Bluemix_notm}} Público y no ha autorizado a {{site.data.keyword.Bluemix_notm}} acceso a GitHub, pulse **Autorizar** para ir al sitio web de GitHub. Si no tiene ninguna sesión de GitHub activa, se le solicitará que inicie sesión. Pulse **Autorizar aplicación** para permitir que {{site.data.keyword.Bluemix_notm}} acceda a su cuenta de GitHub. Si tiene una sesión activa de GitHub pero no ha introducido recientemente su contraseña, es posible que se le solicite que introduzca la contraseña de GitHub para confirmarla.

 b. Revise las ubicaciones de repositorio de destino predeterminadas para el repositorio de GitHub. Dichos repositorios se clonan a partir del repositorio de ejemplo. Si es necesario, cambie el nombre de los repositorios de destino.
 ![Ubicaciones de repositorio de destino predeterminadas](images/toolchain_github_config.png)

1. Si tiene una cadena de herramientas y le está añadiendo esta integración de herramientas, en el panel de instrumentos de DevOps, en la página **Cadenas de herramientas**, pulse la cadena de herramientas para abrir su página Visión general. Si lo prefiere, en la página Visión general de la app, en la tarjeta de Entrega continua, pulse **Ver cadena de herramientas** y luego **Visión general**.

 a. Pulse **Añadir una herramienta**.

 b. En la sección Integraciones de herramientas, pulse **GitHub**. 

1. Si tiene un repositorio de GitHub y desea utilizarlo, pulse **Existente** y escriba el URL. 
1. Si desea utilizar un repositorio nuevo de GitHub, escriba un nombre para el repositorio de GitHub, escriba el URL del repositorio que está clonando o bifurcando y seleccione el tipo de repositorio:

 a. Para crear un repositorio vacío, pulse **Nuevo**.

 b. Para crear una copia de un repositorio de GitHub, pulse **Clonar**.

 c. Para bifurcar un repositorio de GitHub de modo que pueda aportar cambios a través de todas las solicitudes de extracción, pulse **Bifurcar**.

1. Si desea utilizar GitHub Issues para realizar un seguimiento de los problemas, seleccione el recuadro de selección **Habilitar GitHub Issues**.
1. Si desea realizar un seguimiento del despliegue de cambios en el código mediante la creación de etiquetas y comentarios en las confirmaciones, y etiquetas y comentarios en los problemas a los que hacen referencia las confirmaciones, marque el recuadro de selección **Hacer un seguimiento del despliegue cambios de código**. Para obtener más información, consulte [Seguimiento de dónde se despliega el código con cadenas de herramientas ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/blogs/bluemix/2017/03/track-code-deployed-toolchains/){:new_window}.
1. Pulse **Crear integración**.
1. Pulse la tarjeta correspondiente al repositorio GitHub con el que desee trabajar. Se abrirá el sitio web de GitHub, donde puede ver el contenido del repositorio.

  **Consejo**: puede utilizar estas herramientas integradas de gestión del código fuente en Eclipse Orion {{site.data.keyword.webide}} para editar el repositorio de GitHub y desplegar una app desde su espacio de trabajo.

1. Si ha habilitado GitHub Issues, pulse **GitHub Issues** para abrirlo. Puede utilizar esta instancia de GitHub Issues para toda la cadena de herramientas, aunque la cadena de herramientas contenga varios repositorios GitHub.     

**Nota:** Si no tiene privilegios de administrador sobre el repositorio con el que va a enlazar, la integración se verá limitada porque no podrá utilizar un webhook. Los webhooks se necesitan para activar automáticamente un conducto cuando se envía una confirmación al repositorio. Sin un webhook, debe iniciar los conductos manualmente.

Para obtener más in formación, consulte [GitHub ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/devops/method/content/code/tool_github/){: new_window} y [GitHub Issues ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}.


## Configuración de GitHub Enterprise and Issues en Bluemix dedicado
{: #configghe}

 **Nota:** Estas instrucciones se aplican a {{site.data.keyword.Bluemix_notm}} dedicado para {{site.data.keyword.ghe_short}}. Si utiliza su propia versión gestionada de {{site.data.keyword.ghe_short}}, algunos pasos pueden diferir en función de sus procedimientos internos.

{{site.data.keyword.ghe_long}} es un servicio de alojamiento basado en web para repositorios Git. {{site.data.keyword.ghe_short}} dedicado es únicamente para clientes de {{site.data.keyword.Bluemix_notm}} dedicado. GitHub Issues es una herramienta de seguimiento que mantiene todo su trabajo y sus planificaciones en un mismo lugar. Está integrado con el repositorio de desarrollo de modo que pueda centrarse en las tareas importantes. Para obtener más información sobre {{site.data.keyword.ghe_short}} dedicado y GitHub Issues, consulte [Iniciación a {{site.data.keyword.ghe_long}}](/docs/services/ghededicated/index.html){: new_window} y [GitHub Issues ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}.

Puede configurar {{site.data.keyword.ghe_short}} como una integración de herramientas de la cadena de herramientas para que pueda gestionar el código fuente en la instancia de [{{site.data.keyword.Bluemix_notm}} Dedicado de la empresa](/docs/dedicated/index.html#dedicated){: new_window}.

1. Si configura la integración de esta herramienta mientras crea la cadena de herramientas, siga estos pasos:

 a. Antes de iniciar sesión en {{site.data.keyword.ghe_short}} Dedicado por primera vez, pida al administrador de región de su empresa que añada su ID de usuario a la instancia de {{site.data.keyword.Bluemix_notm}} Dedicado desde el registro de usuario de la empresa utilizando LDAP. Para obtener información sobre cómo configurar la cuenta de {{site.data.keyword.ghe_short}}, consulte [Iniciación a {{site.data.keyword.ghe_long}}](/docs/services/ghededicated/index.html){: new_window}.

 b. En la sección Integraciones configurables, pulse **{{site.data.keyword.ghe_short}}**.    

 c. Revise el nombre predeterminado para el nuevo repositorio de {{site.data.keyword.ghe_short}}. Si es necesario, cambie el nombre del repositorio nuevo. La siguiente imagen muestra un ejemplo de un repositorio clonado desde un repositorio de ejemplo. Puede utilizar un repositorio existente o uno nuevo. Para utilizar un repositorio nuevo, puede crear un repositorio vacío, clonarlo o bifurcarlo. 
 ![Ubicaciones de repositorio predeterminado](images/toolchain_ghe_config.png)

1. Si tiene una cadena de herramientas y le está añadiendo esta integración de herramientas, en el panel de instrumentos de DevOps, en la página **Cadenas de herramientas**, pulse la cadena de herramientas para abrir su página Visión general. Si lo prefiere, en la página Visión general de la app, en la tarjeta de Entrega continua, pulse **Ver cadena de herramientas** y luego **Visión general**.

 a. Pulse **Añadir una herramienta**.

 b. En la sección Integraciones de herramientas, pulse **{{site.data.keyword.ghe_short}}**.

1. Si tiene un repositorio de {{site.data.keyword.ghe_short}} que desea utilizar, escriba el URL para el repositorio. Para el tipo de repositorio, pulse **Existente**.
1. Si desea utilizar un repositorio nuevo de {{site.data.keyword.ghe_short}}, escriba un nombre para el repositorio, escriba el URL del repositorio que está clonando o bifurcando y seleccione el tipo de repositorio:

 a. Para crear un repositorio vacío, pulse **Nuevo**.

 b. Para crear una copia de un repositorio, pulse **Clonar**.

 c. Para bifurcar un repositorio de modo que pueda aportar cambios a través de todas las solicitudes de extracción, pulse **Bifurcar**.

1. Para utilizar GitHub Issues para realizar un seguimiento de los problemas, seleccione el recuadro de selección **Habilitar GitHub Issues**.
1. Pulse **Crear integración**.
1. Pulse la tarjeta correspondiente al repositorio {{site.data.keyword.ghe_short}} con el que desee trabajar. Se abrirá el repositorio de {{site.data.keyword.ghe_short}} de la empresa.

  **Consejo**: puede utilizar estas herramientas integradas de gestión del código fuente en Eclipse Orion {{site.data.keyword.webide}} para editar el repositorio de {{site.data.keyword.ghe_short}} y desplegar una app desde su espacio de trabajo.

1. Si ha habilitado GitHub Issues, pulse **GitHub Issues**. Puede utilizar esta instancia de GitHub Issues para toda la cadena de herramientas, aunque la cadena de herramientas contenga varios repositorios GitHub.     

**Nota:** Si no tiene privilegios de administrador sobre el repositorio con el que va a enlazar, la integración se verá limitada porque no podrá utilizar un webhook. Los webhooks se necesitan para activar automáticamente un conducto cuando se envía una confirmación al repositorio. Sin un webhook, debe iniciar los conductos manualmente.


## Configuración de Jenkins
{: #jenkins}

Jenkins es una herramienta de código abierto basada en la web que compila y prueba software continuamente, dando soporte a prácticas de integración continua y de entrega continua. 

**Importante**: Antes de crear una integración de herramientas Jenkins, debe tener un servidor Jenkins. 

Con la integración de herramientas Jenkins, puede enviar notificaciones de trabajos Jenkins a otras herramientas de la cadena de herramientas, como por ejemplo Slack y PagerDuty. Para realizar un seguimiento del código en los despliegues, puede añadir mensajes de despliegue a sus confirmaciones Git y a los problemas de Git o JIRA relacionados. También puede ver los despliegues en la página Conexiones de cadena de herramientas. Puede enviar los resultados de las pruebas a {{site.data.keyword.DRA_short}}, añadir objetivos de calidad automatizados y realizar un seguimiento del riesgo del despliegue. 

Configure Jenkins para automatizar la creación, las pruebas y el despliegue automáticos de sus apps:

1. Si configura la integración de esta herramienta al crear la cadena de herramientas, en la sección Integraciones configurables, pulse **Jenkins**.
1. Si tiene una cadena de herramientas y le está añadiendo esta integración de herramientas, en el panel de instrumentos de DevOps, en la página **Cadenas de herramientas**, pulse la cadena de herramientas para abrir su página Visión general. Como alternativa, en la página Visión general de la app, en la tarjeta de Entrega continua, pulse **Ver cadena de herramientas**. A continuación, pulse **Visión general**.  

 a. Pulse **Añadir una herramienta**.

 b. En la sección Integraciones de herramientas, pulse **Jenkins**. 

1. Escriba el nombre que desea visualizar para esta integración de herramientas en la tarjeta de Jenkins de la cadena de herramientas.
1. Escriba el URL correspondiente al servidor Jenkins que desea abrir cuando pulse la tarjeta de Jenkins en la cadena de herramientas.
1. Copie el webhook de la cadena de herramientas generado. 
1. En el servidor Jenkins, siga estos pasos: 

 a. Instale la [CLI de Cloud Foundry ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html){: new_window}.

 b. Instale el plugin IBM Cloud DevOps Cloud Foundry con uno de estos mandatos: 

  * Mac OS: `cf install-plugin https://icd.ng.bluemix.net/icd_darwin_amd64`

  * Linux o Docker: `cf install-plugin https://icd.ng.bluemix.net/icd_linux_amd64`

 c. Instale y configure el plugin IBM Cloud DevOps Jenkins para DevOps Insights and Notifications. Para obtener más información, consulte [Instalación y configuración del plugin](/docs/services/DevOpsInsights/insights_risk.html#integrate_jenkins){: new_window}.

 d. En cada trabajo para el que desea enviar notificaciones a la cadena de herramientas, siga estos pasos:

  * Marque el recuadro de selección **Este proyecto esté parametrizado**. 

  * Añada el parámetro `ICD_WEBHOOK_URL`. 

  * Pegue el webhook de cadena de herramientas generado.
 ![URL del Webhook](images/jenkins_webhook_url.png)

  * Añada una acción posterior a la compilación para IBM Cloud DevOps - Webhook Notification y marque el recuadro de selección **Trabajo completado**. ![Acción posterior a la compilación](images/jenkins_postbuild_action.png)  

 e. En los trabajos de despliegue, siga estos pasos: 

  * Añada los parámetros `ICD_WEBHOOK_URL`, `CF_API`, `CF_ORG`, `CF_SPACE` y `CF_APP`. En estos ejemplos se muestra cómo añadir cada uno de estos parámetros. ![Parámetro Webhook URL](images/jenkins_set_webhook_url.png)
 ![Parámetro CFI API](images/jenkins_set_cfapi.png)
 ![Parámetro CFI ORG](images/jenkins_set_cforg.png)
 ![Parámetro CFI SPACE](images/jenkins_set_cfspace.png)
 ![Parámetro CFI APP](images/jenkins_set_cfapp.png)

  * Configure los enlaces para la CLI de Cloud Foundry mediante la variable de nombre de usuario `CF_CREDS_USR` y la variable de contraseña `CF_CREDS_PSW`. ![Enlaces de CLI de Cloud Foundry](images/jenkins_config_bindings.png)  

  * En el campo **Compilación**, escriba estos mandatos para iniciar una sesión y utilizar el plugin de IBM Cloud DevOps Cloud Foundry para enviar correlaciones que se puedan desplegar en la aplicación, con capacidad de rastreo de confirmaciones de Git, a la cadena de herramientas: ![Mandatos de compilación](images/jenkins_build_commands.png)    

  * En el campo **Compilación**, escriba el mandato `cf icd --create-connection $ICD_WEBHOOK_URL $CF_APP` para enviar las correlaciones que se pueden desplegar en la aplicación a la cadena de herramientas.     

 f. Guarde los cambios y vuelva a la página Configurar la integración para la integración de herramientas de Jenkins. 

1. Pulse **Crear integración**.
1. En la cadena de herramientas, pulse **Jenkins** para ver el servidor Jenkins.   

Para obtener más información, consulte [Jenkins ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/devops/method/content/deliver/tool_jenkins/){: new_window}.


## Configuración de JIRA
{: #jira}

JIRA es una herramienta que realiza un seguimiento de problemas y errores relacionados con el software. La integración de herramientas JIRA actualiza los problemas del proyecto cuando Jenkins o {{site.data.keyword.deliverypipeline}} ejecutan un despliegue. Para que la integración de herramientas JIRA realice el seguimiento de los problemas, debe utilizar JIRA Smart Commits en los mensajes de confirmación. Para obtener más in formación sobre JIRA Smart Commits, consulte [Utilización de Smart Commits ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://confluence.atlassian.com/fisheye/using-smart-commits-298976812.html){: new_window}.

Configure JIRA de modo que planifique, realice un seguimiento y distribuya código de calidad:

1. Si configura la integración de esta herramienta al crear la cadena de herramientas, en la sección Integraciones configurables, pulse **JIRA**.
1. Si tiene una cadena de herramientas y le está añadiendo esta integración de herramientas, en el panel de instrumentos de DevOps, en la página **Cadenas de herramientas**, pulse la cadena de herramientas para abrir su página Visión general. Como alternativa, en la página Visión general de la app, en la tarjeta de Entrega continua, pulse **Ver cadena de herramientas**. A continuación, pulse **Visión general**.  

 a. Pulse **Añadir una herramienta**.

 b. En la sección Integraciones de herramientas, pulse **JIRA**. 

1. Si tiene un proyecto JIRA y desea conectar con el mismo, para el tipo de JIRA pulse **Existente**:

 a. Escriba la clave de proyecto JIRA para el proyecto JIRA. Encontrará la clave del proyecto en el URL del proyecto JIRA. 

 b. Escriba el URL de la API base de la instancia de JIRA. Encontrará el URL de la API en la cabecera de la instancia de JIRA. Pulse el icono **Administración** y pulse **Sistema**.

 c. Opcional: Escriba su nombre de usuario de JIRA. El nombre de usuario solo es necesario si va a conectar con una instancia privada de JIRA o si va a conectar con una instancia pública y desea recibir información sobre capacidad de rastreo. 

 d. Opcional: Escriba su contraseña de JIRA. La contraseña solo es necesaria si va a conectar con una instancia privada de JIRA o si va a conectar con una instancia pública y desea recibir información sobre capacidad de rastreo. 

 e. Para realizar un seguimiento del despliegue de cambios en el código para el proyecto mediante la creación de etiquetas y comentarios para problemas a los que se hace referencia, marque el recuadro de selección **Hacer un seguimiento del despliegue de cambios de código**. Asegúrese de utilizar JIRA Smart Commit para hacer referencia a los problemas de JIRA en las confirmaciones de GitHub. Si no selecciona esta opción, la integración de herramientas JIRA pasa por alto las confirmaciones.

1. Si desea crear un proyecto JIRA, para el tipo de JIRA pulse **Nuevo**:

 a. Escriba una clave de proyecto JIRA que utilizará para el proyecto nuevo. Esta clave se utiliza como identificador exclusivo en el URL del proyecto. 

 b. Escriba un nombre para el proyecto JIRA. 

 c. Escriba el URL de API base para la instancia de JIRA. Encontrará el URL de la API en la cabecera de la instancia de JIRA. Pulse el icono **Administración** y pulse **Sistema**.

 d. Escriba el nombre de usuario para el responsable del proyecto JIRA que desea utilizar para este proyecto. Para especificar alguien como responsable de proyecto JIRA, dicha persona debe tener permiso de responsable del proyecto en JIRA.

 e. Escriba el nombre de usuario del administrador de esta instancia de JIRA.

 f. Escriba la contraseña del administrador de esta instancia de JIRA.

 g. Para realizar un seguimiento del despliegue de cambios en el código para el proyecto mediante la creación de etiquetas y comentarios para problemas a los que se hace referencia, marque el recuadro de selección **Hacer un seguimiento del despliegue de cambios de código**. Asegúrese de utilizar JIRA Smart Commit para hacer referencia a los problemas de JIRA en las confirmaciones de GitHub. Si no selecciona esta opción, la integración de herramientas JIRA pasa por alto las confirmaciones.

1. Pulse **Crear integración**.
1. Desde la cadena de herramientas, pulse **JIRA** para ver el panel de control del proyecto JIRA al que se ha conectado.

Para obtener más información, consulte [JIRA ![icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/devops/method/content/code/tool_jira/){: new_window}.


## Configuración de Nexus
{: #nexus}

Configure el gestor de repositorios Nexus para que guarde los artefactos de compilación en el repositorio de Nexus (repo):

1. Si configura la integración de esta herramienta al crear la cadena de herramientas, en la sección Integraciones configurables, pulse **Nexus**.
1. Si tiene una cadena de herramientas y le está añadiendo esta integración de herramientas, en el panel de instrumentos de DevOps, en la página **Cadenas de herramientas**, pulse la cadena de herramientas para abrir su página Visión general. Como alternativa, en la página Visión general de la app, en la tarjeta de Entrega continua, pulse **Ver cadena de herramientas**. A continuación, pulse **Visión general**.  

 a. Pulse **Añadir una herramienta**.

 b. En la sección Integraciones de herramientas, pulse **Nexus**. 

1. Escriba un nombre para esta instancia de la integración de herramientas Nexus.
1. Escriba el URL correspondiente al repositorio Nexus que desea abrir cuando pulse la tarjeta de Nexus en la cadena de herramientas.
1. Seleccione el tipo de repositorio con el que desea conectar. 
1. Si ha seleccionado **Registro de npm**, siga estos pasos:

 un. Escriba la dirección de correo electrónico asociada al registro.

 b. Escriba la señal de autenticación asociada al registro.

 c. Escriba el URL del repositorio de release de Nexus, que es el registro privado del servidor de Nexus. 

 d. Escriba el URL del registro de duplicación o público que utiliza para combinar varios registros npm públicos y privados. Por ejemplo, este URL podría ser el URL del registro virtual en el servidor de Nexus que puede acceder tanto al registro privado como a la memoria caché del registro global de npm. 

1. Si ha seleccionado **Repositorio de Maven**, siga estos pasos:

 a. Escriba el ID de usuario asociada al repositorio. 

 b. Escriba la contraseña asociada al repositorio. 

 c. Escriba el URL del repositorio de release de Nexus, que es el repositorio de release privado del servidor de Nexus. 

 d. Escriba el URL del repositorio de instantáneas de Nexus, que es el repositorio de instantáneas privado del servidor de Nexus. 

 e. Escriba el URL del repositorio de duplicación o público que utiliza para combinar varios repositorios Maven públicos y privados. Por ejemplo, este URL podría ser el URL del repositorio virtual en el servidor de Nexus que puede acceder tanto al repositorio privado como a la memoria caché del repositorio central de Maven.

1. Pulse **Crear integración**.
1. En la cadena de herramientas, pulse la tarjeta correspondiente al repositorio Nexus con el que desee trabajar. Se abrirá el sitio web de Nexus, donde puede ver el contenido del repositorio.
1. Opcional: si utiliza una cadena de herramientas en {{site.data.keyword.Bluemix_notm}} Público y desea crear la app utilizando Nexus con npm, configure el conducto para añadir un trabajo de compilación de npm. Para obtener instrucciones sobre cómo configurar el trabajo de creación, consulte [Configuración de un trabajo de compilación de npm de Nexus en el conducto](#config_nexus_npm).
1. Opcional: si utiliza una cadena de herramientas en {{site.data.keyword.Bluemix_notm}} Público y desea crear la app utilizando Nexus con Maven, configure el conducto para añadir un trabajo de compilación de Maven. Para obtener instrucciones sobre cómo configurar el trabajo de creación, consulte [Configuración de un trabajo de compilación de Maven de Nexus en el conducto](#config_nexus_maven).

### Configuración de un trabajo de compilación de npm de Nexus en el conducto
{: #config_nexus_npm}

Antes de configurar un trabajo de compilación de npm en el conducto, necesita un conducto en funcionamiento que pueda utilizar para crear el repositorio SCM como entrada y debe configurar Nexus para su cadena de herramientas. Para obtener instrucciones sobre cómo configurar Nexus, consulte la sección [Nexus](#nexus). 

Configure {{site.data.keyword.deliverypipeline}} para añadir un trabajo de compilación de npm: 

1. Cree una etapa y establezca la entrada al repositorio SCM adecuado.
1. En la etapa, añada un trabajo de trabajo de compilación. 
1. Configure el trabajo de compilación: ![Trabajo de compilación de npm](images/nexus_npm_job.png)

  a. Para el tipo de compilador, seleccione **Compilación de NPM**.

  b. Si ha configurado varias instancias de la integración de herramientas de Nexus, escriba el nombre de la integración de herramientas de Nexus para la que desea configurar el trabajo de compilación. 

  c. Para el tipo de integración de herramientas, seleccione **Nexus**.

  d. Para el mandato de compilación, escriba los mandatos para crear el módulo npm o publicarlo en el registro. En este ejemplo se muestran los mandatos para crear el módulo o publicarlo.
     ```
     npm install
     # or
     npm publish --registry "${NPM_RELEASE_URL}"
     ```
  **Consejo**: Encontrará el URL y las credenciales de usuario que ha utilizado para conectar con el registro en los valores de configuración correspondientes a la integración de herramientas de Nexus.
  e. Si el trabajo de compilación publica en el registro de Nexus y el formato de su versión del módulo de nodo es `x.y.z-SNAPSHOT.w`, marque el recuadro de selección **Incrementar versión del módulo de instantánea**.  El trabajo de compilación actualiza automáticamente la versión del módulo antes de que publique en el registro de Nexus. El trabajo de compilación selecciona la versión más alta del módulo a partir del registro de npm y el archivo `package.json` local e incrementa la versión del módulo utilizando semver. El trabajo de compilación no envía los cambios al repositorio SCM.

1. Pulse **GUARDAR**. Siempre que se ejecute el conducto, este trabajo de compilación utilizará la información de configuración de la integración de herramientas de Nexus para conectar con el registro de npm. 

### Configuración de un trabajo de compilación de Maven de Nexus en el conducto
{: #config_nexus_maven}

Antes de configurar un trabajo de compilación de Maven en el conducto, necesita un conducto en funcionamiento que pueda utilizar para crear el repositorio SCM como entrada y debe configurar Nexus para su cadena de herramientas. Para obtener instrucciones sobre cómo configurar Nexus, consulte la sección [Nexus](#nexus). 

Configure {{site.data.keyword.deliverypipeline}} para añadir un trabajo de compilación de Maven: 

1. Cree una etapa y establezca la entrada al repositorio SCM adecuado.
1. En la etapa, añada un trabajo de trabajo de compilación. 
1. Configure el trabajo de compilación: ![Trabajo de compilación de Maven](images/nexus_maven_job.png)

  a. Para el tipo de compilador, seleccione **Compilación de Maven**.

  b. Si ha configurado varias instancias de la integración de herramientas de Nexus, escriba el nombre de la integración de herramientas de Nexus para la que desea configurar el trabajo de compilación de Maven. 

  c. Para el tipo de integración de herramientas, seleccione **Nexus**.

  d. Para el mandato de compilación, escriba los mandatos para crear el módulo Maven o publicarlo en el registro de instantáneas. En este ejemplo se muestran los mandatos para crear el módulo o publicarlo.
     ```
     mvn -B clean package
     # or
     mvn -DaltDeploymentRepository="snapshots::default::${MAVEN_SNAPSHOT_URL}" deploy
     ```
  **Consejo**: Encontrará el URL y las credenciales de usuario que ha utilizado para conectar con el registro en los valores de configuración correspondientes a la integración de herramientas de Nexus.
1. Pulse **GUARDAR**. Siempre que se ejecute el conducto, este trabajo de compilación utilizará la información de configuración de la integración de herramientas de Nexus para conectar con el registro de Maven. 

Para obtener más información, consulte [Nexus ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/devops/method/content/code/tool_nexus/){: new_window}.


## Configuración de una herramienta personalizada (Otras herramientas)
{: #othertool}

Si el equipo utiliza una herramienta no incluida en la lista de integraciones de las cadenas de herramientas, puede integrar una herramienta personalizada.

Configure una herramienta personalizada para que funcione con otras herramientas de la cadena de herramientas y que esté disponible para el equipo:

1. Si configura la integración de esta herramienta al crear la cadena de herramientas, en la sección Integraciones configurables, pulse **Otra herramienta**.
1. Si tiene una cadena de herramientas y le está añadiendo esta integración de herramientas, en el panel de instrumentos de DevOps, en la página **Cadenas de herramientas**, pulse la cadena de herramientas para abrir su página Visión general. Si lo prefiere, en la página Visión general de la app, en la tarjeta de Entrega continua, pulse **Ver cadena de herramientas** y luego **Visión general**.

 a. Pulse **Añadir una herramienta**.

 b. En la sección Integraciones de herramientas, pulse **Otra herramienta**. 

1. Escriba el nombre de la herramienta.
1. Seleccione la fase del ciclo de vida que esté asociada de forma más cercana con la herramienta. Esta selección determina la categoría en la que se lista la herramienta en la página Visión general.
1. Añada un URL de icono. El icono se mostrará en la tarjeta de la integración de herramientas. 
1. Añada un URL de documentación.
1. Especifique un nombre de instancia de la herramienta. Por ejemplo: My Team Tool.
1. Añada un URL de instancia de herramienta. Este URL se abre siempre que se pulsa en la tarjeta de la integración de herramientas. 
1. Añada una descripción de la herramienta.
1. (Avanzado) Añada propiedades adicionales si es necesario. Por ejemplo, liste cualquier información o atributos necesarios para que la herramienta se integre con otras herramientas en la cadena de herramientas.  
1. Pulse **Crear integración**.

Para obtener más información, consulte [Introducción a la integración de herramientas personalizadas para cadenas de herramientas de {{site.data.keyword.Bluemix_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/blogs/bluemix/2016/10/custom-tool-integration-with-bluemix-toolchains/){: new_window}.


## Configuración de PagerDuty
{: #pagerduty}

PagerDuty integra datos de varios sistemas de supervisión en una única vista. Cuando se produce un problema, PagerDuty se asegura de que el miembro del equipo más adecuado para corregirlo reciba una notificación. Si el miembro del equipo no responde al problema, pueden configurarse sistemas de escalado para pasar el problema a ingenieros o gestores de operaciones secundarios.

Configure PagerDuty para enviar notificaciones cuando se producen errores en la fase de conducto para que pueda corregir los problemas con mayor celeridad y reducir el tiempo de inactividad:

1. Si configura la integración de esta herramienta al crear la cadena de herramientas, en la sección Integraciones configurables, pulse **PagerDuty**.
1. Si tiene una cadena de herramientas y le está añadiendo esta integración de herramientas, en el panel de instrumentos de DevOps, en la página **Cadenas de herramientas**, pulse la cadena de herramientas para abrir su página Visión general. Si lo prefiere, en la página Visión general de la app, en la tarjeta de Entrega continua, pulse **Ver cadena de herramientas** y luego **Visión general**.

 a. Pulse **Añadir una herramienta**.

 b. En la sección Integraciones de herramientas, pulse **PagerDuty**. 

1. Escriba la clave de acceso de API para su cuenta de PagerDuty. Si no dispone de una cuenta de PagerDuty, [regístrese para obtener una ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://signup.pagerduty.com/accounts/new){: new_window}. Para ver instrucciones para localizar la clave, consulte [Generación de una clave de API ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://support.pagerduty.com/hc/en-us/articles/202829310-Generating-an-API-Key){: new_window}.
1. Escriba el nombre del servicio PagerDuty.
1. Escriba la dirección de correo electrónico del contacto principal de PagerDuty.
1. Escriba el número de teléfono del contacto principal de PagerDuty.
1. Pulse **Crear integración**.
1. Pulse **PagerDuty** para ir a pagerduty.com. Puede ver los sucesos asociados con el servicio PagerDuty que ha especificado al configurar la integración de esta herramienta para su cadena de herramientas.

Para obtener más información, consulte [PagerDuty ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/devops/method/content/manage/tool_pagerduty/){: new_window}.


## Configuración de Sauce Labs
{: #saucelabs}

Sauce Labs ejecuta pruebas de unidad funcionales. Cuando se configura una suite de pruebas de Sauce Labs como trabajo de pruebas en {{site.data.keyword.deliverypipeline}}, la suite de pruebas puede ejecutar pruebas para la app web o móvil como parte del proceso de entrega continuo. Estas pruebas pueden proporcionar un control de flujo muy valioso para los proyectos, y actuar como pasarelas para evitar el despliegue de código defectuoso.

 **Nota**: esta integración de herramientas solo está disponible en {{site.data.keyword.Bluemix_notm}} público. 

Configure Sauce Labs para ejecutar pruebas funcionales automatizadas en varios sistemas operativos y navegadores a fin de poder emular el modo en que el usuario puede utilizar un sitio web o una aplicación:

1. Si configura la integración de esta herramienta al crear la cadena de herramientas, en la sección Integraciones configurables, pulse **Sauce Labs**.
1. Si tiene una cadena de herramientas y le está añadiendo esta integración de herramientas, en el panel de instrumentos de DevOps, en la página **Cadenas de herramientas**, pulse la cadena de herramientas para abrir su página Visión general. Si lo prefiere, en la página Visión general de la app, en la tarjeta de Entrega continua, pulse **Ver cadena de herramientas** y luego **Visión general**.

 a. Pulse **Añadir una herramienta**.

 b. En la sección Integraciones de herramientas, pulse **Sauce Labs**. 

1. Escriba el nombre de usuario asociado con su cuenta de Sauce Labs. Puede [encontrar su nombre de usuario len la página de bienvenida en la parte superior de la página de la cuenta de Sauce Labs ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://saucelabs.com/account){: new_window}.
1. Escriba la clave de acceso para su cuenta de Sauce Labs. Puede [encontrar la clave en la página de la cuenta de Sauce Labs ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://saucelabs.com/account){: new_window}.
1. Pulse **Crear integración**.
1. Pulse **Sauce Labs** para ir a saucelabs.com y ver la actividad de pruebas de la cadena de herramientas. 

 **Consejo**: si ha añadido un trabajo de pruebas de Sauce Labs al {{site.data.keyword.deliverypipeline}}, puede seleccionar la instancia del servicio.

Para obtener más información, consulte [Sauce Labs ![icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/devops/method/content/code/tool_sauce_labs/){: new_window}.


## Configuración de Slack
{: #slack}

**Importante**: las notificaciones que se publican en canales Slack públicos son visibles para todas las personas del equipo. Recuerde que es responsable de todo el contenido que publique.

Slack es un sistema de notificaciones y mensajería en tiempo real y basado en la nube. Slack proporciona una función de chat permanente, que es una alternativa más interactiva que el correo electrónico para facilitar la colaboración del equipo. Puede comunicarse con su equipo en un canal dedicado o en un conjunto de canales directamente relacionados con su trabajo. Asimismo, puede compartir archivos e imágenes a través de los canales o a través de mensajes directos entre dos o más personas. Las comunicaciones en los mensajes directos y en los canales se conservan para poder realizar búsquedas.

Configure Slack para recibir notificaciones acerca de su cadena de herramientas desde las integraciones de herramientas, como actividades de prueba y de despliegue:

1. Si configura la integración de esta herramienta al crear la cadena de herramientas, en la sección Integraciones configurables, pulse **Slack**.
1. Si tiene una cadena de herramientas y le está añadiendo esta integración de herramientas, en el panel de instrumentos de DevOps, en la página **Cadenas de herramientas**, pulse la cadena de herramientas para abrir su página Visión general. Si lo prefiere, en la página Visión general de la app, en la tarjeta de Entrega continua, pulse **Ver cadena de herramientas** y luego **Visión general**.

 a. Pulse **Añadir una herramienta**.

 b. En la sección Integraciones de herramientas, pulse **Slack**. 

1. Escriba el URL del webhook de Slack, que genera Slack en forma de webhook de entrada. Necesita un URL de webhook de Slack para recibir notificaciones acerca de su cadena de herramientas desde las integraciones de herramientas. Para ver instrucciones sobre cómo crear o encontrar su webhook, consulte [Webhooks de entrada ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://api.slack.com/incoming-webhooks){: new_window}.

 **Consejo**: Si ha estado utilizando una clave de API para el canal de Slack para recibir notificaciones acerca de la cadena de herramientas desde las integraciones de herramientas, debe actualizar la configuración para que utilice un webhook en su lugar.

1. Escriba el nombre del canal Slack al que desea enviar las notificaciones. El canal debe existir y debe estar activo en el equipo de Slack. 
1. Escriba el nombre de host del URL para el equipo de Slack, que es la palabra o frase que precede a `.slack.com` en el URL del equipo. Por ejemplo, si el URL del equipo es `https://team.slack.com`, el nombre de host es `team`.
1. Pulse **Crear integración**.

 **Consejo**: Si no se puede acceder al canal y al equipo de Slack que ha especificado, se muestra el error `Error de configuración` en la tarjeta de Slack. Mueva el cursor sobre el mensaje `Error de configuración` y pulse **Reconfigurar**. Asegúrese de utilizar parámetros de configuración válidos para el URL del webhook de Slack, el canal de Slack y el nombre de host del URL del equipo de Slack. Actualice los valores según sus necesidades y pulse **Guardar integración**.

1. Pulse **Slack**. Puede ver toda la actividad de su cadena de herramientas en el canal Slack configurado.

Para obtener más información, consulte [Slack ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/devops/method/content/culture/tool_slack/){: new_window}.
