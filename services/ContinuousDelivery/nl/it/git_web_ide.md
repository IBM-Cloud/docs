---

copyright:
  years: 2017
lastupdated: "2017-5-8"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Utilizzo di Git in Eclipse Orion Web IDE
{: #git_web_ide}

Quando utilizzi Eclipse Orion {{site.data.keyword.webide}}, non hai bisogno del terminale Git: puoi eseguire molti comandi comuni Git nel Web IDE.

Indipendentemente da dove esegui la codifica, puoi utilizzare questo riferimento rapido per svolgere attività comuni.

## Crea un ramo locale
{: #create_branch}

### Eclipse Orion Web IDE
1. Fai clic sull'elenco **Reference**.

1. Fai clic su **New Branch**.

2. Immetti il nome del ramo e fai clic su **Submit**.

### Terminale Git
1. Immetti `git branch <branchname>` e premi Invio.

## Lavora su un ramo locale
{: #start_working_on_branch}

### Eclipse Orion Web IDE
1. Fai clic sull'elenco **Reference** ed espandi **local**.

2. Accanto al ramo da modificare, fai clic sull'icona Checkout <img  class="inline" src="./images/checkout.png" alt="icona Checkout">.

1. Assicurati che il tuo ramo selezionato sia visualizzato nell'elenco **Reference**.

### Terminale Git
1. Per visualizzare i tuoi rami locali, immetti `git branch -l` e premi Invio.

2. Immetti `git checkout <branchname>` e premi Invio.


## Aggiorna un ramo locale per includere le modifiche dal ramo remoto
{: #update_branch}

### Eclipse Orion Web IDE
1. Fai clic su **Sync**.

1. Se rilevi dei conflitti, [risolvili](#resolve_a_rebase_conflict).

### Terminale Git
1. Immetti `git pull` e premi Invio.

## Elimina un ramo locale
{: #delete_branch}

### Eclipse Orion Web IDE
1. Assicurati che il ramo da eliminare non sia stato estratto. Se tale ramo è stato estratto, [estrai un altro ramo](#start_working_on_branch).

1. Fai clic sull'elenco **Reference** ed espandi **local**.

2. Accanto al ramo locale da rimuovere, fai clic su **Delete** <img class="inline"  src="./images/delete.png" alt="icona Delete">.

### Terminale Git
1. Immetti `git branch -d <branchname>` e premi Invio.

##Forza il push delle modifiche locali a un ramo remoto
{: #force_push}

Sovrascrivi il contenuto di un ramo remoto di riferimento con il contenuto del tuo ramo locale attivo.

**Importante:** quando forzi il push di un ramo locale a uno remoto, potresti perdere i commit sul ramo remoto.

### Eclipse Orion Web IDE

1. Nella sezione Working Directory Changes, nella sezione Outgoing, fai clic sulla freccia accanto a **Push**.
2. Fai clic su **Force Push Branch**.
3. Conferma l'avvertenza.

### Terminale Git

1. Immetti `git push <origin> <remote branch> -f` e premi Invio.

## Scarta le modifiche non preparate dal ramo locale attivo
{: #discard_changes}

### Eclipse Orion Web IDE
1. Nella sezione Working Directory Changes, seleziona la casella di spunta per ogni file modificato che contiene le modifiche che vuoi scartare.
2. Fai clic sull'icona Checkout <img class="inline"  src="./images/discard.png" alt="Estrai i file selezionati, scartando tutte le modifiche">.

### Terminale Git
1. Immetti `git checkout -- path/to/file/filename` per scartare le modifiche in un file.

## Esegui il commit dei file ed effettua il push nel ramo remoto
{: #commit}

### Eclipse Orion Web IDE
1. Nella sezione Working Directory Changes, seleziona la casella di spunta per ogni file di cui eseguire il commit.

3. Nel campo **Enter the commit message**, immetti un messaggio che descriva le tue modifiche.

  **Suggerimento**: fornisci un messaggio di commit dettagliato. Il tuo messaggio deve fornire dettagli sufficienti per capire perché la modifica è stata necessaria, senza ulteriori informazioni. Come ausilio, puoi includere un link a un elemento nel programma di traccia del problema del tuo team. La prima riga del messaggio di commit deve contenere meno di 50 caratteri. Aggiungi una riga vuota prima di aggiungere altro testo.

4. Fai clic su **Commit**.

5. Fai clic su **Push**.

### Terminale Git
1. Immetti `git status` e premi Invio.

2. Rivedi le modifiche di cui eseguire il commit. Se tutti i tuoi file sono elencati per l'esecuzione del commit, procedi. Per eseguire il commit di file non preparati, devi prima prepararli.

3. Immetti `git commit` e premi Invio.

4. Immetti il riepilogo del commit, aggiungi una riga vuota e quindi aggiungi la descrizione del commit.

  **Suggerimento**: il riepilogo del commit deve contenere meno di 50 caratteri. La descrizione del commit deve fornire dettagli sufficienti per capire perché la modifica è stata necessaria, senza ulteriori informazioni. Come ausilio, puoi includere un link a un elemento nel programma di traccia del problema del tuo team.

5. Salva il messaggio di commit.

  **Nota:** per salvare il messaggio di commit e chiudere Vim, che potrebbe essere il tuo editor di testo predefinito, premi Esc, digita `:wq` e premi Invio.

4. Immetti `git push` e premi Invio.

## Visualizza la cronologia di commit
{: #view_commit_history}

### Eclipse Orion Web IDE
1. Nella sezione Active Branch, espandi **History** per visualizzare la cronologia di commit per tale ramo.

  La cronologia di commit può essere visualizzata anche come grafico visivo collegato.

1. Fai clic sull'icona dell'**attivazione della rappresentazione grafica** <img  class="inline" src="./images/graphicalhistoryicon.png" alt="icona cronologia grafica">.

  Una volta attivata, la cronologia di commit e le eventuali modifiche in entrata o in uscita per il ramo attivo vengono disegnate come un grafico collegato.  La rappresentazione visiva mostra tutti i commit e i rami su cui sono stati effettuati.

  <img class="screen-shot" src="./images/visualhistoryexample.png" alt="Cronologia commit visiva">

### Terminale Git
1. Immetti `git log` e premi Invio.

2. Esplora i commit del committer.
 * Per visualizzare più elementi, premi Pagina giù.
 * Per visualizzare gli elementi precedenti, premi Pagina su.

3. Per interrompere la visualizzazione degli elementi, premi Q.

## Confronta le modifiche introdotte da un commit
{: #compare_changes}

### Eclipse Orion Web IDE
1. Visualizza la tua cronologia di commit e individua il commit. Per ulteriori informazioni, vedi [ Visualizza la cronologia di commit](#view_commit_history).

2. Visualizza i dettagli del commit facendo clic su di esso.

3. Accanto a un file, fai clic su **>** e rivedi le modifiche del file.

  **Nota:** se un commit ha introdotto una modifica a una riga, la riga originale ha un'ombreggiatura rosa e la nuova riga ha un'ombreggiatura verde.  Allo stesso modo, le righe aggiunte da un commit hanno un'ombreggiatura verde e quelle rimosse da un commit hanno un'ombreggiatura rosa.

### Terminale Git
1. Immetti `git log -p` e premi Invio.

  **Nota:** per visualizzare solo un certo numero di commit, immetti `git log -p -<number_of_commits_to_view>`.

2. Esplora i commit.
 * Per visualizzare più elementi, premi Pagina giù.
 * Per visualizzare gli elementi precedenti, premi Pagina su.

3. Rivedi le modifiche.

  **Nota:** se un commit ha introdotto una modifica a una riga, la riga originale è scritta in rosso e inizia con un segno meno (-). La nuova riga è in verde e inizia con un segno più (+).  Allo stesso modo, le righe aggiunte da un commit sono in verde e iniziano con un segno +. Le righe che sono state rimosse da un commit sono in rosso e iniziano con un segno -.

1. Per interrompere la visualizzazione degli elementi, premi Q.

## Modifica l'ultimo commit
{: #modify_last_commit}

  **Nota:** quando modifichi l'ultimo commit dopo averne eseguito il push a un repository remoto, sovrascrivi la cronologia di commit. Ciò potrebbe causare errori di commit e altri problemi per gli altri contributori del progetto. Assicurati di sapere cosa stai facendo prima di modificare un commit che hai distribuito tramite push a un repository remoto.

### Eclipse Orion Web IDE
1. Seleziona le caselle di spunta per gli elementi da aggiungere al commit.

1. Seleziona la casella di spunta **Amend previous commit**.

2. Se necessario, immetti un nuovo messaggio di commit.

3. Fai clic su **Commit**.

### Terminale Git
1. Controlla il tuo stato. Secondo necessità, prepara o annulla la preparazione dei file.

2. Immetti `git commit --amend` e premi Invio.

3. Nel tuo editor di testo, accetta o modifica il messaggio di commit.

  **Nota:** per salvare il messaggio di commit e chiudere Vim, che potrebbe essere il tuo editor di testo predefinito, premi Esc, digita `:wq` e premi Invio.

## Aggiungi una tag per un commit
{: #tag_commit}

### Eclipse Orion Web IDE
1. Visualizza la tua cronologia di commit e individua il commit. Per ulteriori informazioni, vedi [ Visualizza la cronologia di commit](#view_commit_history).

2. Visualizza i dettagli del commit facendo clic su di esso.

2. Nel riquadro del commit, fai clic su **Create a tag for the commit** <img class="inline"  src="./images/tag.png" alt="Create a tag for the commit">.

3. Nel campo del nome, immetti il testo della tag. Fai clic su **Submit**.

### Terminale Git
1. Visualizza la cronologia di commit e ottieni l'ID del commit a cui aggiungere la tag. Per ulteriori informazioni, vedi [ Visualizza la cronologia di commit](#view_commit_history).

2. Immetti `git tag -a <tag_text> <commit_id>` e premi Invio.

## Modifica il nome e l'indirizzo e-mail del committer
{: #change_the_committer_name_and_email_address}

### Eclipse Orion Web IDE
1. Fai clic sull'icona di configurazione <img class="inline" src="./images/configurations.png" alt="icona di configurazione">.

3. Modifica l'indirizzo e-mail e il nome dell'utente aggiornando i valori user.email e user.name. Fai clic su **Submit** per salvare le modifiche.

### Terminale Git
Per aggiornare il tuo nome e indirizzo e-mail per un singolo repository:

1. Immetti `git config user.email "<your@email.com>"` e premi Invio.

2. Immetti `git config user.name "<Your Name>"` e premi Invio.

Per aggiornare il tuo nome e indirizzo e-mail per tutti i repository:

1. Immetti `git config --global user.email "<your@email.com>"` e premi Invio.

2. Immetti `git config --global user.name "<Your Name>"` e premi Invio.

##Ripristina un commit
{: #revert}

Ripristina le modifiche introdotte da un commit nel tuo ramo attivo.

### Eclipse Orion Web IDE

1. In History, seleziona un commit.

2. Sul lato destro della pagina, sopra il riepilogo del commit, fai clic sull'icona di ripristino <img class="inline" src="./images/revert.png" alt="icona di ripristino">.

### Terminale Git

1. Immetti `git revert <commit ID>` e premi Invio.

## Unisci le modifiche
{: #merge_changes}

Quando hai bisogno di trasmettere le modifiche da un ramo di origine a un ramo di destinazione, devi prima eseguire l'unione. In genere, il ramo di origine è il ramo in cui hai apportato le modifiche e il ramo di destinazione è il tuo ramo master.

### Eclipse Orion Web IDE
1. Decidi quali rami unire.

2. Estrai il ramo di destinazione. Per ulteriori informazioni, vedi [ Lavora su un ramo locale](#start_working_on_branch).

 <img class="screen-shot" src="./images/destinationbranch.png" alt="Estrai il ramo di destinazione">

1. Fai clic sull'elenco **Reference**, espandi **local**, quindi fai clic sul nome del ramo di origine. Le modifiche provenienti dal ramo di origine vengono mostrate nella sezione Incoming.

  <img class="screen-shot" src="./images/sourcebranch.png" alt="Modifiche dal ramo di origine mostrate nella sezione Incoming">

1. Nella sezione Incoming, fai clic sull'icona **Merge** <img  class="inline" src="./images/mergeicon.png" alt="icona Merge nella sezione Incoming">

1. Nell'elenco **Reference**, fai clic sull'icona di estrazione accanto al ramo in cui hai appena unito le modifiche.

1. Se vuoi trasmettere le modifiche, fai clic su **Push**. Altrimenti, a questo punto, puoi creare una distribuzione di prova per assicurarti che tutto funzioni come previsto.

### Terminale Git
1. Decidi quali rami unire.

2. Estrai il ramo di destinazione. Per ulteriori informazioni, vedi [ Lavora su un ramo locale](#start_working_on_branch).

3. Immetti `git merge <source_name>` e premi Invio.


## Risolvi un conflitto di unione
{: #resolve_a_merge_conflict}

### Eclipse Orion Web IDE
1. Nel riquadro Changed Files, rivedi l'elenco dei file che contengono conflitti.

2. Nel Web IDE, apri ogni file che contiene conflitti.

3. Risolvi tutte le modifiche in conflitto.

  **Nota:** elimina tutto il testo che non vuoi mantenere. Ogni conflitto è nel seguente formato:

		<<<<<<< HEAD
		Testo nel ramo estratto.
		=======
		Testo nel ramo unito.
		>>>>>>> commit_ID_from_merged_branch
4. Per ogni file in conflitto, seleziona la casella di spunta. Immetti un messaggio di commit di unione e fai clic su **Commit**.

### Terminale Git
1. Per i file contengono conflitti, rivedi i nomi nel messaggio Git.

2. In un editor di testo, apri un file che contiene conflitti.

3. Risolvi tutte le modifiche in conflitto e quindi salva il file.

  **Nota:** elimina tutto il testo che non vuoi mantenere. Ogni conflitto è nel seguente formato:

		<<<<<<< HEAD
		Testo nel ramo estratto.
		=======
		Testo nel ramo unito.
		>>>>>>> merged_branch
4. Prepara ogni file che hai modificato, quindi esegui il commit dell'unione.

## Riassegna i rami
{: #rebase_branches}

### Eclipse Orion Web IDE
1. Decidi quali rami riassegnare. Il contenuto del ramo di origine viene riassegnato nel ramo di destinazione.

2. Estrai il ramo di destinazione. Per ulteriori informazioni, vedi [ Lavora su un ramo locale](#start_working_on_branch).

1. Fai clic sull'elenco **Reference**.

1. Fai clic sul nome del ramo di origine.

1. Nella sezione Incoming, fai clic sull'icona Rebase <img  class="inline" src="./images/rebase.png" alt="icona Rebase">.

5. Se rilevi dei conflitti, [risolvili](#resolve_a_rebase_conflict).

6. Ripeti il passo precedente il numero di volte necessario per completare l'operazione di riassegnazione.

1. Fai clic sull'elenco **Reference**, espandi **origin**, quindi fai clic sul nome del ramo di origine.

1. Fai clic su **Push**.

### Terminale Git
1. Estrai il ramo da aggiornare immettendo `git checkout <destination_branchname>` e premendo Invio.

2. Immetti `git rebase <source_branchname>` e premi Invio.

3. Se rilevi dei conflitti, [risolvili](#resolve_a_rebase_conflict).

5. Ripeti il passo precedente il numero di volte necessario per completare l'operazione di riassegnazione.

  **Nota:** per interrompere l'operazione di riassegnazione, immetti `git rebase --abort` e premi Invio.

## Risolvi un conflitto di riassegnazione
{: #resolve_a_rebase_conflict}

### Eclipse Orion Web IDE
1. Nella sezione Working Directory Changes, rivedi l'elenco dei file in conflitto.

2. Nel Web IDE, apri ogni file che contiene conflitti.

3. Risolvi tutte le modifiche in conflitto.

  **Nota:** elimina tutto il testo che non vuoi conservare. Ogni conflitto è nel seguente formato:

		<<<<<<< HEAD
		Testo nel ramo estratto.
		=======
		Testo nel ramo unito.
		>>>>>>> commit_ID_from_merged_branch
4. Nel riquadro Rebase, seleziona la casella di spunta per ogni file corretto e fai clic su **Continue**.

### Terminale Git
1. Per i file contengono conflitti, rivedi i nomi nel messaggio Git.

2. In un editor di testo, apri un file che contiene conflitti.

3. Risolvi tutte le modifiche in conflitto e quindi salva il file.

  **Nota:** elimina tutto il testo che non vuoi conservare. Ogni conflitto è nel seguente formato:

		<<<<<<< HEAD
		Testo nel ramo estratto.
		=======
		Testo nel ramo unito.
		>>>>>>> merged_branch
4. Prepara ogni file che hai modificato.

5. Riprendi l'operazione di riassegnazione immettendo `git rebase --continue` e premendo Invio.
