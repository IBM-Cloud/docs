---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Análisis de registros desde la consola de Bluemix
{: #analyzing_logs_bmx_ui}

En {{site.data.keyword.Bluemix}}, puede ver, filtrar y analizar registros desde el separador de registro disponible para cada app de Cloud Foundry o contenedor Docker. {:shortdesc}

{{site.data.keyword.Bluemix_notm}} Público ofrece funciones integradas de registro. Por ejemplo, cuando ejecuta aplicaciones en Cloud Foundry (CF), el servicio de registro captura datos de registro de los componentes del sistema que interactúan con la aplicación, acerca de la aplicación, e incluso datos de registro internos de la aplicación cuando se utiliza stdout y stderr.

Tenga en cuenta la información siguiente sobre la disponibilidad de los datos de registro para el análisis y la retención de registros:

* En las apps de {{site.data.keyword.Bluemix_notm}} Público, los datos de registro se almacenan durante 7 días de forma predeterminada. 
* Puede almacenar hasta 1 GB de datos por día. 
* De forma predeterminada, los registros que están disponibles para su análisis desde la consola de {{site.data.keyword.Bluemix_notm}} incluyen datos correspondientes a las últimas 24 horas.

**Consejo:** Para analizar datos para un periodo personalizado que precede a las últimas 24 horas, consulte [Análisis avanzado de registros con Kibana](logging_analyzing_logs_Kibana.html#analyzing_logs_Kibana). 

##  Visualización de registros de una app Cloud Foundry
{: #launch_logs_tab_bmx_ui_cf}

Para ver los registros de despliegue o de tiempo de ejecución de una app Cloud Foundry, siga los pasos siguientes:

1. En el panel de control Apps, pulse el nombre de su app Cloud Foundry.  
    
2. En la página de detalles de la app, pulse **Registros**. 
    
    En el separador **Registros**, puede ver los registros recientes de la app o la parte más reciente de los registros en tiempo real. Además, puede filtrar registros por componente (tipo de registro), por ID de instancia de la app y por error.
    

##  Visualización de registros de un contenedor Docker
{: #launch_logs_tab_bmx_ui_containers}

Para ver los registros de despliegue o de tiempo de ejecución de un contenedor Docker, siga los pasos siguientes:

1. En el panel de control Apps, pulse en un contenedor o grupo de contenedores.  
    
2. En la página de detallesde la app, pulse **Supervisión y registros**. 

3. Seleccione el separador **Registro**.
    
    En el separador **Registro**, puede ver los registros recientes del contenedor o la parte más reciente de los registros en tiempo real.  

## Formato del registro de apps de CF
{: #log_format_cf}

Los registros de las apps de {{site.data.keyword.Bluemix_notm}} Cloud Foundry se muestran en un formato fijo, parecido al siguiente patrón:

<code><var class="keyword varname">Componente</var>/<var class="keyword varname">IDinstancia</var>/<var class="keyword varname">mensaje</var>/<var class="keyword varname">indicación fecha y hora</var></code>

Cada entrada de registro contiene los siguientes campos: 

| Campo | Descripción |
|-------|-------------|
| Indicación de fecha y hora | La hora de la sentencia de registro. La indicación de fecha y hora se define hasta en milisegundos. |
| Componente | El componente que genera el registro. Para ver la lista de los distintos componentes, consulte [Orígenes de registro para apps de CF](logging_cf_apps.html#logging_bluemix_cf_apps_log_sources). <br> Cada tipo de componente va seguido de una barra inclinada y un dígito que indica la instancia de la aplicación. 0 es el dígito asignado a la primera instancia, 1 es el dígito asignado a la segunda, y así sucesivamente. |
| Mensaje  | Mensaje emitido por el componente. El mensaje varía en función del contexto. |



## Formato de registro para registros de contenedor
{: #log_format_containers}

Los registros de los contenedores se muestran en un formato fijo, parecido al siguiente patrón:

<code><var class="keyword varname">indicación fecha y hora</var>/<var class="keyword varname">máquina</var>/<var class="keyword varname">mensaje</var>  </code>

Cada entrada de registro contiene los siguientes campos: 

| Campo | Descripción |
|-------|-------------|
| Fecha/Hora | La hora de la sentencia de registro. La indicación de fecha y hora se define hasta en milisegundos. |
| Máquina | El nombre de host en el que se ejecuta el contenedor.  |
| Mensaje  | El mensaje emitido. El mensaje varía en función del contexto. |


