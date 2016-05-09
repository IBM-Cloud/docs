---

 

copyright:

  years: 2015, 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Caricamento della tua applicazione
*Ultimo aggiornamento: 17 febbraio 2016*

Dopo che hai eseguito l'accesso a {{site.data.keyword.Bluemix}}, puoi caricare la tua applicazione con il comando cf push.
{:shortdesc}

Prima di iniziare, devi:
  1. Installa le interfacce riga di comando {{site.data.keyword.Bluemix}} e Cloud Foundry.

  <a class="xref" href="http://clis.ng.bluemix.net/ui/home.html" target="_blank" title="(Si apre in una nuova scheda o finestra)"><img class="image" src="images/btn_bx_commandline.svg" alt="Scarica l'interfaccia riga di comando {{site.data.keyword.Bluemix}}" /> </a>  <a class="xref" href="https://github.com/cloudfoundry/cli/releases" target="_blank" title="(Si apre in una nuova scheda o finestra)"><img class="image" src="images/btn_cf_commandline.svg" alt="Scarica l'interfaccia riga di comando Cloud Foundry" /> </a> 

  2. Stabilisci una connessione a {{site.data.keyword.Bluemix}}.

  <pre class="pre">bluemix api https://api.<span class="keyword" data-hd-keyref="DomainName">DomainName</span></pre>
  
  3. Accedi a {{site.data.keyword.Bluemix_notm}}.

  <pre class="pre">bluemix login -u <var class="keyword varname" data-hd-keyref="user_ID">nome_utente</var> -o <var class="keyword varname" data-hd-keyref="org_name">nome_organizzazione</var> -s <var class="keyword varname" data-hd-keyref="space_name">nome_spazio</var></pre>

Quando viene immesso un comando **cf push**, l'interfaccia riga di comando **cf** fornisce
la directory di lavoro all'ambiente {{site.data.keyword.Bluemix_notm}} che usa
un pacchetto di build per creare ed eseguire l'applicazione.

  1. Dalla directory dell'applicazione, immetti il comando **cf
push** con il nome dell'applicazione. Il nome dell'applicazione deve essere univoco nell'ambiente {{site.data.keyword.Bluemix_notm}}.
  
  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -m 512m</pre>
  
  {{site.data.keyword.Bluemix_notm}} include
i pacchetti di build integrati. In alcuni casi, anche per i pacchetti di build integrati, devi fornire inoltre un'opzione -c per specificare il comando utilizzato per avviare la tua applicazione. Ad esempio, devi usare l'opzione -c per distribuire la tua applicazione Node.js:
  
  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -c start_command</pre>
  
  Inoltre, l'applicazione Node.js deve contenere un file package.json valido.

  La distribuzione di tutti gli altri pacchetti di build esterni deve essere eseguita utilizzando l'opzione -b. Ad
esempio:

  <pre class="pre">cf push <var class="keyword varname" data-hd-keyref="app_name">app_name</var> -b buildpack_URL</pre>
  
  **Suggerimento:** quando utilizzi il comando **cf push**, l'interfaccia riga di comando **cf** copia tutti i file e tutte le directory dalla tua directory corrente a Bluemix. Assicurati di avere solo i file richiesti nella directory della tua applicazione.

  Il comando cf push carica e distribuisce la tua applicazione a {{site.data.keyword.Bluemix_notm}}. Per ulteriori informazioni su cf push, vedi [Comandi cf](../cli/reference/cfcommands/index.html). Per informazioni sui pacchetti di build, vedi [Utilizzo dei pacchetti di build della community](../cfapps/byob.html).

  2. Se modifichi la tua applicazione, puoi caricare tali modifiche immettendo nuovamente il comando cf push. L'Interfaccia
riga di comando cf utilizza le tue opzioni precedenti e le tue risposte
ai prompt per aggiornare con i nuovi bit di codice le eventuali istanze dell'applicazione
in esecuzione.

**Suggerimento:** puoi anche caricare o distribuire un'applicazione da DevOps Services. Vedi [Developing a {{site.data.keyword.Bluemix_notm}} application
in Node.js with the Web IDE](https://hub.jazz.net/tutorials/devopsweb/){: new_window}.
