---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-07"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Preguntas más comunes sobre Kibana
{: #logging_qa_kibana}

A continuación encontrará las respuestas a preguntas comunes sobre cómo utilizar las funciones de registro de {{site.data.keyword.Bluemix}}. {:shortdesc}

* [¿Qué puedo hacer si no veo datos en la página Descubrir en Kibana](logging_qa_kibana.html#logging_qa_no_data_discover_kibana)

* [¿Qué puedo hacer si recibo una excepción de autenticación?](logging_qa_kibana.html#logging_qa_no_data_dashboard_kibana)


## ¿Qué puedo hacer si no veo datos en la página Descubrir en Kibana
{: #logging_qa_no_data_discover_kibana}

Hay diferentes escenarios en los que es posible que no vea datos en Kibana:

1. Cuando se inicia Kibana, es posible que no vea datos en la página Descubrir. Recibirá el mensaje siguiente: **No se han encontrado resultados.**. 
2. Si está trabajando en la página Descubrir en Kibana, es posible que, tras un breve periodo de tiempo, reciba el mensaje: **No se han encontrado resultados.** cuando intente realizar una tarea en Kibana.

Para solucionar este problema, siga estos pasos:

1. Consulte el *Selector de tiempo* definido en la página Descubrir y aumente el periodo de tiempo. 

    **Nota**: De forma predeterminada, en {{site.data.keyword.Bluemix_notm}}, el *Selector de tiempo* está definido que muestre datos correspondientes a los 15 últimos minutos.

    Para obtener más información sobre cómo definir el *Selector de tiempo*, consulte [Establecimiento de un filtro de tiempo](../kibana4/k4_filter_logs.html#set_time_filter).
       
2. Pulse la lupa que se encuentra en la barra de búsqueda de la página *Descubrir*. Los datos de la página se renuevan en función de la consulta de búsqueda predeterminada.

    Como alternativa, puede establecer un periodo de *Renovación automática*.

    **Nota**: De forma predeterminada, en {{site.data.keyword.Bluemix_notm}}, el periodo de *Renovación automática* está desactivado (**OFF**).
    
    Para obtener más información sobre cómo habilitarlo, consulte el apartado sobre [Renovación automática de los datos](../kibana4/logging_kibana_analize_logs_interactively.html#kibana_discover_view_refresh_interval).



## ¿Qué puedo hacer si recibo una excepción de autenticación?
{: #logging_qa_no_data_dashboard_kibana}

Si no puede ver datos en las visualizaciones de una página Panel de control y recibe el mensaje de error: **Error: Excepción de autorización.**, compruebe los permisos para ver los datos de cada visualización.

Tenga en cuenta la información siguiente: puede configurar una o varias visualizaciones en la página Panel de control. Si la página Panel de control realiza una solicitud para recopilar los datos que se muestran en dichas visualizaciones, solo se emite una solicitud para todas las visualizaciones. Si no tienen permisos para ver los datos de una de las visualizaciones, toda la solicitud falla.

Para solucionar este problema, siga estos pasos:

1. Identifique las visualizaciones para las que no tiene permisos.

    1. Pulse el icono de *lápiz* de una visualización en la página *Panel de control*. La visualización se abre en la página *Visualizar*. Como alternativa, en la página *Visualizar* cargue una visualización. 
    2. Verifique que puede ver datos.
    
    Repita estos pasos para cada visualización.

2. Solicite acceso para ver datos en dichas visualizaciones al administrador de la nube.

3. Cree una nueva página Panel de control que excluya las visualizaciones para los que no dispone de permisos mientras se le asigna acceso para ver los datos de las visualizaciones que causan el problema. 

    Si comparte el Panel de control, no suprima visualizaciones ya que esto afectaría a otros miembros del equipo que utilicen el mismo panel de control.


