---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Análisis de registro en Kibana mediante un panel de control
{:#kibana_analize_logs_dashboard}

Utilice el *Panel de control* de Kibana para visualizar recopilaciones de visualizaciones agrupadas en los paneles de control. Utilice los paneles de control para analizar los datos de registro y comparar resultados.
{:shortdesc}

En {{site.data.keyword.Bluemix}} hay diferentes tipos de paneles de control que puede definir y personalizar para visualizar y analizar los datos. Por ejemplo, en la siguiente tabla se muestran algunos de los tipos de paneles de control más comunes:

| Tipo de panel de control | Descripción |
|-------------------|-------------|
| Panel de control Single-cf-app | Es un panel de control que muestra información correspondiente a una sola aplicación Cloud Foundry. |
| Panel de control Contenedor único  | Es un panel de control que muestra información correspondiente a un solo contenedor.  |
| Panel de control Grupo de contenedores  | Es un panel de control que muestra información correspondiente a un determinado grupo de contenedores.  |
| Panel de control Multi-cf-app | Es un panel de control que muestra información correspondiente a todas las aplicaciones Cloud Foundry desplegadas en el mismo espacio de {{site.data.keyword.Bluemix_notm}}.  | 
| Panel de control multicontenedor | Es un panel de control que muestra información correspondiente a todos los contenedores desplegados en el mismo espacio de {{site.data.keyword.Bluemix_notm}}.  |
| Panel de control Espacio | Este es un panel de control que muestra datos de registro disponibles en un espacio de {{site.data.keyword.Bluemix_notm}}.  | 
{: caption="Tabla 1. Ejemplos de tipos de paneles de control" caption-side="top"}

Para visualizar los datos de un panel de control, puede configurar paneles. Kibana incluye distintas visualizaciones, como tabla, tendencias e histograma, que puede utilizar para analizar la información. Una visualización se añade como un panel a un panel de control. Puede añadir, eliminar y cambiar la disposición de los paneles del panel de control. El objetivo de cada panel varía. Algunos paneles se organizan en filas que proporcionan los resultados de una o varias consultas. Otros paneles muestran documentos o información personalizada. Cada panel se basa en una búsqueda. La búsqueda define el subconjunto de datos que muestra el panel. Por ejemplo, puede configurar un diagrama de barras, un diagrama circular o una tabla para visualizar los datos y analizarlos.  

En la tabla siguiente se muestran las diferentes tareas que puede llevar a cabo en la página Panel de control:

| Tarea | Más información |
|------|------------------|
| [Crear un nuevo panel de control](logging_kibana_analize_logs_dashboard.html#K4_dashboard_new) | Puede crear varios paneles de control. Cada panel de control se puede diseñar de modo que incluya distintas búsquedas, visualizaciones y un subconjunto diferente de datos de registro.  |
| [Guardar un panel de control](logging_kibana_analize_logs_dashboard.html#k4_dashboard_save) | Puede guardar un panel de control para reutilizarlo en el futuro. |
| [Cargar un panel de control](logging_kibana_analize_logs_dashboard.html#k4_dashboard_reload) | Puede cargar un panel de control para actualizar sus datos, modificarlo o analizar los datos. |
| [Suprimir un panel de control](logging_kibana_analize_logs_dashboard.html#k4_dashboard_delete) | Suprima los paneles de control que ya no necesite. |
| [Exportar un panel de control](logging_kibana_analize_logs_dashboard.html#k4_dashboard_export) | Puede exportar un panel de control como archivo JSON. |
| [Importar un panel de control](logging_kibana_analize_logs_dashboard.html#k4_dashboard_import) | Puede importar un panel de control como archivo JSON. |
| [Compartir un panel de control](logging_kibana_analize_logs_dashboard.html#k4_dashboard_share) | Puede compartir un panel de control a través de su fuente HTML o a través del panel de control de Kibana. |
| [Añadir una visualización](logging_kibana_analize_logs_dashboard.html#k4_dashboard_add_visualization) | Puede añadir una visualización existente o una búsqueda a un panel de control.|
{: caption="Tabla 2. Tareas para trabajar con paneles de control" caption-side="top"}

Para obtener más información sobre Kibana, consulte la [Guía del usuario de Kibana ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.

## Adición de una nueva búsqueda o visualización
{: #k4_dashboard_add_visualization}

Siga estos pasos para añadir una visualización o búsqueda existente:

1. En la barra de herramientas de la página Panel de control, pulse el botón **Añadir visualización** botón ![Añadir visualización](images/k4_dash_add_visualization_icon.jpg "Añadir visualización").

    **Nota**: Puede añadir visualizaciones y búsquedas. 

2. Seleccione el separador **Visualizaciones** para añadir una visualización o seleccione el separador **Búsquedas** para añadir una búsqueda.

3. Pulse sobre la búsqueda o visualización que desee añadir.

    Se añade al panel de control un panel correspondiente a la búsqueda o visualización.

## Creación de un nuevo panel de control de Kibana
{: #K4_dashboard_new}

Siga los siguientes pasos para crear un nuevo panel de control:

1. En la barra de herramientas de la página Panel de control, pulse el botón **Nuevo panel de control** ![Nuevo panel de control](images/k4_dash_new_icon.jpg "Nuevo panel de control").

2. Añada una o varias búsquedas y visualizaciones. Para obtener más información, consulte [Adición de una nueva búsqueda o visualización](logging_kibana_analize_logs_dashboard.html#K4_dashboard_add_visualization).

    Cuando añade una búsqueda o una visualización, se añade un panel al panel de control.

3. Arrastre un panel y suéltelo en la parte del panel de control en el que lo desea colocar.
 
4. Guarde el panel de control para su reutilización en el futuro. Para obtener más información, consulte [Cómo guardar un panel de control de Kibana](logging_kibana_analize_logs_dashboard.html#k4_dashboard_save).

## Supresión de un panel de control de Kibana
{: #k4_dashboard_delete}

Para suprimir una visualización, siga los pasos siguientes en la página Valores:

1. En la página Valores, seleccione el separador **Objetos**.

2. En el separador **Visualizaciones**, seleccione las visualizaciones que desea suprimir.

3. Pulse **Suprimir**.

## Exportación de un panel de control de Kibana
{: #k4_dashboard_export}

Para exportar un panel de control como archivo JSON, siga los pasos siguientes en la página Valores:

1. En la página Valores, seleccione el separador **Objetos**.

2. En el separador **Panel de control**, seleccione el panel de control que desea exportar.

3. Pulse **Exportar**.

4. Guarde el archivo.

## Importación de un panel de control de Kibana
{: #k4_dashboard_import}

Para importar un panel de control como archivo JSON, siga los pasos siguientes en la página Valores:

1. En la página Valores, seleccione el separador **Objetos**.

2. En el separador **Panel de control**, seleccione **Importar**.

3. Seleccione un archivo y pulse **Abrir**.

El panel de control se añade a la lista de paneles de control.

## Carga de un panel de control de Kibana
{: #k4_dashboard_reload}

Siga los siguientes pasos para cargar un nuevo panel de control guardado:

1. En la barra de herramientas de la página Panel de panel de control, pulse el botón **Cargar panel de control guardado** ![Cargar panel de control guardado](images/k4_dash_load_icon.jpg "Cargar panel de control guardado").

2. Seleccione el panel de control que desea cargar. 

## Cómo guardar un panel de control de Kibana
{: #k4_dashboard_save}

Siga los pasos siguientes para guardar un panel de control de Kibana después de personalizarlo:

1. En la barra de herramientas, pulse el botón **Guardar** ![Guardar panel de control](images/k4_dash_save_icon.jpg "Guardar panel de control").

2. Escriba un nombre para el panel de control.

    **Nota:** si intenta guardar un panel de control con un nombre que contenga espacios en blanco, no se guardará.

3. Junto al campo de nombre, pulse el icono **Guardar**.

## Compartición de un panel de control de Kibana
{: #k4_dashboard_share}

Siga los siguientes pasos para compartir un panel de control:

1. En la barra de herramientas de la página Panel de control, pulse el botón **Compartir panel de control** ![Compartir panel de control](images/k4_dash_share_icon.jpg "Compartir panel de control").

2. Seleccione una de las acciones siguientes:

    * **Incorporar este panel de control**: Selecciones esta opción para compartir el panel de control a través del HTML de origen. 
    
        Pulse el botón de copia ![Copiar en portapapeles](images/k4_copy_to_clipboard.jpg "Copiar en portapapeles") para copiar el código HTML que puede utilizar para incorporar el panel de control en el HTML de origen. 
        
        **Nota**: Para ver el panel de control, los usuarios deben poder acceder a Kibana.
	
    * **Compartir un enlace**: Seleccione esta opción para compartir el panel de control en Kibana con otros usuarios.



