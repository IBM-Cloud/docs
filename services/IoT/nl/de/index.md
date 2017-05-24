---

copyright:
  years: 2016, 2017
lastupdated: "2017-05-03"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Einführung in {{site.data.keyword.iot_short_notm}}
{: #gettingstartedtemplate}

{{site.data.keyword.iot_full}} für {{site.data.keyword.Bluemix_notm}} ist ein vielseitiges Toolkit, das Gateway-Geräte, Gerätemanagement und leistungsfähigen Anwendungszugriff zur Verfügung stellt. Durch Verwendung von {{site.data.keyword.iot_short_notm}} können Sie Daten zu verbundenen Geräten erfassen und Echtzeitdaten aus Ihrer Organisation analysieren.
{:shortdesc}

## Vorbereitende Schritte
{: #byb}

Bevor Geräte verbunden und Daten verwendet werden können, müssen Sie sich für ein {{site.data.keyword.Bluemix_notm}}-Konto registrieren und eine Instanz des {{site.data.keyword.iot_short_notm}}-Service in Ihrer {{site.data.keyword.Bluemix_notm}}-Organisation erstellen. Sie können eine {{site.data.keyword.iot_short_notm}}-Instanz direkt über die [{{site.data.keyword.iot_short_notm}}-Seite im Bluemix-Servicekatalog ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.{DomainName}/catalog/services/internet-of-things-platform/){:new_window} erstellen.  

Detaillierte Informationen zur Vorgehensweise beim Anmelden eines Kontos in {{site.data.keyword.Bluemix_notm}}, beim Konfigurieren von Regionen sowie andere Einstellungen für die Kontoverwaltung finden Sie in [Bluemix-Konto verwalten](https://console.ng.bluemix.net/docs/admin/account.html#signup).

Sie können Ihre {{site.data.keyword.iot_short_notm}}-Instanz im Dashboard einrichten und konfigurieren. Zum Öffnen des Dashboards wechseln Sie zu Ihrer Instanz des {{site.data.keyword.iot_short_notm}}-Service in {{site.data.keyword.Bluemix_notm}} und klicken Sie anschließend auf **Dashboard starten**.

## Schritt 1: Verbinden Sie Ihre Geräte
{: #up_and_running}

Um den Service betriebsbereit zu machen, müssen Sie folgende Optionen betrachten, deren Auswahl von Ihrer Situation abhängt:

   |   Service ist bereitgestellt | Service ist nicht bereitgestellt
  ------------- | -------------
  **Ich verfüge über ein Gerät, das ich verbinden kann** | [Verbinden Sie Ihr Gerät mit {{site.data.keyword.iot_short_notm}}](iotplatform_task.html#iotplatform_task).| Untersuchen Sie die Geräteverbindung in [Organisationsdemo wiedergeben ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://discover-iot.eu-gb.mybluemix.net/?cm_mc_uid=44491599487314618721024&cm_mc_sid_50200000=1462798151#/play){:new_window}.
  **Ich verfüge nicht über ein Gerät, das ich verbinden kann** | [Erstellen und verbinden Sie einen Node-RED-Gerätesimulator](nodereddevice_sample.html){:new_window}. | Beginnen Sie mit [Watson IoT Platform Starter](https://console.ng.bluemix.net/docs/starters/IoT/iot500.html).
eitere Informationen zur Vorgehensweise beim Verbinden bestimmter Gerätetypen mit {{site.data.keyword.iot_short_notm}} finden Sie in [developerWorks-Anleitungen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/recipes/tutorials/category/internet-of-things-iot/){:new_window}.  

Entwicklerdokumentation für Geräteverbindungen siehe
- [MQTT-Konnektivität für Geräte](devices/mqtt.html).
- [MQTT-Konnektivität für Gateways](gateways/mqtt.html).

## Schritt 2: Analysieren Sie Ihre Gerätedaten
{: #analyzing_data}

Beginnen Sie mit der Durchsicht der Echtzeitdaten, die die Geräte an {{site.data.keyword.iot_short_notm}} senden.

{{site.data.keyword.iot_short_notm}} schließt folgende Analysetools ein:  
- [Boards und Karten](data_visualization.html) zum Visualisieren Ihrer Gerätedaten in Echtzeit.
- [Regeln und Aktionen](analytics.html), die von Gerätedaten in Echtzeit ausgelöst werden.

Ein schnelles Einführungsbeispiel finden Sie in der developerWorks-Anleitung [Regeln und Aktionen mit IBM Watson IoT Platform Cloud Analytics verwenden ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/recipes/tutorials/using-rules-and-actions-with-ibm-watson-iot-platform-cloud-analytics/){:new_window}.

## Schritt 3: Erstellen Sie Anwendungen, mit denen Ihre Gerätedaten verarbeitet werden
{: #develop_applications}

Erweitern Sie die Datenanalysefunktionen von {{site.data.keyword.iot_short_notm}}, indem Sie Ihre eigenen Anwendungen erstellen und verbinden, mit denen Echtzeitdaten von Geräten und archivierte Gerätedaten verarbeitet werden können.

Weitere Informationen finden Sie in den folgenden Abschnitten:   
- Lesen Sie die [Dokumentation für Anwendungsentwickler](applications/api.html) und die [{{site.data.keyword.iot_short_notm}}-API-Dokumentation](reference/api.html).
- Lesen Sie die [{{site.data.keyword.iot_short_notm}}-Clientbibliotheken](iot_platform_client_lib.html), die Tools und Dateien zum Erstellen und Entwickeln von Code für die Integration und das Verbinden Ihrer Geräte und Anwendungen bereitstellen.
- [{{site.data.keyword.cloudantfull}}-Service](cloudant_connector.html) mit Ihrer {{site.data.keyword.iot_short_notm}}-Instanz verbinden, um Langzeitdaten zum Gerät zu speichern.
