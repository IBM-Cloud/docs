---



copyright:

  years: 2015, 2017
lastupdated: "2017-04-12"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Berechnung der Gebühren
{: #charges}

Die Höhe der Gebühren hängt von den jeweiligen Ressourcen ab, die von einem bestimmten Service oder Container bzw. einer bestimmten Laufzeit oder einer Unterstützungsoption verwendet werden. Bei den Ressourcen kann es sich um die Anzahl der API-Aufrufe, die Anzahl der Instanzen, die Hauptspeichermenge, den Speicherplatz, usw. handeln. {{site.data.keyword.Bluemix_notm}} stellt auch eine detaillierte Kostenschätzungsfunktionen und eine Kostenberechnungsfunktion bis auf den letzten Cent bereit, die Ihnen beim Planen der Gebühren behilflich sein können. Sie können die tatsächlichen Kosten nach dem Erstellen der Apps auf der Seite 'Nutzungsdashboard' überprüfen. 

Über ein belastbares {{site.data.keyword.Bluemix_notm}}-Konto werden die Gebühren für Berechnungen, Container und Services erhoben, die von Ihrer Organisation in Anspruch genommen werden. Es kann vorkommen, dass Sie von anderen {{site.data.keyword.Bluemix_notm}}-Benutzern eingeladen werden, unter einem anderen Konto an Organisationen teilzunehmen. Wenn Sie in den Organisationen, in die Sie eingeladen wurden, Apps erstellen oder Services verwenden, werden die Gebühren, die für diese Nutzung anfallen, dem Konto in Rechnung gestellt, das die betreffenden Organisationen enthält. Weitere Informationen zu bestimmten Gebühren können Sie über die Detailseite einer Ressource im {{site.data.keyword.Bluemix_notm}}-Katalog oder über den Preisrechner auf der {{site.data.keyword.Bluemix_notm}}-Seite 'Preisstruktur' aufrufen.

Die Gebühren werden abhängig von den von Ihnen verwendeten Komponenten von {{site.data.keyword.Bluemix_notm}} berechnet. In der folgenden Tabelle wird eine allgemeine Übersicht bereitgestellt:

| Gebührentyp | Beschreibung | {{site.data.keyword.Bluemix_notm}}-Features, die diesen Gebührentyp verwenden | Beispiel |
|------------------|------------------|--------------------------|--------------------------|
| Fest | Die Festpreisgestaltung basiert auf einer vereinbarten monatlichen Gebühr, die nicht angepasst wird. | Services  | Für den Datencache wird ein fester Plan verwendet, der als feste monatliche Rate abgerechnet wird. |
| Nutzungsabhängig | Die nutzungsabhängige Preisgestaltung basiert auf der Anzahl der GB-Stunden, die für Laufzeiten verbraucht werden, der Anzahl der GB-Stunden, die verbraucht wurden und der Anzahl der IP-Adressen und des Speichers für die Container. | Services, Berechnen und Container | Beim Push-Service wird jede Nutzung in Rechnung gestellt, die über die kostenlose monatliche Leistung hinausgeht. |
|  Preisstufen   |  Manche Pläne basieren auf einem Preisstufenmodell, das einen dem tatsächlichen Nutzungsvolumen entsprechenden Nachlass ermöglicht. Für Services können Preistarife für einfache, gestaffelte oder Blockpreisstufen angeboten werden. | Services | Die gestaffelte Preisstruktur wird in der Regel für Gebührenmetriken verwendet, wenn große Mengen pro Monat erwartet werden, zum Beispiel für API-Aufrufe. |
| Reserviert | Die Preisgestaltung für Reservierungen basiert auf einer langfristigen Zusage für einen Service; dafür erhalten Sie einen reduzierten Preis. Bei einem Reservierungsplan erhalten Sie eine dedizierte Serviceinstanz, die sich in der öffentlichen {{site.data.keyword.Bluemix_notm}}-Umgebung leicht einrichten, implementieren und bereitstellen lässt. | Services | Für DB2 on Cloud werden Reservierungspläne bereitgestellt.|

## Gebühren für Rechenressourcen
{: #compute}

Ihnen werden die Zeit, die Ihre Apps aktiv sind, und der Speicher, der verwendet wird, in Form von berechneten *GB-Stunden* in Rechnung gestellt. GB-Stunden berechnen sich aus der Anzahl der Anwendungsinstanzen multipliziert mit dem genutzten Speicher pro Instanz multipliziert mit den Stunden, die die Instanzen aktiv sind. Sie können die Anzahl der Instanzen und die Speicherkapazität pro Instanz nach Bedarf anpassen. Sie können darüber hinaus Speicher oder Instanzen hinzufügen, um eine Skalierung auf weitere Benutzer zu realisieren. Die endgültige Gebühr basiert auf GB-Stunden: Ihre Anwendungsinstanzen multipliziert mit der Speicherkapazität pro Instanz multipliziert mit den Stunden, die sie aktiv waren.

Beispiel: Nehmen Sie eine Laufzeit an, die pro GB-Stunde einen Preis von $0,07 in zwei 512-MB-Instanzen kostet und 30 Tage (720 Stunden) aktiv ist. Diese Ressourcen würden nach den folgenden Berechnungen $24,15 USD kosten, wobei eine kostenfreie Leistung von 375 GB-Stunden berücksichtigt wird:

```
2 Instanzen x 0,5 GB x 720 Stunden = 720 GB-Stunden.
(720 - 375) GB-Stunden x $0,07 pro GB-Stunde = $24,15
```

## Gebühren für Services
{: #services}

Viele Services schließen monatliche kostenlose Leistungen ein. Die Nutzung von Services, die nicht von den kostenlosen Leistungen abgedeckt ist, wird auf eine der beiden folgenden Arten in Rechnung gestellt:
<dl>
<dt>Feste Gebühren</dt>
    <dd>Sie wählen einen Plan aus und bezahlen einen Pauschalbetrag. Beispiel: Für den Datencacheservice wird ein Pauschalbetrag berechnet.</dd>
<dt>Nutzungsabhängige Gebühren</dt>
    <dd>Sie bezahlen entsprechend Ihrer Laufzeit- und Servicenutzung. Beispiel: Beim Push-Service wird jede Nutzung in Rechnung gestellt, die über die kostenlose monatliche Leistung hinausgeht.</dd>
<dt>Reservierungsgebühren</dt>
    <dd><p>Als Eigner eines Kontos für nutzungsabhängige Zahlung oder eines Abonnementkontos können Sie sich eine Serviceinstanz bei einer langfristigen Verpflichtung zu einem reduzierten Preis reservieren lassen. Beispiel: Sie können sich das Angebot 'DB2 on Cloud' in der herkömmlichen Größe für 12 Monate reservieren lassen.</p>
    <p>Für manche {{site.data.keyword.Bluemix_notm}}-Services werden Reservierungspläne angeboten. Sie können einen Reservierungsplan im {{site.data.keyword.Bluemix_notm}}-<strong>Katalog</strong> durch Klicken auf die Kachel des Service anfordern. Wählen Sie anschließend den Serviceplan aus, der Ihren Anforderungen am ehesten entspricht. Wenn ein Reservierungsplan verfügbar ist, klicken Sie auf <strong>Anfordern</strong> und gehen gemäß den Eingabeaufforderungen vor, um Ihre Anforderung zu senden. Sie erhalten eine E-Mail, in der die Preisinformationen für den Reservierungsplan enthalten sind. Außerdem wird sich bald ein {{site.data.keyword.Bluemix_notm}}-Vertriebsbeauftragter mit Ihnen in Verbindung setzen, um den Kauf durchzuführen.</p></dd>
<dt>Gestaffelte Preise</dt>
    <dd>Ähnlich wie bei den nutzungsabhängigen Gebühren bezahlen Sie die Gebühren entsprechend Ihrer Laufzeit- und Servicenutzung. Bei gestaffelten Preisen werden jedoch zusätzliche Preisstufen hinzugefügt, wobei oft reduzierte Gebühren in Stufen mit hohem Verbrauch angeboten werden. Gestaffelte Preise werden einfach, gestaffelt oder als Block angeboten.</dd>
</dl>

### Einfache Preisstufe
{: #simple_tier}

Im Modell mit einer einfachen Preisstufe wird der Einzelpreis durch die Preisstufe bestimmt, in die Ihr Nutzungsvolumen fällt. Der Gesamtpreis besteht aus der Menge multipliziert mit dem Einzelpreis in dieser Preisstufe. Beispiel:

| Menge der Posten | Einzelpreis für alle Posten |
|-------------------|--------------------------|
| Stufe 1: 1 - 1000  | $ 1 USD                   |
| Preisstufe 2: 1001 - 2000    |    $ 0,90 USD                      |
| Preisstufe 3: 2001 - 3000                  |   $ 0,75 USD                       |
| Preisstufe 4: 3001 - 4000           |      $ 0,60 USD                    |
|Preisstufe 5: &gt; 4000 | $ 0,40 USD |
{:caption="Tabelle 1. Tabelle der einfachen Preisabstufung" caption-side="top"}

In der folgenden Tabelle sind die Gebühren dargestellt, die im Rahmen eines Plans anfallen, der auf dem Preismodell mit einfacher Preisstufe basiert:

| Menge der Posten | Gebührenberechnung | Gesamtpreis |
|-------------------|--------------------|-------------|
|500 |	500 × 1 = 500 |	$ 500 USD|
|1500 |	1500 × 0,90 = 1350 |	$ 1350 USD|
|2500 |	2500 × 0,75 = 1875 |	$ 1875 USD|
|... |	... |	...|
|5200 |	5200 × 0,40 = 2080 |$ 2080 USD|
{:caption="Tabelle 2. Gebührenberechnung mit einem einfachen Preisstaffelungsmodell" caption-side="top"}

### Gestaffelte Preisstufe
{: #graduated_tier}

Im Modell mit gestaffelter Preisstufe sinkt der Einzelpreis bei einer höheren Nutzungsrate. Der Gesamtpreis besteht aus den kumulativen Gebühren für die einzelnen Nutzungsstufen, bestehend aus der Menge multipliziert mit dem Einzelpreis für die jeweilige Preisstufe. Beispiel:

| Menge der Posten |	Einzelpreis für Posten in dieser Preisstufe|
|-------------------|------------------------------------|
|    Stufe 1: 1 - 1000 |	$ 1 USD |
|   Preisstufe 2: 1001 - 2000 |	$ 0,90 USD |
|    Preisstufe 3: 2001 - 3000 |	$ 0,75 USD |
|    Preisstufe 4: 3001 - 4000 |	$ 0,60 USD |
|    Preisstufe 5: &gt; 4000 |	$ 0,40 USD |
{:caption="Tabelle 3. Tabelle mit erweiterter Preisstaffelung" caption-side="top"}

In der folgenden Tabelle sind die Gebühren dargestellt, die im Rahmen eines Plans anfallen, der auf dem Preismodell mit gestaffelter Preisstufe basiert:

|Menge der Posten | Gebührenberechnung | Gesamtpreis|
|------------------|--------------------|------------|
|500 |	500 × 1 (Einzelpreis für Preisstufe 1) = 500 |	$ 500 USD|
|1500 |	(1000 × 1 (Einzelpreis für Preisstufe 1)) + (500 × 0,90 (Einzelpreis für Preisstufe 2)) = 1450 |	$ 1450 USD|
|2500 |	(1000 × 1 (Einzelpreis für Preisstufe 1)) + (1000 × 0,90 (Einzelpreis für Preisstufe 2)) + (500 × 0,75 (Einzelpreis für Preisstufe 3)) = 2275 |	$ 2275 USD |
|... |	... |	...|
|5200 |	(1000 × 1 (Einzelpreis für Preisstufe 1)) + (1000 × 0,90 (Einzelpreis für Preisstufe 2)) + (1000 × 0,75 (Einzelpreis für Preisstufe 3)) + (1000 × 0,60 (Einzelpreis für Preisstufe 4)) + (1200 × 0,40 (Einzelpreis für Preisstufe 5)) = 3730 |	$ 3730 USD|
{:caption="Tabelle 4. Gebührenberechnung mit dem erweiterten Preisstaffelungsmodell" caption-side="top"}

### Blockpreisstufe
{: #block_tier}

Im Preismodell mit Blockpreisstufen ist der Preis eine feste Gebühr für die genutzte Menge innerhalb einer Nutzungsstufe. Der Gesamtpreis besteht aus der Gebühr für die jeweilige Nutzungsstufe, unabhängig von der tatsächlichen Nutzung. Jede nachfolgende Preisstufe bietet ein niedrigeres Preis-Menge-Verhältnis. Beispiel:

|Menge der Posten |	Gesamtpreis für alle Posten|
|------------------|-----------------------------|
| Preisstufe 1: &lt;= 1000 |	$ 1000 USD|
| Preisstufe 2: &lt;= 2000 |	$ 1900 USD|
| Preisstufe 3: &lt;= 3000 |	$ 2800 USD|
| Preisstufe 4: &lt;= 4000 |	$ 3500 USD|
| Preisstufe 5: &lt;= 10000 |	$ 5000 USD|
{:caption="Tabelle 5. Tabelle der Blockpreisstaffelung" caption-side="top"}

In der folgenden Tabelle sind die Gebühren dargestellt, die im Rahmen eines Plans anfallen, der auf dem Preismodell mit Blockpreisstufe basiert:

|Menge der Posten |	Gebührenberechnung |	Gesamtpreis|
|------------------|-----------------------|---------------|
|500 |	Die Anzahl der Posten fällt in die Preisstufe 1, d. h., der Gesamtpreis beträgt $ 1000 USD. |	$ 1000 USD|
|1500 |	Die Anzahl der Posten fällt in die Preisstufe 2, d. h., der Gesamtpreis beträgt $ 1900 USD. |	$ 1900 USD|
|... |	... |	...|
|5200 |	Die Anzahl der Posten fällt in die Preisstufe 5, d. h., der Gesamtpreis beträgt $ 5000 USD. |	$ 5000 USD|
{:caption="Tabelle 6. Gebührenberechnung mit dem Blockpreisstaffelungsmodell" caption-side="top"}
