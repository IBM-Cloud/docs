---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Modifica del codice con Eclipse Orion {{site.data.keyword.webide}}
{: #web_ide}

Ultimo aggiornamento: 26 ottobre 2016
{: .last-updated}

Eclipse Orion {{site.data.keyword.webide}} è un ambiente di sviluppo basato sul browser in cui puoi sviluppare per il web. Puoi sviluppare in JavaScript, HTML e CSS con l'aiuto dell'assistenza del contenuto, del completamento del codice e del controllo errori. {{site.data.keyword.webide}} utilizza quasi tutti i linguaggi e offre l'evidenziazione della sintassi per molti tipi di file [ (il link si apre in una nuova finestra)](https://hub.jazz.net/docs/overview/#dev_support){: new_window}. Il controllo di origine è integrato in Git o Jazz SCM e può distribuire il codice localmente per verificare ed eseguire il debug delle tue applicazioni.
{:shortdesc}

Cosa più importante, {{site.data.keyword.webide}} si avvale della tecnologia web. Non hai nulla da installare, da mantenere e da scalare. Puoi sviluppare ovunque tu abbia una connessione a internet.

## Configurazione dell'editor
{: #editorsetup}

{{site.data.keyword.webide}} è personalizzabile in modo che puoi scegliere gli schemi di colori, gli strumenti tecnici e le impostazioni che incontrano i tuoi bisogni di sviluppo. Per visualizzare e modificare le impostazioni, dal menu a sinistra, fai clic sull'icona **Impostazioni** <img class="inline" src="./images/webide_settings_icon_light.png"  alt="Icona Impostazioni">.

Se durante la modifica hai la necessità di cambiare spesso le impostazioni, puoi accedere rapidamente a esse utilizzando l'icona **Impostazioni dell'editor locali** <img class="inline" src="./images/webide_local_settings_icon_light.png"  alt="Icona Impostazioni dell'editor locali"> nell'angolo superiore destro dell'editor

![Impostazioni dell'editor locali](images/webide_local_editor_settings_light.png)

Per impostazione predefinita, le impostazioni per lo stile dell'editor e la dimensione del carattere vengono sempre visualizzate. Per includere altre impostazioni dell'editor nel menu, completa la seguente procedura:

1. Fai clic sull'icona **Impostazioni dell'editor locali** <img class="inline" src="./images/webide_local_settings_icon_light.png"  alt="Icona Impostazioni dell'editor locali">.

2. Fai clic su **Impostazioni dell'editor**.

3. Per includere o escludere un'impostazione dal menu **Impostazioni dell'editor locali**, fai clic sul circolo vicino all'impostazione.

![Attiva impostazioni dell'editor](images/webide_editor_settings_toggle_light.png)


## Modifica del codice
{: #editcode}

{{site.data.keyword.webide}} ha due sezioni principali. La prima sezione è il navigator dei file sulla sinistra, che mostra i tuoi file del progetto in tre strutture. Dal navigator dei file, puoi creare, ridenominare, eliminare e gestire i tuoi file e cartelle.

**Suggerimento:** per caricare i file nel navigator dei file, trascinaceli dal tuo computer.

La seconda sezione è il pannello dell'editor sulla destra. L'editor fornisce diverse funzioni di scrittura del codice, tra cui l'assistenza del contenuto e la convalida della sintassi.

![Web IDE](images/webide_light.png)

### Utilizzo di più file
1. Per lavorare con due file contemporaneamente, fai clic sull'icona **Modifica modalità di suddivisione editor** <img class="inline" src="./images/webide_split_editor_icon_light.png"  alt="Icona Suddivisione editor"> nella parte superiore dell'editor.
2. Dal menu che si apre, seleziona una vista.

 Dopo avere selezionato la vista, se era già stato aperto un file nell'editor, viene visualizzato in entrambe le viste dell'editor.

 Per aprire o modificare un file visualizzato in una delle due viste dell'editor:
 1. Sposta il cursore del mouse nella vista editor che desideri modificare.
 2. Nel navigator dei file, fai clic su un file.

### Tasti di scelta rapida
Molti dei comandi in {{site.data.keyword.webide}} sono accessibili tramite dei tasti di scelta rapida.

Per visualizzare un elenco dei tasti di scelta rapida nell'editor, premi Alt+Shift+?. Se stai utilizzando un SO Mac, premi Ctrl+Shift+?.

## Gestione del codice di origine
{: #sourcecontrol}

{{site.data.keyword.webide}} è integrata con gli strumenti di gestione del codice di origine. Per lavorare con il repository Git, fai clic sull'icona **Repository Git** <img class="inline" src="./images/webide_git_icon_light.png"  alt="Icona Repository Git">. Per ulteriori informazioni, consulta [Source control with Git (il link si apre in una nuova finestra)](https://hub.jazz.net/docs/git/){: new_window}.


## Distribuzione di un'applicazione dal tuo spazio di lavoro
{: #deploy}

1. Per distribuire la tua applicazione, dalla barra del menu, seleziona o [crea (il link si apre in una nuova finestra)](https://hub.jazz.net/tutorials/livesync/#launch_configuration){: new_window} una configurazione di avvio.
1. Fai clic sull'icona di distribuzione <img class="inline" src="./images/webide_deploy_button_light.png"  alt="L'icona di distribuzione">. Viene distribuita un'istanza alla tua applicazione utilizzando i contenuti correnti del tuo spazio di lavoro e l'ambiente definito nella tua configurazione di avvio. 
2. Dopo che la tua applicazione è stata distribuita, puoi utilizzare la barra di esecuzione per arrestare, riavviare o eseguire il debug della applicazione, dei log di visualizzazione o di altro.
![Barra di esecuzione](images/webide_runbar_light.png)

 ## Modifica al di fuori di {{site.data.keyword.webide}}
{: #editlocal}

Per utilizzare un editor all'esterno di {{site.data.keyword.webide}}, configura {{site.data.keyword.Bluemix_live}} in modo che tu possa lavorare direttamente con i tuoi file del progetto in qualsiasi strumento. {{site.data.keyword.Bluemix_live_notm}} è un'applicazione della riga di comando che sincronizza le modifiche nel tuo file system locale con lo spazio di lavoro nel cloud in {{site.data.keyword.jazzhub}}. 

### Attività preliminari 

Scarica e installa la CLI (command-line interface) di [{{site.data.keyword.Bluemix_live_notm}} (il link si apre in una nuova finestra)](http://livesyncdownload.ng.bluemix.net){: new_window}.

### Sincronizzazione del tuo ambiente locale con {{site.data.keyword.Bluemix_notm}}
{: #edit_local_download}

1. Apri una finestra della riga di comando.
2. Accedi a {{site.data.keyword.Bluemix_notm}}:

	```
	bl login
	```
	{: pre}

3. Quando ti viene richiesto, immetti il tuo ID IBM e la password.
4. Visualizza un elenco dei tuoi progetti {{site.data.keyword.Bluemix_notm}}: 

	```
	bl projects
	```
	{: pre}

4. Sincronizza il tuo ambiente locale con il tuo progetto in {{site.data.keyword.Bluemix_notm}}:

	```
	bl sync projectName
	```
	{: pre}

dove `projectName` è il tuo nome dell'applicazione {{site.data.keyword.Bluemix_notm}}.

Quando hai finito le modifiche, immetti `q` per terminare la sincronizzazione.

### Abilitazione della funzione Desktop Sync per modificare il codice localmente

La funzione Desktop Sync è simile alla modalità Live Edit per la riga di comando. Hai bisogno della funzione Desktop Sync per eseguire il debug nella riga di comando.
1. In un'altra finestra della riga di comando, abilita la funzione Desktop Sync:

	```
	cd localDirectory
	bl start
	```
	{: codeblock}

2. Utilizza la configurazione di avvio che hai creato in {{site.data.keyword.webide}}. Dopo che hai selezionato la configurazione di avvio, la funzione Desktop Sync viene abilitata nel tuo ambiente locale. Nella finestra della riga di comando che hai appena aperto, puoi visualizzare l'URL dell'applicazione, di debug, di gestione e visualizzare lo stato di {{site.data.keyword.Bluemix_live_notm}}.

3. Aggiorna il browser e verifica che puoi visualizzare le modifiche che hai salvato nei file statici nello spazio di lavoro locale. 

### Disabilitazione della funzione Desktop Sync

1. In una seconda finestra della riga di comando, immetti `bl stop`.
2. Nella prima finestra della riga di comando, immetti `q`.
