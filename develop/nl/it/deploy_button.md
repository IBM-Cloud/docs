---

 

copyright:

  years: 2015, 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


#Creazione di un pulsante Distribuisci a {{site.data.keyword.Bluemix_notm}} {: #deploy-button} 

*Ultimo aggiornamento: 2 marzo 2016* 

Il pulsante Distribuisci a {{site.data.keyword.Bluemix}} è un modo efficiente per condividere la tua applicazione originata da Git pubblica in modo che altri utenti possano sperimentarne il codice ed eseguirne la distribuzione a IBM {{site.data.keyword.Bluemix_notm}}. Il pulsante
richiede una configurazione minima e puoi inserirlo dovunque siano supportate le markup. Un utente che fa clic sul pulsante crea
una copia clonata del codice in un nuovo repository Git in modo che la tua applicazione originale rimanga invariata. 
{: shortdesc} 

**Suggerimento:** se il branding dell'azienda è importante, puoi [incorporare un flusso iFrame Distribuisci a {{site.data.keyword.Bluemix_notm}}](../develop/deploy_button_embed.html) nel tuo contenuto invece di inserire un pulsante. Quando le persone creano una copia clonata della tua applicazione
originata da Git pubblica, restano nel tuo contenuto invece di essere reindirizzati al sito web di bluemix.net. 

Quando qualcuno fa clic sul tuo pulsante, si verificano le seguenti azioni: 

1. Se la persona non ha un account {{site.data.keyword.Bluemix}} attivo,
è necessario che venga creato un account di prova. 

2. La persona può selezionare una regione, organizzazione, spazio e nome applicazione. Il nome applicazione consigliato viene creato in base al nome applicazione precedente,
al nome utente della persona e all'ora. 

3. Il ramo master del repository Git pubblico originale viene clonato in un nuovo progetto {{site.data.keyword.jazzhub_title}} privato con un nuovo repository Git. 

4. Se l'applicazione richiede un file di build, esso viene rilevato automaticamente e l'applicazione viene creata. 

5. Se per il processo di creazione e distribuzione è stata configurata una pipeline, l'applicazione viene distribuita con un file `pipeline.yml`.

6. Se l'applicazione richiede un contenitore, per distribuire l'applicazione in un contenitore {{site.data.keyword.Bluemix_notm}} vengono utilizzati un file `pipeline.yml`, che definisce il servizio **IBM Containers**, e un Dockerfile, che definisce un'immagine. 

7. L'applicazione viene distribuita all'organizzazione {{site.data.keyword.Bluemix_notm}} della persona. 

##Esempi del pulsante {: #button-examples} 

Vedi un esempio di pulsante dell'applicazione per un repository {{site.data.keyword.jazzhub_short}} pubblico:

<p>
<a class="xref" href="https://bluemix.net/deploy?repository=https://hub.jazz.net/git/idsorg/sample-java-cloudant" target="_blank" title="(Si apre in una nuova scheda o finestra)"><img class="image" src="images/deploy_buttonx2.png" alt="Distribuisci a Bluemix" /></a>
</p> 

Vedi
un esempio di pulsante dell'applicazione per un repository GitHub pubblico: 

<p>
<a class="xref" href="https://bluemix.net/deploy?repository=https://github.com/ibmjstart/bluemix-node-mysql-uploader" target="_blank" title="(Si apre in una nuova scheda o finestra)"><img class="image" src="images/deploy_buttonx2.png" alt="Distribuisci a Bluemix" /></a>
</p> 

Vedi un esempio
di pulsante per un'applicazione distribuita in un contenitore {{site.data.keyword.Bluemix_notm}}: 

<p>
<a class="xref" href="https://bluemix.net/deploy?repository=https://github.com/Puquios/hello-containers" target="_blank" title="(Si apre in una nuova scheda o finestra)"><img class="image" src="images/deploy_buttonx2.png" alt="Distribuisci a Bluemix" /></a>
</p> 

##Creazione di un pulsante {: #create-button}

Per creare un pulsante Distribuisci a {{site.data.keyword.Bluemix_notm}}: 

