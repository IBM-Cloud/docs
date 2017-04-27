---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Análisis de métricas en Grafana
{:#analyzing_metrics_grafana}

En {{site.data.keyword.Bluemix}}, puede utilizar Grafana, una plataforma de visualización y análisis de código abierto, para supervisar, buscar, analizar y visualizar métricas en diversos gráficos, como diagramas y tablas. Utilice Grafana para realizar tareas avanzadas de análisis.
{:shortdesc}

Puede iniciar Grafana de cualquiera de estas formas:

* Desde {{site.data.keyword.Bluemix_notm}}

    Puede iniciar métricas de contenedor Docker específicas en Grafana, en el contexto de dicho contenedor en concreto.  
    
    Para obtener más información, consulte [Cómo ir al panel de control de Grafana desde el panel de control de {{site.data.keyword.Bluemix_notm}}](monitoring_analyzing_metrics_grafana.html#launch_grafana_from_bluemix).

* Desde un enlace directo del navegador

    Puede iniciar Grafana para que los datos que ve agreguen registros de servicios de un espacio de {{site.data.keyword.Bluemix_notm}} especificado.
    
    Para obtener más información, consulte [Cómo ir al panel de control de Kibana desde un navegador web](monitoring_analyzing_metrics_grafana.html#launch_grafana_from_browser).
    


##  Cómo ir al panel de control de Grafana desde el panel de control de Bluemix
{: #launch_grafana_from_bluemix}

La consulta que se utiliza para filtrar los datos que aparecen en Grafana recupera los datos correspondientes al contenedor de {{site.data.keyword.Bluemix_notm}} desde el que ha iniciado Kibana.  

Para ver las métricas de un contenedor Docker en Grafana, siga los pasos siguientes:

1. Inicie una sesión en {{site.data.keyword.Bluemix_notm}} y pulse el contenedor en el panel de control de {{site.data.keyword.Bluemix_notm}}.  
    
2. En la barra de navegación, pulse **Supervisión y registros**. Se abre el separador de supervisión.  
    
3. Pulse **Vista avanzada**. Se abre el panel de control de **Grafana**.

Para obtener más información sobre Grafana, consulte la [Guía del usuario de Grafana![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](http://docs.grafana.org/){: new_window}.


##  Cómo ir al panel de control de Grafana desde un navegador web
{: #launch_grafana_from_browser}

La consulta que se utiliza para filtrar los datos que aparecen en Grafana recupera datos de un espacio de la organización {{site.data.keyword.Bluemix_notm}}. La información de métricas que muestra Grafana incluye registros correspondientes a todos los recursos desplegados dentro del espacio de la organización {{site.data.keyword.Bluemix_notm}} en la que ha iniciado la sesión.

Siga los pasos siguientes para iniciar Grafana desde un navegador:

1. Abra [https://logmet.<span class="keyword" data-hd-keyref="DomainName">NombreDominio</span>](https://logmet.{DomainName}) para iniciar una sesión en la interfaz de usuario de Grafana.

2. Seleccione **Grafana**.
     
Para obtener más información sobre Grafana, consulte la [Guía del usuario de Grafana![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](http://docs.grafana.org/){: new_window}.
