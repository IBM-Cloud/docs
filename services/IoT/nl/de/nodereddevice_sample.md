---

copyright:
  years: 2016, 2017
lastupdated: "2016-08-26"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Node-RED-Gerätesimulator erstellen und verbinden
Verwenden Sie Node-RED, um einen Gerätesimulator zu erstellen und Daten zum simulierten Gerät an Ihre {{site.data.keyword.iot_full}}-Organisation zu senden.  
{:shortdesc}

Node-RED ist ein Tool, mit dem Hardware-Geräte, APIs und Online-Services auf eine neue und interessante Weise miteinander verbunden werden können. Weitere Informationen finden Sie auf der Website von [Node-RED](http://nodered.org/).  

Sie können Ihre Node-RED-Instanz in Ihrer eigenen Umgebung ausführen oder Sie können sie als {{site.data.keyword.Bluemix_notm}}-Anwendung verwenden. Der folgende Prozess enthält die Anweisungen für {{site.data.keyword.Bluemix_notm}}.

Gehen Sie wie folgt vor, um den Node-RED-Gerätesimulator zu erstellen und zu verbinden:

1. Node-RED-Gerätesimulator erstellen
   Senden Sie mithilfe des Gerätesimulators MQTT-Gerätenachrichten an {{site.data.keyword.iot_short_notm}}. Der Gerätesimulator hat das Senden von Daten für einen Frachtcontainer an einen MQTT-Broker wie beispielsweise {{site.data.keyword.iot_short_notm}} simuliert.
    1. Melden Sie sich unter 'https://console.ng.bluemix.net' bei {{site.data.keyword.Bluemix_notm}} an.
    2. Wählen Sie die Registerkarte **Katalog** aus.
    3. Suchen Sie im Servicekatalog den Abschnitt mit den Boilerplates und klicken Sie auf die Option für **Node-RED Starter Community BETA**. **Tipp:** Klicken Sie [hier](https://console.ng.bluemix.net/catalog/starters/node-red-starter/), um direkt zur Seite mit Node-RED Starter zu wechseln.
    4. Wählen Sie auf der Seite mit Node-RED Starter den Bereich aus, in dem Sie Node-RED bereitstellen möchten, überprüfen Sie die Auswahl für 'App erstellen' und klicken Sie auf **Erstellen**, um Node-RED zu Ihrer Bluemix-Organisation hinzuzufügen.  
    Beispiel:  
     - Bereich: dev
     - Name: myDevice
     - Host: myDevice

    Behalten Sie bei den übrigen Optionen die Standardwerte bei. Nach der Bereitstellung der Anwendung gelangen Sie zu einer Seite, auf der Sie mit der Codeerstellung mithilfe von Node-RED beginnen können.  
    **Hinweis:** Der Staging-Prozess benötigt einige Minuten.

    3. Klicken Sie auf die Verknüpfung 'Routen', um Node-RED zu öffnen.  
    Beispiel: `http://simulatedDevice.mybluemix.net`
    4. Klicken Sie auf **Go to your Node-RED flow editor**, um den Editor zu öffnen.
    5. Kopieren Sie die Node-RED-Flussdaten, die Sie im Abschnitt [Flussdaten des Node-RED-Knotens](#flow_data) dieses Dokuments finden.
    5. Klicken Sie im Node-RED-Ablaufeditor in der rechten oberen Ecke auf das Menü und wählen Sie **Import > Clipboard** aus.  
    6. Fügen Sie den Inhalt der Zwischenablage in das Eingabefeld des Importknotens ein und klicken Sie auf **Ok**.
    Der Ablauf des Gerätesimulators wird nun in den Ablaufeditor importiert.

2. Gerät bei {{site.data.keyword.iot_short_notm}}   registrieren
Führen Sie folgende Schritte aus, um das Node-RED-Beispielgerät zu verbinden:
 1. Wechseln Sie in {{site.data.keyword.Bluemix_notm}} zum Dashboard.
 2. Wählen Sie den Bereich aus, in dem Sie {{site.data.keyword.iot_short_notm}} bereitgestellt haben.
 3. Klicken Sie auf die Kachel für **{{site.data.keyword.iot_short_notm}}**.
 4. Klicken Sie auf **Dashboard starten**, um das {{site.data.keyword.iot_short_notm}}-Dashboard zu starten.
 5. Wählen Sie **Geräte** aus.
 6. Klicken Sie auf **Gerät hinzufügen**.
 7. Klicken Sie auf **Gerätetyp erstellen**.
 9. Geben Sie einen beschreibenden Namen und eine Beschreibung des Gerätetyps ein, wie beispielsweise `sample_device`.
 10. Optional: Geben Sie Attribute zum Gerätetyp ein.
 11. Optional: Geben Sie Metadaten zum Gerätetyp ein.
 12. Klicken Sie auf **Erstellen**, um den neuen Gerätetyp hinzuzufügen.
 13. Klicken Sie auf **Weiter**, um Ihr Gerät hinzuzufügen.
 14. Geben Sie eine Geräte-ID wie beispielsweise `Device001` ein.
 15. Optional: Geben Sie Metadaten zum Gerät ein.
 16. Klicken Sie auf **Weiter**, um eine Geräteverbindung mit einem automatisch generierten Authentifizierungstoken hinzuzufügen.
 17. Überprüfen Sie, dass die Übersichtsinformationen richtig sind und klicken Sie anschließend auf **Hinzufügen**, um die Verbindung hinzuzufügen.
 18. Kopieren Sie auf der Seite mit den Geräteinformationen, die sich daraufhin öffnet, die Geräteinformationen und speichern Sie sie:  
  <ul>
  <li> Organisations-ID
  <li> Gerätetyp
  <li> Geräte-ID
  <li> Authentifizierungsmethode
  <li> Authentifizierungstoken
  </ul>
  **Tipp:** Sie benötigen die Organisations-ID, das Authentifizierungstoken, den Gerätetyp und die Geräte-ID in den nächsten Schritten, um die Konfiguration der Node-RED-Anwendung für das Ausführen einer Verbindung abzuschließen.

2. Gerät mit {{site.data.keyword.iot_short_notm}} verbinden  
 1. Öffnen Sie den Node-RED-Ablaufeditor.
 2. Doppelklicken Sie auf den Knoten 'Publish to IoT'.
 3. Überprüfen Sie, dass der Topic-Eintrag wie folgt lautet: `iot-2/evt/event_name/fmt/json` **Tipp:** Mit dem Teil '/event_name' des Topics wird der Ereignisname der publizierten Ereignisse festgelegt.
 4. Klicken Sie neben dem Serverfeld auf das Bearbeitungssymbol.
 5. Aktualisieren Sie den Servernamen, sodass er mit dem Namen Ihrer {{site.data.keyword.iot_short_notm}}-Organisation übereinstimmt.  
 ```
 {Organisations-ID}.messaging.internetofthings.ibmcloud.com
 ```  
 Dabei ist {Organisations-ID} die zuvor von Ihnen gespeicherte *Organisations-ID*.
 6. Aktualisieren Sie die Client-ID mit der Organisations-ID, dem Gerätetyp und der Geräte-ID:
 ```
 d:{Organisations-ID}:{Gerätetyp}:{Geräte-ID}
   ```  
   Dabei stehen {Organisations-ID}, {Gerätetyp} und {Geräte-ID} für die zuvor von Ihnen gespeicherten Werte.
 7. Klicken Sie auf die Registerkarte **Security**.
 8. Überprüfen Sie, dass das Feld für den Benutzernamen den Wert `use-token-auth` aufweist.
 9. Aktualisieren Sie das Kennwortfeld mit dem zuvor von Ihnen gespeicherten *Authentifizierungstoken*.
 10. Klicken Sie auf **Update** und anschließend auf **OK**.
 12. Klicken Sie im Node-RED-Ablaufeditor in der rechten oberen Ecke auf die Option **Deploy**.
 13. Überprüfen Sie, dass als Verbindungsstatus für den Knoten 'Publish to IoT' *connected* angezeigt wird.  **Tipp:** Wenn die Verbindung nicht hergestellt wurde, müssen Sie die von Ihnen eingegebenen Einstellungen erneut prüfen. Selbst ein kleiner Fehler beim Ausschneiden und Einfügen führt zu einem Fehlschlagen der Verbindung.

4. Geräteverbindung überprüfen
 1. Öffnen Sie das {{site.data.keyword.iot_short_notm}}-Dashboard auf einer neuen Browserregisterkarte oder in einem neuen Fenster.
 2. Wählen Sie **Geräte** aus und klicken Sie auf die Option für **Device001** bzw. auf den Namen des von Ihnen hinzugefügten Geräts, falls der Name anders lautet.  
 Die Seite mit den Geräteinformationen wird geöffnet. Hier wird Ihnen der Verbindungsstatus Ihres Geräts angezeigt. Das Gerät sollte in diesem Stadium als 'Nicht verbunden' (disconnected) angezeigt werden.   
 3. Klicken Sie in Ihrem Node-RED-Ablaufeditor auf die Schaltfläche im Knoten 'Inject', um Nutzdaten für ein Asset zu generieren.  
 Die Nutzdaten enthalten folgende Datenpunkte:  
 ```
 {"d":
  { "name":"My Device",
    "location":
    {
      "longitude":-87.90,
      "latitude":43.03
    },
    "velocity":13,
    "type":"GPS"
  }
 }
 ```
  {:codeblock}  

 3. Überprüfen Sie auf der Registerkarte für das Debugging im linken Teilfenster, dass Nachrichten erstellt werden.  
 4. Auf der {{site.data.keyword.iot_short_notm}}-Seite mit den Geräteinformationen sollte das Gerät nun als verbunden angezeigt werden. Überprüfen Sie, dass dieselben Datenpunkte als vom Gerät empfangen angezeigt werden.  
 ```
 Ereignis	  Datenpunkt	 Wert	Zeit    Empfangen
 event_name	d.name	My Device	May 16, 2016 2:22:18 PM
 event_name	d.location.longitude	-87.90	May 16, 2016 2:22:18 PM
 event_name	d.location.latitude	43.03	May 16, 2016 2:22:18 PM
 event_name	d.velocity	13	May 16, 2016 2:22:18 PM
 event_name	d.type	GPS	May 16, 2016 2:22:18 PM
 ```  
  {:codeblock}  

 Ihr IoT-Beispielgerät ist nun mit {{site.data.keyword.iot_short_notm}} verbunden und Sie können Gerätedaten anzeigen.

## Flussdaten des Node-RED-Knotens
{: #flow_data}  
Kopieren Sie folgenden Text in Ihre Zwischenablage und fügen Sie ihn anschließend beim Importieren von Knoten in den Node-RED-Ablaufeditor in die Zwischenablage für den Import ein.   
**Wichtig:** Stellen Sie sicher, dass Sie den gesamten Text einschließlich der führenden und der abschließenden eckigen Klammern kopieren.  

```
[{"id":"e658d1b6.c187e8","type":"mqtt-broker","z":"965c3822.02c558","broker":"Organisations-ID.messaging.internetofthings.ibmcloud.com","port":"1883","clientid":"d:Organisations-ID:Gerätetyp:Geräte-ID","usetls":false,"verifyservercert":true,"compatmode":true,"keepalive":"60","cleansession":true,"willTopic":"","willQos":"0","willRetain":"false","willPayload":"","birthTopic":"","birthQos":"0","birthRetain":"false","birthPayload":""},{"id":"23f82ce8.126dc4","type":"mqtt out","z":"965c3822.02c558","name":"Publish to IoT","topic":"iot-2/evt/event_name/fmt/json","qos":"","retain":"","broker":"e658d1b6.c187e8","x":480,"y":273,"wires":[]},{"id":"92e2f51f.5126","type":"inject","z":"965c3822.02c558","name":"Send data","topic":"","payload":"","payloadType":"num","repeat":"","crontab":"","once":false,"x":92,"y":265,"wires":[["832b025d.2d24c"]]},{"id":"832b025d.2d24c","type":"function","z":"965c3822.02c558","name":"Device payload","func":"var name1 = \"My Device\";\nvar type1 = \"GPS\";\nvar longitude1 = [-98.49,-97.74,-96.79,-94.20,-90.19,-94.57,-87.62,-87.90,-93.26,-95.99];\nvar latitude1 = [29.42,30.26,32.77,36.37,38.62,39.09,41.87,43.03,44.97,41.25];\nvar velocity1 = context.get('velocity1')||0;\n\n\n\nvelocity1 = velocity1+1;\nif(velocity1 > 20) velocity1=0;\ncontext.set('velocity1',velocity1);\n\nvar counter1 = context.get('counter1')||0;\ncounter1 = counter1+1;\nif(counter1 > 9) counter1 = 0;\ncontext.set('counter1',counter1);\n\nmsg = {\n \tpayload: JSON.stringify(\n \t { d:{\n \"name\" : name1,\n \"location\" : \n {\n \"longitude\" : longitude1[counter1],\n \t \"latitude\" : latitude1[counter1]\n },\n \"velocity\" : velocity1,\n \t \"type\" : type1\n \t }\n \t }\n )\n}\n\nreturn msg;","outputs":1,"noerr":0,"x":270,"y":108,"wires":[["f04ddebd.f55298","23f82ce8.126dc4"]]},{"id":"f04ddebd.f55298","type":"debug","z":"965c3822.02c558","name":"","active":true,"console":"false","complete":"false","x":250,"y":384,"wires":[]},{"id":"d606058f.d3422","type":"comment","z":"965c3822.02c558","name":"Configure Publish to IoT for your environment","info":"1. Doppelklicken Sie auf den Knoten.\n2. Klicken Sie neben dem Serverfeld auf das Bearbeitungssymbol.\n3. Aktualisieren Sie den Servernamen, sodass er mit dem Namen Ihrer Watson IoT Platform-Organisation übereinstimmt.\n 'Organisations-ID.messaging.internetofthings.ibmcloud.com'\n\n4. Aktualisieren Sie die Client-ID mit Ihrer Organisations-ID, dem Gerätetyp und der Geräte-ID:\n 'd:Organisations-ID:Gerätetyp:Geräte-ID'\n\n5. Klicken Sie auf die Registerkarte für 'Sicherheit'.\n6. Stellen Sie sicher, dass das Feld für den Benutzernamen (username) den Wert 'use-auth-token' aufweist.\n7. Aktualisieren Sie das Kennwortfeld mit dem zuvor gespeicherten Authentifizierungstoken.\n8. Klicken Sie auf die Option zum Aktualisieren und anschließend auf 'OK'.\n9. Klicken Sie in der rechten oberen Ecke des Node-RED-Ablaufeditors auf 'Deploy'. ","x":570,"y":241,"wires":[]},{"id":"b997cfe2.ebfd7","type":"comment","z":"965c3822.02c558","name":"Function Node","info":"Der Knoten 'Function' ermöglicht es Ihnen, jede Nachricht über eine JavaScript-Funktion zu übergeben.\n\nDie JavaScript-Funktion erstellt die Nachrichtennutzdaten, die an Ihre Watson IoT Platform-Organisation gesendet werden.","x":271,"y":77,"wires":[]},{"id":"1ce4e378.c5a565","type":"comment","z":"965c3822.02c558","name":"Debug Node","info":"Der Debugknoten veranlasst, dass alle Nachrichten in der Debug-Seitenleiste angezeigt werden. Standardmäßig werden nur die Nutzdaten der Nachricht angezeigt; es ist aber möglich, das gesamte Nachrichtenobjekt anzuzeigen.","x":250,"y":414,"wires":[]},{"id":"ba916f5e.695db8","type":"comment","z":"965c3822.02c558","name":"Inject Node","info":"Der Knoten 'Inject' ermöglicht es Ihnen, Nachrichten in einen Ablauf einzufügen; dazu klicken Sie entweder auf die Schaltfläche auf dem Knoten oder Sie legen ein Intervall für die Zeit zwischen den Einfügungen fest.,"x":75,"y":236,"wires":[]}]
```
{:codeblock}
