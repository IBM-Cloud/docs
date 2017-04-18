---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Decahose- und PowerTrack-Streams {: #decahose_powertrack}

{{site.data.keyword.twittershort}} bietet Zugriff auf den Twitter Decahose- und den Twitter PowerTrack-Stream auf der Basis der {{site.data.keyword.Bluemix_notm}}-Planregistrierung. 
Beide Streams liefern Echtzeitfeeds und weisen unterschiedliche Merkmale auf, die den jeweiligen Anforderungen entsprechen.
{:shortdesc}

Der Decahose-Stream ist eine zufällige 10%ige Stichprobe von Twitter Firehose. Tweets werden in Echtzeit aus Twitter abgeleitet und der Stream wird durch die Abtastalgorithmen von Twitter bestimmt. Für die meisten statistischen Analysen bietet eine zufällige 10%ige Stichprobe ausreichende Genauigkeit. Decahose-Daten sind für einen Zeitraum von zwei Jahren indexiert; daher werden durch Abfrageantworten möglicherweise keine Tweets zurückgegeben, die älter als zwei Jahre sind. Zugriff auf den Decahose-Stream ist im Rahmen des Plans für die kostenfreie Suche und im Rahmen des Einstiegsplans verfügbar, Zugriff auf den PowerTrack-Stream nur im Rahmen des Einstiegsplans.

Der PowerTrack-Stream bietet den zusätzlichen Vorteil, dass eingehende Tweets auf der Basis eines benutzerdefinierten regelbasierten Filters, des sogenannten Tracks, gefiltert werden können. Im Rahmen des Einstiegsplans können Benutzer bis zu 1000 Regeln pro Konto erstellen. Für eine erweiterte Filterung können mehrere Tracks in einem aggregierten Track kombiniert werden. Die folgenden Abschnitte enthalten Beschreibungen für Trackstatus, Eigenschaften und unterstützte Aktionen,
die für Tracks ausgeführt werden können, wie z. B. Bearbeiten, Löschen usw.

**Anmerkung**: Das Indexieren des PowerTrack-Streams ist auf 1 Million Tweets pro Kalendermonat begrenzt. Sobald das Limit erreicht ist, wird die Indexierung für den Monat gestoppt. Zu Beginn des nächsten Monats können Sie die Tracks reaktivieren; sie werden nicht automatisch aktiviert. Für eine optimale Nutzung des Streams wird das korrekte Management der Tracks unbedingt empfohlen. So können beispielsweise redundante Tracks inaktiviert werden.

## Tracktypen {: #track_types}

Im Rahmen des Einstiegsplans können Benutzer anpassbare Tracks erstellen, mit denen Nachrichten gefiltert werden können, die im PowerTrack-Datenstream erfasst werden.  {{site.data.keyword.twittershort}} unterstützt die beiden folgenden Tracktypen.

<dl>
<dt>Regelbasiert</dt>
<dd>Alle in diesem Track erfassten Nachrichten entsprechen mindestens einer der Regeln, die dem Track zugeordnet sind. Sie können in diesem Tracktyp Regeln hinzufügen, bearbeiten und löschen.

Die vollständige [GNIP-PowerTrack-Regelsyntax](http://support.gnip.com/apis/powertrack2.0/rules.html) wird in regelbasierten Tracks unterstützt. Alle Abfragen müssen der {{site.data.keyword.twittershort}}-[Abfragesprache](twitter_rest_apis.html#querylanguage "Abfragesprache") entsprechen.
</dd>

<dt>Aggregiert</dt>
<dd>Eine Kombination aus zwei oder mehr regelbasierten oder aggregierten Tracks. Mit aggregierten Tracks können mehrere Tracks beliebig gruppiert werden. Sie können einzelne Tracks zu einem aggregierten Tracktyp hinzufügen oder aus diesem löschen. Zu aggregierten Tracks können keine einzelnen Regeln hinzugefügt werden; verwenden Sie zu diesem Zweck stattdessen einen regelbasierten Track. Aggregierte Tracks weisen keinen Status auf, die beteiligten regelbasierten Tracks befinden sich jedoch im Status **Aktiv** oder **Inaktiv**.</dd>
</dl>

## Trackeigenschaften {: #track_properties}
Tracks enthalten die folgenden Eigenschaften. Nicht alle Eigenschaften gelten sowohl für regelbasierte als auch für aggregierte Tracks. Die Eigenschaft 'rules' ist beispielsweise nicht für aggregierte Tracks gültig.

<dl>
<dt>createdDate</dt>
<dd>Gibt an, wann der Track erstellt wurde, und wird im Format `YYYYMMDDHHMM` angegeben.</dd>

<dt>endDate</dt>
<dd>Gibt an, wann der Track die Erfassung von Nachrichten stoppt. Der angegebene Wert muss in der Zukunft liegen und einem der folgenden Formate entsprechen: `YYYY-MM-DD` oder `YYYY-MM-DDTHH:MM:SSZ`. Wenn ein Datum in der Vergangenheit angegeben wird, wird ein HTTP 400-Fehler zurückgegeben.

Diese Eigenschaft ist für aggregierte Tracks nicht gültig.</dd>

<dt>id</dt>
<dd>Eine eindeutige Referenz-ID, die einem Track bei der Erstellung zugewiesen wird. Die ID wird für regelbasierte und aggregierte Tracks in einem GUID-Zeichenfolgeformat (z. B. 3F2504E0-4F89-41D3-9A0C-0305E82C3301) dargestellt.</dd>

<dt>name</dt>
<dd>Beschreibender Name des Tracks. Die Eindeutigkeit dieser Eigenschaft ist nicht gewährleistet.</dd>

<dt>rules</dt>
<dd>Eine Gruppe von Regeln, einschließlich Abfrageschlüsselwörtern und anderen Parametern, die die Trackfilter definieren. Diese Eigenschaft ist für regelbasierte Tracks gültig, nicht jedoch für aggregierte Tracks.</dd>

<dt>state</dt>
<dd>Muss **aktiv** oder **inaktiv** lauten. Ein aktiver Track erfasst Nachrichten, ein inaktiver Track nicht. Sie können den Status eines Tracks zu jedem beliebigen Zeitpunkt ändern.

Diese Eigenschaft ist für aggregierte Tracks nicht gültig.</dd>

<dt>trackIds</dt>
<dd>Ein Array mit Track-IDs. Diese Eigenschaft ist nur für aggregierte Tracks gültig.</dd>

<dt>type</dt>
<dd>Gibt an, ob es sich um einen regelbasierten Track (**Rule**) oder
um einen aggregierten Track (**Aggregated**) handelt.

Weitere Informationen zu Trackeigenschaften, einschließlich Trackoperationen und Modellschemas, finden Sie in der REST-API-Dokumentation von {{site.data.keyword.twittershort}}.</dd>
</dl>

