---

copyright:
  years: 2017
lastupdated: "2017-4-5"
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

# Cómo trabajar con conductos compuestos (experimental)
{: #deliverypipeline_create_composite}

Con la función de conductos compuestos para {{site.data.keyword.deliverypipeline}}, puede gestionar procesos de entrega continua e integración continua repetibles para apps de software relacionadas.
{:shortdesc}

Puede crear conductos compuestos para gestionar las apps de una cadena de herramientas. Si la cadena de herramientas contiene apps desplegadas por {{site.data.keyword.deliverypipeline}}, la cadena de herramientas se actualiza de forma dinámica cuando se añaden o retiran conductos de entrega de la cadena de herramientas. También puede añadir apps procedentes de fuentes externas al conducto compuesto.

## Creación de un conducto compuesto
{: #compositepipeline_create_for_toolchain}

1. En el menú que hay junto al logotipo de Bluemix, pulse **Servicios > DevOps**

1. En el menú de la izquierda, pulse **Conductos**.

2. Para habilitar la característica de conducto compuesto, pulse **Más información** y luego pulse **Habilitar**. El conducto compuesto se habilita para cada usuario, de modo que sólo los miembros de la organización (org) que decidan utilizar la característica experimental podrán ver los conductos compuestos que cree.

2. Pulse **Crear** > **Conducto compuesto**.

3. Escriba un nombre para el conducto compuesto. También puede modificar la descripción del conducto.

4. En la lista **Cadena de herramientas**, seleccione una cadena de herramientas.

    1. Para crear una cadena de herramientas y un conducto compuesto vacíos, seleccione **Nuevo**.

    2. Para crear un conducto compuesto para una de las cadenas de herramientas, seleccione su nombre.

5. Si crea una cadena de herramientas vacía, seleccione **Añadir entornos predeterminados**. Puede utilizar estos entornos lógicos predeterminados para controlar la ejecución de procesos a través del conducto compuesto.

6. Pulse **Crear**.

Las etapas que haya configurado se correlacionan automáticamente con el espacio adecuado de la organización y se crea un plan de despliegue para el conducto compuesto.

Si ha creado el conducto compuesto para una cadena de herramientas que contiene conductos de entrega, las apps correspondientes a todos los conductos de la cadena de herramientas se añaden al conducto compuesto. Las etapas que haya configurado en los conductos de entrega se correlacionan automáticamente con los espacios adecuados de la organización y se muestran sus estados.
Para ver el estado de cada trabajo de una app, expanda la app.

También se crea un plan de despliegue para el conducto compuesto. De forma predeterminada, los trabajos de todas las apps se ejecutan en paralelo para un espacio, pero puede cambiar el orden del despliegue de las apps en el plan.

Si ha creado el conducto compuesto para una nueva cadena de herramientas, se crea un plan de despliegue para que lo personalice.

![Expanda cada app para ver cada trabajo de su conducto](images/composite_view.png "expandir cada app")

## Modificación del plan de despliegue
{: #compositepipeline_modify_dp}

De forma predeterminada, se crea un plan de despliegue para un conducto compuesto. Este plan de despliegue captura toda la información sobre las etapas de cualquier conducto de entrega de la cadena de herramientas. Puede ver y modificar el plan de despliegue de cada etapa.

En la etapa para la que desea modificar el plan de despliegue, pulse el menú y pulse **Plan de despliegue**.

![Abra el plan de despliegue](images/open_deployment_plan.png "abrir el plan de despliegue")

Se muestra la lista de las tareas de despliegue del entorno.

![Plan de despliegue predeterminado para un conducto compuesto que contiene tres conductos individuales](images/composite_deploy_plan.png)

Para obtener más información sobre cómo modificar el plan de despliegue, consulte [Personalización de planes de despliegue para conductos compuestos](/docs/services/ContinuousDelivery/pipeline_deployment_plan.html).

## Modificación de conductos individuales
{: #compositepipeline_add_job}

Puede modificar conductos individuales del conducto compuesto.

1. Expanda la app.

2. En el menú de la etapa, pulse **Configurar**.

3. Añada, modifique o suprima trabajos de la etapa. Para ver instrucciones detalladas, consulte [Adición de un trabajo a una etapa](pipeline_build_deploy.html#deliverypipeline_add_job).

## Ejecución de trabajos en un conducto compuesto
{: #compositepipeline_run_jobs}

Después de expandir una app para ver sus trabajos, puede ejecutar manualmente todos sus trabajos en una etapa. Pulse el icono **Desplegar en *etapa*** en el espacio de una app.

![Ejecución de una etapa en una sola app](images/composite_run_stage.png)

Para ejecutar todos los trabajos de todas las apps que están en un espacio, pulse el icono **Desplegar en *espacio*** en el espacio correspondiente al conducto compuesto.

![Ejecución de una etapa en todas las apps](images/composite_run_space.png)

Los trabajos se ejecutan de acuerdo con el plan de despliegue del conducto compuesto.

## Visualización de registros
{: #compositepipeline_view_logs}

Para ver los registros correspondientes a un trabajo, expanda la app que contiene el trabajo y pulse en el trabajo.

## Utilización de IBM Bluemix DevOps Connect para integrar con IBM UrbanCode Deploy
{: #compositepipeline_devops_connect}

IBM Bluemix DevOps Connect coordina la comunicación entre la instalación local de IBM&reg; UrbanCode&reg; Deploy y {{site.data.keyword.contdelivery_short}}. Después de instalar DevOps Connect, puede crear integraciones que puede utilizar para gestionar apps de IBM UrbanCode Deploy con conductos compuestos.

**Requisitos previos**

   * Para registrar DevOps Connect, debe tener un ID de IBM.

   * Asegúrese de que [Java&trade; Runtime Environment versión 8 actualización 121 o posterior ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://java.com/en/download/){:new_window} esté en el sistema host y de que la variable del sistema PATH esté establecida en su ubicación.

   * Necesita una señal de autorización de administrador de IBM UrbanCode Deploy.

Para utilizar DevOps Connect para integrar con IBM UrbanCode Deploy, siga estos pasos:

1. Instale DevOps Connect y utilícelo para integrar su organización con IBM UrbanCode Deploy.

  1. En un conducto compuesto pulse **Añadir app**. En la lista **Gestionado por**, seleccione **IBM UrbanCode Deploy**.

  1. Visualice los pasos de la integración. Para ver una lista de apps, pulse el icono de información (![Icono de información](/images/info.png)) que hay junto a **Apps** y pulse **Configurar IBM UrbanCode Deploy para esta organización**.

  1. In la ventana Configurar integración de UrbanCode Deploy, pulse **Descargar** para descargar DevOps Connect. Coloque el archivo JAR en un sistema que tenga acceso a IBM UrbanCode Deploy.

  1. En la ventana, copie el script de instalación de DevOps Connect. El script contiene el mandato para iniciar DevOps Connect y las credenciales necesarias para identificar el servicio {{site.data.keyword.contdelivery_short}}.

  1. En el sistema en el que ha colocado DevOps Connect, abra un shell de mandatos y pegue el script que ha copiado.

  1. Ejecute el script. DevOps Connect muestra mensajes de arranque.

1. Registre DevOps Connect.

  1.  En el sistema en el que ha colocado DevOps Connect, utilice un navegador web para abrir el panel de control de DevOps Connect. El URL predeterminado es https://localhost:8443. Para cambiar el URL y ver otras opciones de arranque, consulte la [documentación de DevOps Connect ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/urbancode/plugindoc/urbancode-sync/ibm-urbancode-sync-utility/1-2/){:new_window}.


1. En la página "Registrarse en IBM", escriba su ID de IBM y su contraseña y pulse **Registrar**. Debe registrarse cada vez que inicie DevOps Connect.

1. Con DevOps Connect, utilice el plugin de IBM UrbanCode Deploy para DevOps Connect para crear una integración entre la organización e IBM UrbanCode Deploy.

    1. En la página Integraciones, pulse **Añadir nueva**.

    1. En el campo **Nombre**, escriba un nombre para la integración.

    1. En la lista **Tipo de integración**, seleccione **IBM UrbanCode Deploy para DevOps Connect**.

    1. En el campo **URI del servidor**, escriba el URL público del servidor de IBM UrbanCode Deploy; por ejemplo, `https://my_UCD.example.com:8443`.

    1. En el campo **Señal de autenticación**, escriba o pegue la señal de autenticación que ha generado IBM UrbanCode Deploy.

    1. En el campo **Correo electrónico del usuario de administración**, escriba su dirección de correo electrónico.

    1. Para confirmar que la integración se ha realizado correctamente, pulse **Ejecutar integración**. DevOps Connect se conecta a la instancia de IBM UrbanCode Deploy especificada en el campo **URI del servidor**. DevOps Connect recibe autorización de la señal que se ha pegado en el campo **Señal de autenticación**.

    1. Pulse **Guardar**.

Si la integración se ha realizado correctamente, puede añadir apps de IBM UrbanCode Deploy a los conductos compuestos. Para obtener más información, consulte [Adición de apps de IBM UrbanCode Deploy](/docs/services/ContinuousDelivery/pipeline_composites.html#compositepipeline_add_apps).


## Adición de apps de IBM UrbanCode Deploy
{: #compositepipeline_add_apps}

Si es miembro de una organización que se ha integrado con IBM UrbanCode Deploy mediante DevOps Connect, puede añadir las apps a las que puede acceder en IBM UrbanCode Deploy al conducto compuesto. Para ver instrucciones de instalación, consulte [Utilización de IBM Bluemix DevOps Connect para integrar con IBM UrbanCode Deploy](/docs/services/ContinuousDelivery/pipeline_composites.html#compositepipeline_devops_connect).

Si es miembro de una organización que está conectada a IBM UrbanCode Deploy, puede añadir apps de UrbanCode Deploy a conductos compuestos, seleccionar los procesos de apps que desea incluir en el plan de despliegue y personalizar el despliegue de las apps.

1. En el conducto compuesto, pulse **Añadir app**.

2. En la lista **Gestionado por**, seleccione **IBM UrbanCode Deploy**. Si recientemente ha integrado {{site.data.keyword.contdelivery_short}} con IBM UrbanCode Deploy, es posible que tenga que renovar el navegador para ver el servidor.

3. Seleccione las apps que desea añadir y pulse **Continuar**. Se muestran todos los procesos de apps que están disponibles para las apps de IBM UrbanCode Deploy. Se añaden al plan de despliegue entradas para ejecutar los procesos que ha seleccionado.

4. Seleccione los procesos de apps que desea a utilizar para las apps. Utilice las opciones de búsqueda y de filtro para localizar los procesos.

5. Pulse **Guardar**. Cada app de IBM UrbanCode Deploy que ha seleccionado se visualiza como una app en el conducto compuesto.

6. Correlacione entornos entre las apps de IBM UrbanCode Deploy y los entornos lógicos del conducto compuesto:

    1. En el menú que hay junto al nombre del entorno lógico, seleccione **Gestionar entornos lógicos**.

    ![Selección de Gestionar entornos lógicos](images/composite_logical_env.png)

    2. Para cada app del conducto compuesto, seleccione los entornos que ha definido en IBM UrbanCode Deploy. Los procesos de apps que seleccione se ejecutarán solo en los entornos de dicha app.

    3. Pulse **Guardar**.

    4. Repita estos pasos para cada entorno lógico que utilice.
