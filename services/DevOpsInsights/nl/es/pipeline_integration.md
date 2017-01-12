---

copyright:
  years: 2016
lastupdated: "2016-11-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Integración de {{site.data.keyword.DRA_short}} con {{site.data.keyword.deliverypipeline}}
{: #toolchain_configure_pipeline}

Tras añadir {{site.data.keyword.DRA_full}} a una cadena de herramientas y definir las políticas que supervisa, debe integrar {{site.data.keyword.DRA_short}} con su conducto.
{:shortdesc}

<!--##Configuring the {{site.data.keyword.deliverypipeline}}

{: #toolchain_integration}
To use {{site.data.keyword.DRA_short}}, add it to any toolchain that uses the {{site.data.keyword.deliverypipeline}}.

1. In {{site.data.keyword.Bluemix_notm}}, on the **Toolchains** tab, open a toolchain.

2. On the toolchain's Overview page, click the add (+) button.

3. In the Tool Integrations section, select **{{site.data.keyword.DRA_short}}**.

4. Click **Create Integration**.

5. In your toolchain, click the {{site.data.keyword.deliverypipeline}} tile. You can configure {{site.data.keyword.DRA_short}} in any number of pipelines.-->

## Preparación de etapas de conducto para {{site.data.keyword.DRA_short}}
{: #toolchain_pipeline_props}

Debe crear varias propiedades de entorno en cada etapa de conducto que contenga trabajos de compilación o despliegue:

1. Pulse **Configuración de etapa** y, a continuación, **Configurar etapa**.

2. Pulse **PROPIEDADES DE ENTORNO**.

3. Añada las siguientes tres propiedades de texto y guarde los cambios de la etapa:

<table><thead>
<tr>
<th>Propiedad de entorno</th>
<th>Descripción</th>
</tr>
</thead><tbody>
<tr>
<td><code>LOGICAL_APP_NAME</code></td>
<td>Nombre de la app tal como aparece en los paneles de control de {{site.data.keyword.DRA_short}}. </td>
</tr>
<tr>
<td><code>LOGICAL_ENV_NAME</code></td>
<td>Nombre del entorno en que se ejecuta la app. Esta propiedad se utiliza para categorizar la app en los paneles de control de {{site.data.keyword.DRA_short}}.</td>
</tr>
<tr>
<td><code>BUILD_PREFIX</code></td>
<td>Prefijo que se añade a las compilaciones tal como se muestra en los paneles de control de {{site.data.keyword.DRA_short}}.</td>
</tr>
</tbody></table>


## Actualización de trabajos de prueba para {{site.data.keyword.DRA_short}}
{: #toolchain_pipeline_upload}

Para empezar, recupere la información de configuración de un trabajo de prueba.

1. En la etapa que contiene el trabajo de prueba, pulse el icono **Configuración de etapa** ![Icono de configuración de etapa de conducto](images/pipeline-stage-configuration-icon.png). Pulse **Configurar etapa**.
2. Cree un trabajo. Para el tipo de trabajo, seleccione **Prueba**.
3. Seleccione un trabajo de prueba que utilice el tipo de prueba Simple y copie la información de los campos **Mandato de prueba** y **Directorio de trabajo** a un editor. Necesitará esta información más tarde.
4. En el mismo trabajo de prueba Simple, cambie el tipo de probador seleccionando **Probador avanzado**.
5. En el campo **Mandato de prueba**, pegue los mandatos que ha copiado del campo **Mandato de prueba** del trabajo de prueba Simple.
6. En el campo **Directorio de trabajo**, pegue la vía de acceso que ha copiado del campo **Directorio de trabajo** del trabajo de prueba Simple.
7. Complete los campos restantes para cargar los resultados de prueba de un tipo de prueba específico. Si desea cargar resultados de un segundo tipo de prueba en el mismo trabajo, complete también los campos que tienen el prefijo *Adicional*.

 * Tipo de métrica
 * Formato
 * Ubicación del archivo de resultados
8. Pulse **Guardar** para volver al conducto.

Los valores de los campos **Tipo de métrica** y **Ubicación del archivo de resultados** deben coincidir con el formato correcto:

<table><thead>
<tr>
<th>Tipo de métrica</th>
<th>Formatos soportados</th>
</tr>
</thead><tbody>
<tr>
<td>Prueba de verificación funcional</td>
<td>Mocha, JUnit</td>
</tr>
<tr>
<td>Prueba de unidad</td>
<td>Mocha, JUnit, Karma/Mocha</td>
</tr>
<tr>
<td>Cobertura de código</td>
<td>Istanbul, Blanket.js</td>
</tr>
</tbody></table>

La *Figura 1* muestra un trabajo de prueba que está configurado para ejecutar pruebas de unidad, cargar los resultados en formato de Mocha y cargar los resultados de la cobertura de código en formato de Istanbul.

![Trabajo de carga de Deployment Risk Analytics](images/DRA_upload_job.png)
*Figura 1. Cargar resultados en DevOps Analytics*

## Definición de puertas de {{site.data.keyword.DRA_short}} en el conducto
{: #toolchain_pipeline_gates}

Las puertas de {{site.data.keyword.DRA_short}} comprueban si los resultados de las pruebas cumplen la política definida. Si no se cumple la política, la puerta de {{site.data.keyword.DRA_short}} falla. Generalmente, las puertas se colocan al final de cada etapa del conducto. Esta ubicación es ideal para comprobar la calidad de la compilación con la política para asegurarse de que es seguro promocionarla de un entorno a otro. Sin embargo, puede colocar puertas en cualquier sitio del conducto donde desee comprobar un criterio específico.

1. En una etapa, pulse el icono **Configuración de etapa** ![Icono de configuración de etapa de conducto](images/pipeline-stage-configuration-icon.png) y pulse **Configurar etapa**.
2. Pulse **Añadir trabajo**. Para el tipo de trabajo, seleccione **Prueba**.
3. Especifique un nombre para el nuevo trabajo, como *Puerta (Prueba de unidad)*.
4. Para el tipo de probador, **Puerta de {{site.data.keyword.DRA_short}}**.
5. Especifique el nombre del entorno. Asegúrese de que este valor coincida con el que ha definido en sus [propiedades de entorno](#toolchain_pipeline_props).
6. Defina el nombre de la política que se debe comprobar en esta puerta.

 Este nombre debe coincidir exactamente con uno de los nombres de política que ha definido. Puede especificar sólo políticas que están definidas en la misma organización de {{site.data.keyword.Bluemix_notm}} como su cadena de herramientas.

7. Opcional: Para hacer que una puerta funcione en modalidad de advertencia, desmarque el recuadro de selección **Dejar de ejecutar esta etapa si el trabajo falla**. En modalidad de advertencia, {{site.data.keyword.DRA_short}} completa el mismo análisis de política en la puerta y genera informes, pero si se produce un error, el conducto no se detiene.
8. Pulse **Guardar** para volver al conducto.
9. Configure puertas para todas sus políticas de {{site.data.keyword.DRA_short}} repitiendo estos pasos.

![Trabajo de Mocha de Deployment Risk Analytics](images/DRA_gate_job.png)
*Figura 2. Puerta de DevOps Analytics*

Cuando haya terminado de configurar su conducto, empiece a utilizar use {{site.data.keyword.DRA_short}}. Para obtener instrucciones, consulte [Ejecución de Delivery Pipeline](./pipeline_decision_reports.html#toolchain_reports).
