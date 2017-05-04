---

copyright:
  years: 2017
lastupdated: "2017-04-04"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# Introduzione a Tomcat su Bluemix
{: #getting_started}

* {: download} Congratulazioni, hai distribuito un'applicazione di esempio Hello World su {{site.data.keyword.Bluemix}}!  Per iniziare, segui questa guida dettagliata. O <a class="xref" href="http://bluemix.net" target="_blank" title="(Scarica il codice di esempio)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="Scarica codice di esempio" />scarica codice di esempio</a> o esplora da solo.

Seguendo questa guida, configurerai un ambiente di sviluppo, distribuirai un'applicazione localmente e in {{site.data.keyword.Bluemix}} e integrerai un servizio database {{site.data.keyword.Bluemix}} nella tua applicazione.

## Prerequisiti
{: #prereqs}

Avrai bisogno di quanto segue:
* [Account {{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net/registration/)
* [CLI Cloud Foundry ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Eclipse IDE for Java EE Developers ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/neon2){: new_window}
* [Git ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://git-scm.com/downloads){: new_window}
* [Maven ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://maven.apache.org/download.cgi){: new_window}
* [Apache Tomcat version 8.0.41 ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://tomcat.apache.org/download-80.cgi#8.0.41 ){: new_window}


## 1. Clona l'applicazione di esempio
{: #clone}

Ora sei pronto per iniziare ad utilizzare l'applicazione Tomcat di esempio. Clona il repository e modifica la directory in cui è ubicata l'applicazione di esempio. 
```
git clone https://github.com/IBM-Bluemix/get-started-tomcat
```
{: pre}

```
cd get-started-tomcat
```
{: pre}

Studia i file nella directory *get-started-tomcat* per acquisire familiarità con i contenuti.

## 2. Esegui l'applicazione localmente
{: #run_locally}

Devi installare le dipendenze e creare un file .war come definito nel file pom.xml per eseguire l'applicazione.

Installa le dipendenze.

```
mvn clean install  
```
{: pre}


Copia GetStartedTomcat.war dalla directory `target` nella tua directory `tomcat-install-dir` `webapps`.

Esegui l'applicazione.  
```
<tomcat-install-dir>/bin/startup.bat|.sh
```
{: screen}

Visualizza la tua applicazione in: http://localhost:8080/GetStartedTomcat/

Utilizza `shutdown.bat|.sh` per arrestare la tua applicazione.  Tieni presente che potresti aver bisogno di fornire l'autorizzazione di esecuzione dei comandi.
{: tip}

## 3. Prepara l'applicazione per la distribuzione a {{site.data.keyword.Bluemix_notm}}
{: #prepare}

Per distribuire a {{site.data.keyword.Bluemix_notm}}, può essere utile impostare un file manifest.yml. Il manifest.yml include le informazioni di base sulla tua applicazione, come il nome, quanta memoria allocare per ogni istanza e la rotta. Abbiamo fornito un file manifest.yml di esempio nella directory `get-started-tomcat`.

Apri il file manifest.yml e modifica `name` da `GetStartedTomcat` con il nome della tua applicazione, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
  applications:
  - name: GetStartedTomcat
    random-route: true
    memory: 256M
    path: target/TomcatHelloWorldApp.war
    buildpack: java_buildpack
  ```
  {: codeblock}

In questo file manifest.yml, **random-route: true** genera una rotta casuale per la tua applicazione per evitare il conflitto con altre rotte.  Se scegli di farlo, puoi sostituire **random-route: true** con **host: myChosenHostName**, fornendo un nome host di tua scelta. [Ulteriori informazioni...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## 4. Distribuisci l'applicazione
{: #deploy}

Puoi utilizzare la CLI Cloud Foundry per distribuire le applicazioni.

Scegli il tuo endpoint API

```
cf api <API-endpoint>
```
{:pre}

Sostituisci *API-endpoint* nel comando con un endpoint API dal seguente elenco.

|URL                             |Regione          |
|:-------------------------------|:---------------|
| https://api.ng.bluemix.net     | Stati Uniti Sud       |
| https://api.eu-gb.bluemix.net  | Regno Unito |
| https://api.au-syd.bluemix.net | Sydney         |


Accedi al tuo account {{site.data.keyword.Bluemix_notm}}: 

```
cf login
```
{: pre}

Dall'interno della directory *get-started-tomcat* trasmetti la tua applicazione a {{site.data.keyword.Bluemix_notm}}
```
cf push
```
{: pre}

Ci possono volere circa due minuti. Se si riscontra un errore nel processo di distribuzione puoi utilizzare il comando `cf logs <Your-App-Name> --recent` per risolverlo.

Quando la distribuzione è stata completata dovresti visualizzare un messaggio che indica che la tua applicazione è in esecuzione.  Visualizza la tua applicazione all'URL elencato nell'output del comando trasmesso.  Puoi anche immettere il
  ```
cf apps
  ```
  {: pre}
  comando per visualizzare lo stato delle tue applicazioni e l'URL.

## 6. Sviluppo in Eclipse 
{: #developing_in_eclipse}

IBM® Eclipse Tools per {{site.data.keyword.Bluemix}} fornisce plugin che è possibile installare in un ambiente Eclipse esistente per assisterti nell'integrazione del IDE (integrated development environment) dello sviluppatore con {{site.data.keyword.Bluemix_notm}}.

Scarica e installa [IBM Eclipse Tools for Bluemix](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix).

Importa questo esempio in Eclipse utilizzando l'opzione `File` -> `Import` -> `Maven` -> `Existing Maven Projects`.

Crea una definizione server Tomcat:
  - Nella vista `Servers` fai clic con il tasto destro su -> `New` -> `Server`.
  - Seleziona `Apache` -> `Tomcat v8.0 Server`.
  - Scegli la tua `tomcat-install-dir`.
  - Continua la procedura guidata con le opzioni predefinite per finire. 

Esegui la tua applicazione localmente sul server Apache: 
  - Fai clic con il tasto destro sull'esempio `GetStartedTomcat` e seleziona l'opzione `Run As` -> `Run on Server`.
  - Trova e seleziona il server Tomcat localhost e fai clic su su fine.
  - In pochi secondi, la tua applicazione dovrebbe essere eseguita all'indirizzo http://localhost:8080/TomcatHelloWorldApp/

Crea una definizione server {{site.data.keyword.Bluemix_notm}}:
  - Nella vista `Servers`, fai clic con il tasto destro su -> `New` -> `Server`.
  - Seleziona `IBM` -> `IBM Bluemix` e segui le istruzioni nella procedura guidata.
  - Immetti le tue credenziali e fai clic su `Next`
  - Seleziona i tuoi `org` e `space` e fai clic su `Finish`

Esegui la tua applicazione su {{site.data.keyword.Bluemix_notm}}:
  - Fai clic con il tasto destro sull'esempio `GetStartedTomcat` e seleziona l'opzione `Run As` -> `Run on Server`.
  - Trova e seleziona `IBM Bluemix` fai clic su su fine.
  - Una procedura guidata ti guiderà con le opzioni di distribuzione. Assicurati di scegliere un `Name` univoco per la tua applicazione.
  - In pochi minuti, la tua applicazione dovrebbe essere in esecuzione nell'URL che hai scelto.

Ora stai eseguendo il tuo codice localmente e sul cloud! 

## 7. Aggiungi un database
{: #add_database}

Successivamente, aggiungeremo un database NoSQL a questa applicazione e la configureremo in modo che possa essere eseguita localmente o su Bluemix.

1. Accedi a {{site.data.keyword.Bluemix_notm}} nel tuo browser. Seleziona il `Dashboard`. Seleziona la tua applicazione facendo clic sul relativo nome nella colonna `Name`.
2. Fai cli su `Connections` e su `Connect new`.
2. Nella sezione `Data & Analytics`, seleziona `Cloudant NoSQL DB` e `Create` il servizio.
3. Seleziona `Restage` quando richiesto. {{site.data.keyword.Bluemix_notm}} riavvierà la tua applicazione e fornirà le credenziali del database alla tua applicazione utilizzando la variabile di ambiente `VCAP_SERVICES`. Questa variabile di ambiente è disponibile solo per l'applicazione quando viene eseguita su {{site.data.keyword.Bluemix_notm}}.

Le variabili di ambiente ti abilitano a separare le impostazioni di distribuzione dal tuo codice di origine. Ad esempio, invece di impostare come hardcoded una password del database, puoi archiviarla in una variabile di ambiente di riferimento nel tuo codice di origine. [Ulteriori informazioni...](/docs/manageapps/depapps.html#app_env)
{: tip}

## 8. Utilizza il database 
{: #use_database}
Ora aggiorneremo il tuo codice locale per puntare a questo database. Archivieremo le credenziali per i servizi in un file properties. Questo file sarà utilizzato SOLO quando l'applicazione è in esecuzione localmente. Quando è in esecuzione in {{site.data.keyword.Bluemix_notm}}, le credenziali saranno lette dalla variabile di ambiente VCAP_SERVICES.

1. Apri Eclipse e il file src/main/resources/cloudant.properties:
  ```
  cloudant_url=
  ```
  {: pre}

2. Nel tuo browser apri la IU {{site.data.keyword.Bluemix_notm}}, seleziona your App -> Connections -> Cloudant -> View Credentials

3. Copia e incolla solo l'`url` dalle credenziali nel campo `url` del file `cloudant.properties` e salva le modifiche. Il risultato sarà qualcosa di simile:
  ```
  cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```

4. Riavvia il server Liberty in Tomcat dalla vista `Servers`. 

  Aggiorna la tua vista del browser all'indirizzo: http://localhost:8080/GetStartedTomcat/. Tutti i nomi immessi nell'applicazione saranno ora aggiunti al database.

  La tua applicazione locale e {{site.data.keyword.Bluemix_notm}} stanno condividendo il database.  Visualizza la tua applicazione {{site.data.keyword.Bluemix_notm}} all'URL elencato nell'output del comando trasmesso precedentemente.  I nomi che aggiungi dall'applicazione dovrebbero essere visualizzati entrambi quando aggiorni i browser.

Ricorda che se non hai bisogno della tua applicazione live su {{site.data.keyword.Bluemix_notm}}, arrestala così da non incorrere in alcun addebito non previsto.
{: tip}  
