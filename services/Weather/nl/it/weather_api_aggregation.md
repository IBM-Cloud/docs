---

copyright:
  years: 2016
lastupdated: "2016-06-15"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Aggregazione API
{: #api_aggregation}

Alcune API {{site.data.keyword.weather_short}} possono essere aggregate. Puoi utilizzare l'aggregazione per combinare due o più chiamate API atomic
in una singola richiesta HTTP.
{: shortdesc}

Una chiamata API atomic fa riferimento a ognuna delle API che definisce un alias per l'aggregazione. Ogni documento utente API
contiene l'alias per il nome di aggregazione nella sezione formato URL se è disponibile per
l'aggregazione. Ad esempio, l'API di previsione giornaliera standard dispone di un alias per l'aggregazione
`v2fcstdaily10` che può essere utilizzato per richiamare le previsioni giornaliere di 10 giorni come parte di una richiesta
aggregata.

L'aggregazione ha le seguenti limitazioni:

* La dimensione totale non compressa per l'aggregazione completa deve essere inferiore a 1
megabyte.
* Gli URL devono avere una lunghezza inferiore ai 4,096 caratteri (inclusi protocollo, nome host,
percorso e stringa di query).
* Puoi aggregare fino a 10 API atomic.

**Nota:** se la tua richiesta o risposta viola una di queste limitazioni, riceverai una risposta di errore
con un codice di stato HTTP 500 (solitamente 500 o 502, ma ne possono essere restituiti anche
altri).

## URL API aggregati
L'URL API aggregato inizia con `/v2/aggregate/` ed è seguito dagli alias
separati da punto e virgola.
Ad esempio, per aggregare l'API di previsione giornaliera di 10 giorni (`v2fcstdaily10`) con
le osservazioni correnti (`v2obscurrent`), utilizzare il seguente formato:

```
/v2/aggregate/v2fcstdaily10;v2obscurrent
```

## Regole del parametro di query per le API e l'aggregazione
I parametri di query sono necessari per tutte le richieste. I parametri di query per l'aggregazione
vengono trasmessi così come le chiamate API atomic con
alcune regole extra. Le seguenti sezioni descrivono
come possono essere applicati per formare differenti aggregazioni.

### Specifica i parametri di query da applicare a tutte le API atomic

Il formato di aggregazione più semplice è
quando i parametri di query vengono applicati a tutte le API atomic. In questo caso, i parametri di query hanno il formato standard
`?param1=value1&amp;param2=value2`.

Il seguente esempio applica
`geocode=31.44,84.33&amp;language=en&amp;units=e` per le API atomic
`v2fcstdaily10` e `v2obscurrent`:

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2obscurrent?geocode=31.44,84.33&amp;language=en&amp;units=e
```

### Specifica quale API atomic riceve quale parametro di query

Se hai bisogno di specificare i parametri per delle API atomic specifiche,
i parametri di query possono utilizzare la notazione di ubicazione
`?R1.param1=value1&amp;R2.param2=value2`. Questo formato utilizza `param1`
per la prima API atomic e `param2` per la seconda API atomic.

Il seguente esempio applica `geocode=31.44,84.33&amp;language=en&amp;units=e` a
`v2fcstdaily10` e `geocode=44.44,50.23&amp;language=en&amp;units=e`
a `v2obscurrent`.

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2obscurrent?R1.geocode=31.44,84.33&amp;R2.geocode=44.44,50.23&amp;language=en&amp;units=e
```

### Raggruppa i parametri di query per API atomic specifiche

Puoi raggruppare i parametri utilizzando la notazione di ubicazione
come un formato separato da virgola `?R1,R2.param1=value1&amp;param2=value2`.
Questo formato utilizza `param1` per la prima e la seconda API atomic e
`param2` per tutte le API atomic.

Il seguente esempio applica `geocode=34.06,84.21&amp;language=enUS&amp;units=e` a `v2fcstdaily10` e
`v2obscurrent`. Applica `geocode= 33.06,81.11&amp;language=enUS&amp;units=e` a
`v2loc`:

```
https://twcservice.mybluemix.net/api/weather/v2 /aggregate/v2fcstdaily10;v2obscurrent;v2loc ?R1,R2.geocode= 34.06,84.21 &amp;R3.geocode= 33.06,81.11 &amp;language=enUS&amp;units=e
```

### Richiedi la stessa risorsa più volte

Puoi richiedere la stessa risorsa più volte,
come ad esempio in altre lingue o con differenti unità di misura. Con questo formato, l'API atomic può essere ripetuta nella richiesta:
`/v2/aggregate/v2fcstdaily10;v2fcstdaily10` e
l'annotazione di ubicazione del parametro può essere utilizzata per indicare in quale modo richiedere quale API:
`?R1.param1=value1&amp;R2.param1=value2`. In questo caso, l'utente riceve la stessa risorsa
formata o tradotta in modi diversi.

Il seguente esempio applica `geocode=31.44,84.33&amp;language=en&amp;units=e` alla prima
`v2fcstdaily10` e `geocode=31.44,84.33&amp;language=fr&amp;units=m`
alla seconda `v2fcstdaily10`:

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2fcstdaily10?geocode=31.44,84.33&amp;R1.language=en&amp;R2.language=fr&amp;R1.units=e&amp;R2.units=m
```

Il seguente esempio applica `geocode=31.44,84.33&amp;language=en&amp;units=e` alla prima
`v2fcstdaily10` e
`geocode=33.54,85.43&amp;language=en&amp;units=e` alla seconda
`v2fcstdaily10` per richiamare più ubicazioni per gli stessi
dati:

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2fcstdaily10?R1.geocode=31.44,84.33&amp;R2.geocode=33.54,85.43&amp;language=en&amp;units=e
```




