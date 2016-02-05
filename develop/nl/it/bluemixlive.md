{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}

#{{site.data.keyword.Bluemix_notm}} Live Sync {: #live-sync}

*Ultimo aggiornamento: 8 dicembre 2015*  

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

Per ulteriori dettagli sui comandi, vedi la [documentazione della CLI Bluemix Live Sync](../cli/reference/bl/index.html). 

<ol>
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

'applicazione deve utilizzare il pacchetto di build IBM SDK for Node.js. I pacchetti di build personalizzati non sono supportati. 

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


># Link correlati {:class="linklist"}
>## Esercitazioni ed esempi {:id="samples"}
>* [Verificare ed eseguire il debug di un'applicazione Node.js con Bluemix Live Sync](https://hub.jazz.net/tutorials/livesync)
>
># Link correlati {:class="linklist"}
>## Link correlati {:id="general"}
>* [comandi bl](https://www.ng.bluemix.net/docs/cli/bl_cli.html)   
>
>{:elementKind="article" id="rellinks"}
