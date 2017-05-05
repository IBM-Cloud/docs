---

copyright:
  years: 2017
lastupdated: "2017-3-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Personalización de planes de despliegue para conductos compuestos
{: #tasks_overview}

En un plan de despliegue para un conducto compuesto, una tarea representa una actividad significativa para el negocio que está asociada al despliegue de software. Las tareas se definen en planes de despliegue.

{:shortdesc}

La mayoría de las tareas tienen un punto de partida, un punto final y una duración que se puede medir. Una tarea puede ser de uno de los siguientes tipos:

<ul>
<li>Las tareas manuales pueden representar cualquier actividad que está asociada con un despliegue de software, como por ejemplo colocar un servidor fuera de línea o actualizar una base de datos.</li>
<li>Las tareas UrbanCode Deploy representan apps de IBM&reg; UrbanCode&reg; Deploy. Puede ejecutar apps de IBM UrbanCode Deploy con tareas de tipo IBM UrbanCode Deploy. </li>
<li>Las tareas de Continuous Delivery Pipeline representan instancias de {{site.data.keyword.deliverypipeline}}, que forma parte de {{site.data.keyword.contdelivery_full}}. Puede gestionar las instancias de {{site.data.keyword.deliverypipeline}} con este tipo de tarea.</li>
<li>Las tareas retrasadas representan sucesos críticos que se producen en un determinado momento. </li>
<li>Las tareas de cabecera son elementos organizativos. Por ejemplo, puede utilizar una tarea de cabecera para identificar un grupo de tareas.</li>
</ul>

<!-- You can add tasks to deployment plans by creating tasks or you can import tasks from CSV files that are created by IBM UrbanCode Release or another application. You can also copy tasks from other deployment plans. See [Importing tasks](/docs/services/UCCR/UCCR_deployPlan.html#plan_importTasks) for information about the format of the CSV file. -->

## Creación de tareas
{: #tasks_create}

Al crear una tarea, seleccione el plan de despliegue en el que desea añadir la tarea. De forma predeterminada, las tareas nuevas se insertan al final del plan de despliegue. Después de crear una tarea, puede moverla o copiarla y pegarla en otra plan de despliegue. También puede crear dependencias con otras [tareas](/docs/services/ContinuousDelivery/pipeline_deployment_plan.html#tasks_dependencies).

Después de guardar una tarea, se muestran iconos de acción para la tarea. Puede utilizar los iconos de acción para cambiar el estado de la tarea durante un despliegue. Todas las tareas tienen el icono de acción **Omitir**. Se muestran otros iconos, como por ejemplo **Iniciar**, cuando el contexto resulta adecuado. 

![](../UCCR/images/deploy-plan-intro.png "Plan de despliegue típico")

*Figura 1. Un plan de despliegue sencillo con tareas e iconos de acción*

Cada tarea de un plan de despliegue está contenida en una fila distinta. La información que se muestra para cada tarea se describe en la tabla siguiente.

### Tabla 1. Propiedades de tareas

| Propiedad  | Descripción  |
| ------------------ | ------------------ |
| Nombre               |Nombre de tarea                                          |
| Tipo               |Tipo de tarea: Manual, Continuous Delivery Pipeline, Retrasada, Correo electrónico, Cabecera/Nota, UrbanCode Deploy|             
| Estado             |Estado de la tarea: No iniciada, completa, error, omitida, no aplicable |
| Propietario              |Persona a la que se asigna la tarea                                                        |
| Hora de inicio  |Hora de inicio y hora de inicio prevista en función del inicio planificado, o duración estimada de otras tareas        |
| Hora final               |Hora a la que la se ha resuelto la tarea        |
| Duración               |Periodo de tiempo transcurrido entre el inicio de la tarea y la resolución de la tarea (en minutos)        |
| Dependencias               |Número de tareas que constituyen requisitos previos para la tarea y que dependen de la tarea        |

---
Después de añadir tareas a planes de despliegue, puede gestionarlas de varias formas:
   * Para mover una tarea, arrástrela a una nueva ubicación.

   * Para copiar una tarea o un grupo, pulse la tarea, pulse el icono **Copiar** <img class="inline" src="../UCCR/images/copy-group.png" alt="icono copiar">, coloque el cursor donde desea insertar la tarea copiada y pulse el icono **Pegar** <img class="inline" src="../UCCR/images/paste-group.png" alt="icono pegar">.

   * Para cortar una tarea o un grupo de un plan de despliegue, pulse la tarea y pulse **Cortar** <img class="inline" src="../UCCR/images/cut-group.png" alt="icono cortar">.

   * Para suprimir una tarea, pulse sobre la misma y pulse **Suprimir** <img class="inline" src="../UCCR/images/trash-group.png" alt="icono suprimir">. La tarea se elimina del plan de despliegue.

<!-- ## Creating UrbanCode Deploy tasks
{: #tasks_UDTasks}

UrbanCode Deploy tasks manage UrbanCode Deploy applications. When you run an UrbanCode Deploy task, the associated UrbanCode Deploy application runs by using the process, version, and environment specified by the task. You can set the version and environment at design time or wait and select them at run time.

During deployments, UrbanCode Deploy tasks start automatically when they become eligible to run.   

**Important** Applications become available after {{site.data.keyword.uccr_short}} is integrated with UrbanCode Deploy. The applications that are available to a deployment plan depend on the team that is assigned to the plan. The applications that are managed by the team in UrbanCode Deploy are also available in {{site.data.keyword.uccr_short}}.

Complete the following tasks to create an UrbanCode Deploy task.

1. On the Deployment Plan Details page, click **Create Task**. If you want to insert a task at a specific position in the plan, select a task before using the **Create Task**. The new task is inserted above the selected task.

1. On the Create Task dialog box, in the **Type** list, select **UrbanCode Deploy**.

1. In the **Name** field, enter a name for the task.

3. In the **Duration (minutes)** field, enter the number of minutes that you expect the task to run until it is completed. The estimated duration is used to calculate expected deployment times.

3. In the **Tags** list, attach a tag to the task. You can select multiple tags. To create a tag, type the tag name in list's text field.

3. In the **Application Name** list, select an application.

3. In the **Process** list, select an application process. Processes that belong to the selected UrbanCode Deploy application are available.

3. In the **Environment** list, select an application environment. Environments that belong to the selected UrbanCode Deploy application are available.  To postpone selecting an environment until you are ready to run the deployment, select **Use Version Tab**.

3. In the **Version** list, select an application version. Versions refer to IBM UrbanCode Deploy application snapshots. Versions that belong to the selected application are available.  To postpone selecting a version, select **Use Version Tab**. If the application process does not require a version, select **No Version**. You might select this last option if you are running a configuration-type process that does not require components.

3. In the **Assigned groups and users** list, assign the task to a user or group. The assigned user runs the task during deployment.

3. In the **Owner** list, select the task owner. The default owner is the user who created the task. The **Owner** list is displayed after the task is assigned to a user or group.    

5. Click **Save**. The task is inserted into the deployment plan.

After the task is created, the plan's **Version** tab is updated with information about the application assigned to the task. If you selected **Use Version Tab** for the application environment and version, use the Version tab to set those options before running the deployment. -->

## Creación de tareas manuales
{: #tasks_manual}

Normalmente, las tareas manuales representan una actividad asociada con un release de software que tiene un punto de partida, un punto final y una duración que se puede medir. 

Para crear una tarea manual, siga estos pasos:

1. En la página Detalles del plan de despliegue, pulse **Crear tarea**. Para insertar una tarea en una posición específica en el plan, antes de pulsar **Crear tarea**, seleccione una tarea. La nueva tarea se inserta sobre la tarea seleccionada.

1. En la ventana Crear tarea, en la lista **Tipo**, seleccione **Manual**.

1. En el campo **Nombre**, escriba un nombre para la tarea. 

3. En el campo **Duración (minutos)**, escriba el número de minutos que cree que durará la ejecución de la tarea hasta que se complete. La duración estimada se utiliza para calcular los tiempos de despliegue previstos. 

3. En la lista **Etiquetas**, adjunte una etiqueta a la tarea. Puede seleccionar varias etiquetas. Para crear una etiqueta, escriba el nombre de la etiqueta en campo de texto de la lista. 

3. En la lista **Grupos y usuarios asignados**, asignar la tarea a un usuario o grupo. El usuario asignado ejecuta la tarea durante el despliegue.

3. En la lista **Propietario**, seleccione el propietario de la tarea. El propietario predeterminado es el usuario que ha creado la tarea. La lista **Propietario** se muestra después de que la tarea se asigne a un usuario o grupo.    

5. Pulse **Guardar**. La tarea se inserta en el plan de despliegue.

## Creación de tareas retrasadas
{: #tasks_delayed}

Las tareas retrasadas representan hitos o sucesos críticos durante un despliegue. Con tareas retrasadas, puede asegurarse de que las tareas importantes se inician a la hora prevista. Normalmente, las tareas retrasadas constituyen requisitos previos para otras tareas importantes. 

Una tarea retrasada se inicia cuando resulta adecuada su ejecución y finaliza a una hora especificada por el usuario. Una tarea retrasada iniciada tiene el estado "En curso" hasta que alcanza su hora planificada, cuando su estado cambia a "Completado". Cuando se completa una tarea retrasada, las tareas que dependen de ella empiezan a ejecutarse.

Para crear una tarea retrasada, siga estos pasos:

1. En la página Detalles del plan de despliegue, pulse **Crear tarea**. Si desea insertar una tarea en una posición específica en el plan, antes de pulsar **Crear tarea**, seleccione una tarea. La nueva tarea se inserta sobre la tarea seleccionada.

1. En la ventana Crear tarea, en la lista **Tipo**, seleccione **Retrasada**.

1. En el campo **Nombre**, escriba un nombre para la tarea. 

3. En el campo **Hora**, escriba o seleccione la hora a la que se completará la tarea. 

3. En el campo **Huso horario**, seleccione el huso horario para el valor que se especifica en el campo **Hora**.     

5. Pulse **Guardar**. La tarea se inserta en el plan de despliegue.

## Creación de tareas de cabecera
{: #tasks_header}

Las tareas de cabecera representan elementos de la organización que puede añadir a planes de despliegue. Si crea un grupo de tareas, puede identificar el grupo con una tarea de cabecera. Las tareas de cabecera pueden tener dependencias, como cualquier otra tarea.

<!-- When you import a deployment plan from IBM UrbanCode Release, segment tasks are bracketed by note-type Start Segment and End Segment tasks. Segment dependencies are represented by dependencies to End Segment tasks. -->

Para crear una tarea de cabecera, siga estos pasos:

1. En la página Detalles del plan de despliegue, pulse **Crear tarea**. Si desea insertar una tarea en una posición específica en el plan, antes de pulsar **Crear tarea**, seleccione una tarea. La nueva tarea se inserta sobre la tarea seleccionada.

1. En la ventana Crear tarea, en la lista **Tipo**, seleccione **Cabecera**.

1. En el campo **Nombre**, escriba un nombre para la tarea. El nombre puede representar un nombre de grupo de tareas. 

3. En el campo **Descripción**, escriba o pegue una descripción. Puede escribir una nota, un recordatorio y otra instrucción. 

5. Pulse **Guardar**. La tarea se inserta en el plan de despliegue.

## Creación de tareas de Delivery Pipeline
{: #tasks_pipelineCD}

En el servicio {{site.data.keyword.contdelivery_short}}, {{site.data.keyword.deliverypipeline}} automatiza los flujos de trabajo de DevOps. Puede gestionar sus instancias de {{site.data.keyword.deliverypipeline}} con tareas de conducto.

Para crear una tarea de Delivery Pipeline, siga estos pasos:

1. En la página Detalles del plan de despliegue, pulse **Crear tarea**. Si desea insertar una tarea en una posición específica en el plan, antes de pulsar **Crear tarea**, seleccione una tarea. La nueva tarea se inserta sobre la tarea seleccionada.

1. En la ventana Crear tarea, en la lista **Tipo**, seleccione **Continuos Delivery Pipeline**.

1. En el campo **Nombre**, escriba un nombre para la tarea. El nombre puede representar un nombre de grupo de tareas. 

3. En el campo **Descripción**, escriba o pegue una descripción. Puede escribir una nota, un recordatorio y otra instrucción. 

3. En el campo **ID de conducto**, escriba o pegue el ID de conducto. 

3. En el campo **Nombre de etapa**, escriba o pegue el nombre de la etapa. 

5. Pulse **Guardar**. La tarea se inserta en el plan de despliegue.

## Gestión de grupos de tareas
{: #tasks_groups}

Puede combinar dos o más tareas en un grupo de tareas. Cuando cree un grupo, defina el patrón de ejecución del grupo, que puede ser secuencial o paralelo. Puede ejecutar las tareas de un grupo de patrón en paralelo en cualquier orden y puede ejecutar las tareas simultáneamente, a menos que existen dependencias. Las tareas de grupos secuenciales se ejecutan en orden de lista, empezando por la primera tarea o situada al principio. 

Puede insertar grupos dentro de otros grupos. Puede insertar un grupo de patrón secuencial dentro de un grupo de patrón en paralelo y viceversa. Sin embargo, no puede insertar un grupo de patrón secuencial dentro de otro grupo de patrón secuencial ni insertar un grupo de patrón en paralelo dentro de otro grupo en paralelo.   

Para crear un grupo de tareas, siga estos pasos:

1. En la página Detalle del plan de despliegue, seleccione dos o más tareas.

1. Dependiendo del tipo de grupo que desee crear, siga uno de estos pasos:

  <ul>
  <li>Para crear grupo en paralelo, pulse el icono **Paralelo** <img class="inline" src="../UCCR/images/para-icon.png" alt="icono de grupo paralelo">. Si no puede crear un grupo paralelo con las tareas seleccionadas, el icono está inhabilitado. Por ejemplo, es posible que no pueda crear un grupo paralelo si todas las tareas seleccionadas ya están en un grupo paralelo. </li>
  <li>Para crear un grupo secuencial, pulse **Secuencial** icono <img class="inline" src="../UCCR/images/seq-icon.png" alt="icono de grupo secuencial">. </li>
  </ul>

El grupo se forma y se añade una barra de selección de grupo al plan de despliegue. Si ha seleccionado tareas no contiguas, las tareas forman una lista contigua que empieza con la tarea seleccionada que está más arriba. 

En la figura siguiente se muestra un grupo paralelo. La barra de selección de grupo identifica el tipo de grupo: paralelo <img class="inline" src="../UCCR/images/para-select.png" alt="selección de grupo paralelo"> o secuencial <img class="inline" src="../UCCR/images/seq-select.png" alt="selección de grupo secuencial">.

(![](../UCCR/images/group-select.png "Plan de despliegue típico"))

*Figura 2. Un grupo paralelo*

Para mover un grupo, pulse en la **barra de selección de grupo** o pulse en cualquier lugar del grupo y arrástrelo a una nueva ubicación.

Para copiar un grupo, seleccione el grupo, pulse el icono **Copiar** <img class="inline" src="../UCCR/images/copy-group.png" alt="icono copiar">, coloque el cursor donde desee insertar el grupo de copiado y pulse **Pegar** <img class="inline" src="../UCCR/images/paste-group.png" alt="icono pegar">.

Para cortar un grupo, seleccione el grupo y pulse el icono **Cortar** <img class="inline" src="../UCCR/images/cut-group.png" alt="icono cortar">.

Para desagrupar un grupo, seleccione el grupo y pulse el icono **Desagrupar** <img class="inline" src="../UCCR/images/ungroup-icon.png" alt="icono desagrupar"> en la barra de selección del grupo. 

Para suprimir las tareas que se encuentran en un grupo, seleccione el grupo y pulse el icono **Suprimir** <img class="inline" src="../UCCR/images/trash-group.png" alt="icono suprimir">. Las tareas se eliminan del plan de despliegue.

## Gestión de etiquetas de tareas
{: #tasks_tags}

Las etiquetas son elementos organizativos que puede añadir a tareas. Puede filtrar planes de despliegue por etiqueta. Por ejemplo, durante un despliegue en un entorno de producción, puede inhabilitar las tareas que incluyan la etiqueta `DEV_only`, que indica que las tareas son solo para entornos de desarrollo. 

Para añadir una etiqueta a una tarea, siga estos pasos:

1. En la página Detalles del plan de despliegue, seleccione una tarea o un grupo de tareas y pulse **Gestionar etiquetas** <img class="inline" src="../UCCR/images/task-tag.png" alt="gestionar etiquetas">. Puede seleccionar varias tareas y grupos. 

1. En la ventana "Gestionar etiquetas para tareas seleccionadas", en la lista **Etiquetas comunes** seleccione etiquetas. Para crear una etiqueta, escriba un nombre en el recuadro de texto de la lista. 

1. Pulse **Guardar**.

Las etiquetas se muestran en las filas de las tareas en la página Detalles del plan de despliegue. En la siguiente figura, la tarea Desplegar WAR tiene dos etiquetas: `Despliegue (Deployment)` y `Crítico (Critical)`.

El plan de despliegue utiliza las etiquetas y se muestran en el separador **Versiones** de la página Detalles del plan de despliegue. Para representar una tarea que no se debe aplicar a un despliegue, quite las etiquetas de la tarea. Las tareas con el estado "No aplicable" no se pueden iniciar.  

![](../UCCR/images/task-tag-labels.png "Plan de despliegue típico")

*Figura 3. Etiquetas de tareas*

## Creación de dependencias de tareas
{: #tasks_dependencies}

Puede hacer que una tarea sea un requisito previo para otras tareas. Si una tarea es un requisito previo, las tareas dependientes no se pueden iniciar, aunque sean aptas de no ser por las dependencias, hasta que se resuelva el requisito previo. 

Una tarea puede tener varias tareas dependientes y varias
tareas de requisito previo. Puede definir dependencias para una tarea con cualquier
otra tarea del plan de despliegue. Si embargo, no se pueden crear dependencias circulares. Por ejemplo, no puede hacer que una tarea dependa de una tarea que a su vez depende de la primera tarea. 

Mediante el control de dependencias de tareas puede asegurarse de que los sucesos se producen en el orden previsto. 

Para hacer que una tarea sea un requisito previo para otras tareas, siga estos pasos: 

1. En la página Detalles del plan de despliegue, seleccione una tarea o un grupo de tareas y pulse **Gestionar requisitos previos** <img class="inline" src="../UCCR/images/task-depend.png" alt="requisito previo de tarea">. Puede seleccionar varias tareas y grupos. 

1. En la ventana "Gestionar requisitos previos para tareas seleccionadas", en la lista **Tareas de requisito previo para tareas seleccionadas**, seleccione la tarea de requisito previo. 

1. Pulse **Guardar**.

Las dependencias de tareas se muestran en la columna Dependencias de la página Detalle del plan de despliegue. Las flechas hacia arriba indican requisitos previos; las flechas hacia abajo indican dependencias de tareas.

En la siguiente figura, la primera tarea no tiene ningún requisito previo y dos tareas dependen de ella. La segunda tarea tiene una tarea de requisito previo y ninguna tarea depende de ella.

(![](../UCCR/images/plan-w-depend.png "Plan de despliegue típico"))

*Figura 4. Dependencias de tareas*

Para revisar o modificar dependencias, seleccione la tarea y pulse **Gestionar requisitos previos** <img class="inline" src="../UCCR/images/task-depend.png" alt="requisito previo de tarea">.
