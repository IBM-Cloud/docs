---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-06"

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Filtrado de registros de apps de Cloud Foundry por ID de aplicación conocido en Kibana
<!-- for example, Uploading your data -->
{: #logging_kibana_known_application_id}
<!-- Provide an appropriate ID above -->

<!-- The short description section should include a sentence describing why this task is needed. For search engine optimization, include the service long name and "Bluemix". For example: -->

Si conoce el ID de aplicación de su app de Cloud Foundry, puede ver y filtrar rápidamente los registros por el ID de aplicación (application_id) de su app en el panel de control de Kibana. Puede acceder al panel de control de Kibana desde el separador **Registros** de la app de Cloud Foundry. 
{:shortdesc}

<!-- Include a sentence to briefly introduce the steps/subtopics. Example: -->
Lleve a cabo las tareas siguientes para ver y filtrar los registros de la app de Cloud Foundry por ID de aplicación conocido en el panel de control de Kibana:

1. Acceda al separador **Registros** de la app de Cloud Foundry. 

    1. Pulse el nombre de la app en el panel de control **Apps** de {{site.data.keyword.Bluemix_notm}}.
    2. Pulse el separador **Registros**. 
    
    Se muestran los registros de la app.

2. Acceda al panel de control de Kibana de la app. Para ello, pulse **Vista avanzada** ![Enlace de vista avanzada](images/logging_advanced_view.jpg). Se visualiza el panel de control de Kibana.

3. En el panel de control de Kibana, pulse el icono **Carpeta** ![icono Carpeta](images/logging_folder.jpg) para mostrar un menú que enumere todos los paneles de control recientes. 

    **Nota:** además de los paneles de control guardados por nombre, el menú enumera paneles de control sin nombre según el formato siguiente: *ALCH_TENANT_ID_application_id*. 

    ![Lista de paneles de control](images/logging_list_of_dashboards.jpg)

4. Seleccione el panel de control con un nombre que contenga el application_id conocido. 

    El panel de control carga y muestra información filtrada para su application_id.

5. Si lo desea, puede añadir más campos a la sección de filtro, por ejemplo **instance_id** para habilitar o inhabilitar el filtrado de registros por ID de instancia. 
  
    1. En la ventana **TODOS LOS SUCESOS**, pulse una fila de suceso de registro para ver los detalles de dicho suceso. 
	
        ![Ventana Todos los sucesos que muestra detalles del suceso de registro seleccionado](images/logging_selected_log_event.jpg)
	
    2. Elija un suceso que muestre el valor del campo que desea filtrar.
	
    3. Añada un filtro.
    
        Para añadir un filtro que incluya información sobre dicho valor de campo específico, pulse el icono **Lupa** ![icono Lupa](images/logging_magnifying_glass.jpg) en la fila de la tabla que contiene el campo que desea filtrar. 
	
        Para añadir un filtro que excluya información sobre este valor de campo concreto, pulse el icono **Exclusión** ![icono de exclusión](images/logging_exclusion_icon.png) en la fila de la tabla que contiene el campo que desea filtrar.  

        Se añade una nueva condición de filtro al panel de control de Kibana.
	
	    ![Condición de filtro para el campo instance_id](images/logging_instance_id_filter.jpg)
	
6. Guarde este panel de control con un nombre que reconozca. 

    Pulse el icono **Guardar** ![icono Guardar](images/logging_save.jpg) y escriba un nombre para el panel de control. 

    **Nota:** si intenta guardar un panel de control con un nombre que contenga espacios en blanco, no se guardará. Escriba un nombre sin espacios y pulse el icono **Guardar**.

    ![Guarde el nombre del panel de control](images/logging_save_dashboard.jpg).


Ha creado un panel de control que filtra las entradas de registro por ID de aplicación e ID de instancia. Puede cargar el panel de control que ha guardado en cualquier momento pulsando el icono **Carpeta** ![icono Carpeta](images/logging_folder.jpg) y seleccionando el panel de control por nombre.
