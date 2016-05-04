---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Personalizzazione del JRE
{: #customizing_jre}

*Ultimo aggiornamento: 23 marzo 2016*

Le applicazioni vengono eseguite in un JRE (Java runtime
environment) fornito e configurato dal pacchetto di build Liberty. Il pacchetto di build Liberty rende anche possibile configurare la versione o il tipo di JRE, personalizzare
le opzioni JVM o sovrapporre le funzioni JRE.

## IBM JRE

Per impostazione predefinita, le applicazioni
sono configurate per essere eseguite con una versione leggera di IBM JRE. Questo JRE
leggero è semplificato per fornire una funzionalità di base ed essenziale con
un ingombro su disco e in memoria decisamente ridotto. Per ulteriori informazioni sui contenuti del JRE leggero, consulta [Liberty for Java runtime](http://download.boulder.ibm.com/ibmdl/pub/software/dw/jdk/docs/bluemix/libertyforjava_jre.doc.html).

Per impostazione predefinita, viene utilizzato IBM JRE versione 8. Utilizza la variabile di ambiente JBP_CONFIG_IBMJDK per specificare una versione alternativa di IBM JRE. Ad esempio, per utilizzare
				l'IBM JRE 7.1 più recente, imposta la seguente variabile di
				ambiente:
```
    $ cf set-env myapp JBP_CONFIG_IBMJDK "version: 1.7.+"
```
{: #codeblock}

La proprietà version può essere impostata su un intervallo di versioni. Gli intervalli di versione supportati
sono due: 1.7.+ e 1.8.+. Per dei risultati ottimali, utilizza Java 8.

## OpenJDK
{: #openjdk}

Facoltativamente, le applicazioni possono essere configurate per
l'esecuzione con OpenJDK come JRE. Per abilitare l'esecuzione di un'applicazione con OpenJDK, imposta la variabile di ambiente JVM su "openjdk". Ad esempio, utilizzando
lo strumento riga di comando, esegui il comando:
```
    $ cf set-env myapp JVM 'openjdk'
```
{: #codeblock}

Se abilitato, viene utilizzato OpenJDK versione 8 per impostazione predefinita. Utilizza la variabile di ambiente JBP_CONFIG_OPENJDK  per specificare una versione alternativa di OpenJDK. Ad
				esempio, per utilizzare l'OpenJDK 7 più recente, imposta la seguente variabile di
				ambiente:
```
    $ cf set-env myapp JBP_CONFIG_OPENJDK "version: 1.7.+"
```
{: #codeblock}

La proprietà version può essere impostata su un intervallo di versioni come 1.7.+ o qualsiasi versione
				specifica elencata nell'[elenco di versioni OpenJDK disponibili](https://download.run.pivotal.io/openjdk/lucid/x86_64/index.yml). Per dei risultati ottimali, utilizza Java 8.

## Configurazione delle opzioni JRE
{: #configuring_jre}

### Configurazione predefinita di JVM
{: #jvm_default_config}

Il pacchetto di build Liberty configura le opzioni JVM predefinite tenendo conto di quanto segue:

* Il limite di memoria dell'applicazione.  Le impostazioni heap JVM applicate sono calcolate in base:
  * il limite di memoria di un'applicazione, come spiegato in [Limiti di memoria e pacchetto di build Liberty](memoryLimits.html#memory_limits)
  * il tipo di JRE, poiché le opzioni correlate all'heap per JVM variano in base alle opzioni supportate del JRE.

* Le [Funzioni Liberty supportate in Bluemix](libertyFeatures.html#libertyfeatures).
  * Le transazioni database globali con commit in due fasi non sono supportate in Bluemix e sono pertanto disabilitate impostando -Dcom.ibm.tx.jta.disable2PC=true.

* L'ambiente Bluemix.

    Le opzioni JVM sono configurate per fornire l'ottimizzazione in un ambiente Bluemix e per essere di ausilio nella diagnostica di condizioni di errore correlate alla memoria.
  * il rilevamento e il ripristino rapido delle condizioni di errore di un'applicazione viene configurato disabilitando
le opzioni di dump JVM e terminando i processi quando la memoria di un'applicazione si esaurisce.
  * l'ottimizzazione della virtualizzazione (solo per IBM JRE).
  * l'instradamento delle informazioni sulle risorse di memoria disponibili dell'applicazione quando si è verificato
l'errore al Loggregator.
  * se un'applicazione è configurata per abilitare i dump di memoria JVM, l'interruzione dei processi Java è disabilitata e i dump di memoria JVM vengono instradati a una directory "dumps" dell'applicazione	comune. Questi dump possono essere quindi visualizzati dal dashboard Bluemix o dalla CLI CF.

Il seguente è un esempio della configurazione JVM predefinita di esempio generata dal pacchetto di build per un'applicazione distribuita con un limite di memoria 512M:
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

### Personalizzazione della configurazione della JVM
{: #customizing_jvm}

Le applicazioni possono personalizzare le opzioni JVM con le specifiche definite dal JRE configurato per l'applicazione. Fai riferimento alle linee guida su come specificare un'opzione e sul suo utilizzo direttamente dalla documentazione del JRE poiché le opzioni variano in base al JRE.

<table>
<tr>
<th align="left">JRE</th>
<th align="left">Formato delle opzioni della riga di comando</th>
<th align="left">Riferimento</th>
</tr>

<tr>
<td>IBM JRE</td>
<td>include le opzioni di runtime (con prefisso -X), le eventuali proprietà di sistema Java (con prefisso -D) e non raccomanda -XX per un utilizzo casuale (queste opzioni sono soggette a modifica)
</td>
<td>[Opzioni della riga di comando della Versione 8](http://www-01.ibm.com/support/knowledgecenter/SSYKE2_8.0.0/com.ibm.java.lnx.80.doc/diag/appendixes/cmdline/cmdline.html), [Opzioni della riga di comando della Versione 7](http://www-01.ibm.com/support/knowledgecenter/SSYKE2_7.0.0/com.ibm.java.lnx.70.doc/diag/appendixes/cmdline/cmdline.html)
</td>
</tr>

<tr>
<td> OpenJDK </td>
<td>è basato sul runtime HotSpot che ha la notazione di
-X per non standard, -XX per le opzioni sviluppatore e i flag booleani
per abilitare o disabilitare l'opzione </td>
<td>[Panoramica di runtime di HotSpot](http://openjdk.java.net/groups/hotspot/docs/RuntimeOverview.html) </td>
</tr>
</table>

Un'applicazione che richiede le opzioni JVM personalizzate può impostare l'opzione come un valore per una delle variabili di ambiente IBM_JAVA_OPTIONS, JAVA_OPTS o JVM_ARGS in Bluemix. Fai riferimento alla sezione Variabili di ambiente su come impostare la variabile di ambiente di un'applicazione. Un server in pacchetto o una directory server può anche includere un file jvm.options che contiene le opzioni di riga di comando invece dell'impostazione di una variabile di ambiente.

Quando le opzioni JVM vengono applicate al JRE, vengono applicate prima le opzioni
predefinite del pacchetto di build Liberty, seguite dalle opzioni personalizzate. Le opzioni personalizzate sono accodate in
un ordine specificato, che è elencato nella tabella. La sequenza delle opzioni Java applicate definisce quali opzioni hanno la precedenza. Le opzioni applicate per ultime hanno la precedenza sulle opzioni applicate in precedenza.

Nota: alcune opzioni potrebbero non diventare effettive se non vengono attivate da un agent.

<table>
<tr>
<th align="left">Ordine applicato</th>
<th align="left">Impostazione delle opzioni JVM dell'applicazione</th>
<th align="left">Descrizione</th>
<th align="left">Tipo di applicazione supportato</th>
<th align="left">Per aggiornare l'opzione JVM di un'applicazione distribuita</th>
<th align="left">Applicabile a OpenJDK JRE</th>
</tr>

<tr>
<td>1</td>
<td>IBM_JAVA_OPTIONS</td>
<td>una variabile di ambiente supportata da IBM JRE</td>
<td>Tutti</td>
<td>Riavviare o ripreparare l'applicazione</td>
<td>No</td>
</tr>

<tr>
<td>2</td>
<td>JAVA_OPTS</td>
<td>una variabile di ambiente mediante il framework del pacchetto di build Liberty Java Options</td>
<td>Tutti</td>
<td>Ripreparare l'applicazione</td>
<td>Sì</td>
</tr>

<tr>
<td>3</td>
<td>jvm.options</td>
<td>un file di configurazione JVM supportato dalla directory server o dal server in pacchetto di runtime Liberty</td>
<td>Package server</td>
<td>Ripreparare l'applicazione</td>
<td>Sì</td>
</tr>

<tr>
<td>4</td>
<td>JVM_ARGS</td>
<td>una variabile di ambiente supportata dal runtime Liberty</td>
<td>Tutti</td>
<td>Riavviare o ripreparare l'applicazione</td>
<td>Sì</td>
</tr>
</table>

### Determinare le opzioni JVM applicate di un'applicazione in esecuzione
{: #determining_applied_jvm_options}

Fatta eccezione per le opzioni definite dall'applicazione che sono specificate con la variabile di ambiente JVM_ARGS, le opzioni risultanti sono rese persistenti nella variabile di ambiente come opzioni della riga di comando (applicazioni Java autonome) oppure in un file jvm.options (applicazioni Java non autonome). Le opzioni JVM applicate per l'applicazione possono essere visualizzate dal dashboard Bluemix o dalla CLI CF.

Le opzioni JVM per l'applicazione JAVA autonoma sono mantenute come opzioni della riga di comando. Possono essere visualizzate dal file staging_info.yml.
```
    $ cf files myapp staging_info.yml
```
{: #codeblock}

Le opzioni JVM per la distribuzione di WAR, EAR, directory server e server in pacchetto sono memorizzate in un file jvm.options.

Per visualizzare il file jvm.options per WAR, EAR e directory server, esegui il comando:
```
    $ cf files myapp app/wlp/usr/servers/defaultServer/jvm.options
```
{: #codeblock}

Per visualizzare il file jvm.options per un server in pacchetto, sostituisci <nomeServer> con il nome del tuo server ed esegui il comando:
```
    $ cf files myapp app/wlp/usr/servers/<nomeServer>jvm.options
```
{: #codeblock]

#### Utilizzo di esempio
{: #example_usage}

Distribuzione di un'applicazione con le opzioni JVM personalizzate per abilitare la registrazione della raccolta di dati inutilizzati dettagliata della JVM di IBM JRE:
* Le opzioni JVM incluse nel file manifest.yml di un'applicazione:
```
    env:
      JAVA_OPTS: "-verbose:gc -Xverbosegclog:./verbosegc.log,10,1000"
```
{: #codeblock}

* Per visualizzare la registrazione della raccolta di dati inutilizzati dettagliata della JVM:
```
    $ cf files myapp app/wlp/usr/servers/defaultServer/verbosegc.log.001
```
{: #codeblock}    

* Aggiornamento dell'opzione JVM di IBM JRE dell'applicazione distribuita per attivare un heap, uno snap e un javacore oppure una condizione di memoria esaurita (OutOfMemory):

Imposta la variabile di ambiente dell'applicazione con l'opzione JVM e riavvia l'applicazione.
```
    $ cf set-env myapp JVM_ARGS '-Xdump:heap+java+snap:events=systhrow,filter=java/lang/OutOfMemoryError'
    $ cf restart myapp
```
{: #codeblock}

* Per visualizzare i dump JVM generati quando viene attivata la condizione di memoria esaurita:
```
    $ cf files myapp dumps

    Getting files for app myapp in org myemail@email.com / space dev as myemail@email.com...
    OK

    Snap.20141106.100252.81.0003.trc           307.3K
    heapdump.20141106.100252.81.0001.phd       3.9M
    javacore.20141106.100252.81.0002.txt     870.5K
```
{: #codeblock}

### Sovrapposizione del JRE
{: #overlaying_jre}

Ci sono alcuni casi in cui è necessario
aggregare i file con il JRE per esporne le funzioni. Lo sviluppatore dell'applicazione può fornire i file JRE per la personalizzazione.

I
file da sovrapporre possono essere impacchettati con WAR, EAR,
o JAR dell'applicazione in una cartella resources alla root dell'archivio. Per un server (directory server o file compresso), i file possono essere impacchettati in una cartella resources nella directory server, con il file server.xml.

* WAR file
  * WEB-INF
  * resources
    * other files
    * .java-overlay


* EAR file
  * META-INF
  * resources
    * other files
    * .java-overlay


* JAR file
  * META-INF
  * resources
    * other files
    * .java-overlay


* server_name DIR
  * apps
  * dropins
  * server.xml
  * resources
    * other files
    * .java-overlay

La directory .java-overlay contiene dei file specifici nella stessa gerarchia di file di Java JRE di cui si sta eseguendo la sovrapposizione a partire da	.java/jre.

Ad esempio, se desideri utilizzare la crittografia AES a 256 bit, devi soprapporre questi file di politica Java:
```
    .java\jre\lib\security\US_export_policy.jar
    .java\jre\lib\security\local_policy.jar
```
{: #codeblock}

Scarica i file di politica senza limitazioni appropriati e aggiungili all'applicazione come:
```
    resources\.java-overlay\.java\jre\lib\security\US_export_policy.jar
    resources\.java-overlay\.java\jre\lib\security\local_policy.jar
```
{: #codeblock}

Quando esegui il push dell'applicazione, questi jar si sovrappongono ai jar di politica predefiniti nel runtime Java. Questi processo abilita la crittografia AES a 256 bit.

# rellinks
## general
* [Runtime Liberty](index.html)
* [Panoramica di Liberty Profile](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
