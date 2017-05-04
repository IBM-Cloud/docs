---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Cómo ir al panel de control de Kibana desde un navegador web
{: #launch_Kibana_from_browser}

Inicie Kibana desde un navegador si necesita analizar entradas de registro en un espacio de {{site.data.keyword.Bluemix}}.
{:shortdesc}

La consulta que se utiliza para filtrar los datos que aparecen en Kibana recupera las entradas de registro correspondientes a un espacio de la organización {{site.data.keyword.Bluemix_notm}}. La información de registro que muestra Kibana incluye registros correspondientes a todos los recursos desplegados dentro del espacio de la organización {{site.data.keyword.Bluemix_notm}} en la que ha iniciado la sesión. 

Siga los pasos siguientes para iniciar Kibana desde un navegador:

1. Abra [https://logmet.<span class="keyword" data-hd-keyref="DomainName">NombreDominio</span>](https://logmet.{DomainName}) para iniciar una sesión en la interfaz de usuario de Kibana.

2. Seleccione la versión de Kibana que desea utilizar para analizar los registros.
    * Seleccione el separador **Kibana 4** para trabajar con Kibana 4. Se abrirá la página Descubrir. Para obtener más información, consulte [logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively).
    * Seleccione el separador **Kibana 3** para trabajar con Kibana 3. Se abrirá el panel de control de Kibana predeterminado.Para obtener más información sobre cómo personalizar un panel de control de Kibana 3, consulte [esta publicación del blog](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/). 
     
        **Nota:** Kibana 3 está en desuso. 

    Si la página Descubrir no muestra ninguna entrada de registro, ajuste el selector de tiempo. Para obtener más información, consulte [Establecimiento de un filtro de tiempo](logging_kibana_set_time_filter.html#set_time_filter).

Para obtener más información sobre Kibana, consulte la [Guía del usuario de Kibana![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.
