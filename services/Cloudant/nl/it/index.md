---

copyright:

  anni: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Introduzione a Cloudant
{: #getting-started-with-cloudant}
Ultimo aggiornamento: 12 agosto 2016
{: .last-updated}

{{site.data.keyword.cloudant}} è un DBaaS (document database as a service) che memorizza di dati in JSON.
È creato tenendo presente la scalabilità,
l'alta disponibilità
e la durabilità.
Viene fornito con un'ampia varietà di opzioni di indicizzazione come map-reduce,
Cloudant Query,
full-text e
geospaziale.
La replica delle funzionalità rende più semplice mantenere i dati
sincronizzati tra i cluster di database, i PC desktop e i dispositivi mobili. {:shortdesc}

Puoi avviare la console {{site.data.keyword.cloudant}} dalla pagina di avvio dei servizi nel dashboard Bluemix.

Per utilizzare il servizio, attieniti alla seguente procedura:
<ol>
<li>Crea un'istanza del servizio utilizzando il dashboard Bluemix
o l'interfaccia della riga di comando CloudFoundry.
<p>Per creare un'istanza utilizzando il dashboard,
completa la seguente procedura:
<ol>
<li>Accedi a Bluemix.</li>
<li>Nel dashboard,
fai clic sul link '<code>Work With Data</code>' nel pannello Data &amp; Analytics.</li>
<li>Fai clic sul pulsante '<code>New Service</code>'.</li>
<li>Nell'elenco dei servizi,
fai clic sul pulsante {{site.data.keyword.cloudant}}.</li>
<li>Nella pagina delle informazioni {{site.data.keyword.cloudant}},
fai clic sul pulsante '<code>Choose {{site.data.keyword.cloudant}}</code>'.</li>
<li>Nella pagina del catalogo {{site.data.keyword.cloudant}},
inserisci i dettagli per il servizio di cui hai bisogno.
Fai clic sul pulsante '<code>Create</code>' quando sei pronto a procedere.</li>
<li>Quando l'istanza Cloudant è stata creata,
ti viene presentata con il dashboard per tale istanza.
Fai clic sul link '<code>Service Credentials</code>' per visualizzare tutti i dettagli di cui hai bisogno per accedere alla tua istanza.</li>
</ol>
</p>
<p>Per creare un'istanza utilizzando l'interfaccia della riga di comando CloudFoundry,
completa la seguente procedura: <ol>
<li>Installa lo strumento CloudFoundry <code>cf</code> sul tuo sistema.
Le istruzioni su come eseguire tale operazione sono disponibili nella <a href="https://console.ng.bluemix.net/docs/cli/index.html">Bluemix CLI and dev tools guide</a>.</li>
<li>Crea una nuova istanza del servizio utilizzando il comando:<br/>
<pre><code>cf create-service</code></pre></li>
<li>Ti viene presentata con un elenco di servizi disponibili.
Scegline uno,
quindi immetti un piano e un nome dell'istanza univoci per il servizio.
Viene suggerito un nome casuale per l'istanza,
ma puoi modificarlo con qualsiasi nome preferisci.</li>
<li>Dopo aver creato il servizio,
puoi ottenere un elenco di tutti i servizi che hai creato:<br/>
<pre><code>cf services</code></pre></li>
<li>Prima di usare un servizio nell'applicazione, devi eseguire il bind del servizio alla tua applicazione.
Eseguilo con il comando:<br/>
<pre><code>cf bind-service</code></pre>
Dall'elenco dei risultati,
seleziona una delle applicazioni e uno
dei servizi.
Il comando <code>cf</code> ti notifica quando l'azione di bind ha esito positivo.</li>
</ol>
</p>
</li>
<li><p>Dopo aver creato un'istanza di servizio, saranno visualizzati dei dati JSON simili ai seguenti e sarà possibile visualizzarli nel dashboard Bluemix:<br/>
<pre><code>{
  "cloudantNoSQLDB": {
    "name": "Cloudant-3s",
    "label": "cloudantNoSQLDB",
    "plan": "shared",
    "credentials": {
      "username": "unnomeutente",
      "password": "secret",
      "host": "myhost-bluemix.cloudant.com",
      "port": 443,
      "url": "https://unnomeutente:secret@myhost-bluemix.cloudant.com"
    }
  }
}</code></pre></p>
{: screen}
<p>I dati vengono inoltre aggiunti alla variabile di ambiente <code>VCAP_SERVICES</code> di ogni applicazione Bluemix a cui è associato il servizio.</p>
<p>Le credenziali del servizio vengono memorizzate in un oggetto JSON contenete i seguenti campi:
<ul>
<li><code>key</code>: Il nome del servizio (cloudantNoSQLDB)</li>
<li><code>name</code>: Il nome fornito dall'utente dell'istanza del servizio</li>
<li><code>host</code>: Il nome host del server</li>
<li><code>port</code>: Il numero di porta in cui è in esecuzione il servizio, di norma 443</li>
<li><code>username</code>: Il nome utente per l'autenticazione</li>
<li><code>password</code>: La password per l'autenticazione</li>
<li><code>url</code>: L'URL dell'istanza del servizio</li>
</ul></li>
<li><p>Nelle applicazioni Bluemix, puoi leggere le credenziali dalla variabile di ambiente <code>VCAP_SERVICES</code>. </p>
<p>Nelle applicazioni in esecuzione all'esterno di Bluemix o in un'altra area geografica in
Bluemix, puoi richiamare le credenziali
dal dashboard Bluemix e aggiungerle alla configurazione dell'applicazione.</p>
</li>
<li>Per accedere al database, il meccanismo di base è di inviare
le richieste all'host e alla porta forniti tramite HTTPS, utilizzando il nome utente e la password per l'autenticazione. Le tue richieste possono essere inviate utilizzando diversi linguaggi e piattaforme dell'applicazione,
inclusi:
<ul>
<li><a href="https://github.com/cloudant/sync-android">Android</a></li>
<li><a href="https://github.com/cloudant/CDTDatastore">Apple iOS</a></li>
<li><a href="https://github.com/cloudant/java-cloudant">Java</a></li>
<li><a href="https://github.com/cloudant/objective-cloudant">Objective C and Swift</a></li>
<li><a href="https://github.com/cloudant/python-cloudant">Python</a></li>
</ul>
... e molti altri.
Per ulteriori informazioni consulta la
<a href="https://cloudant.com/for-developers/">Cloudant Developer homepage</a>
e l'elenco delle <a href="http://docs.cloudant.com/libraries.html">Client Libraries</a>.
</li>
<li>Quando la tua applicazione è pronta,
puoi distribuirla all'ambiente Bluemix per la verifica.
Per distribuire un'applicazione,
utilizza il comando:<br/>
<pre><code>cf push</code></pre></li>
<li>Per annullare il bind di un'istanza del servizio a un'applicazione,
utilizza il comando:<br/>
<pre><code>cf unbind-service</code></pre></li>
<li>Per eliminare un'istanza del servizio
utilizza il comando:<br/>
<pre><code>cf delete-service</code></pre></li>
</ol>

Ulteriori informazioni sull'autenticazione al database e su come effettuare le richieste, sono disponibili in [Guida di riferimento API](https://docs.cloudant.com/api.html).

# Link correlati
{: #rellinks}

## Esercitazioni ed esempi
{: #samples}

* [Cloudant client libraries](https://docs.cloudant.com/libraries.html)
* [Using Cloudant with Liberty on Bluemix](https://developer.ibm.com/bluemix/2014/07/08/cloudant_on_bluemix/)
* [Cloudant Guides](https://docs.cloudant.com/guides.html)

## Guida di riferimento alle API
{: #api}

* [Cloudant API reference](https://docs.cloudant.com/api.html)

## Link correlati
{: #general}

* [Cloudant website and dashboard](https://cloudant.com/)
* [Cloudant Blog](https://cloudant.com/blog)
