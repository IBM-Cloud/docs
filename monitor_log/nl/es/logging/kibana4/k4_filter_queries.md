---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Filtrado registros mediante la definición de consultas de búsqueda personalizada
{:#k4_filter_queries}

En la barra de búsqueda de la página Descubrir, puede definir y guardar consultas de búsqueda utilizando el lenguaje de consulta de Lucene. Para cada búsqueda, puede aplicar filtros para precisar las entradas que están disponibles para el análisis.
{:shortdesc}

Complete las tareas siguientes para filtrar los registros utilizando una búsqueda personalizada:

1. Acceda al separador **Registros** de la app Cloud Foundry (CF) o contenedor. 

    1. Pulse el nombre de la app o el contenedor en el panel de control de {{site.data.keyword.Bluemix}}.
    2. Para aplicaciones CF, pulse el separador **Registros**. Para contenedores, pulse **Supervisión y registros** y seleccione el separador **Registro**. 
    
    Se muestran los registros. 

2. Acceda a Kibana. Pulse **Vista avanzada** ![enlace de vista avanzada](images/logging_advanced_view.jpg). Se visualiza el panel de control de Kibana.

    Cuando se accede a Kibana, se aplica la búsqueda predeterminada. Puede ver los registros para consulta la lista de instancias del recurso para el que ha iniciado Kibana. Puede filtrar los registros para cualquiera de los recursos de {{site.data.keyword.Bluemix_notm}} o para todos ellos en este espacio.

En lugar de "keyword", el término correcto es "term" para Lucene.

3. Examine la página Descubrir para ver el subconjunto de datos que muestra. Para obtener más información, consulte [Identificación de los datos que se muestran en la página Descubrir de Kibana](logging_kibana_analize_logs_interactively.html#k4_identify_data). A continuación, modifique la consulta predeterminada para filtrar las entradas.

    **Nota:** Utilice el lenguaje de consulta de Lucene para definir la consulta personalizada. Para obtener más información, consulte [Apache Lucene - Sintaxis del analizador de consultas![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://lucene.apache.org/core/2_9_4/queryparsersyntax.html){: new_window}
    
    Cuando Kibana se inicia desde {{site.data.keyword.Bluemix_notm}}, para modificar la consulta y definir varios criterios de búsqueda puede utilizar los términos lógicos **AND** y **OR**. Estos operadores deben estar en mayúsculas.    
    
    * Para buscar una palabra clave, o parte de una palabra clave, escriba una palabra seguida de un símbolo de comodín \*; por ejemplo, `Java*`. 
    * Para buscar una determinada frase, escriba la frase entre comillas dobles; por ejemplo, `"Java/1.8.0"`.
    * Para crear búsquedas más complejas, puede utilizar los términos lógicos AND y OR; por ejemplo `"Java/1.8.0" OR "Java/1.7.0"`.
    * Para buscar un valor dentro de un campo determinado, escriba la búsqueda con el siguiente formato: *log_field_name:search_term*; por ejemplo, `instance_id:"1"`. 
    * Para buscar un rango de valores para un determinado campo de registro, escriba la búsqueda con el siguiente formato: *log_field_name:[start_of_range TO end_of_range]*; por ejemplo, `instance_id:["1" TO "2"]`. 

     Por ejemplo, para una app CF, puede crear una consulta `application_id:9d222152-8834-4bab-8685-3036cd25931a AND instance_id:["0" TO "1"]` que solo muestre las entradas correspondientes a las instancias *0* y *1*. 

4. Guarde la consulta para poderla reutilizar más adelante. Para obtener más información, consulte [Cómo guardar una búsqueda](logging_kibana_filtering_logs.html#k4_save_search). 

**Nota:** Si tiene que suprimir una consulta, consulte [Supresión de una búsqueda](logging_kibana_filtering_logs.html#k4_delete_search).



