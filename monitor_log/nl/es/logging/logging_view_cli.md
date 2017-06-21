---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Análisis de registros desde la CLI
{: #analyzing_logs_cli}

En {{site.data.keyword.Bluemix}}, puede ver, filtrar y analizar registros mediante la interfaz de línea de mandatos. Utilice la línea de mandatos para gestionar los registros mediante programa. 
{:shortdesc}

Para analizar los registros de la aplicación Cloud Foundry (CF), utilice el mandato siguiente: `cf logs` Para obtener más información, consulte [Análisis de registros de app CF desde la CLI](logging_view_cli.html#analyzing_cf_logs_cli).

Para analizar los registros del contenedor Docker, utilice el mandato siguiente: `cf ic logs` Para obtener más información, consulte [Análisis de registros del contenedor Docker desde la CLI](logging_view_cli.html#analyzing_container_logs_cli).


## Análisis de registros de app de CF desde la CLI
{: #analyzing_cf_logs_cli}

Utilice el mandato **cf logs** para visualizar registros de una app Cloud Foundry y de componentes del sistema que interactúan con la misma cuando se despliega la app en {{site.data.keyword.Bluemix_notm}}. El mandato **cf logs** muestra las secuencias de registro STDOUT y STDERR de una aplicación Cloud Foundry.

Para ver los registros en los que está interesado o para excluir el contenido que no desea ver, puede utilizar el mandato **cf logs** con opciones de filtrado, como por ejemplo,**cut** y **grep** en la interfaz de línea de mandatos cf:

* Para ver los registros correspondientes a una app Cloud Foundry, consulte [Visualización del registro de una app Cloud Foundry](logging_view_cli.html#full_log_cli).
* Para ver los registros más recientes de una app Cloud Foundry, consulte [Visualización de las últimas entradas de registro de una app Cloud Foundry](logging_view_cli.html#tailing_log_cli).
* Para ver los registros de una app Cloud Foundry correspondientes a un determinado periodo de tiempo, consulte [Visualización de una sección de los registros](logging_view_cli.html#partial_log_cli).
* Para ver las entradas de los registros de una app Cloud Foundry que contienen palabras clave específicas, consulte [Visualización de entradas de registro que contienen determinadas palabras clave](logging_view_cli.html#partial_by_keyword_log_cli).


### Visualización del registro de una app Cloud Foundry
{: #full_log_cli}

Para ver todos los registros disponibles de una app Cloud Foundry, siga estos pasos:

1. Abra un terminal e inicie una sesión en {{site.data.keyword.Bluemix}}.

2. Desde la línea de mandatos, ejecute el siguiente mandato para visualizar todos los registros:

   <pre class="pre screen"><code>cf logs <var class="keyword varname">nombreapp</var></code></pre>
   
   
### Visualización de las últimas entradas de registro de una app Cloud Foundry
{: #tailing_log_cli}

Para ver los registros más recientes disponibles para una app Cloud Foundry, siga los pasos siguientes:

1. Abra un terminal e inicie una sesión en {{site.data.keyword.Bluemix}}.

2. Desde la línea de mandatos, ejecute el siguiente mandato para visualizar todos los registros:

     <pre class="pre screen"><code>cf logs <var class="keyword varname">nombreapp</var> --recent</code></pre>

<div class="note tip"><span class="tiptitle">Consejo:</span> Cuando ejecute el mandato <span class="keyword cmdname">cf push</span> o <span class="keyword cmdname">cf
start</span> en una ventana de línea de mandatos, puede escribir <samp class="ph codeph">cf
logs appname --recent</samp> en otra ventana de línea de mandatos para ver los
registros en tiempo real. </div>


### Visualización de una sección de un registro Cloud Foundry
{: #partial_log_cli}

Para ver una parte de los registros disponibles para una app Cloud Foundry correspondientes a un determinado periodo de tiempo, siga los pasos siguientes:

1. Abra un terminal e inicie una sesión en {{site.data.keyword.Bluemix}}.

2. Desde la línea de mandatos, ejecute el siguiente mandato para visualizar todos los registros:

    <pre class="pre screen"><code>cf logs <var class="keyword varname">appname</var> --recent  | cut -c 29-40,46-</code></pre>
    
    Para obtener más información sobre la opción **cut**, escriba **cut --help**.


### Visualización de las entradas de registro que contienen determinadas palabras clave
{: #partial_by_keyword_log_cli}

Para visualizar las entradas de registro que contienen determinadas palabras clave de una app Cloud Foundry, siga estos pasos:

1. Abra un terminal e inicie una sesión en {{site.data.keyword.Bluemix}}.

2. Desde la línea de mandatos, ejecute el siguiente mandato para visualizar todos los registros:

    <pre class="pre screen"><code>cf logs <var class="keyword varname">appname</var> --recent | grep '<var class="keyword varname">keyword</var>'</code></pre>
    

Por ejemplo, para visualizar las entradas de registro que contienen la palabra clave **APP**, puede utilizar el mandato siguiente:

<pre class="pre screen"><code>cf logs appname --recent | grep '\[App'
</code></pre>

Para obtener más información sobre la opción **grep**, escriba **grep --help**.


### Registros de aplicación de Cloud Foundry
{: #cf_app_logs_cli}

Dispone de los siguientes registros de una aplicación Cloud Foundry después de desplegarla en {{site.data.keyword.Bluemix}}:

**buildpack.log**

Este archivo de registro registra sucesos informativos detallados para la depuración. Puede utilizar este registro para resolver problemas de ejecución del paquete de compilación.

Para generar datos en el archivo *buildpack.log* debe habilitar el rastreo del paquete de compilación mediante el mandato siguiente: `cf set-env appname JBP_LOG_LEVEL DEBUG`
   
Para ver este registro, ejecute el siguiente mandato: `cf files appname app/.buildpack-diagnostics/buildpack.log`


**staging_task.log**

Este archivo de registro registra mensajes después de los principales pasos de la tarea de transferencia. Puede utilizar este registro para resolver problemas de transferencia.

Para ver este registro, ejecute el siguiente mandato: `cf files appname logs/staging_task.log`


**Nota:** Para obtener información sobre cómo habilitar el registro de aplicación, consulte [Depuración de errores de tiempo de ejecución](/docs/debug/index.html#debugging-runtime-errors).

## Análisis de registros del contenedor Docker desde la CLI
{: #analyzing_container_logs_cli}

Utilice el mandato `cf ic logs` para visualizar los registros de un contenedor en {{site.data.keyword.Bluemix_notm}}. Por ejemplo, puede utilizar los registros para analizar por qué un contenedor se ha detenido o para revisar la salida del contenedor. 

Para ver errores de aplicación correspondientes a la app que se ejecuta en un contenedor mediante el mandato `cf ic logs`, la aplicación debe grabar sus registros en las secuencias de salida estándar (STDOUT) y de error estándar (STDERR). Si diseña la aplicación para que grabe en estas secuencias de salida estándar, podrá ver los registros a través de la línea de mandatos aunque el contenedor se haya concluido o se haya colgado.

Para obtener más información sobre el mandato `cf ic logs`, consulte [Mandato cf ic logs](/docs/containers/container_cli_reference_cfic.html#container_cli_reference_cfic__logs).


