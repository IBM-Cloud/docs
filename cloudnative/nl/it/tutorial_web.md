---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Esercitazione end-to-end dello starter di base web 
{: #tutorial}

La seguente esercitazione end-to-end spiega i passi per creare un progetto da uno starter di base web, inclusi gli strumenti che devi avere installato e, successivamente, i passi per eseguire il codice del progetto. 

## Installazione degli strumenti per sviluppatori
{: #dev_tools}

Assicurati di aver installato gli [strumenti per sviluppatori prerequisiti ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](get_code.html#prereq-dev-tools){: new_window}.


## Creazione di un progetto utilizzando la {{site.data.keyword.dev_console}}
{: #create-devex}

1. Crea un progetto nella {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}}.

	1. Dalla pagina **Introduzione** nella {{site.data.keyword.dev_console}}, fai clic su **Crea progetto**.

		In alternativa puoi fare clic su **Crea progetto** dalla pagina **Progetti**.

	2. Seleziona **Applicazione web** e fai clic su **Avanti**. 

	3. Seleziona **Web di base** e fai clic su **Avanti**.

	4. Immetti il nome del tuo progetto. Per questa esercitazione, utilizza `WebBasicProject`.   

	5. Immetti un nome host. Per questa esercitazione, utilizza `devhost` 

	6. Selezionare la tua piattaforma di linguaggio. Per questa esercitazione, utilizza `Swift`.
   
	7. Fai clic su **Crea**.

2. Facoltativo: aggiungi la funzionalità Data.

	1. Fai clic su **Visualizza** per **Data** nella pagina **Panoramica progetto**.

      In alternativa, puoi fare selezionare **Crea** o **Aggiungi esistente** nella pagina **Funzionalità > Dati**.

   2. Immetti il nome del tuo servizio e fai clic su **Crea**.


3. Genera il tuo codice del progetto.

	1. Fai clic su **Richiama codice** nella pagina **Panoramica progetto** per selezionare il tuo linguaggio.
   
		In alternativa puoi fare clic sulla pagina **Codice**.
      
	2. Fai clic su **Genera codice**.
   
	3. Quando il codice del progetto ha terminato la generazione, fai clic su **Scarica codice** per scaricare il tuo archivio del progetto.

4. Facoltativo: [Aggiorna il tuo progetto](project_overview_page.html#update_language) per generare un nuovo linguaggio.


## Creazione di un progetto utilizzando la {{site.data.keyword.dev_cli_notm}}
{: #create-cli}

1. Assicurati di aver installato la [{{site.data.keyword.dev_cli_short}}](dev_cli.html).

2. Nella tua finestra del terminale, passa a una directory locale di tua scelta ed esegui il seguente comando.
  
	```
	bx dev create
	```
	{: codeblock}


3. Fornisci i seguenti valori quando richiesto:

	* Seleziona un modello: 1 (per Web)
	* Seleziona uno starter: 1 (per Web di base)
	* Seleziona un linguaggio: 2 (per Swift)
	* Immetti un nome per il tuo progetto: `WebBasicProjectCLI`
	* Immetti un nome host per il tuo progetto: `myhost`

4. Se desideri aggiungere servizi al tuo progetto, immetti `y` quando ti viene domandato e rispondi alle rimanenti domande.

5. Quando il tuo progetto `WebBasicProjectCLI` è stato correttamente salvato, passa alla cartella `WebBasicProjectCLI`. 

6. Aggiungi il tuo proprio codice, crea o esegui il progetto.
 
	1. Crea il progetto con il seguente comando: 
   
		```
 		bx dev build
 		```     
		{: codeblock}

	2. Esegui il progetto con il seguente comando: 
 
		```
		bx dev run
		```
		{: codeblock}


## Esecuzione di un progetto web
{: #run}

### Localmente
{: #local notoc}

1. Installa le tue dipendenze del nodo:

  ```
  npm install
  ```
  {: codeblock}

2. Integra il tuo codice di frontend in un modulo:

  ```
  node_modules/.bin/gulp
  ```
  {: codeblock}

3. Compila il tuo server:

  ```
  swift build
  ```
  {: codeblock}

4. Esegui la tua applicazione: 

  ```
  .build/debug/WebBasicProjectCLI
  ```
  {: codeblock}

5. Apri il tuo browser in `http://localhost:8080`.


### Utilizzo della {{site.data.keyword.dev_cli_short}}
{: #dev notoc}

1. Installa le dipendenze del nodo:

  ```
  npm install
  ```
  {: codeblock}

2. Integra il tuo codice di frontend in un modulo:

  ```
  gulp
  ```
  {: codeblock}

3. Esegui la compilazione:

  ```
  bx dev run
  ```
  {: codeblock}

4. Apri il tuo browser in `http://localhost:8080`.


## Esecuzione del tuo progetto in Xcode
{: #Xcode}

1. Crea un progetto Xcode. 

	Prima di poter sviluppare in Xcode, devi utilizzare il gestore del pacchetto Swift per creare un progetto Xcode.
	
	```
	swift project generate-xcodeproj
	```
	{: codeblock}

2. Modifica la tua destinazione attiva con l'eseguibile:

	Successivamente, apri il tuo progetto in Xcode e assicurati che la tua destinazione attiva sia l'eseguibile. Puoi tenere premuto il tasto dell'opzione mentre fai clic sul menu a discesa per selezionare l'eseguibile attivo desiderato.

3. Premi **run**.

4. Apri il tuo browser in `http://localhost:8080`.

