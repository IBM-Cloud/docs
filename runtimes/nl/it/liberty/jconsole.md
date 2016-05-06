---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Monitoraggio di Liberty in Bluemix con JConsole
{: #jconsole}

*Ultimo aggiornamento: 23 marzo 2016*

## La procedura per monitorare il runtime Liberty Bluemix con JConsole è la seguente:
{: #steps_to_monitor}

1. Esegui il push della tua applicazione all'interno di un pacchetto del server contenente un server.xml appropriato.
2. Avvia l'applicazione JConsole con le proprietà di sistema appropriate sulla riga di comando.
3. Fornisci l'URL di accesso remoto, il nome utente e la password corretti alla JConsole.

### Esegui il push del package server
{: #push_server_package}

Esegui il push del package server contenente la tua applicazione limitandolo
a una singola istanza. Il tuo file server.xml deve contenere le funzioni `monitor-1.0` e `restConnector-1.0`. Deve contenere anche un elemento basicRegistry e un elemento administrator-role.
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

   * Nota: la password deve essere codificata con lo strumento securityUtility fornito da Liberty.

### Avvia l'applicazione JConsole
{: #start_jconsole_app}

La JConsole è inclusa con l'installazione Java.  Per avviare l'applicazione JConsole vai in &lt;java-home&gt;/bin ed esegui il seguente comando:
```
    $ jconsole -J-Djava.class.path=<java-home>/lib/jconsole.jar;<liberty-home>/wlp/clients/restConnector.jar
```
{: #codeblock}

Potresti dover trasmettere ulteriori parametri per configurare il trustStore Java. I seguenti parametri dovrebbero funzionare nella maggior parte dei casi:
```
    -J-Djavax.net.ssl.trustStore=<java-home>/jre/lib/security/cacerts -J-Djavax.net.ssl.trustStorePassword=changeit -J-Djavax.net.ssl.trustStoreType=jks
```
{: #codeblock}

### Completa la connessione
{: #start_jconsole_app}
  * Compila il campo Processo remoto con il seguente URL:
    * service:jmx:rest://&lt;appName&gt;.mybluemix.net:443/IBMJMXConnectorREST.
  *  Compila inoltre i campi Username e Password con un utente con ruolo administrator-role e una password dal file server.xml.
  * Fai clic su Connect.

Quando la connessione
viene stabilita correttamente, la JConsole inizia il monitoraggio.

Se la connessione non riesce, puoi produrre dei log utili per diagnosticare il problema.  Prova prima a raccogliere la traccia lato client aggiungendo ** -J-Djava.util.logging.config.file=c:/tmp/logging.properties** al
comando jconsole.
Viene qui di seguito riportato un file di proprietà di registrazione di esempio:
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

Puoi anche aggiungere <b>&dash;J&dash;Djavax.net.debug=ssl</b> al comando jconsole. Ciò produce la traccia di diagnostica SSL in una finestra di output JConsole
separata.  Infine, puoi abilitare la traccia sul lato server aggiungendo quanto segue al tuo file server.xml:
```
    <logging traceSpecification="com.ibm.ws.jmx.*=all"/>
```
{: codeblock}

# rellinks
## general
* [Runtime Liberty](index.html)
* [Panoramica di Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
