---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-08"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Análisis de registros en Kibana mediante visualizaciones 
{:#logging_kibana_visualizations}

Utilice la página *Visualizar* de Kibana para crear visualizaciones, como gráficos y tablas, que puede utilizar para analizar los datos de registro y comparara los resultados. {:shortdesc}

Puede utilizar una visualización de forma individual para analizar los registros. 

* Puede crear visualizaciones a partir de una búsqueda que defina y guarde en la página *Descubrir* o a partir de una nueva consulta que defina en la página *Visualizar*. La búsqueda define el subconjunto de datos que muestra una visualización. 

* El tipo de visualización que elija determina cómo se visualizan los datos para su análisis.

En la tabla siguiente encontrará los distintos tipos de visualizaciones: 

| Tipo de visualización | Descripción |
|-----------------------|-------------|
| Gráfico de áreas | Muestra gráficamente datos cuantitativos. Utilícelo para comparar dos o más conjuntos de datos agregados. |
| Tabla de datos | Muestra datos sin formato en formato de tabla para una agregación compuesta. |
| Gráfico de líneas | Muestra los datos que se basan en tiempo. Utilícelo para comparar dos o más conjuntos de datos agregados basados en tiempo. |
| Widget Markdown | Utilícelo para ver información de texto.  |
| Métrica | Utilícelo para ver un recuento de aciertos o el promedio exacto de un campo numérico. |
| Gráfico circular | Utilícelo para ver los distintos valores de un campo.  | 
| Gráfico de barras verticales | Muestra datos basados en tiempo y datos que no se basan en tiempo. Utilícelo para agrupar datos.  |

En la página Visualizar, puede realizar cualquiera de las siguientes tareas: 

| Tarea | Más información |
|------|------------------|
| [Crear una nueva visualización](logging_kibana_visualizations.html#logging_k4_visualizations_create) | Puede crear visualizaciones a partir de una búsqueda que defina y guarde en la página *Descubrir* o a partir de una nueva consulta que defina en la página *Visualizar*.  |
| [Guardar una visualización](logging_kibana_visualizations.html#logging_kibana_visualizations_save) | Puede guardar visualizaciones para reutilizarlas en el futuro.  |
| [Cargar una visualización](logging_kibana_visualizations.html#logging_kibana_visualizations_reload) | Puede cargar una visualización para actualizar sus datos, modificarlos o analizar los datos. |
| [Suprimir una visualización](logging_kibana_visualizations.html#logging_kibana_visualizations_delete) | Suprima las visualizaciones que ya no necesite.  |
| [Exportar una visualización](logging_kibana_visualizations.html#logging_kibana_visualizations_export) | Puede exportar una visualización como archivo JSON.   |
| [Importar una visualización](logging_kibana_visualizations.html#logging_kibana_visualizations_import) | Puede importar una visualización como archivo JSON.   |
| [Compartir una visualización](logging_kibana_visualizations.html#logging_kibana_visualizations_share) | Puede compartir una visualización a través de su HTML de origen o a través del panel de control de Kibana.  |


## Creación de visualizaciones a partir de consultas en Kibana
{:#logging_k4_visualizations_create}

Complete los siguientes pasos para crear una visualización desde la página Visualizar: 

1. Inicie Kibana y seleccione la página **Visualizar**. 

2. Cree una nueva visualización. En la barra de herramientas, pulse el botón **Nueva visualización** ![Nueva visualización](images/k4_visualization_new_icon.jpg "Nueva visualización").

3. Seleccione una visualización. 
    
4. Seleccione uno origen de búsqueda. Elija una de estas opciones:

    * Pulse **Desde una nueva búsqueda**.
    * Pulse **Desde una búsqueda guardada**. 
  
5. Configure la consulta. 

    * Si selecciona **Desde una búsqueda guardada**, seleccione una consulta de búsqueda. La consulta se utiliza para recuperar los datos que se utilizan para la visualización. 

        Después de seleccionar una búsqueda, se abre el programa de creación de visualizaciones y carga los datos correspondientes a la consulta seleccionada. Aparece el mensaje siguiente: *Esta visualización está enlazada a una búsqueda guardada: your_search_name*. 
	
	**Nota**: los cambios que realice en una búsqueda guardada se reflejan automáticamente en la visualización. Para inhabilitar las actualizaciones automáticas que realice en la consulta que está enlazada a esta visualización, efectúe una doble pulsación en el mensaje *Esta visualización está enlazada a una búsqueda guardada: your_search_name* 

    * Si selecciona **Desde una nueva búsqueda**, defina una consulta nueva. La consulta se utiliza para definir el subconjunto de datos que recupera y utiliza la visualización.

        Para obtener más información, consulte [Filtrado de registros mediante la definición de consultas personalizadas](k4_filter_queries.html#k4_filter_queries).

6. En el programa de creación de visualizaciones, seleccione agregaciones de métricas para el eje Y.

7. En el programa de creación de visualizaciones, seleccione un tipo de receptáculo. Luego seleccione una agregación de receptáculo. 
  
8. Añada subreceptáculos para desglosar los datos. 

Para obtener más información sobre Kibana, consulte la [Guía del usuario de Kibana![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.
 
## Cómo guardar una visualización
{:#logging_kibana_visualizations_save}

Siga los pasos siguientes para guardar una visualización en la página Visualizar: 

1. En la barra de herramientas de la página Visualizar, pulse el botón **Guardar visualización** ![Guardar visualización](images/k4_visualization_save_icon.jpg "Guardar visualización").

2. Escriba un nombre para la visualización. 

3. Pulse Guardar. 

## Carga de una visualización
{:#logging_kibana_visualizations_reload}

Siga los siguientes pasos para cargar una visualización guardada: 

1. En la barra de herramientas de la página Visualizar, pulse el botón **Cargar visualización guardada** ![Cargar visualización guardada](images/k4_visualization_open_icon.jpg "Cargar visualización guardada").

2. Seleccione la visualización que desea cargar.  



## Supresión de una visualización
{:#logging_kibana_visualizations_delete}

Para suprimir una visualización, siga los pasos siguientes en la página Valores: 

1. En la página Valores, seleccione el separador **Objetos**. 

2. En el separador **Visualizaciones**, seleccione las visualizaciones que desea suprimir. 

3. Pulse **Suprimir**.


## Exportación de una visualización
{:#logging_kibana_visualizations_export}

Para exportar una visualización como archivo JSON, siga los pasos siguientes en la página Valores: 

1. En la página Valores, seleccione el separador **Objetos**. 

2. En el separador **Visualizaciones**, seleccione la visualización que desea exportar. 

3. Pulse **Exportar**. 

4. Guarde el archivo.

## Importación de una visualización
{:#logging_kibana_visualizations_import}

Para importar una visualización como archivo JSON, siga los pasos siguientes en la página Valores: 

1. En la página Valores, seleccione el separador **Objetos**. 

2. En el separador **Visualizaciones**, seleccione **Importar**.

3. Seleccione un archivo y pulse **Abrir**. 

La visualización se añade a la lista de visualizaciones. 


## Cómo compartir una visualización
{:#logging_kibana_visualizations_share}

Siga los pasos siguientes para compartir una visualización en la página Visualizar: 

1. En la barra de herramientas de la página Visualizar, pulse el botón **Compartir visualización** ![Compartir visualización](images/k4_visualization_share_icon.jpg "Compartir visualización").

2. Seleccione una de las acciones siguientes:

    * **Incorporar esta visualización**: Selecciones esta opción para compartir la visualización a través del HTML de origen.  
    
        Pulse el botón de copia ![Copiar en portapapeles](images/k4_copy_to_clipboard.jpg "Copiar en portapapeles") para copiar el código HTML que puede utilizar para incorporar la visualización en el HTML de origen.  
	
	**Nota**: Para ver la visualización, los usuarios deben poder acceder a Kibana.
	
    * **Compartir un enlace**: Seleccione esta opción para compartir la visualización en Kibana con otros usuarios.



