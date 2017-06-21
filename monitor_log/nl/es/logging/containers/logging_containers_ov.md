---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Registro correspondiente al servicio IBM Bluemix Container
{: #logging_containers_ov}

En {{site.data.keyword.Bluemix}}, puede ver, filtrar y analizar registros de contenedor mediante el panel de control de {{site.data.keyword.Bluemix_notm}}, Kibana y la interfaz de línea de mandatos.
{:shortdesc}

Los registros de contenedor se supervisan y se reenvía desde fuera del contenedor mediante rastreadores. Los rastreadores envían los datos a un sistema Elasticsearch multiarrendatario de {{site.data.keyword.Bluemix_notm}}.

**Nota:** Tiene la posibilidad de analizar los registros de contenedores Docker en {{site.data.keyword.Bluemix_notm}} que se despliegan en la infraestructura de nube gestionada de {{site.data.keyword.IBM}}.

En la figura siguiente se muestra una vista de nivel alto del registro de {{site.data.keyword.containershort}}:

![Visión general de componentes de alto nivel para contenedores](images/logging_containers_ov.jpg "Visión general de componentes de alto nivel para contenedores")

El registro de contenedores se habilita automáticamente al desplegar el contenedor en {{site.data.keyword.Bluemix_notm}}.


## Métodos para analizar registros de contenedor
{: #logging_containers_ov_methods}
 
Puede elegir cualquiera de los siguientes métodos para analizar los registros de un contenedor:

* Analizar el registro en {{site.data.keyword.Bluemix_notm}} para ver la actividad más reciente del contenedor.
    
    Puede ver, filtrar y analizar registros desde el separador **Supervisión y registro** disponible para cada contenedor. Para obtener más información, consulte [Análisis de registros desde el panel de control de Bluemix](../logging_view_dashboard.html#analyzing_logs_bmx_ui).
    
* Analizar registros en Kibana para realizar tareas avanzadas de análisis.
    
    Puede utilizar Kibana, una plataforma de visualización y análisis de código abierto, para supervisar, buscar, analizar y visualizar datos en diversos gráficos, como diagramas y tablas. Para obtener más información, consulte [Análisis de registros en Kibana](../kibana4/logging_analyzing_logs_Kibana.html#analyzing_logs_Kibana).

* Analizar registros mediante la CLI para utilizar mandatos a fin de gestionar registros mediante programación.
    
    Puede ver, filtrar y analizar registros mediante la interfaz de línea de mandatos con el mandato **cf ic logs**. Para obtener más información, consulte [Análisis de registros desde la interfaz de línea de mandatos](../logging_view_cli.html#analyzing_logs_cli).

## Registros recopilados para contenedores
{: #logging_containers_ov_logs_collected}

De forma predeterminada, se recopilan los siguientes registros:

<table>
  <caption>Tabla 1. Registros</caption>
  <tbody>
    <tr>
      <th align="center">Registro</th>
      <th align="center">Descripción</th>
    </tr>
    <tr>
      <td align="left" width="30%">/var/log/messages</td>
      <td align="left" width="70%"> De forma predeterminada, los mensajes de Docker se almacenan en la carpeta /var/log/messages del contenedor. Este registro incluye los mensajes del sistema.
      </td>
    </tr>
    <tr>
      <td align="left">./docker.log</td>
      <td align="left">Este es el registro de Docker. <br> El archivo de registro de Docker no se almacena como archivo dentro del contenedor, pero se recopila igualmente. Este archivo de registro se recopila de forma predeterminada, ya que constituye el convenio estándar de Docker para exponer la información
stdout (salida estándar) y stderr (error estándar) del contenedor. Si un proceso del contenedor se registra en stdout o stderr, se recopilará dicha información. 
      </td>
     </tr>
  </tbody>
</table>

Para recopilar registros adicionales, añada la variable de entorno de **LOG_LOCATIONS** con una vía de acceso al archivo de registro cuando cree el contenedor. Puede añadir varios archivos de registro separándolos con comas. Para obtener más información, consulte [Recopilación de datos de registro no predeterminado desde un contenedor](logging_containers_other_logs.html#logging_containers_collect_data).



## Retención de registros
{: #logging_containers_ov_log_retention}

Tenga en cuenta la información siguiente sobre la retención de registros:

* Se almacena un máximo de 1 GB por espacio de datos al día. Cualquier registro que supere dicha capacidad de 1 GB se descartará. Las asignaciones de capacidades se restablecen todos los días a las 12:30 AM UTC. 

    Para aumentar su capacidad, póngase en contacto con el equipo de soporte. En la incidencia de soporte, incluya el ID de espacio correspondiente a la solicitud de incremento de capacidad, el nuevo tamaño de la capacidad y el motivo de la solicitud.

* Se pueden buscar hasta 7 GB de datos para un máximo de 7 días. Los datos de registro se renuevan (Primero en entrar, primero en salir) una vez que se ha alcanzado 7 GB de datos o 7 días.

