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

# Gestión de interconexiones
{: #deliverypipeline_managing}
Última actualización: 30 de agosto de 2016
{: .last-updated}

Puede administrar, configurar y ampliar las integraciones de IBM&reg; Bluemix&reg; {{site.data.keyword.deliverypipeline}}.
{:shortdesc}

Complete las tareas siguientes para administrar, configurar y ampliar un conducto.

## Control de acceso
{: #deliverypipeline_access}

Puede restringir quién puede ejecutar etapas o modificar un conducto. Para ello, vaya a la página Valores de canalización, a la que puede acceder pulsando el icono **Configuración de etapa** en la página Conducto: Todas las etapas.

![El icono de engranaje de valores de interconexión](./images/pipeline_settings.png)

## Propiedades y recursos del entorno
{: #deliverypipeline_envprop}

Puede utilizar propiedades de entorno y recursos preinstalados para interactuar con el servicio de {{site.data.keyword.deliverypipeline}}. Por ejemplo, puede incorporarlos a un script de trabajo o a un mandato de prueba. Para obtener más información, consulte [Propiedades de entorno y recursos para el servicio de {{site.data.keyword.deliverypipeline}}](./deploy_var.html).

Puede añadir sus propias propiedades de entorno a una etapa desde su separador **PROPIEDADES DE ENTORNO**. Las propiedades de entorno están disponibles para todos los trabajos en una etapa.

Puede añadir cuatro tipos de propiedades desde el separador Propiedades de entorno:
* **Texto**: Una clave de propiedad con un valor de línea única.
* **Área de texto**: Una clave de propiedad con un valor de varias líneas.
* **Seguro**: Una clave de propiedad con un valor de línea única. El valor se visualiza como asteriscos.
* **Propiedades**: Un archivo del repositorio del proyecto. Este archivo puede contener varias propiedades. Cada propiedad debe estar en su propia línea. Para pares de clave-valor independientes, utilice el signo igual (=).

## Ampliación de las posibilidades del conducto
{: #deliverypipeline_extend}

Puede ampliar las prestaciones del conducto Build & Deploy configurando los trabajos para utilizar servicios soportados. Por ejemplo, los trabajos de prueba pueden ejecutar exploraciones de código estáticas y los trabajos de compilación pueden globalizar series.

Para obtener más información sobre cómo ampliar las funciones de conducto, consulte [Ampliación de las funciones de servicio de {{site.data.keyword.deliverypipeline}}](./deliverypipeline_extension.html).

<!-- [1]: https://www.ng.bluemix.net/docs/manageapps/deployingapps.html#appmanifest
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
[23]: ./images/pipeline_settings.png
[24]: https://www.ng.bluemix.net/docs/services/reqnsi.html#add_service
[25]: ../deploy_var
[26]: ./images/click_stage_run_number.png
[27]: ./images/diagram.jpg -->
