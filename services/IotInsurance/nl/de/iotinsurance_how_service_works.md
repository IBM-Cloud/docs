---

copyright:
  years: 2016
lastupdated: "2016-10-26"

---


{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Funktionsweise des Service
{{site.data.keyword.iotinsurance_full}} erstellt einen Ablauf zum Erfassen, Verwalten und Analysieren von Daten von verbundenen Versicherungsnehmern.
{:shortdesc}

Der Versicherer erstellt eine Instanz von {{site.data.keyword.iotinsurance_short}} innerhalb der {{site.data.keyword.Bluemix_notm}}-Organisation. In den Häusern der Kunden des Versicherungsunternehmens sind Sensoren installiert, die mit der Cloud des Sensoranbieters verbunden sind. Über ihre mobilen Geräte berechtigen Kunden den Service {{site.data.keyword.iotinsurance_short}} für den Empfang der Sensordaten. Der Transformator {{site.data.keyword.iotinsurance_short}} stellt eine Verbindung zur Cloud des Sensoranbieters her, entnimmt die Daten der einzelnen Benutzer und sendet diese an den {{site.data.keyword.iot_short_notm}}-Server. Wenn der Sensor anzeigt, dass die Parameter, die in den Shields des Versicherungsunternehmens angegeben sind, im Haushalt des Kunden gegeben sind, werden sowohl an das Dashboard des Versicherungsunternehmens als auch an das Gerät des Kunden entsprechende Benachrichtigungen gesendet.

Ein verbundener Sensor ermittelt ein Ereignis, z. B. einen Wasserleitungsschaden, und sendet diese Informationen an einen Smart Home-Anbieter wie Wink.  {{site.data.keyword.iotinsurance_short}} erkennt das Signal über seine Verbindung mit der Cloud des Smart Home-Anbieters und erstellt Alertnutzdaten. Die Nutzdaten werden mittels MQTT zur Verarbeitung an die {{site.data.keyword.iotinsurance_short}}-Shield-Engine gesendet. Die Shield-Engine analysiert, ob die Nutzdaten mit den durch die Shield-Regeln definierten Kriterien übereinstimmen. Ist dies der Fall, gibt die Shield-Engine mittels MQTT Nutzdaten für eine Gefahr an die {{site.data.keyword.iotinsurance_short}}-Aktionsengine aus. Die Aktionsengine führt Aktionen aus, die das Shield für den jeweiligen Gefahrentyp definiert, z. B. Senden einer Textnachricht an den Hausbesitzer.

{{site.data.keyword.iotinsurance_short}} ist für die Übergabe von Nutzdaten zu Alerts und Gefahren zwischen den Komponenten auf {{site.data.keyword.iot_full}} angewiesen. Für ein vollständiges, funktionierendes System sind Benutzer, Shields und Zuordnungen zwischen Benutzern und Shields erforderlich.

![{{site.data.keyword.iotinsurance_short}}-Prozess. Dieses Diagramm wird im Textkörper des Themas beschrieben.](images/IoT4I_process.svg "{{site.data.keyword.iotinsurance_short}}-Prozess")

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
