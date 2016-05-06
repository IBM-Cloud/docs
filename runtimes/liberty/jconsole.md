---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Monitoring Liberty in Bluemix with JConsole
{: #jconsole}

*Last Updated: 23 March 2016*

## The steps to monitor the Bluemix Liberty runtime with JConsole follow:
{: #steps_to_monitor}

1. Push your app within a server package containing an appropriate server.xml.
2. Start the JConsole app with the appropriate system properties on the command line.
3. Provide the proper Remote Process url, Username, and Password to JConsole.

### Push the server package
{: #push_server_package}

Push the server package containing your application limiting it to a single instance. Your server.xml file must contain the `monitor-1.0` and `restConnector-1.0` features. It must also contain a basicRegistry element and administrator-role element.
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
{: codeblock}

   * Note: The password should be encoded with the securityUtility tool provided by Liberty.

### Start the JConsole app
{: start_jconsole_app}

JConsole is included with your Java installation.  To start the JConsole app go to &lt;java-home&gt;/bin and run the following command:
```
    $ jconsole -J-Djava.class.path=<java-home>/lib/jconsole.jar;<liberty-home>/wlp/clients/restConnector.jar
```
{: codeblock}

You may have to pass additional parameters to configure Java trustStore. The following parameters should work in most cases:
```
    -J-Djavax.net.ssl.trustStore=<java-home>/jre/lib/security/cacerts -J-Djavax.net.ssl.trustStorePassword=changeit -J-Djavax.net.ssl.trustStoreType=jks
```
{: codeblock}

### Complete the connection
{: start_jconsole_app}
  * Fill in the Remote Process field the following url:
    * service:jmx:rest://&lt;appName&gt;.mybluemix.net:443/IBMJMXConnectorREST.
  *  Also fill in the Username and Password fields with an administrator-role role user and password from the server.xml file.
  * Click Connect.

When the connection succeeds, JConsole starts monitoring.

If the connection fails, you can produce logs to help diagnose the problem.  First, try collecting client side trace by adding **-J-Djava.util.logging.config.file=c:/tmp/logging.properties** to the jconsole command.
Here is a sample logging properties file:
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
{: codeblock}

You can also add <b>&dash;J&dash;Djavax.net.debug=ssl</b> to the jconsole command. This produces SSL diagnostic tracing in a separate JConsole output window.  Lastly, you can enable tracing on the server side by adding the following to your server.xml file:
```
    <logging traceSpecification="com.ibm.ws.jmx.*=all"/>
```
{: codeblock}

# rellinks
## general
* [Liberty runtime](index.html)
* [Liberty Profile Overview](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
