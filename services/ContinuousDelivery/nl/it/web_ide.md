---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-25"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Sviluppo con Eclipse Orion Web IDE
{: #web_ide}

Eclipse Orion {{site.data.keyword.webide}} è un ambiente di sviluppo basato sul browser in cui puoi sviluppare per il web. Puoi sviluppare in JavaScript, HTML e CSS con l'aiuto dell'assistenza del contenuto, del completamento del codice e del controllo errori. {{site.data.keyword.webide}} utilizza quasi tutti i linguaggi e offre l'evidenziazione della sintassi per molti tipi di file. Il controllo di origine è integrato e può distribuire il codice localmente per verificare ed eseguire il debug delle tue applicazioni.
{:shortdesc}

Cosa più importante, {{site.data.keyword.webide}} si avvale della tecnologia web. Non hai nulla da installare, da mantenere e da scalare. Puoi sviluppare ovunque tu abbia una connessione a internet.

## Configurazione dell'IDE
{: #editorsetup}

{{site.data.keyword.webide}} è personalizzabile in modo che puoi scegliere gli schemi di colori, gli strumenti tecnici e le impostazioni che incontrano i tuoi bisogni di sviluppo. Per visualizzare e modificare le impostazioni, dal menu a sinistra, fai clic sull'icona **Impostazioni** <img class="inline" src="images/webide_settings_icon_light_small.png"  alt="L'icona impostazioni">.

Se durante la modifica hai la necessità di cambiare spesso le impostazioni, puoi accedere rapidamente a esse utilizzando l'icona **Impostazioni dell'editor locali** <img class="inline" src="images/webide_local_settings_icon_light_small.png"  alt="Icona Impostazioni dell'editor locali">. 

![Impostazioni dell'editor locali](images/webide_local_editor_settings_light.png)

Per impostazione predefinita, le impostazioni per lo stile dell'editor e la dimensione del carattere vengono sempre visualizzate. Per includere altre impostazioni dell'editor nel menu, completa la seguente procedura:

1. Fai clic sull'icona **Impostazioni dell'editor locali** <img class="inline" src="images/webide_local_settings_icon_light_small.png"  alt="Icona Impostazioni dell'editor locali">.

2. Fai clic su **Impostazioni dell'editor**.

3. Per includere o escludere un'impostazione dal menu **Impostazioni dell'editor locali**, fai clic sulla stella accanto a ogni impostazione.

![Attiva impostazioni dell'editor](images/webide_editor_settings_toggle_light.png)


## Modifica del codice
{: #editcode}

{{site.data.keyword.webide}} ha due sezioni principali. La prima sezione è il navigator dei file, che mostra i tuoi file del progetto in tre strutture. Dal navigator dei file, puoi creare, ridenominare, eliminare e gestire i tuoi file e cartelle.

**Suggerimento:** per caricare i file nel navigator dei file, trascinaceli dal tuo computer.

La seconda sezione è il pannello dell'editor. L'editor fornisce diverse funzioni di scrittura del codice, tra cui l'assistenza del contenuto e la convalida della sintassi.

![Web IDE](images/webide_light.png)

### Utilizzo di più file
1. Per lavorare con due file contemporaneamente, fai clic sull'icona **Modifica modalità di suddivisione editor** <img class="inline" src="images/webide_split_editor_icon_light_small.png"  alt="Icona Suddivisione editor">.
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

{{site.data.keyword.webide}} è integrata con gli strumenti di gestione del codice di origine. Per lavorare con il repository Git, fai clic sull'icona **Repository Git** <img class="inline" src="images/webide_git_icon_light_small.png"  alt="Icona Repository Git">. 

 **Suggerimento**: se stai utilizzando {{site.data.keyword.webide}} con le toolchain aperte, il tuo spazio di lavoro viene prepopolato con GitHub,  {{site.data.keyword.ghe_short}} o i repository Git e del tracciamento del problema. I repository associati con la tua toolchain corrente sono evidenziati.


## Distribuzione di un'applicazione dal tuo spazio di lavoro
{: #deploy}

1. Per distribuire la tua applicazione, dalla barra del menu, seleziona o crea una configurazione di avvio.
1. Fai clic sull'icona di distribuzione <img class="inline" src="images/webide_deploy_button_light_small.png"  alt="L'icona di distribuzione">. Viene distribuita un'istanza alla tua applicazione utilizzando i contenuti correnti del tuo spazio di lavoro e l'ambiente definito nella tua configurazione di avvio. 
2. Dopo che la tua applicazione è stata distribuita, puoi utilizzare la barra di esecuzione per arrestare, riavviare o eseguire il debug della applicazione, dei log di visualizzazione o di altro.
![Barra di esecuzione](images/webide_runbar_light.png)    

<!-- 3/6/2016: bl commands don't work with V2/CD 
## Editing outside of the {{site.data.keyword.webide}}
{: #editlocal}

To use an editor besides the {{site.data.keyword.webide}}, set up {{site.data.keyword.Bluemix_live}} so that you can work directly with your project files in any tool. {{site.data.keyword.Bluemix_live_notm}} is a command-line application that synchronizes the changes in your local file system with your cloud workspace in {{site.data.keyword.jazzhub}}. 

### Before you begin 

Download and install the [{{site.data.keyword.Bluemix_live_notm}} command-line interface![External link icon](../../icons/launch-glyph.svg "External link icon")](http://livesyncdownload.ng.bluemix.net){: new_window}.

### Synchronizing your local environment with {{site.data.keyword.Bluemix_notm}}
{: #edit_local_download}

1. Open a command-line window.
2. Sign in to {{site.data.keyword.Bluemix_notm}}:

	```
	bl login
	```
	{: pre}

3. When you are prompted, enter your IBMid and password.
4. View a list of your {{site.data.keyword.Bluemix_notm}} projects: 

	```
	bl projects
	```
	{: pre}

4. Synchronize your local environment with your project on {{site.data.keyword.Bluemix_notm}}:

	```
	bl sync projectName
	```
	{: pre}

where `projectName` is your {{site.data.keyword.Bluemix_notm}} app's name.

When you are finished editing, enter `q` to end synchronization.

### Enabling the Desktop Sync feature to edit code locally

The Desktop Sync feature is like Live Edit mode for the command line. You need the Desktop Sync feature to debug on the command line.
1. In another command-line window, enable the Desktop Sync feature:

	```
	cd localDirectory
	bl start
	```
	{: codeblock}

2. Use the launch configuration that you created in the {{site.data.keyword.webide}}. After you select the launch configuration, the Desktop Sync feature is enabled in your local environment. In the command-line window that you just opened, you can view the app's URL, the debug URL, the manage URL, and view the {{site.data.keyword.Bluemix_live_notm}} state.

3. Refresh the browser and verify that you can see the changes that you saved to static files in the local workspace. 

### Disabling the Desktop Sync feature

1. In the second command-line window, enter `bl stop`.
2. In the first command-line window, enter `q`.

--> 
