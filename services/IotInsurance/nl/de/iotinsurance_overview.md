---

copyright:
  years: 2016
lastupdated: "2016-10-26"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}


# Informationen zu {{site.data.keyword.iotinsurance_short}}
{: #about}
Letzte Aktualisierung: 21. Oktober 2016
{: .last-updated}

{{site.data.keyword.iotinsurance_full}} ist eine integrierte IoT-Produktionsinstanz zur Erfassung und Analyse von Gesamtkontextdaten für Versicherungsnehmer, die eine personalisierte Risikobewertung, Echtzeitschutz und eine Reduzierung der Versicherungskosten ermöglicht.
{: shortdesc}

{{site.data.keyword.iotinsurance_short}} bietet eine Gesamtkontextansicht der Vermögenswerte und der Situation des Versicherungsnehmers, einschließlich Informationen wie Standortdaten, Wetterdaten, Verkehrsdaten und Gesundheitszustand. Durch die detaillierte Analyse dieser Informationen kann das Versicherungsunternehmen dem Versicherungsnehmer eine personalisierte Risikobewertung und Echtzeitschutz bereitstellen. Die Vorteile für den Versicherungsnehmer bestehen unter anderem in der Risikovermeidung in Form von frühzeitigen Warnungen, personalisierter Beratung und einer effizienten Bearbeitung und Begleichung von Leistungsansprüchen. Die Vorteile für das Versicherungsunternehmen beinhalten Kundenzufriedenheit, Kundenbindung und Ausgabensenkung durch Vermeidung von Schadensfällen sowie durch Prozessautomation.

## Architektur
{: #architecture}

![{{site.data.keyword.iotinsurance_short}}-Architektur. Dieses Diagramm wird im Textkörper des Themas beschrieben.](images/IoT4I_architecture.svg "{{site.data.keyword.iotinsurance_short}}-Architektur")

Die {{site.data.keyword.iotinsurance_short}}-Komponenten arbeiten wie in diesem Abschnitt beschrieben zusammen. Diese Organisation wird auch im Architekturdiagramm angezeigt. Im {{site.data.keyword.iotinsurance_short}}-Dashboard werden Daten angezeigt, die in {{site.data.keyword.iot_short_notm}} und in der {{site.data.keyword.cloudantfull}}-Datenbank gespeichert werden. Die intelligenten mobilen Endgeräte des Benutzers, die über die Wink-Cloud miteinander verbunden sind, senden Daten an den Transformator, der die Daten verarbeitet und an {{site.data.keyword.iot_short_notm}} sendet. Die Daten werden von der Shield-Engine verarbeitet und, wenn die Shield-Kriterien erfüllt sind, über APIs an die Aktionsengine gesendet. Die Aktionsengine nutzt {{site.data.keyword.mobilepushfull}}, um Benachrichtigungen an die mobile Anwendung des Benutzers zu senden. Der Benutzer kann die mobile Anwendung auch zum Antworten auf Alerts oder Angebote verwenden. Die Antwort wird vom {{site.data.keyword.amafull}}-Service verarbeitet und über die APIs an {{site.data.keyword.iot_short_notm}} und anschließend an das {{site.data.keyword.iotinsurance_short}}-Dashboard zurückgegeben.

## Insurance-Dashboard
{: #insurance_dashboard}
Das Insurance-Dashboard gibt den Benutzern im Versicherungsunternehmen (wie z. B. Sachbearbeitern) eine Gesamtübersicht mit den relevanten Informationen zu ihren Kunden. Sie können die Shields und Ereignisse auf Landes-, Bezirks- oder Kundenebene anzeigen.

Das Beispiel-Insurance-Dashboard wird mit simulierten Daten geladen, um Ihnen zu zeigen, welche Informationen Sie sammeln und analysieren können.

## Beispiel für mobile App
{: #mobileapp}
Über das Beispiel für eine mobile App können Versicherungsnehmer (z. B. Hauseigentümer) die Informationen anzeigen und darauf reagieren, die {{site.data.keyword.iotinsurance_short}} von den Sensoren in ihren Häusern sendet.

Unter Verwendung eines Mobilgeräts berechtigen die Hauseigentümer den Service, eine Verbindung zur Cloud des Sensoranbieters herzustellen, um Daten zu senden und zu empfangen. Beispiel: Ein Hauseigentümer erhält eine Benachrichtigung in der mobilen Starter-App, wenn der Sensor einen Wasserleitungsschaden erkennt. Weitere Informationen finden Sie unter [Beispiel für mobile App installieren und verbinden](iotinsurance_mobile_app.html}).

## REST- und Echtzeit-APIs
{: #rest_api}
Die REST-APIs werden von der mobilen Starter-App, dem Insurance-Dashboard, der Shield-Engine sowie dem Risikocontroller verwendet. Sie geben Benutzern Informationen zu den Zuordnungen zwischen Geräten, Shields und Aktionen. Durch die Verwendung der APIs können Programmierer neue Benutzer erstellen, Ereignisdaten generieren, neue Shields erstellen und registrieren sowie Ereignisdaten abrufen.

Die API, auf die Sie über die Servicekonsole zugreifen, wird für Ihre Instanz von {{site.data.keyword.iotinsurance_short}} angepasst.

Auf der Seite 'API' haben Sie die folgenden Möglichkeiten:  
  - Sie können alle verfügbaren API-Aufrufe sowie die zugehörige Dokumentation anzeigen.
  - Sie können einzelne API-Aufrufe testen.  Sie können einen API-Aufruf auswählen, um alle Informationen anzuzeigen; klicken Sie anschließend auf die Option zum Testen.

Sie können die API-Beispiele als Unterstützung bei der Einführung in allgemeine Szenarios verwenden. Weitere Informationen finden Sie bei den [{{site.data.keyword.iotinsurance_short}}-API-Beispielen](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs).


## Transformator
{: #transformer}
Der Transformator fordert neue Informationen von der Cloud-Server-API an und setzt diese so um, dass sie den Daten in {{site.data.keyword.iotinsurance_short}} entsprechen. Die Daten werden anschließend veröffentlicht, damit sie von der übrigen {{site.data.keyword.iotinsurance_short}}-Implementierung verwendet werden können. Benutzer müssen die Transformatorkomponente für den Zugriff auf die Sensordaten in der Cloud und die Verarbeitung der aufgezeichneten Daten autorisieren. Die Autorisierung wird mithilfe der mobilen Starter-App erteilt. Derzeit wird nur der Cloudanbieter 'Wink' unterstützt.

## Shield-Engine
{: #shield_engine}
Auf der Grundlage der Informationen, die in einem Ereignis gespeichert werden, stellt die Shiled-Engine fest, ob es zu einer Gefahrensituation gekommen ist (z. B. ein Wasserleitungsschaden). Wurde eine Gefahrensituation ermittelt, werden die Daten an die Aktionsengine übergeben.

## Aktionsengine
{: #action_engine}
Mit der Aktionsengine werden die Aktionen bestimmt, die auf Basis der in dem Shield angegebenen Informationen auszuführen sind.

Mithilfe der {{site.data.keyword.iotinsurance_short}}-API können Sie neue Shields in JavaScript erstellen.

## Shields
{: #shields}
Bei einem 'Shield' handelt es sich um einen bestimmten Schutz, den ein Kunde beim Versicherer anfordert. Beispiel: Ein Hauseigentümer erwirbt für sein Haus Versicherungsschutz gegen Feuer, Wasserschäden, Einbruch und andere Gefahren. Die {{site.data.keyword.iotinsurance_short}}-Lösung bietet einen integrierten Schutz gegen Wasserschäden. Kunden werden benachrichtigt und können reagieren, sobald ein Ereignis des Typs 'Wasser' ihr Haus gefährdet. Unter Verwendung der REST-API können Entwickler zusätzliche Shields hinzufügen.
Shields werden in der {{site.data.keyword.iotinsurance_short}}-Analyseengine ausgeführt. Die Analyseengine erkennt den Gefahrentyp (z. B. *Wasserleitungsschaden*), das Benutzerkonto des Sensors, der die Gefahrenmeldung gesendet hat, sowie die Shields, die dem Konto zugeordnet sind. Auf der Basis dieser Informationen können Maßnahmen ergriffen werden.

# Zugehörige Links
{: #rellinks}

## Lernprogramme und Beispiele
{: #samples}
* [Code einer mobilen Beispiel-App unter GitHub](https://github.com/ibm-watson-iot/ioti-mobile){:new_window}

## API-Referenz
{: #api}
* [{{site.data.keyword.iotinsurance_short}}-API](https://iot4i-api-docs.mybluemix.net/){:new_window}
* [{{site.data.keyword.iotinsurance_short}}-API-Beispiele](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window}

## Zugehörige Links
{: #general}
* [{{site.data.keyword.iot_full}}-Dokumentation](https://console.ng.bluemix.net/docs/services/IoT/index.html)
* [Support-Forum für Entwickler](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [Stack Overflow-Support-Forum](http://stackoverflow.com/questions/tagged/ibm-bluemix)
