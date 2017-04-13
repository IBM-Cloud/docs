---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-07"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Verifizierte Leistung
{: #etn_performance}


Die folgenden Verhaltensarten wurden von IBM getestet und überprüft. Die Ergebnisse wurden in einem Netz mit hohem Sicherheitsniveau erzielt (sofern nicht anders angegeben):
{:shortdesc}

### Leistung/Belastung

Ziel dieses Tests war das Messen des TPS-Werts (TPS - Transaktionen pro Sekunde) für Aufrufe und Abfragen in kurzen Testintervallen von 10 Minuten und langen Testintervallen von 60 Minuten, während PBFT sowie Sicherheit und Datenschutz aktiviert waren.  Die Leistung kann abhängig von Umgebung, Anwendungstyp, Konfigurations- und Sicherheitseinstellungen, Stapelgröße der Transaktionen und anderen Faktoren abweichen.  (**Hinweis:** Diese Messwerte wurden in einem verteilten Multi-Tenant-Netz ermittelt.)

- Chaincode: example02
- Protokollstufe: error
- Threadanzahl: 100
- Stapelgröße: 1000
- Dauer: 10 Min. und 60 Min.
- Transaktionstypen: Aufruf a->b, Aufruf b->a, anschließend Wiederholen und Abfrage von a, Abfrage von b, anschließend Wiederholen

| Transaktionstyp | Anzahl der Peers | Anzahl der Threads | Ausführungsdauer (Min) | Transaktionen pro Sekunde |
| ---------- |:-------:|:-----:|:------:|:------:|
| Aufrufe   |  4  | 100 | 10 | 72  |
| Aufrufe   |  4  | 100 | 60 | 66  |
| Abfragen   |  4  | 100 | 10 | 252 |
| Abfragen   |  4  | 100 | 60 | 248 |

### Ausfallsicherheit/Konsens

Anhand der folgenden Tests sollte die Stabilität und Ausfallsicherheit von PBFT sichergestellt werden, wenn ein Byzantine-Fehler auftritt.  Folgende Tests wurden durchgeführt:

- Stoppen eines Knotens und weiterhin Senden von Transaktionen zum Bereitstellen, Aufrufen und Abfragen.  Das Netz funktioniert weiterhin. Wird auf jedem Knoten im Netz ausgeführt.
- Stoppen von zwei Knoten; das Netz wird gestoppt, weil kein Konsens gegeben ist.
- Neustart eines im vorherigen Test gestoppten Knotens.  Die Verarbeitung im Netz wird wiederaufgenommen und der neu gestartet Knoten wird mit anderen validierenden Peers synchronisiert. Die detaillierten Schritte der PBFT-Tests finden Sie im Abschnitt [Konsens und Verfügbarkeit testen](etn_pbft.html).

Informationen zu den weiteren Tests und überprüften Funktionen finden Sie im Abschnitt [Weitere Tests](etn_next.html).  
