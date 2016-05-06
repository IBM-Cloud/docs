---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Personalización del JRE
{: #customizing_jre}

*Última actualización: 23 de marzo de 2016*

Las aplicaciones se ejecutan en entorno de tiempo de ejecución Java (JRE), proporcionado y configurado por el paquete de compilación de Liberty. El paquete de compilación de Liberty también permite configurar la versión o el tipo de JRE, personalizar las opciones de JVM o solapar las funciones de JRE.

## IBM JRE

De forma predeterminada, las aplicaciones se configuran para ejecutarse con una versión reducida de IBM JRE. Esta versión ligera de JRE se ha limitado para ofrecer la función esencial con una ocupación de memoria y de disco mucho más reducida. Para obtener más información sobre el contenido del JRE ligero, consulte [Tiempo de ejecución de Liberty for Java](http://download.boulder.ibm.com/ibmdl/pub/software/dw/jdk/docs/bluemix/libertyforjava_jre.doc.html).

Se utiliza IBM JRE versión 8 de forma predeterminada. Utilice la variable de entorno JBP_CONFIG_IBMJDK para especificar una versión alternativa de IBM JRE. Por ejemplo, para utilizar la versión más reciente de IBM JRE 7.1, establezca la variable de entorno siguiente:
```
    $ cf set-env myapp JBP_CONFIG_IBMJDK "version: 1.7.+"
```
{: #codeblock}

La propiedad de la versión se puede establecer en un rango de versiones. Hay dos rangos de versiones admitidos: 1.7.+ y 1.8.+. Para obtener los mejores resultados, utilice Java 8.

## OpenJDK
{: #openjdk}

De forma opcional, las aplicaciones se pueden configurar para ejecutarse con OpenJDK como JRE. Para permitir que una aplicación se ejecute con OpenJDK, establezca la variable de entorno JVM en "openjdk". Por ejemplo, con la herramienta de línea de mandatos cf, ejecute el mandato:
```
    $ cf set-env myapp JVM 'openjdk'
```
{: #codeblock}

Si está habilitado, se utiliza OpenJDK versión 8 de forma predeterminada. Utilice la variable de entorno JBP_CONFIG_OPENJDK para especificar una versión alternativa de OpenJDK. Por ejemplo, para utilizar la versión más reciente de OpenJDK 7, establezca la siguiente variable de entorno:
```
    $ cf set-env myapp JBP_CONFIG_OPENJDK "version: 1.7.+"
```
{: #codeblock}

La propiedad de la versión se puede establecer en un rango de versiones como 1.7.+ o cualquier versión específica listada en la [lista de versiones de OpenJDK disponibles](https://download.run.pivotal.io/openjdk/lucid/x86_64/index.yml). Para obtener los mejores resultados, utilice Java 8.

## Configuración de las opciones de JRE
{: #configuring_jre}

### Configuración predeterminada de JVM
{: #jvm_default_config}

El paquete de compilación de Liberty configura las opciones predeterminadas de JVM teniendo en cuenta los siguientes aspectos:

* Límite de memoria de una aplicación.  Los valores aplicados del almacenamiento dinámico de JVM se calculan en función de:
  * el límite de memoria de una aplicación, tal y como se detalla en [Límites de memoria y el paquete de compilación de Liberty](memoryLimits.html#memory_limits)
  * el tipo de JRE, ya que las opciones del almacenamiento dinámico de la JVM pueden variar en función de las opciones admitidas de JRE.

* Las [Características de Liberty soportadas en Bluemix](libertyFeatures.html#libertyfeatures).
  * No se admiten las transacciones de bases de datos globales de confirmación en dos fases en Bluemix y, por lo tanto, quedan inhabilitadas mediante el valor -Dcom.ibm.tx.jta.disable2PC=true.

* El entorno de Bluemix.

    Las opciones de JVM se configuran para proporcionar optimización en un entorno de Bluemix y para ayudar en los diagnósticos de las condiciones de error relacionadas con la memoria.
  * El error y la recuperación rápidos de una aplicación se configuran inhabilitando las opciones de volcado de JVM y la interrupción de los procesos cuando se agota la memoria de una aplicación.
  * ajuste de la virtualización (solo para IBM JRE).
  * direccionamiento de la información en los recursos de memoria disponible de la aplicación en el momento de producirse el error en Loggregator.
  * si se ha configurado una aplicación para habilitar los volcados de memoria de JVM, se inhabilitará la interrupción de los procesos Java, y los volcados de memoria de JVM se direccionan a un directorio común "volcados" de la aplicación. Estos volcados pueden visualizarse desde el panel de control de Bluemix o la interfaz de línea de mandatos (CLI) CF.

A continuación se muestra una configuración de JVM predeterminada de ejemplo que se genera con el paquete de compilación para una aplicación desplegada con un límite de memoria de 512 M:
```
    -Xtune:virtualized
    -Xmx384M
    -Xdump:none
    -Xdump:heap:defaults:file=../../../../../dumps/heapdump.%Y%m%d.%H%M%S.%pid.%seq.phd
    -Xdump:java:defaults:file=../../../../../dumps/javacore.%Y%m%d.%H%M%S.%pid.%seq.txt
    -Xdump:snap:defaults:file=../../../../../dumps/Snap.%Y%m%d.%H%M%S.%pid.%seq.trc
    -Xdump:tool:events=systhrow,filter=java/lang/OutOfMemoryError,request=serial+exclusive,exec=../../../../.buildpack-diagnostics/killjava.sh
    -Dcom.ibm.tx.jta.disable2PC=true
```
{: #codeblock}

### Personalización de la configuración de JVM
{: #customizing_jvm}

Las aplicaciones pueden personalizar las opciones de JVM con las especificaciones definidas por el JRE configurado para la aplicación. Haga referencia a las directrices sobre cómo especificar una opción y su uso directamente desde la documentación del JRE, ya que las opciones pueden variar en función del JRE.

<table>
<tr>
<th align="left">JRE</th>
<th align="left">Formato de opciones de línea de mandatos</th>
<th align="left">Referencia</th>
</tr>

<tr>
<td>IBM JRE</td>
<td>incluye opciones de tiempo de ejecución (con el prefijo -X), cualquier propiedad de sistema Java (con el prefijo -D) y no recomienda -XX para un uso casual (estas opciones están sujetas a cambios)
</td>
<td>[Opciones de línea de mandatos de Versión 8](http://www-01.ibm.com/support/knowledgecenter/SSYKE2_8.0.0/com.ibm.java.lnx.80.doc/diag/appendixes/cmdline/cmdline.html), [opciones de línea de mandatos de Versión 7](http://www-01.ibm.com/support/knowledgecenter/SSYKE2_7.0.0/com.ibm.java.lnx.70.doc/diag/appendixes/cmdline/cmdline.html)
</td>
</tr>

<tr>
<td> OpenJDK </td>
<td>se basa en el tiempo de ejecución de HotSpot que tiene la notación de -X para no estándar, -XX para las opciones de desarrollador y los distintivos booleanos para habilitar o inhabilitar la opción </td>
<td>[Visión general del tiempo de ejecución de HotSpot](http://openjdk.java.net/groups/hotspot/docs/RuntimeOverview.html) </td>
</tr>
</table>

Una aplicación que requiere opciones personalizadas de JVM puede definir la opción como valor de una de las variables de entorno IBM_JAVA_OPTIONS, JAVA_OPTS o JVM_ARGS en Bluemix. Consulte la sección Variables de entorno sobre cómo definir la variable de entorno de una aplicación. Un servidor empaquetado o directorio de servidores también puede incluir un archivo jvm.options
que contenga las opciones de línea de mandatos en lugar de definir una variable de entorno.

Al aplicarse las opciones de JVM al JRE, las opciones predeterminadas del paquete de compilación de Liberty se aplican en primer lugar, y posteriormente se aplican las opciones personalizadas. Las opciones personalizadas se añaden en un orden específico, que se detalla en la tabla. La secuencia de las opciones de Java aplicadas define las opciones que tienen prioridad. Las opciones que se aplican en último lugar tienen prioridad sobre las opciones aplicadas anteriormente.

Nota: Es posible que algunas opciones no surtan efecto a no ser que las desencadene un agente.

<table>
<tr>
<th align="left">Orden de aplicación</th>
<th align="left">Valor de opciones de JVM de la aplicación</th>
<th align="left">Descripción</th>
<th align="left">Tipo de aplicación admitido</th>
<th align="left">Para actualizar la opción de JVM de una aplicación desplegada</th>
<th align="left">Aplicable a OpenJDK JRE</th>
</tr>

<tr>
<td>1</td>
<td>IBM_JAVA_OPTIONS</td>
<td>una variable de entorno admitida por IBM JRE</td>
<td>Todos</td>
<td>Reinicie o vuelva a transferir la aplicación</td>
<td>No</td>
</tr>

<tr>
<td>2</td>
<td>JAVA_OPTS</td>
<td>una variable de entorno a través de la infraestructura de opciones Java del paquete de compilación de Liberty</td>
<td>Todos</td>
<td>Vuelva a transferir la app</td>
<td>Sí</td>
</tr>

<tr>
<td>3</td>
<td>jvm.options</td>
<td>un archivo de configuración de JVM admitido por el servidor empaquetado o directorio de servidores de tiempo de ejecución de Liberty</td>
<td>Paquete de servidor</td>
<td>Vuelva a transferir la app</td>
<td>Sí</td>
</tr>

<tr>
<td>4</td>
<td>JVM_ARGS</td>
<td>una variable de entorno admitida por el tiempo de ejecución de Liberty</td>
<td>Todos</td>
<td>Reinicie o vuelva a transferir la app</td>
<td>Sí</td>
</tr>
</table>

### Determinación de las opciones de JVM aplicadas de una aplicación en ejecución
{: #determining_applied_jvm_options}

A excepción de las opciones definidas por la aplicación especificadas con la variable de entorno JVM_ARGS, las opciones resultantes se persisten en el entorno de ejecución como opciones de línea de mandatos (aplicaciones Java autónomas) o en un archivo jvm.options (aplicaciones Java no autónomas). Las opciones de JVM aplicadas de la aplicación se pueden visualizar desde el panel de control de Bluemix o la interfaz de línea de mandatos (CLI) CF.

Las opciones JVM para la aplicación Java autónoma se mantienen como opciones de línea de mandatos. Se pueden visualizar en el archivo staging_info.yml.
```
    $ cf files myapp staging_info.yml
```
{: #codeblock}

Las opciones para despliegue de WAR, EAR, directorio de servidor y servidor empaquetado se mantienen en un archivo jvm.options.

Para ver el archivo jvm.options para WAR, EAR y directorio de servidor, ejecute el mandato:
```
    $ cf files myapp app/wlp/usr/servers/defaultServer/jvm.options
```
{: #codeblock}

Para ver el archivo jvm.options para un servidor empaquetado, sustituya <serverName> por el nombre de su servidor y ejecute el mandato:
```
    $ cf files myapp app/wlp/usr/servers/<serverName>jvm.options
```
{: #codeblock]

#### Uso de ejemplo
{: #example_usage}

Despliegue de una aplicación con las opciones personalizadas de JVM para habilitar el registro de recogida de basura detallada de JVM de IBM JRE:
* Las opciones de JVM incluidas en el archivo manifest.yml de una aplicación:
```
    env:
      JAVA_OPTS: "-verbose:gc -Xverbosegclog:./verbosegc.log,10,1000"
```
{: #codeblock}

* Para visualizar el registro generado de recogida de basura detallada de JVM:
```
    $ cf files myapp app/wlp/usr/servers/defaultServer/verbosegc.log.001
```
{: #codeblock}    

* Actualización de la opción de JVM de IBM JRE de una aplicación desplegada para desencadenar un heap, snap y javacore en una condición OutOfMemory:

Defina la variable de entorno de la aplicación con la opción de JVM y reinicie la aplicación:
```
    $ cf set-env myapp JVM_ARGS '-Xdump:heap+java+snap:events=systhrow,filter=java/lang/OutOfMemoryError'
    $ cf restart myapp
```
{: #codeblock}

* Para visualizar los volcados de JVM generados al desencadenarse la condición de falta de memoria:
```
    $ cf files myapp dumps

    Getting files for app myapp in org myemail@email.com / space dev as myemail@email.com...
    OK

    Snap.20141106.100252.81.0003.trc           307.3K
    heapdump.20141106.100252.81.0001.phd       3.9M
    javacore.20141106.100252.81.0002.txt     870.5K
```
{: #codeblock}

### Superposición del JRE
{: #overlaying_jre}

En algunos casos es necesario empaquetar los archivos con el JRE para disponer de su funcionalidad. El desarrollador de aplicaciones puede suministrar archivos JRE para su personalización.

Los archivos que se deben solapar se pueden empaquetar con el archivo WAR, EAR o JAR de la aplicación en una carpeta de recursos en la raíz del archivo. En el caso de un servidor (archivo comprimido o directorio del servidor), los archivos se pueden empaquetar en una carpeta de recursos en el directorio del servidor, con el archivo server.xml.

* archivo WAR
  * WEB-INF
  * resources
    * otros archivos
    * .java-overlay


* archivo EAR
  * META-INF
  * resources
    * otros archivos
    * .java-overlay


* archivo JAR
  * META-INF
  * resources
    * otros archivos
    * .java-overlay


* server_name DIR
  * apps
  * dropins
  * server.xml
  * resources
    * otros archivos
    * .java-overlay

El directorio .java-overlay contiene archivos específicos en la misma jerarquía de archivos que el Java JRE que se está solapando, empezando por .java/jre.

Por ejemplo, si desea utilizar el cifrado AES de 256 bits, tiene que solapar estos archivos de política de Java:
```
    .java\jre\lib\security\US_export_policy.jar
    .java\jre\lib\security\local_policy.jar
```
{: #codeblock}

Descargue los archivos de política sin restricciones adecuados y añádalos a su aplicación como:
```
    resources\.java-overlay\.java\jre\lib\security\US_export_policy.jar
    resources\.java-overlay\.java\jre\lib\security\local_policy.jar
```
{: #codeblock}

Cuando envíe la aplicación, estos archivos jar solaparán los archivos jar de política predeterminados en el tiempo de ejecución de Java. Este proceso habilita el cifrado AES de 256 bits.

# rellinks
## general
* [Tiempo de ejecución de Liberty](index.html)
* [Visión general del perfil de Liberty](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
