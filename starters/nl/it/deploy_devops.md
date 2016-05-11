---

 

copyright:

  years: 2015, 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:download: .download}

# Inizia a codificare con Git
*Ultimo aggiornamento: 2 marzo 2016*  

Puoi creare un repository Git ospitato che viene distribuito automaticamente a {{site.data.keyword.Bluemix}}. Puoi poi modificare il codice eseguito nella tua applicazione eseguendo il push
delle modifiche nel repository Git. 
{:shortdesc}

1. Per iniziare, nella pagina Panoramica dell'applicazione, fai clic su **Aggiungi pipeline e repository Git** o, nella modalità classica {{site.data.keyword.Bluemix_notm}}, fai clic su **AGGIUNGI GIT**. 
2. Nella finestra così visualizzata, assicurati che la casella di spunta **Inserisci il pacchetto dell'applicazione starter nel repository e abilita la pipeline Crea e distribuisci** sia selezionata. Il repository Git viene creato. Se il codice di starter è disponibile,
è caricato nel repository. Inoltre, l'applicazione viene distribuita dal servizio Delivery Pipeline in esecuzione in {{site.data.keyword.jazzhub}}.  
3. Per aggiornare la tua applicazione, puoi utilizzare la riga comandi o il Web IDE.  
   **Se utilizzi la riga comandi:**
   a. Clona il tuo repository Git dall'URL Git nella pagina Panoramica dell'applicazione.  
   b. Aggiorna il codice nel tuo editor preferito.  
   c. Esegui il push delle modifiche dall'interfaccia della riga di comando Git.  
	    
   **Se utilizzi il Web IDE:**  
   a. Nella pagina Panoramica dell'applicazione, fai clic su **Modifica codice**. Il tuo progetto viene aperto nel Web IDE.  
   b. Apporta le modifiche necessarie ed esegui il push utilizzando il supporto Git integrato.  
		
L'applicazione aggiornata viene ridistribuita in {{site.data.keyword.Bluemix_notm}}.  

Per istruzioni dettagliate, vedi [Set up Git integration and auto-deploy in DevOps Services](https://hub.jazz.net/tutorials/jazzeditor/#git_integration_and_autodeployment).  

## Hai aggiunto Git? Prova {{site.data.keyword.Bluemix_notm}} Live Sync  

Se stai creando un'applicazione Node.js, puoi utilizzare {{site.data.keyword.Bluemix_notm}} Live Sync per aggiornare rapidamente l'istanza dell'applicazione su {{site.data.keyword.Bluemix_notm}} ed eseguire attività di sviluppo come faresti sul desktop.  

Per ulteriori informazioni su {{site.data.keyword.Bluemix_notm}} Live Sync, vedi [{{site.data.keyword.Bluemix_notm}} Live Sync](../develop/bluemixlive.html). Per ulteriori dettagli sui comandi, vedi la [documentazione della CLI {{site.data.keyword.Bluemix_notm}} Live Sync](../cli/reference/bl/index.html). Per utilizzare {{site.data.keyword.Bluemix_notm}} Live Sync con il Web IDE, vedi [Live Edit](../develop/bluemixlive.html).  

1. Scarica e installa la riga di comando bl di {{site.data.keyword.Bluemix_notm}} Live Sync. 

<p>
<a class="xref" href="http://livesyncdownload.ng.bluemix.net/downloads/blive_setup.msi" target="_blank" title="(Si apre in una nuova scheda o finestra)"><img class="image" src="images/bl_gs_icons_windows_b.svg" alt="Pulsante Scarica la riga di comando bl per Windows" /> </a>
<a class="xref" href="http://livesyncdownload.ng.bluemix.net/downloads/BluemixLive.pkg" target="_blank" title="(Si apre in una nuova scheda o finestra)"><img class="image" src="images/bl_gs_icons_mac-osx_b.svg" alt="Pulsante Scarica la riga di comando bl per Mac" /> </a>
</p>

**Importante:** lo strumento riga di comando bl è disponibile solo per  Windows 7 e 8 e per Mac OS X versione 10.9 o successive. 

2. Su una riga di comando, accedi utilizzando il seguente comando. Ti verranno richiesti il tuo ID e la tua password IBM®. 
```
bl login
```

3. Visualizza l'elenco dei progetti disponibili per la sincronizzazione di {{site.data.keyword.Bluemix_notm}} Live Sync immettendo il seguente comando: 
```
bl projects
```
Trova il nome progetto nell'elenco che corrisponde alla
tua applicazione. Il nome del progetto ha il formato *alias* | *nome applicazione*. 

4. Sincronizza il tuo ambiente locale con il tuo progetto su {{site.data.keyword.Bluemix_notm}} immettendo
il seguente comando. Se sei il proprietario del progetto, devi specificare solo il nome-della-tua-applicazione per nomeProgetto. 
<!--- this command needs italicized parameters projectName localDirectory and yellow on 'local' -->
```
bl sync projectName -d localDirectory --verbose
```
L'esecuzione di questo comando (così come la sincronizzazione) continua finché
non si immette una "q". L'opzione --verbose visualizza informazioni sulla registrazione e sullo stato. Se qualcuno dei tuoi argomenti contiene uno spazio, devi racchiudere il nome tra virgolette. 

5. In un'altra finestra di riga di comando, nella tua directory locale, distribuisci l'applicazione a {{site.data.keyword.Bluemix_notm}} in
modalità Live Edit immettendo il seguente comando:
```
bl start
```  

Quando modifichi i file nella tua directory locale, le modifiche vengono propagate automaticamente sia
all'applicazione che è in esecuzione su {{site.data.keyword.Bluemix_notm}} sia
allo spazio di lavoro cloud del progetto. Se devi riavviare l'applicazione Node, puoi utilizzare
il comando:
```
bl start --restart 
```
