---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Acerca de {{site.data.keyword.deliverypipeline}}
{: #deliverypipeline_about}
Última actualización: 29 de agosto de 2016
{: .last-updated}

El servicio de IBM&reg; Bluemix&reg; {{site.data.keyword.deliverypipeline}}, también conocido como conducto, automatiza el despliegue continuo de los proyectos de Bluemix. En un conducto, las secuencias de etapas recuperan la entrada y los trabajos de ejecución, como compilaciones, pruebas y despliegues.
{:shortdesc}

En las secciones siguientes se describen los detalles conceptuales que hay detrás de los conductos.

## Etapas
{: #deliverypipeline_stages}

Las etapas organizan la entrada y los trabajos a medida que se compila, se despliega y se prueba el código. Las etapas aceptan la entrada de cualquier repositorio de control de origen o compilan trabajos en otras etapas. Al crear la primera etapa, se establecerán los valores predeterminados en el separador **INPUT**.

La entrada de una etapa se pasa a los trabajos que contiene, y a cada trabajo se le da un contenedor limpio para ejecutarla. Los trabajos de una etapa no se pueden pasar artefactos entre sí.

Puede definir propiedades del entorno de etapas que se pueden utilizar en todos los trabajos. Por ejemplo, podría definir una propiedad `TEST_URL` que pasa un único URL para desplegar y probar trabajos en una sola etapa. El trabajo de despliegue podría desplegarse en dicho URL, y el trabajo de prueba podría probar la app en ejecución en el URL.

De forma predeterminada en una etapa, las compilaciones y los despliegues se desencadenan automáticamente cada vez que se entreguen cambios a un repositorio de control de origen del proyecto. Las etapas y los trabajos se ejecutan en serie; permiten el control de flujo para el trabajo. Por ejemplo, puede situar una etapa de prueba antes de una etapa de despliegue. Si fallan las pruebas en la etapa de prueba, no se ejecutará la etapa de despliegue.

Puede que desee un control más estricto de una etapa específica. Si no desea que se ejecute una etapa cada vez que se produzca un cambio en su entrada, puede inhabilitar la prestación. En el separador **ENTRADA**, en la sección Desencadenante de etapa, pulse **Ejecutar trabajos sólo cuando esta etapa se ejecute manualmente**.

![El separador ENTRADA](./images/input_tab_only_execute.png)

## Trabajos
{: #deliverypipeline_jobs}

Un trabajo es una unidad de ejecución dentro de una etapa. Una etapa puede contener varios trabajos, y los trabajos de una etapa se ejecutan secuencialmente. De forma predeterminada, si falla un trabajo, no se ejecutarán los trabajos posteriores de la etapa.

![Compilar y probar trabajos en una etapa](./images/jobs.png)

Los trabajos se ejecutan en directorios de trabajo discretos dentro de los contenedores Docker creados para cada ejecución de conducto. Antes de que se ejecute un trabajo, su directorio de trabajo se rellena con la entrada definida en el nivel de etapa. Por ejemplo, es posible que tenga una etapa que contenga un trabajo de prueba y un trabajo de despliegue. Si instala dependencias en un trabajo, no estarán disponibles en el otro trabajo. Sin embargo, si convierte en disponibles las dependencias en la entrada de la etapa, estarán disponibles para ambos trabajos.

Excepto para los trabajos de compilación simples, al configurar un trabajo, puede incluir scripts shell UNIX que incluyan mandatos de compilación, prueba o despliegue. Dado que los trabajos se ejecutan en contenedores ad hoc, las acciones de un trabajo no pueden afectar a los entornos de ejecución de otros trabajos, incluso aunque estos trabajos formen parte de la misma etapa.

Una vez que se ejecute un trabajo, el contenedor creado para él se descartará. Los resultados de una ejecución de trabajo pueden continuar, pero el entorno en el que se ha ejecutado no.

**Nota**: Los trabajos se pueden ejecutar durante un máximo de 60 minutos. Cuando los trabajos superan dicho límite, fallarán. Si un trabajo está superando el límite, divídalo en varios trabajos. Por ejemplo, si un trabajo lleva a cabo tres tareas, puede dividirlo en tres trabajos: uno para cada tarea.

Para obtener más información sobre cómo añadir un trabajo a una etapa, [consulte Adición de un trabajo a una etapa](./build_deploy.html#deliverypipeline_add_job).

### Trabajos de compilación

Los trabajos de compilación compilan el proyecto en preparación para el despliegue. Generan artefactos que se pueden enviar a un directorio de archivado de compilación, aunque de forma predeterminada, los artefactos se colocan en el directorio raíz del proyecto.

Los trabajos que toman entrada de trabajos de compilación deben hacer referencia a los artefactos de compilación en la misma estructura en la que se crearon. Por ejemplo, si un trabajo de compilación archiva artefactos de compilación en un directorio de `salida`, un script de despliegue podría hacer referencia al directorio de `salida` en lugar de al directorio raíz del proyecto para desplegar el proyecto compilado.

**Nota**: Si selecciona el tipo de compilador **Simple** para un trabajo de compilación, salte el proceso de compilación. En ese caso, el código no se compila, pero se envía a la etapa de despliegue tal cual. Para compilar y desplegar, seleccione un tipo de compilador distinto a **Simple**.

#### Propiedades de entorno para scripts de compilación
Puede incluir propiedades de entorno dentro de los mandatos shell de compilación del trabajo de compilación. Las propiedades proporcionan acceso a información sobre el entorno de ejecución del trabajo. Para obtener más información, [consulte Propiedades del entorno y recursos para el servicio {{site.data.keyword.deliverypipeline}}](./deploy_var.html).

### Trabajos de despliegue

Los trabajos de despliegue cargan el proyecto a Bluemix como una app y son accesibles desde un URL. Una vez que se despliegue un proyecto, puede encontrar la app desplegada en el panel de control de Bluemix. Puede configurar los trabajos de compilación y de despliegue como etapas independientes o añadirlos a la misma etapa para que se ejecuten automáticamente.

Los trabajos de despliegue pueden desplegar nuevas apps o actualizar apps existentes. Incluso si despliega por primera vez una app utilizando otro método, como por ejemplo la interfaz de línea de mandatos de Cloud Foundry o la barra de ejecución en el IDE de web, puede actualizar la app utilizando un trabajo de despliegue. Para actualizar una app, en el trabajo de despliegue, utilice el nombre de dicha app.

Puede desplegar en una o más regiones y servicios. Por ejemplo, puede configurar el servicio de {{site.data.keyword.deliverypipeline}} de forma que los artefactos de desarrollo utilicen IBM Containers, que se prueben en una región y que se desplieguen en producción en varias regiones. Para obtener más información, consulte [Regiones](../../overview/index.html#ov_intro__reg).

#### Propiedades de entorno para los scripts de despliegue

Puede incluir propiedades de entorno dentro de un script de despliegue del trabajo de despliegue. Estas propiedades proporcionan acceso a la información sobre el entorno de ejecución del trabajo. Para obtener más información, [consulte Propiedades del entorno y recursos para el servicio {{site.data.keyword.deliverypipeline}}](./deploy_var.html).

### Trabajos de prueba
Si desea solicitar que se cumplan las condiciones, incluya trabajos de prueba antes o después de los trabajos de compilación y despliegue. Puede personalizar trabajos de prueba para que sean tan simples o tan complejos como se necesite. Por ejemplo, puede emitir un mandato cURL y esperar una respuesta determinada. También puede ejecutar una suite de pruebas de unidad o desencadenar pruebas funcionales con servicios de prueba de terceros, como por ejemplo Sauce Labs.

Si sus pruebas generan archivos de resultados en formato XML JUnit, se mostrará un informe basado en los archivos de resultados en el separador **Pruebas** de cada página de resultados de prueba. Si falla una prueba, el trabajo también fallará.

#### Propiedades del entorno para los scripts de prueba

Puede incluir propiedades de entorno en el script de un trabajo de prueba. Las propiedades proporcionan acceso a información sobre el entorno de ejecución del trabajo. Para obtener más información, [consulte Propiedades del entorno y recursos para el servicio {{site.data.keyword.deliverypipeline}}](./deploy_var.html).

## Archivos de manifiesto
{: #deliverypipeline_manifest}

Los archivos de manifiesto, que se denominan `manifest.yml` y se almacenan en el directorio raíz de un proyecto, controlan la forma en que se despliega el proyecto en Bluemix. Para obtener información sobre cómo crear archivos de manifiesto para un proyecto, [consulte la Documentación de Bluemix sobre los manifiestos de la aplicación](https://www.ng.bluemix.net/docs/manageapps/deployingapps.html#appmanifest). Para integrarse con Bluemix, el proyecto debe tener un archivo de manifiesto en su directorio raíz. Sin embargo, no es necesario que realice el despliegue en función de la información del archivo.

En el conducto, puede especificar todo lo que puede hacer un archivo de manifiesto utilizando argumentos del mandato `cf push`. Los argumentos del mandato `cf push` son útiles en los proyectos que tienen varios destinos de despliegue. Si varios trabajos de despliegue intentan utilizar la ruta especificada en el archivo de manifiesto del proyecto, se producirá un conflicto.

Para evitar conflictos, puede especificar una ruta utilizando `cf push` seguido del argumento del nombre de host, `-n`, y un nombre de ruta. Al modificar el script de despliegue para etapas individuales, puede evitar conflictos de ruta al desplegar en varios destinos.

Para utilizar los argumentos del mandato `cf push`, abra los valores de configuración para un trabajo de despliegue y modifique el campo **Desplegar script**. Para obtener más información, [consulte la documentación de Cloud Foundry Push](http://docs.cloudfoundry.org/devguide/installcf/whats-new-v6.html#push).

## Un conducto de ejemplo
{: #deliverypipeline_example}

Un conducto de ejemplo puede contener tres etapas:

1. Una etapa de compilación que compila y ejecuta procesos de compilación en una app.
2. Una etapa de prueba que despliega una instancia de la app y, a continuación, ejecuta pruebas en esta.
3. Una etapa de producción que despliega una instancia de producción de la app probada.

Este conducto se muestra en el siguiente diagrama conceptual:

![Un diagrama conceptual de etapas y trabajos en un conducto](./images/diagram.jpg)

*Un modelo conceptual de un conducto de tres etapas*

Las etapas toman su entrada de repositorios y trabajos de compilación, y los trabajos de una etapa se ejecutan de forma secuencial e independiente entre sí. En el conducto de ejemplo, las etapas se ejecutarán secuencialmente, aunque las etapas de Prueba y de Producción tomen la salida de la etapa de Compilación como su entrada.

<!--
[1]: https://www.ng.bluemix.net/docs/manageapps/deployingapps.html#appmanifest
[2]: https://www.ng.bluemix.net/docs/#services/DeliveryPipeline/index.html#getstartwithCD
[3]: http://docs.cloudfoundry.org/devguide/installcf/whats-new-v6.html#push
[4]: https://console.ng.bluemix.net/?ace_base=true/#/pricing/cloudOEPaneId=pricing
[5]: ./images/open_logs.png
[6]: #manifests
[7]: ./images/runbar-annotated-dark.png
[8]: ./images/input_tab_only_execute.png
[9]: ./images/deploy_to.png
[10]: ./images/view_logs_and_history.png
[11]: ./images/play_button.png
[12]: ./images/basicAnimate.gif
[13]: ./images/AddStage.png
[14]: ./images/AddJob.png
[15]: ./images/jobs.png
[16]: ./images/RunStage.png
[17]: https://www.ng.bluemix.net/docs/starters/container_pipeline.html#container_pipeline
[18]: ../../../tutorials/basicbuild
[19]: #add_stage
[20]: #add_job
[21]: ../deploy_ext
[22]: ./images/pipeline_settings_icon.png
[23]: https://www.ng.bluemix.net/docs/services/reqnsi.html#add_service
[24]: ../deploy_var
[25]: ./images/click_stage_run_number.png
[26]: ./images/diagram.jpg
-->
