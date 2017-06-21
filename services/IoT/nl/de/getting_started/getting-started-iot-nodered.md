---

copyright:
  years: 2017
lastupdated: "2017-04-24"
---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Einführung in {{site.data.keyword.iot_short_notm}} Starter
{: #gettingstartedtemplate}
<!-- Provide an appropriate ID above -->

Beginnen Sie Ihre Arbeit mit {{site.data.keyword.iot_full}} unter Verwendung des {{site.data.keyword.iot_short_notm}} Starter-GitHub-Projekts. Unter Verwendung der Starter-Anwendung können Sie in kürzester Zeit ein Gerät simulieren, Karten erstellen, Daten generieren und damit beginnen, Daten zu analysieren und im {{site.data.keyword.iot_short_notm}}-Dashboard anzuzeigen.   
{:shortdesc}

## Übersicht
{: #overview}  

Die Starter-Anwendung stellt die folgenden Services automatisch bereit und verbindet sie: 
<dl>
<dt>**{{site.data.keyword.iot_short_notm}}**</dt>
<dd>Ein IoT-Web-Service, der Gateway-Management, Gerätemanagement und Anwendungszugriff beinhaltet. Unter Verwendung von {{site.data.keyword.iot_short_notm}} können Sie Daten von verbundenen Geräten erfassen und Echtzeitdaten aus Ihrer Organisation analysieren. </dd>
<dt>**{{site.data.keyword.sdk4nodefull}}**</dt>
<dd>Die Laufzeitumgebung, in der Node-RED ausgeführt wird. </br>Weitere Informationen finden Sie in der Dokumentation zu [{{site.data.keyword.sdk4nodefull}} Starter](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html). </dd>
<dd>Node-RED ist ein Tool, mit dem Hardware-Geräte, APIs und Online-Services auf eine neue und interessante Weise miteinander verbunden werden können. Sie können Node-RED verwenden, um einen simulierten Thermostat zu erstellen, der simulierte Daten an Ihren {{site.data.keyword.iot_short_notm}}-Service sendet. Sie haben die Möglichkeit, Karten zu erstellen, um Echtzeitdaten im {{site.data.keyword.iot_short_notm}}-Dashboard anzuzeigen. </br>Weitere Informationen finden Sie in der [Node-RED-Dokumentation](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html#nodered). </dd>
<dt>**{{site.data.keyword.cloudantfull}}**</dt><dd>Die Datenbank, in der Node-RED Metadaten speichert. </dd>
</dl>

## Vorbereitende Schritte
{: #byb}  

- Erforderliche Konten  
Sie können erst beginnen, wenn Sie über ein [IBM Bluemix-Konto](https://bluemix.net/registration) verfügen. 

- Navigation  
Um das Wechseln zwischen den verschiedenen Aufgaben im folgenden Prozess zu vereinfachen, öffnen Sie das {{site.data.keyword.Bluemix_notm}}-Dashboard, das {{site.data.keyword.iot_short_notm}}-Dashboard und die Node-RED-Anwendung in verschiedenen Registerkarten Ihres Browsers. 
<dl>
<dt>*{{site.data.keyword.Bluemix_notm}}-Dashboard*</dt>
<dd>Hier können Sie den Status Ihrer Bereitstellung ermitteln, die Dokumentation lesen und Dashboards starten. </dd>
<dt>*{{site.data.keyword.iot_short_notm}}-Dashboard*</dt>
<dd>Hier haben Sie die Möglichkeit, Gerätetypen zu definieren, Geräte zu registrieren, eingehende Sensordaten zu überwachen, Datenvisualisierungskarten zu erstellen
und Datenvisualisierungen live anzuzeigen. </dd>
<dt>*Node-RED*</dt>
<dd>Hier können Sie den Ablauf des Gerätesimulators konfigurieren und ausführen und Sie können mit anderen Abläufen arbeiten, um Daten von {{site.data.keyword.iot_short_notm}} zu verarbeiten. </dd>
</dl>

## Schritt 1: {{site.data.keyword.iot_short_notm}} Starter bereitstellen
{: #deployStarter}

Führen Sie die folgenden Schritte aus, um die Starter-Beispielanwendung bereitzustellen: 

1. Starter-Anwendung bereitstellen. 
 1. Klicken Sie auf <a href="https://bluemix.net/devops/setup/deploy?repository=https://github.com/ibm-watson-iot/iot-platform-bluemix-starter"><img src="https://bluemix.net/devops/graphics/create_toolchain_button.png" height=25></a>, um eine neue Continuous Delivery Toolchain in Bluemix zu erstellen: (über Continuous Delivery)  
 **Tipp:** Wenn Sie die Bereitstellung lieber von der Befehlszeile durchführen wollen, [finden Sie {{site.data.keyword.iot_short_notm}} Starter](https://github.com/ibm-watson-iot/iot-platform-bluemix-starter) in der IBM Watson IoT-Organisation in GitHub. 
 2. Melden Sie sich bei IBM Bluemix an, wenn Sie dazu aufgefordert werden. 
 3. Wählen Sie bei Bedarf die Bluemix-Organisation aus, in der Sie die Starter-Anwendung bereitstellen wollen. 
 4. Behalten Sie den Toolchain-Namen bei oder ändern Sie ihn bei Bedarf. Er wird als Standard-App-Name und als URL-Stammverzeichnis der App verwendet: `<app-name>.mybluemix.net`
 5. Klicken Sie auf **Erstellen**.   
**Tipp:** Klicken Sie auf die Kachel **Delivery Pipeline**, um den Fortschritt Ihrer ersten Bereitstellung zu überwachen. 
 6. Wenn die Bereitstellung abgeschlossen ist, klicken Sie auf **App anzeigen**, um Ihre neue Node-RED-Anwendung in einer neuen Registerkarte zu öffnen. 
2. Starter-App-Services lokalisieren. 
 1. Wählen Sie **Dashboard** im Bluemix-Menü aus. 
 2. Lokalisieren Sie die folgenden Services unter *Alle Services*: 
    - iot-starter
    - iotp-starter-cloudantNoSQLDB
 3. Lokalisieren Sie die Toolchain unter *Alle Apps*: 
    - default-toolchain-{id}}


## Schritt 2: Simuliertes Gerät in {{site.data.keyword.iot_short_notm}} definieren. 
{: #definingsimdev}

Führen Sie die folgenden Schritte aus, um ein Szenario zu simulieren, das ein Thermostat verwendet, um die Temperatur, die Feuchtigkeit und den Ort eines Wohnraums überwacht. 

1.	{{site.data.keyword.iot_short_notm}}-Dashboard starten. 
  1. Klicken Sie im Bluemix-Dashboard unter *Alle Services* auf den Namen Ihrer {{site.data.keyword.iot_short_notm}}-Instanz.
**Tipp:** Der Instanzname enthält normalerweise den Bestandteil `iotp-starter`. 
  2. Klicken Sie auf die Option zum **Starten**, um das {{site.data.keyword.iot_short_notm}}-Dashboard in einer neuen Browserregisterkarte zu öffnen.    
Die Seite `Alle Boards` wird standardmäßig angezeigt. 
2. Gerätetyp erstellen. 
  1.	Wählen Sie **Geräte** im Hauptmenü aus und klicken Sie anschließend auf **Gerät hinzufügen**. 
  2.	Klicken Sie auf der Seite "Gerät hinzufügen" auf **Gerätetyp erstellen**. 
  3.	Klicken Sie auf der Seite "Gerätetyp erstellen" auf **Gerätetyp erstellen**. 
  4. Geben Sie einen eindeutigen Namen (z. B. `Thermostat`) für Ihren Gerätetyp ein und klicken Sie auf **Weiter**. 
  5. Optional: Auf den nächsten beiden Seiten können eine Vorlage sowie Metadaten definiert werden. Andernfalls klicken Sie auf diesen Seiten einfach auf **Weiter**. 
  6.	Klicken Sie auf **Erstellen**, um den Gerätetyp hinzuzufügen. 
3.	Gerät hinzufügen, das den neu erstellten Gerätetyp verwendet. 
  1. Auf der Seite "Gerät hinzufügen" wird der gerade hinzugefügte Gerätetyp in der Liste der Gerätetypen angezeigt. Klicken Sie auf **Weiter**, um ein Gerät hinzuzufügen, das diesen Gerätetyp verwendet. 
  2. Geben Sie eine eindeutige Geräte-ID ein (z. B. `LivingRoomThermo1`). 
  3. Optional: Die Angabe beschreibender Daten auf der Seite "Gerät hinzufügen" oder die Eingabe von Gerätemetadaten auf der nächsten Seite ist optional. Sie können diese Seiten einfach überspringen, indem Sie auf jeder Seite auf **Weiter** klicken. 
  4. Klicken Sie auf der Seite "Sicherheit" auf **Weiter**, um ein Authentifizierungstoken für Ihr Gerät zu generieren. 
  5. Stellen Sie sicher, dass die Informationen auf der Seite "Zusammenfassung" richtig sind, und klicken Sie auf **Hinzufügen**, um das Gerät hinzuzufügen. Klicken Sie auf **Zurück**, um zur vorherigen Seite zurückzukehren. 
4.	Informationen notieren, die auf der Seite mit Ihren Geräteberechtigungsnachweisen angezeigt werden.    
Sie benötigen die folgenden Informationen, um den Simulator zu konfigurieren und die Daten anzuzeigen: 
 - Organisations-ID
 - Gerätetyp
 - Geräte-ID
 - Authentifizierungsmethode
 - Authentifizierungstoken

## Schritt 3: Node-RED-Gerätesimulator konfigurieren und ausführen.   
{: #confignodered}  
Sie können den Node-RED-Gerätesimulator so konfigurieren, dass MQTT-Gerätenachrichten mit Informationen zu Temperatur und Feuchtigkeit an {{site.data.keyword.iot_short_notm}} gesendet werden. 

1. Node-RED-Ablaufeditor starten. 
  1. Klicken Sie im Bluemix-Dashboard unter *Alle Apps* auf den Namen Ihrer Toolchain.   
**Tipp:** Der Toolchain-Name enthält normalerweise den Bestandteil `default-toolchain...`. 
  2. Öffnen Sie über das Toolchain-Dashboard Ihre Node-RED-Instanz, indem Sie auf **Routen** klicken und den Routenlink auswählen.   
  2. Klicken Sie auf **Zu Node-RED-Ablaufeditor wechseln**, um den Editor zu öffnen.
2. Gerät bereitstellen. 
  1. Klicken Sie im Gerätesimulatorablauf doppelt auf den blauen Knoten **An IBM IoT Platform senden**. 
  2. Stellen Sie sicher, dass die Authentifizierung auf **Bluemix-Service** eingestellt ist. 
  3. Geben Sie den **Gerätetyp** und die **Geräte-ID** Ihres Geräts ein und klicken Sie auf **Fertig**. 
  4. Stellen Sie das Gerät bereit, indem Sie auf **Bereitstellen** klicken. 
3. Node-RED-Temperaturüberwachungsablauf konfigurieren. 
  1. Klicken Sie im Gerätesimulatorablauf doppelt auf den blauen Knoten **IBM IoT App In**. 
  2. Wählen Sie in der Authentifizierung **Bluemix-Service** aus. 
  3.	Wählen Sie **Alle** für Gerätetyp, Geräte-ID, Ereignis und Format aus. 
  4.	Klicken Sie auf **Fertig**. 
  5.  Stellen Sie Ihren Monitor bereit, indem Sie auf **Bereitstellen** klicken. 
4. Geräteverbindung prüfen. 
  1.	Öffnen Sie das {{site.data.keyword.iot_short_notm}}-Dashboard.   
**Tipp:** Wenn das {{site.data.keyword.iot_short_notm}}-Dashboard nicht bereits in einer anderen Registerkarte geöffnet ist, kehren Sie zu Ihrem {{site.data.keyword.Bluemix_notm}}-Dashboard zurück, klicken Sie auf den Namen Ihrer {{site.data.keyword.iot_short_notm}}-Instanz und klicken Sie anschließend auf **Dashboard starten**. 
  2. Wählen Sie **Geräte** im Hauptmenü aus. 
  3. Klicken Sie auf den Namen des Geräts, das Sie hinzugefügt haben.    
Die Geräteinformationen zeigen den Verbindungsstatus Ihres Geräts an. 
  4.	Klicken Sie in Ihrem Node-RED-Ablaufeditor doppelt auf den Knoten **Daten senden**, wählen Sie für den Wert "repeat" die Einstellung **interval** und legen Sie eine Frequenz von `3` Sekunden fest. 
  5. Klicken Sie auf **Fertig**. 
  6. Stellen Sie Ihre Änderungen bereit, indem Sie auf **Bereitstellen** klicken.   
Die Nutzdaten beinhalten Datenpunkte (z. B. diejenigen im folgenden Beispiel): 
```
{"d":{"temp":15,"humidity":50,"location":{"longitude":-98.49,"latitude":29.42}}}
```
  7. Optional: Öffnen Sie die Registerkarte "Debug", um zu prüfen, ob Nachrichten erstellt werden. 
    1. Wählen Sie **Ansicht** in dem Menü aus, das Sie oben in der Anzeige befindet. 
    2. Wählen Sie **Seitenleiste anzeigen** aus. 
    3. Klicken Sie auf die Registerkarte "Debug", um Nachrichten anzuzeigen. 
  8. Prüfen Sie auf der Seite "{{site.data.keyword.iot_short_notm}}-Geräteinformationen", dass Datenpunkte von dem Gerät im Abschnitt "Sensorinformationen" angezeigt werden. 


## Schritt 4: Karten in {{site.data.keyword.iot_short_notm}} erstellen, um Live-Daten anzuzeigen.   
{: #createcards}  
Sie können ein Board sowie Karten erstellen, um Gerätedaten im {{site.data.keyword.iot_short_notm}}-Dashboard anzuzeigen. Weitere Informationen zu Boards und Karten finden Sie in [Echtzeitdaten mithilfe von Boards und Karten visualisieren](https://console.ng.bluemix.net/docs/services/IoT/data_visualization.html). 

1. Board erstellen. 
  1. Öffnen Sie das {{site.data.keyword.iot_short_notm}}-Dashboard.   
  **Tipp:** Wenn das {{site.data.keyword.iot_short_notm}}-Dashboard nicht bereits in einer anderen Registerkarte geöffnet ist, kehren Sie zu Ihrem {{site.data.keyword.Bluemix_notm}}-Dashboard zurück, klicken Sie auf den Namen Ihrer {{site.data.keyword.iot_short_notm}}-Instanz und klicken Sie anschließend auf **Dashboard starten**.   
  2. Erstellen Sie ein Board, das die Karten für Ihre simulierten Geräte enthalten soll. 
    1. Wenn die Seite "Alle Boards" noch nicht angezeigt wird, wählen Sie **Boards** im Hauptmenü des {{site.data.keyword.iot_short_notm}}-Dashboards aus und klicken Sie anschließend auf **Neues Board erstellen**. 
    2. Geben Sie einen Namen für das Board ein (z. B. `Heimarbeitsplatz`) und klicken Sie auf **Weiter**. 
    3. Klicken Sie auf der nächsten Seite auf **Übergeben**.   
  3. Klicken Sie auf das gerade erstellte Board, um es zu öffnen. 
2. Karte erstellen, um die Temperatur anzuzeigen. 
  1. Klicken Sie auf **Neue Karte hinzufügen** und wählen Sie anschließend den Kartentyp **Kurvendiagramm** im Abschnitt "Geräte" aus. 
  2. Wählen Sie Ihr Gerät aus der Geräteliste aus und klicken Sie anschließend auf **Weiter**. 
  3. Klicken Sie auf **Neues Dataset verbinden**. 
  4. Wählen Sie auf der Seite "Wertkarte erstellen" die folgenden Werte aus oder geben Sie sie ein und klicken Sie auf **Weiter**. 
    - Ereignis: update
    - Eigenschaft: temp
    - Name: Temperature
    - Typ: Float
    - Einheit: °C
    - Genauigkeit: 2
    - Min.: 0
    - Max.: 50
  5. Wählen Sie auf der Seite "Kartenvorschau" den Wert **L** für die Kurvendiagrammgröße aus und klicken Sie auf **Weiter**. 
  6. Ändern Sie den Namen der Karte auf der Seite "Karteninformationen" in **Temperature** (Temperatur) und klicken Sie auf **Übergeben**.    
Die Karte für die Temperatur wird auf dem Dashboard angezeigt und sie enthält ein Kurvendiagramm mit Live-Temperaturdaten. 
3. Karte erstellen, um die Feuchtigkeit anzuzeigen. 
  1. Klicken Sie auf **Neue Karte hinzufügen** und wählen Sie anschließend den Kartentyp **Messanzeige** im Abschnitt "Geräte" aus. 
  2. Wählen Sie Ihr Gerät aus der Liste aus und klicken Sie anschließend auf **Weiter**. 
  3. Klicken Sie auf **Neues Dataset verbinden**. 
  4. Wählen Sie auf der Seite "Wertkarte erstellen" die folgenden Werte aus oder geben Sie sie ein und klicken Sie auf **Weiter**.
  Ereignis: update
     - Eigenschaft: humidity
     - Name: Humidity
     - Typ: Float
     - Einheit: %
     - Genauigkeit: 1
     - Min.: 10
     - Max.: 95
  5. Wählen Sie auf der Seite "Kartenvorschau" den Wert **M** für die Messanzeigengröße aus und klicken Sie auf **Weiter**. 
  6. Ändern Sie den Namen der Karte auf der Seite "Karteninformationen" in **Humidity** (Feuchtigkeit) und klicken Sie auf **Übergeben**.    
Die Karte für die Feuchtigkeit wird auf dem Dashboard angezeigt und sie enthält eine Messanzeige, die die Live-Feuchtigkeitsdaten zeigt.   

<!-- 4. Create a card to display location
  1. Click **Add New Card**, and then select the **Value** card type, which is located in the Devices section.
  2. Select your device from the list, then click **Next**.
  3. Click **Connect new data set**.
  4. In the Create Value Card page, select or enter the following values.
     - Event: update
     - Property: location.latitude
     - Name: Latitude
     - Type: Float
     - Unit: "°N"
     - Precision: 2
     - Min: -180
     - Max: 180
  5. Click **Connect new data set**.
  6. In the Create Value Card page, select or enter the following values and click **Next**.
     - Event: update
     - Property: location.longitude
     - Name: Longitude
     - Type: Float
     - Unit: "°E"
     - Precision: 2
     - Min: -180
     - Max: 180
  7. In the Card Preview page, select **M** as the text size, and click **Next**.
  8. In the Card Information page, change the name of the card to **Location** and click **Submit**.   
The location card appears on the dashboard and shows the live latitude and longitude of the device.-->

## Weitere Schritte  
{: #whats-next}  
Da Ihr simuliertes Gerät jetzt Daten an {{site.data.keyword.iot_short_notm}} sendet, können Sie Ihr IoT-Projekt weiter iterieren. 
 - Ihre Karten zeigen die Daten, die von Ihrem Node-RED-Ablauf generiert werden.   
Node-Red sendet so lange Daten, bis Sie den Prozess stoppen. Um die simulierten Daten zu stoppen, führen Sie die folgenden Schritte aus: 
    1.	Klicken Sie in Ihrem Node-RED-Ablaufeditor doppelt auf den grauen Knoten **Daten senden**, wählen Sie für den Wert "repeat" die Einstellung **interval** und legen Sie eine Frequenz von **3** Sekunden fest. 
    2. Klicken Sie auf **Fertig**. 
    3. Stellen Sie Ihre Änderungen bereit, indem Sie auf **Bereitstellen** klicken. 

 - Schließen Sie ein physisches Gerät an.   
[Durchsuchen Sie die 'IoT Recipes'](https://developer.ibm.com/recipes/?post_type=tutorials&s=watson+iot), um eine Verbindung zu einem physischen Gerät (wie z. B. Raspberry Pi) herzustellen und Daten an {{site.data.keyword.iot_short_notm}} zu senden. 

 - Durchsuchen Sie die Visualisierungsoptionen.   
[Stellen Sie eine node.js-Beispielanwendung bereit, um Gerätedaten zu visualisieren](https://www.bluemix.net/docs/services/IoT/visualizingdata_sample.html). 

 -	Schützen Sie den Node-RED-Ablaufeditor mit einem Kennwort.    
Standardmäßig können alle Benutzer auf den Editor zugreifen und Abläufe ändern. Gehen Sie wie folgt vor, um den Editor durch ein Kennwort zu schützen: 
    1.	Klicken Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard auf den Namen Ihrer Starter-Anwendung, um die Anwendungsseiten zu öffnen. 
    2. Klicken Sie auf **Laufzeit**, um die Seite "Laufzeit" anzuzeigen. 
    3. Klicken Sie auf **Umgebungsvariable**, um die Seite "Umgebungsvariablen" anzuzeigen. 
    4. Klicken Sie im Abschnitt **Benutzerdefiniert** auf **Hinzufügen** und geben Sie anschließend die folgenden benutzerdefinierten Variablen ein: 
         -	NODE_RED_USERNAME - Benutzername, der den Editor schützen soll
         -	NODE_RED_PASSWORD - Kennwort, das den Editor schützen soll
    3.	Klicken Sie auf **Speichern**. 
