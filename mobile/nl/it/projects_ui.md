---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Utilizzo di uno starter IU per creare un progetto
{: #projects_ui}

Puoi utilizzare uno [Starter IU](starters.html#UI_Starter) nel dashboard {{site.data.keyword.Bluemix}} Mobile per creare un progetto nell'ambiente {{site.data.keyword.Bluemix_notm}}. Questa procedura non si applica ai progetti che utilizzano gli starter codice. Consulta [Creazione di un progetto con uno starter codice](projects_code.html) per istruzioni sugli starter codice.
{:shortdesc}

Completa i seguenti passi per creare un progetto con uno starter IU:

1. Crea un nuovo progetto dashboard Mobile in {{site.data.keyword.Bluemix_notm}}.

 Inizia con la scheda *Introduzione* dopo aver selezionato il catalogo Mobile. Esistono le descrizioni degli starter selezionati che puoi utilizzare e diversi modi per creare un progetto in base a quanta assistenza ti serve. Se desideri iniziare con un aiuto minimo, seleziona **Crea progetto**.

 Se già disponi di progetti, puoi seleziona la scheda *Progetti* mentre sei nella scheda *Introduzione*. Dal dashboard {{site.data.keyword.Bluemix_notm}} Mobile, vista **Progetti**, puoi selezionare un progetto con cui lavorare, utilizza le *Azioni* di un progetto per eliminarlo o per scaricarne il codice o crea un nuovo progetto. Se il progetto è stato iniziato con uno starter IU, puoi anche aprire il progetto nel builder IU direttamente dal menu *Azioni*. 

	1. Nella console {{site.data.keyword.Bluemix_notm}}, seleziona **Mobile** dopo aver espanso il menu con le tre righe affianco al logo {{site.data.keyword.Bluemix_notm}}. 
	
	2. Seleziona **Crea progetto**. 

	  In alternativa puoi selezionare la scheda **Progetti** per visualizzare i progetti che sono già presenti nel tuo ambiente mobile e creare un nuovo progetto facendo clic su **Crea progetto**. 

	3. Seleziona lo starter che meglio corrisponde al tipo di applicazione che desideri creare e seleziona **Crea progetto**. Esistono **Starter IU** e **Starter codice**. Consulta [Starter](starters.html) per ulteriori informazioni sugli starter e su come utilizzarli. 
	
	4. Immetti un nome per il tuo progetto e seleziona **Crea**.
	
2. Effettua le tue selezioni nella schermata **Panoramica progetto**.  La schermata **Panoramica progetto** visualizza le informazioni sul tuo progetto e sulle funzionalità facoltative che puoi aggiungere al tuo progetto come {{site.data.keyword.mobilepushshort}}.  

	1. Facoltativo: seleziona **Aggiungi** per aggiungere una delle funzionalità elencate al tuo progetto. Modifica il **Nome servizio** per il tuo servizio e fai clic su **Crea**. Quando aggiungi i servizi al tuo progetto, ti colleghi alla pagina {{site.data.keyword.Bluemix_notm}} per tale servizio. Configura il servizio fornendo le informazioni obbligatorie per esso.
	
	2. Facoltativo: ripeti il passo *a* per ogni ulteriore funzionalità che desideri aggiungere al tuo progetto. 

3. Progetta la tua interfaccia utente utilizzando il builder IU.

   **Nota:** poiché gli starter codice non dispongono di un'interfaccia utente personalizzabile, la scheda *Progettazione* non è disponibile.

    1. Seleziona **Builder IU** nel menu di navigazione per personalizzare la progettazione della tua applicazione. 
	
		**Suggerimento:** per visualizzare una veloce panoramica del builder IU, seleziona **Mostrami come funziona** nella navigazione dopo aver selezionato il builder IU. 
	
	2. Personalizza il tuo layout dell'applicazione dalla scheda **Schermate**.
	
	3. Aggiungi nuove schermate selezionando **Crea schermata**. Denomina una nuova schermata per rendere più facile il riferimento alla tua applicazione. Puoi scegliere tra i seguenti tipi di schermata: 
		* Menu
		* Elenco
		* Associazione
		* Personalizzata 
		* Grafico
		
	4. Puoi modificare il titolo del menu della tua applicazione selezionando la casella di testo *Menu* nella sezione **Layout** della tua interfaccia e sostituendo il contenuto nel campo **Dati da visualizzare**. Visualizza i tuoi aggiornamenti nella sezione del dispositivo simulato.
	
		Aggiorna gli elementi di progettazione selezionando ognuno di essi e aggiornando le informazioni, se necessario. Questi elementi vengono visualizzati in un formato ad albero. Puoi modificare l'ordine o l'ubicazione degli elementi del menu trascinando un elemento in una nuova ubicazione. Tutti gli elementi secondari di un elemento vengono invece spostati con l'elemento principale. Le informazioni testuali nei tre elementi visualizzate nei campi **Dati da visualizzare** fanno riferimento al contenuto nel foglio di calcolo dell'origine dati. *Non modificare questi elementi nella vista **Progettazione** perché vengono sovrascritti dal contenuto nelle origini dati identificate nella vista **Dati**.* 
		
		Un elemento che viene identificato nell'albero come un *Modulo* è indipendente e può essere modificato inline. Non dispone di informazioni di riferimento da un'origine dati.
	
	5. Seleziona **Dati** nella navigazione per visualizzare i dati che vengono utilizzati dall'applicazione. Nel template sono disponibili informazioni predefinite; tuttavia, puoi modificare l'origine dei dati selezionando **Crea nuovo**. Puoi fare riferimento a più di una origine dati, in modo da fornire un nome per ogni origine che vuoi utilizzare. Puoi anche selezionarla dalla seguenti opzioni di origine dati
		* Cloud
		* Locale
		* Cloudant
		* Google Sheet
		* Excel Online
		* Google Drive
	
		Puoi anche importare, esportare o modificare il contenuto presente nella tabella, se in locale, utilizzando i pulsanti e selezionando il contenuto nella tabella.
	     
		**Nota:** se importi dati che non corrispondono alla struttura dei dati predefiniti, attiva lo slider *Sostituisci schema*. Un esempio di questo è un file .csv con meno colonne rispetto ai dati forniti con il tuo starter.
		 
	6. Seleziona **Navigazione** per personalizzare le azioni di navigazione nella tua applicazione. Questa opzione è facoltativa perché per molte schermate le azioni di navigazione vengono create automaticamente in base alle relazioni delle schermate. Puoi modificare la schermata di destinazione selezionando la schermata o il campo *da* cui vuoi navigare nell'elenco delle voci di menu. Seleziona quindi la schermata *verso* cui vuoi navigare nel campo della schermata di destinazione.  
		 
	7. Seleziona **Accesso utente** nella navigazione per modificare i requisiti di accesso al tuo progetto. Puoi attivare/disattivare l'accesso utente con lo switch. Quando l'accesso utente è attivo, puoi impostare il timeout utente di inattività e le credenziali degli utenti che possono accedere all'applicazione.
	
	8. Seleziona **Impostazioni** nel menu di navigazione per modificare le informazioni generali e i colori per il tuo progetto. Questa schermata è dove immetti la chiave API Google, se necessaria per le funzionalità che hai aggiunto al tuo progetto. Questa schermata è inoltre dove aggiungi il tuo identificativo bundle univoco registrato con l'Apple Store o il Google Play Store.
	
		Se desideri aggiungere l'SDK IBM MobileFirst Foundation al tuo progetto, attiva lo switch.
		
	9. Se hai attivato lo switch per aggiungere IBM MobileFirst Platform Foundation al tuo progetto nella schermata *Impostazioni*, viene visualizzata una selezione **Foundation** nella navigazione. Seleziona **Foundation** e completa le informazioni necessarie specifiche per IBM MobileFirst Platform Foundation.
	
	10. Seleziona **Pubblica** nel menu di navigazione per immettere le informazioni finali per creare la tua applicazione mobile. Puoi immettere il tuo identificativo Bundle per iOS e l'identificativo Applicazione per Android.
	
		Se stai creando un'applicazione iOS, devi ottenere il tuo identificativo bundle, il tuo certificato di distribuzione come ad esempio un file `.p12` e il tuo profilo di provisioning come un file `.mobileprovision` dal portale di provisioning di Apple. Possono essere creati contemporaneamente e con lo stesso computer che utilizzerai quando invierai la tua applicazione all'Apple store. Il certificato di distribuzione e il profilo di provisioning devono basarsi sull'identificativo bundle. 	
4. Torna alla schermata *Panoramica progetto* per richiamare il codice per la tua applicazione e provalo! Puoi scaricare il codice direttamente per i sistemi operativi iOS o Android o scansionando un codice QR per il sistema operativo Android. 


