---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Cloud Analytics
{: #cloud_analytics}

Mithilfe von Cloud Analytics für {{site.data.keyword.iot_short}} geben Sie Regelbedingungen an, die auf Echtzeitdaten von Geräten basieren, und die Alerts und optionale Aktionen auslösen, wenn die Bedingungen erfüllt sind.    
{: shortdesc}

Beispielsweise können Sie eine Regel erstellen, um sicherzustellen, dass ein Alert an das Dashboard auf dem Gerät eines Benutzers und eine E-Mail an den Administrator gesendet wird, wenn die Verbindung zum Gerät verloren geht oder die Temperatur des Geräts einen Höchststand erreicht.

## Vorbereitende Schritte
{: #byb}
Stellen Sie sicher, dass die Geräteeigenschaften, die Sie als Bedingungen in Ihren Regeln verwenden möchten, Schemas zugeordnet wurden. Weitere Informationen finden Sie in [Geräte verbinden](iotplatform_task.html) und [Schemas erstellen](im_schemas.html).

Lesen Sie außerdem die Anleitung [Regeln und Aktionen mit {{site.data.keyword.iot_short}} Cloud Analytics verwenden ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/recipes/tutorials/using-rules-and-actions-with-ibm-watson-iot-platform-cloud-analytics/){: new_window}, um die in Cloud Analytics verwendeten Regeln und Aktionen kennenzulernen.

## Regeln und Aktionen verwalten  
{: #managing_rules}

Verwenden Sie das Dashboard **Regeln**, um Regeln und Aktionen für Ihre Organisation zu erstellen und zu verwalten.

Verwenden Sie folgende Boards, um eine Übersicht der Regeln und Alerts zu erhalten, die für Ihr Gerät ausgelöst wurden:

 |Boardname | Beschreibung |  
 |:---|:---|  
  |Regelbasierte Analyse | Zeigt die für Ihre Organisation geltenden Regeln an. Zusätzliche Karten listen ausgelöste Alerts, zugeordnete Geräte, Geräteeigenschaften und Alertinformationen auf. |  
 |Gerätebezogene Analyse | Zeigt die mit Ihrer Organisation verbundenen Geräte an. Zusätzliche Karten zeigen Alerts für ausgewählte Geräte, Informationen zu einem ausgewählten Gerät, Geräteeigenschaften und Alertinformationen an. |

 Weitere Informationen zu den standardmäßigen Analyseboards finden Sie in [Echtzeitdaten mithilfe von Boards und Karten visualisieren](data_visualization.html#default_boards).


## Regeln erstellen
{: #rules}

Regeln sind bedingungsbasierte Entscheidungspunkte, die gerätebezogene Echtzeitdaten und vordefinierte Schwellenwerte oder andere Eigenschaftsdaten abgleichen, um ein Alert auszulösen, wenn eine Bedingung erfüllt wird. Zusätzlich zu einem im {{site.data.keyword.iot_short}}-Dashboard angezeigten Alert können Sie mindestens eine Aktion hinzufügen, mit der bei Auslösen einer Regel Geschäftslogik ausgeführt wird.

**Wichtig:** Bevor Sie Regeln für einen Gerätetyp erstellen können, müssen Sie ein Schema für den Gerätetyp erstellen. Informationen finden Sie in [Schemas für Gerätetypen erstellen](im_schemas.html).

Gehen Sie wie folgt vor, um eine Regel zu erstellen:
1. Wechseln Sie im {{site.data.keyword.iot_short}}-Dashboard zu **Regeln**.
2. Klicken Sie auf **Regel erstellen**, benennen Sie die Regel und ordnen Sie Ihr eine Beschreibung zu, wählen Sie einen Gerätetyp aus, für den die Regel gelten soll, und klicken Sie anschließend auf **Weiter**.  
3. Fügen Sie zum Einrichten der Regellogik mindestens eine IF-Bedingung hinzu, die als Auslöser für die Regel verwendet wird.  
Sie können Bedingungen in parallelen Reihen hinzufügen, um sie als OR-Bedingungen anzuwenden, oder Sie können Bedingungen in sequenziellen Spalten hinzufügen, um sie als AND-Bedingungen anzuwenden.  
**Wichtig:** Um eine Bedingung auszulösen, die zwei Eigenschaften vergleicht, oder um mindestens zwei Eigenschaftsbedingungen auszulösen, die sequenziell durch AND verbunden sind, müssen die auslösenden Datenpunkte in dieselbe Gerätenachricht eingeschlossen werden. Wenn die Daten in mehr als einer Nachricht empfangen werden, werden die Bedingung oder die sequenziellen Bedingungen nicht ausgelöst.  
**Beispiele:**  
Eine einfache Regel kann einen Alert auslösen, wenn ein Parameterwert größer als ein angegebener Wert ist:
Bedingung = `temp_cpu>80`  
Eine komplexere Regel kann zu einem Auslösen führen, wenn eine Übereinstimmung mit einer Kombination aus Schwellenwerten auftritt:
Bedingung = `temp_cpu>60 AND cpu_load>90`   

4. Konfigurieren Sie für Ihre Regel Anforderungen für bedingte Auslöser.  
Zum Steuern der Anzahl von Alerts, die für eine Regel in einem bestimmten Zeitraum ausgelöst werden, können Sie für Ihre Regel Anforderungen für bedingte Auslöser konfigurieren.  
**Wichtig:** Das bedingte Auslösen gilt für jede Bedingung in der Regel. Wenn beispielsweise für eine Regel mithilfe von OR fünf unterschiedliche parallele Bedingungen festgelegt wurden, wird für den Zähler des bedingten Auslösers jede Bedingung, die als 'true' erkannt wird, gezählt.
Gehen Sie wie folgt vor, um für eine Regel das bedingte Auslösen festzulegen:
 1. Klicken Sie im Regeleditor auf den Standardlink **Jedes Mal auslösen, wenn Bedingungen erfüllt sind**, um das Dialogfeld 'Anforderung für Häufigkeit festlegen' zu öffnen.
 2. Wählen Sie den bedingten Auslöser, den Sie in Ihrer Regel verwenden wollen, aus und konfigurieren Sie ihn.
 <ul>
 <li>Jedes Mal auslösen, wenn Bedingungen erfüllt sind</li>
 <li>Auslösen, wenn Bedingungen N-mal in M *Zeiteinheit* erfüllt sind</li>
 </ul>  
 Eine detailliertere Beschreibung von bedingten Auslösern finden Sie in [Bedingtes Auslösen für Regeln](#conditional "Bedingtes Auslösen - Übersicht").
5. Erstellen Sie mindestens eine Aktion, die auftritt, wenn die Regelbedingungen erfüllt sind, oder wählen Sie eine Aktion aus.  
Weitere Informationen zu Aktionen finden Sie in [Aktionen mit Regeln verwenden](#shared "Aktionen erstellen").   
 Beispiel: Eine Aktion kann darin bestehen, eine E-Mail zu senden oder einen Webhook zu posten.
3. **Optional:** Wählen Sie für die Regel eine Alertpriorität aus.  
 Die Priorität wird zum Klassifizieren der Alerts verwendet, die im Board **Regelbasierte Analyse** angezeigt werden. Die Standardpriorität ist 'Niedrig'.
6. Wenn Sie mit Ihrer Regel zufrieden sind, klicken Sie auf **Speichern** für das Speichern ohne Aktivierung oder klicken Sie auf **Aktivieren**, um die Regel zu speichern und zu aktivieren.

Ihre Regel wird erstellt. Wenn Sie die Regel aktivieren und die Bedingungen der Regel erfüllt sind, wird dem Board **Boards > Regelbasierte Analyse** ein Alert hinzugefügt und eine Regelaktion wird ausgeführt.

## Bedingtes Auslösen für Regeln
{: #conditional}

Zum Steuern der Anzahl von Alerts, die für eine Regel in einem bestimmten Zeitraum ausgelöst werden, können Sie für Ihre Regel Anforderungen für bedingte Auslöser konfigurieren.

Je nach der Häufigkeit von Nachrichten und den Regelbedingungen kann eine Regel sehr häufig ausgelöst werden, nachdem die Bedingung für das Auslösen erfüllt wurde. Wenn die Bedingung beispielsweise `temp >= 90` lautet und die Temperatur ansteigt und sich bei '91' stabilisiert, wird die Regel bei jeder eingehenden Nachricht ausgelöst. Je nach der Häufigkeit der Gerätenachrichten und der Aktionen, deren Ausführung für die Regel festgelegt wurde, kann dieser Umfang an Alerts schnell dazu führen, dass Ihr E-Mail-Eingang gefüllt ist oder ein Twitter-Feed mit Nachrichten überflutet wird, die keinen zusätzlichen Wert bereitstellen.

**Wichtig:** Das bedingte Auslösen gilt für jede Bedingung in der Regel. Wenn beispielsweise für eine Regel mithilfe von OR fünf unterschiedliche parallele Bedingungen festgelegt wurden, wird für den Zähler des bedingten Auslösers jede erfüllte Bedingung gezählt.

Bedingung | Beschreibung
------------- | -------------
Jedes Mal auslösen, wenn Bedingungen erfüllt sind | Die Regel wird jedes Mal ausgelöst, wenn die Regelbedingungen erfüllt sind.
Auslösen, wenn Bedingungen *N*-mal in *M* *Tage/Stunden/Minuten/angepasst* erfüllt sind | Die Regel wird ausgelöst, wenn die Bedingungen im ausgewählten Zeitintervall *N*-mal erfüllt sind, und sie wird erst wieder ausgelöst, wenn der konfigurierte Zeitraum vorüber ist. </br>Beispiel: Die Anforderung für den bedingten Auslöser lautet `Trigger only once if conditions are met 4 times in 30 minutes` (Nur einmal auslösen, wenn Bedingungen innerhalb von 30 Minuten viermal erfüllt werden). Das Gerät sendet alle fünf Minuten eine neue Nachricht. Um 12 Uhr mittags übersteigt die Temperatur zum ersten Mal 90 Grad Fahrenheit, wodurch die Bedingung erreicht wird. Der Zähler für den bedingten Auslöser wird gestartet, aber die Regel wird noch nicht ausgelöst.  Nach 15 Minuten und nachdem drei weitere Nachrichten mit der Information `temp > 90` empfangen wurden, wird die Regel ausgelöst. Die Regel wird anschließend während der nächsten 15 Minuten nicht ausgelöst, ungeachtet der Temperatur.
Nur beim ersten Mal, wenn Bedingungen erfüllt sind, auslösen; zurücksetzen, wenn Bedingungen nicht mehr erfüllt sind | Die Regel wird ausgelöst, wenn Bedingungen erfüllt sind, aber sie wird anschließend für nachfolgende Nachrichten, die die Bedingungen auch erfüllen, nicht mehr ausgelöst. Die Kriterien für das Auslösen werden durch die erste Nachricht, die die Regelbedingungen nicht erfüllt, zurückgesetzt.
Auslösen, wenn Bedingungen während einer Zeit von *M* *Tage/Stunden/Minuten/angepasst* bestehen bleiben | Die Regel wird nach Ablauf des ausgewählten Zeitintervalls ausgelöst, wenn alle während des Zeitintervall empfangenen Datenpunkte die Bedingungen erfüllen oder wenn keine zusätzlichen Datenpunkte empfangen werden. Das Zeitintervall startet, wenn die Bedingungen erstmals erfüllt werden.



## Aktionen in Regeln verwenden
{: #shared}

Zusätzlich zum Anzeigen von Alerts im Dashboard für Alerts unterstützt {{site.data.keyword.iot_short}} verschiedene Typen von Aktionen, die durch Regeln ausgelöst werden, wie beispielsweise das Senden von E-Mails und das Übergeben von Webhooks.

Sie können Aktionen direkt im Regeleditor erstellen oder die Aktionen auf der Registerkarte 'Aktionen' erstellen und die Aktionen anschließend auswählen, wenn Sie Ihre Regeln erstellen.

Gehen Sie wie folgt vor, um auf der Registerkarte 'Aktionen' eine Aktion zu erstellen:
1. Wechseln Sie im {{site.data.keyword.iot_short}}-Dashboard zu **Regeln**.
2. Wählen Sie im Dashboard 'Regeln' die Registerkarte **Aktionen** aus.
2. Klicken Sie auf **Aktion erstellen**, benennen Sie die Aktion, ordnen Sie ihr eine Beschreibung zu und wählen Sie einen Aktionstyp aus; klicken Sie anschließend auf **Weiter**.
3. Geben Sie die für den von Ihnen erstellten Aktionstyp erforderlichen Parameter an.  
Aktionstypen:  
 - [E-Mail senden](#email "E-Mail senden")
 - [IFTTT](#ifttt "IFTTT")
 - [Node-RED](#nodered "Node-RED")
 - [Webhook](#webhook "Webhook")
4. Klicken Sie auf **OK**, um die neue Aktion zu erstellen.

Die Aktion steht nun im Regeleditor zur Verfügung.

**Hinweis:** Die folgenden Beispiele stellen alle eine Aktion dar, die mithilfe der folgenden Regelbedingung einen Servicetechniker benachrichtigt, wenn die Temperatur, die durch die Eigenschaft `temp_cpu` eines Geräts angegeben wird, 80 Grad Fahrenheit übersteigt: `temp_cpu >= 80`

### E-Mail senden  
{: #email}
Verwenden Sie die Aktion 'E-Mail senden', um eine E-Mail an mindestens einen Empfänger zu senden, wenn eine Regel ausgelöst wird.

Beispiel: [E-Mail senden](#emailex).

Zum Konfigurieren der Aktion 'E-Mail senden' werden folgende Parameter verwendet:

Parameter | Beschreibung
---|---
Name | Der Name der Aktion, der im Dashboard 'Alerts' verwendet wird.
Beschreibung | Eine Kurzbeschreibung der Aktion.
Betreff | Die Betreffzeile der E-Mail. Die Standardbetreffzeile lautet 'IBM Watson IoT-Alert: E-Mail-Aktion'.
An | Wird ausgewählt, um den Alert nur an Sie selbst oder an eine durch Kommas getrennte Liste von E-Mail-Adressen zu senden. Wenn Sie auswählen, an sich selbst zu senden, wird die E-Mail an die E-Mail-Adresse von {{site.data.keyword.iot_short}} gesendet, mit der Sie sich angemeldet haben.
Cc | Kein Eintrag oder eine durch Kommas getrennte Liste von E-Mail-Adressen.
Der Hauptteil der E-Mail wird automatisch aus der Nachricht des Geräts zu dem Zeitpunkt erstellt, an dem die Regel ausgelöst wurde.  
**Wichtig:** E-Mails schließen standardmäßig keine Gerätedaten ein, die möglicherweise sensible Informationen enthalten. Ändern Sie die Einstellung für **Daten einfügen**, um Gerätedaten einzuschließen.

#### Beispiel: 'E-Mail senden' verwenden
{: #emailex}

In diesem Beispiel wird die Aktion so konfiguriert, dass die Funktion 'E-Mail senden' zum Senden einer E-Mail an den leitenden Servicetechniker und außerdem zum Senden einer Backup-E-Mail an dessen Manager verwendet wird.

Gehen Sie wie folgt vor, um die E-Mail-Aktion zu erstellen:
1. Wechseln Sie im {{site.data.keyword.iot_short}}-Dashboard zu **Regeln**.
2. Klicken Sie auf **Aktion erstellen**.
4. Geben Sie als Aktionsnamen `Serviceanforderungs-E-Mail senden` ein.
5. Geben Sie als Beschreibung `E-Mail an Servicetechniker und dessen Manager senden` ein.
3. Wählen Sie als Typ **E-Mail** aus.
6. Wählen Sie für das Feld 'An' **Bestimmte Personen** aus und geben Sie `service.engineer@company.com` ein.
7. Wählen Sie für das Feld 'CC' **Bestimmte Personen** aus und geben Sie `service.manager@company.com` ein.
8. Geben Sie in der Betreffzeile Folgendes ein: `Service erforderlich`.
10. Wählen Sie **Daten einfügen** aus, um die Gerätedaten in die E-Mail einzuschließen.
11. Klicken Sie auf **Fertigstellen**, um die Aktion zu speichern.  


### IFTTT  
{: #ifttt}

Verwenden Sie die Aktion 'IFTTT', um eine IFTTT-Anleitung auszulösen, wenn eine Regel ausgelöst wird. Weitere Informationen zum Auslösen von Aktionen als IFTTT-Anleitungen finden Sie auf der IFTTT-Site in [Maker Channel ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://ifttt.com/maker){: new_window}.

Beispiel: [IFTTT zum Posten einer Trello-Karte verwenden](#iftttex).

Zum Konfigurieren einer IFTTT-Aktion werden folgende Parameter verwendet:

Parameter | Beschreibung
---|---
Name | Der Name der Aktion, der im Dashboard 'Alerts' verwendet wird.
Beschreibung | Eine Kurzbeschreibung der Aktion.
Schlüssel | Der Maker Channel-Schlüssel, der zum Auslösen des Ereignisses verwendet wird.
Ereignis | Der Ereignisname, den Sie als Auslöser für das Maker-Ereignis konfiguriert haben. Sie können mehrere Anleitungen mit unterschiedlichen Auslösern erstellen, von denen jede einen anderen Ereignisnamen hat.
Wert 1-3 | In diesen Parametern, die an die Aktion in Ihrer IFTTT-Anleitung übergeben werden, können Sie beliebigen Inhalt übergeben. **Tipp:** Sie können die [Variablensubstitution](#variable_substitution) verwenden, um zusätzliche Daten dynamisch in den Header einzuschließen.

#### Beispiel: IFTTT zum Posten einer Trello-Karte verwenden {: #iftttex}

In diesem Beispiel ist die Aktion so konfiguriert, dass zum Posten einer Karte an eine Serviceanforderungsliste in Trello IFTTT verwendet wird.

Gehen Sie wie folgt vor, um die 'Karte in Trello posten' zu erstellen:
1.	Stellen Sie in IFTTT eine Verbindung zum Trello-Kanal her.
2.	Stellen Sie in IFTTT eine Verbindung zum Maker-Kanal her. Notieren Sie den IFTTT-Schlüssel. Sie benötigen diesen Schlüssel, um eine Verbindung von {{site.data.keyword.iot_short_notm}} zu IFTTT herzustellen.
5.	Erstellen Sie eine Anleitung in IFTTT:
 1. Klicken Sie auf **THIS**.
 2. Wählen Sie den Kanal **Maker** aus.  
 2. Klicken Sie auf **Receive a web request**.
 3. Geben Sie den Ereignisnamen `post-Trello-card` ein.
 4. Klicken Sie auf **THAT**.
 5. Wählen Sie den Kanal **Trello** aus.
 6. Wählen Sie das Trello-Board aus, in dem die Karte erstellt werden soll.
 7. Geben Sie den Namen einer Liste an, in der die Karten hinzugefügt werden sollen.
 8. Bearbeiten Sie den Titel und die Beschreibung.
 9. Ordnen Sie die Mitglieder '@service.engineer' und '@service.manager' zu.
 8. Klicken Sie auf **Create Action**.   
3. Wechseln Sie im {{site.data.keyword.iot_short}}-Dashboard zu **Regeln > Aktionen** und erstellen Sie eine neue Aktion, die folgende Parameter aufweist:
<ul>
<li>Typ - **IFTTT**</li>
<li>Name - `Serviceanforderungskarte posten`</li>
<li>Beschreibung - `IFTTT zum Posten einer Karte in der Serviceanforderungsliste in Trello verwenden`</li>
<li>Schlüssel - Ihr IFTTT-Schlüssel</li>
<li>Ereignis - `post-Trello-card`</li>
<li>Fügen Sie optional Werte für 'Wert 1-3' hinzu. **Tipp:** Sie können die [Variablensubstitution](#variable_substitution) verwenden, um Gerätedaten dynamisch einzuschließen.</li>
</ul>
4. Klicken Sie auf **OK**, um die Aktion zu speichern.


### Node-RED
{: #nodered}

Verwenden Sie die Aktion 'Node-RED', um eine Verbindung zu einer Node-RED-Anwendung herzustellen, wenn eine Regel ausgelöst wird. Weitere Informationen zur Verwendung von Node-RED finden Sie in [Apps mit der Starteranwendung von Internet of Things erstellen](https://www.ng.bluemix.net/docs/starters/IoT/iot500.html).

Beispiel: [Node-RED zum Senden einer Textnachricht verwenden](#noderedex).

Zum Konfigurieren einer Node-RED-Aktion werden folgende Parameter verwendet:

Parameter | Beschreibung
---|---
Name | Der Name der Aktion, der im Dashboard 'Alerts' verwendet wird.
Beschreibung | Eine Kurzbeschreibung der Aktion.
URL | Die URL des als Ziel verwendeten HTTP-Eingabeknotens von Node-RED.
Benutzername | Schließen Sie diese Angabe ein, falls sie für den Node-RED-Service erforderlich ist.
Kennwort | Schließen Sie diese Angabe ein, falls sie für den Node-RED-Service erforderlich ist. **Wichtig:** Das Kennwort wird in Klartext gesendet.
Hauptteil | Das Feld für den Hauptteil wird standardmäßig vorab mit allen Variablen gefüllt, die in der [Variablensubstitution](#variable_substitution) enthalten sind.

#### Beispiel: Node-RED zum Senden einer Textnachricht verwenden
{: #noderedex}

In diesem Beispiel ist die Aktion so konfiguriert, dass zum Senden einer Textnachricht an den Servicetechniker Node-RED mit einem Twilio-Knoten verwendet wird.

Gehen Sie wie folgt vor, um die Aktion 'Textnachricht senden' zu erstellen:
1. Suchen Sie in Twilio einen Nachrichtenübertragungsservice oder erstellen Sie einen neuen, um ihn zum Senden von Textnachrichten über Ihr Twilio-Konto zu verwenden. Informationen finden Sie in der [Twilio-Dokumentation ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.twilio.com/help){: new_window}.
2. Richten Sie in Bluemix ein Node-RED-Konto mit der Node-RED-URL `http://mynodered.mybluemix.net/red/` ein und greifen Sie darauf zu. Weitere Informationen finden Sie im Abschnitt [Apps mit Node-RED Starter erstellen](https://www.ng.bluemix.net/docs/starters/Node-RED/nodered.html) in der Bluemix-Dokumentation.
3. Erstellen Sie in Node-RED einen einfachen Ablauf aus zwei Knoten, wie beispielsweise [RTI-alert]->[SMS].  
Dabei ist der erste Knoten ein HTTP-Knoten und der zweite ist ein Twilio-Knoten.
 1. Fügen Sie den HTTP-Eingabeknoten hinzu und konfigurieren Sie ihn mit den folgenden Attributen:
  <ul>
  <li>Methode - POST</li>
  <li>URL - `RTI-alert`</li>
  <li>Name - RTI-Aktion</li>
  </ul>
  2. Fügen Sie den Ausgabeknoten für die HTTP-Antwort hinzu und stellen Sie zwischen diesem Knoten und den HTTP-Eingabeknoten eine Verbindung her, indem Sie zwischen dem Ausgabeport des einen eine Verbindung zum Eingabeport des anderen ziehen.
  3. Fügen Sie einen Twilio-Ausgabeknoten hinzu und konfigurieren Sie ihn mit den folgenden Attributen:
  <ul>
  <li>Service - **Externer Service**</li>
  <li>Twilio - Neue Twilio-API hinzufügen</li>
  <li>SMS an - `Telefonnummer des Servicetechnikers`</li>
  <li>Name - **SMS**</li>
  </ul>
  4. Verbinden Sie die Knoten miteinander  
  Verbinden Sie die http- und twilio-Knoten miteinander, indem Sie jeweils den Ausgabeport des einen Knotens zum Eingangsport des anderen Knotens ziehen.
  5. Klicken Sie auf die Schaltfläche für **Bereitstellen**, um den Ablauf auf dem Server bereitzustellen.
4. Wechseln Sie im {{site.data.keyword.iot_short}}-Dashboard zu **Regeln > Aktionen** und erstellen Sie eine neue Aktion, die folgende Parameter aufweist:
 - Typ - **Node-RED**
 - Name - `Textnachricht mithilfe von Node-RED und Twilio senden`
 - Beschreibung - `Textnachricht an den Servicetechniker senden`.
 - URL - `http://mynodered.mybluemix.net/RTI-alert`
 - Hauptteil   
 ```json
 {"text":"*Ein Gerät benötigt Ihre Aufmerksamkeit*\n Time: {{timestamp}}\n {{site.data.keyword.iot_short}} instance: {{tenantId}}\n Device: {{deviceId}}\n Rule: {{ruleName}}\n Description: {{ruleDescription}}\n Condition: {{ruleCondition}}\n Raw device message: \n{{message}}"}
 ```  
5. Klicken Sie auf **Fertigstellen**, um die Aktion zu speichern.



### Webhook
{: #webhook}

Verwenden Sie die Aktion 'Webhook', um eine HTTP-Anforderung an einen für Webhooks aktivierten Web-Service zu senden, wenn ein Alert ausgelöst wird. Ein Webhook kann beispielsweise verwendet werden, um eine Serviceanforderung für ein Asset zu öffnen, wenn ein Sensor im Gerät eine abnormalen Messwert berichtet.

Beispiel: [Webhook zum Posten in Slack verwenden](#webhookex).

Zum Konfigurieren einer Webhook-Aktion werden folgende Parameter verwendet:

Parameter | Beschreibung
---|---
Name | Der Name der Aktion, der im Dashboard 'Alerts' verwendet wird.
Beschreibung | Eine Kurzbeschreibung der Aktion.
URL | Die URL des als Ziel verwendeten und für Webhooks aktivierten Servers. **Tipp:** Sie können die [Variablensubstitution](#variable_substitution) verwenden, um zusätzliche Daten dynamisch in die URL einzuschließen.
Methode | Der Typ des auszuführenden Webhook-Aufrufs. Wählen Sie einen der folgenden Typen aus: GET, HEAD, OPTIONS, PATCH, PUT, POST oder DELETE.
Benutzername | Schließen Sie diese Angabe ein, wenn sie für den Web-Service erforderlich ist.
Kennwort | Schließen Sie diese Angabe ein, wenn sie für den Web-Service erforderlich ist. **Wichtig:** Das Kennwort wird in Klartext gesendet.
Header | Header bestehen aus Schlüssel-/Wertpaaren. **Tipp:** Sie können die [Variablensubstitution](#variable_substitution) verwenden, um zusätzliche Daten dynamisch in den Header einzuschließen.
Inhaltstyp | Der Typ des Hauptteilinhalts: URL-verschlüsseltes JSON-, XML- oder WWW-Format oder unverschlüsselter Text.  Verfügbar für die Methoden OPTIONS, PATCH, PUT, POST und DELETE.
Hauptteil | Der Hauptteil des Webhook-Aufrufs.  Verfügbar für die Methoden OPTIONS, PATCH, PUT, POST und DELETE. Das Feld für den Hauptteil wird standardmäßig vorab mit allen Variablen gefüllt, die in der [Variablensubstitution](#variable_substitution) enthalten sind. **Wichtig:** Für den Webhook-Server ist es möglicherweise erforderlich, dass der Hauptteil bestimmte Felder enthält. Beispielsweise muss ein Slack-Webhook das Feld 'text' enthalten.   

#### Beispiel: Webhook zum Posten in Slack verwenden
{: #webhookex}

In diesem Beispiel ist die Aktion so konfiguriert, dass zum Posten einer Nachricht im Slack-Kanal '#service-requests' (Serviceanforderungen) ein Webhook verwendet wird.

Gehen Sie wie folgt vor, um die Aktion 'In Slack posten' zu erstellen:
1. Richten Sie in Slack für den Kanal '#service-requests' die Integration für eingehende Webhooks ein. Notieren Sie die URL des Webhooks. Weitere Informationen finden Sie in der [Slack-Dokumentation ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://api.slack.com/incoming-webhooks){: new_window}.
2. Wechseln Sie im {{site.data.keyword.iot_short}}-Dashboard zu **Regeln > Aktionen** und erstellen Sie eine neue Aktion, die folgende Parameter aufweist:
 - Name - `Serviceanforderung in Slack posten`
 - Typ - **Webhook**
 - URL - `URL Ihres Slack-Webhooks`
 - Methode - **POST**
 - Inhaltstyp - `application/json`
 - Hauptteil   
 ```json
 {"text":"*Ein Gerät benötigt Ihre Aufmerksamkeit*\n Time: {{timestamp}}\n {{site.data.keyword.iot_short}} instance: {{tenantId}}\n Device: {{deviceId}}\n Rule: {{ruleName}}\n Description: {{ruleDescription}}\n Condition: {{ruleCondition}}\n Raw device message: \n{{message}}"}
 ```  
  **Wichtig:** Der Slack-Webhook muss mindestens das Feld 'text' enthalten. Informationen finden Sie in der Slack-Dokumentation im Abschnitt [Incoming Webhooks ![Symbol für externen Link](../icons/launch-glyph.svg)](https://api.slack.com/incoming-webhooks "Slack-Dokumentation"){: new_window}.
11. Klicken Sie auf **Fertigstellen**, um die Aktion zu speichern.


### Variablensubstitution  
{: #variable_substitution}

Schließen Sie folgende Variablensubstitutionen ein, um Gerätedaten dynamisch einzubeziehen. Die Variable muss in doppelte geschweifte Klammern gesetzt werden.

Variable | Beschreibung
---|---
**URL, Kopfzeile und Hauptteil** |
`{{timestamp}}` | Die Zeitmarke der Nachricht.
`{{orgId}}` | Die Organisations-ID des {{site.data.keyword.iot_short_notm}}-Service.
`{{tenantId}}` | Nicht mehr verwendet: Die ID des {{site.data.keyword.iotrtinsights_full}}-Service.
`{{deviceId}}` | Die ID des Geräts.
`{{ruleName}}` | Der Name der Regel, die die Aktion enthält.
`{{ruleID}}` | Die ID der Regel, die die Aktion enthält.
**Nur Hauptteil** |
`{{ruleDescription}}`| Die Beschreibung der Regel, die die Aktion enthält.
`{{ruleCondition}}` | Die Regelbedingung, die die Aktion ausgelöst hat.
`{{message}}` | Die Rohfassung der Gerätenachricht, die den Datenpunktwert enthält, durch den die Regel ausgelöst wurde.

## Anleitungen für Cloud Analytics

Die folgenden Anleitungen beschreiben die Vorgehensweise zur Verwendung von Cloud Analytics-Funktionen in verschiedenen Anwendungsfällen:

- [Analyse von Echtzeitdaten mit IBM Watson™ IoT Platform Analytics ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/recipes/tutorials/real-time-data-analysis-using-ibm-watson-iot-platform-analytics/){: new_window}

- [Vorhersageanalyse für IOT-Beispieldaten ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/recipes/tutorials/predictive-analytics-on-iot-sample-data/){: new_window}

- [Gerätelistenkarte VEREINFACHT die Echtzeitgeräteüberwachung im WIoTP-Dashboard ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/recipes/tutorials/device-list-card-simplifies-real-time-device-monitoring-on-wiotp-dashboard/){: new_window}

- [Aktionen in IBM Watson IoT Platform Cloud Analytics ausführen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/recipes/tutorials/perform-actions-in-ibm-watson-iot-platform-cloud-analytics/){: new_window}

- [Mithilfe von IBM Data Science Experience Anomalien in Zeitreihen erkennen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.ibm.com/recipes/tutorials/use-ibm-data-science-experience-to-detect-time-series-anomalies/){: new_window}
