---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-31"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Deployment Risk
{: #gettingstarted}

{{site.data.keyword.DRA_short}} proporciona información diversa sobre los despliegues, especialmente su riesgo. Puede utilizarlo para automatizar la protección de la calidad en su conducto de entrega mediante el uso de políticas y puertas. 
{:shortdesc}

Después de abrir {{site.data.keyword.DRA_short}} desde la cadena de herramientas, pulse **Deployment Risk**. Desde aquí, podrá obtener una visión general de las aplicaciones en los entornos de producción y transferencia y profundizar para comprender la cobertura de código, el rendimiento de las pruebas y los informes de seguridad. Los paneles de control se rellenan automáticamente con la información más reciente sobre las pruebas de {{site.data.keyword.DRA_short}} de sus conductos.

## Acerca de Deployment Risk
{: #about}

Utilice Deployment Risk para imponer estándares de calidad en su cadena de herramientas mediante políticas y puertas. Las políticas comprenden conjuntos de reglas y las puertas que las imponen. Por ejemplo, podría crear una política denominada "Unit Testing and Test Coverage" que precisa que las compilaciones satisfagan estándares de realización de pruebas de unidad y estándares de cobertura de código. A continuación añadiría una puerta que haría referencia a la política de su proceso de entrega continua. Las compilaciones que no satisfagan la política se detendrán en la puerta. 

Deployment Risk funciona con {{site.data.keyword.deliverypipeline}}, que es parte de {{site.data.keyword.contdelivery_full}}, y con proyectos de Jenkins. En un alto nivel, las instrucciones para utilizarlos son similares.  

Si está utilizando {{site.data.keyword.deliverypipeline}}, siga estos pasos:

1. [Cree políticas y reglas](#policies_and_rules) para que {{site.data.keyword.DRA_short}} las gestione.
2. [Prepare las etapas de su conducto](#integrate_pipeline) para la integración con {{site.data.keyword.DRA_short}}.

3. [Cree o edite trabajos de pruebas](#configure_pipeline_jobs) en el conducto para subir los resultados a {{site.data.keyword.DRA_short}}.
4. [Añada puertas](#configure_pipeline_gates) al conducto para que tomen decisiones de promoción en base a dichos resultados y a sus políticas.
5. Ejecute el conducto y [visualice los resultados](#view_results).

Si utiliza Jenkins, siga estos pasos:

1. [Cree políticas y reglas](#policies_and_rules) para que {{site.data.keyword.DRA_short}} las gestione.
2. [Instale y configure el plugin Jenkins](#integrate_jenkins).
3. [Cree trabajos de pruebas y puertas tal como se describe en las instrucciones del plugin](#integrate_jenkins). Las pruebas suben resultados para que {{site.data.keyword.DRA_short}} los analice y las puertas utilizan dichos resultados para tomar decisiones de promoción.
4. Ejecute el proyecto y [visualice los resultados](#view_results). 

Independientemente de cómo compila y despliega su código, los resultados serán los mismos: las compilaciones que satisfagan los estándares pasarán las puertas de Deployment Risk y las compilaciones que no lo hagan, serán detenidos. 

## Requisitos previos
{: #prerequisites}

Deployment Risk precisa una configuración adicional más allá de lo que se describe en [Iniciación con {{site.data.keyword.DRA_short}}](/docs/services/DevOpsInsights/index.html).

Para utilizar Deployment Risk, necesita dos cosas:

* Una instancia de {{site.data.keyword.deliverypipeline}} o un proyecto de Jenkins
* Pruebas que utilizará para evaluar su proyecto

## Creación de políticas y reglas
{: #policies_and_rules}

Las políticas son conjuntos de reglas que controlan las puertas en su conducto de entrega. Si su código no satisface o excede una política instaurada en una puerta concreta, se detiene el despliegue para evitar que se liberen cambios con un riesgo elevado.

Las políticas se definen en {{site.data.keyword.DRA_short}}. Las políticas se crean en la organización (org) de {{site.data.keyword.Bluemix_notm}} que contiene {{site.data.keyword.DRA_short}}. Todas las aplicaciones que se encuentran en la misma organización puede utilizar la política. 

### Creación de políticas
{: #create_policies}

Para crear una política:

1. En la navegación izquierda, pulse **Valores**.

2. Pulse **Políticas**.

3. Pulse **Crear política** y, a continuación, especifique un nombre y una descripción para la nueva política.

4. Pulse **Siguiente**.

4. Añada al menos una regla a la política:
  1. Pulse **Añadir regla a política**.
  2. Seleccione el tipo de regla.
  3. Especifique los detalles y las condiciones de la regla.
  4. Pulse **Guardar**.

5. Cuando haya acabado de añadir reglas a la política, pulse **Completado**.

### Creación de reglas
{: #creating_rules}

Las reglas definen los criterios que utilizarán las políticas para juzgar el cumplimiento o incumplimiento de la misma. Podría crear una política "Unit Testing and Test Coverage" que contenga una regla de prueba de unidad que requiera al menos un éxito del 80% de la misma y una regla de cobertura que precise el 100% de la cobertura de código. Si añade una puerta que haga referencia a esta regla en un conducto, la puerta impide que las compilaciones que no satisfacen ambas reglas continúen. 

Puede exigir una prueba satisfactoria sea como sea marcándola como crítica. Para crear una regla, seleccione una política y, a continuación, pulse **Añadir regla a política**. 

#### Creación de reglas de prueba de verificación funcional
{: #criteria_fvt}

1. Escriba una descripción y seleccione un formato.

2. Especifique el porcentaje de casos de prueba que deben pasar correctamente para considerarse satisfactorio.

3. Defina los casos de prueba que sean críticos.

4. Para supervisar las regresiones de casos de prueba, marque el recuadro de selección **Supervisar la regresión de casos de prueba**.

5. Pulse **Guardar**.


#### Creación de reglas de prueba de unidad
{: #criteria_ut}

1. Escriba una descripción y seleccione un formato.

2. Especifique el porcentaje de casos de prueba que deben pasar correctamente para considerarse satisfactorio.

3. Defina los casos de prueba que sean críticos.

4. Para supervisar las regresiones de casos de prueba, marque el recuadro de selección **Supervisar la regresión de casos de prueba**.

5. Pulse **Guardar**.


#### Creación de reglas de cobertura de código
{: #criteria_codecoverage}

1. Escriba una descripción y seleccione un formato.

2. Especifique el porcentaje de cobertura de código que es necesario para considerarse satisfactorio.

3. Para supervisar las regresiones de cobertura de código, marque el recuadro de selección **Supervisar la regresión de casos de prueba**.

4. Pulse **Guardar**.

#### Creación de reglas de exploración de seguridad estática
{: #criteria_static}

Puede integrar {{site.data.keyword.DRA_short}} con IBM Application Security on Cloud para ejecutar exploraciones de app dinámicas y de código estático. Para obtener más información sobre Application Security on Cloud, consulte [la documentación oficial](/docs/services/ApplicationSecurityonCloud/index.html).

1. Especifique una descripción.

2. Especifique el número máximo de problemas de seguridad baja, media o elevada que esta regla permite. 

3. Pulse **Guardar**.

#### Creación de reglas de exploración de seguridad dinámica
{: #criteria_dynamic}

Puede integrar {{site.data.keyword.DRA_short}} con {{site.data.keyword.appseccloudfull}} para ejecutar exploraciones de app dinámicas. Para obtener más información sobre Application Security on Cloud, consulte [la documentación oficial](/docs/services/ApplicationSecurityonCloud/index.html).

1. Especifique una descripción.

2. Especifique el número máximo de problemas de seguridad baja, media o elevada que esta regla permite. 

3. Pulse **Guardar**.

## Configuración de {{site.data.keyword.deliverypipeline}} 
{: #configuration}

Después de añadir {{site.data.keyword.DRA_short}} a una cadena de herramientas y de definir las políticas que supervisa, intégrelo con {{site.data.keyword.deliverypipeline}}. Para obtener más información sobre los conductos, consulte la [documentación oficial](/docs/services/ContinuousDelivery/pipeline_working.html).

### Preparación de etapas de conducto
{: #integrate_pipeline}

Para que Deployment Risk analice su proyecto, debe definir etapas de transferencia y producción en su conducto. Las etapas se definen utilizando propiedades de entorno de texto, que puede encontrar en el menú de configuración de cada etapa ![Icono de configuración de etapa de conducto](images/pipeline-stage-configuration-icon.png) bajo **Propiedades de entorno**.

1. En la etapa de transferencia, establezca la propiedad `LOGICAL_ENV_NAME` en `STAGING`. 

2. En la etapa de producción, establezca la propiedad `LOGICAL_ENV_NAME` en `PRODUCTION`. 

También puede añadir las siguientes propiedades a etapas que compilan o despliegan su app:

* `LOGICAL_APP_NAME`, que define el nombre de la app en el panel de control.
* `BUILD_PREFIX`, que define el texto que se añade como prefijo a las compilaciones de etapa. Este texto solo se muestra en el panel de control. 

### Adición de trabajos de prueba
{: #configure_pipeline_jobs}

{{site.data.keyword.DRA_short}} se integra en su conducto utilizando dos tipos de trabajos de prueba: unos que suben resultados a {{site.data.keyword.DRA_short}} para su análisis, y puertas que actúan en dicho análisis. 

En primer lugar, añade trabajos de Advanced Tester a su conducto para ejecutar pruebas y subir resultados. 

**Nota:** Si desea actualizar un trabajo de prueba para subir los resultados en {{site.data.keyword.DRA_short}}, guarde sus configuraciones en un lugar adecuado antes de continuar. A continuación, abra su menú de configuración del trabajo y vaya al paso 3. 

1. En la etapa en la que desea añadir el trabajo que sube los resultados, pulse el icono **Configuración de etapa** ![Icono de configuración de etapa de conducto](images/pipeline-stage-configuration-icon.png). Pulse **Configurar etapa**.
2. Cree un trabajo de prueba y escriba un nombre para el mismo. 
3. Seleccione **Advanced Tester** como tipo de trabajo.
4. Complete los campos **Mandato de prueba** y **Directorio de trabajo** tal como lo haría con un trabajo de prueba de conducto normal. 
5. Complete los campos restantes para subir los resultados de la prueba para un tipo de prueba concreto. 

 1. Elija el tipo de métrica que coincida con lo que definió en la política de {{site.data.keyword.DRA_short}} que desea utilizar.
 2. Escriba una ubicación para el archivo de resultados. Esta ubicación es relativa al directorio de trabajo. 

6. Si desea cargar resultados de un segundo tipo de prueba en el mismo trabajo, complete los campos que tienen el prefijo *Adicional*.
7. Pulse **Guardar** para volver al conducto.

Los valores de los campos **Tipo de métrica** y **Ubicación del archivo de resultados** deben coincidir con el formato correcto:

<table><thead>
<tr>
<th>Tipo de métrica</th>
<th>Formatos soportados</th>
</tr>
</thead><tbody>
<tr>
<td>Prueba de verificación funcional</td>
<td>Mocha, xUnit</td>
</tr>
<tr>
<td>Prueba de unidad</td>
<td>Mocha, xUnit, Karma/Mocha</td>
</tr>
<tr>
<td>Cobertura de código</td>
<td>Istanbul, Blanket.js</td>
</tr>
</tbody></table>

La Figura 1 muestra un trabajo de prueba que está configurado para ejecutar pruebas de unidad, cargar los resultados en formato de Mocha y cargar los resultados de la cobertura de código en formato de Istanbul.

![Trabajo subido de DevOps Insights](images/insights_upload_job.png)
*Figura 1. Subir resultados para DevOps Insights*

### Definición de puertas
{: #configure_pipeline_gates}

Las puertas de {{site.data.keyword.DRA_short}} comprueban si los resultados de las pruebas cumplen con una política definida. Si no se cumple la política, de forma predeterminada la puerta de {{site.data.keyword.DRA_short}} falla. También puede configurar las puertas para que actúen en un rol de advertencia que permite el progreso en el conducto, incluso después de una anomalía.

El panel de control de Deployment Risk se basa en la presencia de una puerta después un trabajo de despliegue en el entorno de transferencia. Si desea utilizar el panel de control, asegúrese de que tiene una puerta después de realizar el despliegue en el entorno de transferencia y antes de realizar el despliegue en un entorno de producción.

Normalmente, las puertas se colocan en el conducto antes de la promoción de la compilación. Estas ubicaciones son ideales para comprobar la calidad de la compilación con las políticas para asegurarse de que es seguro promocionarla de un entorno a otro. Sin embargo, puede colocar puertas en cualquier sitio del conducto donde desee comprobar un criterio específico. Las puertas que se colocan antes del despliegue en un entorno de transferencia todavía impondrán las políticas, pero no aparecerán en el panel de control de Deployment Risk.

1. En una etapa, pulse el icono **Configuración de etapa** ![Icono de configuración de etapa de conducto](images/pipeline-stage-configuration-icon.png) y pulse **Configurar etapa**.
2. Pulse **Añadir trabajo**. Para el tipo de trabajo, seleccione **Prueba**.
3. Para el tipo de probador, **Puerta de {{site.data.keyword.DRA_short}}**.
4. Especifique el nombre del entorno. Asegúrese de que este valor coincida con el que ha definido en sus [propiedades de entorno](#toolchain_pipeline_props).
5. Especifique el nombre de la política a comprobar en esta puerta.

 Este nombre debe coincidir exactamente con uno de los nombres de política que ha definido. Puede especificar sólo políticas que están definidas en la misma organización de {{site.data.keyword.Bluemix_notm}} como su cadena de herramientas.

6. Opcional: Para hacer que una puerta funcione en modalidad de advertencia, desmarque el recuadro de selección **Dejar de ejecutar esta etapa si el trabajo falla**. En modalidad de advertencia, {{site.data.keyword.DRA_short}} completa el mismo análisis de política en la puerta y genera informes, pero si se produce un error, el conducto no se detiene.
7. Pulse **Guardar** para volver al conducto.
8. Configure puertas para todas sus políticas de {{site.data.keyword.DRA_short}} repitiendo estos pasos.

![Trabajo Mocha de Deployment Risk](images/insights_gate_job.png)
*Figura 2. Puerta de DevOps Insights*

Cuando haya terminado de configurar su conducto, empiece a utilizar use {{site.data.keyword.DRA_short}}. Para obtener instrucciones, consulte [Ejecución de Delivery Pipeline](/docs/services/DevOpsInsights/pipeline_decision_reports.html#toolchain_reports).

## Configuración de un proyecto Jenkins
{: #integrate_jenkins}

Después de añadir {{site.data.keyword.DRA_full}} a una cadena de herramientas abierta y de definir las políticas que supervisa, puede integrarla con un proyecto Jenkins. 

El plugin IBM Cloud DevOps para Jenkins integra proyectos Jenkins con cadenas de herramientas. Una *cadena de herramientas* es un conjunto de integraciones de herramientas que dan soporte a tareas de desarrollo, despliegue, y operaciones. El poder colectivo de una cadena de herramientas es mayor que la suma de sus integraciones de herramientas individuales. Las cadenas de herramientas abiertas son parte del servicio {{site.data.keyword.contdelivery_full}}. Para obtener más información sobre el servicio {{site.data.keyword.contdelivery_short}}, consulte [su documentación](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/cd_about.html).

Después de instalar el plugin IBM Cloud DevOps, puede publicar los resultados de las pruebas en {{site.data.keyword.DRA_short}}, añadir puertas de calidad automatizadas y realizar un seguimiento del riesgo del despliegue. También puede enviar notificaciones de trabajos a otras herramientas en su cadena de herramientas como, por ejemplo, Slack y PagerDuty. Para ayudarle en el seguimiento de despliegues, la cadena de herramientas puede añadir mensajes de despliegue a confirmaciones Git y los correspondientes problemas Git o JIRA relacionados. También puede ver los despliegues en la página Conexiones de la cadena de herramientas. 

El plugin proporciona una interfaz de línea de mandatos y las acciones posteriores a la compilación para dar soporte a la integración. {{site.data.keyword.DRA_short}} agrega y analiza los resultados de pruebas de unidad, pruebas funcionales, herramientas de cobertura de código, exploraciones de código de seguridad estático y exploraciones de código de seguridad dinámico para determinar si el código cumple las políticas predefinidas en las puertas especificadas del proceso de despliegue. Si el código no cumple o supera una política, el despliegue se detiene para impedir que se liberen cambios arriesgados. Puede utilizar {{site.data.keyword.DRA_short}} como red de seguridad para su entorno de entrega continua, como método para implementar y mejorar con el tiempo los estándares de calidad y como una herramienta de visualización de datos para ayudarle a comprender el estado de salud de su proyecto.

### Requisitos previos
{: #jenkins_prerequisites}

Debe tener acceso a un servidor que ejecute un proyecto Jenkins.

### Creación de una cadena de herramientas
{: #jenkins_create}

Antes de poder integrar {{site.data.keyword.DRA_short}} con un proyecto Jenkins, debe crear una cadena de herramientas. 

1. Para crear una cadena de herramientas, vaya a la página [Crear una cadena de herramientas](https://console.ng.bluemix.net/devops/create) y siga las instrucciones en dicha página. 

2. Después de crear la cadena de herramientas, añada {{site.data.keyword.DRA_short}} a la misma. Consulte la [documentación de {{site.data.keyword.DRA_short}}](https://console.ng.bluemix.net/docs/services/DevOpsInsights/index.html) para obtener más información. 

### Instalación del plugin
{: #jenkins_install}

Primero, descargue el plugin desde {{site.data.keyword.DRA_short}}.  

1. En la página de Visión general de la cadena de herramientas, pulse **DevOps Insights**.
2. Pulse **Valores** y, a continuación, **Instalación del plugin Jenkins**.
3. Siga las instrucciones de la página para descargar el plugin.

A continuación, instale el plugin en el servidor Jenkins.

1. Pulse **Gestionar Jenkins &gt; Gestionar plugins** y pulse el separador **Avanzado**.
2. Pulse **Elegir archivo** y seleccione el archivo de instalación del plugin IBM Cloud DevOps. 
3. Pulse **Cargar**.
4. Reinicie Jenkins y verifique se ha instalado el plugin.

### Configuración de trabajos de Jenkins para el panel de control de Deployment Risk
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
    
### Configuración de notificaciones
{: #jenkins_notifications}

Tiene la posibilidad de configurar los trabajos de Jenkins para que envíen notificaciones a herramientas como, por ejemplo, Slack o PagerDuty siguiendo las instrucciones en la [documentación de Bluemix](https://console.ng.bluemix.net/docs/services/ContinuousDelivery/toolchains_integrations.html#jenkins).

Este ejemplo muestra cómo configurar `ICD_WEBHOOK_URL` para configuraciones de trabajos: ![Establecer el parámetro ICD_WEBHOOK_URL](images/Set-Parameterized-Webhook.png "Establecer un webhook parametrizado")

Este ejemplo muestra cómo configurar acciones posteriores a la compilación para notificaciones de trabajo: ![Acciones posteriores a la compilación para notificaciones webhook](images/PostBuild-WebHookNotification.png "Configurar notificaciones webhook en acciones posteriores a la compilación")

## Visualización de resultados
{: #view_results}

Tras ejecutarse un conducto, {{site.data.keyword.DRA_short}} empieza a recopilar y analizar los resultados de las pruebas para establecer una línea base. Los datos de cada ejecución posterior se recopila y se compara con los resultados anteriores. Las puertas de decisión utilizan estos datos para determinar cuándo se debe detener un despliegue. 

Puede ver los datos de evaluación de despliegue y de puertas desde el panel de control de Deployment Risk. Para abrir el panel de control, abra {{site.data.keyword.DRA_short}} y en el menú lateral, pulse **Deployment Risk**.

Si está utilizando un conducto de {{site.data.keyword.contdelivery_short}}, puede ver informes individuales de ejecución de las puertas desde el propio conducto. Para ver el informe de decisión de una puerta del conducto, siga estos pasos:

1. En la etapa que contiene la puerta que se debe comprobar, pulse **Ver registros e historial**.

2. Desde el trabajo que contiene la puerta, pulse el nombre de la puerta.

3. En la ventana de registros, busque el mensaje `Comprobar aquí informe de {{site.data.keyword.DRA_short}}` y pulse el enlace para abrir el informe.






