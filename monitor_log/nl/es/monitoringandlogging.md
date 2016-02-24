{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Supervisión y registro
{: #monitoringandlogging}

*Última actualización: 8 de diciembre de 2015*

Al supervisar sus apps y revisar los registros, puede seguir la ejecución de la aplicación y el flujo de datos para comprender mejor su despliegue. Además, puede reducir el tiempo y esfuerzo necesarios para localizar cualquier problema y repararlo.
{:shortdesc}

Las app {{site.data.keyword.Bluemix}} se pueden distribuir ampliamente (app de varias instancias) y la ejecución de la aplicación y sus datos se puede compartir en varios servicios. En este entorno complejo, la supervisión de las apps y la revisión de los registros es importante para gestionar las app.

{{site.data.keyword.Bluemix_notm}} tiene un mecanismo de registro incorporado para producir archivos de registro para las app a medida que se ejecutan. En los registros puede ver los errores, avisos y mensajes informativos que se generan para la app. Además, también puede configurar la app para escribir mensajes de registro en el archivo de registro. Para obtener más información sobre los formatos de registro y sobre cómo ver los registros, consulte [Registro para apps {{site.data.keyword.Bluemix_notm}}](#logging_for_bluemix_apps).

La supervisión de la app le permite ver y controlar el despliegue de la aplicación. Con la supervisión puede llevar a cabo las siguientes tareas: 

* Recopilar y supervisar información de rendimiento para instancias de app y comprobar si son funcionales.
* Tener una mejor perspectiva de las operaciones de la aplicación (por ejemplo, detectar los posibles cuellos de botella o cuando se deben efectuar actualizaciones).
* Estimar los cargos y el uso de recursos.

Para las operaciones estables de sus despliegues en la plataforma {{site.data.keyword.Bluemix_notm}}, desea detectar problemas de inmediato y determinar las causas de forma eficiente. Para llevar a cabo este objetivo, tenga en cuenta la resolución de problemas a la hora de diseñar las app y utilice servicios o herramientas para la supervisión y el registro al desplegar la app en {{site.data.keyword.Bluemix_notm}}.

##Apps de supervisión en ejecución en Cloud Foundry
{: #monitoring_bluemix_apps}

Cuando utiliza la infraestructura Cloud Foundry para ejecutar sus apps en {{site.data.keyword.Bluemix_notm}}, desea mantenerse al día con la información del rendimiento (como, por ejemplo, el estado, el uso de recursos y las métricas de tráfico). Con esta información de rendimiento puede tomar decisiones o llevar a cabo acciones según convenga.

Para supervisar apps de {{site.data.keyword.Bluemix_notm}}, utilice uno de los siguientes métodos:

* Servicios de {{site.data.keyword.Bluemix_notm}}. Monitoring and Analytics ofrece un servicio que puede utilizar para supervisar el rendimiento de sus app. Además, este servicio también proporciona características como, por ejemplo, análisis de registros. Para obtener más información, consulte [Supervisión y análisis](../services/monana/index.html).
* Opciones de terceros. Por ejemplo, [New Relic](http://newrelic.com/){:new_window}.

##Registro para apps en ejecución en Cloud Foundry
{: #logging_for_bluemix_apps}

Los archivos de registro se crean automáticamente al utilizar la infraestructura Cloud Foundry para ejecutar sus apps en {{site.data.keyword.Bluemix_notm}}. Puede ver los registros desde el panel de control de {{site.data.keyword.Bluemix_notm}} o desde la interfaz de línea de mandatos cf. También puede filtrar los registros para ver aquellas secciones que le interesen.

###Formato de anotación
{: #log_format}

Los registros de las app {{site.data.keyword.Bluemix_notm}} se muestran en un formato fijo, parecido al siguiente patrón:

```
         1         2         3         4         5
12345678901234567890123456789012345678901234567890
--------------------------------------------------
yyyy-MM-ddTHH:mm:ss:SS-0500 [App/0]      OUT <message>
```
{:screen}

Cada entrada de registro contiene cuatro campos. Consulte la siguiente lista para obtener la descripción breve de cada campo:

<dl>
<dt><strong>Indicación de fecha y hora</strong></dt>
<dd>
<pre class="pre screen"><code>yyyy-MM-ddTHH:mm:ss:SS-0500</code></pre>
<p>Columns: 1 - 27</p>
<p>La hora de la sentencia de registro. La indicación de fecha y hora se define hasta en milisegundos.</p>
</dd>

<dt><strong>Componente</strong></dt>
<dd>
<pre class="pre screen"><code>[App/0]</code></pre>
<p>Columns: 29 - 40</p>
<p>El componente que genera registros. En la lista siguiente se proporciona la definición de todos los componentes:</p>

<dl>
<dt><strong>APP</strong></dt>
<dd>Aplicación. El componente APP va seguido de una barra inclinada y un dígito que indica la instancia de la aplicación, donde 0 es la primera instancia, 1 es la segunda, y así sucesivamente.</dd>

<dt><strong>API</strong></dt>
<dd>API de Cloud Foundry.</dd>

<dt><strong>DEA</strong></dt>
<dd>Droplet Execution Agent.</dd>

<dt><strong>LGR</strong></dt>
<dd>Loggregator.</dd>

<dt><strong>RTR</strong></dt>
<dd>Router.</dd>

<dt><strong>STG</strong></dt>
<dd>Transferencia. </dd>
</dl>
</dd>

<dt><strong>Secuencia</strong></dt>
<dd>
<pre class="pre screen"><code>OUT</code></pre>
<p>Columns: 42 - 44</p>
<p>La secuencia en la que se escribe el mensaje de registro. <samp class="ph codeph">OUT</samp> hace referencia a la secuencia <samp class="ph codeph">stdout</samp> y <samp class="ph codeph">ERR</samp>, a la secuencia <samp class="ph codeph">stderr</samp>.</p>
</dd>

<dt><strong>Mensaje</strong></dt>
<dd>
<pre class="pre screen"><code>&lt;<var class="keyword varname">Mensaje</var>&gt;</code></pre>
<p>Columns: 46 - end of line</p>
<p>Mensaje emitido por el componente. El mensaje varía en función del contexto.</p>
</dd>

</dl>

###Visualización de registros
{: #viewing_logs}

Puede utilizar el panel de control de {{site.data.keyword.Bluemix_notm}} o la interfaz de línea de mandatos para ver los registros.

####VISUALIZACIÓN DE REGISTROS DESDE EL PANEL DE CONTROL DE {{site.data.keyword.Bluemix_notm}}

Para ver los registros **Despliegue** o **Tiempo de ejecución**, lleve a cabo los siguientes pasos:
1. Pulse el mosaico de la app. Se mostrará la página de detalles de la app.
2. En la barra de navegación izquierdo, pulse **Registros**.

####VISUALIZACIÓN DE REGISTROS DESDE LA INTERFAZ DE LÍNEA DE MANDATOS

Elija una de las siguientes opciones para ver los registros desde la interfaz de línea de mandatos:

<ul>
<li>Seguimiento de los registros al desplegar apps.
<p>Utilice el mandato **cf logs** para mostrar registros desde la app y desde los componentes del sistema que interactúan con la app al desplegar apps en {{site.data.keyword.Bluemix_notm}}. Puede escribir los siguientes mandatos en la interfaz de línea de mandatos cf. Para obtener más información sobre los registros cf, consulte [Tipos de registro y sus mensajes en Cloud Foundry](http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html){:new_window}.</p>
<dl>
<dt><strong>cf logs <var class="keyword varname">nombreapp</var> --recent</strong></dt>
<dd>Visualizar registros recientes.</dd>

<dt><strong>cf logs <var class="keyword varname">nombreapp</var></strong></dt>
<dd>Visualizar registros que se generan desde el momento en que se ejecuta este mandato.</dd>
</dl>
<div class="note tip"><span class="tiptitle">Consejo:</span> Cuando ejecute el mandato <span class="keyword cmdname">cf push</span> or <span class="keyword cmdname">cf
start</span> en una ventana de línea de mandatos, puede escribir <samp class="ph codeph">cf
logs appname --recent</samp> en otra ventana de línea de mandatos para ver los
registros en tiempo real. </div>
</li>

<li>Visualización de registros después de desplegar las apps.

<p>Si el registro de la aplicación está habilitado, puede ver los siguientes registros de aplicación si se detectan problemas con la app en tiempo de ejecución. Los registros de aplicación pueden ayudarle a determinar la causa del error.</p>

<dl><strong>buildpack.log</strong></dt>
<dd>
<p>Este archivo de registro registra sucesos informativos detallados para la depuración. Puede utilizar este registro para resolver problemas de ejecución del paquete de compilación.</p>
<p>Para generar datos en el archivo <span class="ph filepath">buildpack.log</span> debe habilitar el rastreo del paquete de compilación mediante el mandato siguiente:
<pre class="pre">cf set-env <var class="keyword varname">nombre_app</var> JBP_LOG_LEVEL DEBUG</pre>
<p>
<p>Para ver este registro, ejecute el siguiente mandato:<pre class="pre">cf files <var class="keyword varname">nombre_app</var> app/.buildpack-diagnostics/buildpack.log</pre>
</p>
</dd>

<dt><strong>staging_task.log</strong></dt>
<dd><p>Este archivo de registro registra mensajes después de los principales pasos de la tarea de transferencia. Puede utilizar este registro para resolver problemas de transferencia.</p>
<p>Para ver este registro, ejecute el siguiente mandato:<pre class="pre">cf files <var class="keyword varname">nombre_app</var> logs/staging_task.log</pre>
</p>
</dd>
</dl>
</li></ul>


**Nota:** Para obtener información sobre cómo habilitar el registro de aplicación, consulte [Depuración de errores de tiempo de ejecución](../troubleshoot/debugging.html#debug_runtime).

###Filtrado de registros
{: #filtering_logs}

Para ver los registros en los que está interesado o para excluir el contenido que no desea ver, puede utilizar el mandato **cf logs** con opciones de filtrado, como por ejemplo,**cut** y **grep** en la interfaz de línea de mandatos cf.

* Para ver una parte en lugar de todos los registros detallados, utilice la opción **cut**. Por ejemplo, para visualizar la información de los componentes y de los mensajes, utilice el mandato siguiente:
```
cf logs appname --recent | cut -c 29-40,46- 
```

Para obtener más información sobre la opción **grep**, escriba cut --help.
* Para visualizar las entradas de registro que contienen ciertas palabras clave, utilice la opción **grep**. Por ejemplo, para visualizar las entradas de registro que contienen la palabra clave [APP, puede utilizar el mandato siguiente:
```
cf logs appname --recent | grep '\[App'
```
Para obtener más información sobre la opción **grep**, escriba `grep --help`.

###Configuración del registro de terceros
{: #thirdparty_logging}

{{site.data.keyword.Bluemix_notm}} mantiene una cantidad limitada de información de registro en la memoria. Cuando se registra información, la información antigua se sustituye por la nueva. Para mantener toda la información de registro, puede guardar los registros en un servicio de gestión de registros de terceros.

Para transferir los registros de la aplicación y del sistema a un servicio de gestión de registros de terceros, siga estos pasos:

1. Registre un servicio de gestión de registros de terceros.
    
    Puede utilizar cualquier servicio de gestión de registros de terceros que dé soporte al [protocolo syslog](http://tools.ietf.org/html/rfc5424){:new_window}, como por ejemplo Papertail, Splunk Storm, SumoLogic y Logentries. Registre un servicio de gestión de registros de terceros y configure el servicio para que proporcione un destino para los registros en {{site.data.keyword.Bluemix_notm}}. Después de completar la configuración, el servicio suele proporcionarle un URL de syslog como destino de sus registros en {{site.data.keyword.Bluemix_notm}}. Para obtener información sobre cómo configurar servicios de gestión de registros de terceros, consulte [Configuración de determinados servicios de gestión de registros de terceros](http://docs.cloudfoundry.org/devguide/services/log-management-thirdparty-svc.html){:new_window}.

2. Cree un a instancia de servicio proporcionada por el usuario.
	
	Para transferir los registros de {{site.data.keyword.Bluemix_notm}} al servicio de gestión de registros de terceros, primero debe crear una instancia de servicio proporcionada por el usuario. Utilice el siguiente mandato para crear una instancia de servicio proporcionada por el usuario, donde nombre_servicio es el nombre de la instancia de servicio proporcionada por el usuario y URL_syslog es el URL obtenido del servicio de registro de terceros. 
	
	```
	cf create-user-provided-service <nombre_servicio> -l <URL_syslog>
	```
	
3. Enlace la instancia de servicio a la aplicación.

	Utilice el mandato siguiente para enlazar la instancia de servicio a la aplicación, donde nombre_app es el nombre de la aplicación y nombre_servicio es el nombre de la instancia de servicio proporcionada por el usuario. 
	
	```
	cf bind-service nombreapp <nombre_servicio>
	```
	
	A continuación se le solicitará que vuelva a transferir la aplicación escribiendo cf restage nombre_app para que los cambios entren en vigor. Cuando se generen registros, podrá ver mensajes parecidos en el servicio de gestión de registros de terceros tras un breve intervalo de tiempo.

**Nota:** Los registros que ve en la interfaz de línea de mandatos no tienen el formato de syslog y es posible que no coincidan exactamente con los mensajes que se muestran en los servicios de gestión de registros de terceros.
