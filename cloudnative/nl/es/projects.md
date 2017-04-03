---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Proyectos
{: #projects}

La {{site.data.keyword.dev_console}} de {{site.data.keyword.Bluemix}} combina la interfaz de usuario, los datos y los servicios de la aplicación en un *proyecto* completo. Al crear un proyecto, se mantienen todas las partes necesarias de la aplicación y las prestaciones añadidas en el servidor de {{site.data.keyword.Bluemix_notm}}. Puede descargar el código de la app y las credenciales e iniciadores necesarios si los servicios están configurados en su proyecto. Puede ver todos sus proyectos seleccionando **Proyectos**.  

Para ver más información sobre un determinado proyecto, selecciónelo en la página **Proyectos**. Se abrirá la página **Visión general del proyecto**, que incluye los servicios configurados y disponibles para el proyecto. Los servicios son prestaciones independientes que amplían la aplicación añadiendo una función. Debido a que se añaden individualmente, puede añadir los servicios que necesite, como los servicios push, de autenticación, datos y almacenamiento, entre otros. Cuando añade un servicio al proyecto en la página **Visión general del proyecto** y sigue las instrucciones para configurarlo, se asocia automáticamente a la app. Para obtener más información sobre la página Visión general del proyecto, consulte la [página Visión general del proyecto](project_overview_page.html).

Para crear el proyecto, debe seleccionar un [patrón](patterns.html), seguido por un [iniciador](starters.html).


## Página Visión general del proyecto
{: #project_overview}

Puede ver y trabajar con un único proyecto de la {{site.data.keyword.dev_console}} de {{site.data.keyword.Bluemix}} seleccionando el proyecto en la página **Proyectos**, que abre la página Visión general del proyecto.
{: shortdesc}

La página **Visión general del proyecto** muestra un mosaico de cada prestación configurada o disponible para que se configure con el proyecto seleccionado. El mosaico muestra el tipo de prestación y un botón *acciones* con tres puntos alineados en vertical. Ejemplos de prestaciones que podrían estar disponibles o configuradas son {{site.data.keyword.mobilepushshort}}, Analytics, o Data and Storage. Las prestaciones compatibles dependen del tipo de proyecto y de las prestaciones disponibles en la región, de modo que no todas las prestaciones estarán disponibles para que se asocien con todos los proyectos.  

Cuando un tipo de prestación aún no está asociada al proyecto, se muestra el botón **Crear** en el mosaico. Las opciones del botón de acciones sirven para crear una instancia del servicio o para añadir una instancia de servicio existente cuando la prestación aún no está asociada. Si se selecciona **Añadir existentes**, se muestra una lista de instancias de servicio de dicho tipo en su espacio.

Si la prestación ya está asociada a este proyecto, el nombre de la instancia del servicio asociado se muestra en el mosaico tras el tipo de prestación. Esto facilita la búsqueda de la instancia de servicio relacionada con el proyecto en la {{site.data.keyword.dev_console}}. Las acciones que están disponibles en el botón de acciones son **Ver** y **Eliminar** cuando el servicio ya está asociado al proyecto. Cuando se elimina una instancia de servicio solo se elimina la asociación a este proyecto; no se suprime la instancia del servicio de la {{site.data.keyword.dev_console}}. Para suprimir una instancia de servicio, pulse la página **Web y móvil > Servicios** para ver y suprimir las instancias de servicio.

Seleccione **Obtener el código** en el mosaico **Código** para descargar el código correspondiente al proyecto. Para obtener más información sobre cómo descargar el código, consulte [Obtener código](get_code.html).


## Actualización del proyecto para utilizar un nuevo Iniciador
{: #update-starter}

1. Desde la página **Proyectos** o **Visión general del proyecto**, pulse el icono **Menú de desbordamiento** y seleccione **Actualizar iniciador**.

2. Elija un nuevo iniciador y pulse **Actualizar**.

3. Pulse **Obtener el código** en la página **Visión general del proyecto** para seleccionar el lenguaje.

   Como alternativa, pulse la página **Código**.


## Actualización del proyecto para generar un nuevo lenguaje
{: #update-language}

1. Desde las páginas **Proyectos** o **Visión general del proyecto**, pulse el icono **Menú de desbordamiento** y seleccione **Actualizar iniciador**.

2. Seleccione un nuevo lenguaje y pulse **Actualizar**.

3. Pulse **Obtener el código** en la página **Visión general del proyecto** para seleccionar el lenguaje.
