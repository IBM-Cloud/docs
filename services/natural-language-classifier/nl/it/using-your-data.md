---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-20"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Utilizzo dei tuoi propri dati
Dopo aver creato, preparato ed eseguito la query di {{site.data.keyword.nlclassifierfull}} con i dati nell'esempio in [Introduzione](/doc/natural-language-classifier/getting-started.html), desidererai creare un classificatore che utilizza i tuoi propri dati. Assembla e fornisci questi dati di formazione.
{:shortdesc}

## Struttura dei dati di formazione
Puoi fornire i dati per preparare {{site.data.keyword.nlclassifiershort}} nel formato separato da virgole (CSV).

Nel formato CSV, una riga nel file rappresenta un record di esempio. Ogni record ha due o più colonne. La prima colonna è il testo rappresentativo da classificare. Le colonne aggiuntive sono classi che si applicano a tale testo. La seguente immagine mostra un file CSV con quattro record. Ogni record in questo esempio include l'input di testo e una classe, che sono separati da una virgola:

![](images/train_sample.png)

Questo esempio è un piccolo esempio. I dati di formazione appropriati includono molti più record.

Scarica il file <a target="_blank" href="https://watson-developer-cloud.github.io/doc-tutorial-downloads/natural-language-classifier/weather_data_train.csv" download="weather_data_train.csv">weather_data_train.csv</a> per visualizzare un file dei dati di formazione di esempio.

### Metadati aggiuntivi

In aggiunta al testo e alle classi, la richiesta, per creare un classificatore, include ulteriori informazioni. I metadati identificano i dati e puoi anche includere un nome per aiutarti nell'identificare il classificatore.

### Formato del file dei dati di formazione

Assicurati che i tuoi dati di formazione CSV rispettino i seguenti requisiti del formato:

- I dati devono essere codificati in UTF-8.
- Separa i valori del testo e ogni valore della classe da un delimitatore virgola. Ogni record (riga) termina con un carattere di fine riga, che è un carattere speciale o una sequenza di caratteri che indica la fine della riga.
- Ogni record deve avere un valore testo e almeno un valore classe.
- I valori della classe non possono includere tasti tab o caratteri di fine riga.
- I valori del testo non possono contenere tasti tab o nuove righe senza una gestione speciale. Per conservare i tasti tab o le nuove righe, eludi il tasto tab con `\t` e le nuove righe con `\r`, `\n` o `\r\n`.

	Ad esempio, `Example text\twith a tab` è valido `Example text    with a tab` non è valido.
- Racchiudi sempre i valori testo o classe tra virgolette nei dati di formazione quando includono i seguenti caratteri:
	- Virgole: `"Example text, with comma"`.
	- Virgolette. In aggiunta, le virgolette devono essere sostituite con doppie virgolette: `"Example text with ""quotation"""`.

## Limitazioni della dimensione.
Esiste sia il limite minimo che massimo dei dati di formazione:

-   I dati di formazione devono avere almeno cinque record (righe) e non più di 15.000 record.
-   La lunghezza totale massima di un valore di testo è di 1024 caratteri.

## Lingue 
Sebbene la lingua predefinita sia l'inglese, puoi specificare la lingua dei dati di formazione quando crei il classificatore. La lingua dei dati di formazione deve corrispondere alla lingua del testo che si intende classificare. Per i dettagli, consulta [API reference ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](http://www.ibm.com/watson/developercloud/natural-language-classifier/api/v1/){:new_window}.

Il classificatore supporta inglese (en), arabo (ar), francese (fr), tedesco (de), giapponese (ja), italiano (it), portoghese brasiliano (pt) e spagnolo (es).

## Linee guida per una corretta preparazione
Le seguenti linee guida non sono applicate dall'API. Tuttavia, il classificatore tende a funzionare meglio quando i dati di formazione le applicano:

- Limita la lunghezza del testo di input a meno di 60 parole.
- Limita il numero di classi a diverse centinaia. Il supporto per un numero maggiore di classi potrebbe venire incluso in versioni successive del servizio.
- Assicurati che ogni classe corrisponda ad almeno 5 - 10 record quando ogni record di testo ha una sola classe. Questo numero fornisce abbastanza preparazione a tale classe.
- Valuta il bisogno di più classi. Due motivi comuni portano più classi:
	- Quando il testo è vago, l'identificazione di una sola classe non è sempre è chiara.
	- Quando gli esperti interpretano il testo in modi differenti, più classi supportano tali interpretazioni.

	Tuttavia, se molti testi nei tuoi dati di formazione includono più classi o se alcuni testi hanno più di tre classi, potresti dover affinare le classi. Ad esempio, controlla se le classi cono gerarchiche. Se sono gerarchiche, includi il nodo foglia come classe.
-  Includi i termini uniti da trattino standard quando fanno parte dei dati di formazione (`back-to-back` o ` part-time job`).

	Tuttavia, non collegare parole adiacenti per creare nuovi termini non presenti nella lingua dei dati di formazione. Ad esempio, invece di definire `dish-ran-away` o `with_the_spoon`, definisci le frasi rilevanti come parole separate (`dish ran away` e `with the spoon`) con la classe appropriata.

## Messa a punto dei dati di formazione
L'apprendimento automatico descrive un processo di apprendimento di alcune proprietà da una serie di dati e le applica ai nuovi dati. Il servizio {{site.data.keyword.nlclassifiershort}} segue questo processo. È preparato per collegare le classi predefinite ai testi di esempio e quindi ad applicare queste classi ai nuovi input.

Per cui, il classificatore preparato è buono soltanto quanto i dati di formazione. Ogni valore di testo nei dati deve rappresentare i tipi di testo che ti aspetti il classificatore preveda. Ogni classe che prevedi sia restituita deve inoltre essere presente nei dati di formazione e le classi associate ad ogni testo devono essere corrette.

Ad esempio, quando i testi nei tuoi dati di formazione sono domande, utilizza le domande rappresentative e tipiche dei tuoi utenti. Potresti raccogliere questi testi dai dati utente attuali o disporre di persone che sono esperte nel tuo campo per creare tali testi.

Questa natura accurata e rappresentativa dei dati è importante perché ti guida attraverso tutti i processi e i risultati del classificatore. In aggiunta, più record includi nei dati di formazione, maggiore è l'opportunità del classificatore di trovare una corrispondenza.
