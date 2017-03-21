---

copyright:
  years: 2015, 2017
lastupdated: "2017-2-21"

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#Incorporazione di una distribuzione nel flusso iFrame {{site.data.keyword.Bluemix_notm}}
{: #embed-d2bm-iframe}


Puoi incorporare la distribuzione nel flusso {{site.data.keyword.Bluemix_notm}} come
un iFrame in molti tipi di contenuto che supportano le markup. Ad esempio, puoi incorporare l'iFrame nei file readme, nei blog, negli articoli e nelle pagine web.

{: shortdesc}

Il flusso iFrame è utile quando desideri mantenere il branding della tua azienda. Quando le persone fanno clic sul tuo iFrame incorporato, restano nel
tuo contenuto invece di essere reindirizzati al sito web di bluemix.net. Se non sei interessato al branding dell'azienda, puoi inserire un [pulsante Distribuisci a {{site.data.keyword.Bluemix_notm}}](/docs/develop/deploy_button.html) standard nel contenuto invece dell'iFrame.

##Passi nel flusso iFrame {: #iframe-steps}

1. Se non hai un account {{site.data.keyword.Bluemix_notm}} attivo,
procedi alla creazione di un account di prova.

2. Puoi selezionare una regione, un'organizzazione (org), uno spazio e un nome applicazione. Il nome applicazione consigliato viene creato dal nome applicazione precedente, dal tuo nome utente e dalla data/ora.

3. Il ramo master del repository Git pubblico originale viene clonato in un nuovo progetto {{site.data.keyword.jazzhub_short}} privato con un nuovo repository Git.

4. Se l'applicazione richiede un file di build, esso viene rilevato automaticamente e l'applicazione viene creata.

5. L'applicazione viene distribuita alla tua organizzazione {{site.data.keyword.Bluemix_notm}}.

##Esempi del flusso iFrame {: #iframe-example}

<p>
<a class="xref" href="http://d2bm-iframe-sample.ng.bluemix.net/" target="_blank" title="(Si apre in una nuova scheda o finestra)">IBM
Bluemix D2BM iFrame Sample<img class="image" src="../icons/launch-glyph.svg" alt="icona link esterno"/></a> fornisce un esempio di flusso iFrame per un repository Git pubblico.<div class="image"><img class="image" src="images/d2bm_iframe_sample2.png" alt="Esempio di flusso iFrame Distribuisci a Bluemix" /></div>
</p>

<p>
Per visualizzare l'origine per questo esempio, fai clic su <a class="xref" href="https://hub.jazz.net/project/idsorg/d2bm-iframe-sample/overview" target="_blank" title="(Si apre in una nuova scheda o finestra)">origine<img class="image" src="../icons/launch-glyph.svg" alt="icona link esterno"/></a>.
</p>

##Incorporazione del flusso iFrame {: #embed-iframe}  

<ol>
<li>Carica il programma di utilità JavaScript da <a class="xref" href="https://bluemix.net/deploy/embed.js" target="_blank" title="(Si apre in una nuova scheda o finestra)">https://bluemix.net/deploy/embed.js<img class="image" src="../icons/launch-glyph.svg" alt="icona link esterno"/></a>. Questo programma di utilità dipende da jQuery e viene caricato aggiungendo la seguente tag di script al tuo documento:
<pre class="pre">
<code>&lt;script type="text/javascript" src="https://bluemix.net/deploy/embed.js"&gt;&lt;/script&gt;</code>
</pre>
</li>
<li> Istanzia il constructor <code>DeployToBluemixIFrame</code> utilizzando questi argomenti:

<dl class="parml">
<dt class="pt dlterm">domNodeId</dt>
<dd class="pd">L'ID del domNode in cui desideri inserire l'iFrame nel tuo contenuto.</dd>

<dt class="pt dlterm">callback</dt>
<dd class="pd">Questo argomento viene richiamato quando il flusso iFrame viene completato oppure
se si verifica un errore. L'argomento risponde con il risultato. Il seguente frammento di
codice mostra un callback del risultato che ha avuto esito positivo:</dd>

<dt class="pt dlterm">args</dt>
<dd class="pd">L'oggetto che contiene i parametri di input al widget. Sono disponibili i seguenti parametri:

<dl class="parml">

<dt class="pt dlterm">repository</dt>
<dd class="pd">Il repository Git da utilizzare come origine per la clonazione e la distribuzione. Questo valore è obbligatorio.</dd>

<dt class="pt dlterm">app_name</dt>
<dd class="pd">Il nome applicazione predefinito da utilizzare come valore specifico nel campo <strong>app_name</strong> all'interno
dell'iFrame. Questo valore è facoltativo.</dd>


<dt class="pt dlterm">region_id</dt>
<dd class="pd">L'ID della regione di destinazione predefinita. Ad esempio: <code>ibm:yp:us-south</code>. Questo valore è facoltativo.</dd>

<dt class="pt dlterm">organization_guid</dt>
<dd class="pd">Il guid dell'organizzazione di destinazione predefinita. Per trovare questo valore, fai clic su <strong>Gestisci organizzazioni</strong> > <i>nome_organizzazione</i>. L'URL per l'organizzazione contiene il guid per tale organizzazione. Questo valore è facoltativo.</dd>

<dt class="pt dlterm">space_guid</dt>
<dd class="pd">Il guid dello spazio di destinazione predefinito. Per trovare questo valore, fai clic su <strong>Gestisci organizzazioni</strong> > <i>nome_spazio</i>. L'URL per lo spazio
contiene il guid per tale spazio. Questo valore è facoltativo.</dd>

<dt class="pt dlterm">auto_login</dt>
<dd class="pd">Specifica se l'iFrame effettua automaticamente l'accesso dell'utente. Il
valore predefinito è <code>true</code>. Questo valore è facoltativo.</dd>

<dt class="pt dlterm">width</dt>
<dd class="pd">La larghezza dell'iFrame. Questo valore è facoltativo. Il valore predefinito è <code>620</code>.</dd>

<dt class="pt dlterm">height</dt>
<dd class="pd">L'altezza dell'iFrame. Questo valore è facoltativo. Il
valore predefinito è <code>470</code>.</dd>
</dl>

</dd>
</dl>
</li>
</ol>  

**Suggerimento:** per ridurre al minimo l'interazione con l'iFrame, puoi precompilare i campi **app_name**, **region_id**, **organization_guid**, **space_guid** e **auto_login**.
