---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#Host delle applicazioni in {{site.data.keyword.Bluemix_notm}}

*Ultimo aggiornamento: 9 maggio 2016*

<!--The whole topic is staging only -->

Con {{site.data.keyword.Bluemix}},
puoi creare applicazioni e fornire un host per le applicazioni esistenti. Purché pronte per il cloud, le tue applicazioni possono essere migrate in
{{site.data.keyword.Bluemix_notm}}. {{site.data.keyword.Bluemix_notm}} fornisce diversi modi per eseguire le tue applicazioni, ad esempio Cloud Foundry, IBM Containers e Virtual Machines.

##Come far sì che le tue applicazioni siano pronte per il cloud
{: #cloud-readyapps}

Quando un'applicazione pronta per il cloud viene progettata e creata,
segue i principi della piattaforma cloud. Un'applicazione pronta per il cloud
può utilizzare le capacità fornite dalla piattaforma cloud.

Se la tua applicazione osserva tutti i seguenti principi,
essa è pronta per il cloud e può essere migrata in {{site.data.keyword.Bluemix_notm}}. Se l'applicazione viola uno dei principi, puoi generalmente modificarla
per far sì che rispetti tutti i principi.

* Non codificare direttamente la tua applicazione in una topologia specifica.

  In
un ambiente non cloud, l'applicazione potrebbe utilizzare una particolare topologia
di distribuzione. Tuttavia, la topologia dell'applicazione potrebbe cambiare nelle applicazioni cloud,
poiché i servizi e le applicazioni pronti per il cloud consentono
modifiche immediate per la scalabilità. Le modifiche per la scalabilità includono il ridimensionamento dinamico
e il ridimensionamento manuale del numero di istanze di un'applicazione.

  Crea
la tua applicazione in modo che sia il più possibile generica e senza stati, in modo da preservare
la tua applicazione dagli effetti delle modifiche di scalabilità.

* Non presupporre che il file system locale sia permanente.

  Poiché
un'istanza di un'applicazione può essere spostata, eliminata o duplicata sul cloud in qualsiasi momento,
non affidarti ai file scritti nel file
system. Se un'applicazione utilizza il file system locale come cache delle
informazioni più utilizzate, tra cui i registri delle applicazioni, le informazioni
vengono perse nel momento in cui l'istanza viene arrestata e riavviata in un'ubicazione
o VM differente.

  Invece che nel file system locale, puoi memorizzare
le informazioni in un servizio, quale un database SQL o NoSQL. In un ambiente cloud dinamico, è fondamentale anche che
i tuoi log siano disponibili in un servizio avente durata superiore alle istanze dell'applicazione in cui
vengono generati i log.

* Non memorizzare gli stati delle sessioni nella tua applicazione.

  Lo stato
del tuo sistema viene definito dai database e dalla memoria condivisa e non
da ciascuna istanza dell'applicazione in esecuzione. Qualsiasi tipo di mancanza
di stato limita la scalabilità di un'applicazione. Cerca di ridurre al minimo
l'impatto dello stato della sessione, memorizzandolo in un'ubicazione centralizzata
sul server.

  Se non puoi eliminare del tutto lo stato della sessione, eseguine il push
in una memoria altamente disponibile esterna al server della tua
applicazione. Tra le memorie utilizzabili vi sono IBM WebSphere Extreme Scale, Redis,
Memcached o un database esterno.

* Non utilizzare dipendenze da infrastrutture specifiche.

  Questo principio generale
si rivela sotto vari aspetti. Ad esempio, non partire dal presupposto che
i servizi utilizzati dalla tua applicazione siano associati a indirizzi IP o nomi host
specifici. Poiché i servizi potrebbero essere trasferiti o rigenerati
nel tuo ambiente cloud, potrebbero cambiare anche i nomi host
e gli indirizzi IP.

  L'estrazione di dipendenze specifiche dell'ambiente in una
serie di file di proprietà rappresenta un miglioramento, ma resta inappropriato. La migliore prassi prevede la risoluzione degli endpoint dei servizi attraverso il registro
di un servizio esterno o la delega dell'intera funzione di instradamento
al bus di un servizio o a un programma di bilanciamento dei carichi con un nome virtuale.

* Non utilizzare API infrastruttura nella tua applicazione.

  Se la tua applicazione si affida
a un'API infrastruttura specifica, la modifica dell'infrastruttura
risulta più complessa, poiché un'API infrastruttura
può fare riferimento a livelli differenti del tuo stack software.

  Puoi
invece affidarti ai prodotti commerciali od open source esistenti e
lasciare le soluzioni PaaS nel livello PaaS in modo da mantenerle al di fuori del codice della
tua applicazione.

* Non utilizzare protocolli oscuri.

  Non utilizzare protocolli oscuri che
richiedono una configurazione aggiuntiva per la resilienza.

  Le applicazioni basate
su protocolli standard hanno maggiore resilienza con gli elementi della configurazione
delegati alla piattaforma. I protocolli standard includono HTTP, SSL,
database standard, accodamento e connessioni ai servizi Web.

* Non affidarti a funzioni specifiche del sistema operativo

  Se hai già utilizzato
funzioni specifiche del sistema operativo, puoi risolvere il problema utilizzando librerie di compatibilità,
quali Cygwin e Mono. Cygwin è una libreria di compatibilità che fornisce una serie di strumenti Linux in un ambiente Windows. Mono è una libreria di compatibilità che fornisce le funzionalità di Windows .NET in Linux.

  Evita le dipendenze specifiche del sistema operativo;
utilizza invece servizi forniti dall'infrastruttura middleware
o da fornitori di servizi.

* Non installare manualmente la tua applicazione.

  Nell'ambiente cloud dinamico, la tua
applicazione potrebbe essere installata spesso on-demand Il processo di installazione deve avere script ed essere affidabile e i dati della configurazione
devono essere esternalizzati dagli script.

  Acquisisci almeno l'installazione
della tua applicazione come una serie uniforme di script
indipendenti dal sistema operativo. Fa in modo che le dimensioni dell'installazione della tua applicazione
restino contenute e preservane la portabilità, in modo che si adegui a differenti tecniche di automazione. Inoltre,
riduci al minimo le dipendenze richieste dall'installazione dell'applicazione.

Per ulteriori informazioni sulle applicazioni pronte per il cloud, vedi [12-factor
app](http://12factor.net/){:new_window}.

##Migrazione delle tue applicazioni
{: #ht_hostapp}

Invece di spostare completamente le applicazioni nell'ambiente cloud,
puoi migrarle in {{site.data.keyword.Bluemix_notm}}
in modo incrementale. Puoi migrare prima una parte della tua applicazione
e connetterla al system of record o ai dati esistenti, attraverso il
servizio Cloud Integration.

Nelle tue applicazioni cloud potresti dover accedere ai servizi
o ai dati backend quali, ad esempio, un system of record. In {{site.data.keyword.Bluemix_notm}},
puoi utilizzare il servizio Secure Gateway per stabilire un tunnel protetto
tra un'organizzazione {{site.data.keyword.Bluemix_notm}}
e la rete backend aziendale. Il servizio consente alle applicazioni
su {{site.data.keyword.Bluemix_notm}} di
accedere ai servizi e ai dati della rete backend. Per i dettagli, vedi [Reaching enterprise backend with Bluemix Secure Gateway via console](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){:new_window}.

Per distribuire la tua applicazione su {{site.data.keyword.Bluemix_notm}} come
applicazione Cloud Foundry, seleziona un runtime dal Catalogo {{site.data.keyword.Bluemix_notm}}. Il runtime contiene un'applicazione starter Hello World che puoi sostituire con la tua propria applicazione. Se non riesci a trovare uno starter con il runtime desiderato, puoi portare un pacchetto di build personalizzato compatibile con Cloud Foundry in {{site.data.keyword.Bluemix_notm}} utilizzando l'opzione –b con il comando cf push. Per i dettagli, vedi [Utilizzo dei pacchetti di build della community](../cfapps/byob.html).

Puoi usare i seguenti servizi e strumenti forniti da {{site.data.keyword.Bluemix_notm}}:

*Tabella 1. Strumenti {{site.data.keyword.Bluemix_notm}}*

| Strumento	| Metodo |
|:------|:--------|
|Interfaccia riga di comando Cloud Foundry (cf cli)	|Gestisci il tuo codice su un client locale e utilizza l'interfaccia riga di comando
Cloud Foundry per eseguire manualmente il push della tua applicazione su {{site.data.keyword.Bluemix_notm}}. Per ulteriori informazioni, vedi [Caricamento delle tue applicazioni](../starters/upload_app.html).|
|Eclipse	|Gestisci il tuo codice in Eclipse e utilizza gli strumenti di IBM Eclipse per {{site.data.keyword.Bluemix_notm}} per distribuire la tua applicazione.|
|Integrazione di Git	|Gestisci il tuo codice su GitHub e integra Git
in {{site.data.keyword.Bluemix_notm}}. Puoi collaborare con altri sviluppatori. La tua applicazione viene distribuita
automaticamente in {{site.data.keyword.Bluemix_notm}}
quando esegui il commit delle modifiche nel codice. Non devi eseguire manualmente il push dell'applicazione.|
|{{site.data.keyword.Bluemix_notm}} DevOps
Delivery Pipeline	|Gestisci il tuo codice sul repository DevOps GitHub
e distribuisci la tua applicazione su {{site.data.keyword.Bluemix_notm}}
utilizzando DevOps Delivery Pipeline.|


Se la piattaforma Cloud Foundry non risponde ai requisiti della tua applicazione,
puoi utilizzare un contenitore o una VM in cui il runtime venga configurato
e aggiornato con più opzioni personalizzate.

##Caricamento delle tue applicazioni attraverso la CLI cf
{: #ht_cfcli}

Puoi
gestire il tuo codice su un client locale e utilizzare l'interfaccia riga di comando
Cloud Foundry per caricare manualmente la tua applicazione su {{site.data.keyword.Bluemix_notm}}. Se modifichi il codice, per eseguire il codice aggiornato è necessario che riesegua il push dell'applicazione su
{{site.data.keyword.Bluemix_notm}}.

Per effettuare la migrazione della tua applicazione, attieniti alla seguente procedura:

<ol>
<li>Installa l'interfaccia riga di comando Cloud Foundry. Assicurati
di usare la versione più recente dell'interfaccia riga di comando cf.
<ol>
<li>Scarica il programma di installazione per il tuo sistema
operativo.</li>
<li>Segui la procedura guidata di installazione della riga di comando.</li>
<li>Utilizza il seguente comando per verificare la versione
dell'interfaccia riga di comando cf:
<pre>cf -v</pre></li>
</ol>
</li>

<li>Facoltativo: se desideri specificare e salvare i dettagli di distribuzione prima di distribuire un'applicazione a {{site.data.keyword.Bluemix_notm}}, puoi aggiungere il manifest dell'applicazione effettuando le seguenti operazioni:
<ol>
<li>Passa alla directory di lavoro della tua applicazione e crea un file denominato manifest.yml, che è il nome predefinito.</li>
<li>Specifica i dettagli di distribuzione nel file manifest. Il seguente esempio mostra un file manifest per un'applicazione Java™.
<pre class="pre codeblock"><code>applications:
- disk_quota: 1024M
  host: myjavatest
  name: MyJavaTest
  path: webStarterApp.war
  domain: mybluemix.net
  instances: 1
  memory: 512M</code></pre>
<p>Per ulteriori informazioni sulle
opzioni supportate utilizzabili in questo file, vedi il [Manifesto dell'applicazione](../manageapps/depapps.html#appmanifest).

</p></li></ol>
</li>

<li>Esegui il push della tua applicazione. Puoi caricare la tua applicazione
attraverso il comando cf push.
<ol>
<li>Connettiti ed accedi a {{site.data.keyword.Bluemix_notm}} eseguendo
il seguente comando. Quando richiesto, seleziona la tua organizzazione
e il tuo spazio.
<pre>cf login -a https://api.ng.bluemix.net</pre></li>
<li>Dalla directory della tua applicazione, immetti il comando cf push
seguito dal nome dell'applicazione. Tale nome deve essere univoco
nell'ambiente {{site.data.keyword.Bluemix_notm}}.
<pre>cf push nomeapplicazione</pre></li>
<li>Facoltativo: se utilizzi un pacchetto di build esterno, devi utilizzare l'opzione -b con il comando cf push. Ad
                                    esempio:
<pre>cf push nomeapplicazione -b buildpack_URL</pre>
<p>Per ulteriori informazioni, vedi
Utilizzo di pacchetti di build della community.</p>
</li></ol>
</li>

<li>Facoltativo: se modifichi la tua applicazione, devi caricare queste modifiche immettendo di nuovo il comando cf push. L'Interfaccia
riga di comando cf utilizza le tue opzioni precedenti e le tue risposte
ai prompt per aggiornare con i nuovi bit di codice le eventuali istanze dell'applicazione
in esecuzione.</li>
</ol>

**Note:**

* Quando utilizzi il comando cf push, l'interfaccia riga di comando cf copia tutti i file e tutte le directory dalla tua directory corrente a {{site.data.keyword.Bluemix_notm}}. Assicurati di avere solo i file richiesti nella directory della tua applicazione.
* Accertati che la memoria della tua organizzazione sia sufficiente per tutte le istanze
della tua applicazione. Per visualizzare la quota di memoria per la tua organizzazione, utilizza cf org org_name.
* Per ulteriori informazioni su cf push, vedi [comandi cf](../cli/reference/cfcommands/index.html).

##Migrazione dei tuoi dati e utilizzo dei servizi
{: #ht_service}

Una volta
caricata la tua applicazione su {{site.data.keyword.Bluemix_notm}},
seleziona il servizio a cui è collegata l'applicazione dal Catalogo {{site.data.keyword.Bluemix_notm}},
crea un'istanza di servizio, esegui il bind dell'istanza all'applicazione
e riavvia l'applicazione.

La variabile di ambiente VCAP_SERVICES della tua applicazione è un
oggetto JSON che contiene informazioni su come interagire con un'istanza di servizio
in {{site.data.keyword.Bluemix_notm}}. Tali informazioni includono il nome dell'istanza di servizio, le credenziali e
l'URL di connessione all'istanza di servizio.

Per eseguire il codice su {{site.data.keyword.Bluemix_notm}},
devi aggiungere la logica del codice per l'analisi della variabile VCAP_SERVICES,
al fine di ottenere informazioni sulla connessione al servizio. Modifica la tua applicazione
per acquisire la porta e l'host dell'istanza di servizio assegnati dinamicamente
attraverso le variabili di ambiente. Il seguente esempio mostra come
acquisire le credenziali di un'istanza di servizio Postgre SQL all'interno di un'applicazione
Ruby:

```
services = JSON.parse(ENV['VCAP_SERVICES'], :symbolize_names => true)
        url = services.values.map do |srvs|
          srvs.map do |srv|
            if srv[:credentials][:uri] =~ /^postgres/
              srv[:credentials][:uri]
            else
              []
            end
          end
        end.flatten!.first
```		
{:codeblock}

Per accertarti che la tua applicazione possa essere eseguita in un ambiente locale
una volta modificata l'applicazione per {{site.data.keyword.Bluemix_notm}},
verifica che sia presente la variabile d'ambiente VCAP_SERVICES,
che viene impostata per tutte le applicazioni {{site.data.keyword.Bluemix_notm}} Cloud
Foundry.


# Link correlati
{: #rellinks}

## Link correlati
{: #general}

* [IBM Containers](../containers/container_cli_ov.html)
* [Virtual Machine](../virtualmachines/vm_index.html)
* [Introduzione a Delivery Pipeline](../services/DeliveryPipeline/index.html)
* [Distribuzione di applicazioni con IBM Eclipse Tools for Bluemix](../manageapps/eclipsetools/eclipsetools.html)
* [Twelve-factor app](http://12factor.net/){:new_window}
* [Reaching enterprise backend with Bluemix Secure Gateway via console](https://developer.ibm.com/bluemix/2015/04/01/reaching-enterprise-backend-bluemix-secure-gateway/){:new_window}
