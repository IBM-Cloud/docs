---



copyright:

  years: 2015, 2016



---
{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}

#{{site.data.keyword.Bluemix_notm}} Live Sync {: #live-sync}

*Ultimo aggiornamento: 08 aprile 2016*  

Se stai creando un'applicazione Node.js, puoi utilizzare {{site.data.keyword.Bluemix}} Live Sync per aggiornare rapidamente l'istanza dell'applicazione su {{site.data.keyword.Bluemix_notm}} e sviluppare come faresti sul desktop senza rieseguire la distribuzione.   
{: shortdesc}

Quando apporti una modifica,
puoi vedere tale modifica nell'applicazione {{site.data.keyword.Bluemix_notm}} in esecuzione
immediatamente. {{site.data.keyword.Bluemix_notm}} Live Sync funziona sia dalla riga di comando sia in Web IDE. Puoi eseguire il debug delle applicazioni scritte in Node.js utilizzando {{site.data.keyword.Bluemix_notm}} Live Sync.  

{{site.data.keyword.Bluemix_notm}} Live Sync si articola in tre funzioni.

**Desktop Sync**  
    Puoi sincronizzare qualsiasi struttura ad albero di directory desktop con uno spazio di lavoro di progetto basato sul cloud con una modalità di funzionamento simile a quella di Dropbox. Web IDE modifica direttamente lo stesso spazio di lavoro basato sul cloud; in questo modo, entrambi restano sincronizzati. Desktop
Sync funziona per qualsiasi tipo di applicazione. Per utilizzare Desktop Sync, devi scaricare
e installare l'interfaccia riga di comando BL.  

**Live Edit**
    Puoi apportare modifiche a un'applicazione Node.js in esecuzione in {{site.data.keyword.Bluemix_notm}} e verificarla subito nel tuo browser. Qualsiasi modifica da te apportata in una directory desktop sincronizzata o in Web IDE viene propagata immediatamente al file system dell'applicazione.  

**Debug**  
    Mentre un'applicazione Node.js è in modalità Live Edit, puoi accedere a essa mediante shell ed
eseguirne il debug. Puoi modificare il codice in modo dinamico, inserire dei punti
di interruzione, analizzare in dettaglio il codice, riavviare il runtime e altro ancora,
utilizzando il programma di debug Node Inspector.  

Puoi utilizzare Desktop Sync per tenere il tuo spazio di lavoro desktop sincronizzato con lo spazio di lavoro del progetto basato sul cloud che modifichi direttamente con  Web IDE. Puoi utilizzare Live Edit per propagare le modifiche nello spazio di lavoro del progetto basato sul cloud alla tua
applicazione in esecuzione. Puoi utilizzare una di queste funzioni o entrambe. Se inoltre utilizzi Desktop Sync o Live Edit per passare la tua applicazione alla modalità Live Edit, puoi eseguire il debug della tua applicazione in esecuzione.

Il processo Bluemix Live Sync è illustrato nel seguente diagramma.

*Figura 1. Processo Bluemix Live Sync*
![Immagine del processo Bluemix Live Sync](images/bluemix-live-sync.png)

Se stai sviluppando un'applicazione Java in esecuzione su Liberty, puoi eseguire il debug in remoto utilizzando [Eclipse Tools for Bluemix](../manageapps/eclipsetools/eclipsetools.html#eclipsetools).

##Desktop Sync {: #desktop-sync}

Puoi utilizzare la funzione Desktop Sync di Bluemix Live Sync per aggiornare rapidamente l'istanza dell'applicazione su {{site.data.keyword.Bluemix_notm}} ed eseguire attività di sviluppo come faresti sul desktop.

Per Desktop Sync valgono le seguenti considerazioni:
* Desktop Sync viene eseguito nei seguenti sistemi operativi:
  * Windows 7 o 8
  * Mac OS X versione 10.9 o successive
      **Nota:** Windows richiede .NET Framework versione 4.5. Se non hai .NET installato, ti viene richiesto di installarlo quando installi l'interfaccia riga di comando {{site.data.keyword.Bluemix_notm}} Live Sync.  
