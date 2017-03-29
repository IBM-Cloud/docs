---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Análisis de registros de app de CF desde el panel de control de Bluemix
{: #analyzing_logs_bmx_ui}

En {{site.data.keyword.Bluemix}}, puede ver, filtrar y analizar registros desde el separador **Registro** disponible para cada aplicación de Cloud Foundry. Utilice el panel de control de {{site.data.keyword.Bluemix}} para ver la actividad más reciente de la aplicación.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} Público ofrece un servicio integrado de registro. Cuando ejecuta aplicaciones en Cloud Foundry, el servicio de registro captura datos de registro de los componentes del sistema que interactúan con la aplicación, acerca de la aplicación, e incluso datos de registro internos de la aplicación cuando se utiliza stdout y stderr.

Los registros de las apps de {{site.data.keyword.Bluemix_notm}} se muestran en un formato fijo, parecido al siguiente patrón:

<code><var class="keyword varname">Componente</var>/<var class="keyword varname">IDinstancia</var>     <var class="keyword varname">mensaje</var>     <var class="keyword varname">indicación fecha y hora</var></code>
   
Para obtener más información sobre el formato de registro, consulte [Formato del registro de apps de Cloud Foundry](logging_view_dashboard.html#log_format_cf).

**Nota:** en {{site.data.keyword.Bluemix_notm}} Público, los datos de registro se almacenan durante 7 días de forma predeterminada. Puede buscar hasta 1 GB de datos por día.



##  Acceso al separador de registro de Bluemix
{: #launch_logs_tab_bmx_ui}

Para ver los registros de despliegue o de tiempo de ejecución de una aplicación Cloud Foundry, siga los pasos siguientes:

1. Inicie una sesión en {{site.data.keyword.Bluemix_notm}} y pulse el nombre de la app en el panel de control **Apps** de {{site.data.keyword.Bluemix_notm}}. 

    Se muestra la página de detalles de la app.
    
2. En la barra de navegación, pulse **Registros**.

    Se abre el separador Registros. 
    
    En el separador **Registros**, puede ver los registros recientes de la app o la parte más reciente de los registros en tiempo real. Además, puede filtrar registros por componente (tipo de registro), por ID de instancia de la app y por error.



## Formato del registro de apps de Cloud Foundry
{: #log_format_cf}

Cada entrada de registro contiene los siguientes campos: 

<dl>
<dt><strong>Indicación de fecha y hora</strong></dt>
<dd>
<p>La hora de la sentencia de registro. La indicación de fecha y hora se define hasta en milisegundos.</p>
</dd>

<dt><strong>Componente</strong></dt>
<dd>
<pre class="pre screen"><code>[App/0]</code></pre>
<p>El componente que genera el registro. </p>
<p>Cada tipo de componente va seguido de una barra inclinada y un dígito que indica la instancia de la aplicación. 0 es el dígito asignado a la primera instancia, 1 es el dígito asignado a la segunda, y así sucesivamente. Tenga en cuenta que puede filtrar para ver únicamente una instancia de la app en el panel de control.</p>
<p>En la lista siguiente se describen los distintos tipos de componentes:</p>

<dl>
<dt><strong>LGR</strong></dt>
<dd>Loggregator: el componente LGR proporciona información sobre Cloud Foundry Loggregator, que reenvía registros desde dentro de Cloud Foundry.</dd>

<dt><strong>RTR</strong></dt>
<dd>Direccionador: el componente RTR proporciona información sobre las solicitudes HTTP enviadas a una aplicación.</dd>

<dt><strong>STG</strong></dt>
<dd>Transferencia: el componente STG proporciona información sobre cómo se transfiere o se vuelve a transferir una aplicación.</dd>

<dt><strong>APP</strong></dt>
<dd>Aplicación: el componente APP proporciona los registros procedentes de la aplicación. Aquí es donde se mostrarán los valores de stderr y stdout en el código.
</dd>

<dt><strong>API</strong></dt>
<dd>API de Cloud Foundry: el componente API proporciona información sobre las acciones internas resultantes de la solicitud de un usuario de cambiar el estado de una aplicación.</dd>

<dt><strong>DEA</strong></dt>
<dd>Droplet Execution Agent: el componente DEA proporciona información sobre el inicio, detención o bloqueo de una aplicación. 
<p>Este componente sólo está disponible si la aplicación se ha desplegado en la arquitectura de Cloud Foundry que se basa en DEA.</p></dd>

<dt><strong>CELL</strong></dt>
<dd>Célula de Diego: el componente CELL proporciona información sobre el inicio, detención o bloqueo de una aplicación. 
<p>Este componente sólo está disponible si la aplicación se ha desplegado en la arquitectura de Cloud Foundry que se basa en Diego.</p></dd>

<dt><strong>SSH</strong></dt>
<dd>SSH: el componente SSH proporciona información cada vez que un usuario accede a una aplicación con el mandato **cf ssh**. 
<p>Este componente sólo está disponible si la aplicación se ha desplegado en la arquitectura de Cloud Foundry que se basa en Diego.</p></dd>

</dl>
</dd>

<dt><strong>Mensaje</strong></dt>
<dd>
<pre class="pre screen"><code>&lt;<var class="keyword varname">Mensaje</var>&gt;</code></pre>
<p>Mensaje emitido por el componente. El mensaje varía en función del contexto.</p>
</dd>
</dl>

En la figura siguiente se muestran los distintos componentes (tipos de registro) de una arquitectura Cloud Foundry basada en Droplet Execution Agent (DEA):
![Tipos de registro de una arquitectura DEA.](images/logging_F1.png "Components in a Cloud Foundry architecture that is based on the Droplet Execution Agent.")




