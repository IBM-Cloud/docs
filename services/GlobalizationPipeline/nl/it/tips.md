---

copyright:
  years: 2015, 2017
lastupdated: "2016-07-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Suggerimenti sulla machine translation
{: #globalizationpipeline_tips}


La machine translation può essere valida fornendo un'approssimazione di un significato del testo di origine. Tuttavia, la qualità e l'utilità della machine translation varia significativamente a seconda della lingua di destinazione e dal motore della machine translation che utilizzi. Uno dei fattori chiave nella qualità della machine translation è la qualità dell'origine stessa. Il testo di origine che viene caricato con espressioni colloquiali, frasi incomplete, punteggiatura non corretta e parole o frasi ambigue può non venire tradotte correttamente.
{:shortdesc}

Quando crei la tua IU dell'applicazione {{site.data.keyword.Bluemix_notm}}, segui delle linee base di scrittura per migliorare non solo la lingua di origine ma anche la qualità della machine translation.

In aggiunta, chiedi a dei madrelingua di controllare e modificare la machine translation. Inoltre, raccogli i feedback dai tuoi utenti dell'applicazione; sono probabilmente i migliori giudici dell'utilità e dell'accuratezza della traduzione.

## Suggerimenti sullo stile di scrittura
{: #writingstyletips}

* **Utilizza frasi semplici di media o breve lunghezza (5 - 20 parole):** i motori della machine translation hanno difficoltà a tradurre frasi complesse e composte, incluse frasi con punti e virgole. Comunica un pensiero per frase. Se una frase contiene due verbi attivi che comunicano due pensieri, dividi la frase in due. I motori della machine translation hanno anche problemi nell'analizzare frasi troppo corte per fornire abbastanza contenuto.
* **Frasi da evitare:** Utilizza frasi complete se possibile. Le frasi sono accettabili per i titoli e sottotitoli ma evita di scrivere in modo telegrafico. Utilizza frasi complete per introdurre gli elenchi.
* **Evita idiomi, gerghi e tecnicismi:** sostituisci la frasi per le quali una traduzione letterale non ha senso. Ad esempio, sostituisci "on the fly" con "dynamic," "on the other hand" con "alternatively," e "keep in mind" con "remember."
* **Evita umorismo, sarcasmo, espressioni colloquiali, emoticon e metafore.**
* **Devi essere conciso:** rimuovi ripetizioni e testo non necessari. Ad esempio, sostituisci "It is useful to remember that large values increase the response time" con "Large values increase the response time."
* **Evita frasi scritte completamente in maiuscolo:** il maiuscolo fornisce indizi sul significato della parola. Ad esempio, se scrivi "BILL", il motore della machine translation non può determinare se tu intendi il nome "Bill" o la parola "bill."
* **Evita parole ambigue:** ad esempio, non utilizzare "once" al posto di "after" o "when." Non utilizzare "while" al posto di "although" o "whereas." Non utilizzare "may" quando intendi "might" o "can."
* **Evita pronomi:** ripeti i nomi o i gruppi nominali quando possibile. Il pronome "it" è particolarmente problematico.
* **Scrivi nella voce attiva quando possibile:** le frasi attive sono normalmente più chiare delle frasi passive. Ad esempio, scrivi "The utility determines which path is most efficient" invece di "The most efficient path is determined."
* **Evita informazioni culturali specifiche.**
* **Tieni presente che i motori della machine translation possono tradurre i nomi dei prodotti:** molti paesi lasciano il nome del prodotto inglese originale, ma i motori della machine translation potrebbero tentare di tradurre i nomi dei prodotti, specialmente se i nomi contengono parole reali. Prima di utilizzare un nome del prodotto, verificane la traduzione. Se riscontri dei problemi, modifica il testo o la traduzione di conseguenza.
* **Assicurati che tutte le informazioni siano scritte in una sola lingua:** i motori della machine translation possono assumere che tutte le informazioni siano in una sola lingua, anche se il testo include una o più parole in un'altra lingua. Ad esempio, se il testo include "en route" (francese), il motore della machine translation tenta di tradurre queste parole come se fossero parole in inglese.
* **Evita slogan di marketing:** gli slogan di marketing spesso fanno affidamento sulla comprensione di un pubblico di una cultura in particolare. Evita questi tipi di slogan perché i motori della machine translation possono avere problemi a tradurli correttamente.
* **Assicurati che gli elementi elencati siano completi e simili:** ad esempio, se un elemento inizia con un verbo, assicurati che tutti gli elementi inizino con un verbo.
* **Evita l'utilizzo di prego o grazie:** queste parole possono essere fuori luogo o paternalistiche in alcune culture.
* **Scrivi le date in formato non numerico:** i formati delle date numerici sono diversi a seconda del paese. Scrivi il nome del mese, giorno e anno. Ad esempio utilizza 1 September 2003 invece di 9/01/03, che potrebbe essere interpretato sia come 1 September 2003 che come 9 January 2003.

## Suggerimenti sulla grammatica
{: #grammartips}

* **Utilizza la punteggiatura corretta:** l'omissione di punti e virgole può causare a un motore della machine translation di interpretare male le informazioni.
* **Assicurati che i soggetti concordino con i rispettivi verbi:** assicurati che i soggetti al plurale abbiano i verbi al plurale e i soggetti singoli li abbiano al singolare.
* **Utilizza i verbi con il presente semplice:** molte altre lingue non hanno le qualità dei verbi inglesi, come ad esempio voice e tense. Evita il future e il paste tense se possibile. Ad esempio, puoi riscrivere "If you run this program, DB2® will return an error message" con "If you run this program, DB2 returns an error message."
* **Assicurati che i pronomi concordino con i rispettivi antecedenti:** ad esempio, "A user should first determine their tasks" dovrebbe essere riscritto come "Users should first determine their tasks.".
* **Evita modifiche pendenti:** posiziona le modifiche correttamente in modo che modifichino il nome previsto. Ad esempio, "While typing in commands, the program does not send any messages to you" può essere riscritto come "While typing in commands, you do not receive any messages from the program."
* **Evita le doppie negazioni:** ad esempio, "Do not omit the date" può essere sostituito con "Include the date."
* **Evita le forme verbali dell'infinito (to write), del participio presente (writing) e del participio passato (wrote) all'inizio delle frasi:** queste forme verbali sono spesso ambigue e difficili da tradurre.
* **Evita le stringhe dei nomi:** limita le frasi di nomi composti, come ad esempio "special filter factor estimate considerations," a non più di tre parole.
* **Evita l'utilizzo delle parole in più categorie grammaticali:** in inglese, molte parole, come ad esempio "default," possono essere sia un nome che un verbo. Questa struttura non è corretta in molte altre lingue. Devi essere coerente su come utilizzi ogni parola. Ad esempio, utilizza sempre "default" come un nome.
* **Assicurati che gli elementi di una frase siano simili:** ad esempio, utilizza tutti i nomi o tutti i verbi in un elenco nella frase; non mischiare nomi e verbi.
* **Non omettere le parole necessarie:** ad esempio, invece di "The file names are displayed in uppercase characters and the file extensions in lowercase," utilizza "The file names are displayed in uppercase characters and the file extensions are displayed in lowercase characters." Utilizza la parola "that" per essere chiaro. Ad esempio, sostituisci "If you determine the problem is a missing file" con "If you determine that the problem is a missing file."
* **Non utilizzare un trattino in modo parentetico:** ad esempio, non scrivere "When you get to this point - the point when all data has been loaded - you need to test the system." Sostituisci i trattini con virgole o riscrivi la frase.
 
## Suggerimenti sulla terminologia
{: #terminologytips}

* **Utilizza la terminologia coerentemente:** evita di utilizzare più termini per fare riferimento alla stessa cosa. Evita di utilizzare un solo termine come riferimento a più di una cosa.
* **Includi spiegazioni per ogni termine specialistico.**
* **Evita i termini che hanno significati diversi in altri ambienti e contesti:** questi termini includono "billion," "domestic," e "foreign."
* **Utilizza la formazione della parola, l'unione di parole con un trattino e il maiuscolo in modo standardizzato e coerente:** ad esempio, scrivi "fix pack" invece di "fix pack".
* **Utilizza il minuscolo a meno che il termine non sia un nome proprio.**
* **Evita simboli speciali:** se necessiti di utilizzare il simbolo #, non fare riferimento ad esso come al segno della libbra. Invece, chiamalo il simbolo del numero (#).
* **Evita abbreviazioni:** i motori della machine translation possono riconoscere abbreviazioni comuni, come ad esempio IBM e DB2 ma non riconoscono tutte le abbreviazioni. Evita le abbreviazioni quando possibile. Non utilizzare abbreviazioni latine, come ad esempio "i.e.," e "etc."

## Suggerimenti sulla punteggiatura
{: #punctuationtips}

* **Evita di utilizzare una barra al posto di "and or":** riscrivi la frase per indicare il significato esatto. Ad esempio, puoi riscrivere "You can view the draft copy and/or the review copy" come "You can view the draft copy, the review copy, or both."
* **Non indicare il plurale aggiungendo (s):** utilizza la frase "one or more" o utilizza solo la forma al plurale.
* **Non utilizzare la e commerciale (&) invece della e.**
* **Utilizza le virgole per separare gli elementi in un elenco nella frase e inserisci una virgola prima della congiunzione in un elenco:** ad esempio, "Select your company, location, and profession."

## Suggerimenti sull'ortografia
{: #spellingtips}

* **Controlla l'ortografia:** le parole con un'ortografia sbagliata possono creare errori nella traduzione. Controlla sempre gli errori di battitura!
* **Utilizza l'ortografia coerentemente:** assicurati che i termini, gli acronimi e i nomi propri siano sempre scritti nello stesso modo, incluso l'utilizzo delle lettere minuscole e maiuscole.

## Suggerimenti sulla presentazione visuale
{: #visualtips}

* **Evita il testo nei grafici.**
* **Evita di utilizzare la formattazione con enfasi.**

