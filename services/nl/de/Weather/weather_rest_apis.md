---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# REST-APIs von Insights for Weather verwenden
{: #rest_apis}

*Letzte Aktualisierung: 6. April 2016*

Sie können die [REST-APIs von Insights for Weather](https://twcservice.{APPDomain}/rest-api/){:new_window} verwenden, um Wetterdaten abzurufen. Sie können API-Operationen testen und sofort die Ergebnisse anzeigen, um so Ihre Anwendungen schneller erstellen zu können.

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

Mit den APIs von Insights for Weather können Sie durch die Angabe von Koordinaten für Breiten- und Längengrade Wetterdaten abrufen.
Sie können die folgenden APIs verwenden.

|**API**                                  |**Beschreibung**              |
|-----------------------------------------|-----------------------------|
|`GET /v2/forecast/daily/10day`           |Gibt Wettervorhersagen für den aktuellen Tag und die nächsten neun Tage für eine Geoortung zurück. Jede Tagesvorhersage kann eine Tag- und eine Nachtvorhersage enthalten. Diese Segmente sind separate Objekte in den JSON-Antworten. Vorhersagedaten für den Tag einer Tagesvorhersage stehen nach 15:00 Uhr Ortszeit nicht mehr zur Verfügung. Nach dieser Uhrzeit wird die Vorhersage für den Tag in Ihrer Anwendung
nicht mehr angezeigt.|
|`GET /v2/forecast/hourly/24hour`         |Gibt eine stündliche Vorhersage für den aktuellen Tag und die nächsten 24 Stunden für eine Geoortung zurück. Die stündlichen Vorhersagedaten können bis zu 24 stündliche Vorhersagen für jeden Standort enthalten. Wenn neue Daten empfangen werden, müssen Sie alle vorherigen stündlichen Vorhersagen für einen Standort löschen.|
|`GET /v2/observations/current`           |Gibt die aktuellen Wetterbedingungen für eine Geoortung zurück. Diese aktuellen Beobachtungen werden in der Datenbank bis zu 10 Minuten bei bestimmten Berichtsstationen gespeichert. Ferner werden 24 Stunden der Beobachtungen pro Station gespeichert. Die aktuellen Beobachtungsdaten werden fortlaufend aktualisiert
und anhand der FIFO-Methode (Daten mit neuester Beobachtung austauschen und die alten Beobachtungen
in den Archivierungsspeicher verschieben) basierend auf den Datums-/Zeitangaben der Beobachtungen ersetzt.|
|`GET /v2/observations/timeseries/24hour` |Gibt die aktuellen Beobachtungen
und bis zu 24 Stunden der letzten Beobachtungsdaten ausgehend vom aktuellen Zeitpunkt zurück. Wetterbeobachtungen werden von physischen Einheiten zusammengestellt,
die weltweit implementiert sind, sowie von den aktuellen Beobachtungen.|
*Tabelle 1. Insights for Weather API-Zusammenfassung*

## Zeitreihenbeobachtungen
{: #time_series}

Die Zeitreihenbeobachtungsdaten stellen Informationen zu Temperatur, Niederschlag, Wind,
Luftdruck, Sichtweite, UV-Strahlung und andere zugehörige Beobachtungselemente bereit, darunter
Beobachtungsstation, Datum/Uhrzeit der Beobachtungen, Wettersymbolcodes und Wetterbezeichnungen. Der Unterschied zwischen Zeitreihenbeobachtungen und aktuellen Beobachtungen liegt im Zeitraum
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

## Aufbau der URLs
{: #url_construction}

Die Insights for Weather-APIs verwenden
zum Abrufen und Filtern von Wetterdaten eine allgemeine URL-Struktur und verschiedene Abfrageparameter.
Die URLs, die an die Insights for Weather-APIs übergeben wurden, sind folgendermaßen aufgebaut:

```
https://twcservice.mybluemix.net/api/weather/v2/<product group>/&format={format type}&geocode={latitude,longitude}&language={language code}&units={units code}

```

|**Attribut**     |**Beschreibung**                                    |
|------------------|---------------------------------------------------|
|`hostname`        |Der per Hosting bereitgestellte URL-Pfad (z. B.
`https://twcservice.mybluemix.net:443/api/weather`)|
|`version`         |Die aktuelle Iteration (z. B. "v2")|
|`product group`   |Das Produkt (z. B. "observations" oder "forecast")|
|`geocode`         |Der optionale Breiten- und Längengrad. Zum Beispiel lauten die Daten für Ottawa in Kanada "45.4214,75.6919". Wenn Sie eine geocodierte Koordinate angeben, gibt die API Daten für den Standort zurück,
der dieser Koordinate am nächsten liegt. Punkte werden als Dezimaltrennzeichen und Kommas
zum Trennen von Breitengrad- und Längengradwerten verwendet. Wenn Sie einen Geocode bereitstellen,
werden die tatsächlich verwendeten Werte für Breitengrad und Längengrad in den Metadaten der
Antwort zurückgegeben.|
|`language`        |Die Sprache, in der die Antwort zurückgegeben werden soll. Der Standardwert ist 'en-US'. Die Standardsprache oder die angeforderte Übersetzungssprache wird im Sprachparameter (language)
in den Metadaten der Antwort zurückgegeben.|
|`units`           |Die optionale Einheit, in der die Antwort zurückgegeben werden soll. Die API
unterstützt die Maßeinheiten 'English' (e), 'Metric' (m) und 'UK-Hybrid' (h). Wenn Sie die Maßeinheiten angeben, nicht jedoch einen Wert, gibt die API die Daten
in der Maßeinheit zurück, die dem Sprachencode entspricht. Die Standardeinheit oder
die angeforderte Einheit wird im Maßeinheitsparameter (units) in den Metadaten
der Antwort zurückgegeben.|
*Tabelle 2. URL-Details*

## Maßeinheiten
{: #units_measure}

Wenn Sie die Insights for Weather-APIs verwenden, müssen Sie nicht explizit eine Maßeinheit übergeben. Die Insights for Weather-APIs übernehmen als Standard die Maßeinheit, die mit dem Sprachencode in der URL verbunden ist. Wenn Sie jedoch eine andere Maßeinheit als die Standardeinheit angeben möchten,
können Sie eine Maßeinheit übergeben, die die Standardeinheit überschreibt.

* Für 'en-US' oder 'en' lautet der Code der Standardmaßeinheit 'English/Imperial'. Der Einheitencode ist "e".
* Für 'en-GB' ist die Standardmaßeinheit 'Hybrid-UK'. Der Einheitencode ist "h".
* Für alle anderen Sprachen ist die Standardmaßeinheit 'Metric'. Der Einheitencode ist "m".

## Sprachkonvertierung
{: #language_translation}

Die Insights for Weather-APIs übersetzen die Bezeichnungen und Maßeinheiten. Wenn Sie eine Anforderungs-URL formatieren,
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
|`sky_cover`         | Beschreibung der Bewölkungssituation in Abhängigkeit von der Wolkendecke (in Prozent)|
|`ptend_desc`        | Beschreibender Text der Luftdrucktendenz während der letzten drei Stunden|
*Tabelle 3. Übersetzte Antwortfelder*

## Verarbeitung von Datenfeldern mit Nullwerten oder fehlenden Datenfeldern in API-Antworten
{: #handling_null_or_missing}

Wenn ein Datenfeld null ist, da die Daten nicht verfügbar sind, geben die Insights for Weather-APIs entweder
die entsprechenden Feldtags mit dem Wort "null" zurück oder sie geben das Feld überhaupt nicht zurück.

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
|405       |Methode nicht zulässig. Beispiel: Anstelle einer GET-Anforderung wird eine POST-Anforderung gesendet.|
|406       |Nicht zulässig. Beispiel: Mit GZIP komprimierte Antworten werden nicht akzeptiert.|
|408       |Zeitlimitüberschreitung für Anforderung. Der Client hat in dem Zeitrahmen,
in dem der Server gewartet hat, keine Anforderung gesendet.|
|500       |Interner Serverfehler. Der Server hat eine nicht erwartete Bedingung erkannt,
die ihn daran gehindert hat, die Anforderung zu verarbeiten.|
|502 - 504   |Service nicht verfügbar oder Gateway-Fehler. Diese Fehlercodes werden zurückgegeben,
wenn der Service vorübergehend nicht verfügbar ist.|
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
