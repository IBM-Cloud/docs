---

copyright:
  years: 2015, 2016

---


{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Supervisión y registro
{: #monitoringandlogging}

*Última actualización: 11 de mayo de 2016*

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

Los archivos de registro se crean automáticamente al utilizar la infraestructura Cloud Foundry para ejecutar sus apps en {{site.data.keyword.Bluemix_notm}}. Cuando encuentra errores en cualquier etapa del despliegue al tiempo de ejecución, puede
comprobar los registros en busca de pistas que pudieran ayudar a solucionar su problema.

<!-- 2016.1.27: original shortdes: Log files are automatically created when you are using the Cloud Foundry infrastructure to run your apps on {{site.data.keyword.Bluemix_notm}}. You can view logs from the {{site.data.keyword.Bluemix_notm}} Dashboard, the cf command line interface, or external hosts. You can also filter the logs to see the parts that you are interested in. -->



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
<dd>Transferencia.</dd>
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

Puede ver los registros para sus app Cloud Foundry  en tres lugares:

  * [Panel de control de {{site.data.keyword.Bluemix_notm}}](#viewing_logs_UI){:new_window}
  * [Interfaz de línea de mandatos](#viewing_logs_cli){:new_window}
  * [Host de registro externo](#thirdparty_logging){:new_window}

#### Visualización de registros desde el panel de control de {{site.data.keyword.Bluemix_notm}}
{: #viewing_logs_UI}

Para ver los registros de despliegue o de tiempo de ejecución, realice los pasos siguientes:
1. Inicie sesión en {{site.data.keyword.Bluemix_notm}}, y a continuación pulse en el icono de su app en el panel de control. Se mostrará la página de detalles de la app.
2. En la barra de navegación izquierdo, pulse **Registros**.

En la consola **Registros**, puede ver los registros recientes para su app o la parte más reciente de los registros en tiempo real. Además, puede filtrar registros por tipo de registro y canal.

**Notas:** Los registros no se conservan tras una detención anómala de la app o tras un nuevo despliegue.



#### Visualización de registros desde la interfaz de línea de mandatos
{: #viewing_logs_cli}

Elija una de las siguientes opciones para ver los registros desde la interfaz de línea de mandatos:

<ul>
<li>Seguimiento de los registros al desplegar apps.
<p>Utilice el mandato **cf logs** para mostrar registros desde la app y desde los componentes del sistema que interactúan con la app al desplegar apps en {{site.data.keyword.Bluemix_notm}}. Puede escribir los siguientes mandatos en la interfaz de línea de mandatos cf. Para obtener más información sobre los registros cf, consulte <a href="http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html" target="_blank">Tipos de registro y sus mensajes en Cloud Foundry</a> </p>
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
<p>Para ver este registro, ejecute el siguiente mandato:
<pre class="pre">cf files <var class="keyword varname">nombre_app</var> app/.buildpack-diagnostics/buildpack.log</pre>
</p>
</dd>

<dt><strong>staging_task.log</strong></dt>
<dd><p>Este archivo de registro registra mensajes después de los principales pasos de la tarea de transferencia. Puede utilizar este registro para resolver problemas de transferencia.</p>
<p>Para ver este registro, ejecute el siguiente mandato:
<pre class="pre">cf files <var class="keyword varname">nombre_app</var> logs/staging_task.log</pre>
</p>
</dd>
</dl>
</li></ul>


**Nota:** Para obtener información sobre cómo habilitar el registro de aplicación, consulte [Depuración de errores de tiempo de ejecución](../debug/index.html#debugging-runtime-errors).




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



### Configuración de hosts de registro externo
{: #thirdparty_logging}

{{site.data.keyword.Bluemix_notm}} mantiene una cantidad limitada de información de registro en la memoria. Cuando se registra información, la información antigua se sustituye por la nueva. Para mantener toda la información de registro, puede guardar los registros en un host de log externo, como un servicio de gestión de registros de terceros o en otro host.

Para enviar la secuencia de los registros de su app y el sistema a un host de registro externo, realice los pasos siguientes:

  1. Determine el punto final de registro. 
     
	 Puede enviar registros a un agregador de registros de terceros, como Papertrail, Splunk o Sumologic. También puede enviar
registros a un host de syslog, un host de syslog encriptado con TLS (Seguridad de la capa de transporte) o un punto final POST de HTTPS. Los métodos para
obtener los puntos finales del registro varían para los distintos hosts de registro.

  2. Cree un a instancia de servicio proporcionada por el usuario.
     
	 Utilice el mandato ```cf create-user-provided-service``` (o ```cups``, una versión abreviada del mismo)
para crear una instancia de servicio proporcionado por el usuario: 
	 ```
	 cf create-user-provided-service <nombre_servicio> -l <punto_final_registro>
	 ```
	 **nombre_servicio**
	 
	 El nombre de la instancia de servicio proporcionado por el usuario.
	 
	 **punto_final_registro**
	 
	 El punto final del registro al que {{site.data.keyword.Bluemix_notm}} envía los registros. Consulte la tabla siguiente
para sustituir *punto_final_registro* por su valor:
	 
	 <table>
     <thead>
     <tr>
     <th>Punto final de registro</th>
     <th>Mandato</th>
	 <th>Notas</th>
     </tr>
     </thead>
     <tbody>
     <tr>
     <td>host de syslog</td>
     <td>`cf cups my-logs -l syslog://HOST:PORT`</td>
	 <td>Por ejemplo, para habilitar el registro en Papertrail, escriba `cf cups my-logs -l syslog://<papertrail-url>`. Sustituya
`<papertrail-url>` por el URL de su punto final de registro de Papertrail.</td>
     </tr>
	 <tr>
     <td>syslog-tls host</td>
     <td>`cf cups my-logs -l syslog-tls://HOST:PORT`</td>
	 <td>El certificado debe ser de confianza para una autoridad de certificados. No utilice certificados autofirmados.</td>
     </tr>
	 <tr>
     <td>HTTPS POST</td>
     <td>`cf cups my-logs -l https://HOST:PORT`</td>
	 <td>Este punto final debe estar en Internet de forma pública, y accesible por {{site.data.keyword.Bluemix_notm}}</td>
     </tr>
     </tbody>
     </table>	
  3. Enlazar una instancia de servicio a la app.

	 Utilice el mandato siguiente para enlazar la instancia de servicio a su app: 
	
	 ```
	 cf bind-service nombreapp <nombre_servicio>
	 ```
	 **nombre_app**
	 
	 El nombre de su app.
	 
	 **nombre_servicio**
	 
	 El nombre de la instancia de servicio proporcionado por el usuario.
	 
  4. Volver a transferir la app. 
     Escriba ```cf restage appname``` para que los cambios surtan efecto. 

#### Visualización de registros de hosts externos
{: #viewing_logs_external}

	 
Cuando se generan los registros, tras un breve retardo, puede ver los mensajes en su host de registros externo, que es parecido a los mensajes
que ve desde la interfaz de usuario de {{site.data.keyword.Bluemix_notm}} o desde la interfaz de línea de mandatos cf.  Si tiene varias
instancias de su app, los registros se agregan y puede ver todos los registros de su app. Además, los registros se conservan
después de una detención anómala de la app, o tras su redespliegue.

**Nota:** Los registros que ve en la interfaz de línea de mandatos no tienen el formato de syslog y es posible que no coincidan exactamente con los mensajes que se muestran en su host de registro externo. 


