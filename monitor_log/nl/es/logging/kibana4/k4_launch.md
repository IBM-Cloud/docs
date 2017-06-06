---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Navegación al panel de control de Kibana
{: #k4_launch}

Inicie Kibana desde la interfaz de usuario de {{site.data.keyword.Bluemix}} o directamente desde un navegador web.
{:shortdesc}

Inicie Kibana desde {{site.data.keyword.Bluemix_notm}} para ver y analizar datos en el contexto del recurso desde el que inicia Kibana. Por ejemplo, puede iniciar Kibana para sus registros de app de CF específicos, en el contexto de dicha app específica o puede iniciar Kibana para sus registros de contenedor de Docker específicos, en el contexto de dicho contenedor específico. 
    
Inicie Kibana desde un enlace directo de navegador si desea ver datos de registros agregados desde los servicios dentro de un espacio de {{site.data.keyword.Bluemix_notm}} concreto. La consulta que se utiliza para filtrar los datos que aparecen en el panel de control recupera las entradas de registro correspondientes a un espacio de la organización {{site.data.keyword.Bluemix_notm}}. La información de registro que muestra Kibana incluye registros correspondientes a todos los recursos desplegados dentro del espacio de la organización {{site.data.keyword.Bluemix_notm}} en la que ha iniciado la sesión. 

Para obtener más información sobre Kibana, consulte la [Guía del usuario de Kibana ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.
    

##  Navegación al panel de control de Kibana desde el panel de control de Bluemix
{: #launch_Kibana_from_bluemix}

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


##  Navegación al panel de control de Kibana desde un navegador web
{: #launch_Kibana_from_browser}

La consulta que se utiliza para filtrar los datos que aparecen en Kibana recupera las entradas de registro correspondientes a un espacio de la organización {{site.data.keyword.Bluemix_notm}}. La información de registro que muestra Kibana incluye registros correspondientes a todos los recursos desplegados dentro del espacio de la organización {{site.data.keyword.Bluemix_notm}} en la que ha iniciado la sesión.

Siga los pasos siguientes para iniciar Kibana desde un navegador:

1. Abra [https://logmet.<span class="keyword" data-hd-keyref="DomainName">NombreDominio</span>](https://logmet.{DomainName}) para iniciar una sesión en la interfaz de usuario de Kibana.

2. Seleccione la versión de Kibana que desea utilizar para analizar los registros.
    * Seleccione el separador **Kibana 4** para trabajar con Kibana 4. Se abrirá la página Descubrir. Para obtener más información, consulte [logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively).
    * Seleccione el separador **Kibana 3** para trabajar con Kibana 3. Se abrirá el panel de control de Kibana predeterminado. Para obtener información sobre cómo utilizar Kibana 3 para analizar registros, consulte [Análisis de registros en Kibana 3 (en desuso)](../logging_view_kibana3.html#analyzing_logs_Kibana3). Para obtener más información sobre cómo personalizar un panel de control de Kibana 3, consulte [este artículo del blog ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/).
     
        **Nota:** Kibana 3 está en desuso.

    Si la página Descubrir no muestra ninguna entrada de registro, ajuste el selector de tiempo. Para obtener más información, consulte [Establecimiento de un filtro de tiempo](logging_kibana_set_time_filter.html#set_time_filter).


