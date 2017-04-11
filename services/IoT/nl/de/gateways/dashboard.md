---

copyright:

years: 2015, 2017

lastupdated: "2017-03-16"


---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Gateways verbinden
{: #IoT_connectGateway}

Bevor Sie beginnen können, Daten von Geräten zu empfangen, die mit Ihren Gateways verbunden sind, müssen Sie das Gateway mit {{site.data.keyword.iot_full}} verbinden. Zum Herstellen einer Verbindung zwischen einem Gateway und {{site.data.keyword.iot_short_notm}} gehört die Erstellung eines Gateway-Gerätetyps und die Registrierung des Gateways in {{site.data.keyword.iot_short_notm}}. Sie können die Registrierungsinformationen anschließend verwenden, um das Gateway mit {{site.data.keyword.iot_short_notm}} zu verbinden.
{:shortdesc}

Gateways sind in {{site.data.keyword.iot_short_notm}} eine besondere Geräteklasse. Gateways dienen anderen Geräten als Zugangspunkt für {{site.data.keyword.iot_short_notm}}.


## Vorbereitende Schritte
{: #Prerequisites}

Gateway-Geräte haben im Vergleich zu regulären Geräten zusätzliche Berechtigungen und können folgende Funktionen ausführen:
- Registrieren neuer Geräte in {{site.data.keyword.iot_short_notm}}
- Senden und Empfangen der eigenen Sensordaten wie ein direkt verbundenes Gerät
- Senden und Empfangen von Daten im Namen der mit ihnen verbundenen Geräte
- Ausführen eines Gerätemanagementagenten, sodass sie ebenso wie die verbundenen Geräte verwaltet werden können  
Informationen für Gateway-Entwickler finden Sie in [MQTT-Konnektivität für Gateways](mqtt.html).

Sie können Gateways auch verwenden, um Edge Analytics für die Daten auszuführen, die die Gateway-Geräte senden. Weitere Informationen finden Sie in [Edge Analytics](../edge_analytics.html) und [Edge Analytics-Agent installieren](#edge).

## Schritt 1: Gateway in {{site.data.keyword.iot_short_notm}} registrieren  
{: #register_gateway}

Zum Registrieren eines Gateways gehört die Klassifizierung des Geräts als Gateway-Typ, das Benennen des Gateways und das Angeben von Gateway-Informationen. Anschließend stellen Sie ein Verbindungstoken bereit oder Sie akzeptieren ein Token, das von {{site.data.keyword.iot_short_notm}} generiert wird.


**Tipp:** Sie können Gateways im {{site.data.keyword.iot_short_notm}}-Dashboard einzeln hinzufügen oder Sie können mit der [Organisationsadministrations-API ![Symbol für externen Link](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/orgAdmin.html#!/Device_Bulk_Configuration/post_bulk_devices_add){: new_window} ein Gateway oder gleichzeitig mehrere Gateways hinzufügen.

Gehen Sie wie folgt vor, um ein Gateway über das {{site.data.keyword.iot_short_notm}}-Dashboard hinzuzufügen:

1. Wählen Sie im {{site.data.keyword.iot_short_notm}}-Dashboard die Option **Geräte** aus.
2. Klicken Sie auf **Gerät hinzufügen**.
3. Wählen oder erstellen Sie einen Gerätetyp für das Gerät, das Sie hinzufügen.  
Jedem Gerät, das mit {{site.data.keyword.iot_short_notm}} verbunden ist, muss ein Gerätetyp zugeordnet sein. Gerätetypen sind Gruppen von Geräten, denen allgemeine Merkmale gemeinsam sind.  
 1. Klicken Sie auf **Gerätetyp erstellen** und anschließend auf **Gateway-Typ erstellen**.
 2. Geben Sie einen Namen für den Gerätetyp, wie beispielsweise `my_gateway_type`, und eine Beschreibung des Gateway-Typs ein.   
 **Wichtig:** Der Name des Gerätetyps darf maximal 36 Zeichen umfassen und nur folgende Zeichen enthalten:
 <ul>
  <li>Alphanumerische Zeichen (a-z, A-Z, 0-9)</li>
  <li>Bindestriche (-)</li>
  <li>Unterstreichungszeichen (&lowbar;)</li>
  <li>Punkte (.)</li>
  </ul>3. Optional: Geben Sie Attribute und Metadaten zu dem Gateway-Typ ein.    
 **Tipp:** Sie können Attribute und Metadaten später hinzufügen und bearbeiten.
 4. Klicken Sie auf **Erstellen**, um den neuen Gateway-Typ hinzuzufügen.
10. Klicken Sie auf **Weiter**, um mit dem Hinzufügen Ihres Gateway-Geräts mit dem ausgewählten Gateway-Typ zu beginnen.
11. Geben Sie eine Geräte-ID, wie beispielsweise `my_gateway_device`, ein.  
Die Geräte-ID wird zum Ermitteln des Gateway-Geräts im {{site.data.keyword.iot_short_notm}}-Dashboard verwendet und ist auch ein erforderlicher Parameter für das Herstellen einer Verbindung zwischen Ihrem Gateway-Gerät und {{site.data.keyword.iot_short_notm}}.  
**Wichtig:** Die Geräte-ID darf maximal 36 Zeichen umfassen und nur folgende Zeichen enthalten:
 <ul>
 <li>Alphanumerische Zeichen (a-z, A-Z, 0-9)</li>
 <li>Bindestriche (-)</li>
 <li>Unterstreichungszeichen (&lowbar;)</li>
 <li>Punkte (.)</li>  
 </ul>
 **Tipp:** Bei netzverbundenen Geräten kann die Geräte-ID beispielsweise die MAC-Adresse des Geräts ohne trennende Doppelpunkte sein.  
12. Optional: Klicken Sie auf **Zusätzliche Felder**, um Informationen zum Gateway-Gerät hinzuzufügen, wie beispielsweise Seriennummer, Hersteller, Modell usw.  
 **Tipp:** Sie können diese Informationen später hinzufügen und bearbeiten.
12. Optional: Geben Sie JSON-Metadaten zum Gerät ein.  
 **Tipp:** Sie können Metadaten zum Gerät später hinzufügen und bearbeiten.
13. Klicken Sie auf **Weiter**, um das Hinzufügen Ihres Gateway-Geräts abzuschließen.
14. Überprüfen Sie, dass die Übersichtsinformationen richtig sind und klicken Sie anschließend auf **Hinzufügen**, um das Gateway-Gerät hinzuzufügen.  
**Tipp:** Sie haben die Option, ein automatisch generiertes Authentifizierungstoken zu akzeptieren oder selbst ein Authentifizierungstoken anzugeben. Wenn Sie auswählen, ein eigenes Token zu erstellen, müssen Sie sicherstellen, dass es eine Länge von 8-36 Zeichen hat, aus einer Mischung von Groß- und Kleinbuchstaben, Zahlen, und Bindestrichen, Unterstreichungszeichen oder Punkten besteht. Das Token darf keine Folgen aus wiederholten Zeichen, Wörterbuchwörter, Benutzernamen oder andere vordefinierte Folgen enthalten.
15. Kopieren Sie auf der Seite mit den Geräteinformationen folgende Geräteinformationen und speichern Sie sie:  
 - Organisations-ID, wie beispielsweise `tubo8x`
 - Gerätetyp, wie beispielsweise `my_gateway_type`
 - Geräte-ID. **Tipp:** Bei netzverbundenen Geräten kann dies beispielsweise die MAC-Adresse ohne trennende Doppelpunkte sein.
 - Authentifizierungsmethode, wie beispielsweise `token`
 - Authentifizierungstoken, wie beispielseise `PtBVriRqIg4uh)_-Kl`  
  **Tipp:** Sie benötigen die Organisations-ID, das Authentifizierungstoken, den Gerätetyp und die Geräte-ID, um Ihr Gerät für das Herstellen einer Verbindung zu {{site.data.keyword.iot_short_notm}} zu konfigurieren.  

Herzlichen Glückwunsch, Ihr Gateway-Gerät wurde registriert. Sie können Ihr Gateway-Gerät nun für das Herstellen einer Verbindung zu {{site.data.keyword.iot_short_notm}} konfigurieren.

Die Anleitung [Gateways in IBM Watson IoT Platform registrieren ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/recipes/tutorials/how-to-register-gateways-in-ibm-watson-iot-platform/){:new_window} enthält eine Erläuterung der erforderlichen Schritte zum Registrieren eines Gateways.

## Schritt 2: Verbinden des Gateways mit {{site.data.keyword.iot_short_notm}}
{: #connect_gateway}

Nach dem Registrieren eines Gateways in {{site.data.keyword.iot_short_notm}} verwenden Sie die Registrierungsinformationen, um für das Gateway eine Verbindung zu {{site.data.keyword.iot_short_notm}} herzustellen und mit dem Empfang von Daten zu beginnen, die von Geräten stammen, die mit dem Gateway verbunden sind.

Informationen zum Herstellen einer Verbindung zu {{site.data.keyword.iot_short_notm}} finden Sie in [MQTT-Konnektivität für Gateways](mqtt.html).

**Tipp:** Es gibt eine Reihe von Anleitungen, die für das Herstellen einer Verbindung zwischen Geräten und {{site.data.keyword.iot_short_notm}} zur Verfügung stehen. Lesen Sie die [Anleitungen für das Verbinden von Geräten ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/recipes/tutorials/category/internet-of-things-iot/){:new_window}, die unter IBM.com zur Verfügung stehen.


## Schritt 3: Verbinden der Geräte über das Gateway
{: #gateway_devices}

Geräte, die mit dem Gateway verbunden sind, werden automatisch zu {{site.data.keyword.iot_short_notm}} hinzugefügt, wenn das Gateway Nachrichten publiziert, die vom Gerät stammen. Sowohl der Gerätetyp als auch das Gerät selbst werden automatisch erstellt, wenn das Gateway eine Nachricht für eine Kombination aus Gerätetyp und Geräte-ID publiziert, die nicht bereits vorhanden ist.

Informationen zur automatischen Registrierung des Geräts und zum Publizieren und Empfangen von Daten für verbundene Geräte finden Sie in [MQTT-Konnektivität für Gateways](mqtt.html).


Wenn ein Gerät erfolgreich mit Ihrem Gateway verbunden wurde, wird es im Dashboard Ihrer {{site.data.keyword.iot_short_notm}}-Organisation angezeigt.

Die Anleitung [Raspberry Pi als Gateway mit Watson IoT verbinden ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/recipes/tutorials/connecting-raspberry-pi-as-a-gateway-to-watson-iot-using-node-red/){:new_window} enthält eine schrittweise Erläuterung des Ablaufs.

**Hinweis:** Für Geräte und Gateways, die direkt mit {{site.data.keyword.iot_short_notm}} verbunden sind, wird im {{site.data.keyword.iot_short_notm}}-Dashboard ein Statussymbol angezeigt, mit dem angegeben wird, dass sie verbunden sind. Das Dashboard zeigt Geräte, die über ein Gateway indirekt verbunden sind, als nicht verbunden an, da es keine Kenntnis der Konnektivität von Geräten zum Gateway hat.


## Edge Analytics-Agent installieren
{: #edge}

Der Edge Analytics-Agent (EAA) ist eine Softwarekomponente, die auf der Grundlage einer für die Edge-Verarbeitung optimierten Streaming-Engine erstellt wurde, um Edge Analytics-Operationen für ein Gateway auszuführen, indem Edge Analytics-Regeln aus dem {{site.data.keyword.iot_short_notm}}-Dashboard hochgeladen und verwaltet werden. Weitere Informationen zu Edge Analytics finden Sie in [Edge Analytics](../edge_analytics.html).

### Edge Analytics-Agenten (EAA) installieren
{: #eaa_install}

Gehen Sie wie folgt vor, um den Edge Analytics-Agenten in Ihrem Gateway zu installieren:
1. Wechseln Sie im {{site.data.keyword.iot_short}}-Dashboard zu **Regeln**.
2. Klicken Sie auf **Edge-Agenten herunterladen**, um zur [IBM Edge Analytics-Community ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/developerworks/community/groups/service/html/communitystart?communityUuid=3df173af-0c21-4b9c-9fd1-e8e5561ef460&ftHelpTip=true){:new_window} zu wechseln.
3. Navigieren Sie zum Abschnitt **Dateien** und laden Sie die passenden komprimierten Verzeichnisse für Ihren Typ von Gateway herunter.  
Die Edge Analytics-Lösung ist als SDK für Geräte, die Java unterstützen, oder als DSLink für Cisco-Gateway-Einheiten verfügbar. 
4. Informationen zur Vorgehensweise, wie die EAA-Softwarekomponente in Ihrem Gateway installiert und konfiguriert wird, finden Sie in den folgenden Informationen:
 - SDK  
 Lesen Sie die PDF- und Readme-Dateien und sehen Sie sich die verlinkten Videos an, die in der Community verfügbar sind.  
 Die [Edge-Anleitung für SDK - Einführung (SDK) ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/recipes/tutorials/getting-started-with-the-ibm-edge-analytics-sdk-in-watson-iot-platform/){:new_window}.
 - DSLink  
 Die Anleitung [Einführung in Edge Analytics in Watson IoT Platform ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/recipes/?post_type=pnext_tutorial&p=19472){:new_window}.

### Konfigurationseinstellungen für den Edge Analytics-Agent (EAA)
{: #eaa_configuration}

Sie können die für EAA geltende config.properties-Datei verwenden, um Konfigurationsparameter für die Basissoftware festzulegen.

Gehen Sie wie folgt vor, um die EAA-Konfiguration zu aktualisieren:
1. Suchen Sie in dem Gateway-System, auf dem der EAA ausgeführt wird, die EAA-Datei 'config.properties'.  
Beispiel:
`../dglux-server/dslinks/ibm-watson-iot-edge-analytics-dslink-java-0.0.1/config.properties`
2. Erstellen Sie vor dem Bearbeiten der Einstellungen eine Sicherungskopie der Datei.
3. Öffnen Sie die config.properties-Datei zur Bearbeitung.
4. Bearbeiten Sie die Konfigurationsparameter für Ihre Umgebung:
 <dl>
 <dt>DataDirectSendEnable</dt>
 <dd>BOOLEAN (true|false)</br>
 TRUE (default) - Alle Daten an {{site.data.keyword.iot_short_notm}} senden.</br>
 FALSE - Nur Daten an {{site.data.keyword.iot_short_notm}} senden, wenn für die Engine Regeln festgelegt wurden. </dd>
 <dt>MonitorInterval</dt>
 <dd>INTEGER (in Millisekunden)</br>
 Die Zeit in Millisekunden, die verstreicht, bis eine neue Überwachungsnachricht an {{site.data.keyword.iot_short_notm}} gesendet wird. </br>
 Legen Sie einen niedrigen Wert fest, sodass Überwachungsmesswerte häufiger berichtet werden. Legen Sie einen hohen Wert fest, um zu {{site.data.keyword.iot_short_notm}} detailliertere Überwachungsdaten zu erhalten. </br>
 DEFAULT: 60000    </br>
 RECOMMENDED RANGE: [1000, 360000]</dd>
 <dt>MonitorLogDesample</dt>
 <dd>INTEGER  </br>
 Interpolationsverhältnis zwischen der Anzahl von Überwachungsnachrichten, die an {{site.data.keyword.iot_short_notm}} gesendet wurden, verglichen mit der Anzahl der Nachrichten, die in das lokale Protokoll eingegeben wurden. Wenn beispielsweise für `MonitorLogDesample` der Wert '10' festgelegt wird, wird für jeweils zehn Nachrichten, die an {{site.data.keyword.iot_short_notm}} gesendet werden, nur ein Eintrag in das lokale Protokoll geschrieben. </br>Eine größere Zahl hält das lokale Protokoll klein. Eine kleine Zahl bietet ein detaillierteres lokales Protokoll.</br>
 DEFAULT: 10</br>
 RECOMMENDED RANGE: [1, 100]</dd>
 <dt>MemoryAlertThreshold</dt>
 <dd>INTEGER (in Megabyte)</br>
 Der Schwellenwert für den freien JVM-Heapspeicher, bei dessen Erreichen an das Diagnoseprotokoll von {{site.data.keyword.iot_short_notm}} eine Warnungsprotokollnachricht zum Speicher geschrieben wird. Der Alert wird durch die Überwachung ausgelöst. </br>Ein kleiner Wert reduziert die Anzahl der Alertnachrichten, die an {{site.data.keyword.iot_short_notm}} gesendet werden. Durch einen hohen Wert erhalten Sie frühzeitig eine Warnung, falls auf dem EAA-Server Speicherprobleme zu erwarten sind.</br>**Tipp:** Sie können [Cloud Analytics](../cloud_analytics.html)-Regeln zum Konfigurieren von Alertaktionen wie beispielsweise E-Mail-Benachrichtigungen verwenden, damit Sie Alerts zu Speicherproblemen erhalten. Informationen zu den verfügbaren Eigenschaften, die Sie zum Erstellen von Regeln verwenden können, finden Sie in [Diagnosemesswerte des Edge Analytics-Agenten](../edge_analytics.html#eaa_metrics).</br>
  DEFAULT: 10</br>
 RECOMMENDED RANGE: [10 oder 5 % des Gesamtspeichers von 200]</dd>
 </dl>
5. Speichern Sie die bearbeitete Datei und starten Sie den Edge Analytics-Agenten anschließend erneut.

Beispiel für eine config.properties-Datei für den EAA
```
#######################################################################
# Engine Parameters
#######################################################################
# DataDirectSendEnable
#                    - BOOLEAN(true|false) Auf 'true' festgelegt, um
#                      alle Daten weiterzuleiten; festgelegt auf
#                      'false', um das direkte Senden von Daten an IoTP
#                      zu inaktivieren, wenn in der Engine keine Regel
#                      festgelegt ist.
#                      DEFAULT: true
#######################################################################
DataDirectSendEnable=true

#######################################################################
# Monitoring Parameters
#######################################################################
# MonitorInterval    - INTEGER Zeitintervall in Millisekunden bevor
#                      eine neue Überwachungsnachricht generiert
#                      wird. Legen Sie einen niedrigen Wert fest, um
#                      Überwachungsmesswerte häufiger zu berichten.
# Legen Sie einen hohen Wert fest, um zu IoTP
#                      detaillierte Überwachungsdaten zu erhalten.
#                      DEFAULT: 60000    RECOMMEND: [1000, 360000]
# MonitorLogDesample - INTEGER Das Interpolationsverhältnis der Anzahl
#                      der an IoTP gesendeten Nachrichten vs. lokales
#                      Protokoll, d.h., die Anzahl der Überwachungs-
#                      nachrichten N, bei denen der EAA pro N Nach-
#                      richten nur eine an das Informationsprotokoll
#                      ausgeben würde. Legen Sie einen hohen Wert
#                      Wert fest, um das Protokoll klein zu halten. #                      Legen Sie einen niedrigen Wert fest, um im
#                      lokalen Protokoll detaillierte Überwachungs-
#                      informationen zu erhalten.
#                      DEFAULT: 10       RECOMMEND: [1, 100]
# MemoryAlertThreshold
#                    - INTEGER freier JVM-Heapspeicher in Megabyte, bei
#                      dessen Unterschreiten eine Protokollnachricht
#                      generiert und an das IoTP-Diagnoseprotokoll
#                      gesendet wird. Der Alert wird durch die Über-
#                      wachung ausgelöst. Legen Sie einen niedrigen
#                      Wert fest, um unnötige Alertnachrichten an IoTP
#                      zu vermeiden. Legen Sie einen hohen Wert fest,
#                      um frühzeitig einen Alert zu erhalten, wenn das
#                      System absturzgefährdet ist. Festlegen auf
#                      Min(Max(10MB, 5 % des Gesamtspeichers), 200MB)
#                      wird empfohlen.
#                      DEFAULT: 10       RECOMMEND: [10, 200]
#######################################################################

MonitorInterval=60000
MonitorLogDesample=10
MemoryAlertThreshold=10
```
