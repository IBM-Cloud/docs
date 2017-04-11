---



copyright:
  years: 2015，2017
lastupdated: "2017-3-10"

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}

#{{site.data.keyword.Bluemix_notm}} Live Sync
{: #live-sync}

 
Se stai creando un'applicazione Node.js, puoi utilizzare {{site.data.keyword.Bluemix}} Live Sync per aggiornare rapidamente l'istanza dell'applicazione su {{site.data.keyword.Bluemix_notm}} e sviluppare senza la ridistribuzione manuale.    
{: shortdesc}

Quando apporti una modifica,
puoi vedere tale modifica nell'applicazione {{site.data.keyword.Bluemix_notm}} in esecuzione
immediatamente. {{site.data.keyword.Bluemix_notm}} Live Sync funziona  
<!--from both the command line and -->
in Eclipse Orion Web IDE (Web IDE). Puoi eseguire il debug delle applicazioni scritte in Node.js utilizzando {{site.data.keyword.Bluemix_notm}} Live Sync.  

{{site.data.keyword.Bluemix_notm}} Live Sync si articola in due funzioni.
<!-- three -->

<!--
**Desktop Sync**  

You can synchronize any desktop directory tree with a cloud-based project workspace similar to the way Dropbox works. The Web IDE directly edits the same cloud-based workspace, so both stay in sync. Desktop Sync works for any kind of application. To use Desktop Sync, you need to download and install the BL command line interface.  
-->

**Live Edit**

Puoi apportare modifiche a un'applicazione Node.js in esecuzione in {{site.data.keyword.Bluemix_notm}} e verificarla subito nel tuo browser. Qualsiasi modifica da te apportata nel Web IDE viene propagata immediatamente al file system dell'applicazione.  

**Debug**  

Mentre un'applicazione Node.js è in modalità Live Edit, puoi accedere a essa mediante shell ed
eseguirne il debug. Puoi modificare il codice in modo dinamico, inserire dei punti
di interruzione, analizzare in dettaglio il codice, riavviare il runtime e altro ancora,
utilizzando il programma di debug Node Inspector.  

<!-- You can use Desktop Sync to keep your desktop workspace in sync with the cloud-based project workspace that you edit directly with the Web IDE. -->

Puoi utilizzare Live Edit per propagare le modifiche nello spazio di lavoro del progetto basato sul cloud alla tua
applicazione in esecuzione. 
<!-- You can use one or both of these features. And if you use Desktop Sync or -->
Se utilizzi Live Edit per passare la tua applicazione alla modalità Live Edit, puoi eseguire il debug della tua applicazione in esecuzione.


Il processo Bluemix Live Sync è illustrato nel seguente diagramma.    

Figura 1. Processo Bluemix Live Sync
    

![Immagine del processo Bluemix Live Sync](images/bluemix-live-sync.png)

Se stai sviluppando un'applicazione Java in esecuzione su Liberty, puoi eseguire il debug in remoto utilizzando [Eclipse Tools for Bluemix](/docs/manageapps/eclipsetools/eclipsetools.html#eclipsetools).


##Live Edit {: #live-edit}

Se stai creando un'applicazione Node.js, quando apporti modifiche al tuo progetto utilizzando Web IDE, la funzione Live Edit di {{site.data.keyword.Bluemix_notm}} Live Sync può aggiornare rapidamente l'istanza dell'applicazione in esecuzione su {{site.data.keyword.Bluemix_notm}}. Live Edit ti consente di effettuare attività di sviluppo come faresti sul desktop senza eseguire nuovamente la distribuzione.

Live Edit è supportato solo per le applicazioni Node.js.

In Eclipse Orion Web IDE (Web IDE), nella barra di esecuzione, fai clic su **Live Edit**.

![Immagine della barra di esecuzione con Live Edit](images/bluemix-live-sync-light.png)

Live Edit ti consente di visualizzare rapidamente in anteprima le modifiche alle applicazioni Node.js in esecuzione su {{site.data.keyword.Bluemix_notm}}. Quando aggiorni
il tuo codice con Live Edit attivato, puoi aggiornare la finestra del browser
della tua applicazione web per vedere tali modifiche riflesse entro pochi secondi
da quando le hai apportate.

<!--
For a tutorial on using the Live Edit feature of {{site.data.keyword.Bluemix_notm}} Live Sync, see the tutorial [Test and debug a Node.js app with Bluemix Live Sync![External link icon](../icons/launch-glyph.svg "External link icon")](https://hub.jazz.net/tutorials/livesync){:new_window}.
-->

Quando modifichi i file nel tuo Web IDE, ne viene eseguita automaticamente la ridistribuzione alla tua applicazione in esecuzione su {{site.data.keyword.Bluemix_notm}}. Se devi riavviare l'applicazione Node, puoi utilizzare il pulsante **Riavvia** nella barra di esecuzione.

**NOTA:** per un'esperienza più congruente durante l'utilizzo della funzione Live Edit di {{site.data.keyword.Bluemix_notm}} Live Sync, sono richiesti 256MB di ulteriore memoria e saranno aggiunti.

##Debug di {{site.data.keyword.Bluemix_notm}}
Live {: #live-debug}

Puoi accedere alla funzione Debug di {{site.data.keyword.Bluemix_notm}} Live Sync se {{site.data.keyword.Bluemix_notm}} Live Sync è abilitato per la tua applicazione Node.js.

Con la funzione di debug, puoi modificare il codice in modo dinamico, inserire dei punti di interruzione, analizzare in dettaglio il codice, riavviare il runtime e altro ancora, e tutto questo mentre la tua applicazione viene servita da {{site.data.keyword.Bluemix_notm}}. Puoi sviluppare in modo incrementale la tua applicazione in modo agile, grazie alla possibilità di scegliere
da un ampio elenco di servizi {{site.data.keyword.Bluemix_notm}}.

Debug di {{site.data.keyword.Bluemix_notm}} Live
include le seguenti funzioni:

* Controllo del runtime dell'applicazione
* Debug utilizzando [node-inspector![icona link esterno](../icons/launch-glyph.svg "External link icon")](https://github.com/node-inspector/node-inspector){:new_window}
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

Distribuisci l'applicazione e vai quindi a `https://app-host.mybluemix.net/bluemix-debug/manage` per accedere all'interfaccia utente di debug {{site.data.keyword.Bluemix_notm}}. Quando ti viene richiesto di autenticarti, immetti il tuo ID utente e il token di accesso personale o la password dell'ID IBM.    

<!--
   **Note**: Your user ID for DevOps Services can be either an IBMid or a federated ID (corporate ID). If you use federated authentication, to log in to your Bluemix Live Sync command-line client, you must use a personal access token instead of a password. If you don't use federated authentication, your IBMid and password work with all clients. For more information about creating a personal access token, see [What's federated authentication and how does it affect me?![External link icon](../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/devops-services/2016/06/23/whats-federated-authentication-and-how-does-it-affect-me/){:new_window}
   -->

###Ripristino delle configurazioni dell'applicazione e disabilitazione di Debug di Bluemix Live {: #restore_live_debug}

1. Rimuovi la variabile di ambiente ENABLE_BLUEMIX_DEV_MODE dal file `manifest.yml` dell'applicazione.

2. Ripristina il comando di avvio originale e il valore di memoria dell'applicazione.

3. Distribuisci l'applicazione.


## Link correlati
{: #general}

* [Eclipse tools for Bluemix![icona link esterno](../icons/launch-glyph.svg "External link icon")](https://www.ng.bluemix.net/docs/manageapps/eclipsetools/eclipsetools.html){:new_window}