<ol>
<li> Copia e modifica uno dei seguenti template di frammento e includi un repository Git pubblico.
<p></p>
<p>
<strong>Suggerimento</strong>: se vuoi specificare l'input di build per un progetto DevOps Services, aggiungi un parametro di ramo all'URL Git. Quando aggiungi un parametro di ramo, il repository Git pubblico originale, inclusi tutti i sui rami, viene clonato in un nuovo progetto DevOps Services privato con un nuovo repository Git. Il ramo Git specificato viene impostato come input per il lavoro di build. Se non specifichi un ramo, l'input per il lavoro di build viene impostato sul ramo master per impostazione predefinita.
</p>
<ul>
<li>HTML:
<p>
Ramo master predefinito:
</p>
<pre class="codeblock">
&lt;a href="https://bluemix.net/deploy?repository=&lt;git_repository_URL>" # [required]&gt;&lt;img src="https://bluemix.net/deploy/button.png" alt="Deploy to Bluemix"&gt;&lt;/a&gt;
</pre>
<p>
Ramo Git specificato:
</p>
<pre class="codeblock">
&lt;a href="https://bluemix.net/deploy?repository=&lt;git_repository_URL&gt;&branch=&lt;git_branch>" # [required]&gt;&lt;img src="https://bluemix.net/deploy/button.png" alt="Deploy to Bluemix"&gt;&lt;/a&gt;
</pre>
</li>
<li>Markdown:
<p>
Ramo master predefinito:
</p>
<pre class="codeblock">
[&#33;[Deploy to Bluemix]&#40;https://bluemix.net/deploy/button.png&#41;]&#40;https://bluemix.net/deploy?repository=&lt;git_repository_URL> # [required]&#41;
</pre>
<p>Ramo Git specificato:
</p>
<pre class="codeblock">
[&#33;[Deploy to Bluemix]&#40;https://bluemix.net/deploy/button.png&#41;]&#40;https://bluemix.net/deploy?repository=&lt;git_repository_URL> &branch=&lt;git_branch&gt; # [required]&#41;
</pre>
</li>
</ul>
</li>
<li>Inserisci il frammento in blog, articoli, wiki, file readme o dovunque tu desideri
promuovere la tua applicazione. 
</li>
</ol>

##Considerazione sul frammento per il pulsante {: #button-snippet}

Consulta queste considerazioni quando personalizzi il frammento per il pulsante Distribuisci a Bluemix. 

* Entrambi i template utilizzano un percorso predefinito a un'immagine pulsante esterna in formato PNG e in inglese. 

    * Se preferisci utilizzare un'immagine SVG per il pulsante invece di un PNG, è disponibile una versione SVG. Puoi modificare il
percorso all'immagine pulsante esterna utilizzata nel frammento impostandolo come `https://bluemix.net/deploy/button.svg`.
	
	* Se preferisci utilizzare un'immagine più grande per il pulsante, è disponibile un'immagine PNG la cui dimensione è il doppio di quella originale. Puoi
modificare il percorso dell'immagine pulsante esterna utilizzata nel frammento impostandolo come `https://bluemix.net/deploy/button_x2.png`. 
	
	* Se preferisci memorizzare l'immagine localmente, puoi scaricare l'immagine e memorizzarla nel repository Git. Regola il percorso per utilizzare l'ubicazione relativa dell'immagine. 
	
	* Se vuoi utilizzare una versione tradotta del pulsante, puoi fare riferimento a esso in remoto oppure scaricarlo da [ftp://public.dhe.ibm.com/cloud/bluemix/deploy_button](ftp://public.dhe.ibm.com/cloud/bluemix/deploy_button). 
	
##Considerazione sul repository per il pulsante {: #button-repo} 

Consulta queste considerazioni per il repository del progetto che utilizzerai nel pulsante Distribuisci a Bluemix. 

<ul>
<li>Non è necessario che un <code>manifest.yml</code> sia presente nel
tuo repository. Tuttavia, se la tua applicazione richiede che siano eseguiti degli altri servizi, devi
fornire un file manifest che dichiara tali servizi.  

Con il file manifest, puoi specificare: 
    <ul>
    <li>Un nome applicazioni univoco.</li>  
    <li>Declared services: un'estensione manifest, che crea o cerca i servizi obbligatori o facoltativi di cui è prevista la configurazione prima che venga distribuita l'applicazione, come ad esempio il servizio di memorizzazione nella cache dei dati. Puoi trovare un elenco dei piani, delle etichette e dei servizi {{site.data.keyword.Bluemix_notm}} idonei utilizzando l'<a href="https://github.com/cloudfoundry/cli/releases">interfaccia riga di comando CF</a> per eseguire il comando <code>cf marketplace</code> oppure sfogliando il <a href="https://console.ng.bluemix.net/?ssoLogout=true&cm_mmc=developerWorks-*-dWdevcenter-*-devops-services-_-lp#/store"> catalogo {{site.data.keyword.Bluemix_notm}} </a>.

    
    <strong>Nota:</strong> è un'estensione IBM del formato manifest Cloud Foundry standard. Questa estensione potrebbe essere modificata in una futura release man mano che la funzione si evolve e viene migliorata.
	
	<a href="http://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html#minimal-manifest" target="_blank">Impara come creare un file <code>manifest.yml</code>.</a>  
<pre class="codeblock">
	---
    #Template manifest.yml

  declared-services:
    &lt;`nome_istanza_servizio_arbitrario`&gt;:  # [obbligatorio]
      label: &lt;`nome_servizio_effettivo`&gt; # [obbligatorio] Il nome servizio effettivo dal marketplace
      plan: Shared # [facoltativo] Se fornito, utilizzato per richiamare il servizio dichiarato. Altrimenti, assume come valore predefinito 'Free' o 'free'.
  applications:
  - services
    - &lt;`nome_istanza_servizio_arbitrario`&gt;
    name: &lt;`nomeapplicazione`&gt;
    host: &lt;`apphostname`&gt;
</pre>

<pre class="codeblock">
	---
    #Esempio di manifest.yml

  declared-services: 
      sample-java-cloudant-cloudantNoSQLDB:
        label: cloudantNoSQLDB
        plan: Shared
  applications:
  - services
    - sample-java-cloudant-cloudantNoSQLDB
    name: My app
    host: myapp
</pre>
   </li>
   </ul>
	<li> Se il repository deve essere creato prima che venga distribuita l'applicazione, viene attivato un build automatico del codice nel repository
prima della distribuzione. I build automatici si verificano quando nella directory root del repository viene rilevato un file script di
build. 
	
	Builder supportati: 
	    <ul>
		<li> <a href="http://ant.apache.org/manual/using.html" target="_blank">Ant:</a> /<code>build.xml</code>, che crea l'output nella cartella <code>./output/</code> </li>
		<li> <a href="http://docs.cloudfoundry.org/buildpacks/java/build-tool-int.html#gradle" target="_blank">Gradle:</a> <code>/build.gradle</code>, che crea l'output nella cartella <code>. </code> </i>
		<li> <a href="http://gruntjs.com/getting-started#the-gruntfile" target="_blank">Grunt:</a> <code>/Gruntfile.js</code>,
che crea l'output nella cartella <code>.</code> </li>
		<li> <a href="http://docs.cloudfoundry.org/buildpacks/java/build-tool-int.html#maven" target="_blank">Maven: </a> <code>/pom.xml</code>, che
crea l'output nella cartella <code>./target/</code></li>
	   </ul>
	</li>	
	<li>Per configurare la pipeline per il progetto, includi un file <code>pipeline.yml</code> in una directory <code>.bluemix</code>. Puoi creare un file <code>pipeline.yml</code> manualmente oppure puoi generarne uno da un progetto DevOps Services esistente. Per creare un file pipeline.yml da un progetto {{site.data.keyword.jazzhub_short}} e aggiungerlo al tuo repository, completa questa procedura. 
<ol>
<li>Apri il progetto DevOps Services in un browser e fai clic su <b>Crea e distribuisci</b>.</li>
<li>Configura la tua pipeline con i lavori di creazione e distribuzione.</li>
<li>Nel tuo browser, aggiungi <code>/yaml</code> all'URL del pipeline del progetto e premi Invio. 
<br>Esempio: <code>https://hub.jazz.net/pipeline/<proprietario>/<nome_progetto>/yaml</code></li>
<li>Salva il file <code>pipeline.yml</code> risultante.</li>
<li>Nella directory root del tuo progetto, crea una directory <code>.bluemix</code>.</li>
<li>Carica il file <code>pipeline.yml</code> nel repository <code>.bluemix</code>.</li>
</ol> </li>
	<li>Se stai distribuendo un'applicazione in un contenitore tramite <strong>IBM Containers</strong>, devi includere Dockerfile nella directory root del repository e un file <code>pipeline.yml</code> in una directory <code>.bluemix</code>. 
	<ul>
	    <li> Per saperne di più sulla creazione dei Dockerfile, <a href="https://docs.docker.com/reference/builder/" target="_blank">vedi la documentazione di Docker</a>. </li>
	    <li>Puoi creare un file <code>pipeline.yml</code> manualmente oppure puoi generarne uno da un progetto DevOps Services esistente. Per creare manualmente un file <code>pipeline.yml</code> specifico per i contenitori, <a href="https://github.com/Puquios/" target="_blank">vedi gli esempi in GitHub</a>. </li>
        </ul>

 </li>
 </ul>
</ul>

Per un aiuto nella risoluzione dei problemi, vedi [Il pulsante Distribuisci a Bluemix non distribuisce un'applicazione](../troubleshoot/index.html#deploytobluemixbuttondoesntdeployanapp){:new_window}.	
