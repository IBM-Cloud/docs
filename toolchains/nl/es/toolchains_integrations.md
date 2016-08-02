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

*Última actualización: 17 de junio de 2016*
{: .last-updated}

Puede configurar integraciones de herramientas que admitan tareas de desarrollo, despliegue y operaciones mientras crea una cadena de herramientas, o bien puede añadir y configurar integraciones de herramientas par personalizar una cadena de herramientas existente.   
{:shortdesc}

**Importante**: esta capacidad es experimental. Es posible que las cadenas de herramientas no sean estables y que cambien de tal modo que no sean compatibles con versiones anteriores. No se recomienda su uso en entornos de producción. Para utilizar cadenas de herramientas, debe realizar una [solicitud única de acceso](https://new-console.ng.bluemix.net/devops?cm_mmc=IBMBluemixGarageMethod-_-MethodSite-_-10-19-15::12-31-18-_-toolchains-welcome-page){: new_window}. Las cadenas de herramientas están disponibles únicamente en el sur de EE. UU. 

**Consejo**: si desea empezar a desarrollar su propio código, asegúrese de que configura las integraciones de las herramientas GitHub y GitHub Issues antes de configurar el {{site.data.keyword.deliverypipeline}}.

## Configuración del conducto de entrega
{: #deliverypipeline}

El {{site.data.keyword.deliverypipeline}} automatiza el despliegue continuado de los proyectos a través de secuencias de fases que recuperan entradas y ejecutan trabajos, como compilaciones, pruebas y despliegues.  

Configure el {{site.data.keyword.deliverypipeline}} para automatizar la creación, las pruebas y el despliegue automáticos de sus apps:  

1. Si configura la integración de esta herramienta al crear la cadena de herramientas, en la sección Configurable Integrations, pulse **Delivery Pipeline**. En función de la plantilla que utilice, los campos disponibles serán distintos. Revise los valores del campo predeterminado y, si es necesario, realice cambios. 
1. Si tiene una cadena de herramientas y añade esta integración de herramienta a dicha cadena, en el panel de control DevOps, en la pestaña **Cadenas de herramientas**, pulse la cadena de herramientas para abrir la página de integraciones de herramientas. Como alternativa, en la página Visión general de la aplicación, en el título Entrega continua, pulse **Ver cadena de herramientas**. A continuación, pulse **Tool Integrations**. 
1. Pulse el botón de adición (+).
1. En la sección Tool Integrations, pulse **Delivery Pipeline**.
1. Especifique un nombre para el nuevo conducto. 
1. Sis tiene previsto utilizar el conducto para desplegar una interfaz de usuario, seleccione la casilla **Viewable App**. Todas las apps creadas por el conducto se muestran en la lista **VIEW APP** de la página Tool Integrations de la cadena de herramientas. 
1. Pulse **Create Integration** para añadir el {{site.data.keyword.deliverypipeline}} a la cadena de herramientas. 
1. Pulse el título para {{site.data.keyword.deliverypipeline}} para ver el conducto y configurarlo. Para obtener información básica sobre como configurar un conducto, consulte [Creación y despliegue de conductos](../services/DeliveryPipeline/build_deploy.html){: new_window}.

  **Consejo**: si desea activar el conducto al transferir cambios al repositorio de GitHub, debe configurar GitHub para la cadena de herramientas antes de definir las fases del conducto. Las fases del conducto necesitan los URL Git para el repositorio de GitHub. Cada fase de conducto puede hacer referencia a un único repositorio de GigHub que esté asociado con la cadena de herramientas. Para obtener instrucciones sobre cómo configurar GitHub, consulte la sección [GitHub y GitHub Issues](#github). 
  
1. Opcional: si desea que Sauce Labs ejecute pruebas en la app, configure el {{site.data.keyword.deliverypipeline}} para añadir el trabajo de pruebas Sauce Labs. Para obtener instrucciones sobre cómo configurar el trabajo de pruebas, consulte [Configuración de un trabajo de pruebas Sauce Labs en el conducto](#config_saucelabs). 

### Configuración de un trabajo de pruebas Sauce Labs en el conducto
{: #config_saucelabs}

Antes de configurar un trabajo de pruebas Sauce Labs en el conducto, necesita un conducto de trabajo que incluya fases para crear y desplegar la app, y debe configurar Sauce Labs para su cadena de herramientas. Para obtener instrucciones sobre cómo configurar Sauce Labs, consulte la sección [Sauce Labs](#saucelabs). 

Configure el {{site.data.keyword.deliverypipeline}} para añadir un trabajo de pruebas Sauce Labs:

1. Si no tiene ninguna fase que despliegue una versión de pruebas de su app, cree una. 
1. En la fase, añada un trabajo de prueba después del trabajo de despliegue. Disponer de estos trabajos en la misma fase permite que accedan al mismo conjunto de propiedades del entorno. ![Trabajo de prueba](images/toolchain_test_job.png) 

1. Configure la fase: 

  a. En la pestaña **ENVIRONMENT PROPERTIES**, cree tres propiedades: CF_APP_NAME, SAUCE_USERNAME y SAUCE_ACCESS_KEY.
  
  b. Introduzca su nombre de usuario y clave de acceso para Sauce Labs. De este modo, externaliza estos valores para poder utilizarlos en sus pruebas. 
  
1. Configure el trabajo de despliegue. En el campo **Deploy Script**, incluya este mandato: export CF_APP_NAME="$CF_APP". Este mandato exporta el nombre de la app como propiedad del entorno. 
1. Configure el trabajo de prueba. Los valores de la imagen siguiente son ejemplos. Los campos **Service Instance**, **Target**, **Organization** y **Space** se rellenan con el nombre de usuario de Sauce Labs, la región, la organización y el espacio que se está utilizando actualmente.
![Trabajo de configuración](images/toolchain_configure_job.png)

  a. Para e tipo de prueba, seleccione **Sauce Labs**.
  
  b. Como nombre de instancia, seleccione el nombre de usuario de Sauce Labs que ha utilizado al configurar Sauce Labs para su cadena de herramientas.  
  
   **Consejo**: para ver el nombre de usuario y la clave de acceso que ha utilizado al configurar Sauce Labs para su cadena de herramientas, pulse **Configurar**. 
  
  c. En el campo **Test Execution Command**, especifique los mandatos que instalan las dependencias necesarias para las pruebas y, a continuación, ejecute las pruebas. Por ejemplo, para una app Node.js hipotética, puede introducir lo siguiente: 
     ```
     npm install
     node_modules/grunt-cli/bin/grunt test:sauce:parallel
     ```
  
    d. Si desea ver los informes de las pruebas en los registros del trabajo de prueba, seleccione la casilla **Enable Test Report** y establezca el valor de Test Result File Pattern en `test/*.xml`.
  
1. Pulse **SAVE**. Ahora, siempre que se ejecute su conducto se ejecutarán las pruebas de Sauce Labs. 

Para obtener más información, consulte [Conducto de entrega](https://www.ibm.com/devops/method/content/deliver/tool_build_and_deploy/){: new_window}.

## Adición de Deployment Risk Analytics
{: #dra}

{{site.data.keyword.DRA_full}} recopila y analiza los resultados de las pruebas de unidad, de las pruebas funcionales y de las herramientas de cobertura de código para determinar si el código cumple los criterios predefinidos en las puertas especificadas del proceso de despliegue. Si el código no cumple o excede los criterios, el despliegue se detiene para evitar la exposición a riesgos. Puede utilizar Deployment Risk Analytics como red de seguridad para el entorno de entrega continuada o como método para implementar y mejorar los estándares de calidad.  

 **Consejo**: esta integración de herramienta está pre-configurada. No es necesario configurar ningún parámetro y tampoco es posible modificar la configuración existente. 
 
Añada Deployment Risk Analytics para mantener y mejorar la calidad de su código en Bluemix supervisando las implementaciones para identificar los riesgos antes de distribuir la aplicación: 

1. Si tiene una cadena de herramientas y añade esta integración de herramienta a dicha cadena, en el panel de control DevOps, en la pestaña **Cadenas de herramientas**, pulse la cadena de herramientas para abrir la página de integraciones de herramientas. Como alternativa, en la página Visión general de la aplicación, en el título Entrega continua, pulse **Ver cadena de herramientas**. A continuación, pulse **Tool Integrations**. 
1. Pulse el botón de adición (+).
1. En la sección Tool Integrations, pulse **Deployment Risk Analytics**. 
1. Pulse **Create Integration**.
1. Pulse en el título para Deployment Risk Analytics y, a continuación, complete los primeros pasos: crear criterios, conectar los criterios al conducto y ejecutar el conducto. Para obtener más información, consulte [Deployment Risk Analytics](https://www.ibm.com/devops/method/content/deliver/tool_deployment_risk_analytics/){: new_window}.

## Adición de Eclipse Orion {{site.data.keyword.webide}}
{: #webide}

Eclipse Orion {{site.data.keyword.webide}} es un entorno integrado basado en web en el que puede crear, editar, ejecutar, depurar y controlar las tareas de control del código fuente. Puede pasar sin problemas de editar a ejecutar, enviar y desplegar.  

 **Consejo**: esta integración de herramienta está pre-configurada. No es necesario configurar ningún parámetro y tampoco es posible modificar la configuración existente. 
 
Añada la integración de la herramienta Eclipse Orion {{site.data.keyword.webide}} para completar las tareas de control del código fuente: 

1. Si tiene una cadena de herramientas y añade esta integración de herramienta a dicha cadena, en el panel de control DevOps, en la pestaña **Cadenas de herramientas**, pulse la cadena de herramientas para abrir la página de integraciones de herramientas. Como alternativa, en la página Visión general de la aplicación, en el título Entrega continua, pulse **Ver cadena de herramientas**. A continuación, pulse **Tool Integrations**. 
1. Pulse el botón de adición (+).
1. En la sección Tool Integrations, pulse **Eclipse Orion Web IDE**. 
1. Pulse **Create Integration**.
1. Pulse el título para el nuevo Eclipse Orion Web IDE. El espacio de trabajo ya contiene el repositorio de GitHub. Los repositorios que están asociados a la cadena de herramientas actual aparecen resaltados. 

Para obtener más información, consulte [Web IDE](https://www.ibm.com/devops/method/content/code/tool_web_ide/){: new_window}.


## Configuración de GitHub y GitHub Issues
{: #github}

GitHub es un servicio de alojamiento basado en web para repositorios Git. Puede tener copias locales y remotas de sus repositorios, lo que facilita la colaboración.  

GitHub Issues es una herramienta de seguimiento que mantiene todo su trabajo y sus planificaciones en un mismo lugar. Está integrado con el repositorio de desarrollo de modo que pueda centrarse en las tareas importantes. 

Configure GitHub y GitHub Issues para gestionar el código fuente en la nube: 

1. Si configura la integración de esta herramienta mientras crea la cadena de herramientas, siga estos pasos: 

 a. En la sección Configurable Integrations, pulse **GitHub**. Si no ha concedido a {{site.data.keyword.Bluemix}} acceso a GitHub, pulse **Authorize** para ir al sitio web de GitHub. Si no tiene ninguna sesión de GitHub activa, se le solicitará que inicie sesión. Pulse **Authorize Application** para permitir que {{site.data.keyword.Bluemix}} acceda a su cuenta de GitHub. Si tiene una sesión activa de GitHub pero no ha introducido recientemente su contraseña, es posible que se le solicite que introduzca la contraseña de GitHub para confirmarla. 
 
 b. Revise las ubicaciones de repositorio de destino predeterminadas para el repositorio de GitHub. Dichos repositorios se clonan a partir del repositorio de ejemplo. Si es necesario, cambie el nombre de los repositorios de destino.
![Ubicaciones de repositorio de destino predeterminadas](images/toolchain_github_config.png)
   
1. Si tiene una cadena de herramientas y añade esta integración de herramienta a dicha cadena, en el panel de control DevOps, en la pestaña **Cadenas de herramientas**, pulse la cadena de herramientas para abrir la página de integraciones de herramientas. Como alternativa, en la página Visión general de la aplicación, en el título Entrega continua, pulse **Ver cadena de herramientas**. A continuación, pulse **Tool Integrations**. 
1. Pulse el botón de adición (+).
1. En la sección Tool Integrations, pulse **GitHub**.
1. Si tiene un repositorio de GitHub y desea utilizarlo, escriba el URL. Para el tipo de repositorio, pulse **Link**.
1. Si desea utilizar un repositorio nuevo de GitHub, escriba un nombre para el repositorio de GitHub, escriba el URL del repositorio que está clonando o bifurcando y seleccione el tipo de repositorio:  

 a. Para crear un repositorio vacío, seleccione **New**. 
 
 b. Para crear una copia de un repositorio de GitHub, seleccione **Clone**.
 
 c. Para bifurcar un repositorio de GitHub de modo que pueda aportar cambios a través de todas las solicitudes de extracción, seleccione **Fork**.
 
1. Si desea utilizar GitHub Issues para realizar un seguimiento de los problemas, seleccione la casilla **Enable GitHub Issues**. 
1. Pulse **Create Integration**.
1. Pulse el título del repositorio de GitHub con el que desee trabajar para ir a github.com y ver el contenido del repositorio. 
 
  **Consejo**: puede utilizar estas herramientas integradas de gestión del código fuente en Eclipse Orion Web IDE para editar el repositorio de GitHub y desplegar una app desde su espacio de trabajo. 

1. Si ha habilitado GitHub Issues, pulse el título de GitHub Issues para ir a Issues.

Para obtener más información, consulte [GitHub](https://www.ibm.com/devops/method/content/code/tool_github/){: new_window} y [GitHub Issues](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}.    

##Uso de {{site.data.keyword.ghe_short}} dedicado
{: #ghe}

{{site.data.keyword.ghe_long}} es la versión alojada en IBM Cloud y totalmente gestionada de {{site.data.keyword.ghe_short}}, disponible para entornos Bluemix dedicados. GitHub proporciona la experiencia de codificación social preferida por los desarrolladores. [{{site.data.keyword.Bluemix_notm}} dedicado](../dedicated/index.html#dedicated){: new_window} proporciona un entorno informático en la nube en hardware aislado físicamente que se integra en su red. 

{{site.data.keyword.ghe_short}} dedicado es únicamente para clientes de {{site.data.keyword.Bluemix_notm}} dedicado. 

### Configuración de la cuenta 

{{site.data.keyword.ghe_short}} incluye un inicio de sesión único con {{site.data.keyword.Bluemix_notm}} dedicado. Para iniciar sesión en {{site.data.keyword.ghe_short}}, pegue el URL del administrador de su región o del correo electrónico de bienvenida en un navegador. El URL debe tener este patrón: `github.nombre-dedicado-empresa.bluemix.net`. Inicie sesión con su ID de usuario y contraseña para {{site.data.keyword.Bluemix_notm}} dedicado para que su cuenta de {{site.data.keyword.ghe_short}} se cree automáticamente. 

**Nota:** si un mensaje indica que su ID de usuario no existe, solicite al administrador de su zona que añada su ID de usuario en el registro de usuarios de {{site.data.keyword.Bluemix_notm}} dedicado. Si usted es el administrador de la región, consulte [Gestión de usuarios y permisos de {{site.data.keyword.Bluemix_notm}} dedicado](https://new-console.stage1.ng.bluemix.net/docs/admin/index.html#oc_useradmin){: new_window}.

En la mayoría de los casos, el nombre de usuario de GitHub es el nombre abreviado del correo electrónico, a menos que dicho nombre incluya caracteres no admitidos por GitHub, como, por ejemplo, un punto. Si el nombre incluye caracteres que GitHub no admite, dichos caracteres se sustituyen por guiones.      

### Adición de una dirección de correo electrónico a la cuenta

Para recibir notificaciones, debe añadir su dirección de correo electrónico a la configuración de su cuenta de {{site.data.keyword.ghe_short}}. Una vez que haya añadido su dirección de correo electrónico, podrá beneficiarse de las funciones de codificación sociales de {{site.data.keyword.ghe_short}}.    
 
Para añadir su dirección de correo electrónico a su cuenta de {{site.data.keyword.ghe_short}} dedicado, siga estos pasos:     
1. En la esquina superior derecha de cualquier página de GitHub, pulse en el icono de su perfil y, a continuación, pulse **Settings**.    
2. En la barra lateral, pulse **Emails**.    
3. Añada su dirección de correo electrónico y pulse **Add**.     

{: #ghe_auth}
### Creación de una señal de acceso personal o una clave SSH para la autenticación

Para realizar operaciones Git remotas como `clone` o `push` desde su repositorio local de Git, debe utilizar una señal de acceso personal o una clave SSH para autenticarse con {{site.data.keyword.ghe_short}}. La autenticación a través de HTTPS solo se admite utilizando una señal de acceso; no puede utilizar su ID de usuario y contraseña para clonar o publicar desde un repositorio local. Las solicitudes de API también requieren una señal de acceso personal. 

**Nota:** para utilizar una señal de acceso personal o una clave SSH para la autenticación, debe configurar Git localmente. Para obtener instrucciones, consulte [Configuración de Git](https://help.github.com/enterprise/2.6/user/articles/set-up-git/){: new_window}.    

Para crear una señal de acceso personal, siga estos pasos:     
   1. En la esquina superior derecha de cualquier página de GitHub, pulse en el icono de su perfil y, a continuación, pulse **Settings**.    
   2. En la barra lateral, pulse **Personal access tokens**.   
   3. Pulse **Generate new token**.
   4. Añada una descripción de la señal y pulse **Generate token**.
   5. Copie la señal en una ubicación segura o en una app de gestión de contraseñas. **Nota:** por motivos de seguridad, una vez que abandone la página ya n podrá volver a ver la señal.     

Utilice la señal de acceso personal en lugar de una contraseña para acceder a la línea de mandatos a través de HTTPS.  


Para crear una clave SSH, siga estos pasos: 
   1. Abra Git Bash (Windows) o una nueva ventana de terminal (Linux y Mac).    
   2. Pegue el texto siguiente, sustituyendo la dirección de correo electrónico por la que ha añadido en su cuenta de {{site.data.keyword.ghe_short}}: 
   
     ``
     ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
     # Crea una nueva clave ssh, utilizando como etiqueta el correo electrónico indicado
     Generar un par de claves rsa pública/privada``

   3. Cuando se le solicite que especifique un archivo en el que guardar la clave, pulse Intro para aceptar la ubicación predeterminada. 
   4. En el indicador, escriba su contraseña segura. Para obtener más información, consulte [Utilización de contraseñas de clave SSH](https://help.github.com/enterprise/2.6/user/articles/working-with-ssh-key-passphrases/){: new_window}.   

Añada su clave SSH al agente ssh:    
   1. Asegúrese de que el agente ssh esté habilitado. Introduzca el siguiente mandato mediante Git Bash para habilitar el agente ssh: ``
      # Inicie el agente ssh en segundo plano
      $ eval "$(ssh-agent -s)"
      Agent pid 59566
      ``    
  
   2. Añada su clave SSH al agente ssh mediante este mandato:
      ``
      $ ssh-add ~/.ssh/id_rsa
      ``    
   3. Añada la clave SSH a su cuenta de GitHub. Para obtener más información, consulte [Adición de una clave SSH nueva a su cuenta de GitHub](https://help.github.com/enterprise/2.6/user/articles/adding-a-new-ssh-key-to-your-github-account/){: new_window}.    
   

### Configuración de organizaciones, equipos y repositorios GitHub    

Configurar organizaciones GitHub es de gran utilidad ya que permite crear grupos distintos de usuarios que trabajan en proyectos o tareas similares. Organizar equipos dentro de una misma organización supone, además, poder controlar el acceso a los repositorios. Para obtener más información, consulte [Organizaciones y equipos](https://help.github.com/enterprise/2.6/admin/guides/user-management/organizations-and-teams/){: new_window}.

**Nota:** las organizaciones de GitHub son distintas de las de Bluemix. 

Realice las tareas siguientes para configurar el proyecto del equipo: 

   1. [Cree una organización.](https://help.github.com/enterprise/2.6/user/articles/creating-a-new-organization-account/){: new_window}.
   2. [Cree un repositorio para su organización.](https://help.github.com/enterprise/2.6/user/articles/create-a-repo/){: new_window}.
   3. [Invite a usuarios a que se unan a su organización.](https://help.github.com/enterprise/2.6/user/articles/inviting-users-to-join-your-organization/){: new_window}.
   4. [Seleccione como mínimo un miembro del equipo para asignarle permisos de propietario en su organización](https://help.github.com/enterprise/2.6/user/articles/changing-a-person-s-role-to-owner/){: new_window}.    
   
  **Nota:** antes de invitar a usuarios a su organización, deben iniciar sesión en {{site.data.keyword.ghe_short}} como mínimo una vez para que sus cuentas de {{site.data.keyword.ghe_short}} estén disponibles para la invitación. 
   
### Obtención de soporte
Para obtener respuestas, envíe sus preguntas a [Desbordamiento de pila](http://stackoverflow.com/questions/ask?tags=ibm-bluemix_github-enterprise){: new_window}. 

Para obtener más soporte, utilice estos recursos:     
   1. Complete el formulario que se encuentra en https://ibm.biz/bluemixsupport.   
   2. Envíe una nueva incidencia a través de Client Success Portal en https://support.ibmcloud.com/ics/support/mylogin.asp?login=bluemix.    


## Configuración de PagerDuty
{: #pagerduty}

PagerDuty integra datos de varios sistemas de supervisión en una única vista. Cuando se produce un problema, PagerDuty se asegura de que el miembro del equipo más adecuado para corregirlo reciba una notificación. Si el miembro del equipo no responde al problema, pueden configurarse sistemas d escalado para pasar el problema a ingenieros o gestores de operaciones secundarios. 

Configure PagerDuty para enviar notificaciones cuando se producen errores en la fase de conducto para que pueda corregir los problemas con mayor celeridad y reducir el tiempo de inactividad: 

1. Si configura la integración de esta herramienta al crear la cadena de herramientas, en la sección Configurable Integrations, pulse **PagerDuty**. 
1. Si tiene una cadena de herramientas y añade esta integración de herramienta a dicha cadena, en el panel de control DevOps, en la pestaña **Cadenas de herramientas**, pulse la cadena de herramientas para abrir la página de integraciones de herramientas. Como alternativa, en la página Visión general de la aplicación, en el título Entrega continua, pulse **Ver cadena de herramientas**. A continuación, pulse **Tool Integrations**. 
1. Pulse el botón de adición (+).
1. En la sección Tool Integrations, pulse **PagerDuty**.
1. Escriba el nombre del sitio de PagerDuty asociado con su cuenta de PagerDuty. Si no tiene ninguna cuenta de PagerDuty, [regístrese en una](https://signup.pagerduty.com/accounts/new){: new_window}.
1. Escriba la calve de acceso de API para su cuenta de PagerDuty. Para obtener instrucciones sobre cómo encontrar la clave, consulte [Autenticación de API](https://signup.pagerduty.com/accounts/new){: new_window}.
1. Escriba el nombre del servicio PagerDuty.
1. Escriba la dirección de correo electrónico del contacto principal de PagerDuty. 
1. Escriba el número de teléfono del contacto principal de PagerDuty. 
1. Pulse **Create Integration**.
1. Pulse el título de PagerDuty para ir a pagerduty.com. Puede ver los eventos asociados con el servicio PagerDuty que ha especificado al configurar la integración de esta herramienta para su cadena de herramientas.  

Para obtener más información, consulte [PagerDuty](https://www.ibm.com/devops/method/content/manage/tool_pagerduty/){: new_window}.


## Configuración de Sauce Labs
{: #saucelabs}

Sauce Labs ejecuta pruebas de unidad funcionales. Cuando se configura una suite de pruebas de Sauce Labs como trabajo de pruebas en {{site.data.keyword.deliverypipeline}}, la suite de pruebas puede ejecutar pruebas para la app web o móvil como parte del proceso de entrega continuo. Estas pruebas pueden proporcionar un control de flujo muy valioso para los proyectos, y actuar como pasarelas para evitar el despliegue de código defectuoso. 

Configure Sauce Labs para ejecutar pruebas funcionales automatizadas en varios sistemas operativos y navegadores a fin de poder emular el modo en que el usuario puede utilizar un sitio web o una aplicación: 

1. Si configura la integración de esta herramienta al crear la cadena de herramientas, en la sección Configurable Integrations, pulse **Sauce Labs**. 
1. Si tiene una cadena de herramientas y añade esta integración de herramienta a dicha cadena, en el panel de control DevOps, en la pestaña **Cadenas de herramientas**, pulse la cadena de herramientas para abrir la página de integraciones de herramientas. Como alternativa, en la página Visión general de la aplicación, en el título Entrega continua, pulse **Ver cadena de herramientas**. A continuación, pulse **Tool Integrations**. 
1. Pulse el botón de adición (+).
1. En la sección Tool Integrations, pulse **Sauce Labs**.
1. Escriba el nombre de usuario asociado con su cuenta de Sauce Labs. Puede [encontrar su nombre de usuario en el mensaje de bienvenida de la parte superior de la página de la cuenta de Sauce Labs](https://saucelabs.com/account){: new_window}.
1. Escriba la clave de acceso para su cuenta de Sauce Labs. [Encontrara la clave en la esquina inferior izquierda de la página de la cuenta de Sauce Labs](https://saucelabs.com/account){: new_window}.
1. Pulse **Create Integration**.
1. Pulse el título de Sauce Labs para ir a saucelabs.com y verla actividad de prueba para la cadena de herramientas. 

 **Consejo**: si ha añadido un trabajo de pruebas de Sauce Labs al {{site.data.keyword.deliverypipeline}}, puede seleccionar la instancia del servicio. 

Para obtener más información, consulte [Sauce Labs](https://www.ibm.com/devops/method/content/code/tool_sauce_labs/){: new_window}.


## Configuración de Slack
{: #slack}

**Importante**: las notificaciones que se publican en canales Slack públicos son visibles para todas las personas del equipo. Recuerde que es responsable de todo el contenido que publique. 

Slack es un sistema de notificaciones y mensajería en tiempo real y basado en la nube. Slack proporciona una función de chat permanente, que es una alternativa más interactiva que el correo electrónico para facilitar la colaboración del equipo. Puede comunicarse con su equipo en un canal dedicado o en un conjunto de canales directamente relacionados con su trabajo. Asimismo, puede compartir archivos e imágenes a través de los canales o a través de mensajes directos entre dos o más personas. Las comunicaciones en los mensajes directos y en los canales se conservan para poder realizar búsquedas.  

Configure Slack para recibir notificaciones acerca de su cadena de herramientas desde las integraciones de herramientas, como actividades de prueba y de despliegue: 

1. Si configura la integración de esta herramienta al crear la cadena de herramientas, en la sección Configurable Integrations, pulse **Slack**. 
1. Si tiene una cadena de herramientas y añade esta integración de herramienta a dicha cadena, en el panel de control DevOps, en la pestaña **Cadenas de herramientas**, pulse la cadena de herramientas para abrir la página de integraciones de herramientas. Como alternativa, en la página Visión general de la aplicación, en el título Entrega continua, pulse **Ver cadena de herramientas**. A continuación, pulse **Tool Integrations**.
1. Pulse el botón de adición (+).
1. En la sección Tool Integrations, pulse **Slack**.
1. Escriba la señal de autenticación de API para su cuenta de Slack. Debe utilizar la señal con acceso completo garantizado para autenticarse con Slack. Para obtener instrucciones sobre cómo encontrar la señal, consulte [Configuración de Slack](https://api.slack.com/web#authentication){: new_window}.
1. Escriba el nombre del canal Slack al que desea enviar las notificaciones. Si el canal que intenta especificar no existe, se crea. Si el canal se ha archivado, se reactiva. 
1. Pulse **Create Integration**.
1. Pulse el título de Slack. Puede ver toda la actividad de su cadena de herramientas en el canal Slack configurado. 

Para obtener más información, consulte [Slack](https://www.ibm.com/devops/method/content/culture/tool_slack/){: new_window}.
