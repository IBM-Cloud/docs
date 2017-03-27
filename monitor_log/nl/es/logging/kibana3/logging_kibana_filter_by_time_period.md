---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-06"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Filtrado de registros de apps de Cloud Foundry por tiempo en Kibana
<!-- for example, Uploading your data -->
{: #logging_kibana_time_filter}


Puede ver y filtrar registros de aplicaciones de {{site.data.keyword.Bluemix_notm}} por tiempo en el panel de control de Kibana. Puede acceder al panel de control de Kibana desde el separador **Registros** de la app de Cloud Foundry. 
{:shortdesc}

Lleve a cabo las tareas siguientes para ver y filtrar los registros de la app de Cloud Foundry por tiempo en el panel de control de Kibana:

1. Acceda al separador **Registros** de la app de Cloud Foundry. 

    1. Pulse el nombre de la app en el panel de control **Apps** de {{site.data.keyword.Bluemix_notm}}.
    2. Pulse el separador **Registros**. 
    
    Se muestran los registros de la app.

2. Acceda al panel de control de Kibana de la app. Para ello, pulse **Vista avanzada** ![Enlace de vista avanzada](images/logging_advanced_view.jpg). Se visualiza el panel de control de Kibana.


3. En el panel de control de Kibana, pulse **Filtro de tiempo**; ![filtro de tiempo de Kibana](images/logging_kibana_time_filter.jpg); luego seleccione **Personalizado** en el menú desplegable. Se visualiza la ventana siguiente:

    ![Filtro de tiempo personalizado en el panel de control de Kibana](images/logging_custom_time_filter.jpg)

4. Pulse los campos **Desde** y **Hasta** para editar la hora inicial y final del filtro. 
    
    Para incluir registros hasta este momento, pulse el enlace **ahora**. 
    Cuando esté satisfecho con el rango de tiempo, pulse **Aplicar**. 

Ahora el panel de control de Kibana mostrará los sucesos registrados correspondientes al filtro de tiempo personalizado.
