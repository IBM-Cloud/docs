---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Análisis de registros en Kibana
{: #analyzing_logs_Kibana3}

En {{site.data.keyword.Bluemix}}, puede utilizar Kibana, una plataforma de visualización y análisis de código abierto, para supervisar, buscar, analizar y visualizar datos en diversos gráficos, como diagramas y tablas. Utilice Kibana para realizar tareas avanzadas de análisis.
{:shortdesc}

Puede iniciar Kibana de cualquiera de estas formas:

* Desde el panel de control de la app Cloud Foundry

    Puede iniciar los registros específicos de la app CF en Kibana, en el contexto de la app específica.
    
    La consulta que se utiliza para filtrar los datos que aparecen en el panel de control recupera las entradas de registro de la aplicación Cloud Foundry. La información de registro que muestra el panel de control de Kibana está relacionada con una sola aplicación Cloud Foundry y todas sus instancias. Para obtener más información, consulte [Cómo ir al panel de control de Kibana desde el panel de control de {{site.data.keyword.Bluemix}}](logging_view_kibana3.html#launch_Kibana_from_bluemix).

* Desde un enlace directo del navegador

    Puede que desee iniciar el panel de control de Kibana personalizado que agrega datos de servicios a un espacio de {{site.data.keyword.Bluemix}} proporcionado.
    
    La consulta que se utiliza para filtrar los datos que aparecen en el panel de control recupera las entradas de registro correspondientes a un espacio de la organización {{site.data.keyword.Bluemix}}. La información de registro que muestra el panel de control de Kibana incluye registros correspondientes a todos los recursos desplegados dentro del espacio de la organización {{site.data.keyword.Bluemix}} en la que ha iniciado la sesión. Para obtener más información, consulte [Cómo ir al panel de control de Kibana desde un navegador web](logging_view_kibana3.html#launch_Kibana_from_browser).
    
    También puede cambiar o eliminar la consulta inicial y añadir más consultas. Para obtener más información, consulte [Filtrado de registros de la app Cloud Foundry con consultas en Kibana](kibana3/logging_kibana_query.html#logging_kibana_query).


Kibana es una interfaz basada en navegador en la que puede personalizar paneles de control que luego puede utilizar para analizar datos de registro y realizar tareas avanzadas de gestión. 

En {{site.data.keyword.Bluemix}}, puede analizar datos utilizando el panel de control predeterminado de Kibana que está disponible para cada app Cloud Foundry y para cada espacio de la organización. De forma predeterminada, estos paneles de control muestran todos los datos disponibles correspondientes a las últimas 24 horas a través de un panel que incluye una fila Histograma y una fila Tabla de sucesos. 

Para restringir la información mostrada a través de cualquier panel de control predeterminado, puede añadir consultas y filtros a un panel de control predeterminado. A continuación, puede guardar el panel de control para su reutilización en el futuro. 

Los datos que muestran un panel de control de Kibana se controlan mediante la consulta. Para modificar la información que se visualiza en un panel de control, puede cambiar la consulta, añadir varias consultas, y, a continuación, guardar el panel de control. Puede personalizar, guardar y compartir varios paneles de control simultáneamente. Por ejemplo, así es cómo Kibana muestra información acerca de una sola app en el espacio.

También puede configurar filtros desde campos de registro, por ejemplo message_type e instance_ID. Para obtener más información, consulte [Formato del registro de Kibana](logging_view_kibana3.html#kibana_log_format_cf). Puede habilitar o inhabilitar dinámicamente estos filtros. El panel de control mostrará las entradas de registro que cumplan la consulta y los criterios de filtro que habilite. Para obtener más información, consulte [Filtrado de datos en el panel de control de Kibana](logging_view_kibana3.html#filter_data_kibana_dashboard).

Para visualizar los datos, puede configurar paneles. Kibana incluye distintos paneles, como tabla, tendencias e histograma, que puede utilizar para analizar la información. Puede añadir, eliminar y cambiar la disposición de los paneles del panel de control. El objetivo de cada panel varía. Algunos paneles se organizan en filas que proporcionan los resultados de una o varias consultas. Otros paneles muestran documentos o información personalizada. Para obtener más información, consulte [Personalización de un panel de control de Kibana](logging_view_kibana3.html#customize_kibana_dashboard).

Después de personalizar un panel de control, puede elegir entre cualquiera de las acciones siguientes:

* Puede guardar el panel de control para su reutilización en el futuro. Para obtener más información, consulte [Cómo guardar un panel de control de Kibana](logging_view_kibana3.html#save_Kibana_dashboard).

* Puede exportar o compartir un enlace directo a un panel de control de Kibana con otro usuario. Para obtener más información, consulte [Exportación y compartición de los paneles de control de Kibana](kibana3/logging_kibana_export_share_dashboard.html#sexporting_sharing_kibana_dash).

* Puede incluir el panel de control en una página web. Para que un usuario vea un panel de control incorporado, dicho usuario debe tener permisos para acceder a Kibana.

Para obtener más información, consulte la documentación de [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html).

**Nota:** Kibana 4 y Kibana 3 reciben soporte. Kibana 3 está en desuso.


##  Cómo ir al panel de control de Kibana desde el panel de control de Bluemix
{: #launch_Kibana_from_bluemix}

La consulta que se utiliza para filtrar los datos que aparecen en el panel de control recupera las entradas de registro de la aplicación Cloud Foundry. La información de registro que muestra el panel de control de Kibana está relacionada con una sola aplicación Cloud Foundry y todas sus instancias.

Para ver los registros de una aplicación Cloud Foundry en Kibana, siga los pasos siguientes:

1. Inicie una sesión en {{site.data.keyword.Bluemix_notm}} y pulse el nombre de la app en el panel de control **Apps** de {{site.data.keyword.Bluemix_notm}}. Se abre la página de detalles de la app.
    
2. En la barra de navegación, pulse **Registros**. Se abre el separador Registros. 
    
3. Pulse **Vista avanzada**. Se abre el panel de control de **Kibana 3**.

Si no ve ningún registro, ajuste el selector de tiempo de la cabecera.

Para obtener más información sobre cómo personalizar un panel de control de Kibana, consulte [esta publicación del blog](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/) o la documentación de [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html).

##  Cómo ir al panel de control de Kibana desde un navegador web
{: #launch_Kibana_from_browser}

La consulta que se utiliza para filtrar los datos que aparecen en el panel de control recupera las entradas de registro correspondientes a un espacio de la organización {{site.data.keyword.Bluemix}}. La información de registro que muestra el panel de control de Kibana incluye registros correspondientes a todos los recursos desplegados dentro del espacio de la organización {{site.data.keyword.Bluemix}} en la que ha iniciado la sesión.

Siga los pasos siguientes para abrir un panel de control de Kibana desde un navegador:

1. Abra [https://logmet.<span class="keyword" data-hd-keyref="DomainName">NombreDominio</span>](https://logmet.{DomainName}) para iniciar una sesión en la interfaz de usuario de Kibana.

2. Seleccione el separador **Kibana 3** para trabajar con Kibana 3. Seleccione el separador **Kibana 4** para trabajar con Kibana 4. Se abrirá el panel de control de Kibana predeterminado. 

Si no ve ningún registro, ajuste el selector de tiempo de la cabecera.

Para obtener más información sobre cómo personalizar un panel de control de Kibana, consulte [esta publicación del blog](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/) o la documentación de [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html).



## Filtrado de datos en un panel de control de Kibana
{: #filter_data_kibana_dashboard}

En {{site.data.keyword.Bluemix}}, puede analizar datos utilizando el panel de control predeterminado de Kibana que se proporciona por recurso o por espacio de {{site.data.keyword.Bluemix}}. De forma predeterminada, estos paneles de control muestran todos los datos disponibles correspondientes a las últimas 24 horas. Sin embargo, puede restringir la información mostrada a través del panel de control. Puede añadir consultas y filtros a un panel de control predeterminado y luego guardarlo para volverlo a utilizar en el futuro.

En un panel de control, puede añadir varias consultas y filtros. Una consulta defina un subconjunto de las entradas de registro.  Un filtro ajusta la selección de datos mediante la inclusión o exclusión de información. 

Para las apps Cloud Foundry, la lista siguiente muestra ejemplos de cómo filtrar datos:
* Si está buscando información en los registros que incluya términos clave, puede crear consultas para filtrar por esos términos. Con Kibana, puede comparar consultas visualmente en el panel de control. Para obtener más información, consulte [Filtrado de registros de la app Cloud Foundry con consultas en Kibana](kibana3/logging_kibana_query.html#logging_kibana_query).

* Si busca información dentro de un periodo de tiempo específico, puede filtrar datos dentro de un intervalo de tiempo. Para obtener más información, consulte [Filtrado de registros de la app Cloud Foundry por tiempo en Kibana](kibana3/logging_kibana_filter_by_time_period.html#logging_kibana_time_filter).

* Si está buscando información correspondiente a un determinado ID de específica, puede filtrar datos por ID de instancia. Para obtener más información, consulte [Filtrado de los registros de la app Cloud Foundry por ID de instancia en Kibana](kibana3/logging_kibana_filter_by_instance_id.html#logging_kibana_instance_id) y [Filtrado de los registros de la app Cloud Foundry por ID de aplicación conocida en Kibana](kibana3/logging_kibana_filter_by_known_application_id.html#logging_kibana_known_application_id).

* Si está buscando información correspondiente a un determinado componente, puede filtrar datos por componente (tipo de registro). Para obtener más información, consulte [Filtrado de los registros de la app Cloud Foundry por tipo de registro en Kibana](kibana3/logging_kibana_filter_by_component.html#logging_kibana_component_filter).

* Si está buscando información, por ejemplo mensajes de error, puede filtrar datos por tipo de mensaje. Para obtener más información, consulte [Filtrado de los registros de la app Cloud Foundry por tipo de mensaje en Kibana](kibana3/logging_kibana_filter_by_message_type.html#logging_kibana_message_type_filter).

## Personalización de un panel de control de Kibana
{: #customize_kibana_dashboard}

Hay diferentes tipos de paneles de control que puede personalizar para visualizar y analizar los datos, por ejemplo:
* Panel de control Single-cf-app: es un panel de control que muestra información correspondiente a una sola aplicación Cloud Foundry.  
* Panel de control Multi-cf-app: es un panel de control que muestra información correspondiente a todas las aplicaciones Cloud Foundry desplegadas en el mismo espacio de {{site.data.keyword.Bluemix}}. 

Cuando personaliza un panel de control, puede configurar consultas y filtros para seleccionar un subconjunto de los datos de registro que desea mostrar en el panel de control.

Para visualizar los datos, puede configurar paneles. Kibana incluye distintos paneles, como tabla, tendencias e histograma, que puede utilizar para analizar la información. Puede añadir, eliminar y cambiar la disposición de los paneles del panel de control. El objetivo de cada panel varía. Algunos paneles se organizan en filas que proporcionan los resultados de una o varias consultas. Otros paneles muestran documentos o información personalizada. Por ejemplo, puede configurar un diagrama de barras, un diagrama circular o una tabla para visualizar los datos y analizarlos.  


## Cómo guardar un panel de control de Kibana
{: #save_Kibana_dashboard}

Siga los pasos siguientes para guardar un panel de control de Kibana después de personalizarlo:

1. En la barra de herramientas, pulse el icono **Guardar**.

2. Escriba un nombre para el panel de control.

    **Nota:** si intenta guardar un panel de control con un nombre que contenga espacios en blanco, no se guardará.

3. Junto al campo de nombre, pulse el icono **Guardar**.



## Análisis de registro mediante un panel de control de Kibana
{: #analyze_kibana_logs}

Después de personalizar un panel de control de Kibana, puede visualizar y analizar los datos a través de sus paneles. 

Para buscar información, puede anclar o desanclar consultas. 

* Puede anclar una consulta al panel de control y la búsqueda se activa automáticamente.
* Para eliminar contenido del panel de control, puede desactivar una consulta.

Para filtrar información, puede habilitar o inhabilitar filtros. 

* Puede marcar el recuadro de selección **Conmutar** ![Recuadro Conmutar para incluir un filtro](images/logging_toggle_include_filter.jpg) en un filtro para habilitarlo.   
* Puede deseleccionar el recuadro **Conmutar** ![recuadro Conmutar para que incluya un filtro](images/logging_toggle_exclude_filter.jpg) en un filtro para inhabilitarlo. 

Los gráficos y diagramas del panel de control muestran los datos. Puede utilizar los gráficos y diagramas del panel de control para supervisar los datos. 

Por ejemplo, para un panel de control Single-cf-app, el panel incluye información sobre una aplicación de Cloud Foundry. Los datos que puede visualizar y analizar se limitan a dicha app. Puede utilizar el panel de control para analizar datos correspondientes a todas las instancias de la app. Puede comparar instancias. Puede filtrar la información por ID de instancia. 

Puede definir y marcar una consulta para cada ID de instancia en el panel de control. 

![Panel de control con consultas marcadas](images/logging_kibana_dash_activate_query.jpg)

Luego puede activar o desactivar consultas individuales en función de la información de la instancia que desea ver en el panel de control. 

En la figura siguiente se muestra una consulta activada y otra desactivada:

![Panel de control con consultas marcadas](images/logging_kibana_dash_deactivate_query.jpg)

Si desea comparar 2 instancias de un histograma, puede definir dos consultas en el mismo panel de control, una para cada ID de instancia. Puede asignarles un alias y un color exclusivo para identificarlas fácilmente. Kibana gestiona varias consultas uniéndolas con un operador lógico OR. 

En la figura siguiente se muestra el panel para configurar un alias y un color para una consulta, para marcarla en el panel de control y para desactivarla:

![Asistente del panel de control para configurar una consulta](images/logging_kibana_query_def.jpg)



## Formato de registro de Kibana para aplicaciones de Cloud Foundry
{: #kibana_log_format_cf}

Puede configurar un panel de control de Kibana para que muestre los campos siguientes para cada entrada de registro:

<dl>
<dt><strong>@timestamp</strong></dt>
<dd>
<pre class="pre screen"><code>aaaa-MM-ddTHH:mm:ss:SS-0500</code></pre>
<p>La hora del suceso registrado. La indicación de fecha y hora se define hasta en milisegundos.</p>
</dd>

<dt><strong>@version</strong></dt>
<dd>
<p></p>
</dd>

<dt><strong>ALCH_TENANT_ID</strong></dt>
<dd>
<p>El ID del recurso de {{site.data.keyword.Bluemix_notm}}.</p>
</dd>

<dt><strong>_id</strong></dt>
<dd>
<p>El ID exclusivo del documento de registro.</p>
</dd>

<dt><strong>_index</strong></dt>
<dd>
<p>El índice de la entrada de registro.</p>
</dd>

<dt><strong>_type</strong></dt>
<dd>
<p>El tipo de registro; por ejemplo, <samp>syslog</samp>.</p>
</dd>

<dt><strong>app_name</strong></dt>
<dd>
<p>El nombre de la aplicación de {{site.data.keyword.Bluemix_notm}}.</p>
</dd>

<dt><strong>application_id</strong></dt>
<dd>
<p>El ID exclusivo de la aplicación de {{site.data.keyword.Bluemix_notm}}.</p>
</dd>

<dt><strong>host</strong></dt>
<dd>
<p>El nombre de la aplicación que ha generado los datos del registro.</p>
</dd>

<dt><strong>instance_id</strong></dt>
<dd>
<p>El ID de instancia de la instancia de aplicación que ha generado los datos de registro.</p>
</dd>

<dt><strong>module</strong></dt>
<dd>
<p></p>
</dd>

<dt><strong>loglevel</strong></dt>
<dd>
<p>La gravedad del suceso registrado.</p>
</dd>

<dt><strong>message</strong></dt>
<dd>
<pre class="pre screen"><code>&lt;<var class="keyword varname">Mensaje</var>&gt;</code></pre>
<p>Mensaje emitido por el componente. El mensaje varía en función del contexto.</p>
</dd>

<dt><strong>message_type</strong></dt>
<dd>
<pre class="pre screen"><code>OUT</code></pre>
<p>La secuencia en la que se escribe el mensaje de registro. <samp class="ph codeph">OUT</samp> hace referencia a la secuencia <samp class="ph codeph">stdout</samp> y <samp class="ph codeph">ERR</samp>, a la secuencia <samp class="ph codeph">stderr</samp>.</p>
</dd>

<dt><strong>org_id</strong></dt>
<dd>
<p>El ID exclusivo de la organización de {{site.data.keyword.Bluemix_notm}}.</p>
</dd>

<dt><strong>org_name</strong></dt>
<dd>
<p>El nombre de la organización de {{site.data.keyword.Bluemix_notm}} en la que se transfiere la app.</p>
</dd>

<dt><strong>origin</strong></dt>
<dd>
<p></p>
</dd>

<dt><strong>source_id</strong></dt>
<dd>
<pre class="pre screen"><code>[App/0]</code></pre>
<p>El componente que genera registros. En la siguiente lista se describen los registros de cada componente:</p>

<dl>
<dt><strong>API</strong></dt>
<dd>Respuestas registradas a llamadas de API que solicitan un cambio en el estado de la app.</dd>

<dt><strong>APP</strong></dt>
<dd>Respuestas registradas procedentes de la app.</dd>

<dt><strong>CELL</strong></dt>
<dd>Respuestas registradas procedentes de la célula de Diego que indican cuándo se inicia, se detiene o se cuelga una app.</dd>

<dt><strong>LGR</strong></dt>
<dd>Respuestas registradas de loggregator que indican problemas con el proceso de registro.</dd>

<dt><strong>RTR</strong></dt>
<dd>Respuestas registradas del componente direccionador cuando direcciona solicitudes HTTP a la app.</dd>

<dt><strong>SSH</strong></dt>
<dd>Respuestas registradas procedentes de la célula de Diego cuando un usuario accede a un contenedor de app mediante el mandato **cf ssh**.</dd>

<dt><strong>STG</strong></dt>
<dd>Respuestas registradas procedentes de la célula de Diego o de Droplet Execution Agent cuando el app se transfiere o se vuelve a transferir.</dd>
</dl>
</dd>

<dt><strong>space_name</strong></dt>
<dd>
<p>El nombre del espacio de {{site.data.keyword.Bluemix_notm}} en el que se transfiere la app.</p>
</dd>

<dt><strong>timestamp</strong></dt>
<dd>
<p>La hora del suceso registrado. La indicación de fecha y hora se define hasta en milisegundos.</p>
</dd>

<dt><strong>_type</strong></dt>
<dd>
<p>El tipo de registro, por ejemplo <samp>syslog</samp>.</p>
</dd>
</dl>




