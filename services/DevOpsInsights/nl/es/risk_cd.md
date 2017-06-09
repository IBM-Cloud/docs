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

# Integración con un conducto Continuous Delivery

Después de añadir {{site.data.keyword.DRA_short}} a una cadena de herramientas y de definir las políticas que supervisa, intégrelo con {{site.data.keyword.deliverypipeline}}. Para obtener más información sobre los conductos, consulte la [documentación oficial](/docs/services/ContinuousDelivery/pipeline_working.html).

## Preparación de etapas de conducto
{: #integrate_pipeline}

Para que Deployment Risk analice su proyecto, debe definir etapas de transferencia y producción en su conducto. Las etapas se definen utilizando propiedades de entorno de texto, que puede encontrar en el menú de configuración de cada etapa ![Icono de configuración de etapa de conducto](images/pipeline-stage-configuration-icon.png) bajo **Propiedades de entorno**.

1. En la etapa de transferencia, establezca la propiedad `LOGICAL_ENV_NAME` en `STAGING`. 

2. En la etapa de producción, establezca la propiedad `LOGICAL_ENV_NAME` en `PRODUCTION`. 

También puede añadir las siguientes propiedades a etapas que compilan o despliegan su app:

* `LOGICAL_APP_NAME`, que define el nombre de la app en el panel de control.
* `BUILD_PREFIX`, que define el texto que se añade como prefijo a las compilaciones de etapa. Este texto solo se muestra en el panel de control. 

## Adición de trabajos de prueba
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

## Definición de puertas
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

Cuando haya terminado de configurar su conducto, empiece a utilizar use {{site.data.keyword.DRA_short}}. 
