---

copyright:
  years: 2016

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

# Compilación y despliegue
{: #deliverypipeline_build_deploy}
Última actualización: 17 de Noviembre de 2016
{: .last-updated}

El servicio de IBM&reg; Bluemix&reg; {{site.data.keyword.deliverypipeline}} permite implementar una integración continua repetible y un proceso de entrega continuo.
{:shortdesc}

Complete las tareas siguientes para crear y configurar un conducto.

## Adición de una etapa
{: #deliverypipeline_add_stage}

1. En la página Conducto, pulse **AÑADIR ETAPA**. Se abrirá la página Configuración de etapa.
2. Configurar la etapa.
  1. En el separador **ENTRADA**, seleccione una entrada para la etapa.
  2. En el separador **TRABAJOS**, añada y configure al menos un trabajo. La primera etapa normalmente tiene como mínimo un trabajo de compilación.
3. Pulse **GUARDAR**.

## Adición de un trabajo a una etapa
{: #deliverypipeline_add_job}

1. En la etapa, pulse el icono **Configuración de etapa** y, a continuación, pulse **Configurar etapa**.
2. Pulse el separador **TRABAJOS**.
3. Pulse **AÑADIR TRABAJO**. Seleccione el tipo de trabajo para añadir.
4. Configurar el trabajo.
5. Pulse **GUARDAR**.

![Adición de un trabajo a una etapa](./images/AddJob2.png)

## Ejecución de una etapa
{: #deliverypipeline_run_stage}

Puede ejecutar de manera manual una etapa pulsando el icono **Run Stage** en la página Conducto. 

![Al pulsar el icono Run Stage en una etapa](./images/RunStage.png)

También puede solicitar compilaciones y despliegues a demanda desde la página de historial de compilaciones de una de estas dos formas:
* Arrastre una compilación al recuadro que hay bajo una etapa configurada.
* Junto a una compilación, pulse el icono **Enviar a** y, a continuación, seleccione un espacio en el que desplegarlo.
  ![La etapa Ejecutar con este icono de compilación](./images/deploy_to.png)

Para cancelar una etapa de ejecución, en la etapa, pulse **Ver registros e historial**. En la lista de trabajos, pulse el número del trabajo en ejecución y, a continuación, pulse **CANCELAR**. También puede cancelar trabajos individualmente pulsando un trabajo y, a continuación, pulsando **CANCELAR**, o pulsando el icono **Detener** junto a un trabajo en su etapa.

## Despliegue de una app
{: #deliverypipeline_deploy}

Un trabajo de despliegue configurado correctamente despliega la app al destino siempre que se ejecute el trabajo. Para ejecutar manualmente un trabajo de despliegue, pulse el icono **Etapa de ejecución** de la etapa en la que se encuentra el trabajo.

### Revisiones de entrada
Al ejecutar una etapa manualmente, o si la ejecuta porque la etapa anterior se ha completado, la etapa de ejecución selecciona su revisión de entrada. Normalmente, la revisión de entrada es un número de compilación. Para seleccionar la revisión de entrada, la etapa seguirá estas condiciones: 

* Si se selecciona una revisión específica, utilícela.
* Si no se especifica una revisión específica, busque etapas anteriores hasta que se encuentre una etapa que utilice la misma entrada. Busque y utilice la última revisión de ejecución correcta de dicha entrada.
* Si no se especifica una revisión específica y ninguna otra etapa utiliza el origen especificado como entrada, utilice la revisión más reciente de la entrada.

**Consejo:** Puede desplegar una compilación anterior. En la etapa que contiene la compilación, pulse **Ver registros e historial**. En la página que se abre, pulse para expandir el número de ejecución y, a continuación, pulse el trabajo de compilación. Pulse **ENVIAR A**, y seleccione un destino.

### Adición de servicios para aplicaciones
Puede añadir servicios a las aplicaciones y gestionar los servicios desde el panel de control de Bluemix o la interfaz de línea de mandatos (CLI) de Cloud Foundry. También puede emitir mandatos de CLI de Cloud Foundry en scripts para trabajos de conductos de DevOps Services. Por ejemplo, puede añadir un servicio a una app en el script de un trabajo de despliegue. Para obtener más información sobre cómo añadir servicios, consulte [Adición de un servicio para la aplicación](https://www.ng.bluemix.net/docs/services/reqnsi.html#add_service).

## Visualización de registros
{: #deliverypipeline_view_logs}

Puede ver los registros para trabajos y ver etapas a medida que se ejecutan en la página Historial de etapas.

Para ver el registro de un trabajo, pulse el trabajo. Como alternativa, en una etapa, pulse **Ver registros e historial**.

Para ver el registro de tiempo de ejecución de una aplicación desplegada, pulse **Ver registro de tiempo de ejecución**.

![Áreas de un icono de etapa que se pueden pulsar para abrir los registros relevantes](./images/view_logs_and_history.png)

Además de los registros de trabajos, puede ver resultados de pruebas de unidades, artefactos generados y cambios de códigos para cualquier trabajo de compilación.

También puede ejecutar, cancelar o configurar una etapa desde la página Historial de etapas. Pulse **EJECUTAR** para ejecutar una etapa o **CONFIGURAR** para configurar una etapa. Mientras una etapa está en ejecución, puede cancelarla pulsando el número de ejecución y, a continuación, pulsando **CANCELAR**.


