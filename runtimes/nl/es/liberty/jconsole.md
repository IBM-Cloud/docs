---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Supervisión de Liberty en Bluemix con JConsole
{: #jconsole}

*Última actualización: 23 de marzo de 2016*

## A continuación se muestran los pasos para supervisar el tiempo de ejecución de Bluemix Liberty con JConsole:
{: #steps_to_monitor}

1. Envíe la app dentro de un paquete de servidor que contenga un archivo server.xml adecuado.
2. Inicie la app JConsole con las propiedades del sistema adecuadas en la línea de mandatos.
3. Especifique los valores URL de proceso remoto, Nombre de usuario y Contraseña adecuados en JConsole.

### Enviar el paquete de servidor
{: #push_server_package}

Envíe el paquete de servidor que contiene la aplicación, limitándolo a una sola instancia. El archivo server.xml debe contener las características `monitor-1.0` y `restConnector-1.0`. También debe contener un elemento basicRegistry y un elemento administrator-role.
```xml
       <featureManager>
           <feature>jsp-2.2</feature>
           <feature>monitor-1.0</feature>
           <feature>restConnector-1.0</feature>
       </featureManager>

       <basicRegistry>
           <user name="jconuser" password="jconpassw0rd"/>
       </basicRegistry>

       <administrator-role>
           <user>jconuser</user>
       </administrator-role>
```
{: #codeblock}

   * Nota: La contraseña se debe codificar con la herramienta securityUtility que suministra Liberty.

### Inicie la app de JConsole
{: #start_jconsole_app}

JConsole se incluye con la instalación de Java. Para iniciar la app de JConsole, vaya a &lt;java-home&gt;/bin y ejecute el siguiente mandato:
```
    $ jconsole -J-Djava.class.path=<java-home>/lib/jconsole.jar;<liberty-home>/wlp/clients/restConnector.jar
```
{: #codeblock}

Puede que tenga que pasar parámetros adicionales para configurar Java trustStore. Los parámetros siguientes deberían funcionar en la mayoría de los casos:
```
    -J-Djavax.net.ssl.trustStore=<java-home>/jre/lib/security/cacerts -J-Djavax.net.ssl.trustStorePassword=changeit -J-Djavax.net.ssl.trustStoreType=jks
```
{: #codeblock}

### Completar la conexión
{: #start_jconsole_app}
  * Rellene el campo Proceso remoto con el siguiente url:
    * service:jmx:rest://&lt;appName&gt;.mybluemix.net:443/IBMJMXConnectorREST.
  *  En los campos Nombre de usuario y Contraseña especifique un usuario y contraseña con el rol de administrador desde el archivo server.xml.
  * Pulse Conectar.

Cuando se establece una conexión correcta, JConsole empieza a supervisar.

Si la conexión falla, puede generar registros para ayudar a diagnosticar el problema.  En primer lugar, intente recopilar el rastreo del lado del cliente añadiendo **-J-Djava.util.logging.config.file=c:/tmp/logging.properties** al mandato jconsole.
A continuación se muestra un ejemplo de archivo de propiedades de registro:
```
    handlers= java.util.logging.FileHandler
    .level=INFO java.util.logging.FileHandler.pattern = /tmp/jmxtrace.log
    java.util.logging.FileHandler.limit = 50000
    java.util.logging.FileHandler.count = 1
    java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter
    javax.management.level=FINEST
    javax.management.remote.level=FINER
    com.ibm.level=FINEST
```
{: #codeblock}

También puede añadir <b>&dash;J&dash;Djavax.net.debug=ssl</b> al mandato jconsole. Este genera el rastreo de diagnóstico de SSL en otra ventana de salida de JConsole.  Por último, puede habilitar el rastreo en el lado del servidor añadiendo lo siguiente a su archivo server.xml:
```
    <logging traceSpecification="com.ibm.ws.jmx.*=all"/>
```
{: codeblock}

# rellinks
## general
* [Tiempo de ejecución de Liberty](index.html)
* [Visión general del perfil de Liberty](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
