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
Última actualización: 17 de Noviembre de 2016
{: .last-updated}

Puede administrar, configurar y ampliar las integraciones de IBM&reg; Bluemix&reg; {{site.data.keyword.deliverypipeline}}.
{:shortdesc}

Complete las tareas siguientes para administrar, configurar y ampliar un conducto.

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

Puede ampliar las prestaciones del conducto configurando los trabajos para utilizar servicios soportados. Por ejemplo, los trabajos de prueba pueden ejecutar exploraciones de código estáticas y los trabajos de compilación pueden globalizar series.

Para obtener más información sobre cómo ampliar las funciones de conducto, consulte [Ampliación de las funciones de servicio de {{site.data.keyword.deliverypipeline}}](./deliverypipeline_extension.html).

