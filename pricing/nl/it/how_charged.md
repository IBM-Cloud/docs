---



copyright:

  years: 2015, 2017
lastupdated: "2017-04-12"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Modalità di addebito
{: #charges}

Gli addebiti variano a seconda delle risorse utilizzate da una specifica opzione di servizio, runtime, contenitore o supporto. Le risorse possono essere il numero di chiamate API, il numero di istanze, la
memoria, l'archiviazione e così via. {{site.data.keyword.Bluemix_notm}} fornisce anche degli stimatori del costo dettagliati e un calcolatore dei costi accurato per aiutarti a pianificare i tuoi addebiti. Puoi controllare il costo effettivo dopo aver creato le tue applicazioni nella pagina Dashboard di utilizzo.

Con un account fatturabile {{site.data.keyword.Bluemix_notm}}, gli addebiti a tuo carico sono basati sull'elaborazione, sui contenitori e sui servizi utilizzati nella tua organizzazione. Potresti essere invitato da altri utenti {{site.data.keyword.Bluemix_notm}}
a partecipare ad organizzazioni sotto un account differente. Se crei delle applicazioni o utilizzi dei servizi nelle organizzazioni alle quali sei invitato, l'utilizzo che ne consegue viene addebitato all'account che contiene tali organizzazioni. Per ulteriori informazioni su uno specifico piano puoi utilizzare la pagina dei dettagli di una risorsa dal catalogo {{site.data.keyword.Bluemix_notm}} o il calcolatore dei prezzi nella pagina Prezzi {{site.data.keyword.Bluemix_notm}}.

Vengono applicati diversi tipi di addebiti a seconda delle funzioni di {{site.data.keyword.Bluemix_notm}} che stai utilizzando. La seguente tabella fornisce una panoramica di alto livello:

| Tipo di addebito | Descrizione | Funzioni {{site.data.keyword.Bluemix_notm}} che utilizzano questo tipo di addebito | Esempio |
|------------------|------------------|--------------------------|--------------------------|
| Fisso | Il prezzo forfettario è basato su un addebito mensile concordato che non viene adeguato. | Servizi  | Data Cache ha un piano fisso che viene addebitato a una tariffa mensile fissa. |
| Misurato | Il prezzo a utilizzo misurato è basato sul numero di GB-ore consumate per i runtime e sul numero di GB-ore e sulla quantità di indirizzi IP e archiviazione per i contenitori. | Servizi, elaborazione e contenitori | Per il servizio Push, la quota di utilizzo che supera la franchigia mensile viene addebitata. |
|  A livelli   |  Alcuni piani di prezzo sono basati su un modello di prezzi a livelli, quindi puoi ottenere uno sconto basato sui
volumi in base al tuo utilizzo effettivo. I servizi possono offrire dei piani di prezzo di livello a blocchi, graduale o semplice. | Servizi | Il prezzo a livelli viene di norma utilizzato per le metriche di addebito di cui è prevista una quantità molto elevata al mese, come le chiamate API. |
| Riservato | Il prezzo riservato è basato su un impegno a lungo termine per un servizio, in modo da consentirti di ottenere un prezzo scontato. Con un piano riservato, ottieni un'istanza del servizio dedicato facile da configurare, distribuire e consegnare in ambiente {{site.data.keyword.Bluemix_notm}} pubblico. | Servizi | DB2 su Cloud ha dei piani riservati.|

## Addebiti per le risorse di elaborazione
{: #compute}

L'addebito è basato sul tempo di esecuzione delle tue applicazioni e sulla memoria utilizzata, calcolata come *GB-ore*. GB-ore è il calcolo
del numero di istanze applicazione, moltiplicato per la memoria per ogni singola
istanza, moltiplicato per le ore di esecuzione delle istanze. Puoi personalizzare il numero di
istanze e la quantità di memoria per ogni singola istanza in base alle tue
esigenze. Puoi anche aggiungere memoria o istanze per eseguire un ridimensionamento per un numero maggiore di utenti. L'addebito finale è in GB-ora: il numero di istanze applicazione moltiplicato per la memoria per ogni singola istanza, moltiplicato per le ore di esecuzione.

Considera ad esempio un runtime che costa $0,07 per GB-ora e due istanze di 512 MB, in esecuzione per 30 giorni (720 ore). Queste risorse costerebbero $24,15 USD, compresa la franchigia di 375 GB-ore, con i seguenti calcoli:

```
2 istanze x 0,5 GB x 720 ore = 720 GB-ore.
(720 - 375) GB-ore x $0,07 per GB-ora = $24,15
```

## Addebiti per i servizi
{: #services}

Molti servizi
includono delle franchigie mensili. L'utilizzo dei servizi che non è incluso come parte
della franchigia viene addebitato in uno dei seguenti modi:
<dl>
<dt>Addebiti fissi</dt>
    <dd>Selezioni un piano e paghi in base a una tariffa forfettaria. Ad esempio, il servizio Data Cache viene addebitato a una tariffa forfettaria.</dd>
<dt>Addebiti misurati</dt>
    <dd>Paghi in base al consumo che fai di runtime e servizi. Ad esempio, con il
servizio Push, la quota di utilizzo che supera la franchigia mensile viene
addebitata.</dd>
<dt>Addebiti riservati</dt>
    <dd><p>In quanto proprietario di un account Pagamento a consumo o di un account Sottoscrizione, puoi riservare un'istanza del servizio, con un impegno a lungo termine, per un prezzo scontato. Ad esempio, puoi riservare l'offerta standard DB2 on Cloud di grandi dimensioni per 12 mesi.</p>
    <p>Alcuni servizi {{site.data.keyword.Bluemix_notm}} offrono dei piani riservati. Puoi richiedere un piano riservato dal <strong>Catalogo</strong> {{site.data.keyword.Bluemix_notm}} facendo clic sul tile del servizio. Seleziona quindi il piano di servizio che meglio soddisfa le tue esigenze. Se è disponibile un piano riservato, fai clic su <strong>Richiesta</strong> e attieniti alle richieste che ti vengono presentate per inviare la tua richiesta. Riceverai un'e-mail che contiene le informazioni sul prezzo del piano riservato. Verrai anche contattato al più presto da un rappresentante del settore Vendite di {{site.data.keyword.Bluemix_notm}} per completare l'acquisto.</p></dd>
<dt>Addebiti a livelli</dt>
    <dd>Analogamente agli addebiti misurati, paghi in base al tuo consumo di runtime e servizi. Tuttavia, gli addebiti a livelli aggiungono degli ulteriori livelli di prezzo, spesso offrendo degli addebiti scontati nei livelli con un più ampio consumo. Il prezzo a livelli è offerto in modalità semplice, graduale o a blocchi.</dd>
</dl>

### Livello semplice
{: #simple_tier}

Nel modello di livello semplice, il prezzo unitario è determinato
dal livello in cui rientra la quantità da te utilizzata. Il prezzo
totale è tale quantità moltiplicata per il prezzo unitario nel
livello di competenza. Ad
esempio:

| Quantità di elementi | Prezzo unitario per tutti gli elementi |
|-------------------|--------------------------|
| Livello 1: 1 - 1000  | $1 USD                   |
| Livello 2: 1001 - 2000    |    $0,90 USD                      |
| Livello 3: 2001 - 3000                  |   $0,75 USD                       |
| Livello 4: 3001 - 4000           |      $0,60 USD                    |
|Livello 5: &gt; 4000 | $0,40 USD |
{:caption="Tabella 1. Tabella prezzi di livello semplice" caption-side="top"}

La seguente tabella
illustra quanto paghi con un piano basato su un modello di prezzi di livello semplice:

| Quantità di elementi | Calcolo dell'addebito | Prezzo totale |
|-------------------|--------------------|-------------|
|500 |	500 × 1 = 500 |	$500 USD|
|1500 |	1500 × 0,90 = 1350 |	$1350 USD|
|2500 |	2500 × 0,75 = 1875 |	$1875 USD|
|... |	... |	...|
|5200 |	5200 × 0,40 = 2080 |$2080 USD|
{:caption="Tabella 2. Calcolo dell'addebito utilizzando un modello di prezzi di livello semplice" caption-side="top"}

### Livello graduale
{: #graduated_tier}

Nel modello di livello graduale, il prezzo unitario per livello si riduce
man mano che il tuo livello di utilizzo aumenta. Il prezzo totale è dato
dagli addebiti cumulativi per ciascun livello di utilizzo, che consiste nella
tua quantità moltiplicata per il prezzo unitario al livello di appartenenza. Ad
esempio:

| Quantità di elementi |	Prezzo unitario per gli elementi nel livello|
|-------------------|------------------------------------|
|    Livello 1: 1 - 1000 |	$1 USD |
|   Livello 2: 1001 - 2000 |	$0,90 USD |
|    Livello 3: 2001 - 3000 |	$0,75 USD |
|    Livello 4: 3001 - 4000 |	$0,60 USD |
|    Livello 5: &gt; 4000 |	$0,40 USD |
{:caption="Tabella 3. Tabella prezzi di livello graduale" caption-side="top"}

La seguente tabella
illustra quanto paghi con un piano basato su un modello di prezzi di livello graduale:

|Quantità di elementi | Calcolo dell'addebito | Prezzo totale|
|------------------|--------------------|------------|
|500 |	500 × 1 (prezzo unitario per il livello 1) = 500 |	$500 USD|
|1500 |	(1000 × 1 (prezzo unitario per il livello 1)) + (500 × 0,90 (prezzo unitario per il livello 2)) = 1450 |	$1450 USD|
|2500 |	(1000 × 1 (prezzo unitario per il livello 1)) + (1000 × 0,90 (prezzo unitario per il livello 2)) + (500 × 0,75 (prezzo unitario per il livello 3)) = 2275 |	$2275 USD |
|... |	... |	...|
|5200 |	(1000 × 1 (prezzo unitario per il livello 1)) + (1000 × 0,90 (prezzo unitario per il livello 2)) + (1000 × 0,75 (prezzo unitario per il livello 3)) + (1000 × 0,60 (prezzo unitario per il livello 4)) + (1200 × 0,40 (prezzo unitario per il livello 5)) = 3730 |	$3730 USD|
{:caption="Tabella 4. Calcolo dell'addebito utilizzando un modello di prezzi di livello graduale" caption-side="top"}

### Livello a blocchi
{: #block_tier}

Nel modello di livello a blocchi, il prezzo è un addebito fisso per la
quantità da te impiegata entro uno specifico livello di utilizzo. Il prezzo totale è l'addebito
per il livello di utilizzo da te scelto, indipendentemente dal tuo utilizzo effettivo. Ogni livello
successivo fornisce un rapporto prezzo-quantità più basso. Ad
esempio:

|Quantità di elementi |	Prezzo totale per tutti gli elementi|
|------------------|-----------------------------|
| Livello 1: &lt;= 1000 |	$1000 USD|
| Livello 2: &lt;= 2000 |	$1900 USD|
| Livello 3: &lt;= 3000 |	$2800 USD|
| Livello 4: &lt;= 4000 |	$3500 USD|
| Livello 5: &lt;= 10000 |	$5000 USD|
{:caption="Tabella 5. Tabella prezzi di livello a blocchi" caption-side="top"}

La seguente tabella
illustra quanto paghi con un piano basato su un modello di prezzi di livello a blocchi:

|Quantità di elementi |	Calcolo dell'addebito |	Prezzo totale|
|------------------|-----------------------|---------------|
|500 |	Il numero di elementi rientra nel livello 1, quindi
il prezzo totale è $1000 USD. |	$1000 USD|
|1500 |	Il numero di elementi rientra nel livello 2, quindi
il prezzo totale è $1900 USD. |	$1900 USD|
|... |	... |	...|
|5200 |	Il numero di elementi rientra nel livello 5, quindi
il prezzo totale è $5000 USD. |	$5000 USD|
{:caption="Tabella 6. Calcolo dell'addebito utilizzando un modello di prezzi di livello a blocchi" caption-side="top"}
