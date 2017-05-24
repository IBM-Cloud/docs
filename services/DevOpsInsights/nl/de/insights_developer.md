---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Developer Insights (Experimentell)
{: #gettingstarted}

Mit {{site.data.keyword.DRA_full}} Developer Insights können Sie die Risiken bei der Entwicklung Ihres Projekts umfassend untersuchen. Sie können fehlerträchtige Dateien ermitteln und eine Konformitätsansicht des Projekts im Hinblick auf die DevOps-Verfahren erhalten. {:shortdesc}

Klicken Sie nach dem Öffnen von {{site.data.keyword.DRA_short}} über die Toolchain auf **Developer Insights**. Von hier aus können Sie eine Analysekategorie auswählen, um einen tieferen Einblick in die Codebasis Ihres Projekts zu erhalten. Was einzelne Datensätze aussagen, kann von Team zu Team unterschiedlich sein. Sie können daher für jede Visualisierung einen Drilldown durchführen, um eine weitere Orientierungshilfe zu erhalten.  

## Datenkategorien
Für die Daten, die von {{site.data.keyword.DRA_short}} zum Auffüllen der Dashboards verwendet wird, wird automatisch ein Mining aus dem Repository für die Quellcodeverwaltung des Teams durchgeführt. Weitere Informationen zur Bedeutung der Daten und zu Anwendungsmöglichkeiten für Ihr Projekt erhalten Sie durch Klicken auf **Informationen** oder **Anweisungen** in einem Diagramm. 

### Bewährte Verfahren für Entwickler

Developer Insights stellt eine Reihe von Diagrammen bereit, anhand derer Sie Ihr Projekt gegenüber bewährten DevOps- und Entwicklerverfahren messen können. Verwenden Sie diese Kategorie, um eine übergeordnete Ansicht über den Reifegrad, den Zustand und die Effizienz Ihres Projekts zu erhalten.  

### Fehleranfälligkeit

Die *Fehleranfälligkeit* ist die Wahrscheinlichkeit, dass eine Datei oder ein Commit in Abhängigkeit von Langzeittrends, Erfahrungen von Committern, Änderungshäufigkeit, Änderungsgewichtung und anderen Faktoren Fehler generiert.  

Diese Kategorie kann beim Durchführen von Codeprüfungen oder Verbessern des Prozesses für die Codeprüfung zu rate gezogen werden. Dateien mit einem gewissen Sicherheitsrisiko müssen stärker überprüft werden als relativ sichere Dateien. Umgekehrt können sichere Dateien und Commits als Beispiele für Ihr Team für eine verbesserte Arbeitsweise dienen. 

### Probleme

Die Kategorie 'Probleme' fasst alle Probleme bei der Leistungserfassung für Ihr Team an einem Ort zusammen. Die Probleme werden automatisch nach Typ, Priorität und Tag gruppiert und können im Zeitverlauf angezeigt werden.  

Diese Problemgruppierungen können sich von Team zu Team in ihrer Bedeutung unterscheiden. Für ein Team könnte es beispielsweise interessant sein, ob die meisten mit Tags versehenen Elemente für ein bestimmtes Release geschlossen sind, während ein anderes Team Releases nicht mit Tags versieht und diese gemäß der Priorität der offenen Probleme verarbeitet.   

### Commits

Commits zeigen den Arbeitsumfang an, den Ihre Teammitglieder zur Codebasis beitragen. Untersuchen Sie Ihre Commitdaten, um zu verstehen, an welcher Stelle im Zeitverlauf gesehen ein großer Aufwand betrieben wird und wie Sie die Arbeitslasten Ihres Teams besser verteilen können.  

### Dateien

Die Kategorie 'Dateien' zeigt, welche Dateien in Ihrem Projekt am häufigsten verwendet werden. Ganz gleich, ob Sie Daten anhand der Anzahl der Zeilenänderungen, Commits, Autoren oder Fehler bewerten: Diese Daten verraten Ihnen, in welchen Bereichen Ihr Team besonders aktiv ist.  

Versuchen Sie allgemein sowohl die Anzahl der Mitglieder zu verringern, die eine Datei bearbeiten dürfen, als auch die Häufigkeit, mit der diese Datei geändert wird. Dieses Ziel kann jedoch für einige Dateien, wie allgemeine Konfigurationsdateien, unrealistisch sein. Jedoch sind für einzelne Dateien, an denen Entwickler gleichzeitig viele Änderungen vornehmen, Probleme vorprogrammiert.  

**Hinweis**: DevOps Insights ignoriert Dateien mit den folgenden Erweiterungen:

* .bin
* .cdr
* .jpeg
* .jpg
* .json
* .markdown
* .md
* .png
* .pyc
* .svg
* .text
* .yaml
* .yml

