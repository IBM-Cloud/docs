---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-10"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Informationen zu {{site.data.keyword.iotelectronics}}
{: #iotelectronics_about}

Bei {{site.data.keyword.iotelectronics_full}} handelt es sich um eine integrierte IoT-Produktionsinstanz, mit der Ihre Apps mit Ihren verbundenen Appliances, Sensoren und Gateways kommunizieren und Daten verarbeiten können, die über diese Komponenten erfasst werden.
{:shortdesc}

{{site.data.keyword.iotelectronics}} nutzt für die Herstellung einer Verbindung zwischen Ihren smarten elektronischen Appliances und den von Ihnen entwickelten Anwendungen den Service {{site.data.keyword.iot_full}}. Außerdem wird {{site.data.keyword.iot_short_notm}} für Ihre Unterstützung bei der Analyse und dem Einblick in die Daten aus Ihren Appliances verwendet. Sie können Regeln erstellen, damit Bedingungen ermittelt werden können, die Ihrer Aufmerksamkeit bedürfen, und um automatische Antworten zu definieren, z. B. das Senden von E-Mails, das Ausführen eines Node-RED-Workflows oder das Herstellen einer Verbindung zu Web-Services.

## Starter suchen
{: #iot4eFindingStarter}
Der {{site.data.keyword.iotelectronics}}-Starter befindet sich im [Abschnitt 'Boilerplates'](https://console.{DomainName}/catalog/starters/iot-for-electronics-starter/) des {{site.data.keyword.Bluemix_notm}}-Katalogs.

## Wie {{site.data.keyword.iotelectronics}} genutzt werden kann
{: #Features_iote}
Mithilfe simulierter Appliances und Daten können Sie die Features der {{site.data.keyword.iotelectronics}}-Lösung rasch und unkompliziert kennenlernen.

### Simulierte Appliances verbinden
Sie können simulierte Appliances erstellen und diese mit der Plattform verbinden, um Live-Stream-Daten anzuzeigen. Mithilfe einer webbasierten App können Sie den Empfang von Befehlen und die Durchführung von Operationen für eine Appliance simulieren. Für die Generierung von Anmerkungen und Alerts können Sie Fehler simulieren. Zu Demonstrationszwecken werden Waschmaschinen als simulierte Appliances für den {{site.data.keyword.iotelectronics}}-Starter verwendet. Die von Ihnen zur Herstellung einer Verbindung ausgewählte Appliance kann ein beliebiger Typ von intelligentem Elektronikgerät sein.

### Beispiel für eine mobile Nutzer-App ausprobieren
Wenn Sie ein mobiles iOS-oder Android-Gerät verwenden, können Sie sehen, wie ein Applianceeigner mit der Appliance interagieren kann. Über die Plattform und mithilfe von {{site.data.keyword.Bluemix_notm}} können Sie Befehle an die Appliance senden und Aktualisierungen aus der Appliance empfangen. Sie können Fehlerereignisse simulieren und die Ergebnisse in der mobilen App anzeigen.

### Eigene elektronische Appliances verbinden
Sie können Ihre eigenen Appliances sicher mit der Cloud verbinden und mit der Anpassung Ihrer eigenen Apps beginnen. Es ist eine Reihe geprüfter Beispiele und Anleitungen verfügbar, die Sie ändern und als Machbarkeitsnachweise, zu Testzwecken und für Versuchsreihen einsetzen können.

## Neuerungen für den {{site.data.keyword.iotelectronics}}-Starter
{: #whatsInStarter}
Die Boilerplate für Starter stellt die integrierte {{site.data.keyword.iotelectronics}}-Lösung bereit.  Alle Komponenten werden für Sie automatisch gebunden und bereitgestellt. Mithilfe simulierter Appliances und Daten können Sie über die Starter-App die Features der Lösung schnell und unkompliziert kennenlernen. Das Beispiel der mobilen App verdeutlicht, wie ein Nutzer die Registrierung durchführen, Alerts empfangen und eine verbundene Appliance steuern kann. Sie können die Beispiele als Ausgangspunkte für die Erstellung eigener Anwendungen und für das Erfassen von Daten aus Ihren eigenen Appliances verwenden. Die Lösung enthält die folgenden Services und Anwendungen:

![{{site.data.keyword.iotelectronics}}-Architektur. Dieses Diagramm wird im Textkörper des Themas beschrieben.](images/IoT4E_architecture.svg "{{site.data.keyword.iotelectronics}}-Architektur")

Der {{site.data.keyword.iotelectronics}}-Starter nutzt den {{site.data.keyword.iotelectronics}}-Service und die APIs zur Herstellung einer Verbindung mit {{site.data.keyword.iot_short_notm}}. Die Starter-App und das Beispiel für die mobile App kommunizieren mit dem {{site.data.keyword.iotelectronics}}-Service und sind miteinander durch {{site.data.keyword.amafull}} verbunden. Die folgenden Komponenten sind im Starter enthalten:

Der **{{site.data.keyword.iotelectronics}}-Service** unterstützt die Benutzer- und Applianceregistrierung und Benachrichtigungsvorgänge.

Mit **{{site.data.keyword.iot_full}}** können Ihre Apps mit Ihren verbundenen Appliances, Sensoren und Gateways kommunizieren und Daten verarbeiten, die über diese Komponenten erfasst werden.

<!-- **{{site.data.keyword.iotrtinsights_full}}** enables you to enrich and monitor data from your appliances, visualize what's happening now, and respond to emerging conditions by using automated actions. -->

**{{site.data.keyword.amafull}}** ermöglicht Benutzern mobiler Apps die Anmeldung mithilfe bereits vorhandener Social Media-Konten und garantiert eine sichere Kommunikation mit Back-End-Systemen.

Mit **{{site.data.keyword.sdk4nodefull}}** können Sie serverseitige JavaScript&reg;-Apps entwickeln, bereitstellen und skalieren; außerdem bietet Ihnen diese Software erweiterte Leistung, Sicherheit und Funktionsfähigkeit.

Mit dem **Beispiel für eine mobile App** können Sie über Ihr Mobilgerät wie ein Smartphone oder ein Tablet den Status einer simulierten Appliance anzeigen und mit einer solchen kommunizieren. Unter [Verwenden der mobilen App](iotelectronics_config_mobile.html) finden Sie heraus, wie Sie die mobile App abrufen können.
