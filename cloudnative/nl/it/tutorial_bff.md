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

# Esercitazione end-to-end dello starter di base BFF 
{: #tutorial}

La seguente esercitazione end-to-end spiega i passi per creare un progetto da uno starter di base BFF, inclusi gli strumenti che devi avere installato e, successivamente, i passi per eseguire il codice del progetto. 

## Installazione degli strumenti per sviluppatori
{: #dev_tools}

Assicurati di aver installato gli [strumenti per sviluppatori prerequisiti ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](get_code.html#prereq-dev-tools){: new_window}.


## Creazione di un progetto utilizzando la {{site.data.keyword.dev_console}}
{: #create-devex}

1. Crea un progetto nella {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}}.

	1. Dalla pagina **Introduzione** nella {{site.data.keyword.dev_console}}, fai clic su **Crea progetto**.

		In alternativa puoi fare clic su **Crea progetto** dalla pagina **Progetti**.

	2. Seleziona **Backend for Frontend** e fai cli su **Avanti**.

	3. Seleziona **Backend di base** e fai clic su **Avanti**.

	4. Immetti il nome del tuo progetto. Per questa esercitazione, utilizza `BFFProject`.   

	5. Immetti un nome host. Per questa esercitazione, utilizza `devhost` 

	6. Seleziona la tua piattaforma di linguaggio. Per questa esercitazione, utilizza `Node`.
   
	7. Fai clic su **Crea**.

2. Facoltativo: aggiungi la funzionalità Data.

	1. Fai clic su **Visualizza** per **Data** nella pagina **Panoramica progetto**.

      In alternativa, puoi fare selezionare **Crea** o **Aggiungi esistente** nella pagina **Funzionalità > Data**.

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

	* Seleziona un modello: 3 (per Backend for Frontend)
	* Seleziona uno starter: 1 (per Backend di base)
	* Seleziona un linguaggio: 1 (per Node)
	* Immetti un nome per il tuo progetto: `BFFProjectCLI`
	* Immetti un nome host per il tuo progetto: `myhost`

4. Se desideri aggiungere servizi al tuo progetto, immetti `y` quando ti viene domandato e rispondi alle rimanenti domande.

5. Quando `BFFProjectCLI` è stato correttamente salvato, passa alla cartella `BFFProjectCLI`.

6. A questo punto potresti aggiungere il tuo proprio codice, creare o eseguire il progetto.
 
	1. Crea il tuo progetto con il seguente comando:
   
		```
		bx dev build
		```     
		{: codeblock}
  
	2. Esegui il tuo progetto con il seguente comando: 

 		```
		bx dev run
		```
		{: codeblock}


## Esecuzione di un progetto BFF
{: #running-bff}

### Localmente
{: #bff-local}

1. Compila il tuo server:

  ```
  swift build
  ```
  {: codeblock}

2. Esegui la tua applicazione. Ad esempio, assumendo che la tua applicazione di chiama `MyServer`:

  ```
  .build/debug/MyServer
  ```
  {: codeblock}

3. Puoi eseguire curl sul tuo server con `curl http://localhost:8080`


### Utilizzo del plugin Bluemix
{: #using-blumix}

1. Esegui la compilazione

	```
	bx dev run
	```
	{: codeblock}

2. Puoi eseguire curl sul tuo server con  
  
	```
	curl http://localhost:8080
	```
	{: codeblock}
