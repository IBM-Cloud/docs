---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Filtrado de registros en Kibana
{:#kibana_filtering_logs}

En la página Descubrir, puede crear consultas de búsqueda y aplicar filtros para restringir la información que se muestra para su análisis. {:shortdesc}

* Puede definir una o varias consultas de búsqueda en la barra de búsqueda de la página Descubrir. Una consulta de búsqueda define un subconjunto de las entradas de registro.  Utilice el lenguaje de consulta Lucene para definir una consulta de búsqueda. 

* Puede añadir filtros de la *Lista de campos* o de las entradas de la tabla. Un filtro ajusta la selección de datos mediante la inclusión o exclusión de información. Puede habilitar o inhabilitar un filtro, invertir la acción de filtrado, activar y desactivar el filtro o eliminarlo por completo.  

Después de definir una nueva búsqueda, guárdela para poder utilizarla para un análisis posterior en la página Descubrir o para crear visualizaciones que puede utilizar en los paneles de control personalizados. Para obtener más información, consulte [Cómo guardar una búsqueda](logging_kibana_filtering_logs.html#k4_save_search).

Cuando realiza una nueva búsqueda, el histograma, la tabla y la lista de campos se actualizan automáticamente para mostrar los resultados de la búsqueda. Para averiguar qué datos se muestran, consulte [Identificación de los datos que se muestran en la página Descubrir](k4_identify_data.html#k4_identify_data).

En la lista siguiente se resumen algunos casos de ejemplo sobre cómo filtrar datos en los registros:

* Puede crear búsquedas personalizadas para filtrar los registros. Para obtener más información, consulte [Filtrado de registros mediante la definición de consultas personalizadas](k4_filter_queries.html#k4_filter_queries).

* Puede buscar en el registro las entradas que incluyan un determinado texto en el valor de un campo. Para obtener más información, consulte [Filtrado de registros para un determinado texto en un valor de campo](k4_filter_logs_spec_text.html#k4_filter_logs_spec_text).
 
* Puede buscar en el registro un determinado valor de campo o excluir del registro las entradas correspondientes a un valor de campo específico. Para obtener más información, consulte [Filtrado de registros para un determinado valor de campo](k4_filter_logs_spec_field.html#k4_filter_logs_spec_field).

    * Puede filtrar los registros por tipo de registro. Para obtener más información, consulte [Filtrado de registros por tipo de registro](k4_filter_logs_by_log_type.html#k4_filter_logs_by_log_type).
    * Puede filtrar los registros de la app CF por origen. Para obtener más información, consulte [Filtrado de los registros de la app CF por origen](k4_filter_logs_by_source.html#k4_filter_logs_by_source).
    * Puede filtrar los registros por ID de instancia. Para obtener más información, consulte [Filtrado de registros por ID de instancia](k4_filter_logs_by_instance_id.html#k4_filter_logs_by_instance_id).   
    * Puede filtrar los registros por tipo de mensaje. Para obtener más información, consulte [Filtrado de registros por ID de tipo de mensaje](k4_filter_cf_logs_by_msg_type.html#k4_filter_cf_logs_by_msg_type).  
 
* Puede filtrar los registros para que muestren las entradas comprendidas en un periodo de tiempo. Para obtener más información, consulte [Establecimiento de un filtro de tiempo](logging_kibana_set_time_filter.html#set_time_filter).
     

## Inicio de una nueva búsqueda
{: #k4_new_search}

Para iniciar una nueva búsqueda, pulse el botón **Nueva búsqueda** ![Nueva búsqueda](images/k4_new_search_icon.jpg "Nueva búsqueda") en la barra de herramientas de la página Descubrir. 

## Cómo guardar una búsqueda 
{: #k4_save_search}

Cuando se guarda una búsqueda, se guardan la serie de consulta de la búsqueda y el patrón de índice seleccionado actualmente. 

Siga los pasos siguientes para guardar la búsqueda actual en la página Descubrir: 

1. En la barra de herramientas de la página Descubrir, pulse el botón **Guardar búsqueda** ![Guardar búsqueda](images/k4_save_search_icon.jpg "Guardar búsqueda").

2. Escriba un nombre para la búsqueda.


3. Pulse Guardar. 

## Supresión de una búsqueda
{: #k4_delete_search}

Para suprimir una búsqueda, siga los pasos siguientes en la página Valores: 

1. En la página Valores, seleccione el separador **Objetos**. 

2. En el separador **Búsquedas**, seleccione las búsquedas que desea suprimir. 

3. Pulse **Suprimir**.


## Exportación de una búsqueda
{: #k4_export_search}

Para exportar una búsqueda, siga los pasos siguientes en la página Valores: 

1. En la página Valores, seleccione el separador **Objetos**. 

2. En el separador **Búsquedas**, seleccione las búsquedas que desea exportar. 

3. Pulse **Exportar**. 

4. Guarde el archivo.

## Importación de una búsqueda
{: #k4_import_search}

Para importar una búsqueda, siga los pasos siguientes en la página Valores: 

1. En la página Valores, seleccione el separador **Objetos**. 

2. En el separador **Búsquedas**, seleccione **Importar**.

3. Seleccione un archivo y pulse **Abrir**. 

La búsqueda se añade a la lista de búsquedas. 


## Cómo volver a cargar una búsqueda
{: #k4_reload_search}

Siga los siguientes pasos para cargar una búsqueda guardada: 

1. En la barra de herramientas de la página Descubrir, pulse el botón **Cargar búsqueda** ![Cargar búsqueda](images/k4_load_icon.jpg "Cargar búsqueda").

2. Seleccione la búsqueda que desea cargar.  


## Renovación del contenido de una búsqueda
{: #k4_refresh_search}

Para renovar de forma manual el contenido de una búsqueda, puede pulsar sobre la lupa que está disponible en la barra de búsqueda. 

Para renovar automáticamente los datos que se muestran en la página Descubrir, puede configurar un intervalo de renovación. El valor actual del intervalo de renovación se muestra en la barra de menús de la página Descubrir. De forma predeterminada, la opción para renovar automáticamente está **DESACTIVADA**.

Siga los siguientes pasos para establecer un intervalo de renovación: 

1. En la página Descubrir, pulse el **Filtro de tiempo** que está disponible en la barra de menús.

2. Pulse **Renovación automática** ![Renovación automática](images/k4_auto_refresh_icon.jpg "Renovación automática").

3. Seleccione un intervalo de renovación de la lista. 

    ![Opciones de intervalo de renovación](images/k4_change_autorefresh.jpg "Opciones de intervalo de renovación")


**Nota**: Después de habilitar un intervalo de renovación automática, puede colocarlo en pausa pulsando el botón de pausa ![Pausa](images/k4_auto_refresh_pause_icon.jpg "Pausa").




