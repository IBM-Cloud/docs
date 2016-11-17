---

copyright:
  years: 2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.iot_short_notm}}-Funktionen - Überblick
{: #feature_overview}

Letzte Aktualisierung: 29. Juni 2016
{: .last-updated}

{{site.data.keyword.iot_full}} gründet sich auf folgende Schlüsselbereiche:

  1. Connect - Verbinden von Geräten und Entwickeln von Anwendungen.
  2. Information Management - Speichern und Überprüfen von Gerätedaten und Integration von {{site.data.keyword.iot_short_notm}} mit anderen Services.
  3. Analytics - Visualisieren von Gerätedaten in Echtzeit durch Verwendung des {{site.data.keyword.iot_short_notm}}-Dashboards.
  4. Risk Management - Konfigurieren einer sicheren Konnektivität und Architektur mit Zugriffssteuerung für Benutzer und Anwendungen.

## Connect
{: #connect}

{{site.data.keyword.iot_short_notm}} Connect ('Verbindung herstellen') ist der Ausgangspunkt aller {{site.data.keyword.iot_short_notm}}-Services. Unter {{site.data.keyword.iot_short_notm}} Connect stehen das Herstellen von Verbindungen für Geräte, das Erstellen von Anwendungen, die Steuerung Ihrer Geräte und die Interaktion mit Services von Drittanbietern zur Verfügung.

### Gateway-Geräte

Durch Verwendung eines Gateways können Sie für Geräte Verbindungen zu {{site.data.keyword.iot_short_notm}} herstellen, die andernfalls keine Verbindung zum Internet herstellen könnten. Gateway-Geräte kombinieren die Funktionen eines Geräts und einer Anwendung. Gateways können ebenso wie ein Gerät Befehle empfangen und Gerätedaten senden; sie können aber auch in gleicher Weise wie Anwendungen Befehle an andere Geräte senden, die mit ihnen verbunden sind.

Geräte, die nicht direkt mit dem Internet verbunden werden können, können mit einem Gateway-Gerät verbunden werden und ihre Gerätedaten können an das Gateway-Gerät gesendet werden, das sie wiederum an Ihren {{site.data.keyword.iot_short_notm}}-Service senden kann.

### Gerätemanagement

Gerätemanagementfunktionen können über die Kombination aus Gerätemanagement-API und einem für Geräte installierten Gerätemanagementagenten bereitgestellt werden. Verwaltete Geräte können Gerätemanagementaktionen ausführen, die über das Hauptdashboard von {{site.data.keyword.iot_short_notm}} ausgelöst werden können.

Das Gerätemanagement gibt Ihnen die Möglichkeit, über die {{site.data.keyword.iot_short_notm}}-Benutzerschnittstelle einen Neustart auszuführen, Firmware-Updates herunterzuladen und zu installieren sowie Geräte über Fernzugriff auf Werkseinstellungen zurückzusetzen.

### Integration von Services von Drittanbietern

Die Integration von Services von Drittanbietern ist in {{site.data.keyword.iot_short_notm}} eingebettet und umfasst Unterstützung für standortbezogene Wetterservices von 'The Weather Company', die Ihnen ermöglichen, das aktuelle Wetter an einer Geräteposition zu ermitteln.

---

## Information Management
{: #information_management}

{{site.data.keyword.iot_short_notm}} Information Management ('Informationsmanagement') steuert die Daten, die von Geräten gesendet werden, nachdem sie Ihren {{site.data.keyword.iot_short_notm}}-Service erreicht haben. Zum Informationsmanagement gehört die Datenspeicherung und die Umwandlung von Daten.

### Cache für zuletzt gemeldete Ereignisse des Geräts

Durch Verwendung der {{site.data.keyword.iot_short_notm}}-API für zuletzt gemeldete Ereignisse können Sie das zuletzt von einem Gerät gesendete Ereignis abrufen. Dies funktioniert unabhängig davon, ob das Gerät online oder offline ist, wodurch Sie den Gerätestatus unabhängig vom physischen Standort des Geräts oder dem Status seiner Verwendung abrufen können. Daten zum letzten Ereignis eines Geräts können für jedes Ereignis abgerufen werden, das nicht später als 365 Tage zurückliegt.

### Datenspeicherung von Geräteereignissen

Geräteereignisdaten von Ihrem {{site.data.keyword.iot_short_notm}}-Service können zur späteren Verwendung gespeichert werden. Die Datenspeicherung ist ein wichtiger erster Schritt zur Ausführung einer fundierten Analyse, um über diese Daten Einblick zu gewinnen.  Sie können beispielsweise Änderungen über große Zeiträume verfolgen und Datengruppen für die Verwendung mit leistungsfähigen Analysetools speichern, einschließlich Verwendung von Watson-APIs und der kognitiven Datenverarbeitung.

---

## Analytics
{: #analytics}

### Echtzeitdaten von Geräten visualisieren

Sie können mithilfe von Dashboardkarten Gerätedaten in Echtzeit visualisieren und anzeigen. Dashboardkarten überwachen Gerätedaten in Echtzeit und zeigen diese an, wodurch Sie wichtige Geräte oder Gerätedaten verfolgen können. Diese Visualisierungen werden im Hauptdashboard von {{site.data.keyword.iot_short_notm}} angezeigt, um Ihnen einen schnellen Zugriff auf den Kontext und den Status von Gerätedaten in Echtzeit zu ermöglichen.

---

## Risikomanagement
{: #risk_management}

### Sichere Konnektivität und Architektur

Die Architektur von {{site.data.keyword.iot_short_notm}} wurde so entworfen, dass es Geräten nicht möglich ist, die Identität eines anderen Geräts anzunehmen, wodurch die Integrität Ihrer Gerätedaten gewahrt bleibt. Geräte stellen zu {{site.data.keyword.iot_short_notm}} eine Verbindung über eine Kombination aus einer Client-ID und einem Authentifizierungstoken her, das nur Ihnen bekannt ist. Nach der Registrierung der Geräte oder der Generierung der API-Schlüssel, wird das Authentifizierungstoken zufalls- und hashverschlüsselt, um die Sicherheit Ihrer Berechtigungsnachweise aufrecht zu erhalten. Die Konnektivität über TLS Version 1.2 wird vollständig unterstützt.

---
