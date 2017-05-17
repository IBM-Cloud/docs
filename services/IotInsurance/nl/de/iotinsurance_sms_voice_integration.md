---

copyright:
  years: 2016, 2017
lastupdated: "2017-05-02"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# SMS und Übertragung von gesprochenen Nachrichten aktivieren
{: #supportedcloud}

{{site.data.keyword.iotinsurance_full}} unterstützt die Integration mit Twilio zur Aktivierung von SMS und der Übertragung von gesprochenen Nachrichten. Twilio ist eine Anwendung eines anderen Anbieters, die Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard installieren können.
{: shortdesc}

## Voraussetzungen
Wenn Sie die Übertragung von gesprochenen Nachrichten aktivieren möchten, benötigen Sie ein Twilio-Konto mit der entsprechenden Berechtigung und eine Twilio-Telefonnummer für abgehende Anrufe. Wenn Sie ein kostenfreies Twilio-Konto verwenden, müssen Sie darüber hinaus eine Telefonnummer für das Empfangen von Anrufen oder Nachrichten berechtigen. Weitere Informationen finden Sie in der [Twilio-Dokumentation![Symbol für externen Link](../../icons/launch-glyph.svg)](https://support.twilio.com/hc/en-us/articles/223136107-How-does-Twilio-s-Free-Trial-work-){:new_window}.

## Twilio-Instanz erstellen und konfigurieren
1. Erstellen Sie eine Twilio-Instanz in derselben {{site.data.keyword.Bluemix_notm}}-Organisation und im selben Bereich, in der bzw. dem Sie {{site.data.keyword.iotinsurance_short}} installiert haben. 
    1. Melden Sie sich bei [{{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net) an. 
    2. Wählen Sie die Registerkarte **Katalog** aus. 
    3. Suchen Sie den Abschnitt 'Mobil' des Servicekatalogs und klicken Sie auf **Twilio**. 

    **Tipp:** Klicken Sie [hier ![Symbol für externen Link ](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.ng.bluemix.net/catalog/services/twilio/){: new_window}, um die Twilio-Seite direkt aufzurufen. {: tip}

    4. Geben Sie auf der Twilio-Seite Ihre Berechtigungsnachweise an und führen Sie die Bindung für die Anwendung aus. Gehen Sie hierzu wie folgt vor: 

      1. Geben Sie `Twilio-00` als Servicenamen an. **Wichtig:** Sie müssen `Twilio-00` verwenden, um erfolgreich eine Verbindung zu {{site.data.keyword.iotinsurance_short}} herzustellen. 

      2. Geben Sie Ihre Twilio-Berechtigungsnachweise ein. 

      3. Wählen Sie im Menü **Verbindung herstellen zu** Ihre 'iot4i-action-engine'-Anwendung aus, um die Twilio-Instanz an {{site.data.keyword.iotinsurance_short}} zu binden. 

      4. Klicken Sie auf **Erstellen**.   

    Die Twilio-Anwendung wird in Ihrer Umgebung installiert. Sie werden in einer Nachricht dazu aufgefordert, für die 'iot4i-action-engine'-Anwendung ein erneutes Staging bzw. einen Neustart durchzuführen, um die Bindung zu aktivieren. Sie können den Neustart jetzt durchführen oder nachdem Sie im nächsten Schritt die neue Umgebungsvariable hinzugefügt haben. 

2. Erstellen Sie eine Umgebungsvariable mit dem Namen TWILIO_FROM_NUMBER für die 'iot4i-action-egine'-Komponente. 
    1. Öffnen Sie im Bluemix-Dashboard die 'iot4i-action-engine'-Anwendung. 
    2. Wählen Sie **Laufzeit** aus und klicken Sie dann auf **Umgebungsvariablen**. 
    3. Klicken Sie im Abschnitt **Benutzerdefiniert** auf **Hinzufügen**. 
    4. Geben Sie in der Namensspalte `TWILIO_FROM_NUMBER` und anschließend in der Wertspalte Ihre sprach- und SMS-fähige Telefonnummer ein. 
    5. Klicken Sie auf **Speichern**. 

3. Starten Sie die 'iot4i-action-engine'-Anwendung erneut, indem Sie auf das Neustartsymbol neben der Schaltfläche für die Routen klicken. 

## SMS- und Sprachaktionen zu einem Shield hinzufügen

Wenn Sie SMS- und Sprachfunktionen zu einem Shield hinzufügen möchten, müssen Sie die folgenden Aktionen zur Shielddefinition hinzufügen: 
  - `send-sms`
  - `phone-call`

Ein Beispiel für ein Shield, das eine Liste mit Aktionen enthält, finden Sie in [Einfaches Shield-Beispiel erstellen![Symbol für externen Link](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/blob/master/bl/shield.js){:new_window}. In diesem Beispiel können die SMS- und Sprachaktionen zur Liste der Aktionen hinzugefügt werden, die die Aktionen `email` und `pushios` enthält. 

Weitere Informationen zur Shield-Erstellung finden Sie in [Shield-Toolkit verwenden](iotinsurance_shield_toolkit.html). 
