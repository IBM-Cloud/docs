---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# Beispiele für Aktionen

Die Aktionstypen "E-Mail senden", "IFTTT", "Node-RED" und "Webhook" bieten eine Vielzahl an Optionen zum Ausführen von Tasks, die nur durch Ihre Vorstellungskraft und die von den anderen Tools verwendeten Konnektoren begrenzt werden. Beispiele sind unter anderem Aktionen zum Posten von Gerätestatusnachrichten in Slack, das Senden von Textnachrichten an den Kundendienst oder das Erstellen von Service Requests für Geräte.
{: shortdesc}

Die nachfolgenden Beispiele stellen alle eine Aktion dar, bei der ein Servicetechniker benachrichtigt wird, wenn die von dem Datenpunkt "temp" eines Geräts dargestellte Temperatur 100 Grad überschreitet. Dabei wird folgende Regelbedingung verwendet: `temp >= 100`

Sie können einen oder mehrere der folgenden Aktionstypen auslösen, wenn die Regelbedingung auftritt:   
 - [E-Mail senden](#emailex "E-Mail senden")
 - [Webhook](#webhookex "Webhook")
 - [Node-RED](#noderedex "Node-RED")
 - [IFTTT](#iftttex "IFTTT")

## "E-Mail senden" verwenden{: #emailex}
In diesem Beispiel ist die Aktion so konfiguriert, dass das Real-Time Insights-Feature "E-Mail senden" verwendet wird, um eine E-Mail an den hauptverantwortlichen Servicetechniker zu senden und eine Kopie der E-Mail an dessen Manager.

Gehen Sie wie folgt vor, um die E-Mail-Aktion zu erstellen:
1. Gehen Sie in Real-Time Insights zu **Analytics > Aktionen**.
2. Klicken Sie auf **Neue Aktion hinzufügen**.
3. Wählen Sie den Typ **E-Mail senden** aus.
4. Geben Sie den Aktionsnamen `E-Mail mit Service Request senden` ein.
5. Geben Sie die Beschreibung `E-Mail an Servicetechniker und seinen Manager senden` ein.
6. Geben Sie in das Feld "An" Folgendes ein: `service.engineer@company.com`.
7. Geben Sie in das Feld "CC" Folgendes ein: `service.manager@company.com`.
8. Geben Sie in der Betreffzeile Folgendes ein: `Service erforderlich`.
9. Wählen Sie "Präfix '{{site.data.keyword.iotrtinsights_short}}-Alert' voranstellen" aus, um deutlich zu machen, woher die E-Mail kommt.
10. Damit die Gerätedaten in der E-Mail angegeben werden, wählen Sie das Kontrollkästchen **Keine Gerätedaten in der E-Mail-Nachricht aufführen** ab.
11. Klicken Sie auf **OK**, um die Aktion zu speichern.   




## Webhook zum Posten in Slack verwenden{: #webhookex}

In diesem Beispiel ist die Aktion so konfiguriert, dass ein Webhook zum Posten einer Nachricht an den Slack-Kanal #service-requests verwendet wird.

Gehen Sie wie folgt vor, um die Aktion zum Posten in Slack zu erstellen:
1. Richten Sie in Slack die Integration ankommender Webhooks für den Kanal #service-requests ein. Notieren Sie die Webhooks-URL. Weitere Informationen finden Sie in der [Slack-Dokumentation](https://api.slack.com/incoming-webhooks).
2. Gehen Sie in Real-Time Insights zu **Analytics > Aktionen** und erstellen Sie eine neue Aktion mit den folgenden Parametern:
 - Typ - **Webhook**
 - Name - `Service Request in Slack posten`
 - URL - `Ihre Slack-Webhooks-URL`
 - Methode - **POST**
 - Inhaltstyp - Anwendung/JSON
 - Wählen Sie **Angepassten Nachrichtenhauptteil verwenden** aus
 - Hauptteil```{"text":"*Ein Gerät muss geprüft werden*\n Zeit: {{timestamp}}\n {{site.data.keyword.iotrtinsights_short}}-Instanz: {{tenantId}}\n Gerät: {{deviceId}}\n Regel: {{ruleName}}\n Beschreibung: {{ruleDescription}}\n Bedingung: {{ruleCondition}}\n Unformatierte Gerätenachricht: \n{{message}}"}```
 {: codeblock}  
 **Wichtig:** Der Slack-Webhook muss mindestens das Feld "text" enthalten. Weitere Informationen hierzu finden Sie im Thema [Incoming Webhooks](https://api.slack.com/incoming-webhooks "Slack-Dokumentation") in der Slack-Dokumentation.
11. Klicken Sie auf **OK**, um die Aktion zu speichern.

## Node-RED zum Senden einer Textnachricht verwenden{: #noderedex}

In diesem Beispiel ist die Aktion so konfiguriert, dass Node-RED mit einem Twilio-Knoten verwendet wird, um eine Textnachricht an den Servicetechniker zu senden.

Gehen Sie wie folgt vor, um die Aktion zum Senden einer Textnachricht zu erstellen:
1. Lokalisieren Sie oder erstellen Sie in Twilio einen neuen Nachrichtenübertragungsservice, den Sie zum Senden von Textnachrichten von Ihrem Twilio-Konto verwenden. Weitere Informationen finden Sie in der [Twilio-Dokumentation](https://www.twilio.com/help).
1. Richten Sie in Bluemix Ihr Node-RED-Konto ein und greifen Sie darauf mit der Node-RED-URL `http://mynodered.mybluemix.net/red/` zu. Weitere Informationen finden Sie im Abschnitt [Creating apps with Node-RED Starter](https://www.ng.bluemix.net/docs/starters/Node-RED/nodered.html) in der Bluemix-Dokumentation.
2. Erstellen Sie in Node-RED einen einfachen Ablauf zwischen zwei Knoten wie beispielsweise [RTI-Alert]->[SMS].
Dabei ist der erste Knoten ein HTTP-Knoten und der zweite Knoten ein Twilio-Knoten.
 1. Fügen Sie den Eingabeknoten "HTTP" hinzu und konfigurieren Sie ihn mit den folgenden Attributen:
  <ul>
  <li>Methode - POST</li>
  <li>URL - `RTI-Alert`</li>
  <li>Name - RTI-Aktion</li>
  </ul>
  2. Fügen Sie einen Ausgabeknoten "HTTP-Antwort" hinzu und verbinden Sie diesen und den Eingabeknoten "HTTP", indem Sie den Ausgabeport eines Knotens zu dem Eingabeport des anderen Knotens ziehen.
  3. Fügen Sie einen Ausgabeknoten "Twilio" hinzu und konfigurieren Sie diesen mit den folgenden Attributen:
  <ul>
  <li>Service - **Externer Service**</li>
  <li>Twilio - Neue Twilio-API hinzufügen</li>
  <li>SMS an - `Telefonnummer des Servicetechnikers`</li>
  <li>Name - **SMS**</li>
  </ul>
  4. Verbinden Sie die Knoten.
  Verbinden Sie die Knoten "HTTP" und "Twilio", indem Sie den Ausgabeport eines Knotens zu dem Eingabeport des anderen Knotens ziehen.
  5. Klicken Sie auf die Schaltfläche **Bereitstellen**, um den Ablauf zu dem Server bereitzustellen.
3. Gehen Sie in {{site.data.keyword.iotrtinsights_short}} zu **Analytics > Aktionen** und erstellen Sie eine Aktion mit den folgenden Parametern:
 - Typ - **Node-RED**
 - Name - `Text über Node-RED und Twilio senden`
 - Beschreibung - `Textnachrichtenalert an den Servicetechniker senden`
 - URL - `http://mynodered.mybluemix.net/RTI-alert`
 - HAUPTTEIL```{"text":"*Ein Gerät muss geprüft werden*\n Zeit: {{timestamp}}\n {{site.data.keyword.iotrtinsights_short}}-Instanz: {{tenantId}}\n Gerät: {{deviceId}}\n Regel: {{ruleName}}\n Beschreibung: {{ruleDescription}}\n Bedingung: {{ruleCondition}}\n Unformatierte Gerätenachricht: \n{{message}}"}```
 {: codeblock}
4. Klicken Sie auf **OK**, um die Aktion zu speichern.

## IFTTT zum Posten einer Trello-Karte verwenden{: #iftttex}

In diesem Beispiel wird die Aktion so konfiguriert, dass IFTTT zum Posten einer Karte an eine Liste mit Service Requests in Trello verwendet wird.

Gehen Sie wie folgt vor, um die Aktion zum Posten einer Karte in Trello zu erstellen:
1.	Stellen Sie in IFTTT eine Verbindung zu dem Trello-Kanal her.
2.	Stellen Sie in IFTTT eine Verbindung zu dem Maker-Kanal her. Notieren Sie Ihren IFTTT-Schlüssel. Sie benötigen diesen, um von Real-Time Insights eine Verbindung zu IFTTT herzustellen.
5.	Erstellen Sie in IFTTT ein Rezept:
 1. Klicken Sie auf **THIS**.
 2. Wählen Sie den **Maker**-Kanal aus.   
 2. Klicken Sie auf **Webanforderung empfangen**.
 3. Geben Sie den Ereignisnamen `Trello-Karte-posten` ein.
 4. Klicken Sie auf **THAT**.
 5. Wählen Sie den **Trello**-Kanal aus.
 6. Wählen Sie das Trello-Board aus, in dem die Karte erstellt werden soll.
 7. Geben Sie den Namen einer Liste ein, in der die Karten hinzugefügt werden sollen.
 8. Bearbeiten Sie den Titel und die Beschreibung.
 9. Weisen Sie die Mitglieder @service.engineer und @service.manager zu.
 8. Klicken Sie auf **Aktion erstellen**.   
3. Gehen Sie in {{site.data.keyword.iotrtinsights_short}} zu **Analytics > Aktionen** und erstellen Sie eine Aktion mit den folgenden Parametern:
<ul>
<li>Typ - **IFTTT**</li>
<li>Name - `Service Request-Karte posten`</li>
<li>Beschreibung - `IFTTT zum Posten einer Karte in die Liste der Service Requests in Trello verwenden`. </li>
<li>Schlüssel - Ihr IFTTT-Schlüssel</li>
<li>Ereignis - `Trello-Karte-posten`</li>
<li>Fügen Sie optional Werte für Wert 1 bis 3 hinzu. **Tipp:** Sie können [Variablensubstitution](actions.html#variable_substitution) verwenden, um Gerätedaten dynamisch einzubeziehen. </li>
</ul>
4. Klicken Sie auf **OK**, um die Aktion zu speichern.
