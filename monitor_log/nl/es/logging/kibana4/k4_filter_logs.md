---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Filtrado de registros en Kibana
{:#k4_filter_logs}

En la página Descubrir, puede crear consultas de búsqueda y aplicar filtros para restringir la información que se muestra para su análisis.
{:shortdesc}

* Puede definir una o varias consultas de búsqueda en la barra de búsqueda de la página Descubrir. Una consulta de búsqueda define un subconjunto de las entradas de registro. Utilice el lenguaje de consulta Lucene para definir una consulta de búsqueda. 

* Puede añadir filtros de la *Lista de campos* o de las entradas de la tabla. Un filtro ajusta la selección de datos mediante la inclusión o exclusión de información. Puede habilitar o inhabilitar un filtro, invertir la acción de filtrado, activar y desactivar el filtro o eliminarlo por completo. 

Después de definir una nueva búsqueda, guárdela para poder utilizarla para un análisis posterior en la página Descubrir o para crear visualizaciones que puede utilizar en los paneles de control personalizados. Para obtener más información, consulte [Cómo guardar una búsqueda](logging_kibana_filtering_logs.html#k4_save_search).

Cuando realiza una nueva búsqueda, el histograma, la tabla y la lista de campos se actualizan automáticamente para mostrar los resultados de la búsqueda. Para averiguar qué datos se muestran, consulte [Identificación de los datos que se muestran en la página Descubrir](k4_identify_data.html#k4_identify_data).

En la lista siguiente se resumen algunos casos de ejemplo sobre cómo filtrar datos en los registros:

* Puede crear búsquedas personalizadas para filtrar los registros. Para obtener más información, consulte [Filtrado de registros mediante la definición de consultas personalizadas](k4_filter_queries.html#k4_filter_queries).

* Puede buscar en el registro las entradas que incluyan un determinado texto en el valor de un campo. Para obtener más información, consulte [Filtrado de registros para un determinado texto en un valor de campo](k4_filter_logs_spec_text.html#k4_filter_logs_spec_text).
 
* Puede buscar en el registro un determinado valor de campo o excluir del registro las entradas correspondientes a un valor de campo específico. Para obtener más información, consulte [Filtrado de registros para un determinado valor de campo](k4_filter_logs_spec_field.html#k4_filter_logs_spec_field).
 
* Puede filtrar los registros para que muestren las entradas comprendidas en un periodo de tiempo. Para obtener más información, consulte [Establecimiento de un filtro de tiempo](logging_kibana_set_time_filter.html#set_time_filter).
     

## Adición de un filtro para un valor que no aparece en la *Lista de campos*
{:#k4_add_filter_out_value}

Para añadir un filtro para un valor que no se muestra en la *Lista de campos*, busque los registros que incluyen dicho valor mediante una consulta. A continuación, añada el filtro de la entrada de la tabla que está disponible en la página Descubrir. 

Siga los pasos siguientes para añadir un filtro para un valor que no está disponible en la lista que se muestra en la sección *Lista de campos*:

1. Examine la página Descubrir de Kibana para ver el subconjunto de datos que muestra. Para obtener más información, consulte [Identificación de los datos que se muestran en la página Descubrir de Kibana](logging_kibana_analize_logs_interactively.html#k4_identify_data).

    Por ejemplo, en la figura siguiente se muestran los valores de las instancias correspondientes a una app CF en la *Lista de campos*. 
    
    ![Mostrar valores en la lista de campos](images/k4_add_filter_f1.jpg "Mostrar valores en la lista de campos")
    
    Está interesado en la instancia número *3*, pero no está disponible en la lista que se ve.

2. En la página Descubrir, modifique la consulta para que busque un determinado valor de campo.

    Por ejemplo, para buscar la instancia *3*, la consulta que debe especificar es la siguiente:
   `application_id:9d222152-8834-4bab-8685-3036cd25931a AND instance_id:"3"`
    
    ![Modificar consulta](images/k4_add_filter_f2.jpg "Modificar consulta")
    
    En la tabla verá los registros que coincidan con la consulta. 
    
 3. Expanda un registro y seleccione el botón de lupa ![Botón de lupa en modalidad de inclusión](images/k4_include_field_icon.jpg "Botón de lupa en modalidad de inclusión") para añadir un filtro.
 
     Por ejemplo, para añadir un filtro para el ID de instancia con el valor *3*, pulse el botón de lupa ![Botón de lupa en modalidad de inclusión](images/k4_include_field_icon.jpg "Botón de lupa en modalidad de inclusión") que hay junto al campo *instance_id*.
     
     ![Mostrar tabla](images/k4_add_filter_f3.jpg "Mostrar tabla")
     
4. Compruebe que el filtro se ha añadido.

    Por ejemplo, la figura siguiente muestra el filtro habilitado después de añadirlo desde la tabla.
    
    ![Mostrar filtro](images/k4_add_filter_f4.jpg "Mostrar filtro")
    
    


## Filtrado de los registros correspondientes a un valor de campo específico
{:#k4_filter_logs_spec_field}

Puede buscar entradas que incluyan un determinado valor de campo. 

Siga estos pasos para buscar entradas que incluyan un determinado valor de campo:

1. Examine la página Descubrir de Kibana para ver el subconjunto de datos que muestra. Para obtener más información, consulte [Identificación de los datos que se muestran en la página Descubrir de Kibana](logging_kibana_analize_logs_interactively.html#k4_identify_data).

2. En la *Lista de campos*, identifique el campo para la que desee definir un filtro y pulse sobre el mismo.

    En el campo se muestra un máximo de 5 valores. Cada valor tiene dos botones de lupa. 
    
    Si no puede ver el valor, consulte [Adición de un filtro para un valor que no aparece en la lista de campos](k4_add_filter_out_value.html#k4_add_filter_out_value).

3. Para añadir un filtro que busque entradas con un valor de campo, seleccione el botón de lupa ![Botón de lupa en modalidad de inclusión](images/k4_include_field_icon.jpg "Botón de lupa en modalidad de inclusión") para dicho valor.

    ![Filtro que incluye el valor de campo](images/k4_add_filter_for_field.jpg "Filtro que incluye el valor de campo")

    Para añadir un filtro que busque entradas que no incluyan este valor de campo, seleccione el botón de lupa ![Botón de lupa en modalidad de inclusión](images/k4_exclude_field_icon.jpg "Botón de lupa en modalidad de inclusión") para el valor.

    ![Filtro que excluye el valor de campo](images/k4_add_filter_to_exclude_field.jpg "Filtro que excluye el valor de campo")

4. Elija una de las siguientes opciones para trabajar con filtros en Kibana:

    <table>
      <caption>Tabla 1. Métodos para trabajar con filtros</caption>
      <tbody>
        <tr>
          <th align="center">Opción</th>
          <th align="center">Descripción</th>
          <th align="center">Otra información</th>
        </tr>
        <tr>
          <td align="left">Habilitar</td>
          <td align="left">Seleccione esta opción para habilitar un filtro.</td>
          <td align="left">Cuando añade un filtro, se habilita automáticamente. <br> Si un filtro está inhabilitado, pulse sobre el mismo para habilitarlo.</td>
        </tr>
        <tr>
          <td align="left">Inhabilitar</td>
          <td align="left">Seleccione esta opción para inhabilitar un filtro.</td>
          <td align="left">Después de añadir un filtro, si desea ocultar las entradas correspondientes a un valor de campo, pulse **inhabilitar**.</td>
        </tr>
        <tr>
          <td align="left">Fijar</td>
          <td align="left">Seleccione esta opción para que el filtro se aplique en todas las páginas de Kibana.</td>
          <td align="left">Puede fijar un filtro en la página *Descubrir*, en la página *Visualizar* o en la página *Panel de control*.</td>
        </tr>
        <tr>
          <td align="left">Conmutar</td>
          <td align="left">Seleccione esta opción para conmutar un filtro.</td>
          <td align="left">De forma predeterminada, se muestran las entradas que coinciden con un filtro. Para visualizar las entradas que no coinciden, conmute el filtro.</td>
        </tr>
        <tr>
          <td align="left">Eliminar</td>
          <td align="left">Seleccione esta opción para eliminar un filtro.</td>
          <td align="left"></td>
        </tr>
      </tbody>
    </table>

## Filtrado de los registros de una app CF por origen
{:#k4_filter_logs_by_source}

Siga estos pasos para buscar entradas que incluyan un determinado origen de registro:

1. Examine la página Descubrir de Kibana para ver el subconjunto de datos que muestra. Para obtener más información, consulte [Identificación de los datos que se muestran en la página Descubrir de Kibana](logging_kibana_analize_logs_interactively.html#k4_identify_data).

2. En la *Lista de campos*, seleccione el campo **source_id**.

    ![Lista de filtros que muestra el campo source_id](images/k4_filter_sourceid_F1.jpg "Lista de filtros que muestra el campo source_id")     

3. Para añadir un filtro que busque las entradas que incluyan un determinado source_id, seleccione el botón de lupa ![Botón de lupa en modalidad de inclusión](images/k4_include_field_icon.jpg "Botón de lupa en modalidad de inclusión") para dicho valor.

    Para obtener una lista de orígenes de registro que están disponibles para apps CF, consulte [Orígenes de registro para apps CF](../logging_cf_apps.html#logging_bluemix_cf_apps_log_sources).

    Por ejemplo, para añadir un filtro que incluya las entradas de registro sobre el inicio, detención o caída de una aplicación CF, seleccione el botón de lupa ![Botón de lupa en modalidad de inclusión](images/k4_include_field_icon.jpg "Botón de lupa en modalidad de inclusión") que está disponible para el valor *CELL* en la sección *Lista de campos*. En la figura siguiente se muestra el filtro para el valor de source_id *CELL* habilitado.
    
    ![Filtro que incluye el valor de campo](images/k4_filter_sourceid_F2.jpg "Filtro que incluye el valor de campo")

    Para añadir un filtro que busque las entradas que no incluyan un determinado source_id, elija el botón de lupa ![Botón de lupa en modalidad de exclusión](images/k4_exclude_field_icon.jpg "Botón de lupa en modalidad de exclusión") para el valor.
    
    Por ejemplo, para añadir un filtro que excluya las entradas de registro sobre el inicio, detención o caída de una aplicación CF, seleccione el botón de lupa ![Botón de lupa en modalidad de inclusión](images/k4_exclude_field_icon.jpg "Botón de lupa en modalidad de inclusión") que está disponible para el valor *CELL* en la sección *Lista de campos*. La figura siguiente muestra el filtro que excluye entradas para el valor de source_id *CELL*.

    ![Filtro que excluye el valor de campo](images/k4_filter_sourceid_F3.jpg "Filtro que excluye el valor de campo")


## Filtrado de registros por tipo de registro
{:#k4_filter_logs_by_log_type}

Siga estos pasos para buscar entradas que incluyan un determinado tipo de registro:

1. Examine la página Descubrir de Kibana para ver el subconjunto de datos que muestra. Para obtener más información, consulte [Identificación de los datos que se muestran en la página Descubrir de Kibana](logging_kibana_analize_logs_interactively.html#k4_identify_data).

2. En la *Lista de campos*, seleccione el campo **type**.

    Por ejemplo, en la figura siguiente, solo hay un tipo de registro disponible: *syslog*
    
    ![Lista de filtros que se muestra el tipo de registro del campo](images/k4_filter_log_type_F1.jpg "Lista de filtros que muestra el tipo de registro del campo")
   
3. Para añadir un filtro que busque un determinado tipo de registro, seleccione el botón de lupa ![Botón de lupa en modalidad de inclusión](images/k4_include_field_icon.jpg "Botón de lupa en modalidad de inclusión") para el tipo de registro que desea analizar.

    Por ejemplo, para añadir un filtro que incluya las entradas de registro correspondientes a *syslog*, seleccione el botón de lupa ![Botón de lupa en modalidad de inclusión](images/k4_include_field_icon.jpg "Botón de lupa en modalidad de inclusión") que está disponible para el valor *syslog* en la sección *Lista de campos*. La figura siguiente muestra el filtro que incluye entradas para el tipo de registro *syslog*.

    ![Filtro que incluye entradas de tipo de registro para syslog](images/k4_filter_log_type_F2.jpg "Filtro que incluye entradas de tipo de registro para syslog")

    Para añadir un filtro que busque las entradas que no incluyan un determinado tipo de registro, seleccione el botón de lupa ![Botón de lupa en modalidad de exclusión](images/k4_exclude_field_icon.jpg "Botón de lupa en modalidad de exclusión") para el valor.

     Por ejemplo, para añadir un filtro que excluya las entradas de registro para *syslog*, seleccione el botón de lupa ![Botón de lupa en modalidad de exclusión](images/k4_exclude_field_icon.jpg "Botón de lupa en modalidad de exclusión") que está disponible para el valor *syslog* en el *Lista de campos* sección.. La figura siguiente muestra el filtro que excluye entradas para el tipo de registro *syslog*.
     
     ![Filtro que excluye las entradas de tipo de registro para syslog](images/k4_filter_log_type_F3.jpg "Filtro que excluye las entradas de tipo de registro para syslog")


## Filtrado de registros por ID de instancia
{:#k4_filter_logs_by_instance_id}

Siga estos pasos para ver y filtrar los registros por ID de instancia en el panel de control de Kibana:

1. Examine la página Descubrir de Kibana para ver el subconjunto de datos que muestra. Para obtener más información, consulte [Identificación de los datos que se muestran en la página Descubrir de Kibana](logging_kibana_analize_logs_interactively.html#k4_identify_data).

2. En la *Lista de campos*, seleccione uno de los siguientes campos para buscar un determinado ID de instancia:

    * **instance_ID**: Este campo muestra los distintos ID de instancia disponibles en el registro para una aplicación Cloud Foundry. 
    * **instance**: Este campo muestra los distintos GUID de todas las instancias correspondientes a un grupo de contenedores. 

    Por ejemplo, en la figura siguiente se muestran distintos valores de instancias para una app CF:
    
    ![Lista de filtros que muestra el campo instance_id](images/k4_filter_instanceid_f1.jpg "Lista de filtros que muestra el campo instance_id")
   
3. Para añadir un filtro que busque un determinado tipo de registro, seleccione el botón de lupa ![Botón de lupa en modalidad de inclusión](images/k4_include_field_icon.jpg "Botón de lupa en modalidad de inclusión") para el tipo de registro que desea analizar.

   Por ejemplo, para añadir un filtro que incluya las entradas para la instancia de app CD *2*, seleccione el botón de lupa ![Botón de lupa en modalidad de inclusión](images/k4_include_field_icon.jpg "Botón de lupa en modalidad de inclusión") que está disponible para el valor *2* en la sección Lista de campos. La figura siguiente muestra el filtro que incluye entradas para la instancia *2*.
    
    ![Filtro que incluye entradas de instance_id para la instancia 2](images/k4_filter_instanceid_f2.jpg "Filtro que incluye entradas de instance_id para la instancia 2")

    Para añadir un filtro que busque las entradas que no incluyan un determinado ID de instancia, seleccione el botón de lupa ![Botón de lupa en modalidad de exclusión](images/k4_exclude_field_icon.jpg "Botón de lupa en modalidad de exclusión") para el valor.

     Por ejemplo, para añadir un filtro que excluye entradas para la instancia de app CF *2*, seleccione el botón de lupa ![Botón de lupa en modalidad de exclusión](images/k4_exclude_field_icon.jpg "Botón de lupa en modalidad de exclusión") disponible para el valor *2* en la sección Lista de campos. La figura siguiente muestra el filtro que excluye entradas para la instancia *2*.
     
      ![Filtro que excluye entradas de instance_id para la instancia 2](images/k4_filter_instanceid_f3.jpg "Filtro que excluye entradas de instance_id para la instancia 2")


## Filtrado de registros de la app CF por tipo de mensaje
{:#k4_filter_cf_logs_by_msg_type}

Siga estos pasos para buscar entradas que incluyan un determinado tipo de mensaje:

1. Examine la página Descubrir de Kibana para ver el subconjunto de datos que muestra. Para obtener más información, consulte [Identificación de los datos que se muestran en la página Descubrir de Kibana](logging_kibana_analize_logs_interactively.html#k4_identify_data).

2. En la *Lista de campos*, seleccione el campo **message_type**.

    En la figura siguiente se muestran los valores del campo *message_type* en los registros de una app CF:
    
    ![Lista de filtros que muestra el campo message_type](images/k4_filter_by_msg_type_f1.jpg "Lista de filtros que muestra el campo message_type")     

3. Para añadir un filtro que busque las entradas que incluyan un determinado *message_type*, seleccione el botón de lupa ![Botón de lupa en modalidad de inclusión](images/k4_include_field_icon.jpg "Botón de lupa en modalidad de inclusión") para dicho valor.

    Por ejemplo, para añadir un filtro que incluya las entradas de registro que tengan el valor de message_type *OUT*, seleccione el botón de lupa ![Botón de lupa en modalidad de inclusión](images/k4_include_field_icon.jpg "Botón de lupa en modalidad de inclusión") que está disponible para el valor *OUT* en la sección *Lista de campos*. En la figura siguiente se muestra el filtro para el valor de message_type *OUT* habilitado.
    
    ![Filtro que incluye el valor de campo](images/k4_filter_by_msg_type_f2.jpg "Filtro que incluye el valor de campo")

    Para añadir un filtro que busque las entradas que no incluyan un determinado *message_type*, elija el botón de lupa ![Botón de lupa en modalidad de exclusión](images/k4_exclude_field_icon.jpg "Botón de lupa en modalidad de exclusión") para el valor.
    
    Por ejemplo, para añadir un filtro que excluye las entradas del registro para el message_type *OUT*, seleccione el botón de lupa ![Botón de lupa en modalidad de inclusión](images/k4_exclude_field_icon.jpg "Botón de lupa en modalidad de inclusión") que está disponible para el valor *CELL* en la *Lista de campos* sección.. La figura siguiente muestra el filtro que excluye entradas para el valor de message_type *OUT*.

    ![Filtro que excluye el valor de campo](images/k4_filter_by_msg_type_f3.jpg "Filtro que excluye el valor de campo")


## Filtrado de los registros correspondientes a un texto específico en un valor de campo
{:#k4_filter_logs_spec_text}

Vea y busque entradas que incluyan un texto específico en el valor de un campo. 

**Aviso:** Solo puede realizar una búsqueda de texto libre de campos de serie de caracteres que analice en analizador Elasticsearch. 
    
Cuando Elasticsearch analiza el campo valor de una serie, divide el texto en límites de palabras, según lo establecido por el consorcio Unicode, y elimina los signos de puntuación y las minúsculas en todas las palabras.
    
Siga estos pasos para buscar entradas que incluyan un determinado texto en un valor de campo:

1. Examine la página Descubrir de Kibana para ver el subconjunto de datos que muestra. Para obtener más información, consulte [Identificación de los datos que se muestran en la página Descubrir de Kibana](logging_kibana_analize_logs_interactively.html#k4_identify_data).

2. Identifique los campos que se analizan en ElasticSearch de forma predeterminada.

    Para ver la lista completa de campos analizados que están disponibles para buscar y filtrar datos de registro, [vuelva a cargar la lista de campos](logging_kibana_analize_logs_interactively.html#kibana_discover_view_reload_fields). A continuación, en la *Lista de campos* disponible en la página Descubrir, siga los pasos siguientes:
    
    1. Pulse el icono de configuración ![Icono de configuración](images/k4_configure_icon.jpg "Icono de configuración"). Se muestra la sección **Campos seleccionados**, donde puede filtrar los campos.

        ![Sección Configuración que muestra campos con determinados atributos](images/k4_reset_filters.jpg "Sección Configuración que muestra campos con determinados atributos")
    
    2. Para identificar los campos que se analizan, seleccione **Sí** en el campo de búsqueda **Analizado**.

        ![Atributo analizado](images/k4_reset_filters_analyze_options.jpg "Atributo analizado")
    
        Se muestra la lista de campos analizados.
    
        ![Lista de campos analizados](images/k4_list_analyzed_fields.jpg "Lista de campos analizados")
        
         
    3. Compruebe si el campo en el que desea buscar texto libre es un campo analizado por ElasticSearch de forma predeterminada.
    
3. Si es un campo analizado, modifique la consulta para buscar las entradas en los registros que incluyan dicho texto libre como parte del valor de un campo.

    
**Ejemplo**

Si inicia Kibana para una aplicación Cloud Foundry (CF) desde la IU de {{site.data.keyword.Bluemix}} y desea buscar un determinado mensaje que incluya el ID de mensaje *CWWKT0016I:*, modifique la búsqueda para que incluya el texto libre.
    
1. Compruebe la consulta de búsqueda que se carga y los datos que se muestran en la página Descubrir.
       
    ![Consulta de búsqueda predeterminada](images/k4_filter_by_text_default_query.jpg "Consulta de búsqueda predeterminada")
        
2. Para buscar el ID de mensaje *CWWKT0016I*, modifique la consulta de búsqueda y pulse **Intro**:
    
    <pre class="pre">application_id:f52f6016-3aab-4b5c-aa2e-5493747cb978 AND message:"CWWKT0016I:" </pre>
        
    ![Modificar la consulta](images/k4_filter_by_text_modify_query.jpg "Modificar la consulta")
      
La tabla muestra las entradas de la app CF en las que el texto *CWWKT0016I* forma parte del valor del campo *Mensaje*.
    
![Nueva vista de búsqueda](images/k4_filter_by_text_result_query.jpg "nueva vista de búsqueda")     	
        

## Establecimiento de un filtro de tiempo
{: #set_time_filter}

Vea y filtre registros de {{site.data.keyword.Bluemix_notm}} comprendidos en un periodo de tiempo configurando el *Selector de tiempo*.

Puede configurar el *Selector de tiempo* en la página Descubrir. De forma predeterminada, está establecido en los últimos 15 minutos. 

Siga estos pasos para buscar entradas que incluyan un determinado tiempo:

1. En la barra de menús de la página Descubrir, pulse Selector de tiempo ![Selector de tiempo](images/k4_time_picker_icon.jpg "Selector de tiempo").

2. Configure el intervalo de tiempo. 

    Puede definir cualquiera de los siguientes tipos de intervalos de tiempo:
    
    * Rápido: son intervalos de tiempo predefinidos que incluyen los casos más comunes de los intervalos de tiempo Relativo y Absoluto; por ejemplo *Hoy* y *Este mes*. 
    
        ![Opciones rápidas del Selector de tiempo](images/k4_time_picker_quick.jpg "Opciones rápidas del Selector de tiempo")
    
    * Relativo: son intervalos de tiempo en los que puede especificar la fecha y hora de inicio y la fecha y hora final. Las puede redondear por hora.
    
        ![Opciones relativas del Selector de tiempo](images/k4_time_picker_relative.jpg "Opciones relativas del Selector de tiempo")
    
    * Absoluto: son intervalos de tiempo entre una fecha inicial y una fecha final.
    
        ![Opciones relativas del Selector de tiempo](images/k4_time_picker_absolute.jpg "Opciones absolutas del Selector de tiempo")
      

Después de configurar un intervalo de tiempo, los datos que aparecen en Kibana corresponden a las entradas comprendidas en dicho rango de tiempo.








