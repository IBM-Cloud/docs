---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Cómo ir al panel de control de Kibana desde el panel de control de Bluemix
{: #launch_Kibana_from_bluemix}

Inicie Kibana desde la IU de {{site.data.keyword.Bluemix}} para ver los registros específicos de una aplicación de Cloud Foundry o un contenedor Docker.
{:shortdesc}

La consulta que se utiliza para filtrar los datos que aparecen en Kibana recupera las entradas de registro correspondientes a la app CD de {{site.data.keyword.Bluemix_notm}} o contenedor desde el que ha iniciado Kibana.  

Para ver los registros de una aplicación Cloud Foundry o de un contenedor Docker en Kibana, siga los pasos siguientes:

1. Inicie una sesión en {{site.data.keyword.Bluemix_notm}} y pulse el nombre de la app o el contenedor en el panel de control de {{site.data.keyword.Bluemix_notm}}.  
    
2. Abra el separador de registro en la IU de {{site.data.keyword.Bluemix_notm}}. 

    * Para apps CF, pulse **Registros** en la barra de navegación. 
    * Para contenedores, seleccione **Supervisión y registros** en la barra de navegación y pulse el separador **Registro**.  
    
    Se abre el separador Registros. 
    
3. Pulse **Vista avanzada**. Se abre el panel de control de **Kibana 4**.

    De forma predeterminada, se carga la página **Descubrir** con el patrón de índice predeterminado seleccionado y un filtro de tiempo establecido en los últimos 30 segundos. La consulta de búsqueda está establecida para que coincida con todas las entradas de la app CF o el contenedor Docker. 

    Si la página Descubrir no muestra ninguna entrada de registro, ajuste el selector de tiempo. Para obtener más información, consulte [Establecimiento de un filtro de tiempo](logging_kibana_set_time_filter.html#set_time_filter).

Para obtener más información sobre Kibana, consulte la [Guía del usuario de Kibana![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.

