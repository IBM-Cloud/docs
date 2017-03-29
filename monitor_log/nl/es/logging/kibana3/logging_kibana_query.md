---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Filtrado de registros de apps de Cloud Foundry con consultas en Kibana
{: #logging_kibana_query}

Utilice Kibana para crear consultas para buscar en los registros términos clave y filtrar por dichos términos. Con Kibana, puede comparar consultas visualmente en el panel de control. Puede acceder al panel de control de Kibana desde el separador **Registros** de la app de Cloud Foundry. 
{:shortdesc}

Lleve a cabo las tareas siguientes para crear una consulta para los registros de la app de Cloud Foundry en el panel de control de Kibana:

1. Acceda al separador **Registros** de la app de Cloud Foundry. 

    1. Pulse el nombre de la app en el panel de control **Apps** de {{site.data.keyword.Bluemix_notm}}.
    2. Pulse el separador **Registros**. 
    
    Se muestran los registros de la app.

2. Acceda al panel de control de Kibana de la app. Para ello, pulse **Vista avanzada** ![Enlace de vista avanzada](images/logging_advanced_view.jpg). Se visualiza el panel de control de Kibana.

3. En el panel de control de Kibana, pulse **CONSULTA** ![icono Consulta](images/logging_query.jpg) para visualizar el campo. Cuando se accede a Kibana para ver los registros de la app desde el separador **Registros** de la app, se crea una consulta para mostrar todos los registros correspondientes al application_id de la app.
	
    Para editar la consulta, pulse el campo **CONSULTA** y especifique un término de búsqueda.

    * Para buscar una palabra clave, o parte de una palabra clave, escriba una palabra seguida de un símbolo de comodín \*; por ejemplo, `Java*`. 
	* Para buscar una determinada frase, escriba la frase entre comillas dobles; por ejemplo, `"Java/1.8.0"`.
	* Para crear búsquedas más complejas, puede utilizar los términos lógicos AND y OR; por ejemplo `"Java/1.8.0" OR "Java/1.7.0"`.
	* Para buscar un valor dentro de un campo determinado, escriba la búsqueda con el siguiente formato: *log_field_name:search_term*; por ejemplo, `instance_id:1`.
	* Para buscar un rango de valores para un determinado campo de registro, escriba la búsqueda con el siguiente formato: *log_field_name:[start_of_range TO end_of_range]*; por ejemplo, `instance_id:[1 TO 2]`.

4. Si desea comparar los resultados de dos consultas, puede añadir otro término de consulta al panel de control. Para añadir otra consulta, pulse el icono **+** situado en el final del campo **CONSULTA**.

    ![Campo de consulta](images/logging_query_field.jpg)
	
    Se muestra un nuevo campo **CONSULTA** que contiene el carácter comodín \*. Esta consulta indica a Kibana que incluya todas las entradas.
	
    ![Campo Consulta adicional](images/logging_additional_query_field.jpg)
	
    El panel de control se actualiza con los resultados de la consulta nueva. El panel **SUCESOS POR TIEMPO** muestra una representación gráfica de ambas consultas, junto con el número de términos para cada consulta entre paréntesis. 
	
    ![Panel de control que muestra un gráfico para ambas consultas](images/logging_dashboard_queries.jpg)
	
5. Pulse el nuevo campo **CONSULTA** para editar su contenido y añadir una condición de consulta; por ejemplo, `instance_id:1`. Utilice el panel **SUCESOS POR TIEMPO** para comparar los resultados de las consultas.

    ![Panel de control que muestra un gráfico para ambas consultas](images/logging_dashboard_queries2.jpg)

6. Para suprimir una consulta, mueva el ratón sobre el campo **CONSULTA** que desea suprimir hasta que aparezca el icono **suprimir**. Pulse el icono **suprimir**.

    ![Campo de consulta con icono de supresión](images/logging_delete_query.jpg)

7. Para guardar este panel de control con un nombre que pueda reconocer, pulse el icono **Guardar** ![icono Guardar](images/logging_save.jpg) y escriba un nombre para el panel de control. 

    **Nota:** si intenta guardar un panel de control con un nombre que contenga espacios en blanco, no se guardará. Escriba un nombre sin espacios y pulse el icono **Guardar**.

    ![Guarde el nombre del panel de control ](images/logging_save_dashboard.jpg)


