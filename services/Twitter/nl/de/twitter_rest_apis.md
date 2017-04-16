---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Verwendung der Insights for Twitter-REST-APIs
{: #rest_apis}

Der {{site.data.keyword.twittershort}}-Service verfügt über REST-konforme APIs, um den Twitter-Inhalt zu durchsuchen und zu nutzen. In der Tabelle zur [Abfragesprache](twitter_rest_apis.html#querylanguage){: new.window} sind die Abfragebegriffe aufgeführt, die von den Service-APIs unterstützt werden. Es werden Beispiele bereitgestellt, um zu veranschaulichen, wie Abfragen erstellt werden können.
{:shortdesc}

## REST-API-Dokumentation {: #rest_api}
Die REST-API-Dokumentation wurde mithilfe von Swagger erstellt; dadurch haben Sie die Möglichkeit, API-Operationen zu testen und die Ergebnisse unmittelbar anzuzeigen, um so Ihre Anwendungen ohne zeitliche Verzögerung erstellen zu können.
Derzeit sind die folgenden API-Operationen verfügbar:

* Search: Es wird nach Tweets im Decahose-Stream oder im gefilterten PowerTrack-Stream gesucht.
* Count: Auf der Grundlage einer angegebenen Abfrage wird eine Anzahl von Tweets zurückgegeben.
* Check: Es wird festgestellt, ob eine Liste mit Nachrichten den Twitter-Richtlinien und Twitter-Benutzern entspricht.
* Tracks: Stellt Benutzern des Einstiegsplans eine Reihe von Endpunkten für die Verwaltung von PowerTrack-Filtern zur Verfügung.

Weitere Informationen zu den unterstützten REST-APIs und den zugehörigen Ressourcen finden Sie in der [REST-API-Referenz](https://cdeservice.{APPDomain}/rest-api/){: new_window}. Wählen Sie die Region aus, in der sich Ihre Anwendung befindet. Jede Region ist unabhängig; es ist nicht möglich, Serviceberechtigungsnachweise, die Sie in einer Region erhalten haben, für die Authentifizierung bei einem Service in einer anderen Region zu verwenden.

Klicken Sie in der Referenzdokumentation auf **Operationen auflisten**, um Details zu den einzelnen Operationen anzuzeigen. Wenn Sie auf **Ausprobieren** geklickt haben, werden Sie möglicherweise zur Angabe von Berechtigungsnachweisen aufgefordert. Sie müssen den Benutzernamen und das Kennwort aus Ihren **VCAP_SERVICES**-Umgebungsvariablen angeben. Diese Informationen erhalten Sie, wenn Sie Ihre Anwendung öffnen und im Inhaltsverzeichnis auf die Option **Umgebungsvariablen** klicken.

**Anmerkung**: Ein Fehler bei der Eingabe der korrekten Berechtigungsnachweise führt zu einer Nachricht des Typs "Unauthorized" im Antworthauptteil.

**Wichtig**: Aktive Tracks, die mit dem Feature **Ausprobieren** erstellt werden, erfassen Tweets aus Twitter, die auf Ihr monatliches Kontingent angerechnet werden. Wenn Tracks nicht mehr benötigt werden, ändern Sie deren Status in **inaktiv** oder löschen Sie sie.


## Abfragesprache {: #querylanguage}

Mithilfe von {{site.data.keyword.twittershort}} können Sie unter Verwendung zahlreicher Abfrageparameter und Filter den Twitter-Inhalt durchsuchen, um genauere Ergebnisse zu erzielen.

Sie können für Ihre Abfragen die folgenden booleschen Operatoren verwenden. 

| **Operator**        | **Beschreibung**                                                                                                                   | **Beispiele**      |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------|-------------------|
| term1 **AND** term2 | Es werden Tweets zurückgegeben, die sowohl 'term1' als auch 'term2' enthalten. Leerzeichen zwischen zwei Begriffen werden als AND (und) behandelt; der Operator kann daher weggelassen werden. | `#ibm twitter`      |
| term1 **OR** term2  | Es werden Tweets zurückgegeben, die entweder 'term1' oder 'term2' enthalten.    | `#money OR revenue` |
| -term1              | Es werden Tweets zurückgegeben, die 'term1' nicht enthalten.  |`ibm -apple`  |

*Tabelle 1. Boolesche Operatoren*

Vorrangstellung für Operatoren: "-" hat Vorrang vor "AND" und "AND" hat Vorrang vor "OR". Für eine explizite Vorrangstellung der Operatoren müssen Sie runde Klammern verwenden. Beispiel: Mit `large animals` -(`giraffes` OR `bears`) wird nach Tweets gesucht, die die Begriffe "large" und "animals" enthalten; Tweets mit den Begriffen "giraffes" und "bears" werden dagegen ausgeschlossen.

In der folgenden Tabelle werden die derzeit unterstützten Abfragebegriffe aufgeführt.

| **Begriff** 	| **Beschreibung** 	| **Beispiele** 	|
|----------------------------------------------	|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|---------------------------------------------	|
| Schlüsselwort 	| Eine Übereinstimmung mit Tweets, die in Ihrem Hauptteil das Schlüsselwort enthalten. Bei der Suche wird die Groß-/Kleinschreibung beachtet. 	| Analytics 	|
| "exact phrase match" 	| Eine Übereinstimmung mit Tweets, die die genaue Schlüsselwortreihenfolge enthalten. 	| "IBM and analytics" 	|
| `#hashtag` 	| Eine Übereinstimmung mit Tweets mit dem Hashtag *#hashtag*. 	| `#insight2015` 	|
| `bio_lang:language` 	| Eine Übereinstimmung mit Tweets von Benutzern, deren Profilspracheneinstellungen dem angegebenen Sprachencode entsprechen.  Unter `lang:` finden Sie eine Liste der unterstützten Sprachen. 	| `bio_lang:en` 	|
| `bio_location:"location"` 	| Eine Übereinstimmung mit Tweets von Benutzern, deren Profilpositionseinstellung die angegebene Referenz für `location` enthält. 	| `bio_location:"New York"` 	|
| `country_code:country-code` 	| Eine Übereinstimmung mit Tweets, deren Orts- oder Positionstags dem angegebenen Landescode entsprechen. </br>**Eine Liste der unterstützten Landescodes finden Sie in **https://de.wikipedia.org/wiki/ISO-3166-1-Kodierliste 	| `country_code:us` 	|
| `followers_count: lowerLimit,upperLimit` 	| Eine Übereinstimmung mit Tweets von Benutzern mit einer bestimmten Anzahl an Followern, die innerhalb des angegebenen Bereichs liegt. Die Obergrenze ist optional und beide Grenzwerte werden eingeschlossen. 	| `followers_count:500` 	|
| `friends_count: lowerLimit,upperLimit` 	| Eine Übereinstimmung mit Tweets von Benutzern, die einer bestimmten Anzahl an Benutzern folgen, die innerhalb des angegebenen Bereichs liegt. Die Obergrenze ist optional und beide Grenzwerte werden eingeschlossen. 	| `friends_count:1000,3000` 	|
| `from:twitterHandle` 	| Eine Übereinstimmung mit Tweets von Benutzern mit dem bevorzugten Benutzernamen *twitterHandle*. Das Symbol &commat; darf nicht enthalten sein. 	| `from:alexlang11` 	|
| `has:children` 	| Eine Übereinstimmung mit Tweets von Benutzern mit Kindern. 	| `has:children` 	|
| `is:married` 	| Eine Übereinstimmung mit Tweets von Benutzern, die verheiratet sind. 	| `is:married` 	|
| `is:verified` 	| Eine Übereinstimmung mit Tweets, deren Verfasser von Twitter verifiziert wurde. 	| `analytics is:verified` 	|
| `lang:language-code` 	| Eine Übereinstimmung mit Tweets einer bestimmten Sprache. Im Folgenden sind die unterstützten Sprachencodes aufgeführt: <ul><li>`ar` (Arabisch)</li><li>`zh` (Chinesisch)</li><li>`da` (Dänisch)</li><li>`dl` (Niederländisch)</li><li>`en` (Englisch)</li><li>`fi` (Finnisch)</li><li>`fr` (Französisch)</li><li>`de` (Deutsch)</li><li>`el` (Griechisch)</li><li>`he` (Hebräisch)</li><li>`id` (Indonesisch)</li><li>`it` (Italienisch)</li><li>`ja` (Japanisch)</li><li>`ko` (Koreanisch)</li><li>`no` (Norwegisch)</li><li>`fa` (Persisch)</li><li>`pl` (Polnisch)</li><li>`pt` (Portugiesisch)</li><li>`ru` (Russisch)</li><li>`es` (Spanisch)</li><li>`sv` (Schwedisch)</li><li>`th` (Thailändisch)</li><li>`tr` (Türkisch)</li><li>`uk` (Großbritannien)</li></ul>    | `lang:de` (für die Übereinstimmung mit deutschen Tweets) 	|
| `listed_count: lowerLimit,upperLimit` 	| Eine Übereinstimmung mit Tweets, deren Autor in der Twitter-Liste innerhalb des angegebenen Bereichs aufgeführt ist. Die Obergrenze ist optional und beide Grenzwerte werden eingeschlossen. 	| `listed_count:1000,3000` 	|
| `point_radius:[longitude latitude radius]` 	| Eine Übereinstimmung mit Tweets einer bestimmten geografischen Region, die durch den Längen- und Breitengrad sowie einen Radius angegeben wird. </br></br>Alle Koordinaten werden in Dezimalgraden angegeben. Der Wert für `longitude` muss zwischen -180 und +180 liegen, der Wert für `latitude` zwischen -90 und +90. Bei einem Wert außerhalb des unterstützten Bereichs wird ein Fehler zurückgegeben. Die Werte müssen als Gleitkommazahlen eingegeben werden; ganze Zahlen werden nicht unterstützt. </br></br>Der Radius der Umgebung muss in Meilen (mi) oder Kilometern (km) angegeben werden. 	| `point_radius:[41.128611 -73.707778 5.0mi]` 	|
| `posted:startTime  posted:startTime,endTime` 	| Eine Übereinstimmung mit Tweets, die zur Startzeit "startTime" oder danach gepostet wurden. Die Endzeit (endTime) ist optional und beide Grenzwerte werden eingeschlossen. Zeitmarken müssen eines der folgenden Formate aufweisen:  </br>"yyyy-mm-dd" oder "yyyy-mm-ddTHH:MM:SSZ" </br>  Die Zeitzone basiert auf der koordinierten Weltzeit (UTC). Bei der Angabe von Stunden, Minuten und Sekunden muss die Zeit dem vorgeschriebenen Format entsprechend in "T" und "Z" eingeschlossen werden. 	| `posted:2014-12-01,2014-12-12` 	|
| `sentiment:sentiment-value` 	| Eine Übereinstimmung mit Tweets mit einer bestimmten Stimmung. Die folgenden Werte werden unterstützt: </br><dl>positive</dl> <dlentry>Tweet enthält mehr positive als negative Stimmungsausdrücke.</dlentry> </br></br><dl>negative</dl> <dlentry>Tweet enthält mehr negative als positive Stimmungsausdrücke.</dlentry>  </br></br><dl>neutral</dl>  <dlentry>Der Tweet ist frei von jeglicher Stimmung oder ist in einer Sprache verfasst, für keine Stimmungserkennung angeboten wird.</dlentry> </br></br><dl>ambivalent</dl>  <dlentry>Der Tweet enthält gleich viele positive wie negative Stimmungsausdrücke.</dlentry> 	| `sentiment:positive` 	|
| `statuses_count: lowerLimit,upperLimit` 	| Eine Übereinstimmung mit Tweets von Benutzern, die eine bestimmte Anzahl von Statusangaben gepostet haben, die innerhalb des angegebenen Bereichs liegt. Die Obergrenze ist optional und beide Grenzwerte werden eingeschlossen. 	| `statuses_count:1000,3000` 	|
| `time_zone:timeZone` 	| Eine Übereinstimmung mit Tweets von Benutzern, deren Profileinstellungen der angegebenen Zeitzone entsprechen. 	| `time_zone:"Eastern Time (US & Canada)"` 	|
| `time_zone:city` 	| Eine Übereinstimmung mit Tweets von Benutzern, deren Profileinstellungen der angegebenen Stadt entsprechen. 	| `time_zone:"Dublin"` 	|
*Tabelle 2. Abfragebegriffe*

Alle unterstützten Abfragebegriffe können mit den zuvor beschriebenen booleschen Operatoren kombiniert werden. Beispiel:

`ibm -apple followers_count:500`
