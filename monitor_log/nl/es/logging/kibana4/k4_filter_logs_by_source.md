---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Filtrado de los registros de una app CF por origen
{:#k4_filter_logs_by_source}

Vea y filtre por tipo de origen los registros de una aplicación Cloud Foundry mediante el panel de control.
{:shortdesc}

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




