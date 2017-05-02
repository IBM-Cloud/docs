---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Filtrado de registros de la app CF por tipo de mensaje
{:#k4_filter_cf_logs_by_msg_type}

Puede ver y filtrar registros de Cloud Foundry por tipo de mensaje en Kibana.{:shortdesc}


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

