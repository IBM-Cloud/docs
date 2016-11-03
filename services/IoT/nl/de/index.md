---

copyright:
  years: 2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Einführung in {{site.data.keyword.iot_short_notm}} 
{: #gettingstartedtemplate}
Letzte Aktualisierung: 26. August 2016
{: .last-updated}

{{site.data.keyword.iot_full}} für {{site.data.keyword.Bluemix_notm}} ist ein vielseitiges Toolkit, das Gateway-Geräte, Gerätemanagement und leistungsfähigen Anwendungszugriff zur Verfügung stellt. Durch Verwendung von {{site.data.keyword.iot_short_notm}} können Sie Daten zu verbundenen Geräten erfassen und Echtzeitdaten aus Ihrer Organisation analysieren.
{:shortdesc}

## Vorbereitende Schritte 
{: #byb}

Bevor Geräte verbunden und Daten verwendet werden können, muss in Ihrer {{site.data.keyword.Bluemix_notm}}-Organisation ein {{site.data.keyword.iot_short_notm}}-Service vorhanden sein. Sie können ihn direkt über die [{{site.data.keyword.iot_short_notm}}-Seite im Servicekatalog von Bluemix](https://console.{DomainName}/catalog/services/internet-of-things-platform/) erstellen.   

## Schritt 1: Verbinden Sie Ihre Geräte 
{: #up_and_running}

Um den Service betriebsbereit zu machen, müssen Sie folgende Optionen, deren Auswahl von Ihrer Situation abhängt: 

   |   Service ist bereitgestellt  | Service ist nicht bereitgestellt
  ------------- | -------------
  **Ich verfüge über ein Gerät, das ich verbinden kann**  | [Verbinden Sie Ihr Gerät mit {{site.data.keyword.iot_short_notm}}](iotplatform_task.html#iotplatform_task). | Untersuchen Sie die Geräteverbindung in [Organisationsdemo wiedergeben](http://discover-iot.eu-gb.mybluemix.net/?cm_mc_uid=44491599487314618721024&cm_mc_sid_50200000=1462798151#/play){:new_window}.
**Ich verfüge nicht über ein Gerät, das ich verbinden kann**  | [Erstellen und verbinden Sie einen Node-RED-Gerätesimulator](nodereddevice_sample.html){:new_window}.  | Beginnen Sie mit [Watson IoT Platform Starter](https://new-console.stage1.ng.bluemix.net/docs/starters/IoT/iot500.html){:new_window}.
Weitere Informationen zur Vorgehensweise beim Verbinden bestimmter Gerätetypen mit {{site.data.keyword.iot_short_notm}} finden Sie in [developerWorks Recipes](https://developer.ibm.com/recipes/?post_type=tutorials&s=iot){:new_window}.   

Entwicklerdokumentation für Geräteverbindungen siehe 
- [MQTT-Konnektivität für Geräte](devices/mqtt.html). 
- [MQTT-Konnektivität für Gateways](gateways/mqtt.html). 

## Schritt 2: Analysieren Sie Ihre Gerätedaten 
{: #analyzing_data}

Beginnen Sie mit der Durchsicht der Echtzeitdaten, die die Geräte an {{site.data.keyword.iot_short_notm}} senden. 

{{site.data.keyword.iot_short_notm}} schließt folgende Analysetools ein:   
- [Boards und Karten](data_visualization.html) zum Visualisieren Ihrer Gerätedaten in Echtzeit. 
- [Regeln und Aktionen](analytics.html), die von Gerätedaten in Echtzeit ausgelöst werden. 

Ein schnelles Einführungsbeispiel finden Sie in der developerWorks-Anleitung [Using Rules and Actions with IBM Watson IoT Platform Cloud Analytics](https://developer.ibm.com/recipes/tutorials/using-rules-and-actions-with-ibm-watson-iot-platform-cloud-analytics/){:new_window}. 

## Schritt 3: Erstellen Sie Anwendungen, mit denen Ihre Gerätedaten verarbeitet werden 
{: #develop_applications}

Erweitern Sie die Datenanalysefunktionen von {{site.data.keyword.iot_short_notm}}, indem Sie Ihre eigenen Anwendungen erstellen und verbinden, mit denen Echtzeitdaten von Geräten und archivierte Gerätedaten verarbeitet werden können. 

Weitere Informationen finden Sie in den folgenden Abschnitten:    
- Lesen Sie die [Dokumentation für Anwendungsentwickler](applications/api.html) und die [{{site.data.keyword.iot_short_notm}}-API-Dokumentation](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#/){:new_window}. 
- Lesen Sie die [{{site.data.keyword.iot_short_notm}}-Clientbibliotheken](iot_platform_client_lib.html), die Tools und Dateien zum Erstellen und Entwickeln von Code für die Integration und das Verbinden Ihrer Geräte und Anwendungen bereitstellen. 
- [{{site.data.keyword.cloudantfull}}-Service](cloudant_connector.html) mit Ihrer {{site.data.keyword.iot_short_notm}}-Instanz verbinden, um Langzeitdaten zum Gerät zu speichern. 




# Zugehörige Links 
{: #rellinks}
## Lernprogramme und Beispiele 
{: #samples}
* [Anleitungen für das Verbinden Ihrer Geräte](https://developer.ibm.com/recipes/?post_type=tutorials&s=iot){:new_window} 
* [{{site.data.keyword.iot_short_notm}}-Organisation zum Spielen](https://play.internetofthings.ibmcloud.com/){:new_window} 
* [Intel Galileo mit {{site.data.keyword.iot_short_notm}} verbinden](https://developer.ibm.com/recipes/tutorials/connect-an-intel-galileo-to-the-internet-of-things-foundation-connect/){:new_window} 
* [ARM® mbed™ IoT Starter Kit verbinden](https://developer.ibm.com/recipes/tutorials/arm-mbed-iot-starter-kit-part-1/){:new_window} 
* [Raspberry Pi mit {{site.data.keyword.iot_short_notm}} verbinden](https://developer.ibm.com/recipes/tutorials/raspberry-pi-4/){:new_window} 

## API-Referenz 
{: #api}
* [{{site.data.keyword.iot_short_notm}}-API-Dokumentation](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#/){:new_window} 
* [Entwicklerdokumentation](developer_doc_overview.html) 
