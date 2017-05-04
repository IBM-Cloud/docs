---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Filtrado de registros por tipo de registro
{:#k4_filter_logs_by_log_type}

Vea y filtre registros de {{site.data.keyword.Bluemix}} por tipo de registro.
{:shortdesc}

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



