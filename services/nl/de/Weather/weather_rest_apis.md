---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.weather_short}}-REST-APIs verwenden
{: #rest_apis}

*Letzte Aktualisierung: 01. Juli 2016*
{: .last-updated}

Sie können die [REST-APIs](https://twcservice.{APPDomain}/rest-api/){:new_window} zum Abrufen von Wetterdaten verwenden. Sie können API-Operationen testen und sofort die Ergebnisse anzeigen, um so Ihre Anwendungen schneller erstellen zu können.
{: shortdesc}

Klicken Sie in der Referenzdokumentation auf **Operationen auflisten**,
um Details zu den einzelnen Operationen anzuzeigen.
Wenn Sie Parameter angeben und auf **Ausprobieren** klicken,
können Sie zur Angabe von Berechtigungsnachweisen aufgefordert werden.
Sie müssen den Benutzernamen und das Kennwort aus Ihren Umgebungsvariablen des Typs
`VCAP_SERVICES` angeben.
Diese Informationen erhalten Sie,
wenn Sie Ihre Anwendung öffnen und im Inhaltsverzeichnis auf die Option für die **Umgebungsvariablen** klicken.

**Hinweis:** Alle Bereiche sind voneinander unabhängig. Sie können die Berechtigungsnachweise des Service,
die Ihnen in einer Region bereitgestellt wurden, nicht für die Authentifizierung
bei einem Service in einer anderen Region verwenden.
Wenn Sie keine gültigen Berechtigungsnachweise eingeben, wird im
Antwortteil eine Nachricht über unberechtigten Zugriff ausgegeben.

Mit den REST-APIs können Sie unter Angabe von Koordinaten der Breiten- und Längengrade Wetterdaten abrufen.
Sie können die folgenden APIs verwenden.

|**API**                                  |**Beschreibung**              |
|-----------------------------------------|-----------------------------|
|`GET /v1/{geocode or location ID}/forecast/hourly/48hour.json`  |Gibt die stündliche Wettervorhersage für die nächsten 48 Stunden für angegebene Geoortungsdaten entsprechend dem von Ihnen angegebenen Format zurück. Sie können `geocode/{latitude}/{longitude}` oder `location/{locationId}` angeben. Die stündlichen Vorhersagedaten können bis zu 48 stündliche Vorhersagen für jeden Standort enthalten. Wenn neue Daten empfangen werden, müssen Sie alle vorherigen stündlichen Vorhersagen für einen Standort löschen.|
|`GET /v1/{geocode or location ID}/forecast/daily/{format}.json`   |Gibt die tägliche Wettervorhersage für die nächsten 3, 5, 7 oder 10 Tage für angegebene Geoortungsdaten entsprechend dem von Ihnen angegebenen Format zurück. Die Anzahl der zurückgegebenen Tage wird im Format als `3day`, `5day`, `7day` oder `10day` angegeben. Sie können `geocode/{latitude}/{longitude}` oder `location/{locationId}` angeben. Jede Tagesvorhersage kann eine Tag- und eine Nachtvorhersage sowie eine 24-Stunden-Vorhersage enthalten. Diese Segmente sind separate Objekte in den JSON-Antworten. Vorhersagedaten für den Tag einer Tagesvorhersage stehen nach 15:00 Uhr Ortszeit nicht mehr zur Verfügung. Nach dieser Uhrzeit wird die Vorhersage für den Tag in Ihrer Anwendung
nicht mehr angezeigt.|
|`GET /v1/{geocode or location ID}/forecast/intraday/{format}.json`|Gibt die tägliche Wettervorhersage in 6-Stunden-Zeiträumen für die nächsten 3, 5, 7 oder 10 Tage für angegebene Geoortungsdaten entsprechend dem von Ihnen angegebenen Format zurück. Die Anzahl der zurückgegebenen Tage wird im Format als `3day`, `5day`, `7day` oder `10day` angegeben. Sie können `geocode/{latitude}/{longitude}` oder `location/{locationId}` angeben. Jede Tagesvorhersage kann eine Vorhersage für Vormittag, Nachmittag, Abend und Nacht enthalten. Diese Segmente sind separate Objekte in den JSON-Antworten.|
|`GET /v1/{geocode or location ID}/observations.json`              |Gibt die aktuellen Wetterbedingungen für eine Geoortung zurück. Sie können `geocode/{latitude}/{longitude}` oder `location/{locationId}` angeben. Diese aktuellen Beobachtungen werden in der Datenbank bis zu 10 Minuten bei bestimmten Berichtsstationen gespeichert. Ferner werden 24 Stunden der Beobachtungen pro Station gespeichert. Die aktuellen Beobachtungsdaten werden fortlaufend aktualisiert
und anhand der FIFO-Methode (Daten mit neuester Beobachtung austauschen und die alten Beobachtungen
in den Archivierungsspeicher verschieben) basierend auf den Datums-/Zeitangaben der Beobachtungen ersetzt.|
|`GET /v1/{geocode or location ID}/observations/timeseries.json`   |Gibt die aktuellen Beobachtungen
und bis zu 24 Stunden der letzten Beobachtungsdaten ausgehend vom aktuellen Zeitpunkt zurück. Sie können `geocode/{latitude}/{longitude}` oder `location/{locationId}` angeben. Wetterbeobachtungen werden von physischen Einheiten zusammengestellt,
die weltweit implementiert sind, sowie von den aktuellen Beobachtungen.|
|`GET /v1/{geocode, country code, state, or area}/alerts.json`      |Gibt Wetterbeobachtungen, Warnungen, Aussagen und Empfehlungen zurück, die vom National Weather Service (NWS), Environment Canada und MeteoAlarm (Europa) ausgegeben werden, und enthält die Übersetzung der Ereignisbeschreibung, des Ländernamens und der Warnungsüberschrift in 49 Sprachen. Sie können `geocode/{latitude}/{longitude}`, `country/{countrycode}`, `country/{countrycode}/state/{statecode}`/ oder `country/{countrycode}/area/{areaid}` angeben.|
|`GET /v1/alert/{detail_key}/details.json`                         |Gibt Wetterbeobachtungen, Warnungen, Aussagen und Empfehlungen zurück, die vom National Weather Service (NWS), Environment Canada und MeteoAlarm (Europa) ausgegeben werden. In den Details sind umfassendere Informationen zu der vom Wetteramt ausgegebenen Warnung für das jeweilige Gebiet enthalten sowie die Übersetzung der Ereignisbeschreibung, des Ländernamens und der Warnungsüberschriften in 49 Sprachen.|
|`GET /v1/{geocode or postal code}/almanac/daily.json`             |Gibt tägliche Almanach-Informationen zurück (nur USA), die aus Beobachtungsstationen des National Weather Service stammen und sich auf einen Zeitraum von 10 bis 30 Jahren oder mehr beziehen. Gesammelt und bereitgestellt werden die Informationen vom National Climatic Data Center (NCDC). Sie können `geocode/{latitude}/{longitude}` oder `location/{PostalLocationId}` angeben.|
|`GET /v1/{geocode or postal code}/almanac/monthly.json`           |Gibt monatliche Almanach-Informationen zurück (nur USA), die aus Beobachtungsstationen des National Weather Service stammen und sich auf einen Zeitraum von 30 Jahren oder mehr beziehen. Gesammelt und bereitgestellt werden die Informationen vom National Climatic Data Center (NCDC). Sie können `geocode/{latitude}/{longitude}` oder `location/{PostalLocationId}` angeben.|
|`GET /v3/location/{search or point}`                                  |Ermöglicht die Suche nach Standortnamen oder Geodaten (Längen- und Breitengrade), um einen Satz von Standorten abzurufen, die der Anforderung entsprechen. Der Standortservice unterstützt die Suche nach Städtenamen oder Postleitzahl.|
*Tabelle 1. {{site.data.keyword.weather_short}}-API-Zusammenfassung*

## Tages- und Tageszeitvorhersagen
{: #daily_intraday}
Die API für Tagesvorhersagen kann für jeden Standort mehrere Tage mit Tagesvorhersagen enthalten.
Jeder Tag einer Vorhersage kann bis zu drei einzelne Vorhersagen enthalten. Für jeden angegebenen Vorhersagetag kann die API Tages-, Nacht- und 24-Stunden-Vorhersagen zurückgeben.

Die API für tageszeitliche Vorhersagen kann für jeden Standort mehrere Tage mit Tagesvorhersagen enthalten.
Jeder Vorhersagetag enthält vier einzelne 6-Stunden-Vorhersagen für den Vormittag (7.00 bis 13.00 Uhr), den Nachmittag (13.00 bis 19.00 Uhr), den Abend (19.00 bis 1.00 Uhr) und die Nacht (1.00 bis 7.00 Uhr). Die tageszeitliche Vorhersage ist strukturell ähnlich gegliedert wie die Tagesvorhersage.

Jeder Abschnitt verfügt über eine Nummer für den Tagesabschnitt, einen Namen für den Wochentag und einen Namen für den Tagesabschnitt. Das folgende Beispiel zeigt die Datenfeldreihenfolge und die Datenwerte für `num` (Nummer), `dow` (Wochentag) und `daypart_name` (Name des Tagesabschnitts) für eine Vorhersage, die von den APIs an einem Donnerstagmorgen generiert wird:
* 1, Donnerstag, Vormittag
* 2, Donnerstag, Nachmittag
* 3, Donnerstag, Abend
* 4, Donnerstag, Nacht
* 5, Freitag, Vormittag
* 6, Freitag, Nachmittag
* 7, Freitag, Abend
* 8, Freitag, Nacht

## Aktuelle und Zeitreihenbeobachtungen
{: #time_series}

Die Daten zu aktuellen Wetterbedingungen und Zeitreihenbeobachtungen stellen Informationen zu Temperatur, Niederschlag, Wind, Luftdruck, Sichtweite, UV-Strahlung und andere zugehörige Beobachtungselemente bereit, darunter Beobachtungsstation, Datum/Uhrzeit der Beobachtungen, Wettersymbolcodes und Wetterbezeichnungen. Der Unterschied zwischen Zeitreihenbeobachtungen und aktuellen Beobachtungen liegt im Zeitraum
der Beobachtung, der zu einem oder mehreren Beobachtungsdatasets führt.

Die aktuellen Bedingungen entsprechen den aktuellen Beobachtungen für den Standort,
der ohne Zeitparameter abgerufen wird. Es wird ein Dataset zurückgegeben. Die Zeitreihenbeobachtungen
enthalten zurückliegende Beobachtungen während eines bestimmten Zeitraums
bis einschließlich der letzten 24 Stunden für den angeforderten Standort.

Aktuelle Beobachtungen werden in der primären Datenbank bis zu 48 Stunden
(zwei Tage) für bestimmte Berichtsstationen aufbewahrt. Die aktuellen Beobachtungsdaten
werden dabei fortlaufend aktualisiert und anhand der FIFO-Methode (Daten mit neuester
Beobachtung austauschen und die alten Beobachtungen in den Archivierungsspeicher verschieben)
basierend auf den Datums-/Zeitangaben der Beobachtungen ersetzt. Das Datenvolumen, das aufbewahrt
wird und von einer Station verfügbar ist, kann mehr als 24 einzelne Beobachtungsberichte umfassen. Die Anzahl der Beobachtungen wird durch den Typ
der entsprechenden Beobachtung festgelegt.

## Wetterwarnungen - Überschriften und Details
{: #alerts_levels}
Die Warn-APIs geben Überschriften zu aktiven Wetterwarnungen zurück, die sich auf schwere Gewitter, Tornados, Erdbeben oder Überschwemmungen beziehen.
Diese APIs geben auch nicht wetterbezogene Warnungen zurück, z. B. zu Kindesentführungen oder Strafverfolgung.

**Hinweis**: Diese API steht nur in den Vereinigten Staaten, Kanada und Europa zur Verfügung.

Die API für Warnungsüberschriften stellt im Attribut `detail_key` einen Schlüsselwert bereit, mit dem auf die Warnungsdetails in der API für Warnungsdetails zugegriffen werden kann.
Die API für Warnungsüberschriften kann abgefragt werden, um den Wert `detail_key` abzurufen. Anschließend kann die Antwort der API für Warnungsüberschriften mit dem `detail_key` abgerufen werden.

**Hinweis**: Sie müssen die Datenquellen-Attribution für alle Warnungsdaten anzeigen, die in Ihrer Anwendung angezeigt werden.

Die Attributions-Phrase muss folgende Informationen anzeigen:

*Ausgegeben von <Name der Behörde> - &lt;Code des regionalen Wetteramts&gt;, &lt;Code des nationalen Wetteramts&gt;, &lt;Quelle&gt;, &lt;Haftungsausschluss&gt;*

Beispiel:
* Ausgegeben vom Nationalen Wetterdienst (NWS), Bismarck, USA
* Ausgegeben von der Zentralanstalt für Meteorologie und Geodynamik (ZAMG), Österreich, EMETNET-Meteoalarm

## Almanach-Informationen
{: #almanac_details}
Die Almanach-API erfordert eine Standort-ID und einen Standorttyp (Stadt oder Postleitzahl) oder ein Breiten- und Längengradpaar zum Abrufen der Informationen für einen bestimmten Standort.

Wenn Sie `location` in der URL verwenden, muss der Standort eine Standort-ID (Postleitzahl) mit einem Standorttyp und einem Landescode enthalten. Wenn Sie `geocode` in der URL verwenden, muss der Suchstandort eine gültige Kombination aus Breiten- und Längengrad sein.

Die Almanach-API verwendet Parameter, um entweder Tages- oder Monatsdaten, ein bestimmtes Datum oder einen Datumsbereich von Informationen sowie die Maßeinheiten anzugeben, in denen die Daten zurückgegeben werden sollen.

Die Datumsparameter sind `start` und `end`. Der Parameter `start` ist erforderlich, der Parameter `end` ist optional. Werden die Parameter zusammen verwendet, so gibt die Kombination einen Datenbereich anstelle der Daten eines bestimmten Monats oder Tages zurück.

Das Datumsformat für den Abruf von Ergebnissen des Tagesalmanachs ist ein 4-stelliger numerischer Wert, der Monat und Tag für das angeforderte Datum, also MMTT, darstellt. Einstelligen Tagen **muss** eine Null vorangestellt werden, z. B. '01'.

Das Datumsformat für den Abruf des Monatsalmanachs ist 'Monat', also 'MM'. Einstelligen Monaten **muss** eine Null vorangestellt werden, z. B. '01'. Jedes andere Format führt zu einem API-Fehler und es werden keine Daten zurückgegeben.

**Hinweis**: Wenn Sie in der Anforderung keinen Datumswert angeben, gibt das System den Status 404 (fehlerhafte Anforderung) zurück. Die API gibt keinen Standardwert an.

## Aufbau der URLs
{: #url_construction}

Die REST-APIs verwenden zum Abrufen und Filtern von Wetterdaten eine allgemeine URL-Struktur und Abfrageparameter.
Die URLs, die an die APIs übergeben werden, sind folgendermaßen aufgebaut:

```
https://twcservice.mybluemix.net/api/weather/v1/geocode/<latitude>/<longitude>/<product group>/<date>/<format>&units={units code}&language={language code}
```

Beispiel:

```
https://twcservice.mybluemix.net/api/weather/v1/geocode/33.40/83.42/forecast/daily/3day.json?units=m&language=en-US
```

|**Attribut**     |**Beschreibung**                                    |
|------------------|---------------------------------------------------|
|`hostname`        |Der gehostete URL-Pfad. Beispiel: `https://twcservice.mybluemix.net:443/api/weather`.|
|`version`         |Die aktuelle Iteration. Beispiel: "v1".|
|`location`        |Der Geocode oder die Standort-ID. Die Standortgruppe kann "geocode" oder "location" sein. "geocode/45.4214/75.6919" stellt beispielsweise Ottawa in Kanada dar. Wenn Sie eine geocodierte Koordinate angeben, gibt die API Daten für den Standort zurück,
der dieser Koordinate am nächsten liegt. Punkte werden als Dezimaltrennzeichen und Kommas
zum Trennen von Breitengrad- und Längengradwerten verwendet. Wenn Sie einen Geocode bereitstellen,
werden die tatsächlich verwendeten Werte für Breitengrad und Längengrad in den Metadaten der
Antwort zurückgegeben.|
|`product group`   |Das Produkt. Beispiel: "observations" oder "forecast". Eine Produkt-Untergruppe, z. B. "historical", ist optional.|
|`date`            |Der Datumstyp. Beispiel: "daily" oder "monthly".|
|`format`          |Das Format. Beispiel: "3day", "5day", "7day" oder "10day".|
|`units`           |Die optionale Einheit, in der die Antwort zurückgegeben werden soll. Die API
unterstützt die Maßeinheiten 'English' (e), 'Metric' (m) und 'UK-Hybrid' (h). Wenn Sie die Maßeinheiten angeben, nicht jedoch einen Wert, gibt die API die Daten
in der Maßeinheit zurück, die dem Sprachencode entspricht. Die Standardeinheit oder
die angeforderte Einheit wird im Maßeinheitsparameter (units) in den Metadaten
der Antwort zurückgegeben.|
|`language`        |Die Sprache, in der die Antwort zurückgegeben werden soll. Der Standardwert ist 'en-US'. Die Standardsprache oder die angeforderte Übersetzungssprache wird im Sprachparameter (language)
in den Metadaten der Antwort zurückgegeben.|
*Tabelle 2. URL-Details*

**Hinweis**: Die REST-APIs verwenden für Landescodes die Norm ISO 3166. Weitere Informationen finden Sie auf der [Online-Suchplattform für ISO-Normen](https://www.iso.org/obp/ui/#search/code/){:new_window}.
Die APIs verwenden das Geocode-Koordinatenbezugssystem WGS84. Weitere Informationen finden Sie im [Geo-Basisglossar](https://www.w3.org/2003/01/geo/){:new_window}.

## Maßeinheiten
{: #units_measure}

Wenn Sie die REST-APIs verwenden, müssen Sie nicht explizit eine Maßeinheit übergeben. Die APIs übernehmen als Standard die Maßeinheit, die mit dem Sprachencode in der URL verbunden ist. Wenn Sie jedoch eine andere Maßeinheit als die Standardeinheit angeben möchten,
können Sie eine Maßeinheit übergeben, die die Standardeinheit überschreibt.

* Für 'en-US' oder 'en' lautet der Code der Standardmaßeinheit 'English/Imperial'. Der Einheitencode ist "e".
* Für 'en-GB' ist die Standardmaßeinheit 'Hybrid-UK'. Der Einheitencode ist "h".
* Für alle anderen Sprachen ist die Standardmaßeinheit 'Metric'. Der Einheitencode ist "m".

## Sprachkonvertierung
{: #language_translation}

Die REST-APIs übersetzen die Bezeichnungen und Maßeinheiten. Wenn Sie eine Anforderungs-URL formatieren,
müssen Sie eine gültige Sprache angeben.
Die folgenden Fehler werden übersetzt:

|**Feld**           |**Beschreibung**                                    |
|--------------------|---------------------------------------------------|
|`narrative`         |Die beschreibende Vorhersage für den 24-Stunden-Zeitraum|
|`dow`               |Wochentag|
|`wind_phrase`       |Die Beschreibung der Windrichtung und der Windgeschwindigkeit für eine 12-stündige Tageseinteilung|
|`wdir_cardinal`     |Durchschnittliche Windrichtung am Tag in Kardinalzahlschreibweise|
|`daypart_name`      |Der Name eines Tagesabschnitts von 12 Stunden (darin nicht enthalten die Namen der Tage in den ersten 48 Stunden)|
|`temp_phrase`       |Die Kurzbeschreibung, die die vorhergesagte Höchst- oder Tiefsttemperatur für den 12-stündigen Vorhersagezeitraum enthält|
|`shortcast`         |Ein abgekürzter Teil einer beschreibenden Vorhersage|
|`long_daypart_name` |Der benannte Zeitrahmen für die gültige Wettervorhersage in einem erweiterten Format. Der benannte Zeitrahmen kann entweder für einen
12-Stunden- oder einen 24-Stunden-Zeitrahmen gelten.|
|`golf_category`     |Die Indexkategorie 'Golf', die als Bezeichnung für die Wetterbedingungen für das Golfspielen ausgedrückt wird|
|`phrase_nnchar`     |Sinnvolle Wetterbezeichnung für den Tag|
|`lunar_phrase`      |Kurzcode aus drei Zeichen für Mondphasen|
|`uv_desc`           |Beschreibung für den UV-Index, die den Wert
für den UV-Index durch die Bereitstellung der zugehörigen Risikostufe für die Haut durch Sonneneinstrahlung ergänzt|
|`wx_phrase`         |Eine Textbeschreibung der beobachteten Wetterbedingungen an der Berichtsstation.|
|`pressure_desc`     |Eine Phrase, die die veränderten Messwerte für den Luftdruck im Verlauf der letzten Stunde beschreibt.|
|`headline_text`     |Der Text der Überschrift eines Ereignisses für den Standort.|
|`event_desc`        |Eine Beschreibung des Ereignisses.|
|`cntry_name`        |Der Name des Landes, in dem das Ereignis auftrat, in Groß- und Kleinschreibung.|
*Tabelle 3. Übersetzte Antwortfelder*

## Verarbeitung von Datenfeldern mit Nullwerten oder fehlenden Datenfeldern in API-Antworten
{: #handling_null_or_missing}

Wenn ein Datenfeld null ist, weil die Daten nicht verfügbar sind, geben die REST-APIs entweder die entsprechenden Feldtags mit dem Wort "null" zurück oder sie geben das Feld überhaupt nicht zurück.

## Handhabung von Fehlern
{: #handling_errors}

Die folgenden Fehlercodes sind allen APIs gemeinsam:

|**Fehler** |**Beschreibung**                                    |
|----------|---------------------------------------------------|
|400       |Fehlerhafte Anforderung. Die Anforderung wurde vom Server aufgrund einer fehlerhaften
Syntax nicht verstanden. Dieser Fehlercode wird für alle APIs implementiert. Die API lehnt die Anforderung ab, wenn ungültige Parameter angegeben werden.|
|401       |Nicht autorisiert. Für die Anforderung ist eine Authentifizierung erforderlich.|
|403       |Nicht zulässig. Der Server hat die Anforderung verstanden, lehnt eine Verarbeitung jedoch ab.|
|404       |Nicht gefunden. Wenn in der API-Anforderung ein erforderlicher Parameter nicht vorhanden ist, wird der Fehler "MissingParameterException" mit dem Fehlercode 404 zurückgegeben.|
|500       |Interner Serverfehler. Der Server hat eine nicht erwartete Bedingung erkannt,
die ihn daran gehindert hat, die Anforderung zu verarbeiten.|
*Tabelle 4. Fehlerantwortcode*

Die Antwort bei einem Fehler ist immer gleich. In einer Antwort können mehrere Fehlercodes zurückgegeben werden.
Eine JSON-Fehlerantwort kann beispielsweise folgendermaßen zurückgegeben werden:

```
{
  metadata: {
    transaction_id: "1411496413365:-1880721071"
  },
  success: false,
  errors: [
    {
      error: {
        code: "NDF-0001",
        message: "There was no data found for your product query."
      }
    }
}
```
