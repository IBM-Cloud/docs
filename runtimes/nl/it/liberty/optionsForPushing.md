---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Opzioni per eseguire il push di applicazioni Liberty
{: #options_for_pushing}

*Ultimo aggiornamento: 23 marzo 2016*

La modalità di funzionamento del server Liberty in Bluemix è controllata dal pacchetto di build Liberty. I pacchetti di build possono fornire un ambiente di runtime completo per
una specifica classe di applicazioni. Sono fondamentali per fornire la portabilità tra i cloud e contribuire a
un'architettura open cloud. Il pacchetto di build Liberty fornisce un contenitore WebSphere
Liberty in grado di eseguire applicazioni Java EE 7 e OSGi. Supporta framework di uso comune come Spring e include l'IBM JRE. WebSphere Liberty abilita un rapido sviluppo delle applicazioni che è adatto per il cloud. Il pacchetto di build Liberty supporta più applicazioni che sono distribuite in un singolo server
Liberty. Come parte dell'integrazione del pacchetto di build Liberty in Bluemix, il pacchetto di build verifica che le variabili di ambiente per i servizi di bind siano mostrate come variabili di configurazione nel server Liberty.

Per distribuire le tue applicazioni Liberty a Bluemix, puoi utilizzare i seguenti metodi.

* Esecuzione del push di un'applicazione autonoma
* Esecuzione del push di una directory server
* Esecuzione del push di un server in pacchetto

Importante: quando distribuisci un'applicazione con il pacchetto di build Liberty, specifica un minimo di 512M come limite di memoria per le tue applicazioni. Per ulteriori informazioni, consulta [Limiti di memoria e pacchetto di build Liberty](memoryLimits.html).

## Applicazioni autonome
{: #stand_alone_apps}

Le applicazioni autonome come i file WAR o EAR possono essere distribuite a Liberty in Bluemix.

Per distribuire un'applicazione autonoma, esegui il comando cf push con il parametro -p che punta al file WAR o EAR.
Ad esempio:

```
    $ cf push <nomedellatuaapplicazione> -p myapp.war
```
{: #codeblock}

Quando viene distribuita un'applicazione autonoma, per l'applicazione viene fornita una configurazione Liberty predefinita. La configurazione predefinita abilita le seguenti funzioni Liberty:

* beanValidation-1.1
* [cdi-1.2](optionsForPushing.html#cdi12)
* ejbLite-3.2
* el-3.0
* jaxrs-2.0
* jdbc-4.1
* jndi-1.0
* jpa-2.1
* jsf-2.2
* jsonp-1.0
* jsp-2.3
* managedBeans-1.0
* servlet-3.1
* websocket-1.1
* icap:managementConnector-1.0
* appstate-1.0

Queste funzioni corrispondono alle funzioni del profilo web Java EE 7. Puoi specificare un insieme diverso di funzioni Liberty impostando la variabile di ambiente JBP_CONFIG_LIBERTY. Ad esempio,
per abilitare solo le funzioni jsp-2.3 e websocket-1.1, esegui il comando e prepara di
nuovo l'applicazione:

```
    $ cf set-env myapp JBP_CONFIG_LIBERTY "app_archive: {features: [jsp-2.3, websocket-1.1]}"
```
{: #codeblock}

Nota: per dei risultati ottimali, imposta le funzioni Liberty con la variabile di ambiente JBP_CONFIG_LIBERTY oppure distribuisci la tua applicazione come una [directory server](optionsForPushing.html#server_directory) o un [server in pacchetto](optionsForPushing.html#packaged_server) con un file server.xml personalizzato. L'impostazione di questa
				variabile di ambiente garantisce che la tua applicazione utilizzi solo la funzione di cui
				ha bisogno e che non risenta delle modifiche dell'insieme di funzioni Liberty predefinito del pacchetto di build. Se devi fornire una configurazione Liberty aggiuntiva oltre all'insieme di funzioni, utilizza
					l'opzione [directory
					server](optionsForPushing.html#server_directory) o [server
					in pacchetto](optionsForPushing.html#packaged_server) per distribuire la tua applicazione.

Se hai distribuito un file WAR, l'applicazione web è accessibile sotto il root di contesto come impostato nel file ibm-web-ext.xml incorporato. Se il file ibm-web-ext.xml non esiste, o non specifica il root di contesto, l'applicazione è accessibile sotto la root di contesto. Ad esempio,

```
    http://<nomedellatuaapplicazione>.mybluemix.net/
```
{: #codeblock}

Se hai distribuito un file EAR, l'applicazione web integrata è accessibile sotto il root di contesto come definito nel descrittore di distribuzione EAR. Ad esempio,

```
    http://<nomedellatuaapplicazione>.mybluemix.net/acme/
```
{: #codeblock}

L'intero file di configurazione server.xml Liberty predefinito si presenta come segue:
```
    <server>
       <featureManager>
          <feature>beanValidation-1.1</feature>
          <feature>cdi-1.2</feature>
          <feature>ejbLite-3.2</feature>
          <feature>el-3.0</feature>
          <feature>jaxrs-2.0</feature>
          <feature>jdbc-4.1</feature>
          <feature>jndi-1.0</feature>
          <feature>jpa-2.1</feature>
          <feature>jsf-2.2</feature>
          <feature>jsonp-1.0</feature>
          <feature>jsp-2.3</feature>
          <feature>managedBeans-1.0</feature>
          <feature>servlet-3.1</feature>
          <feature>websocket-1.1</feature>
          <feature>icap:managementConnector-1.0</feature>
          <feature>appstate-1.0</feature>
       </featureManager>

       <application name='myapp' location='myapp.war' type='war' context-root='/'/>
       <httpEndpoint id='defaultHttpEndpoint' host='*' httpPort='${port}'/>
       <webContainer trustHostHeaderPort='true' extractHostHeaderPort='true'/>
       <include location='runtime-vars.xml'/>
       <logging logDirectory='${application.log.dir}' consoleLogLevel='INFO'/>
       <httpDispatcher enableWelcomePage='false'/>
       <applicationMonitor dropinsEnabled='false' updateTrigger='mbean'/>
       <config updateTrigger='mbean'/>
       <cdi12 enableImplicitBeanArchives='false'/>
       <appstate appName='myapp' markerPath='${home}/../.liberty.state'/>
    </server>
```
{: #codeblock}

### CDI 1.2
{: #cdi12}

Per motivi legati alle prestazioni, quando si distribuiscono solo file WAR ed EAR, la [scansione degli archivi di bean impliciti CDI 1.2](https://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_cdi_behavior.html) è disabilitata per impostazione predefinita. La scansione degli archivi di bean impliciti può essere abilitata utilizzando la variabile di ambiente JBP_CONFIG_LIBERTY.
Ad esempio:

```
    $ cf set-env myapp JBP_CONFIG_LIBERTY "app_archive: { implicit_cdi: true }"
```    
{: #codeblock}

Importante: per rendere effettive le tue modifiche alle variabili di ambiente è necessario ripreparare la tua applicazione:

```
    $ cf restage myapp
```
{: #codeblock}

## Directory server
{: #server_directory}

In alcuni casi, potrebbe essere necessario fornire una configurazione server Liberty personalizzata con la tua 				applicazione. Questa configurazione personalizzata potrebbe servirti quando distribuisci un file WAR o EAR e il file server.xml predefinito non ha le specifiche impostazioni di cui la tua applicazione ha bisogno.

Se hai installato il profilo Liberty sulla tua workstation e hai già creato un server Liberty con la tua applicazione, puoi distribuire i contenuti di tale directory in Bluemix.
Ad esempio, se il server Liberty è denominato defaultServer, esegui il comando:

```
    $ cf push <nomedellatuaapplicazione> -p wlp/usr/servers/defaultServer
```
{: #codeblock}

Se sulla workstation non è installato un profilo Liberty, puoi utilizzare la seguente procedura
				per creare una directory server con la tua applicazione:

1. Crea una directory denominata defaultServer.
2. Crea una directory apps nella directory defaultServer.
3. Copia il file WAR o EAR nella directory defaultServer/apps.
4. Nella directory defaultServer, crea un file server.xml con il seguente contenuto di esempio.  Inoltre:
  * Assicurati di aggiornare l'attributo location o type dell'elemento application in modo che corrisponda al nome file e al tipo della tua applicazione.
  * Il file server.xml nel diagramma mostra un insieme di funzioni	minime. È possibile che tu debba regolare l'insieme di funzioni a seconda delle esigenze della tua applicazione.

```
    <server>
        <featureManager>
            <feature>jsp-2.3</feature>
        </featureManager>

        <httpEndpoint id=>

        <application name="myapp" context-root="/" type="war" location="myapp.war"/>
    </server>
```
{: #codeblock}

Dopo che la directory server è pronta, puoi distribuirla a Bluemix.

```
    $ cf push <nomedellatuaapplicazione> -p defaultServer
```
{: #codeblock}

Nota: le applicazioni web distribuite come parte della directory server sono accessibili sotto la [root di contesto, come determinato dal profilo Liberty](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/twlp_dep_war.html?cp=SSAW57_8.5.5%2F1-3-11-0-5-6). Ad esempio:

```
    http://<nomedellatuaapplicazione>.mybluemix.net/acme/
```
{: #codeblock}

## Server in pacchetto
{: #packaged_server}

Puoi anche eseguire il push di un server in pacchetto a Bluemix. Il file di server in pacchetto viene creato utilizzando il comando di package server di Liberty. Oltre ai file di applicazione e configurazione, il file di server in pacchetto può contenere risorse condivise e funzioni utente Liberty richieste dall'applicazione.

Per impacchettare un server Liberty, utilizza il comando ./bin/server package dalla directory di installazione di Liberty. Specifica il nome server e includi l'opzione '––include=usr'.
Ad esempio, se il tuo server Liberty è defaultServer, esegui il comando:

```
    $ wlp/bin/server package defaultServer --include=usr
```
{: #codeblock}

Questo comando genera un file serverName.zip nella directory del server. Puoi quindi eseguire il push di tale file compresso a Bluemix con il comando cf push.
Ad esempio:

```
    $ cf push <nomedellatuaapplicazione> -p wlp/usr/servers/defaultServer/defaultServer.zip
```
{: #codeblock}

Nota: le applicazioni web distribuite come parte del server in pacchetto sono accessibili sotto la root di contesto, come determinato dal profilo Liberty.

### Modifica del file server.xml
{: #modifications_of_serverxml}

Quando viene eseguito il push di un server in pacchetto o di una directory server Liberty, il pacchetto di build Liberty rileva il file server.xml insieme alla tua applicazione. Il pacchetto di build Liberty apporta le seguenti modifiche al file server.xml.

* Il pacchetto di build verifica che nel file sia presente esattamente un singolo elemento httpEndpoint.
* Il pacchetto di build verifica che l'attributo httpPort nell'elemento httpEndpoint punti a una variabile di sistema denominata ${port}. Il pacchetto di build sovrascrive anche l'attributo host.
* Il pacchetto di build imposta l'attributo logDirectory nell'elemento logging in modo che punti a una directory di log di sistema.
* Il pacchetto di build verifica che un file runtime-vars.xml venga unito logicamente al tuo file server.xml. In modo specifico, il pacchetto di build accoda la riga *&lt;include location="runtime-vars.xml" /&gt;* al tuo file server.xml.

### Variabili a cui è possibile fare riferimento
{: #referenceable_variables}

Le seguenti variabili sono definite nel file runtime-vars.xml e si fa riferimento a esse da un file server.xml di cui è stato eseguito il push. Tutte le variabili
sono sensibili al maiuscolo/minuscolo.

* ${port}: la porta HTTP su cui è in ascolto il server Liberty.
* ${vcap_console_port}: la porta dove è in esecuzione la console vcap (in genere uguale a ${port}).
* ${vcap_app_port}: la porta dove è in ascolto il server app (in genere uguale a ${port}).
* ${vcap_console_ip}: l'indirizzo IP della console vcap (di norma l'indirizzo IP su cui è in ascolto il server Liberty).
* ${application_name}: il nome dell'applicazione, come definito utilizzando le opzioni nel comando cf push.
* ${application_version}: la versione di questa istanza dell'applicazione, che assume la forma di un UUID, come b687ea75-49f0-456e-b69d-e36e8a854caa. Questa variabile cambia a ogni successivo push dell'applicazione che contiene del nuovo codice o delle modifiche alle risorse dell'applicazione.
* ${host}: l'indirizzo IP del DEA che sta eseguendo l'applicazione (di norma uguale a ${vcap_console_ip}).
* ${application_uris}: un array in stile JSON degli endpoint che è possibile utilizzare per accedere a questa applicazione, ad esempio: myapp.mydomain.com.
* ${start}: la data e l'ora in cui è stata avviata l'applicazione; assume una forma simile a 2013-08-22 10:10:18 -0400.

### Accesso alle informazioni dei servizi di cui è stato eseguito il bind
{: #accessing_info_of_bound_services}

Quando desideri eseguire il bind di un servizio alla tua applicazione, le informazioni sul servizio,
				come le credenziali di connessione, sono incluse nella [variabile di ambiente VCAP_SERVICES](http://docs.run.pivotal.io/devguide/deploy-apps/environment-variable.html#VCAP-SERVICES) che
				Cloud Foundry imposta per l'applicazione. Per i [servizi configurati automaticamente](autoConfig.html), il pacchetto di build Liberty genera o
				aggiorna le voci di bind di servizio nel file  server.xml. Il contenuto delle voci di bind di
				servizio può essere in uno dei seguenti formati:

* cloud.services.&lt;nome-servizio&gt;.&lt;proprietà&gt;, che descrive informazioni quali il nome, il tipo e il piano del servizio.
* cloud.services.&lt;nome-servizio&gt;.connection.&lt;proprietà&gt;, che descrive le informazioni di connessione per il servizio.

L'insieme di informazioni tipico è il seguente:
* name: il nome del servizio. Ad esempio, mysql-e3abd.
label: il tipo del servizio creato. Ad esempio, mysql-5.5.
* plan: il piano di servizio, come indicato dall'identificativo univoco per tale piano. Ad esempio, 100.
connection.name: un identificativo univoco per la connessione, che assume la forma di un UUID. Ad esempio, d01af3a5fabeb4d45bb321fe114d652ee.
* connection.hostname: il nome host del server che sta eseguendo il servizio. Ad esempio, mysql-server.mydomain.com.
* connection.host: l'indirizzo IP del server che sta eseguendo il servizio. Ad esempio, 9.37.193.2.
* connection.port: la porta su cui il servizio è in ascolto per le connessioni in entrata. Ad esempio, 3306,3307.
* connection.user: il nome utente utilizzato per autenticare questa applicazione presso il servizio. Il nome utente viene generato automaticamente da Cloud Foundry. Ad esempio: unHwANpjAG5wT.
* connection.username: un alias per connection.user.
* connection.password: la password utilizzata per autenticare questa applicazione presso il servizio. La password viene generata automaticamente da Cloud Foundry. Ad esempio: pvyCY0YzX9pu5.

Per i servizi di cui è stato eseguito il bind che non sono configurati automaticamente dal pacchetto di build Liberty, l'applicazione deve gestire direttamente l'accesso della risorsa di backend.

# rellinks
## general
* [Runtime Liberty](index.html)
* [Panoramica di Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
