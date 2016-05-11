---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Liberty in Bluemix mit JConsole überwachen
{: #jconsole}

*Letzte Aktualisierung: 23. März 2016*

## Die Schritte für die Überwachung der Bluemix-Liberty-Laufzeit mit JConsole sind wie folgt:
{: #steps_to_monitor}

1. Führen Sie in einem Serverpaket, das die entsprechende Datei 'server.xml' enthält, eine Push-Operation für die App durch.
2. Starten Sie die JConsole-App mit den entsprechenden Systemeigenschaften über die Befehlszeile.
3. Geben Sie unter 'Remote Process', 'Username' und 'Password' die entsprechenden Angaben für JConsole an.

### Push-Operation für das Serverpaket durchführen
{: #push_server_package}

Führen Sie eine Push-Operation für das Serverpaket mit der Anwendung durch und nehmen Sie
dabei eine Begrenzung auf eine Instanz vor. Die Datei 'server.xml' muss die Features `monitor-1.0` und `restConnector-1.0` enthalten. Ferner muss sie die Elemente 'basicRegistry' und 'administrator-role' enthalten.
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

   * Hinweis: Codieren Sie das Kennwort mit dem von Liberty bereitgestellten Tool 'securityUtility'.

### JConsole-App starten
{: #start_jconsole_app}

JConsole ist in der Java-Installation enthalten.  Wechseln Sie zum Starten der JConsole-App in das Verzeichnis &lt;java-home&gt;/bin und führen Sie den folgenden Befehl aus:
```
    $ jconsole -J-Djava.class.path=<java-home>/lib/jconsole.jar;<liberty-home>/wlp/clients/restConnector.jar
```
{: #codeblock}

Für die Konfiguration des Java-Truststores müssen Sie möglicherweise weitere Parameter übergeben. Die folgenden Parameter funktionieren für die meisten Fälle:
```
    -J-Djavax.net.ssl.trustStore=<java-home>/jre/lib/security/cacerts -J-Djavax.net.ssl.trustStorePassword=changeit -J-Djavax.net.ssl.trustStoreType=jks
```
{: #codeblock}

### Verbindungsaufbau abschließen
{: #start_jconsole_app}
  * Füllen Sie das Feld 'Remote Process' mit der folgenden URL:
    * service:jmx:rest://&lt;appName&gt;.mybluemix.net:443/IBMJMXConnectorREST.
  *  Geben Sie in die Felder 'Username' und 'Password' ferner einen Benutzer mit einer Administratorrolle und das Kennwort aus der Datei 'server.xml' ein.
  * Klicken Sie auf 'Connect'.

Wenn die Verbindung erfolgreich hergestellt wird, beginnt
JConsole mit der Überwachung.

Wenn die Verbindung fehlschlägt, können Protokolle zur Fehlerdiagnose generiert werden.  Erfassen Sie zuerst die Tracedaten auf der Clientseite, indem Sie
**-J-Djava.util.logging.config.file=c:/tmp/logging.properties** zum jconsole-Befehl
hinzufügen.
Beispiel für eine Eigenschaftendatei zur Protokollierung:
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

Sie können auch <b>&dash;J&dash;Djavax.net.debug=ssl</b> zum Befehl 'jconsole' hinzufügen. Dadurch wird ein SSL-Diagnosetracing in einem separaten JConsole-Ausgabefenster erstellt.  Zuletzt können Sie das Tracing auf der Serverseite aktivieren, indem das Folgende zur Datei 'server.xml' hinzufügen:
```
    <logging traceSpecification="com.ibm.ws.jmx.*=all"/>
```
{: codeblock}

# Zugehörige Links
## Allgemein
* [Liberty-Laufzeit](index.html)
* [Übersicht über das Liberty-Profil](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
