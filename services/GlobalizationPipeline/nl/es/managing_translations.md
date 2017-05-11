---

copyright:
  years: 2015, 2017
lastupdated: "2016-10-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Gestión de traducciones
{: #globalizationpipeline_managingtranslations}

Una vez que haya creado paquetes y que haya comenzado a generar traducciones para la aplicación, el contenido generado automáticamente se puede utilizar tal cual o se puede modificar. También puede elegir si desea utilizar una traducción automática que no sea la predeterminada. En esta sección se describe cómo cambiar el motor de traducción automática que realiza las traducciones para los paquetes, cómo realizar la edición humana posterior a la traducción y también cómo puede asignar roles de usuario y restricciones de acceso a las personas que necesitarán acceder a sus traducciones.
{:shortdesc}

## Configuración de la traducción automática
{: #globalizationpipeline_service_to_service}

{{site.data.keyword.GlobalizationPipeline_full}} da soporte a la posibilidad de integrar servicios de traducción automática alternativos para realizar la traducción automática de los paquetes. La adición de un servicio alternativo puede resultar beneficioso si el motor predeterminado utilizado por {{site.data.keyword.GlobalizationPipeline_short}} no ofrece un idioma específico que necesite o si prefiere las traducciones automáticas generadas por otro motor. El uso y los cargos para servicios alternativos están cubiertos bajo los términos de dichos servicios.

Para añadir y configurar un servicio de traducción automática alternativo para {{site.data.keyword.GlobalizationPipeline_short}}, seleccione el separador **Configuración de traducción automática** desde el panel de control {{site.data.keyword.GlobalizationPipeline_short}}.

* Para añadir un servicio de traducción automática que se encuentre en el catálogo de {{site.data.keyword.Bluemix_notm}}, (**Watson Language Translator**), el servicio debe añadirse en primer lugar al espacio de {{site.data.keyword.Bluemix_notm}}.

* Para añadir un servicio de terceros, seleccione el botón para dicho servicio en el separador **Configuración de traducción automática** y proporcione las credenciales de usuario necesarias para acceder al servicio.

Una vez que se haya añadido un servicio de traducción automática a {{site.data.keyword.GlobalizationPipeline_short}}, complete el resto de los pasos para completar la integración de dicho servicio.

1. Pulse **Habilitar** para activar la integración con dicho servicio.

2. Pulse **Actualizar idiomas** para ver la lista actualizada de idiomas de destino soportados.

3. En la lista de idiomas de destino, seleccione el motor de traducción automática que debe realizar la traducción.

4. Pulse **Guardar** para volver al separador **Configuración de traducción automática**.

Una vez que se haya configurado un servicio alternativo con {{site.data.keyword.GlobalizationPipeline_short}}, todos los idiomas de destino que se hayan asignado a dicho motor comenzarán a generarse utilizando dicho motor. 

Para dejar de utilizar un motor de traducción automática alternativo:

1. En el separador **Configuración de traducción automática**, pulse el botón **Inhabilitar** para el servicio que desea dejar de utilizar.

Una vez que esté inhabilitado un servicio de traducción automática alternativo, todas las traducciones generadas por el servicio permanecerán dentro de los paquetes. Sin embargo, la traducción a un determinado idioma de destino puede no estar disponible para futuras actualizaciones si el idioma de destino ya no está soportado por el motor de traducción automática que está habilitado actualmente.

<!-- Review comment: When you disable an engine, do you need to go back and reconfigure the languages?? Does it go back to the default engine? What happens? -->

## Visualización y edición de traducciones
{: #globalizationpipeline_translations}

El servicio de {{site.data.keyword.GlobalizationPipeline_short}} proporciona posibilidades de edición humana posterior a la traducción. Un traductor profesional o alguien con conocimientos en cualquiera de los idiomas de destino puede realizar ediciones a las traducciones generadas. Puede editar para mejorar la calidad o la coherencia de la traducción o para sustituir el texto preferido. Por ejemplo, es posible que desee sobrescribir la traducción de un nombre de producto.

Para ver y editar las traducciones para un idioma de destino:

1. En la página **Detalles del paquete**, seleccione un idioma de destino o pulse el icono **Ver las traducciones** ![Seleccione el icono Ver traducciones para ver las traducciones de un idioma de destino](images/viewProjectDetailIcon.png) desde la columna Acciones.
2. Las traducciones se presentan en una tabla que muestra la información de clave, origen y traducción.
 * **Clave:** Representa un atributo del archivo de recursos que tiene un valor asociado.
 * **Origen:** Representa una serie traducible que se ha incluido en el archivo de recursos subido.
 * **Traducción:** Representa la versión traducida de un valor de origen.
3. En la columna Acciones, pulse el icono **Modificar la traducción** ![Seleccione el icono Modificar la traducción para editar las traducciones de un par de clave/valor concreto](images/editIcon.png) para editar un valor traducible automáticamente.
4. Edite la traducción y pulse **Actualizar** para actualizar el valor traducido original con la edición.

![La ventana de diálogo Modificar traducción proporciona una manera sencilla de editar traducciones.](images/editTranslation.png) 

***Consejo:*** Cuando trabaje con paquetes grandes que incluyan muchas claves traducibles, encontrar un valor determinado puede ser complicado. En la página de traducción de idioma de destino, puede buscar rápidamente en todas las claves, el origen y las traducciones utilizando el recuadro **Buscar...**.

![Utilice el recuadro de búsqueda que se proporciona en la página de traducción de idioma de destino para buscar las claves, el origen, las traducciones, o los tres dentro de un idioma de destino.](images/search.png) 


## Adición de usuarios de API
{: #globalizationpipeline_users}

A medida que gestione las traducciones, es posible que desee otorgar acceso a usuarios de API adicionales basándose en las tareas que tiene que llevar a cabo. Por ejemplo, puede que desee habilitar a un traductor para editar la traducción, pero no podrá modificar la información del paquete.

| Tipo de rol | ¿Desea ver las traducciones? | ¿Desea editar las traducciones? | ¿Desea modificar la información de paquete? |
|-----------|--------------------|--------------------|----------------------------|
| Lector | Sí | No | No |
| Traductor | Sí | Sí | No |
| Administrador | Sí | Sí | Sí |

Si crea más usuarios de API, puede restringir su acceso para uno o varios paquetes específicos, u otorgarles acceso a todos los paquetes disponibles.

Para otorgar a un usuario de API acceso a paquetes en una instancia de servicio de {{site.data.keyword.GlobalizationPipeline_short}}:

1. En el panel de control de {{site.data.keyword.GlobalizationPipeline_short}}, pulse el separador **Usuarios de API**.
2. Pulse **Nuevo usuario de API**.
3. Escriba un **nombre de visualización** y un **comentario** para describir el nuevo usuario de API.
4. Elija un **tipo** para el nuevo usuario de API.
5. Elija para dar acceso al usuario de API a todos los paquetes o solo a los paquetes seleccionados.
6. Pulse **Guardar**.

![Complete el foro para crear un nuevo usuario de API.](images/newUser.png)

Se generarán y se visualizarán un ID de usuario y una contraseña de API. Copie y guarde las credenciales; después de cerrar la ventana, no podrá acceder a ellas de nuevo. Las credenciales se pueden utilizar para el servicio RESTful a través de [SDK](https://github.com/IBM-Bluemix/gp-common). 

Para restablecer la contraseña del usuario de la API:

1. En el panel de control de {{site.data.keyword.GlobalizationPipeline_short}}, pulse el separador **Usuarios de API**.
2. Pulse el icono **Restablecer contraseña** ![Seleccione este icono para restablecer la contraseña de usuarios de API](images/resetPW.png) para restablecer la contraseña para un ID de usuario específico. 
3. Pulse **Sí**. 
