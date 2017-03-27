---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-16"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Filtrado de registros de apps de Cloud Foundry por tipo de mensaje en Kibana
<!-- for example, Uploading your data -->
{: #logging_kibana_message_type_filter}
<!-- Provide an appropriate ID above -->

Puede ver y filtrar registros de aplicaciones de {{site.data.keyword.Bluemix_notm}} por tipo de mensaje en el panel de control de Kibana. Puede acceder al panel de control de Kibana desde el separador **Registros** de la app de Cloud Foundry. 
{:shortdesc}

<!-- Include a sentence to briefly introduce the steps/subtopics. Example: -->
Lleve a cabo las tareas siguientes para ver y filtrar los registros de la app de Cloud Foundry por tipo de mensaje en el panel de control de Kibana:

1. Acceda al separador **Registros** de la app de Cloud Foundry. 

    1. Pulse el nombre de la app en el panel de control **Apps** de {{site.data.keyword.Bluemix_notm}}.
    2. Pulse el separador **Registros**. 
    
    Se muestran los registros de la app.

2. Acceda al panel de control de Kibana de la app. Para ello, pulse **Vista avanzada** ![Enlace de vista avanzada](images/logging_advanced_view.jpg). Se visualiza el panel de control de Kibana.

3. En la ventana **TODOS LOS SUCESOS**, pulse el icono de flecha hacia la derecha para mostrar todos los campos. 

    ![Ventana Todos los sucesos con icono de flecha hacia la derecha](images/logging_all_events_no_fields.jpg)

4. En el panel **Campos**, seleccione **message_type** para visualizar el componente que ha generado cada entrada del registro en la ventana **TODOS LOS SUCESOS**.

    ![Ventana Todos los sucesos con el campo message_type seleccionado](images/logging_message_type.png)

5. En la ventana **TODOS LOS SUCESOS**, pulse una fila de suceso de registro para ver los detalles de dicho suceso. Elija un suceso que muestre el **message_type** que desea filtrar.

    ![Ventana Todos los sucesos que muestra detalles del suceso de registro seleccionado](images/logging_message_type_add_filter.png)

6. Añada un filtro para incluir o excluir información sobre un tipo de mensaje. 

    * Para añadir un filtro que incluya información sobre un tipo de mensaje, pulse el icono **Lupa** ![icono Lupa](images/logging_magnifying_glass.jpg) en la fila message_type de la tabla. 
    
           ![Condición de filtro para el campo message_type](images/logging_message_type_filter.png)
    
    * Para añadir un filtro que excluya información sobre un tipo de mensaje, pulse el icono **Exclusión** ![icono de exclusión](images/logging_exclusion_icon.png) en la fila message_type de la tabla. 
    
    Se añade una nueva condición de filtro al panel de control de Kibana.

7. Si lo desea, repita el paso anterior para añadir un filtro para otros tipos de mensaje. Para ver la lista completa de tipos de mensaje, consulte [Formato de registro](../logging_view_kibana3.html#kibana_log_format_cf).

9. Guarde el panel de control.    
        
    Cuando haya terminado de crear los filtros, pulse el icono **Guardar** ![icono Guardar](images/logging_save.jpg) y escriba un nombre para el panel de control. 
      
    **Nota:** si intenta guardar un panel de control con un nombre que contenga espacios en blanco, no se guardará. Escriba un nombre sin espacios y pulse el icono **Guardar**.
    
    ![Guarde el nombre del panel de control](images/logging_save_dashboard.jpg).

Ha creado un panel de control que filtra las entradas de registro por tipo de mensaje. Puede cargar el panel de control que ha guardado en cualquier momento pulsando el icono **Carpeta** ![icono Carpeta](images/logging_folder.jpg) y seleccionando el panel de control por nombre.
