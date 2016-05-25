---

copyright:
	years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Aggregation von APIs
{: #api_aggregation}

*Letzte Aktualisierung: 31. März 2016*

Einige Insights for Weather-APIs können aggregiert werden. Mit einer Aggregation können Sie mindestens
zwei atomare API-Aufrufe in einer einzelnen HTTP-Anforderung zusammenfassen.
{: shortdesc}

Ein atomarer API-Aufruf referenziert eine der APIs, die einen Alias für die Aggregation definieren. Jedes API-Benutzerdokument enthält den Alias für den Aggregationsnamen im URL-Abschnitt
für Formatierungszeichen (falls für die Aggregation verfügbar). Die Standard-API für tägliche
Vorhersagen hat beispielsweise den Alias `v2fcstdaily10` für die Aggregation, mit dem
die 10-tägige Vorhersage als Teil einer aggregierten Anforderung abgerufen werden kann.

Eine Aggregation weist die folgenden Beschränkungen auf:

* Die dekomprimierte Gesamtantwortgröße für die vollständige Aggregation
darf nicht mehr als 1 MB betragen.
* URLs dürfen nicht länger als 4096 Zeichen lang sein
(einschließlich Protokoll-, Hostnamen-, Pfad- und Abfragezeichenfolge).
* Es können bis zu 10 atomare APIs aggregiert werden.

**Hinweis:** Wenn die Anforderung oder die Antwort gegen eine oder mehrere
dieser Beschränkungen verstößt, wird ein Fehler mit dem HTTP-Statuscode 500
(für gewöhnlich 500 oder 502; es können aber auch andere Codes zurückgegeben werden) ausgegeben. 

## Aggregierte API-URLs
Die aggregierte API-URL beginnt mit `/v2/aggregate/` gefolgt von Aliasnamen, die durch Semikolons getrennt sind.
Um beispielsweise die API für die 10-tägige Vorhersage (`v2fcstdaily10`) mit aktuellen Beobachtungen (`v2obscurrent`) zu aggregieren,
verwenden Sie das folgende Format:

```
/v2/aggregate/v2fcstdaily10;v2obscurrent
```

## Abfrageparameter für atomare APIs und Aggregation
Für alle Anforderungen sind Abfrageparameter erforderlich. Die Abfrageparameter für die Aggregation werden auf dieselbe Art und Weise wie
für die atomaren API-Aufrufe übergeben. Allerdings sind einige zusätzliche Regeln erforderlich. In den folgenden Abschnitten wird beschrieben, wie Sie zum Bilden verschiedener
Aggregationen angewendet werden können. 

### Angeben von Abfrageparametern, die sich auf alle atomaren APIs beziehen

Die einfachste Form der Aggregation ist,
wenn sich Abfrageparameter auf alle atomaren APIs beziehen. In diesem Fall weisen die Abfrageparameter das folgende
Standardformat auf: `?param1=value1&amp;param2=value2`.

Im folgenden Beispiel wird
`geocode=31.44,84.33&amp;language=en&amp;units=e` auf die Anforderung für die atomaren APIs
`v2fcstdaily10` und `v2obscurrent` angewendet: 

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2obscurrent?geocode=31.44,84.33&amp;language=en&amp;units=e
```

### Angeben, welche atomaren APIs welche Abfrageparameter empfangen

Wenn Sie für bestimmte atomare APIs
Parameter angeben müssen, können die Abfrageparameter die Stellenschreibweise
`?R1.param1=value1&amp;R2.param2=value2` verwenden. Bei diesem Format wird `param1` für die erste atomare API und `param2` für die zweite atomare API verwendet.

Im folgenden Beispiel gilt `geocode=31.44,84.33&amp;language=en&amp;units=e` für
`v2fcstdaily10` und `geocode=44.44,50.23&amp;language=en&amp;units=e`
für `v2obscurrent`.

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2obscurrent?R1.geocode=31.44,84.33&amp;R2.geocode=44.44,50.23&amp;language=en&amp;units=e
```

### Gruppieren von Abfrageparametern für bestimmte atomare APIs

Sie können Parameter gruppieren, indem Sie die Stellenschreibweise als durch Kommas getrenntes Format `?R1,R2.param1=value1&amp;param2=value2` verwenden.
Bei diesem Format wird `param1` für die ersten und zweiten atomaren APIs und `param2` für alle atomaren APIs verwendet.

Im folgenden Beispiel gilt `geocode=34.06,84.21&amp;language=enUS&amp;units=e` für `v2fcstdaily10` und
`v2obscurrent`. Es gilt `geocode= 33.06,81.11&amp;language=enUS&amp;units=e` für
`v2loc`:

```
https://twcservice.mybluemix.net/api/weather/v2 /aggregate/v2fcstdaily10;v2obscurrent;v2loc ?R1,R2.geocode= 34.06,84.21 &amp;R3.geocode= 33.06,81.11 &amp;language=enUS&amp;units=e
```

### Anfordern derselben Ressource auf unterschiedliche Weise

Sie können dieselbe Ressourcen
auf unterschiedliche Weise anfordern, beispielsweise in anderen Sprachen oder mit anderer Maßeinheit. Bei diesem Format kann die atomare API in der Anforderung wiederholt werden: `/v2/aggregate/v2fcstdaily10;v2fcstdaily10` und die Stellenschreibweise
des Parameters kann verwendet werden, um anzuzeigen, auf welche Weise die einzelnen APIs angefordert werden sollen:
`?R1.param1=value1&amp;R2.param1=value2`. In diesem Fall empfängt der Benutzer dieselbe Ressource, die auf unterschiedliche Weise
formatiert oder übersetzt ist.

Im folgenden Beispiel gilt `geocode=31.44,84.33&amp;language=en&amp;units=e` für die erste `v2fcstdaily10` und `geocode=31.44,84.33&amp;language=fr&amp;units=m`
für die zweite Anforderung `v2fcstdaily10`:

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2fcstdaily10?geocode=31.44,84.33&amp;R1.language=en&amp;R2.language=fr&amp;R1.units=e&amp;R2.units=m
```

Im folgenden Beispiel gilt `geocode=31.44,84.33&amp;language=en&amp;units=e` für die erste `v2fcstdaily10` und
`geocode=33.54,85.43&amp;language=en&amp;units=e` für die zweite
`Anforderung v2fcstdaily10` zum Abrufen mehrerer Standorte für dieselben Daten: 

```
https://twcservice.mybluemix.net/api/weather/v2/aggregate/v2fcstdaily10;v2fcstdaily10?R1.geocode=31.44,84.33&amp;R2.geocode=33.54,85.43&amp;language=en&amp;units=e
```




