---

copyright:
  years: 2015, 2017
lastupdated: "2017-3-21"

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Actualice su proyecto {{site.data.keyword.jazzhub_short}} a una cadena de herramientas
{: #upgrade_projects}

{{site.data.keyword.jazzhub}} está evolucionando hacia {{site.data.keyword.contdelivery_full}}. Como parte de este cambio, los proyectos se actualizarán a cadenas de herramientas. 

Puede actualizar su proyecto o esperar a que se actualice automáticamente. Se recomienda actualizar el proyecto lo antes posible para poder controlar el nombre de la cadena de herramientas y la organización para la que se crea.   
{: shortdesc}

## Cadenas de herramientas
{: #compare_toolchains}

Las cadenas de herramientas son como proyectos, con algunas diferencias importantes:

- Los proyectos solo pueden tener un repositorio (repo) y un conducto. Las cadenas de herramientas pueden tantos repositorios y conductos como sea necesario.
- Las cadenas de herramientas pueden incluir herramientas que no están disponibles en proyectos, como por ejemplo Slack, Sauce Labs, PagerDuty y {{site.data.keyword.DRA_full}}.
- El acceso a las cadenas de herramientas se gestiona mediante organizaciones estándares de Bluemix. La condición de miembro se mantiene a nivel de organización, a diferencia de los proyectos, donde los miembros se mantienen a nivel de proyecto.

Puede obtener información acerca de las cadenas de herramientas en [YouTube![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://youtu.be/2SIPE1e7NJ4){: new_window} o en [Iniciación a {{site.data.keyword.contdelivery_short}}](/docs/services/ContinuousDelivery/index.html).
[![Enlace externo a YouTube](images/CD_video.png)](https://youtu.be/2SIPE1e7NJ4){: new_window}    

## Requisitos previos
{: #upgrade_prereqs}    

- Para acceder a la cadena de herramientas actualizada del proyecto, necesita un ID de Bluemix. Antes de actualizar, debe verificar que tiene un ID de Bluemix activo. Si no dispone de uno, [regístrese](https://console.ng.bluemix.net/registration/).
- Asegúrese de que el propietario del proyecto de DevOps Services sea correcto. La cadena de herramientas que se crea a partir del proyecto formará parte de la organización de Bluemix de dicho propietario. 

**Importante:** Eclipse Orion {{site.data.keyword.webide}} en la cadena de herramientas no es el {{site.data.keyword.webide}} asociado al proyecto. Si utiliza el {{site.data.keyword.webide}} y tiene cambios sin confirmar, confírmelos antes de actualizar.   


## Actualización de un proyecto a una cadena de herramientas
{: #project_to_toolchain}

Cuando el proyecto esté listo para actualizarse, se mostrará un mensaje en la tarjeta del proyecto y en la página Visión general.

![Imagen de tarjeta con la etiqueta Preparado para actualización](images/card-project-to-upgrade.png)

![Mensaje Momento de actualizar](images/banner-ready-to-upgrade.png)

**Consejo:** Encontrará proyectos que están preparados para la actualización en el menú de la página Mis proyectos:  

![Imagen del elemento de menú Proyectos para actualizar](images/menu-projects-to-upgrade.png)

## Inicio del proceso de actualización
{: #start_upgrade}

Antes de iniciar el proceso de actualización, puede verlo en acción en [YouTube![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://youtu.be/oaZVGveVxBg){: new_window}.
[![Enlace externo a YouTube](images/migration-video2.png)](https://youtu.be/oaZVGveVxBg){: new_window}    
Para actualizar el proyecto a una cadena de herramientas, siga estos pasos:

1. Para iniciar el proceso de actualización, en el mensaje de cabecera pulse **actualizar ahora**. Se abrirá la página "Cadena de herramientas de actualización de proyecto".  

   ![Ejemplo de una página de actualización](images/project-upgrade-toolchain.png)

   Para obtener una visión general del proceso de actualización, lea la descripción de esta página. En este caso, como el proyecto ha utilizado un repositorio de GitHub.com, la cadena de herramientas se conectará al mismo repositorio GitHub. La cadena de herramientas incluirá un nuevo conducto que contiene las mismas etapas y trabajos que el conducto del proyecto. Además, la cadena de herramientas contendrá un puntero a Eclipse Orion {{site.data.keyword.webide}} que se ejecuta en {{site.data.keyword.contdelivery_short}}.

2. Para personalizar la cadena de herramientas, puede configurar algunos valores:

   - Para cambiar el nombre de la cadena de herramientas, edite el campo **Nombre**. 

      ![Campo Nombre](images/name-change.png)

   - Para cambiar la organización de {{site.data.keyword.Bluemix_notm}} en la que se creará la cadena de herramientas, seleccione la organización en el menú de la cuenta:

      ![Selector de organización de Bluemix](images/bluemix-organization-chooser.png)

   Puesto que las cadenas de herramientas se gestionan a nivel de organización, asegúrese de seleccionar una organización donde los miembros del proyecto que necesiten acceder a la cadena de herramientas ya existan o se puedan añadir.  
  
3. Pulse **Crear**. Se crea la nueva cadena de herramientas y se muestra su página Visión general. 

   ![Visión general de la cadena de herramientas actualizada](images/new-toolchain-page.png)

   - Para acceder al repositorio GitHub o al rastreador de problemas asociado, pulse **GitHub** o **Problemas**.
   
   - Para acceder al conducto, pulse **Conducto de entrega**.  
   
   - Para acceder al {{site.data.keyword.webide}}, que aloja el contenido del repositorio que se ha extraído en el espacio de trabajo, pulse **Eclipse Orion {{site.data.keyword.webide}}**. 

## Cómo revisitar el proyecto
{: #revisit_projects}

Está preparado para utilizar la nueva cadena de herramientas. Ahora el proyecto está etiquetado como "Actualizado" y se muestra un mensaje de configuración en la página Visión general. 

![Imagen de tarjeta de proyecto con la etiqueta Actualizado](images/card-upgraded-project.png)

![Proyecto actualizado](images/banner-upgraded.png)

Puede ver los que los proyectos que se han actualizado seleccionando **Proyectos actualizados** en el menú de la página Mis proyectos: 

![Imagen del elemento de menú Proyectos actualizados](images/menu-upgraded-projects.png)

Si tiene que revertir la actualización, suprima la cadena de herramientas. A continuación, cuando vuelva a la página Visión general del proyecto, se volverá a mostrar el mensaje de actualización y podrá volver a actualizar cuando esté preparado. 

## Siguientes pasos
{: #upgrade_next_steps}   

1. Confirme que la actualización se ha completado comprobando el mensaje de la página Visión general del proyecto:    

   ![Proyecto actualizado](images/banner-upgraded.png)    

2. Asigne a los miembros del equipo acceso a la cadena de herramientas.    
    - Cada miembro del equipo debe tener una cuenta de Bluemix válida. Los miembros del equipo que no tienen cuentas deben [registrarse ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/registration){:new_window}.
    - Añada miembros del equipo a la organización (org) a la que pertenece la cadena de herramientas. 
3. Utilice las herramientas de la cadena de herramientas en lugar de las herramientas del proyecto de {{site.data.keyword.jazzhub_short}}. Por ejemplo, para editar código desde un navegador, utilice el IDE Web de la cadena de herramientas.    

## Resolución de problemas
{: #upgrade_troubleshoot}    

Si tiene preguntas o problemas, envíe un correo electrónico a [hub@jazz.net](mailto:hub@jazz.net). En su correo electrónico incluya los URL al proyecto de {{site.data.keyword.jazzhub_short}} y a la cadena de herramientas de {{site.data.keyword.contdelivery_short}}. 

