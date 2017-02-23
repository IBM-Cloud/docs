---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Geräte verbinden
{: #iotplatform_task}

Bevor Sie mit dem Empfang von Daten von Ihren IoT-Geräten beginnen können, müssen Sie sie mit {{site.data.keyword.iot_full}} verbinden. Um ein Gerät mit {{site.data.keyword.iot_short_notm}} zu verbinden, muss das Gerät für {{site.data.keyword.iot_short_notm}} registriert werden; die Registrierungsinformationen werden anschließend verwendet, um das Gerät für die Verbindung zu {{site.data.keyword.iot_short_notm}} zu konfigurieren.
{:shortdesc}

## Vorbereitende Schritte
{: #byb}

Vor dem Beginn des Verbindungsprozesses müssen Sie sicherstellen, dass Ihre Geräte für die Kommunikation mit {{site.data.keyword.iot_short_notm}} folgende Anforderungen erfüllen:

- Ihr Gerät muss in der Lage sein, unter Verwendung der HTTP- oder MQTT-Protokolle zu kommunizieren.
- Die Gerätenachrichten müssen den Anforderungen an die {{site.data.keyword.iot_short_notm}}-Nachrichtennutzdaten entsprechen.

Weitere Informationen finden Sie in [Entwickeln von Geräten in Watson IoT Platform](https://console.ng.bluemix.net/docs/services/IoT/devices/device_dev_index.html).

Führen Sie folgende Schritte aus, um für Ihr Gerät eine Verbindung zu {{site.data.keyword.iot_short_notm}} herzustellen.

## Schritt 1: Gerät mit {{site.data.keyword.iot_short_notm}} registrieren  
{: #iotplatform_subtask1}

Zum Registrieren eines Geräts gehört die Klassifizierung des Geräts als bestimmten Gerätetyp, das Benennen des Geräts und das Bereitstellen von Geräteinformationen. Anschließend stellen Sie ein Verbindungstoken bereit oder Sie akzeptieren ein Token, das von {{site.data.keyword.iot_short_notm}} generiert wird.

Sie können Geräte im {{site.data.keyword.iot_short_notm}}-Dashboard einzeln hinzufügen oder Sie können mit der [{{site.data.keyword.iot_short_notm}}-API](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Bulk_Operations/post_bulk_devices_add) ein Gerät oder gleichzeitig mehrere Geräte hinzufügen.

Gehen Sie wie folgt vor, um ein Gerät über das {{site.data.keyword.iot_short_notm}}-Dashboard hinzuzufügen:

1. Klicken Sie auf die Kachel des {{site.data.keyword.iot_short_notm}}-Service in Ihrem {{site.data.keyword.Bluemix}}-Dashboard, um das Service-Dashboard zu öffnen, oder rufen Sie die folgende URL auf, um direkt zum Dashboard zu wechseln:

 `https://Organisations-ID.internetofthings.ibmcloud.com/dashboard/#/overview `

    Dabei ist *Organisations-ID* die ID Ihrer {{site.data.keyword.Bluemix}}-Organisation.

2. Klicken Sie auf der Serviceseite auf **Dashboard starten**, um mit der Verwaltung Ihrer {{site.data.keyword.iot_short_notm}}-Organiation zu beginnen.

3. Wählen Sie im Dashboard 'Überblick' im Menüteilfenster die Option **Geräte** aus und klicken Sie anschließend auf **Gerät hinzufügen**.
5. Wählen oder erstellen Sie einen Gerätetyp für das Gerät, das Sie hinzufügen.  
Jedem Gerät, das mit {{site.data.keyword.iot_short_notm}} verbunden ist, muss ein Gerätetyp zugeordnet sein. Gerätetypen sind Gruppen von Geräten, denen allgemeine Merkmale gemeinsam sind.  
Wenn Sie Ihr erstes Gerät zur {{site.data.keyword.iot_short_notm}}-Organisation hinzufügen, stehen im Menü **Gerätetyp** keine Gerätetypen zur Verfügung. Sie müssen zunächst einen Gerätetyp erstellen:
 1. Klicken Sie auf **Gerätetyp erstellen**.
 2. Geben Sie einen Namen für den Gerätetypen, wie beispielsweise `my_device_type`, und eine Beschreibung des Gerätetyps ein.   
 **Wichtig:** Der Name des Gerätetyps darf maximal 36 Zeichen umfassen und nur folgende Zeichen enthalten:
 <ul>
  <li>Alphanumerische Zeichen (a-z, A-Z, 0-9)</li>
  <li>Bindestriche (-)</li>
  <li>Unterstreichungszeichen (&lowbar;)</li>
  <li>Punkte (.)</li>
  </ul>
 3. Optional: Geben Sie Attribute und Metadaten zu dem Gerätetyp ein.    
 **Tipp:** Sie können Attribute und Metadaten später hinzufügen und bearbeiten.
 4. Klicken Sie auf **Erstellen**, um den neuen Gerätetyp hinzuzufügen.
10. Klicken Sie auf **Weiter**, um mit dem Hinzufügen Ihres Geräts mit dem ausgewählten Gerätetyp zu beginnen.
11. Geben Sie eine Geräte-ID wie beispielsweise `my_first_device` ein.  
Die Geräte-ID wird zum Ermitteln des Geräts im {{site.data.keyword.iot_short_notm}}-Dashboard verwendet und ist auch ein erforderlicher Parameter für das Herstellen einer Verbindung zwischen Ihrem Gerät und {{site.data.keyword.iot_short_notm}}.  
**Wichtig:** Die Geräte-ID darf maximal 36 Zeichen umfassen und nur folgende Zeichen enthalten:
 <ul>
 <li>Alphanumerische Zeichen (a-z, A-Z, 0-9)</li>
 <li>Bindestriche (-)</li>
 <li>Unterstreichungszeichen (&lowbar;)</li>
 <li>Punkte (.)</li>  
 </ul>
 **Tipp:** Bei netzverbundenen Geräten kann die Geräte-ID beispielsweise die MAC-Adresse des Geräts ohne trennende Doppelpunkte sein.  
12. Optional: Klicken Sie auf **Zusätzliche Felder**, um Geräteeinformationen hinzuzufügen, wie beispielsweise Seriennummer, Hersteller, Modell usw.  
 **Tipp:** Sie können diese Informationen später hinzufügen und bearbeiten.
12. Optional: Geben Sie JSON-Metadaten zum Gerät ein.  
 **Tipp:** Sie können Metadaten zum Gerät später hinzufügen und bearbeiten.
13. Klicken Sie auf **Weiter**, um das Hinzufügen Ihres Geräts abzuschließen.
14. Überprüfen Sie, dass die Übersichtsinformationen richtig sind und klicken Sie anschließend auf **Hinzufügen**, um die Verbindung hinzuzufügen.  
**Tipp:** Sie haben die Option, ein automatisch generiertes Authentifizierungstoken zu akzeptieren oder selbst ein Authentifizierungstoken anzugeben.  
Wenn Sie ein eigenes Token erstellen möchten, stellen Sie sicher, dass es zwischen 8 und 36 Zeichen lang ist und nur aus alphanumerischen Zeichen und den folgenden Sonderzeichen besteht:
 - Bindestrich (-)
 - Unterstreichungszeichen (&lowbar;)
 - Ausrufezeichen (!)
 - Et-Zeichen (&)
 - kommerzielles A (@)
 - Fragezeichen (?)
 - Stern (\*)
 - Pluszeichen (+)
 - Punkt (.)
 - Rechte und linke Klammern  

 **Wichtig:** Das Token darf keine Folgen aus wiederholten Zeichen, Wörterbuchwörter, Benutzernamen oder andere vordefinierte Folgen enthalten.
15. Kopieren Sie auf der Seite mit den Geräteinformationen folgende Geräteinformationen und speichern Sie sie:  
 - Organisations-ID, wie beispielsweise `tubo8x`
 - Gerätetyp, wie beispielsweise `my_device_type`
 - Geräte-ID, wie beispielsweise `my_first_device`
 - Authentifizierungsmethode, wie beispielsweise `token`
 - Authentifizierungstoken, wie beispielsweise `PtBVriRqIg4uh)_-Kl`  
  **Tipp:** Sie benötigen die Organisations-ID, das Authentifizierungstoken, den Gerätetyp und die Geräte-ID, um Ihr Gerät für das Herstellen einer Verbindung zu {{site.data.keyword.iot_short_notm}} zu konfigurieren.  

Herzlichen Glückwunsch, Ihr Gerät wurde registriert. Sie können Ihr Gerät nun für das Herstellen einer Verbindung zu {{site.data.keyword.iot_short_notm}} konfigurieren.

## Schritt 2: Geräte mit {{site.data.keyword.iot_short_notm}} verbinden
{: #iotplatform_subtask2}

Nach dem Registrieren eines Geräts in {{site.data.keyword.iot_short_notm}}, können Sie die Registrierungsinformationen verwenden, um das Gerät zu verbinden und mit dem Empfang von Gerätedaten zu beginnen.

{{site.data.keyword.iot_short_notm}} unterstützt viele Gerätetypen. Der grundlegende Prozess zum Verbinden eines Geräts umfasst in der Regel folgende Schritte:
- Richten Sie Ihr Gerät für das MQTT-Messaging ein und verwenden Sie die Organisation-ID, das Authentifizierungstoken, den Gerätetyp und die Geräte-ID zur Authentifizierung.  
- Senden Sie mithilfe des MQTT-Protokolls Gerätenachrichten an Ihre {{site.data.keyword.iot_short_notm}}-Organisation.

**Tipp:** Für üblicherweise verwendete Geräte stehen viele Verbindungsanleitungen zur Verfügung. Lesen Sie die [Anleitungen für das Verbinden von Geräten](https://developer.ibm.com/recipes/tutorials/category/internet-of-things-iot/), die unter IBM.com zur Verfügung stehen.

Folgende Informationen sind zum Verbinden Ihrer Geräte erforderlich:
- URL: *Organisations-ID*.messaging.internetofthings.ibmcloud.com  
Dabei ist *Organisations-ID* die ID Ihrer {{site.data.keyword.iot_short_notm}}-Organisation.
- Port:
 - 1883
 - 8883 (verschlüsselt)
 - 443 (Websockets)
- Geräte-ID: d:*Orgnisations-ID*:*Gerätetyp*:*Geräte-ID*  
Mit dieser Kombination von Parametern wird Ihr Gerät eindeutig angegeben.
- Benutzername: use-token-auth  
Dieser Wert gibt an, dass Sie zur Autorisierung ein Token verwenden.
- Kennwort: *Authentifizierungstoken*  
Dieser Wert ist das eindeutige Token, das Sie definiert haben oder dass Ihrem Gerät bei der Registrierung zugewiesen wurde.
- Format des Ereignistopics: iot-2/evt/*Ereignis-ID*/fmt/*Format_Zeichenfolge*  
Dabei gibt *Ereignis-ID* den in {{site.data.keyword.iot_short_notm}} angezeigten Ereignisnamen an und *Format_Zeichenfolge* ist das Format des Ereignisses, zum Beispiel 'JSON'.
- Nachrichtenformat: JSON
   
 {{site.data.keyword.iot_short_notm}} unterstützt mehrere Formate wie beispielsweise JSON und 'text'.

Weitere Informationen zum Herstellen einer Verbindung für Ihr Gerät finden Sie in der technischen Dokumentation in [MQTT-Konnektivität für Geräte](devices/mqtt.html).
Der Abschnitt [Konnektivität](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Connectivity/post_device_types_deviceType_devices_deviceId_events_eventName) der API-Dokumentation enthält ebenfalls die erforderlichen Informationen.

## Anleitungen zum Verbinden von Geräten

Die folgenden Anleitungen beschreiben den Ablauf, der verwendet wird, um Geräte zu registrieren und mit Watson IoT Platform zu verbinden.

- [Geräte in IBM Watson IoT Platform registrieren](https://developer.ibm.com/recipes/tutorials/how-to-register-devices-in-ibm-iot-foundation/)

- [Raspberry Pi als Gerät mithilfe von Node-RED mit Watson IoT verbinden](https://developer.ibm.com/recipes/tutorials/deploy-watson-iot-node-on-raspberry-pi/)

- [Arduino Uno-Gerät mit IBM Watson IoT Platform verbinden](https://developer.ibm.com/recipes/tutorials/connect-an-arduino-uno-device-to-the-ibm-internet-of-things-foundation/)

- [Sense HAT mithilfe von Node-RED mit Watson IoT verbinden](https://developer.ibm.com/recipes/tutorials/connecting-a-sense-hat-to-watson-iot-using-node-red/)

- [Raspberry Pi mit Windows IoT Core als Gerät mit Watson IoT Platform verbinden](https://developer.ibm.com/recipes/tutorials/connecting-raspberry-pi-with-windows-iot-core-as-a-device-to-watson-iot-using-node-red/)