* Non devi necessariamente clonare il tuo repository Git.
* Indipendentemente dal tipo di applicazione che stai sviluppando, puoi
sincronizzare il tuo progetto desktop con lo spazio di lavoro cloud.
* Se la tua applicazione è scritta in Node.js, puoi propagare le modifiche alle applicazioni in esecuzione.

Per ulteriori dettagli sui comandi, vedi [Comandi Bluemix Live Sync (bl)](bluemixlive.html#bl-commands).

<ol>
<li>Registrati per un account <a class="xref" href="https://hub.jazz.net/" target="_blank" alt="Bluemix DevOps Services">Bluemix DevOps Services</a> gratuito.</li>
<li>Scarica e installa la riga di comando bl di {{site.data.keyword.Bluemix_notm}} Live Sync.   
<p>
<a class="xref" href="http://livesyncdownload.ng.bluemix.net/downloads/blive_setup.msi" target="_blank" title="(Si apre in una nuova scheda o finestra)"><img class="image" src="images/bl_gs_icons_windows_b.svg" alt="Pulsante Scarica la riga di comando bl per Windows" /> </a>
<a class="xref" href="http://livesyncdownload.ng.bluemix.net/downloads/BluemixLive.pkg" target="_blank" title="(Si apre in una nuova scheda o finestra)"><img class="image" src="images/bl_gs_icons_mac-osx_b.svg" alt="Pulsante Scarica la riga di comando bl per Mac" /> </a>
</p>  

<strong>Importante:</strong> lo strumento riga di comando bl è disponibile solo per  Windows 7 e 8 e per Mac OS X versione 10.9 o successive. </li>

<li>Su una riga di comando, accedi utilizzando il seguente comando. Ti verranno richiesti il tuo ID e la tua password IBM.  
<pre class="codeblock">bl login</pre>
</li>

<li>Visualizza l'elenco dei progetti disponibili per la sincronizzazione di {{site.data.keyword.Bluemix_notm}} Live Sync immettendo il seguente comando:
<pre class="codeblock">bl projects</pre>
<p>Trova il nome progetto nell'elenco che corrisponde alla
tua applicazione. Il nome del progetto ha il formato <i>alias</i> | <i>nome applicazione</i>. </p>
</li>
<li>Sincronizza il tuo ambiente locale con il tuo progetto su {{site.data.keyword.Bluemix_notm}} immettendo
il seguente comando. Se sei il proprietario del progetto, devi specificare solo il nome-della-tua-applicazione per nomeProgetto.
<pre class="codeblock">bl sync projectName -d localDirectory --verbose</pre>
<p>L'esecuzione di questo comando (così come la sincronizzazione) continua finché
non si immette una "q". L'opzione --verbose visualizza informazioni sulla registrazione e sullo stato. Se qualcuno dei tuoi argomenti contiene uno spazio, devi racchiudere il nome tra virgolette. </p></li>
<li>In un'altra finestra di riga di comando, nella tua directory locale, distribuisci l'applicazione a {{site.data.keyword.Bluemix_notm}} in
modalità Live Edit immettendo il seguente comando:
<pre class="codeblock">bl start</pre>
</li>
</ol>

Quando modifichi i file nella tua directory locale, le modifiche vengono propagate automaticamente sia
all'applicazione che è in esecuzione su {{site.data.keyword.Bluemix_notm}} sia
allo spazio di lavoro cloud del progetto. Se devi riavviare l'applicazione Node, puoi utilizzare
il comando:
```
bl start --restart
```

##Live Edit {: #live-edit}

Se stai creando un'applicazione Node.js, quando apporti modifiche al tuo progetto utilizzando Web IDE, la funzione Live Edit di {{site.data.keyword.Bluemix_notm}} Live Sync può aggiornare rapidamente l'istanza dell'applicazione in esecuzione su {{site.data.keyword.Bluemix_notm}}. Live Edit ti consente di effettuare attività di sviluppo come faresti sul desktop senza eseguire nuovamente la distribuzione.

Live Edit è supportato solo per le applicazioni Node.js.

In Web IDE, nella barra di esecuzione, fai clic su **Live Edit**.

![Immagine della barra di esecuzione con Live Edit](images/run-bar-live-edit.png)

Live Edit ti consente di visualizzare rapidamente in anteprima le modifiche alle applicazioni Node.js in esecuzione su {{site.data.keyword.Bluemix_notm}}. Quando aggiorni
il tuo codice con Live Edit attivato, puoi aggiornare la finestra del browser
della tua applicazione web per vedere tali modifiche riflesse entro pochi secondi
da quando le hai apportate.

Per un'esercitazione sull'utilizzo della funzione Live Edit di {{site.data.keyword.Bluemix_notm}} Live Sync, consulta l'esercitazione [Verificare ed eseguire il debug di un'applicazione Node.js con Bluemix Live Sync](https://hub.jazz.net/tutorials/livesync).

Quando modifichi i file nel tuo Web IDE, ne viene eseguita automaticamente la ridistribuzione alla tua applicazione in esecuzione su {{site.data.keyword.Bluemix_notm}}. Se devi riavviare l'applicazione Node, puoi utilizzare il pulsante **Riavvia** nella barra di esecuzione.

**Nota:** per un'esperienza più congruente durante l'utilizzo della funzione Live Edit di {{site.data.keyword.Bluemix_notm}} Live Sync, sono richiesti 256MB di ulteriore memoria e saranno aggiunti.

##Debug di {{site.data.keyword.Bluemix_notm}}
Live {: #live-debug}

Puoi accedere alla funzione Debug di {{site.data.keyword.Bluemix_notm}} Live Sync se {{site.data.keyword.Bluemix_notm}} Live Sync è abilitato per la tua applicazione Node.js.

Con la funzione di debug, puoi modificare il codice in modo dinamico, inserire dei punti di interruzione, analizzare in dettaglio il codice, riavviare il runtime e altro ancora, e tutto questo mentre la tua applicazione viene servita da {{site.data.keyword.Bluemix_notm}}. Puoi sviluppare in modo incrementale la tua applicazione in modo agile, grazie alla possibilità di scegliere
da un ampio elenco di servizi {{site.data.keyword.Bluemix_notm}}.

Debug di {{site.data.keyword.Bluemix_notm}} Live
include le seguenti funzioni:

* Controllo del runtime dell'applicazione
* Debug utilizzando [node-inspector](https://github.com/node-inspector/node-inspector)
* Accesso shell

###Controllo del runtime dell'applicazione {: #app-runtime}

Con il controllo del runtime dell'applicazione, puoi utilizzare Debug
per ispezionare lo stato dell'applicazione in fase di avvio. Questa funzionalità è utile
quando cerchi di risolvere il problema di un'applicazione che si arresta in modo anomalo all'avvio.

Mentre sviluppi la tua applicazione, puoi scegliere tra le seguenti
azioni:

* Eseguire un rapido riavvio dell'applicazione
* Sospendere l'applicazione prima di eventuali esecuzioni di codice

###Debug {: #debug}

Debug include le seguenti funzionalità:

**Limitazione:** è richiesto Google Chrome.

* Impostare dei punti di interruzione nel codice applicativo per mettere in pausa l'esecuzione a una specifica
riga.
* Modificare le condizioni del punto di interruzione per mettere in pausa l'esecuzione
sono quando sono soddisfatti degli specifici criteri.
* Controllare lo stato di campi e variabili locali.
* Visualizzare l'output di debug dalle chiamate `console.log()` immediatamente. Quest'azione
è più rapida del monitoraggio dei log cf.
* Utilizzare l'editor di codice sorgente integrato per apportare delle modifiche
immediate, seppur temporanee, al codice applicativo in esecuzione.

###Shell {: #shell}

Questo strumento ti dà l'accesso shell al contenitore in cui
è in esecuzione la tua applicazione. Usando questo terminale, puoi eseguire in remoto
dei comandi shell di diagnostica per amministrare la tua applicazione.

Esegui il monitoraggio della memoria e dell'utilizzo della CPU all'interno dell'istanza che utilizza i comandi Linux standard, come **top**, **ps** e **kill**.

###Configurazione di un'applicazione per abilitare Debug di {{site.data.keyword.Bluemix_notm}}
Live {: #configure_app_debug}

L'applicazione deve utilizzare il pacchetto di build IBM SDK for Node.js. I pacchetti di build personalizzati non sono supportati.

1. Consenti al pacchetto di build di rilevare il comando di avvio applicazione. Il comando start deve essere rilevato automaticamente dal pacchetto di build, non impostato nel file `manifest.yml`.  

    a. Assicurati che il file `package.json` contenga uno script start che include un comando start per l'applicazione.  
    b. Se il file `manifest.yml` dell'applicazione contiene un comando, impostalo su null.  

2. Imposta la variabile di ambiente.  

    a. Nel file `manifest.yml`, aggiungi questa variabile:
	```
	env:
      ENABLE_BLUEMIX_DEV_MODE: "true"
	```

3. Aumenta la memoria.  

    a. Nel file `manifest.yml` dell'applicazione, aggiungi 128 M o più al valore specificato per l'attributo memoria.

Una volta installato Debug di {{site.data.keyword.Bluemix_notm}} Live,
puoi utilizzare gli strumenti debug.

Distribuisci l'applicazione e vai quindi a `https://app-host.mybluemix.net/bluemix-debug/manage` per accedere all'interfaccia utente di debug {{site.data.keyword.Bluemix_notm}}. Quando ti viene richiesto, immetti il tuo ID e la tua password IBM per autenticarti.

###Ripristino delle configurazioni dell'applicazione e disabilitazione di Debug di Bluemix Live {: #restore_live_debug}

1. Rimuovi la variabile di ambiente ENABLE_BLUEMIX_DEV_MODE dal file `manifest.yml` dell'applicazione.

2. Ripristina il comando di avvio originale e il valore di memoria dell'applicazione.

3. Distribuisci l'applicazione.

## Comandi {{site.data.keyword.Bluemix_notm}} Live Sync (bl)  {: #bl-commands}

Se stai creando un'applicazione Node.js, puoi usare {{site.data.keyword.Bluemix_live}} per
aggiornare rapidamente l'istanza dell'applicazione in esecuzione su {{site.data.keyword.Bluemix_notm}} e sviluppare
come faresti sul desktop senza rieseguire la distribuzione. Quando apporti una modifica,
puoi vedere tale modifica nell'applicazione {{site.data.keyword.Bluemix_notm}} in esecuzione
immediatamente. L'interfaccia riga di comando {{site.data.keyword.Bluemix_live}} è denominata *bl*.
{:shortdesc}

Puoi utilizzare i comandi dell'interfaccia riga di comando **bl** per completare le seguenti attività:

* Avviare e arrestare un'applicazione in esecuzione su {{site.data.keyword.Bluemix_notm}}.
* Creare un nuovo progetto basato sul cloud dal tuo desktop.
* Sincronizzare le modifiche dal tuo desktop allo spazio di lavoro del progetto basato sul cloud e all'applicazione
in esecuzione su {{site.data.keyword.Bluemix_notm}}.
* Visualizzare l'elenco di progetti disponibili per la sincronizzazione.
* Visualizzare lo stato delle applicazioni in esecuzione.

Per ulteriori informazioni sul download e l'utilizzo del comando bl, vedi [Bluemix Live Sync](../develop/bluemixlive.html).

## comandi bl

La riga di comando {{site.data.keyword.Bluemix_live}}, **bl**, ha la seguente sintassi:

```
bl command [arguments][options] [--help]
```

### Comandi
<dl>
<dt>login, l</dt>
<dd>Accedi a {{site.data.keyword.Bluemix_notm}}.</dd>
<dt>logout, lo</dt>
<dd>Disconnettere l'utente.</dd>
<dt>sync, s</dt>
<dd>Avviare il processo di sincronizzazione tra il desktop e il server.</dd>
<dt>create, c</dt>
<dd>Crea un progetto privato, lo collega al repository Git in questa directory e distribuisce
il contenuto a {{site.data.keyword.Bluemix_notm}}.</dd>
<dt>projects, p</dt>
<dd>Elencare tutti i progetti disponibili per la sincronizzazione.</dd>
<dt>start, st</dt>
<dd>Avvia l'istanza dell'applicazione in {{site.data.keyword.Bluemix_notm}}.</dd>
<dt>stop, sp</dt>
<dd>Arresta l'istanza dell'applicazione in {{site.data.keyword.Bluemix_notm}}.</dd>
<dt>status, ss</dt>
<dd>Elenca lo stato dell'istanza dell'applicazione in esecuzione in {{site.data.keyword.Bluemix_notm}}.</dd>
</dl>

### Argomenti
<dl>
<dd>Argomenti per il comando.</dd>
</dl>

### Opzioni
<dl>
<dd>Opzioni per il comando.</dd>
</dl>

### Opzioni globali
<dl>
<dt>--help</dt>
<dd>Visualizzare la pagina di guida per lo specifico comando</dd>
<dt>--verbose</dt>
<dd>Abilitare la registrazione dettagliata.</dd>
</dl>

**Nota:** se qualche argomento od opzione contiene uno spazio, racchiudi il valore tra virgolette doppie.

## help

```
bl [ command ] --help
```

### Utilizzo
<dl>
<dd>Utilizza questo comando per visualizzare la guida su un comando o l'elenco di comandi.</dd>
</dl>

### Esempi

Il seguente comando visualizza l'elenco di comandi:

```bl --help```

Il seguente comando mostra informazioni dettagliate sul comando sync:

```bl sync --help```

## login

```bl login|l [ -u username ][-p password ][ -s server ]```

### Scopo

Utilizza questo comando per accedere a {{site.data.keyword.Bluemix_notm}}. È necessario
effettuare l'accesso solo una volta per sessione.

**Avvertenza:** fornire la tua password come opzione della riga di comando è sconsigliato poiché visibile agli altri e registrata nell'ambito della cronologia dei comandi.

**Nota:** devi registrarti per un account <a class="xref" href="https://hub.jazz.net/" target="_blank" alt="Bluemix DevOps Services">Bluemix DevOps Services</a> gratuito.

### Opzioni

<dl>
<dt>-u username</dt>
<dd>Il tuo ID IBM da utilizzare per accedere a {{site.data.keyword.Bluemix_notm}}.</dd>
<dt>-p password</dt>
<dd>La password del tuo ID IBM.</dd>
<dt>-s server</dt>
<dd>Nome server o indirizzo IP del server {{site.data.keyword.jazzhub_short}}.</dd>
</dl>

### Esempi

Questo comando richiede sia un *nome utente* sia
una *password*:

```bl login```

Questo comando fa effettuare l'accesso all'utente, `name@company.com:`

```bl login –u name@company.com –p pa55w0rd```

Questo comando fa effettuare l'accesso all'utente, `name@company.com` con la password pa55 w0rd che contiene uno spazio e che pertanto richiede delle virgolette:

```bl login –u name@company.com –p “pa55 w0rd”```

## logout

```
bl logout|lo
```

### Scopo

<dl>
<dd>Utilizzare questo comando per la disconnessione.</dd>
</dl>

## Progetti

```
bl projects|p
```

### Scopo

<dl>
<dd>Utilizzare questo comando per elencare tutti i progetti disponibili per la sincronizzazione
da parte dell'utente che ha effettuato l'accesso.</dd>
</dl>

## sync

```
bl sync|s nomeProgetto -d directoryLocale [ --overwritelocal ][ --overwriteremote ] [ --verbose ]
```

### Scopo

<dl>
<dd>Utilizzare questo comando per avviare la sincronizzazione dei contenuti di un progetto con la tua
directory locale. Questo comando viene eseguito finché non viene immesso <code>q</code>. Questo comando può, facoltativamente, visualizzare un log di tutte le modifiche di stato di file e applicazioni.</dd>
</dl>

### Argomento

<dl>
<dt>nomeProgetto</dt>
<dd>Il nome progetto nel formato <i>“alias | mproject”</i> o semplicemente
<i>myproject</i>, se il progetto appartiene all'utente che ha effettuato
l'accesso.</dd>
</dl>

### Opzioni

<dl>
<dt>-d directoryLocale</dt>
<dd>Il percorso della directory locale. Il valore predefinito è la cartella corrente ".".</dd>
<dt>--overwritelocal</dt>
<dd>Sovrascrivere la directory locale con i contenuti dello spazio di lavoro del progetto.</dd>
<dt>--overwriteremote</dt>
<dd>Sovrascrivere lo spazio di lavoro del progetto con i contenuti della directory locale.</dd>
<dt>--verbose</dt>
<dd>Visualizzare la registrazione dettagliata.</dd>
</dl>

### Esempi

Questo comando inizia la sincronizzazione con il progetto associato
se la directory corrente è una destinazione di sincronizzazione
esistente. Se la directory corrente è vuota e non è una destinazione di sincronizzazione esistente, il comando richiede un *nomeProgetto*. Se la directory corrente non
è vuota e non è una destinazione di sincronizzazione esistente,
è richiesta un'opzione di sovrascrittura.

```
bl sync
```

Questo comando inizia la
sincronizzazione ed è equivalente a
```bl sync “alias | myproject”```
se il progetto
appartiene all'utente che ha effettuato l'accesso.

```bl sync  myproject```

Questo comando
inizia la sincronizzazione con il progetto <code>my pro ject</code> il cui nome contiene
degli spazi ed è pertanto racchiuso tra virgolette:

```bl sync “my pro ject”```

Questo comando avvia la sincronizzazione del progetto <code>myproject</code> con la directory myfolder:

```bl sync myproject –d  myfolder```

## create

```
bl create|c [ -n NOME_PROGETTO ][ -r REGION ] [ -o ORG ][ -s SPACE ] [ -g REPOSITORY_GIT ][-e GIT_EXE ] [ --creds ][ --fork ] [ --public ][ --prompt ]
```

### Scopo
<dl>
<dd>Utilizza questo comando da una directory che contiene il codice per
creare un progetto privato, collegarlo a un repository Git e distribuire
il contenuto del repository a {{site.data.keyword.Bluemix_notm}}.</dd>
</dl>

### Opzioni

<dl>
<dt>-n NOME_PROGETTO</dt>
<dd>Un nome per il tuo progetto. Valore predefinito: il nome della directory corrente.</dd>
<dt>-r REGIONE</dt>
<dd>Una regione {{site.data.keyword.Bluemix_notm}}. Valore predefinito: Stati Uniti Sud</dd>
<dt>-o ORG</dt>
<dd>Un'organizzazione {{site.data.keyword.Bluemix_notm}}. Valore predefinito: la prima organizzazione trovata.</dd>
<dt>-s SPAZIO</dt>
<dd>Uno spazio {{site.data.keyword.Bluemix_notm}}. Valore predefinito: il primo spazio trovato.</dd>
<dt>-g REPOSITORY_GIT</dt>
<dd>Nome del repository remoto da utilizzare per un qualsiasi repository Git esistente. Valore predefinito: origine</dd>
<dt>-e EXE_GIT</dt>
<dd>Percorso completo di un eseguibile Git. Valore predefinito: rilevato.</dd>
<dt>--creds</dt>
<dd>Richiedere le credenziali Git.</dd>
<dt>--fork</dt>
<dd>Biforcare questa directory e creare un progetto e un repository.</dd>
<dt>--public</dt>
<dd>Rendere pubblico il nuovo progetto.</dd>
<dt>--prompt</dt>
<dd>Richiedere tutte le opzioni necessarie con le scelte disponibili.</dd>
</dl>

### Esempi

Questo comando avvia il processo per creare un progetto privato e
richiede un nome progetto da utilizzare.

```bl create```

Questo
comando crea un progetto pubblico denominato <code>myNewProject</code>.

```bl create -n mioNuovoProgetto --public```

## status

```
bl status|ss [ nomeProgetto ]
```

### Scopo

<dl>
<dd>Utilizzare questo comando per elencare lo stato delle applicazioni associate alle configurazioni di avvio
nella directory <code>./launchConfigurations</code>.</dd>
</dl>

###Argomento

<dl>
<dt>nomeProgetto</dt>
<dd>Il nome progetto nel formato “alias | myproject” o semplicemente myproject, se il progetto appartiene all'utente che ha effettuato l'accesso.</dd>
</dl>

### Esempi

Questo esempio visualizza lo stato delle applicazioni in esecuzione. Se la directory corrente è una destinazione di sincronizzazione esistente,
utilizza il progetto associato. Se la directory corrente non è una destinazione di
sincronizzazione esistente, il comando richiede il <i>nomeProgetto</i>.

````bl status```

Questo esempio visualizza lo stato del progetto myproject che è equivalente a
```bl status “alias | myproject”```
se il progetto
appartiene all'utente che ha effettuato l'accesso.

```bl status myproject```

Questo esempio
visualizza lo stato dell'applicazione in esecuzione associata al progetto <code>my pro ject</code> il cui nome
contiene degli spazi ed è pertanto racchiuso tra virgolette:

```bl status “my pro ject”```

## start

```
bl start|st nomeProgetto [ -l percorsoConfigurazioneAvvio ] -m percorsoManifest ] [ --liveedit ][--noliveedit ] [ --restart ]
```

### Scopo

<dl>
<dd>Utilizzare questo comando per avviare l'istanza dell'applicazione descritta
dal file di avvio o da quello manifest. L'applicazione viene avviata
in modalità Live Edit per impostazione predefinita, se il pacchetto di build
dell'applicazione supporta Live Edit. Una volta avviata, vengono visualizzati gli URL per l'applicazione,
gli strumenti di debug e il dashboard {{site.data.keyword.Bluemix_notm}}.</dd>
</dl>

### Argomento

<dl>
<dt>nomeProgetto</dt>
<dd>Il nome progetto nel formato <i>“alias | myproject”</i> o semplicemente
<i>myproject</i>, se il progetto appartiene all'utente che ha effettuato
l'accesso.</dd>
</dl>

### Opzioni

<dl>
<dt>-l configurazioneAvvio</dt>
<dd>Il nome della configurazione di avvio (ad esempio <code>mylaunchconfig</code>),
il nome file (ad esempio <code>mylaunchconfig.launch</code>) o un
percorso relativo al progetto al file di configurazione di avvio (ad esempio <code>launchConfigurations/mylaunchconf.launch</code>).</dd>
<dt>-m percorsoManifest</dt>
<dd>Il percorso relativo al progetto al file manifest (ad esempio <code>manifest.yml</code>).</dd>
<dt>--liveedit</dt>
<dd>Avviare l'applicazione associata in modalità Live Edit o uscire con un errore se
il pacchetto di build non supporta la modalità Live Edit.</dd>
<dt>--noliveedit</dt>
<dd>Avviare l'applicazione associata in modalità normale.</dd>
<dt>--view</dt>
<dd>Aprire un browser dell'applicazione in esecuzione.</dd>
<dt>--restart</dt>
<dd>Riavviare un'applicazione già in esecuzione in modalità Live Edit senza rieseguirne la
distribuzione.</dd>
</dl>

### Esempi

Questo comando avvia un'istanza dell'applicazione di <code>myproject</code> associata
al file di avvio <code>launchConfigurations/my.launch</code>.

```bl start myproject –l “launchConfigurations/my.launch”```

Questo comando avvia un'istanza dell'applicazione del progetto associato alla directory corrente con il file di avvio <code>launchConfigurations/my.launch</code>. Se la directory corrente non è una destinazione di sincronizzazione, viene visualizzato un errore.

```bl start –l “launchConfigurations/my.launch” ```

Questo comando avvia un'istanza dell'applicazione del progetto associato alla directory corrente con il file manifest <code>manifest.yml</code>. Le informazioni specificate nel manifest sono utilizzate per creare un nuovo file di configurazione di avvio. Questo comando ti richiede le restanti informazioni obbligatorie e avvia quindi l'applicazione descritta dalla configurazione di avvio:

```bl start –m “mymanifest.yml” ```

Questo comando avvia un'istanza dell'applicazione del progetto associato alla directory corrente con il file manifest <code>manifest.yml</code> ed è equivalente a
```bl start –m manifest.yml```.

```bl start```

## stop

```
bl stop|sp nomeProgetto [ -l configurazioneAvvio ]
```

### Scopo

<dl>
<dd>Utilizzare questo comando per arrestare l'istanza dell'applicazione associata al file di avvio.</dd>
</dl>

### Argomento

<dl>
<dt>nomeProgetto</dt>
<dd>Il nome progetto nel formato “alias | mproject” o semplicemente mproject, se il progetto appartiene all'utente che ha effettuato l'accesso.</dd>
</dl>

### Opzioni

<dl>
<dt>-l configurazioneAvvio</dt>
<dd>Il nome della configurazione di avvio (ad esempio <code>mylaunchconfig</code>),
il nome file (ad esempio <code>mylaunchconfig.launch</code>) o un
percorso relativo al progetto al file di configurazione di avvio (ad esempio <code>launchConfigurations/mylaunchconf.launch</code>).</dd>
</dl>

### Esempi

Questo comando arresta l'applicazione se la directory corrente è una
destinazione di sincronizzazione; in caso contrario esce con un errore. Se non ci sono configurazioni di avvio,
questo comando esce con un errore. Se c'è più di una configurazione di avvio, il comando ti richiede quella da
arrestare.

```bl stop```

Questo comando arresta un'istanza dell'applicazione del progetto in
esecuzione con il file di avvio <code>mylaunchConfig</code>.

```bl stop myproject –l “mylaunchConfig” ```

Questo comando arresta l'applicazione se la directory corrente è una destinazione di sincronizzazione del progetto associato che è stato avviato con il file di avvio <code>launchConfigurations/mylaunchconfig.launch</code>;
in caso contrario, esce con un errore:

```bl stop –l “launchConfigurations/mylaunchconfig.launch” ```  

># Link correlati {:class="linklist"}
>## Esercitazioni ed esempi {:id="samples"}
>* [Verificare ed eseguire il debug di un'applicazione Node.js con Bluemix Live Sync](https://hub.jazz.net/tutorials/livesync)
>
># Link correlati {:class="linklist"}
>## Link correlati {:id="general"}
>* [Eclipse tools for Bluemix](https://www.ng.bluemix.net/docs/manageapps/eclipsetools/eclipsetools.html)   
>
>{:elementKind="article" id="rellinks"}
