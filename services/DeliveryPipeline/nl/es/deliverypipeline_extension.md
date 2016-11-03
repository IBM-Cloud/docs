---

copyright:
  years: 2015, 2016

---

<!-- Copyright info at top of file: REQUIRED
    The copyright info is YAML content that must occur at the top of the MD file, before attributes are listed.
    It must be surrounded by 3 dashes.
    The value "years" can contain just one year or a two years separated by a comma. (years: 2014, 2016)
    Indentation as per the previous template must be preserved.
-->

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Ampliación del servicio {{site.data.keyword.deliverypipeline}}
{: #deliverypipeline_extending}
Última actualización: 29 de agosto de 2016
{: .last-updated}

Puede ampliar las posibilidades del servicio {{site.data.keyword.deliverypipeline}} configurando los trabajos para utilizar servicios soportados. Por ejemplo, los trabajos de prueba pueden ejecutar exploraciones de código estáticas y los trabajos de compilación pueden globalizar series.
{:shortdesc}

<!-- Include a sentence to briefly introduce the steps/subtopics. Example: -->

Las tareas siguientes describen cómo integrar herramientas seleccionadas con un Delivery Pipeline.

## Ejecución de exploraciones de código estático utilizando el conducto

{: #deliverypipeline_scan}

¿Desea encontrar problemas de seguridad en el código antes de desplegarlo? Cuando utilice IBM® Static Analyzer for Bluemix™ como parte del conducto, puede ejecutar las comprobaciones automatizadas en los archivos binarios de compilación `.war`, `.ear`, `.jar`, o `.class` estáticos de la aplicación Java™.

Un conducto que utiliza el servicio de Static Analyzer normalmente incluye estas etapas:

+ Una etapa de compilación para crear los archivos de origen
+ Una etapa de procesamiento que incluye estos trabajos:
  + Un trabajo de compilación para ejecutar el servicio de Static Analyzer
  + Un trabajo de compilación para ejecutar una compilación del contenedor
+ Una etapa de despliegue para desplegar el contenedor


### Creación de una exploración de código estático

Antes de empezar, [revise las Condiciones de uso para el servicio](http://www-03.ibm.com/software/sla/sladb.nsf/sla/bm-6814-01).

<!-- Use ordered list markup for the step section. Include code examples as needed. -->

1. Cree una etapa de proceso.

  a. Pulse **AÑADIR ETAPA**.

  b. Ponga un nombre a la etapa, por ejemplo, `Procesando`.

  c. Para el tipo de entrada, seleccione **Artefactos de compilación**.

  d. Para la etapa y el trabajo, verifique los valores y actualícelos si es necesario.

2. En la etapa de proceso, añada un trabajo de compilación para ejecutar la exploración del código.

  a. En el separador **TRABAJOS**, pulse **AÑADIR TRABAJO**.

  b. Para el tipo de trabajo, seleccione la **Prueba**.

  c. Para el tipo de prueba, seleccione **IBM Security Static Analyzer**.

  d. Para la organización y el espacio, verifique los valores y actualícelos si es necesario.

  e. Seleccione o quite la marca del recuadro de selección **Configurar servicio y espacio automáticamente** según sea necesario.

    * Si desea que el conducto compruebe el espacio de Bluemix para el servicio y una aplicación que enlaza el servicio al contenedor, marque el recuadro de selección. Si el servicio o el enlazado de aplicaciones no existe, el conducto añadirá el plan gratuito del servicio a su espacio. El enlazado de aplicaciones creado se denomina `pipeline_bridge_app`. A continuación, el conducto utilizará las credenciales de pipeline_bridge_app para acceder a los servicios enlazados.

    * Si ya ha configurado el servicio y el enlazado de aplicaciones en el espacio de Bluemix, o si desea [configurar estos requisitos manualmente](https://www.ng.bluemix.net/docs/containers/container_group_pipeline_ov.html#container_binding_pipeline), deje el recuadro de selección sin marcar.

  f. En el campo **Minutos que se debe esperar para que el análisis se complete**, escriba un valor de 0 a 59 minutos. El valor predeterminado es 5 minutos. Un URL al panel de control de Static Analyzer se encuentra en los registros de consola al final del trabajo.

     Si la exploración de Static Analyzer no se ha completado antes del tiempo especificado, el trabajo fallará. Sin embargo, el análisis de la exploración continuará ejecutándose y puede verlo en el panel de control de Static Analyzer. Una vez que se ha completado la exploración de Static Analyzer, si vuelve a ejecutar el trabajo, la solicitud de exploración no se vuelve a enviar y el trabajo del conducto se puede completar. Como alternativa, puede configurar el conducto para no bloquearse en un resultado de exploraciones correctamente. Para obtener instrucciones, consulte el paso siguiente.

  g. Marque o quite la marca del recuadro de selección **Dejar de ejecutar esta etapa si el trabajo falla** en función de lo que desee que suceda si este trabajo falla o se excede el tiempo de espera. Los trabajos pueden fallar cuando las vulnerabilidades son altas.

    * Si marca el recuadro de selección y el trabajo falla, no se ejecutarán los trabajos posteriores de la etapa ni las etapas posteriores.

    * Si desmarca el recuadro de selección y el trabajo falla, la etapa continúa sin bloquear trabajos ni etapas posteriores. Por ejemplo, si sabe que el informe incluye muchos problemas para procesar, puede configurar la etapa para continuar porque la exploración puede tardar mucho tiempo. En este caso de ejemplo, es posible que no desee
que se detenga el resto de los trabajos y etapas sólo porque la exploración está tardando
demasiado tiempo.

  h. Pulse **GUARDAR**.

3. Cuando el trabajo finaliza, vea los resultados pulsando **Ver registros e historial**. Si el análisis se lleva a cabo correctamente o se excede el tiempo de espera, se mostrará un URL en los resultados de la exploración. Si el estado de la exploración es pendiente, espere hasta que se haya completado la exploración para ver los resultados completos.

4. Si tiene que ejecutar la etapa de proceso de nuevo antes de que finalice el análisis, puede hacerlo. Sin embargo, en las siguientes situaciones, no se volverá a enviar un nuevo análisis y se utilizarán los resultados anteriores:
  * La etapa de proceso todavía se estaba ejecutando cuando se ha iniciado un análisis nuevo
  * Ya se ha enviado una exploración para la compilación
  * Aún no se ha ejecutado una nueva compilación de origen

5. Para iniciar un análisis nuevo, complete uno de estos pasos:
  * Ejecute la etapa de compilación que entra en la etapa de proceso y, a continuación, ejecute la etapa de proceso de nuevo.
  * Abra el URL para los resultados de la exploración y pulse el icono **Papelera**. A continuación, ejecute la etapa de proceso de nuevo.

Ejemplos de salida de la consola:

**Exploración satisfactoria**
![Exploración satisfactoria de ejemplo](images/analyzer_success.png)

**Exploración pendiente**
![Exploración pendiente de ejemplo](images/analyzer_pending.png)

Para obtener más información sobre cómo utilizar el servicio de Static Analyzer, [consulte los documentos de servicio de Static Analyzer](https://console.ng.bluemix.net/docs/services/ApplicationSecurityonCloud/index.html).

<!--

## Globalizing strings by using the pipeline
{: #deliverypipeline_globalize}

You can translate strings automatically into other languages when you use the IBM Globalization Pipeline service with your pipeline. IBM Globalization Pipeline uses machine translation to translate your source files as part of the pipeline's build and deployment process.

You can also update the machine-translated strings within the globalization project. A translator or native speaker of the language can then review the machine-translated strings to ensure that they are of a high quality.

To see an example of a typical pipeline that uses the Globalization Pipeline service, watch this video:

<iframe width="640" height="360" src="https://www.youtube.com/embed/UToj7FIomCg?feature=player_embedded" frameborder="0" allowfullscreen></iframe>

### Creating a globalization stage and job
Before you begin:

1. All English-translatable strings should be included in one or more `filename_en.properties` or `filename_en.json` files that all use the same name. For example: `messages_en.properties`.

2. If your messages are in `.json` files, remove the depth from the structure by removing any subkeys. To remove the subkeys, change instances of `{key: {subkey: value, subkey:value}}` to `{key:value, key:value}`.

To create the globalization stage and job:

1. Create a globalization stage.

  a. Click **ADD STAGE**.

  b. Name the stage; for example, `Globalization`.

  c. For the input type, select **SCM repository**.

2. In the globalization stage, add a job to translate the source files.

  a. On the **JOBS** tab, click **ADD JOB**.

  b. For the job type, select **Build**.

  c. For the builder type, select **IBM Globalization Pipeline**.

  d. For the organization and space, verify the values and update them if needed.

  e. In the **Source file name** field, type the name and extension of the `.properties` or `.json` input file. If you have files in different subdirectories, but they all have the same name, you need to type the file name once only. For example, if you have a `messages_en.properties` file in three directories, type `messages_en.properties` for the source file name, and all files with that name will be translated.

  f. Determine whether to select the **Set up service and space for me** check box.

    * If you want the pipeline to check your Bluemix space for the service and an app that binds the service to the container, select this check box. If the service or bound app does not exist, the pipeline adds the free plan of the service to your space for you. The bound app that is created is named `pipeline_bridge_app`. Then, the pipeline uses the credentials from pipeline_bridge_app to access the bound services.

    * If you configured the service and bound app in your Bluemix space already or if you want to [configure these requirements manually](https://www.ng.bluemix.net/docs/containers/container_group_pipeline_ov.html#container_binding_pipeline), leave this check box cleared.

  g. For the Globalization bundle prefix, enter a prefix for the bundle name, which is structured in this format: `<globalization_bundle_prefix>.path.to.source.file`. The pipeline job creates this Globalization bundle for you in the Globalization Pipeline service.

    **Tip:** Use the DevOps Services project name in the prefix so that the project can be identified easily in the Globalization Pipeline service.

  h. Click **SAVE**.

3. Create another stage to package your app. For the input of the job in this stage, use the IBM Globalization Pipeline job from the previous stage. Do not use the source as the input. The Globalization Pipeline job augments the source files with the machine-translated strings.

4. To ensure that the machine-translated content is included in the packaged app, create another stage to package the app in. For the input to that stage, include the Globalization Pipeline job.

The machine translated files are placed in the same directory as the source `.properties` or `.json` file. To view the files, click **Job > Artifacts**.

After the stage is completed, you can review the translated files from the console output. You can also direct translators to the files so that they can review the machine-translation output and provide revisions to improve quality. The revisions are stored in a Cloudant™ database and take precedence over any future machine translations of the same strings.

For more information about using the Globalization Pipeline service from the Bluemix Dashboard, [see the Globalization Pipeline service documentation](https://www.ng.bluemix.net/docs/services/GlobalizationPipeline/index.html).

-->

## Creación de notificaciones de Slack para compilaciones en el conducto
{: #deliverypipeline_slack}

Puede enviar notificaciones sobre los resultados de compilación de IBM Container Service, IBM Security Static Analyzer, e IBM Globalization del Delivery Pipeline a los canales de Slack.

Antes de empezar, cree o copie un URL de WebHook de Slack:

1. Abra la página Integración de Slack para el equipo: `https://_nombre_proyecto_.slack.com/services`
2. En la lista de integraciones, localice **WebHooks entrantes** y pulse **Añadir**.
3. Seleccione un canal y pulse **Añadir integración de WebHooks entrantes**.
4. Añada un **URL de WebHook** o copie uno existente.

Para obtener más información, [consulte los WebHooks entrantes en la documentación de Slack](https://api.slack.com/incoming-webhooks).

Para crear notificaciones de Slack:

1. En el conducto, abra la configuración correspondiente a una etapa.
2. En el separador **PROPIEDADES DE ENTORNO**, pulse **AÑADIR PROPIEDAD**.
3. Seleccione **Propiedades de texto**.
4. Especifique el nombre y un valor para la propiedad de entorno. Repita este paso para crear varias propiedades de entorno.

  *Tabla 1. Propiedades de entorno para configurar notificaciones de Slack*

  <table>
  <tr>
  <th>Nombre</th>
  <th>Valor</th>
  <th>Descripción</th>
  <tr/>
  <tr>
    <td><code>SLACK_WEBHOOK_PATH</code></td>
    <td>Un URL</td>
    <td>Obligatorio. El URL de WebHook que se guarda en los valores para el Proyecto de Slack.</td>
  </tr>
  <tr>
    <td><code>SLACK_COLOR</code></td>
    <td>Puede introducir uno de los siguientes valores:
      <ul><li><code>good</code></li>
      <li><code>warning</code></li>
      <li><code>danger</code></li>
      <li>Cualquier color hexadecimal, como por ejemplo #439FEO</li></ul></td>
    <td>Opcional. El color del borde que se visualiza en un lado del mensaje en Slack. Los colores predeterminados son verde para los mensajes correctos, rojo para los mensajes incorrectos y gris para los mensajes informativos.</td>
  </tr>
  <tr>
    <td><code>NOTIFY_FILTER</code></td>
    <td>Para recibir sólo un subconjunto de los tipos de mensajes, especifique uno de los valores siguientes:
      <ul>
      <li><code>good</code>: recibir sólo mensajes desconocidos, correctos e informativos. Los mensajes incorrectos no se envían.</li>
      <li><code>bad</code>: recibir todos los mensajes.</li>
      <li><code>info</code>: recibir solo los mensajes informativos. Los mensajes correctos, incorrectos y desconocidos no se envían.</li>
      <li><code>unknown</code>: recibir todos los mensajes.</li></ul>
      Ejemplo: Si establece <code>NOTIFY_FILTER = bad</code>, las notificaciones de error sólo se visualizan en el Canal de Slack.</td>
    <td>Opcional. Decida el tipo de mensajes para los que se enviarán notificaciones. De forma predeterminada, se envían los mensajes correctos e incorrectos, pero no los mensajes informativos.
      <ul><li><code>good</code>: resultados de compilación correcta.</li>
      <li><code>bad</code>: resultados de compilación incorrecta.</li>
      <li><code>info</code>: mensajes informativos sobre el proceso de compilación.</li>
      <li><code>unknown</code>: a los mensajes desconocidos no se les asigna ningún tipo.</li></ul></td>
   </table>

5. Pulse **Guardar**.

6. Repita estos pasos para enviar notificaciones de Slack para otras etapas que incluyan trabajos de IBM Container Service, IBM Security Analyzer e IBM Globalization.

La notificación de compilación que se visualiza en Slack incluye un enlace al proyecto de DevOps Services y a veces al panel de instrumentos del proyecto. Para que un usuario de Slack abra estos enlaces, el usuario debe estar registrado con DevOps Services y ser miembro del proyecto en el que está configurado el conducto.

## Creación de notificaciones de HipChat para compilaciones en el conducto
{: #deliverypipeline_hipchat}

Puede enviar notificaciones sobre los resultados de compilación de IBM Container Service, IBM Security Static Analyzer e IBM Globalization desde las salas de Delivery Pipeline a HipChat.

Antes de empezar, cree o copie una señal existente de HipChat:

1. Vaya a su página de Cuenta de HipChat para el equipo: `https://_nombre_proyecto_.hipchat.com/account/api`
2. Cree un token nuevo, o bien utilice uno existente.

Para crear notificaciones de HipChat:

1. En el conducto, abra la configuración correspondiente a una etapa.
2. En el separador **PROPIEDADES DE ENTORNO**, pulse **AÑADIR PROPIEDAD**.
3. Seleccione **Propiedades de texto**.
4. Especifique el nombre y un valor para la propiedad de entorno. Repita este paso para crear varias propiedades de entorno.

  *Tabla 2. Propiedades de entorno para configurar notificaciones de HipChat*

  <table>
  <tr>
  <th>Nombre</th>
  <th>Valor</th>
  <th>Descripción</th>
  </tr>
  <tr>
    <td><code>HIP_CHAT_TOKEN</code></td>
    <td>Serie alfanumérica</td>
    <td>Obligatorio. Consulte "Antes de empezar" para obtener instrucciones sobre cómo crear o copiar una señal existente de HipChat.</td>
  </tr>
  <tr>
    <td><code>HIP_CHAT_ROOM_NAME</code></td>
    <td>Nombre de sala</td>
    <td>Obligatorio.</td>
  </tr>
  <tr>
    <td><code>HIP_CHAT_COLOR</code></td>
    <td>Escriba uno de los valores siguientes:
      <ul><li><code>amarillo</code></li>
      <li><code>rojo</code></li>
      <li><code>verde</code></li>
      <li><code>púrpura</code></li>
      <li><code>gris</code></li>
      <li><code>aleatorio</code></li></ul>
    </td>
    <td>Opcional: Especifique el color de fondo y el color del borde de las notificaciones de HipChat. Si establece <code>HIP_CHAT_COLOR</code>, no tiene que especificar el color al invocar el script.
     <p><code>-l notification_level</code></p> </td>
  </tr>
  <tr>
    <td><code>NOTIFICATION_COLOR</code></td>
    <td>Escriba uno de los valores siguientes:
      <ul><li><code>good</code></li>
      <li><code>danger</code></li>
      <li><code>info</code></li></ul>
    Esta variable se aplica tanto al color de notificación de HipChat como de Clack. Si especifica <code>NOTIFICATION_COLOR</code>, no es necesario especificar <code>HIP_CHAT_COLOR</code> o <code>SLACK_COLOR</code>.</td>
    <td>Opcional: Especifique el color de fondo y el color del borde de las notificaciones tanto HipChat como Slack. Si establece <code>NOTIFICATION_COLOR</code>, no tiene que especificar el color al invocar el script.
     <p><code>-l notification_level</code></p> </td>
  </tr>
  <tr>
    <td><code>NOTIFICATION_LEVEL</code></td>
    <td>Escriba uno de los valores siguientes:
      <ul><li><code>good</code></li>
      <li><code>info</code></li>
      <li><code>bad</code></li></ul></td>
    <td>Opcional: especifique el nivel de notificación. Consulte <code>NOTIFICATION_FILTER</code> para obtener información más detallada sobre qué desencadena la notificación.</td>
  </tr>
  <tr>
    <td><code>NOTIFICATION_FILTER</code></td>
    <td>Escriba uno de los valores siguientes:
      <ul><li><code>good</code></li>
      <li><code>info</code></li>
      <li><code>bad</code></li></ul>
    <td>Opcional: especifique el nivel de filtro de notificación. Las notificaciones se envían cuando se cumplen los parámetros siguientes:
      <ul><li><code>NOTIFICATION_FILTER = good</code> y <code>NOTIFICATION_LEVEL = bad</code>, <code>good</code>, o <code>unknown</code></li>
      <li><code>NOTIFICATION_FILTER = info</code> y <code>NOTIFICATION_LEVEL = bad</code>, <code>good</code>, <code>info</code>, o <code>unknown</code></li>
      <li><code>NOTIFICATION_FILTER = bad</code> y <code>NOTIFICATION_LEVEL = bad</code> o <code>unknown</code></li>
      <li><code>NOTIFICATION_FILTER = unknown</code> y <code>NOTIFICATION_LEVEL = bad</code>, <code>good</code>, o <code>unknown</code></li></ul></td>
    </tr>
  </table>

5. Pulse **Guardar**.

6. Repita estos pasos para enviar las notificaciones de HipChat para otras etapas que incluyan los trabajos de IBM Container Service, IBM Security Static Analyzer, e IBM Globalization.

## Uso de Active Deploy para el despliegue de tiempo de inactividad cero en el conducto
{: #deliverypipeline_activedeploy}

Puede automatizar el despliegue continuo de las apps o de los grupos de contenedores mediante el servicio de IBM® Active Deploy en el Bluemix® DevOps Services Delivery Pipeline. Para obtener más información sobre cómo iniciarse, [consulte la documentación de Active Deploy](https://new-console.ng.bluemix.net/docs/services/ActiveDeploy/updatingapps.html#adpipeline).

## Compilación y despliegue de imágenes del contenedor con el conducto
{: #deliverypipeline_containers}

Puede automatizar las compilaciones de la app y los despliegues del contenedor en Bluemix® mediante IBM® Continuous Delivery Pipeline for Bluemix. El servicio de Delivery Pipeline en los servicios de DevOps da soporte a:
  - Imágenes de creación de Docker
  - Imágenes de despliegue en contenedores a Bluemix

Para obtener más información sobre cómo iniciarse, consulte [la visión general de Delivery Pipeline y los contenedores](https://new-console.ng.bluemix.net/docs/containers/container_pipeline_ov.html#container_pipeline_ov).
