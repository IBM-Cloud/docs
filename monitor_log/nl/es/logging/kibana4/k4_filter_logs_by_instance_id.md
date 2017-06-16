---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Filtrado de registros por ID de instancia
{:#k4_filter_logs_by_instance_id}

Vea y filtre registros de {{site.data.keyword.Bluemix}} por ID de instancia.
{:shortdesc}

Siga estos pasos para ver y filtrar los registros por ID de instancia en el panel de control de Kibana:

1. Examine la página Descubrir de Kibana para ver el subconjunto de datos que muestra. Para obtener más información, consulte [Identificación de los datos que se muestran en la página Descubrir de Kibana](logging_kibana_analize_logs_interactively.html#k4_identify_data). 

2. En la *Lista de campos*, seleccione uno de los siguientes campos para buscar un determinado ID de instancia: 

    * **instance_ID**: Este campo muestra los distintos ID de instancia disponibles en el registro para una aplicación Cloud Foundry.  
    * **instance**: Este campo muestra los distintos GUID de todas las instancias correspondientes a un grupo de contenedores.  

    Por ejemplo, en la figura siguiente se muestran distintos valores de instancias para una app CF: 
    
    ![Lista de filtros que muestra el campo instance_id](images/k4_filter_instanceid_f1.jpg "Lista de filtros que muestra el campo instance_id")
   
3. Para añadir un filtro que busque un determinado tipo de registro, seleccione el botón de lupa ![Botón de lupa en modalidad de inclusión](images/k4_include_field_icon.jpg "Botón de lupa en modalidad de inclusión") para el tipo de registro que desea analizar. 

   Por ejemplo, para añadir un filtro que incluya las entradas para la instancia de app CF *2*, seleccione el botón de lupa ![Botón de lupa en modalidad de inclusión](images/k4_include_field_icon.jpg "Botón de lupa en modalidad de inclusión") que está disponible para el valor *2* en la sección Lista de campos. La figura siguiente muestra el filtro que incluye entradas para la instancia *2*.
    
    ![Filtro que incluye entradas de instance_id para la instancia 2](images/k4_filter_instanceid_f2.jpg "Filtro que incluye entradas de instance_id para la instancia 2")

    Para añadir un filtro que busque las entradas que no incluyan un determinado ID de instancia, seleccione el botón de lupa ![Botón de lupa en modalidad de exclusión](images/k4_exclude_field_icon.jpg "Botón de lupa en modalidad de exclusión") para el valor.

     Por ejemplo, para añadir un filtro que excluye entradas para la instancia de app CF *2*, seleccione el botón de lupa ![Botón de lupa en modalidad de exclusión](images/k4_exclude_field_icon.jpg "Botón de lupa en modalidad de exclusión") disponible para el valor *2* en la sección Lista de campos. La figura siguiente muestra el filtro que excluye entradas para la instancia *2*.
     
      ![Filtro que excluye entradas de instance_id para la instancia 2](images/k4_filter_instanceid_f3.jpg "Filtro que excluye entradas de instance_id para la instancia 2")

