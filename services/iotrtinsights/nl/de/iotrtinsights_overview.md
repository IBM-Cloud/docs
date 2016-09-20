---

copyright:
  years: 2015,2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Produktinformationen zu {{site.data.keyword.iotrtinsights_short}}
{: #iotrtinsights_overview}
*Letzte Aktualisierung: 11. Februar 2016*

{{site.data.keyword.iotrtinsights_short}} stellt eine Echtzeitanalyse-Engine und Analyse-Authoring-Funktionen bereit, die die Kontextualisierung und Überwachung von IoT-Gerätedaten ermöglichen, zu einem schnelleren Verständnis der aktuellen Bedingungen beitragen und die Entscheidungsfindung und Reaktionen auf auftretende Probleme verbessern.
{:shortdesc}

## {{site.data.keyword.iotrtinsights_full}}
{: #iotrtinsights_concept}
{{site.data.keyword.iotrtinsights_short}} verwendet ein einfaches, regelbasiertes Erstellungsmodell und ein erweiterbares Framework, die Sie bei folgenden Tasks unterstützen: Nutzen von IoT-Daten, Kombination dieser Daten mit Master-Assetdaten, Analyse von Situationen im Kontext und Automatisieren von Antworten zur Verbesserung von Operationen, Verfügbarkeit und Service-Leveln. 

{{site.data.keyword.iotrtinsights_short}} stellt eine Verbindung zum {{site.data.keyword.bluemix}} {{site.data.keyword.iot_short}}-Service her, um Echtzeitdatenfeeds von Geräten zu erhalten. Die ankommenden Daten werden mithilfe eines virtuellen Datenmodells interpretiert, das mit Asset-Masterdaten von einem Asset-Management-System, wie zum Beispiel IBM Maximo&reg; Asset Management, erweitert werden kann. 

Außerdem werden benutzerdefinierte Regeln auf die Echtzeit-Streaming-Daten angewendet, um Bedingungen zu erkennen, die ein Eingreifen erfordern. Mithilfe der Aktions-Engine können Sie automatische Antworten auf die festgestellten Bedingungen definieren, wie zum Beispiel Senden einer E-Mail, Auslösen eines IFTTT-Rezepts, Ausführen eines Node-RED-Workflows oder Verwendung von Webhooks, um eine Verbindung zu einer Vielzahl von Web-Services herzustellen.   

Außerdem werden Echtzeitdaten auch in einem konfigurierbaren Dashboard in Form einer Übersicht über Position, Daten, Metriken und Alerts für Ihre IoT-Geräte angezeigt. 

![Die {{site.data.keyword.iotrtinsights_short}}-Architektur](images/iota.svg "{{site.data.keyword.iotrtinsights_short}}-Architektur")
