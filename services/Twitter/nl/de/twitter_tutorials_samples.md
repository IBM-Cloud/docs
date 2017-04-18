---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Insights for Twitter - Beispiele
{: #examples}

Als Einführung in den {{site.data.keyword.twittershort}}-Service können Sie die bereitgestellten Beispiele dazu verwenden, sich mit der Nutzung des Service vertraut zu machen.
{: shortdesc}

## Insights for Twitter - Demo
{: #insights_twitter_demo}

Für das Durchsuchen von Twitter-Datenstreams, die den {{site.data.keyword.twittershort}}-Service nutzen, steht eine Beispielanwendung für Sie zur Verfügung. Sie können auf die Anwendung zugreifen, wenn Sie zu [https://cdetestapp.mybluemix.net/](https://cdetestapp.mybluemix.net/){: new.window} navigieren. Die Anwendung wird in Ihrem Browser geöffnet und es wird ein Suchfeld mit den Schaltflächen **Twitter Search** und **Twitter Count** angezeigt. 

![Abbildung der Benutzerschnittstelle mit Suchfeld.](images/sample1_UI.jpg "Abbildung der Benutzerschnittstelle mit Suchfeld.")

Über die Beispielanwendung können Sie nach Tweets suchen und dabei die in [Abfragesprache](twitter_rest_apis.html#querylanguage){: new.window} beschriebenen unterstützten Parameter und Operatoren verwenden. Wenn Sie beispielsweise "IBM Twitter" eingeben (mit einem Leerzeichen, das auf eine boolesche AND-Operation hinweist) und auf die Option **Twitter Search** klicken, werden Tweets zurückgegeben, die beide Begriffe enthalten.

![Abbildung zum Abfragebegriff und zu den zurückgegebenen Suchergebnissen.](images/sample1_tweet_search.jpg "Abbildung zum Abfragebegriff und zu den zurückgegebenen Suchergebnissen.")

Wenn Sie "IBM Twitter" im Suchfeld angeben, wird nach dem Klicken auf **Twitter Count** die Anzahl der Tweets zurückgegeben, die beide Begriffe enthalten.

![Abbildung zum Abfragebegriff und zu den zurückgegebenen Ergebnissen für die Anzahl.](images/sample1_tweet_count.jpg "Abbildung zum Abfragebegriff und zu den zurückgegebenen Ergebnissen für die Anzahl.")

## Erstellen eines regelbasierten Tracks
{: #creating_rule_track}

Im Rahmen des Einstiegsplans können Benutzer regelbasierte Tracks zum Filtern von Tweets erstellen, die im PowerTrack-Datenstream erfasst werden. Anhand von Beispielen in nachfolgenden Abschnitten wird veranschaulicht, wie Tracks bearbeitet und gelöscht werden und wie ein search- oder count-API-Aufruf für den PowerTrack-Stream ausgeführt wird. Übergeben Sie zum Erstellen eines regelbasierten Tracks eine Anforderung des Typs **POST** mit der Operation /api/v1/tracks, geben Sie den Tracktyp (**Rule**) sowie ein Enddatum (endDate) und mindestens eine Regel an. Der folgende Ausschnitt ist ein Beispiel für eine Anforderung mit zwei Regeln:

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

`username` und `password` sind für die jeweilige Anwendung und Serviceinstanz eindeutig. Diese Informationen können der Umgebungsvariablen **VCAP_SERVICES** entnommen werden. Weitere Informationen hierzu finden Sie in [Einführung in {{site.data.keyword.twittershort}}](index.html#insights_twitter_overview){: new.window}.

Der Hauptteil der Antwort sieht in etwa wie im folgenden Ausschnitt aus:

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

Die Antwort enthält die eindeutige ID, die dem soeben erstellten Track zugeordnet ist. Darüber hinaus ist jeder Regel eine eindeutige ID zugewiesen. Das Enddatum (endDate) gibt an, wann der Track die Erfassung von Nachrichten stoppt; er muss dem UTC-Format entsprechen (`YYYY-MM-DD` oder `YYYY-MM-DDTHH:MM:SSZ`). Für die Eigenschaft 'type' muss entweder **Rule** oder **Aggregated** angegeben werden. Da dieses Beispiel die Erstellung eines regelbasierten Tracks veranschaulicht,
wurde der Typ **Rule** angegeben.

Wenn die Eigenschaft 'state' nicht in der Anforderung angegeben wird, wird der Track erstellt und erhält standardmäßig den Status **Aktiv**. Die Eigenschaft 'name' ist optional und muss nicht eindeutig sein. Für eine bessere Steuerung der Filter wird jedoch empfohlen, einen eindeutigen und aussagekräftigen Namen zu verwenden.

Detailliertere Informationen zur Regelsyntax finden Sie in {{site.data.keyword.twittershort}} - [Abfragesprache](twitter_rest_apis.html#querylanguage){: new.window}.

## Erstellen eines aggregierten Tracks
{: #creating_aggregated_track}

Im Rahmen des Einstiegsplans können Sie aggregierte Tracks erstellen, die zwei oder mehr vorhandene Tracks kombinieren. Aggregierte Tracks können sowohl regelbasierte als auch andere Tracks umfassen. Bei der Suche nach Tweets eines aggregierten Tracks werden Ergebnisse aus den beteiligten Tracks zurückgegeben. Übergeben Sie zum Erstellen eines aggregierten Tracks eine Anforderung des Typs **POST** mit der Operation /api/v1/tracks, geben Sie den Tracktyp (**Aggregated**) sowie zwei oder mehr Track-IDs an. Der folgende Ausschnitt ist ein Beispiel für eine Anforderung mit zwei Tracks:

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
`username` und `password` sind für die jeweilige Anwendung und Serviceinstanz eindeutig. Diese Informationen können der Umgebungsvariablen **VCAP_SERVICES** entnommen werden. Weitere Informationen hierzu finden Sie in [Einführung in {{site.data.keyword.twittershort}}](index.html#insights_twitter_overview){: new.window}.

Der Hauptteil der Antwort sieht in etwa wie im folgenden Ausschnitt aus:

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

Die Antwort enthält die eindeutige ID, die dem aggregierten Track zugeordnet ist. Im Gegensatz zu regelbasierten Tracks enthalten aggregierte Tracks keine Eigenschaft 'endDate' oder 'state', da diese Eigenschaften innerhalb der einzelnen regelbasierten Tracks verwaltet werden.

## Bearbeiten von Tracks
{: #editing_tracks}

Regelbasierte und aggregierte Tracks können bearbeitet werden, um das Filtern von Daten des PowerTrack-Streams zu präzisieren. Wenn Regeln zu vorhandenen Tracks hinzugefügt (oder geändert) werden, bleiben Nachrichten, die auf der Basis früherer Regeln abgerufen wurden, im Track enthalten. Um sicherzustellen, dass in den Suchergebnissen Daten für die neuesten Regeln zurückgegeben werden, löschen Sie den Track und erstellen Sie einen neuen Track mit den gewünschten Regeln.

Das Beispiel in [Regeltrack erstellen](#creating_rule_track){: new.window} enthielt zwei Regeln mit der Track-ID `66ff1961-51fe-4475-8bcd-c02f071d6fd1`. Verwenden Sie zum Hinzufügen der neuen Regel "Champions" die Operation POST /api/v1/tracks/{track Id} und fügen Sie die neue Regel an.

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
Auf ähnliche Weise können Sie Regeln aus einem vorhandenen Track entfernen, indem Sie die Operation GET /api/v1/tracks/{track Id} absetzen und die nicht mehr benötigten Regeln entfernen.

Das Beispiel in [Erstellen eines aggregierten Tracks](#creating_aggregated_track) enthielt zwei Tracks. Ein weiterer Track mit der ID `c4562594-1eeb-4a95-8fac-255428d74bce` kann mithilfe der folgenden Operation zum vorhandenen aggregierten Track hinzugefügt werden:

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

## Löschen von Tracks
{: #deleting_tracks}

Nicht mehr benötigte Tracks können mithilfe einer Operation des Typs DELETE /api/v1/tracks/{trackId} gelöscht werden. Diese Aktion kann sowohl für regelbasierte als auch für aggregierte Tracks angewendet werden. In einem aggregierten Track enthaltene Tracks können erst gelöscht werden, wenn der zu löschende Track aus allen aggregierten Tracks entfernt wurde. Das folgende Beispiel veranschaulicht das Löschen eines Tracks mit der ID `a22206cd-b72b-4b7d-a5a3-e2d08ce02a88`:

```
DELETE https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/a22206cd-b72b-4b7d-a5a3-e2d08ce02a88
HTTP/1.1
```

Alternativ dazu können Sie die Erfassung von Tweets eines bestimmten Tracks stoppen, indem Sie dessen Status in 'Inaktiv' ändern. Anstatt den Track zu löschen, wird er mit dem folgenden Beispiel inaktiviert:

```
POST https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/a22206cd-b72b-4b7d-a5a3-e2d08ce02a88
HTTP/1.1
{
    "state": "Inactive"
}
```

## Suche nach Tweets
{: #searching_tweets}

Sie können in Ihrer Anwendung eine GET-Operation absetzen, um Tweets aus einem der Streams abzurufen. Die Suche nach Decahose-Tweets wird beispielsweise wie folgt implementiert: `/api/v1/messages/search?q=QUERY&size=NUMBER&from=NUMBER`. Im Rahmen des Einstiegsplans können Benutzer die Suche nach Tweets des PowerTrack-Streams wie folgt implementieren: `/api/v1/tracks/{trackId}/messages/search?q=QUERY&size=NUMBER&from=NUMBER`.

Der Parameter "size" gibt die Anzahl der Nachrichten an, die in einer Abfrageantwort zurückgegeben werden sollen, der Parameter "from" gibt die ursprüngliche Nachricht an, die im vollständigen Ergebnissatz zurückgegeben werden soll. Die Referenz {trackId} ist die eindeutige ID für einen bestimmten Track.
Mithilfe von cURL können Sie im Decahose-Stream nach Tweets suchen, die die Zeichenfolge "IBM" enthalten, indem Sie Folgendes eingeben:

```
curl https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/messages/search?q=IBM
```

Dieselbe Abfrage für den PowerTrack-Stream lautet: 

```
curl https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/{trackId}/messages/search?q=IBM
```

`username` und `password` sind für die jeweilige Anwendung und Serviceinstanz eindeutig. Diese Informationen können der Umgebungsvariablen **VCAP_SERVICES** entnommen werden. Weitere Informationen hierzu finden Sie in [Einführung in {{site.data.keyword.twittershort}}](index.html#insights_twitter_overview){: new.window}.

Der Service gibt die Antworten im JSON-Format zurück. In der folgenden Tabelle sind die möglichen Antwortcodes aufgeführt.

| **HTTP-Statuscode** 	| **Ursache**                                                           	|
|------------------	|------------------------------------------------------------------	|
| 200              	| OK                                                               	|
| 400              	| Ungültige oder fehlende Eigenschaften zu Anforderungsnutzdaten.                   	|
| 401              	| Authentifizierung fehlgeschlagen. Es sind ein gültiger Benutzername und ein gültiges Kennwort erforderlich. 	|
| 403              	| Unzulässig; Limit erreicht.                                        	|
| 500              	| Es ist ein interner Fehler aufgetreten.                                  	|

** Tabelle 1. Antwortnachrichten

Der Hauptteil der Antwort kann wie folgt angezeigt werden:

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

Mit dem folgenden URL-codierten Abfrageausdruck werden Tweets zu einem Film abgerufen, und zwar auf der Grundlage eines angegebenen Zeitrahmens und der Häufigkeit. Dieses Beispiel könnte zur Feststellung des Grads des Interesses an oder der Reaktionen auf einen Filmtrailer verwendet werden.

```
/api/v1/messages/search?q=%28posted:2015-02-01T00:00:00Z%20AND%20%23americansniper%29&size=5 
```

Durch die Decodierung der URL sieht die Abfragesyntax und die zugehörige Operation wie folgt aus: "(posted:2015-02-01T00:00:00Z AND #americansniper) &size=5".

## Anzahl der Tweets ermitteln
{: #counting_tweets}

Sie können in Ihrer Anwendung zum Abrufen der Anzahl an Tweets, die mit einer angegebenen Abfrage übereinstimmen, eine GET-Operation anwenden. Abfragen an den Decahose-Stream werden wie folgt eingegeben: `/api/v1/messages/count?q=QUERY`; Abfragen an den PowerTrack-Stream weisen das folgende Format auf: 

```
/api/v1/tracks/{trackId}/messages/count?q=QUERY
```

Mithilfe von cURL können Sie die Anzahl der Tweets im Decahose-Stream ermitteln, die die Zeichenfolge "IBM" enthalten, indem Sie Folgendes eingeben:

```
curl https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/messages/count?q=IBM
```

Dieselbe Abfrage kann für die PowerTrack-Datenquelle wie folgt eingegeben werden: 

```
curl https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/{trackId}/messages/count?q=IBM
```

`username` und `password` sind für die jeweilige Anwendung und Serviceinstanz eindeutig. Diese Informationen können der Umgebungsvariablen **VCAP_SERVICES** entnommen werden. Weitere Informationen hierzu finden Sie in [Einführung in {{site.data.keyword.twittershort}}](index.html#insights_twitter_overview){: new.window}.

Der Service gibt die Antworten im JSON-Format zurück. In der folgenden Tabelle sind die möglichen Antwortnachrichten aufgeführt.

| **HTTP-Statuscode** 	| **Ursache**                                                           	|
|------------------	|------------------------------------------------------------------	|
| 200              	| OK                                                               	|
| 400              	| Ungültige oder fehlende Eigenschaften zu Anforderungsnutzdaten.                   	|
| 401              	| Authentifizierung fehlgeschlagen. Es sind ein gültiger Benutzername und ein gültiges Kennwort erforderlich. 	|
| 403              	| Unzulässig; Limit erreicht.                                        	|
| 500              	| Es ist ein interner Fehler aufgetreten.                                  	|

**Tabelle 2. Antwortnachrichten**

Der Hauptteil der Antwort kann wie folgt angezeigt werden:
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

Mit dem folgenden Abfrageausdruck wird die Anzahl an positiven Tweets abgerufen, die sowohl die Zeichenfolge "IBM" als auch die Zeichenfolge "Bluemix" enthalten. In diesem Fall werden Tweets des Decahose-Streams in der Antwort zurückgegeben.

`.../api/v1/messages/count?q="IBM Bluemix sentiment:positive`

Mit dem folgenden URL-codierten Abfrageausdruck wird über einen angegebenen Zeitraum hinweg die Anzahl an Tweets abgerufen, die die Zeichenfolge "IBM" enthalten. Diese Beispielabfrage könnte zur Messung der Beliebtheit eines Themas und zur Feststellung der Trendfähigkeit dieses Themas genutzt werden. In diesem Beispiel werden Tweets des PowerTrack-Streams zurückgegeben.

`.../api/v1/tracks/{trackId}/messages/count?q=%28posted:2015-02-01T00:00:00Z,2015-02-15T00:00:00Z AND %23IBM%29`

Durch die Decodierung der URL sieht die Abfragesyntax und die zugehörige Operation wie folgt aus: "(posted:2015-02-01T00:00:00Z,2015-02-15T00:00:00Z AND #IBM)".
