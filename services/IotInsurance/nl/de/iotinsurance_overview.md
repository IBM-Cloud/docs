---

copyright:
  years: 2016

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}


# Informationen zu {{site.data.keyword.iotinsurance_short}}
{: #about_servicename}
Letzte Aktualisierung: 15. September 2016
{: .last-updated}

{{site.data.keyword.iotinsurance_full}} ist eine integrierte IoT-Produktionsinstanz zur Erfassung und Analyse von Gesamtkontextdaten für Versicherungsnehmer, die eine personalisierte Risikobewertung, Echtzeitschutz und eine Reduzierung der Versicherungskosten ermöglicht.
{: shortdesc}

{{site.data.keyword.iotinsurance_short}} bietet eine Gesamtkontextansicht der Vermögenswerte und der Situation des Versicherungsnehmers, einschließlich Informationen wie Standortdaten, Wetterdaten, Verkehrsdaten und Gesundheitszustand. Durch die detaillierte Analyse dieser Informationen kann das Versicherungsunternehmen dem Versicherungsnehmer eine personalisierte Risikobewertung und Echtzeitschutz bereitstellen. Die Vorteile für den Versicherungsnehmer bestehen unter anderem in der Risikovermeidung in Form von frühzeitigen Warnungen, personalisierter Beratung und einer effizienten Bearbeitung und Begleichung von Leistungsansprüchen. Die Vorteile für das Versicherungsunternehmen beinhalten Kundenzufriedenheit, Kundenbindung und Ausgabensenkung durch Vermeidung von Schadensfällen sowie durch Prozessautomation.

## Prozessablauf
{: #processFlow}
Der Versicherer verfügt im {{site.data.keyword.Bluemix_notm}}-Service-Broker über eine Instanz. In den Häusern der Kunden des Versicherungsunternehmens sind Sensoren installiert, die mit der Cloud des Sensoranbieters verbunden sind. Über ihre mobilen Geräte berechtigen diese Benutzer den Service {{site.data.keyword.iotinsurance_short}} für den Empfang der Sensordaten aus {{site.data.keyword.iotinsurance_short}}. Der Service {{site.data.keyword.iotinsurance_short}} stellt eine Verbindung zur Cloud des Sensoranbieters her, entnimmt die Daten der einzelnen Benutzer und sendet diese an den IoT-Server. Wenn der Sensor anzeigt, dass die Parameter, die in den Shields des Versicherungsunternehmens angegeben sind, im Haushalt des Kunden gegeben sind, werden sowohl an das Dashboard des Versicherungsunternehmens als auch an das Gerät des Kunden entsprechende Benachrichtigungen gesendet.

## Komponenten
{: #components}

### Insurance-Dashboard
{: #insurance_dashboard}
Das Insurance-Dashboard gibt den Benutzern im Versicherungsunternehmen (wie z. B. Sachbearbeitern) eine Gesamtübersicht mit den relevanten Informationen zu ihren Kunden. Sie können die Shields und Ereignisse auf Landes-, Bezirks- oder Kundenebene anzeigen.

Das Beispiel-Insurance-Dashboard wird mit simulierten Daten geladen, um Ihnen zu zeigen, welche Informationen Sie sammeln und analysieren können.

### Mobile Starter-App
{: #mobileapp}
Über die mobile Starter-App können Versicherungsnehmer (z. B. Hauseigentümer) die Informationen anzeigen und beantworten, die {{site.data.keyword.iotinsurance_short}} von den Sensoren in ihren Häusern sendet.

Unter Verwendung eines Mobilgeräts berechtigen die Hauseigentümer den Service, eine Verbindung zur Cloud des Sensoranbieters herzustellen, um Daten zu senden und zu empfangen. Beispiel: Ein Hauseigentümer erhält eine Benachrichtigung in der mobilen Starter-App, wenn der Sensor einen Wasserleitungsschaden erkennt. Weitere Informationen finden Sie unter [Mobile Starter-App installieren und verbinden](iotinsurance_mobile_app.html).

### REST-API
{: #rest_api}
Die REST-API wird von der mobilen Starter-App, dem Insurance-Dashboard, der Shield-Engine sowie dem Risikocontroller verwendet. Sie gibt Benutzern Informationen zu den Zuordnungen zwischen Geräten, Shields und Aktionen. Durch die Verwendung dieser API können Programmierer neue Benutzer erstellen, Ereignisdaten generieren, neue Shields erstellen und registrieren sowie Ereignisdaten abrufen.

Die API, auf die Sie über die Servicekonsole zugreifen, wird für Ihre Instanz von {{site.data.keyword.iotinsurance_short}} angepasst.

Auf der Seite 'API' haben Sie die folgenden Möglichkeiten:  
  - Sie können alle verfügbaren API-Aufrufe sowie die zugehörige Dokumentation anzeigen.
  - Sie können einzelne API-Aufrufe testen.  Sie können einen API-Aufruf auswählen, um alle Informationen anzuzeigen; klicken Sie anschließend auf die Option zum Testen.

Sie können die API-Beispiele als Unterstützung bei der Einführung in allgemeine Szenarios verwenden. Weitere Informationen finden Sie bei den [{{site.data.keyword.iotinsurance_short}}-API-Beispielen](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs).

### Cloud-Provider
{: #cloudprovider}
Benutzer müssen die Transformatorkomponente für den Zugriff auf die Sensordaten in der Cloud und die Verarbeitung der aufgezeichneten Daten autorisieren. Die Autorisierung wird mithilfe der mobilen Starter-App erteilt. Derzeit wird nur der Cloudanbieter 'Wink' unterstützt.

### Transformator
{: #transformer}
Der Transformator fordert neue Informationen von der Cloud-Server-API an und setzt diese so um, dass sie den Daten in {{site.data.keyword.iotinsurance_short}} entsprechen. Die Daten werden anschließend veröffentlicht, damit sie von der übrigen {{site.data.keyword.iotinsurance_short}}-Implementierung verwendet werden können.

### Analyseengine
{: #analytics_engine}
Auf der Grundlage der Informationen, die in einem Ereignis gespeichert werden, stellt die Analyseengine fest, ob es zu einer Gefahrensituation gekommen ist (z. B. ein Wasserleitungsschaden). Wurde eine Gefahrensituation ermittelt, werden die Daten an den Gefahrencontroller übergeben. Mit der Aktionsengine werden die Daten in der Datenbank angezeigt, um die Aktion festzulegen, die auf Basis der in dem Shield angegebenen Informationen auszuführen ist.

Mithilfe der {{site.data.keyword.iotinsurance_short}}-API können Sie neue Shields in JavaScript erstellen.

### Shields
{: #shields}
Bei einem 'Shield' handelt es sich um einen bestimmten Schutz, den ein Kunde beim Versicherer anfordert. Beispiel: Ein Hauseigentümer erwirbt für sein Haus Versicherungsschutz gegen Feuer, Wasserschäden, Einbruch und andere Gefahren. Die {{site.data.keyword.iotinsurance_short}}-Lösung bietet einen integrierten Schutz gegen Wasserschäden. Kunden werden benachrichtigt und können reagieren, sobald ein Ereignis des Typs 'Wasser' ihr Haus gefährdet. Unter Verwendung der REST-API können Entwickler zusätzliche Shields hinzufügen.
Shields werden in der {{site.data.keyword.iotinsurance_short}}-Analyseengine ausgeführt. Die Analyseengine erkennt den Gefahrentyp (z. B. *Wasserleitungsschaden*), das Benutzerkonto des Sensors, der die Gefahrenmeldung gesendet hat, sowie die Shields, die dem Konto zugeordnet sind. Auf der Basis dieser Informationen können Maßnahmen ergriffen werden.
