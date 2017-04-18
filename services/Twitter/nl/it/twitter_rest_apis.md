---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Utilizzo delle API REST di Insights for Twitter
{: #rest_apis}

Il servizio {{site.data.keyword.twittershort}} è costituito da API REST per cercare e utilizzare il contenuto di Twitter. La tabella [Linguaggio di query](twitter_rest_apis.html#querylanguage){: new.window} elenca i termini di query che sono supportati dalle API di servizio. Vengono forniti degli esempi per dimostrare come possono essere create le query.
{:shortdesc}

## Documentazione API REST {: #rest_api}
La documentazione API REST viene creata utilizzando Swagger, che ti permette di verificare le operazioni API e visualizzare istantaneamente i risultati per aiutarti nella creazione delle tue applicazioni più velocemente.
Sono correntemente disponibili le seguenti operazioni API:

* Ricerca: trova Tweet nel flusso Decahose o nel flusso PowerTrack filtrato.
* Conteggio: restituisce il numero di Tweet in base alla query specificata.
* Controllo: determina se un elenco di messaggi è conforme agli utenti e alle politiche di Twitter.
* Traccia: fornisce agli utenti del piano di ingresso un assortimento di endpoint per gestire i filtri PowerTrack.

Per ulteriori informazioni sulle API REST supportate e le relative risorse, consulta la guida di riferimento [API REST](https://cdeservice.{APPDomain}/rest-api/){: new_window}. Seleziona la regione della tua applicazione. Ogni regione è indipendente; non puoi utilizzare le credenziali del servizio che ti sono state fornite in una regione per l'autenticazione con un servizio in un'altra regione.

Dalla documentazione di riferimento, fai clic su **Elenco operazioni** per visualizzare i dettagli per ogni operazione. Dopo aver fatto clic sul pulsante **Provalo**, potrebbe venirti richiesto di fornire le credenziali. Devi fornire il nome utente e la password dalle tue variabili di ambiente **VCAP_SERVICES**. Puoi trovare queste informazioni aprendo la tua applicazione e facendo clic su **Variabili di ambiente** dalla tabella dei contenuti.

**Nota**: la mancata immissione delle credenziali corrette comporterà il ricevimento di un messaggio "Non autorizzato" nel corpo della risposta.

**Importante**: le tracce attive create utilizzando la funzione **Provalo** raccolgono Tweet da Twitter, che vengono conteggiati nella tua franchigia mensile. Quando le tracce non sono più necessarie, modifica il loro stato in **Inattivo** o semplicemente elimina la traccia.


## Linguaggio di query {: #querylanguage}

Con {{site.data.keyword.twittershort}}, puoi ricercare del contenuto di Twitter utilizzando un'ampia gamma di parametri di query e filtri per produrre risultati più accurati.

Sono supportati i seguenti operatori booleani nelle tue query: 

| **Operatore**        | **Descrizione**                                                                                                                   | **Esempi**      |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------|-------------------|
| term1 **AND** term2 | Restituisce Tweet che contengono sia il term1 che il term2. Lo spazio vuoto tra due termini viene trattato come un AND, in questo modo l'operatore può ometterlo. | `#ibm twitter`      |
| term1 **OR** term2  | Restituisce Tweet che contengono il term1 o il term2.    | `#money OR revenue` |
| -term1              | Restituisce Tweet che non contengono il term1.  |`ibm -apple`  |

*Tabella 1. Operatori booleani*

Precedenza tra gli operatori: "-" ha la precedenza su "AND" e "AND" su "OR". Dovresti utilizzare le parentesi per rendere la precedenza tra gli operatori esplicita. Ad esempio, `large animals` -(`giraffes` OR `bears`) ricerca i Tweet che contengono i termini "large" e "animals" ma esclude i Tweet che contengono "giraffes" e "bears".

La seguente tabella elenca i termini di query al momento supportati.

| **Termine** 	| **Descrizione** 	| **Esempi** 	|
|----------------------------------------------	|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|---------------------------------------------	|
| keyword 	| Trova i Tweet con la parola chiave "keyword" nel loro corpo. La ricerca è sensibile al maiuscolo/minuscolo. 	| analytics 	|
| "exact phrase match" 	| Trova i Tweet che contengono la sequenza esatta della parola chiave. 	| "IBM and analytics" 	|
| `#hashtag` 	| Trova i Tweet con la hashtag *#hashtag*. 	| `#insight2015` 	|
| `bio_lang:language` 	| Trova i Tweet dagli utenti le cui impostazioni della lingua del profilo corrispondono al codice del linguaggio specificato.  Consulta `lang:` per un elenco delle lingue supportate. 	| `bio_lang:en` 	|
| `bio_location:"location"` 	| Trova i Tweet dagli utenti le cui impostazioni dell'ubicazione del profilo contengono il riferimento `location` specificato. 	| `bio_location:"New York"` 	|
| `country_code:country-code` 	| Trova i Tweet contrassegnati da tag o la cui ubicazione corrisponde al codice paese specificato. </br>**Per un elenco dei codici paese supportati, consulta **: http://en.wikipedia.org/wiki/ISO_3166-1 	| `country_code:us` 	|
| `followers_count: lowerLimit,upperLimit` 	| Trova i Tweet dagli utenti con un numero di follower che rientra nell'intervallo specificato. Il limite superiore (upperLimit) è facoltativo ed entrambi i limiti sono inclusivi. 	| `followers_count:500` 	|
| `friends_count: lowerLimit,upperLimit` 	| Trova i Tweet dagli utenti che seguono un numero di utenti che rientrano nell'intervallo specificato. Il limite superiore (upperLimit) è facoltativo ed entrambi i limiti sono inclusivi. 	| `friends_count:1000,3000` 	|
| `from:twitterHandle` 	| Trova i Tweet dagli utenti con il nome utente preferito *twitterHandle*. Non deve contenere il simbolo &commat;. 	| `from:alexlang11` 	|
| `has:children` 	| Trova i Tweet dagli utenti che hanno figli. 	| `has:children` 	|
| `is:married` 	| Trova i Tweet dagli utenti che sono sposati. 	| `is:married` 	|
| `is:verified` 	| Trova i Tweet in cui l'autore è stato verificato da Twitter. 	| `analytics is:verified` 	|
| `lang:language-code` 	| Trova i Tweet da una lingua in particolare. L'elenco dei codici lingua supportati è: <ul><li>`ar` (Arabo)</li><li>`zh` (Cinese)</li><li>`da` (Danese)</li><li>`dl` (Olandese)</li><li>`en` (Inglese)</li><li>`fi` (Finlandese)</li><li>`fr` (Francese)</li><li>`de` (Tedesco)</li><li>`el` (Greco)</li><li>`he` (Ebraico)</li><li>`id` (Indonesiano)</li><li>`it` (Italiano)</li><li>`ja` (Giapponese)</li><li>`ko` (Coreano)</li><li>`no` (Norvegese)</li><li>`fa` (Persiano)</li><li>`pl` (Polacco)</li><li>`pt` (Portoghese)</li><li>`ru` (Russo)</li><li>`es` (Spagnolo)</li><li>`sv` (Svedese)</li><li>`th` (Tailandese)</li><li>`tr` (Turco)</li><li>`uk` (Ucraino)</li></ul>    | `lang:de` (per la corrispondenza con i Tweet in tedesco) 	|
| `listed_count: lowerLimit,upperLimit` 	| Trova i Tweet per cui l'elenco degli autori di Twitter rientra nell'intervallo specificato. Il limite superiore (upperLimit) è facoltativo ed entrambi i limiti sono inclusivi. 	| `listed_count:1000,3000` 	|
| `point_radius:[longitude latitude radius]` 	| Trova i Tweet con una regione geografica, specificata dalle relative coordinate di latitudine e longitudine e un raggio. </br></br>Tutte le coordinate sono rappresentate in gradi decimali. La `longitude` deve essere un valore compreso tra -180 e +180, mentre la `latitude` deve essere un valore compreso tra -90 e +90. Lo specificare un valore al di fuori degli intervalli supportati restituisce un errore. I valori devono essere immessi come numeri con virgola mobile; i numeri interi non sono supportati. </br></br>Il raggio della zona circostante deve essere specificato in miglia (mi) o chilometri (km). 	| `point_radius:[41.128611 -73.707778 5.0mi]` 	|
| `posted:startTime  posted:startTime,endTime` 	| Trova i Tweet che sono stati immessi nello o dopo lo "startTime". Il "endTime" è facoltativo ed entrambi i limiti sono inclusivi. Le date/ore devono essere in uno dei seguenti formati:  </br>"yyyy-mm-dd" o "yyyy-mm-ddTHH:MM:SSZ" </br>  Il fuso orario in UTC (Coordinated Universal Time). Quando si specificano le ore, i minuti e i secondi, l'ora deve essere racchiusa da "T" e "Z", come nel formato prescritto. 	| `posted:2014-12-01,2014-12-12` 	|
| `sentiment:sentiment-value` 	| Trova i Tweet con un sentimento particolare. I valori supportati sono: </br><dl>positive</dl> <dlentry>Il Tweet contiene più frasi di sentimento positivo che negativo.</dlentry> </br></br><dl>negative</dl> <dlentry>Il Tweet contiene più frasi di sentimento negativo che positivo.</dlentry>  </br></br><dl>neutral</dl>  <dlentry>Il Tweet non contiene alcun sentimento o è in una lingua che non offre l'individuazione del sentimento.</dlentry> </br></br><dl>ambivalent</dl>  <dlentry>Il Tweet contiene un numero uguale di frasi di sentimento positivo e negativo.</dlentry> 	| `sentiment:positive` 	|
| `statuses_count: lowerLimit,upperLimit` 	| Trova i Tweet dagli utenti che hanno pubblicato un numero di stati che rientra nell'intervallo specificato. Il limite superiore (upperLimit) è facoltativo ed entrambi i limiti sono inclusivi. 	| `statuses_count:1000,3000` 	|
| `time_zone:timeZone` 	| Trova i Tweet dagli utenti le cui impostazioni del profilo corrispondono al fuso orario specificato. 	| `time_zone:"Eastern Time (US & Canada)"` 	|
| `time_zone:city` 	| Trova i Tweet dagli utenti le cui impostazioni del profilo corrispondono alla città specificata. 	| `time_zone:"Dublin"` 	|
*Tabella 2. Termini di query*

Tutti i termini di query supportati possono essere combinati con gli operatori booleani descritti in precedenza. Ad esempio,

`ibm -apple followers_count:500`
