---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Informationen zu Team Dynamics

Mit {{site.data.keyword.DRA_full}} Team Dynamics kann mithilfe der sozialen Codeanalyse der Grad der Interaktion zwischen Teammitgliedern bestimmt werden, sodass das Team unproduktive Verfahren korrigieren kann.
{:shortdesc}

Klicken Sie nach dem Öffnen von {{site.data.keyword.DRA_short}} über die Toolchain auf **Team Dynamics**. Von hier aus können Sie eine Analysekategorie auswählen, um einen tieferen Einblick in die Gewohnheiten und Vorgehensweise Ihres Teams bei der Zusammenarbeit zu erhalten. Was einzelne Datensätze aussagen, kann von Team zu Team unterschiedlich sein. Sie können daher für jede Visualisierung einen Drilldown durchführen, um eine weitere Orientierungshilfe zu erhalten.   

## Datenkategorien

Für die Daten, die von {{site.data.keyword.DRA_short}} zum Auffüllen der Dashboards verwendet wird, wird automatisch ein Data-Mining aus dem Repository für die Quellcodeverwaltung des Teams durchgeführt. Weitere Informationen zur Bedeutung der Daten und zu Anwendungsmöglichkeiten für Ihr Projekt erhalten Sie durch Klicken auf **Informationen** oder **Anweisungen** in einem Diagramm. 

### Soziale Codierung

Das Diagramm für die soziale Codierung veranschaulicht die Verbindungen zwischen Ihren Projektmitarbeitern auf eine extrem interaktive Art und Weise. Jeder Knoten im Diagramm stellt einen Entwickler dar. Die Größe eines Knotens skaliert logarithmisch zu den Beiträgen eines Entwicklers zu einem Projekt. Die Linien zwischen Knoten stehen für die Zusammenarbeit; je dicker die Linie ist, je enger haben zwei Entwickler über den ausgewählten Zeitraum zusammengearbeitet.  

Jeder Knoten ist in unterschiedlichem Maße blau oder rot. Blau zeigt an, wie viele Codezeilen ein Beitragender als Teil der Gesamtanzahl an Zeilen hinzugefügt hat, die der Beitragende bearbeitet hat. Rot zeigt an, wie viele Codezeilen ein Beitragender entfernt hat. Ein Beitragender, der nur Code hinzugefügt hat, wäre vollständig blau, während ein Beitragender, der jeweils gleich viele Zeilen hinzugefügt und entfernt hat, halb blau und halb rot wäre.  

### Autoren

Die Kategorie 'Autoren' gibt die Anzahl der Commits, Zeilenänderungen und Dateiänderungen pro Beitragender zum Repository an. Anhand der Gesamtanzahl der codierten Zeilen sollte jedoch beispielsweise nicht der Nettobeitrag eines Teammitglieds zu einem Projekt ermittelt werden, jedoch können diese Informationen für Teamleiter und Manager hilfreich sein. Ein Teammitglied, das eine sehr große Anzahl an Zeilenänderungen beiträgt, kann überarbeitet sein, eine Schwachstelle in Ihrem Prozess sein oder im Vergleich zu anderen Teammitgliedern Code ausführlicher darstellen.  
