---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Esempi di Insights for Twitter
{: #examples}

Introduzione al servizio {{site.data.keyword.twittershort}}, utilizza gli esempi forniti per imparare ad utilizzare e su come sfruttare il servizio.
{: shortdesc}

## Demo di Insights for Twitter
{: #insights_twitter_demo}

È disponibile un'applicazione di esempio per la tua ricerca di flussi di dati Twitter che utilizza il servizio {{site.data.keyword.twittershort}}. L'applicazione è accessibile all'indirizzo [https://cdetestapp.mybluemix.net/](https://cdetestapp.mybluemix.net/){: new.window}. L'applicazione si apre in un nuovo browser e visualizza un campo di ricerca con i pulsanti **Twitter Search** e **Twitter Count**. 

![Immagine dell'interfaccia utente con il campo di ricerca.](images/sample1_UI.jpg "Immagine dell'interfaccia utente con il campo di ricerca.")

Dall'applicazione di esempio, puoi ricercare i Tweet utilizzando gli operatori e i parametri supportati descritti in [Linguaggio di query](twitter_rest_apis.html#querylanguage){: new.window}. Ad esempio, immettendo "IBM Twitter" (con uno spazio per rappresentare un'operazione booleana AND) e facendo clic su **Twitter Search**, sono restituiti i Tweet che contengono entrambi i termini.

![Immagine del termine di query e dei risultati della ricerca.](images/sample1_tweet_search.jpg "Immagine del termine di query e dei risultati della ricerca restituiti.")

Con "IBM Twitter" specificato nel campo di ricerca, facendo clic su **Twitter Count** viene restituito il numero di Tweet che contengono entrambi i termini.

![Immagine del termine di query e dei risultati del conteggio.](images/sample1_tweet_count.jpg "Immagine del termine di query e dei risultati del conteggio restituiti.")

## Creazione di una traccia di regole
{: #creating_rule_track}

Come utente del piano di ingresso, puoi creare una traccia basata sulle regole per filtrare i Tweet raccolti nel flusso di dati PowerTrack. Gli esempi nelle successive sezioni dimostrano come modificare ed eliminare le tracce, così come l'esecuzione di una ricerca o una chiamata API di conteggio nel flusso PowerTrack. Per creare una traccia di regole, immetti una richiesta **POST** con l'operazione /api/v1/tracks, specifica il tipo di traccia **Regola**), indica una 'Data di fine' e includi almeno una regola. Il seguente frammento è un richiesta di esempio che include due regole:

```
POST https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks
HTTP/1.1 Content-Type: application/json
{
    "endDate": "2015-10-03T10:23:00Z",
    "name": "My First Rule Track",
    "type": "Rule",
    "rules": [
        {"value": "Canada"},
        {"value": "sport hockey"}
    ]
}
```

I valori `username` e `password` sono univoci nell'applicazione e nell'istanza del servizio. Queste informazioni possono essere ottenute dalle variabili di ambiente **VCAP_SERVICES**. Per ulteriori informazioni, consulta [Introduzione a {{site.data.keyword.twittershort}}](index.html#insights_twitter_overview){: new.window}.

Il corpo della risposta sarà simile al seguente frammento:

```
HTTP/1.1 201 Created
Content-Type: application/json;charset=utf-8
Location: https://cdeservice.mybluemix.net:443/api/v1/tracks/66ff1961-51fe-4475-8bcd-c02f071d6fd1
{
    "id": "66ff1961-51fe-4475-8bcd-c02f071d6fd1",
    "type": "Rule",
    "state": "Active",
    "createdDate": "2015-08-06T20:38:28.940Z",
    "endDate": "2015-10-03T10:23:00Z",
    "name": "My First Rule Track",
    "rules": [
        {
          "id": "06497963-4fe3-47e8-90cd-aaef25f31314"
          "value": "Canada"
        },
        {
          "id": "d021165d-85e2-456a-af16-b9c026d76208",
          "value": "sport hockey"
        }
    ]
}
```

La risposta include l'ID univoco associato con la traccia appena creata. In aggiunta, a ogni regola è assegnato un ID univoco. La data di fine indica quando la traccia si arresta dal raccogliere i messaggi e deve essere conforme al formato UTC `YYYY-MM-DD` o `YYYY-MM-DDTHH:MM:SSZ`). Deve essere specificata la proprietà del tipo **Regola** o **Aggregata**. Questo esempio mostra la creazione di una traccia basata sulle regole, quindi è stato specificato il tipo **Regola**.

Se la proprietà dello stato non è specificata nella richiesta, la traccia viene creata ed è **Attiva** per impostazione predefinita. La proprietà del nome è facoltativa e non è obbligatorio che sia univoca. Per meglio gestire i tuoi filtri, è raccomandata la selezione di un nome descrittivo e univoco.

Per informazioni dettagliate sulla sintassi delle regole, fai riferimento al {{site.data.keyword.twittershort}} [Linguaggio di query](twitter_rest_apis.html#querylanguage){: new.window}.

## Creazione di un traccia aggregata
{: #creating_aggregated_track}

Come utente del piano di ingresso, puoi creare tracce aggregate che combinano due o più tracce esistenti. Le tracce aggregate possono includere le tracce basate sulle regole e altre tracce aggregate. La ricerca di Tweet da una traccia aggregata restituisce i risultati dalle sue tracce costituenti. Per creare una traccia aggregata, immetti una richiesta **POST** con l'operazione /api/v1/tracks, specifica il tipo di traccia (**Aggregata**) e includi due o più ID di traccia. Il seguente frammento è un richiesta di esempio che include due tracce:

```
POST https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks
HTTP/1.1 Content-Type: application/json
{
    "name": "My Aggregated Track",
    "type": "Aggregated",
    "trackIds": [
       {"id": "a22206cd-b72b-4b7d-a5a3-e2d08ce02a88"},
       {"id": "180356df-9a78-491e-b070-f3ffbe00bdf2"}
     ]
}
```
I valori `username` e `password` sono univoci nell'applicazione e nell'istanza del servizio. Queste informazioni possono essere ottenute dalle variabili di ambiente **VCAP_SERVICES**. Per ulteriori informazioni, consulta [Introduzione a {{site.data.keyword.twittershort}}](index.html#insights_twitter_overview){: new.window}.

Il corpo della risposta sarà simile al seguente frammento:

```
HTTP/1.1 201 Created 
Content-Type: application/json;charset=utf-8
Location: https://cdeservice.mybluemix.net:443/api/v1/tracks/66ff1961-51fe-4475-8bcd-c02f071d6fd1
{
  "id": "9808fb82-7ea8-4b8e-9cd5-ad653a6dabe6",
  "type": "Aggregated",
  "createdDate": "2015-08-07T17:05:51.214Z",
  "name": "My Aggregated Track",
  "trackIds": [
    {
      "id": "a22206cd-b72b-4b7d-a5a3-e2d08ce02a88"
    },
    {
      "id": "180356df-9a78-491e-b070-f3ffbe00bdf2"
    }
  ]
}
```

La risposta include l'ID univoco associato con la traccia aggregata. A differenza delle tracce basate sulle regole, le tracce aggregate non includono le proprietà data di fine o stato, perché queste proprietà sono gestite nelle tracce basate sulle regole individuali.

## Modifica delle tracce
{: #editing_tracks}

Le tracce regola e aggregata possono essere modificate per affinare come vengono filtrati i dati nel flusso PowerTrack. Quando le regole vengono aggiunte (o modificate) nelle tracce esistenti, i messaggi che sono richiamati in base alle regole precedenti rimangono archiviati nella traccia. Per verificare che i risultati della ricerca restituiscano i dati per l'ultima serie di regole, elimina la traccia e creane una nuova con la serie di regole prevista.

L'esempio nella [Creazione di una traccia di regole](#creating_rule_track){: new.window} include due regole con un ID di traccia `66ff1961-51fe-4475-8bcd-c02f071d6fd1`. Per aggiungere una nuova regola con un valore di "Champions", utilizza l'operazione POST /api/v1/tracks/{track Id} e aggiungi la nuova regola.

```
POST https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/66ff1961-51fe-4475-8bcd-c02f071d6fd1
HTTP/1.1 Content-Type: application/json
{
    "endDate": "2015-10-03T10:23:00Z",
    "name": "My First Rule Track",
    "type": "Rule",
    "rules": [
        {"value": "Canada"},
        {"value": "sport hockey"},
        {"value": "Champions"}
    ]
}
```
In modo simile, puoi rimuovere le regole da una traccia esistente immettendo l'operazione GET /api/v1/tracks/{track Id} e rimuovere le regole non desiderate.

L'esempio nella [Creazione di una traccia aggregata](#creating_aggregated_track) include due tracce. Può essere aggiunta un'altra traccia con ID `c4562594-1eeb-4a95-8fac-255428d74bce` alla traccia aggregata esistente immettendo la seguente operazione:

```
POST https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/9808fb82-7ea8-4b8e-9cd5-ad653a6dabe6
HTTP/1.1 Content-Type: application/json
{
  "trackIds": [
    {"id": "a22206cd-b72b-4b7d-a5a3-e2d08ce02a88"},
    {"id": "180356df-9a78-491e-b070-f3ffbe00bdf2"},
    {"id": "c4562594-1eeb-4a95-8fac-255428d74bce"}
  ]
}
```

## Eliminazione delle tracce
{: #deleting_tracks}

Puoi eliminare le tracce che non sono più necessarie immettendo l'operazione DELETE /api/v1/tracks/{trackId}. Questa azione può essere applicata ad entrambe le tracce aggregate e basate sulle regole. Le tracce incluse nella traccia aggregata non possono essere eliminate finché la traccia non viene rimossa da tutte le tracce aggregate. Il seguente esempio mostra come eliminare una traccia con ID `a22206cd-b72b-4b7d-a5a3-e2d08ce02a88`:

```
DELETE https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/a22206cd-b72b-4b7d-a5a3-e2d08ce02a88
HTTP/1.1
```

In alternativa, puoi arrestare la raccolta di Tweet da una traccia in particolare modificando il relativo stato con Inattiva. Invece di eliminare la traccia, il seguente esempio la disabilita:

```
POST https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/a22206cd-b72b-4b7d-a5a3-e2d08ce02a88
HTTP/1.1
{
    "state": "Inactive"
}
```

## Ricerca di Tweet
{: #searching_tweets}

Puoi immettere un'operazione GET nella tua applicazione per richiamare i Tweet da entrambi i flussi di dati. Ad esempio, la ricerca per i Tweet Decahose viene implementata come: `/api/v1/messages/search?q=QUERY&size=NUMBER&from=NUMBER`. Per gli utenti del piano di ingresso, la ricerca di Tweet dal flusso PowerTrack viene implementata come: `/api/v1/tracks/{trackId}/messages/search?q=QUERY&size=NUMBER&from=NUMBER`.

Il parametro "size" specifica il numero di messaggi da restituire in una risposta della query, mentre il parametro "from" indica il messaggio iniziale da restituire nella serie di risultati completa. Il riferimento {trackId} è l'identificativo univoco per la traccia specificata.
Utilizzando cURL, puoi ricercare i Tweet nel flusso Decahose che contengono "IBM" digitando:

```
curl https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/messages/search?q=IBM
```

L'invio della stessa query nel flusso PowerTrack deve essere immesso come: 

```
curl https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/{trackId}/messages/search?q=IBM
```

I valori `username` e `password` sono univoci nell'applicazione e nell'istanza del servizio. Queste informazioni possono essere ottenute dalle variabili di ambiente **VCAP_SERVICES**. Per ulteriori informazioni, consulta [Introduzione a {{site.data.keyword.twittershort}}](index.html#insights_twitter_overview){: new.window}.

Il servizio ritorna le risposte nel formato JSON. La seguente tabella elenca i codici di risposta possibili.

| **Codice stato HTTP** 	| **Motivo**                                                           	|
|------------------	|------------------------------------------------------------------	|
| 200              	| OK                                                               	|
| 400              	| Invalid or missing request payload properties.                   	|
| 401              	| Authentication failed. Valid username and password are required. 	|
| 403              	| Forbidden, limit reached.                                        	|
| 500              	| An internal error has occurred.                                  	|

** Tabella 1. Messaggi di risposta

Il corpo delle risposta può essere simile a:

```
{
    "search": {
        "results": 16283624
    },
    "tweets": [{
        "message": {
            ...
            "body": "this is a nice tweet",
            "actor": {
                "followersCount”: 456,
                "displayName": "IBM Tweeter"
                ...
            },
            "cde": {
                "sentiment": {"polarity": "POSITIVE"...
                },
                "author": {"gender": "male"...
                },
                ...
            }
        }
    }]
}
```

La seguente espressione di query codificata URL richiama i Tweet su un film in base all'intervallo di tempo specificato e al numero di ricorrenze. Questo esempio può essere utilizzato per determinare il livello di interesse o le reazioni a un trailer di un film.

```
/api/v1/messages/search?q=%28posted:2015-02-01T00:00:00Z%20AND%20%23americansniper%29&size=5 
```

Decodificando l'URL, l'operazione e la sintassi della query diventa "(posted:2015-02-01T00:00:00Z AND #americansniper) &size=5".

## Conteggio numero di Tweet
{: #counting_tweets}

Puoi applicare un'operazione GET nella tua applicazione per richiamare il numero di Tweet che corrispondono a una query specificata. Le query in Decahose vengono emesse come: `/api/v1/messages/count?q=QUERY`, mentre le chiamate nel flusso PowerTrack utilizzano il seguente formato: 

```
/api/v1/tracks/{trackId}/messages/count?q=QUERY
```

Utilizzando cURL, puoi trovare il numero di Tweet, in Decahose, che contengono "IBM" utilizzando:

```
curl https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/messages/count?q=IBM
```

La stessa query può essere emessa nell'origine dati PowerTrack come: 

```
curl https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/{trackId}/messages/count?q=IBM
```

I valori `username` e `password` sono univoci nell'applicazione e nell'istanza del servizio. Queste informazioni possono essere ottenute dalle variabili di ambiente **VCAP_SERVICES**. Per ulteriori informazioni, consulta [Introduzione a {{site.data.keyword.twittershort}}](index.html#insights_twitter_overview){: new.window}.

Il servizio ritorna le risposte nel formato JSON. La seguente tabella elenca i messaggi di risposta possibili.

| **Codice stato HTTP** 	| **Motivo**                                                           	|
|------------------	|------------------------------------------------------------------	|
| 200              	| OK                                                               	|
| 400              	| Invalid or missing request payload properties.                   	|
| 401              	| Authentication failed. Valid username and password are required. 	|
| 403              	| Forbidden, limit reached.                                        	|
| 500              	| An internal error has occurred.                                  	|

**Tabella 2. Messaggi di risposta**

Il corpo delle risposta può essere simile a:
```
{
  "related": {
      "search": {
          "href": "https://server.bluemix.net/api/v1/messages/search?q=ibm" 
      }
  },
  "search": {
      "results": 21695
  }
}
```

La seguente espressione di query richiama il numero di Tweet positivi che contengono sia "IBM" che "Bluemix". In questo caso, i Tweet da Decahose vengono restituiti nella risposta.

`.../api/v1/messages/count?q="IBM Bluemix sentiment:positive`

La seguente espressione di query codificata URL richiama il numero di Tweet che contengono "IBM" in un periodo di tempo specificato. Questa query di esempio può aiutare a misurare la popolarità di un soggetto e determinare se è di moda. I Tweet dal flusso PowerTrack sono restituiti in questo esempio.

`.../api/v1/tracks/{trackId}/messages/count?q=%28posted:2015-02-01T00:00:00Z,2015-02-15T00:00:00Z AND %23IBM%29`

Decodificando l'URL, l'operazione e la sintassi della query diventa "(posted:2015-02-01T00:00:00Z,2015-02-15T00:00:00Z AND #IBM)".
