---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Supervisión y creación de registros con Cloud Foundry
{: #monitoringandlogging}


Mediante la supervisión de sus apps y la revisión de los registros, puede seguir la ejecución de una aplicación, el flujo de datos y el uso de las aplicaciones para comprender mejor su despliegue. Además, puede reducir el tiempo y el esfuerzo necesario para localizar los problemas y repararlos.
{:shortdesc}

Las aplicaciones de {{site.data.keyword.Bluemix}} se pueden distribuir ampliamente, pueden ser aplicaciones de múltiples instancias. También es posible compartir la ejecución de las aplicaciones y sus datos a lo largo de muchos servicios. En este entorno complejo, la supervisión de sus apps y la revisión de los registros es importante para gestionar dichas apps.

## Supervisión y creación de registros de apps de Cloud Foundry
{: #monitoring_logging_bluemix_apps}

{{site.data.keyword.Bluemix_notm}} tiene un mecanismo de registro incorporado para producir archivos de registro para las apps a medida que se ejecutan. En los registros puede ver los errores, avisos y mensajes informativos que se generan para la app. Además, también puede configurar la app para escribir mensajes de registro en el archivo de registro. Para obtener más información sobre los formatos de registro y cómo ver registros, consulte [Registro de apps que se ejecutan en Cloud Foundry](#logging_for_bluemix_apps).

La supervisión de la app le permite ver y controlar el despliegue de la app. Con la supervisión puede llevar a cabo las siguientes tareas:

* Recopilar y supervisar información de rendimiento para instancias de app y comprobar si son funcionales.
* Tener una mejor perspectiva de las operaciones de la aplicación (por ejemplo, detectar los posibles cuellos de botella o cuando se deben efectuar actualizaciones).
* Estimar los cargos y el uso de recursos.

Para las operaciones estables de sus despliegues en la plataforma {{site.data.keyword.Bluemix_notm}}, desea detectar problemas de inmediato y determinar las causas de forma eficiente. Para llevar a cabo este objetivo, tenga en cuenta la resolución de problemas a la hora de diseñar las apps y utilice servicios o herramientas para la supervisión y el registro al desplegar la app en {{site.data.keyword.Bluemix_notm}}.

### Apps de supervisión en ejecución en Cloud Foundry
{: #monitoring_bluemix_apps}

Cuando utiliza la infraestructura Cloud Foundry para ejecutar sus apps en {{site.data.keyword.Bluemix_notm}}, desea mantenerse al día con la información del rendimiento (como, por ejemplo, el estado, el uso de recursos y las métricas de tráfico). Con esta información de rendimiento puede tomar decisiones o llevar a cabo acciones según convenga.

Para supervisar apps de {{site.data.keyword.Bluemix_notm}}, utilice uno de los siguientes métodos:

* Servicios de {{site.data.keyword.Bluemix_notm}}. Monitoring and Analytics ofrece un servicio que puede utilizar para supervisar el rendimiento de sus aplicaciones. Además, este servicio también proporciona características analíticas como, por ejemplo, el análisis de registros. Para obtener más información, consulte [Supervisión y análisis](/docs/services/monana/index.html#gettingstartedtemplate).
* Opciones de terceros. Por ejemplo, [New Relic ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](http://newrelic.com/){:new_window}.

### Registro para apps en ejecución en Cloud Foundry
{: #logging_for_bluemix_apps}

Los archivos de registro se crean de forma automática cuando se utiliza la infraestructura de Cloud Foundry para ejecutar sus apps en {{site.data.keyword.Bluemix_notm}}. Cuando encuentra errores en una etapa, desde la etapa de despliegue a la de tiempo de ejecución, puede comprobar los registros para obtener indicios que le pueden ayudar a resolver dicho problema.


<!-- 2016.1.27: original shortdes: Log files are automatically created when you are using the Cloud Foundry infrastructure to run your apps on {{site.data.keyword.Bluemix_notm}}. You can view logs from the {{site.data.keyword.Bluemix_notm}} Dashboard, the cf command line interface, or external hosts. You can also filter the logs to see the parts that you are interested in. -->



### Formato de registro y retención
{: #log_format}

De forma predeterminada, en las apps públicas de Cloud Foundry de {{site.data.keyword.Bluemix_notm}}, los datos de los registros se almacenan durante 7 días. Puede buscar en hasta 1 GB de datos por día.

Los registros de las aplicaciones de {{site.data.keyword.Bluemix_notm}} se muestran en un formato fijo, parecido al del siguiente patrón:

```
         1         2         3         4         5
12345678901234567890123456789012345678901234567890
--------------------------------------------------
aaaa-MM-ddTHH:mm:ss:SS-0500 [App/0]      OUT <mensaje>
```
{:screen}

Cada entrada del registro contiene cuatro campos. Consulte la siguiente lista para obtener una descripción breve de cada campo:

<dl>
<dt><strong>Indicación de fecha y hora</strong></dt>
<dd>
<pre class="pre screen"><code>aaaa-MM-ddTHH:mm:ss:SS-0500</code></pre>
<p>Columnas: 1 - 27</p>
<p>La hora de la sentencia de registro. La indicación de fecha y hora se define hasta en milisegundos.</p>
</dd>

<dt><strong>Componente</strong></dt>
<dd>
<pre class="pre screen"><code>[App/0]</code></pre>
<p>Columnas: 29 - 40</p>
<p>El componente que genera registros. </p>
<p>Cada tipo de componente va seguido de una barra inclinada y un dígito que indica la instancia de la aplicación. 0 es el dígito asignado a la primera instancia, 1 es el dígito asignado a la segunda, y así sucesivamente.</p>
<p>La siguiente lista destaca los distintos tipos de componentes:</p>

<dl>
<dt><strong>LGR</strong></dt>
<dd>Loggregator: El componente LGR proporciona información sobre el servicio de creación de registros.</dd>

<dt><strong>RTR</strong></dt>
<dd>RTR: El componente RTR proporciona información sobre las solicitudes HTTP enviadas a una aplicación.</dd>

<dt><strong>STG</strong></dt>
<dd>Staging: El componente STG proporciona información sobre cómo se transfiere o se vuelve a transferir una aplicación.</dd>

<dt><strong>APP</strong></dt>
<dd>Application: El componente APP proporciona información sobre una aplicación.</dd>

<dt><strong>API</strong></dt>
<dd>Cloud Foundry API: El componente API proporciona información sobre las acciones internas resultantes de la solicitud de un usuario de cambiar el estado de una aplicación.</dd>

<dt><strong>DEA</strong></dt>
<dd>Droplet Execution Agent: El componente DEA proporciona información sobre el inicio, detención o bloqueo de una aplicación. 
<p>Este componente sólo está disponible si la aplicación se ha desplegado en la arquitectura de Cloud Foundry que se basa en DEA.</p></dd>

<dt><strong>CELL</strong></dt>
<dd>Digo Cell: El componente CELL proporciona información sobre el inicio, detención o bloqueo de una aplicación. 
<p>Este componente sólo está disponible si la aplicación se ha desplegado en la arquitectura de Cloud Foundry que se basa en Diego.</p></dd>

<dt><strong>SSH</strong></dt>
<dd>SSH: El componente SSH proporciona información cada vez que un usuario accede a una aplicación con el mandato **cf ssh**. 
<p>Este componente sólo está disponible si la aplicación se ha desplegado en la arquitectura de Cloud Foundry que se basa en Diego.</p></dd>

</dl>
</dd>

<dt><strong>Secuencia</strong></dt>
<dd>
<pre class="pre screen"><code>OUT</code></pre>
<p>Columnas: 42 - 44</p>
<p>La secuencia en la que se escribe el mensaje de registro. <samp class="ph codeph">OUT</samp> hace referencia a la secuencia <samp class="ph codeph">stdout</samp> y <samp class="ph codeph">ERR</samp>, a la secuencia <samp class="ph codeph">stderr</samp>.</p>
</dd>

<dt><strong>Mensaje</strong></dt>
<dd>
<pre class="pre screen"><code>&lt;<var class="keyword varname">Mensaje</var>&gt;</code></pre>
<p>Columnas: 46 - final de línea</p>
<p>Mensaje emitido por el componente. El mensaje varía en función del contexto.</p>
</dd>
</dl>

En la figura siguiente se muestran los distintos componentes (tipos de registro) en una arquitectura Cloud Foundry que se basa en Droplet Execution Agent (DEA): ![Tipos de registro en una arquitectura DEA. ](images/logging_F1.png "Componentes (tipos de registro) en una arquitectura Cloud Foundry que se basa en Execution Agent (DEA).")


## Visualización de registros
{: #viewing_logs}

Los registros de las apps de Cloud Foundry se pueden visualizar en cuatro lugares:

  * Panel de control de {{site.data.keyword.Bluemix_notm}}
  * Panel de control de Kibana
  * Interfaz de línea de mandatos
  * Hosts de registros externos

### Visualización de registros desde el panel de control de {{site.data.keyword.Bluemix_notm}}
{: #viewing_logs_UI}

Para ver los registros de despliegue o de tiempo de ejecución, realice los pasos siguientes:
1. Inicie una sesión en {{site.data.keyword.Bluemix_notm}} y, a continuación, pulse en el mosaico de su app. Se muestra la página de detalles de la app.
2. En la barra de navegación, pulse **Registros**.

En la consola **Registros**, puede ver los registros recientes para su app o la parte más reciente de los registros en tiempo real. Además, puede filtrar registros por tipo de registro y canal.

**Nota:** Los registros no se conservan entre despliegues y cuelgues de app.


### Visualización de registros desde el panel de control de Kibana
{: #viewing_logs_Kibana}

Cree un panel de control personalizado para visualizar, de una forma simple o elaborada, los registros de las apps que se ejecutan en un espacio.

1. Abra [https://logmet.<span class="keyword" data-hd-keyref="DomainName">NombreDominio</span>](https://logmet.{DomainName}) para iniciar una sesión en la interfaz de usuario de Kibana.
2. Seleccione el separador **Kibana 3**.
3. Si no ve ningún registro, ajuste el selector de tiempo de la cabecera.
4. Guarde el panel de control como un nuevo panel de control.
  1. En la barra de herramientas, pulse el icono **Guardar**.
  2. Escriba un nombre para el panel de control.
  3. Junto al campo de nombre, pulse el icono **Guardar**.

Para obtener más información sobre cómo personalizar un panel de control de Kibana, consulte [esta publicación del blog](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/) o la documentación de [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html).


### Visualización de registros desde la interfaz de línea de mandatos
{: #viewing_logs_cli}

Elija entre las siguientes opciones para visualizar registros desde la interfaz de línea de mandato:

<ul>
<li>Últimos registros al desplegar aplicaciones.
<p>Utilice el mandato **cf logs** para visualizar registros de su app y de componentes del sistema que interactúan con su app al desplegar apps en {{site.data.keyword.Bluemix_notm}}. Escriba los siguientes mandatos en la interfaz de línea de mandatos de cf. Para obtener más información sobre los registros de cf, consulte <a href="http://docs.cloudfoundry.org/devguide/deploy-apps/streaming-logs.html" target=" _blank">
Tipos de registro y sus mensajes en Cloud Foundry <img src="../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> </p>
<dl>
<dt><strong>cf logs <var class="keyword varname">nombreapp</var> --recent</strong></dt>
<dd>Visualiza registros recientes.</dd>

<dt><strong>cf logs <var class="keyword varname">nombreapp</var></strong></dt>
<dd>Visualiza registros generados desde el momento que ejecuta este mandato.</dd>
</dl>
<div class="note tip"><span class="tiptitle">Consejo:</span> Cuando ejecute el mandato <span class="keyword cmdname">cf push</span> o <span class="keyword cmdname">cf
start</span> en una ventana de línea de mandatos, puede escribir <samp class="ph codeph">cf
logs appname --recent</samp> en otra ventana de línea de mandatos para ver los
registros en tiempo real. </div>
</li>

<li>Visualización de registros después de que se hayan desplegado las apps.

<p>Si la creación de registros de una aplicación está habilitado, podrá ver los siguientes registros de aplicación si encuentra problemas con la app en tiempo de ejecución. Los registros de aplicación pueden ayudar a determinar la causa de los errores.</p>

<dl><dt><strong>buildpack.log</strong></dt>
<dd>
<p>Este archivo de registro registra sucesos informativos detallados para la depuración. Puede utilizar este registro para resolver problemas de ejecución del paquete de compilación.</p>
<p>Para generar datos en el archivo <span class="ph filepath">buildpack.log</span>, debe habilitar el rastreo del paquete de compilación mediante el siguiente mandato:
   <pre class="pre">cf set-env <var class="keyword varname">nombre_app</var> JBP_LOG_LEVEL DEBUG</pre></p>
<p>Especifique el siguiente mandato para visualizar este registro:
<pre class="pre">cf files <var class="keyword varname">nombre_app</var> app/.buildpack-diagnostics/buildpack.log</pre>
</p>
</dd>
<dt><strong>staging_task.log</strong></dt>
<dd><p>Este archivo de registro registra mensajes después de los principales pasos de la tarea de transferencia. Puede utilizar este registro para resolver problemas de transferencia.</p>
<p>Especifique el siguiente mandato para visualizar este registro:
<pre class="pre">cf files <var class="keyword varname">nombre_app</var> logs/staging_task.log</pre>
</p>
</dd>
</dl>
</li></ul>


**Nota:** Para obtener información sobre cómo habilitar el registro de aplicación, consulte [Depuración de errores de tiempo de ejecución](/docs/debug/index.html#debugging-runtime-errors).

### Visualización de registros desde hosts externos
{: #viewing_logs_external}


Cuando se generan los registros, tras un breve retraso, puede ver los mensajes en el host de registros externo. Los registros son parecidos a los mensajes que se ven desde la interfaz de usuario de {{site.data.keyword.Bluemix_notm}} cf o desde la interfaz de línea de mandatos de cf.  Si tiene varias instancias de su app, los registros se agregan y podrá ver todos los registros de su app. Además, los registros se conservan entre despliegues y cuelgues de app.

**Nota:** Registros que se visualizan en la interfaz de línea de mandatos no están en el formato syslog, y podrían no coincidir exactamente con los mensajes que se visualizan en su host de registros externo.




## Filtrado de registros desde la interfaz de línea de mandatos
{: #filtering_logs}

Para ver los registros en los que está interesado o para excluir el contenido que no desea ver, puede utilizar el mandato **cf logs** con opciones de filtrado, como por ejemplo,**cut** y **grep** en la interfaz de línea de mandatos cf.

* Para visualizar una parte en lugar de todos los registros detallados, utilice la opción **cut**. Por ejemplo, para visualizar la información del componente y el mensaje, utilice el mandato siguiente:
```
cf logs appname --recent | cut -c 29-40,46-
```

Para obtener más información sobre la opción **grep**, escriba cut --help.
* Para visualizar entradas de registro que contienen determinadas palabras claves, utilice la opción **grep**. Por ejemplo, para visualizar las entradas de registro que contienen la palabra clave `[APP`, puede utilizar el mandato siguiente:

```
cf logs appname --recent | grep '\[App'
```
Para obtener más información sobre la opción **grep**, escriba `grep --help`.



## Configuración de hosts de registro externo
{: #thirdparty_logging}

{{site.data.keyword.Bluemix_notm}} mantiene una cantidad limitada de información de registro en la memoria. Cuando se registra información, la información antigua se sustituye por la nueva. Para mantener toda la información de registro, puede guardar los registros de la aplicación en un host de registro externo, como un servicio de gestión de registros de terceros o en otro host.

Para enviar la secuencia de los registros de su app y del sistema a un host de registro externo, realice los pasos siguientes:

  1. Determine el punto final de registro.

	 Puede enviar registros a un agregador de registros de terceros, como Papertrail, Splunk o Sumologic. También puede enviar
registros a un host de syslog, un host de syslog encriptado con TLS (Seguridad de la capa de transporte) o un punto final POST de HTTPS. Los métodos para
obtener los puntos finales del registro varían para los distintos hosts de registro.

  2. Cree una instancia de servicio proporcionada por el usuario.

	 Utilice el mandato `cf create-user-provided-service` (o `cups`, una versión abreviada del mismo)
para crear una instancia de servicio proporcionado por el usuario:
	 ```
	 cf create-user-provided-service <nombre_servicio> -l <punto_final_registro>
	 ```
	 &lt;nombre_servicio&gt;

	 El nombre de la instancia de servicio proporcionado por el usuario.

	 &lt;punto_final_registro&gt;

	 El punto final del registro al que {{site.data.keyword.Bluemix_notm}} envía los registros. Consulte la tabla siguiente
para sustituir *punto_final_registro* por su valor:

	 <table>
	 <caption>Tabla 1. Valores de punto final de registro</caption>
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
	 cf bind-service <appname> <nombre_servicio>
	 ```
	 &lt;nombre_app&gt;

	 El nombre de su app.

	 &lt;nombre_servicio&gt;

	 El nombre de la instancia de servicio proporcionado por el usuario.

  4. Vuelva a transferir la app. Escriba `cf restage appname` para que se apliquen los cambios.


### Ejemplo: Envío de secuencia de registros de aplicaciones de Cloud Foundry a Splunk
{: #splunk}

En este ejemplo, Jane, una desarrolladora, creará un servidor virtual utilizando IBM Virtual Servers Beta y una imagen Ubuntu.  Jane intenta enviar una secuencia de registros de app de Cloud Foundry desde {{site.data.keyword.Bluemix_notm}} a Splunk.

  1. Lo primero que hace Jane es configurar Splunk.

     a. Jane descarga Splunk Light desde el [sitio de descarga de Splunk Light ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://www.splunk.com/en_us/download/splunk-light.html){:new_window} y, a continuación, lo instala con el siguiente mandato. El software se instala en */opt/splunk*.

	    ```
        dpkg -i  ~/splunklight-6.3.0-aa7d4b1ccb80-linux-2.6-amd64.deb
        ```

     b. Jane instala y aplica los parches al complemento de tecnología syslog de RFC5424 para realizar la integración con {{site.data.keyword.Bluemix_notm}}. Para obtener más información sobre cómo instalar el complemento, consulte [las directrices de Cloud Foundry ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.cloudfoundry.org/devguide/services/integrate-splunk.html){:new_window}.

	    Jane instala el complemento con los mandatos siguientes:

	    ```
        cd /opt/splunk/etc/apps
        tar xvfz ~/rfc5424-syslog_11.tgz
        ```

        A continuación, aplica los parches al complemento, sustituyendo */opt/splunk/etc/apps/rfc5424/default/transforms.conf* con el nuevo archivo *transforms.conf* que contiene el siguiente texto:

	    ```
        [rfc5424_host]
        DEST_KEY = MetaData:Host
        REGEX = <\d+>\d{1}\s{1}\S+\s{1}(\S+)
        FORMAT = host::$1

        [rfc5424_header]
        REGEX = <(\d+)>\d{1}\s{1}\S+\s{1}\S+\s{1}(\S+)\s{1}(\S+)\s{1}(\S+)
        FORMAT = prival::$1 appname::$2 procid::$3 msgid::$4
        MV_ADD = true
        ```
        {:screen}

     Una vez que Splunk está configurado, Jane debe abrir algunos puertos en la máquina Ubuntu para que acepte la obtención de los syslog entrantes (puerto 5140) y la interfaz de usuario web de Splunk (puerto 8000) porque de forma predeterminada el cortafuegos del servidor virtual de {{site.data.keyword.Bluemix_notm}} está activado.

	    **Nota:** La configuración de iptable se realiza aquí a efectos de la evaluación que Jane está realizando y es temporal. Para configurar los parámetros del cortafuegos en el servidor virtual Bluemix en producción, consulte la documentación de [Grupos de seguridad de red ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://new-console.ng.bluemix.net/docs/services/networksecuritygroups/index.html){:new_window} para obtener información más detallada.

	   ```
	   iptables -A INPUT -p tcp --dport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --sport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --dport 8000 -j ACCEPT
       iptables -A INPUT -p tcp --sport 8000 -j ACCEPT
	   ```
	   {:screen}

	   A continuación, Jane ejecuta Splunk utilizando el siguiente mandato:

       ```
	   /opt/splunk/bin/splunk start --accept-license
       ```

  2. Jane configura los valores de Splunk para aceptar la obtención de syslog desde {{site.data.keyword.Bluemix_notm}}. Debe crear una entrada de datos para la obtención de syslog.

     a. Desde la interfaz web de Splunk, Jane pulsa **Datos > Entrada de datos**. Se visualizará una lista de tipos de entrada a los que Splunk da soporte.

     b. Selecciona **TCP**, porque la obtención de syslog utiliza el protocolo TCP.

     c. En el panel de **TCP**, Jane especifica **5140** en el campo **Puerto**, deja los campos restantes en blanco y, a continuación, pulsa **Siguiente**.

     d. Desde la lista de **Tipo de origen**, selecciona **No categorizado > rfc5424_syslog**.

     e. Para el tipo de **Método**, selecciona **IP**.

     f. En el campo **Índice**, pulsa **Crear un nuevo índice**. Le otorga el nombre "bluemix" al nuevo índice y, a continuación, pulsa **Guardar**.

     g. Por último, en la ventana **Revisar**, confirma que los valores son correctos y pulsa **Enviar** para habilitar esta entrada de datos.

  3. En {{site.data.keyword.Bluemix_notm}}, Jane crea un servicio de obtención de syslog y vincula el servicio a una app.

     a. Jane crea un servicio de obtención de syslog utilizando el siguiente mandato desde la interfaz de línea de mandatos de cf:

     ```
     cf cups splunk -l syslog://dummyhost:5140
     ```

     **Nota:** *dummyhost* no es el nombre real. Se utiliza para ocultar el nombre de host real.

     b. Jane vincula el servicio de obtención de syslog a una app en su espacio y, a continuación, reconstruye la app.

	 ```
     cf bind-service myapp splunk
     cf restage myapp
     ```


Jane prueba su app y, a continuación, escribe la siguiente serie de consulta en la interfaz web de Splunk:

```
source="tcp:5140" index="bluemix" sourcetype="rfc5424_syslog"
```

Jane verá una secuencia de registros en su interfaz web de Splunk. A pesar de que la versión de Splunk que Jane instala es Splunk Light, todavía podrá retener hasta 500MB de registros al día.

## Registro para apps Cloud Foundry en {{site.data.keyword.Bluemix_dedicated_notm}} y {{site.data.keyword.Bluemix_local_notm}}
{: #hybrid_apps_logs_ov}


En {{site.data.keyword.Bluemix_dedicated_notm}} y {{site.data.keyword.Bluemix_local_notm}}, las apps Cloud Foundry se suministran con registro incorporado. Puede revisar los datos que recopilan las apps en la consola de {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

Las apps Cloud Foundry utilizan loggregator de Cloud Foundry para supervisar los registros desde fuera de la app. No es necesario que instale agentes dentro de la app.

### Requisitos de hardware


| **Requisito** |    **1 nodo**     | **3 nodos para la alta disponibilidad** |
|-----------------|-------------------|-------------------|
| vCPU | 19 | 57 |
| Memoria | 80 GB | 240 GB |
| Almacenamiento local | 2,98 TB | 8,94 TB |
{: caption="Tabla 2. Requisitos de hardware para la creación de registros para {{site.data.keyword.Bluemix_local_notm}}" caption-side="top"}

### Instalación

En {{site.data.keyword.Bluemix_dedicated_notm}} y {{site.data.keyword.Bluemix_local_notm}}, los registros están activos para todas de apps de forma predeterminada. Para obtener más información sobre cómo leer los registros estándares, consulte [Registro de apps que se ejecutan en Cloud Foundry](#logging_for_bluemix_apps). Además, el registro avanzado se puede habilitar en los entornos {{site.data.keyword.Bluemix_dedicated_notm}} y {{site.data.keyword.Bluemix_local_notm}}.

* Para confirmar que el registro avanzado está habilitado en los entornos {{site.data.keyword.Bluemix_dedicated_notm}} entornos y {{site.data.keyword.Bluemix_local_notm}}, siga los pasos del apartado [Visualización de registros](#hybrid_apps_logs_dash). Si no tiene el botón **Vista avanzada**, significa que esta función no está habilitada.

* Para añadir el registro avanzada al entorno, siga los pasos de la documentación de [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) o de [{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local).

### Retención de registros

En las apps de {{site.data.keyword.Bluemix_dedicated_notm}} y {{site.data.keyword.Bluemix_local_notm}} Cloud Foundry, los datos de registro se almacenan durante 30 días de forma predeterminada.

## Visualización de registros de apps Cloud Foundry en {{site.data.keyword.Bluemix_dedicated_notm}} y {{site.data.keyword.Bluemix_local_notm}}
{: #hybrid_apps_logs_dash}

Puede revisar los registros de las apps que ejecutan en {{site.data.keyword.Bluemix_dedicated_notm}} y {{site.data.keyword.Bluemix_local_notm}}.
{:shortdesc}

Para ver los registros de una app, siga estos pasos:
1. Seleccione una app en ejecución.
2. Pulse **Registros**. En la vista **Registros** puede ver los registros de la app en ejecución.
4. Pulse el botón **Vista avanzada**. **Vista avanzada** muestra una vista más detallada de los registros mediante Kibana, una herramienta de visualización que utiliza registros y datos con indicación de hora para crear visualizaciones personalizadas. Para obtener más información sobre cómo utilizar la vista avanzada, consulte la documentación de [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html).

Luego puede personalizar un panel de instrumentos de Kibana. Consulte [Personalización de la visualización de registros en un panel de control de Kibana](/docs/containers/monitoringandlogging/container_ml_logs.html#container_ml_dash_logs_custom) para obtener más información.
