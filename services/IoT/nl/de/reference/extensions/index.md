---

copyright:
  years: 2015, 2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Externe Services integrieren
{: #ref-index}
Letzte Aktualisierung: 26. September 2016
{: .last-updated}

Die Integration von externen Services ermöglicht Ihnen den Zugriff auf Daten und Operationen von Drittanbietern oder externen Services innerhalb Ihrer {{site.data.keyword.iot_full}}-Organisation.

## Jasper
{: #jasper}

Jasper ist eine Verwaltungs- und Managementplattform für SIM-Geräte. Jasper ist in das Dashboard von {{site.data.keyword.iot_short_notm}} integriert, sodass es nun möglich ist, Jasper-Geräte über Ihr Organisationsdashboard von {{site.data.keyword.iot_short_notm}} zu verwalten.

### Unterstützte Operationen für Jasper

Die von Ihrer Plattform bereitgestellte Integration von Jasper bietet Unterstützung für folgende Jasper-Operationen:

- Gesamte Jasper-Daten anzeigen
  - Folgendes wird angezeigt: Status, Tarifplan, Datennutzung für den Monat bisher, SMS-Nutzung für den Monat bisher, Telefonnutzung für den Monat bisher, Überschreitungsgrenzwerte, Hinzufügungsdatum und Änderungsdatum.
- SIM-Aktivierungsstatus ändern.
  - Folgendes kann ausgewählt werden: Bestand, Aktivierungsbereit, Aktiviert, Inaktiviert und Ruhezustand.
- SIM-Nutzung anzeigen
  - Folgendes wird angezeigt: Zyklusstartdatum, abrechnungsfähige und gesamte Datennutzung, abrechnungsfähige und gesamte SMS-Nutzung, abrechnungsfähige und gesamte Telefonnutzung.
  - Das Zyklusstartdatum kann im Format JJJJ-MM-TT festgelegt werden.
- Send SMS to SIM
- Tarifplan ändern

Sie können auf diese Operationen im Geräte-Drilldown eines verbundenen Jasper-Geräts zugreifen, nachdem die nachfolgend beschriebenen Konfigurationsschritte abgeschlossen sind.


### Konfiguration für Jasper

Damit eine Verbindung zwischen Ihrem Jasper-Service mit Ihrer {{site.data.keyword.iot_short_notm}}-Organisation hergestellt werden kann, müssen zuvor zwei Konfigurationsphasen ausgeführt werden. Zunächst muss {{site.data.keyword.iot_short_notm}} mit Ihrem Jasper-Service verbunden werden, anschließend müssen Ihre {{site.data.keyword.iot_short_notm}}-Geräte konfiguriert werden.


1. Jasper-Erweiterung aktivieren. Führen Sie folgende Schritte aus, um die Integration von Jasper in Ihre {{site.data.keyword.iot_short_notm}}-Organisation zu ermöglichen.
  1. Wählen Sie im {{site.data.keyword.iot_short_notm}}-Dashboard die Option **Erweiterungen**.
  2. Klicken Sie auf der Seite **Erweiterungen** auf **Erweiterung hinzufügen**.
  3. Klicken Sie neben 'Jasper' auf **Hinzufügen**.
  4. Geben Sie Ihren Benutzernamen, das Kennwort, den Zugriffsschlüssel und die Domänen-ID für Jasper ein.
  5. Klicken Sie auf **Fertig**.

2. Geräte konfigurieren
Sie können die Geräte, die sowohl mit Ihrer {{site.data.keyword.iot_short_notm}}-Organisation als auch mit Ihrem Jasper-Konto verbunden sind, so konfigurieren, dass Daten von Jasper im Dashboard von {{site.data.keyword.iot_short_notm}} angezeigt werden.  
**Wichtig:** Die Jasper-Konfiguration kann nicht im Rahmen des Prozesses zum Hinzufügen von Geräten angewendet werden, nur zuvor bereits verbundene Geräte können mit Jasper konfiguriert werden.  
Führen Sie folgende Schritte aus, um Ihre mit Jasper verbundenen Geräte zu konfigurieren:
 1. Suchen Sie auf der Registerkarte 'Geräte' in Ihrem {{site.data.keyword.iot_short_notm}}-Dashboard nach dem zu konfigurierenden und mit Jasper verbundenen Gerät.
 2. Wählen Sie das Gerät aus, um die Ansicht Drilldown-Ansicht für Geräte zu öffnen.
 3. Blättern Sie abwärts zur Option *Erweiterungskonfiguration*.
 4. Geben Sie die Erweiterungskonfiguration ein, indem Sie das folgende JSON-Format verwenden, und klicken Sie anschließend auf **Änderungen bestätigen**, um Ihre Konfiguration zu speichern.  

```json  
    {
        "jasper": {
            "iccid": "string"
        }
    }

```

Wenn die Organisation erfolgreich konfiguriert ist, wird der Abschnitt *Erweiterungen* unterhalb des Abschnitts zur Erweiterungskonfiguration in der Drilldown-Ansicht für Geräte angezeigt.

## AT&T
{: #att}

### Unterstützte Operationen für AT&T

Die AT&T-Erweiterung ermöglicht folgende AT&T-Operationen:

- Gesamte AT&T- Daten anzeigen
  - Folgendes wird angezeigt: Status, Tarifplan, Datennutzung für den Monat bisher, SMS-Nutzung für den Monat bisher, Telefonnutzung für den Monat bisher, Überschreitungsgrenzwerte, Hinzufügungsdatum und Änderungsdatum.
- SIM-Aktivierungsstatus ändern.
  - Folgendes kann ausgewählt werden: Bestand, Aktivierungsbereit, Aktiviert, Inaktiviert und Ruhezustand.
- SIM-Nutzung anzeigen
  - Folgendes wird angezeigt: Zyklusstartdatum, abrechnungsfähige und gesamte Datennutzung, abrechnungsfähige und gesamte SMS-Nutzung, abrechnungsfähige und gesamte Telefonnutzung.
  - Das Zyklusstartdatum kann im Format JJJJ-MM-TT festgelegt werden.
- Send SMS to SIM
- Tarifplan ändern

### Konfiguration für AT&T

Um Ihre {{site.data.keyword.iot_short_notm}}-Organisation mit AT&T zu verbinden, müssen Sie eine Organisationskonfiguration und eine Gerätekonfiguration ausführen.

Führen Sie folgende Schritte aus, um Ihre {{site.data.keyword.iot_short_notm}}-Plattform zu konfigurieren.

1. AT&T-Erweiterung aktivieren. Führen Sie folgende Schritte aus, um die Integration von AT&T und der {{site.data.keyword.iot_short_notm}}-Organisation zu aktivieren:
  1. Wählen Sie im {{site.data.keyword.iot_short_notm}}-Dashboard die Option **Erweiterungen**.
  2. Klicken Sie auf der Seite **Erweiterungen** auf **Erweiterung hinzufügen**.
  3. Klicken Sie neben AT&T auf die Option **Hinzufügen**.
  4. Geben Sie Ihren Benutzernamen, das Kennwort, den Zugriffsschlüssel und die Domänen-ID für AT&T ein.
  5. Klicken Sie auf **Fertig**.

Zum Verbinden Ihrer {{site.data.keyword.iot_short_notm}}-Organisation mit Ihrem AT&T-Konto müssen zunächst zwei Konfigurationsphasen ausgeführt werden. Führen Sie die Konfiguration der Organisation aus und konfigurieren Sie anschließend Ihre Geräte.


2. Geräte konfigurieren
Sie können die Geräte, die sowohl mit Ihrer {{site.data.keyword.iot_short_notm}}-Organisation als auch mit Ihrem AT&T-Konto verbunden sind, so konfigurieren, dass Daten von AT&T im {{site.data.keyword.iot_short_notm}}-Dashboard angezeigt werden.  
**Wichtig:** Die AT&T-Konfiguration kann nicht im Rahmen des Prozesses zum Hinzufügen von Geräten angewendet werden, nur zuvor bereits verbundene Geräte können mit AT&T konfiguriert werden.  
Führen Sie folgende Schritte aus, um Ihre mit AT&T verbundenen Geräte zu konfigurieren:
 1. Suchen Sie auf der Registerkarte 'Geräte' in Ihrem {{site.data.keyword.iot_short_notm}}-Dashboard nach dem zu konfigurierenden und mit AT&T verbundenen Gerät.
 2. Wählen Sie das Gerät aus, um die Ansicht Drilldown-Ansicht für Geräte zu öffnen.
 3. Blättern Sie abwärts zur Option *Erweiterungskonfiguration*.
 4. Geben Sie die Erweiterungskonfiguration ein, indem Sie das folgende JSON-Format verwenden, und klicken Sie anschließend auf **Änderungen bestätigen**, um Ihre Konfiguration zu speichern.  

```json  
    {
        "atnt": {
            "iccid": "string"
        }
    }

```

Wenn die Organisation erfolgreich konfiguriert ist, wird der Abschnitt *Erweiterungen* unterhalb des Abschnitts zur Erweiterungskonfiguration in der Drilldown-Ansicht für Geräte angezeigt.


## ARM mbed-Connector
{: #arm}

Der ARM mbed-Konnektor ermöglicht Ihnen, für Ihr ARM mbed-Gerät eine Verbindung zu {{site.data.keyword.iot_short_notm}} herzustellen. Die ARM mbed-Erweiterung ermöglicht dem ARM mbed-Portal und {{site.data.keyword.iot_short_notm}}, Daten vom ARM mbed-Portal zu empfangen und an dieses zu senden.

### Konfiguration für die Einrichtung


1. Aktivieren Sie die Erweiterung für den ARM mbed-Konnektor. Zum Aktivieren der Erweiterung für den ARM mbed-Konnektor führen Sie folgende Schritte aus:
  1. Wählen Sie im {{site.data.keyword.iot_short_notm}}-Dashboard die Option **Einstellungen** aus und navigieren Sie zu **Erweiterungen**.
  2. Klicken Sie im Menü **Erweiterungen** auf **Erweiterung hinzufügen**.
  3. Klicken Sie neben der Erweiterung für den ARM bed-Konnektor auf **Hinzufügen**.
  4. Geben Sie Ihren Zugriffsschlüssel und Ihre Domänen-ID für ARM mbed ein. Sie finden diese Angaben mithilfe des ARM bed-Portals unter https://connector.mbed.com.
  5. Prüfen Sie, ob die Berechtigungsnachweise richtig sind, indem Sie auf die Schaltfläche **Verbindung überprüfen** klicken.
  6. Klicken Sie auf **Fertig**.

### Nutzdatenformat

Die von der ARM mbed-Plattform eingehenden Nachrichten haben den Typ 'Benachrichtigung' oder 'asynchrone Antwort'. {{site.data.keyword.iot_short_notm}} kann Befehle an Geräte senden, die mit der ARM mbed-Plattform verbunden sind.

#### Benachrichtigungen

Benachrichtigungen werden durch Änderungen in den Geräte- oder Sensordaten generiert. Nachdem {{site.data.keyword.iot_short_notm}} die Nachricht verarbeitet hat, wird sie auf dieselbe Weise in das Ereignistopic des Geräts geschrieben wie bei einem Gerät, das direkt mit {{site.data.keyword.iot_short_notm}} verbunden ist. Der Ereignistyp für Benachrichtigungen, die von Geräten stammen, die mit der ARM mbed-Plattform verbunden sind, lautet `notify`.

Das folgende Codebeispiel zeigt das Nutzdatenformat für eine Benachrichtigung, die von der API der ARM mbed-Plattform gesendet wurde:

```
{
  "ep":<Endpunkt/Geräte-ID>,
  "path":<Ressourcenpfad>,
  "ct":<Inhaltstyp>,
  "payload":<Nutzdaten mit Base64-Codierung>,
  "max-age":<Gültigkeit der Nutzdaten in Sekunden>
}
```

#### Asynchrone Antworten

Wenn {{site.data.keyword.iot_short_notm}} einen Befehle an ein mit der ARM mbed-Plattform verbundenes Gerät sendet, sendet das Gerät eine Bestätigungsnachricht zurück an {{site.data.keyword.iot_short_notm}}. Diese Bestätigungsnachricht wird als *asynchrone Antwort* bezeichnet und verwendet den Ereignistyp `asyncResponse`.

Das folgende Codebeispiel zeigt das Nutzdatenformat für eine asynchrone Antwort, die vom ARM mbed-Cloud-Service gesendet wurde:

```
{
  "id":<Transaktions-ID>,
  "status":<200, falls Befehl erfolgreich ausgeführt wurde. Überprüfen Sie weitere HTTP-Antwortcodes>,
  "ct":<Inhaltstyp>,
  "max-age":<Gültigkeit der Nutzdaten in Sekunden>,
  "payload":<Nutzdaten mit Base64-Codierung>,
  "ep":<Endpunkt/Geräte-ID, der/die vom Befehl betroffen ist>,
  "path":<Ressourcenpfad, der vom Befehl betroffen ist>
}
```

#### Befehle an die ARM mbed-Plattform senden

{{site.data.keyword.iot_short_notm}} kann Befehle an Geräte senden, die mit der ARM mbed-Plattform verbunden sind. An die ARM mbed-Plattform gesendete Befehle müssen das folgende JSON-Format aufweisen.

```
{
  "method":<PUT oder POST>,
  "deviceId":<Endpunkt/Geräte-ID>,
  "resourceId":<Ressourcenpfad>,
  "payload": <Nutzdaten mit Base64-Codierung>
}
```
Bei der gewählten Methode muss die Groß-/Kleinschreibung beachtet werden. Die Angabe '/' vor dem Ressourcenpfad muss übersprungen werden.


Die Nutzdaten müssen an das folgende Topic publiziert werden:

```
iot-2/type/<Gerätetyp>/id/<Geräte-ID>/cmd/<Befehlstyp>/fmt/<Befehlsformat>
```


## Orange
{: #orange}

Die Orange-Erweiterung ermöglicht Ihnen die Daten der SIM-Karte von Geräten anzuzeigen, die mit {{site.data.keyword.iot_short_notm}} verbunden sind und in die eine Orange-SIM-Arte installiert ist.

https://developer.ibm.com/iotplatform/2016/03/30/watson-iot-platform-integration-with-orange-beta/

### Unterstützte Operationen für Orange

Wenn Sie ein Gerät haben, das mit Ihrem {{site.data.keyword.iot_short_notm}}-Service verbunden ist und eine Orange-SIM-Karte hat, können Sie die Orange-Erweiterung verwenden, um die folgenden Daten der SIM-Karte anzuzeigen:

- SIM-Seriennummer
- Aktivierungsstatus
- Letzter Änderungsstatus
- Letzter Aktualisierungsstatus
- Standortstatus

### Konfiguration für Orange



Gehen Sie wie folgt vor, die Orange-Erweiterung zu aktivieren:

1. Wählen Sie im {{site.data.keyword.iot_short_notm}}-Dashboard die Option **Erweiterungen**.
2. Klicken Sie auf der Seite **Erweiterungen** auf **Erweiterung hinzufügen**.
3. Klicken Sie neben der Orange-Erweiterung auf **Hinzufügen**.
4. Geben Sie Ihren Benutzernamen und das Kennwort für Orange ein.
6. Klicken Sie auf **Fertig**.

Nach dem Aktivieren der Orange-Erweiterung muss jedes Gerät mit einer Orange-SIM-Karte für die Anzeige von Daten der Orange-SIM-Karte konfiguriert werden.

1. Suchen Sie auf der Registerkarte 'Geräte' in Ihrem {{site.data.keyword.iot_short_notm}}-Dashboard nach dem zu konfigurierenden Orange-SIM-Gerät.
2. Wählen Sie das Gerät aus und blättern Sie abwärts zu *Erweiterungskonfiguration*.
3. Geben Sie die Erweiterungskonfiguration ein, indem Sie das folgende JSON-Format verwenden, und klicken Sie anschließend auf **Änderungen bestätigen**, um Ihre Konfiguration zu speichern.

```  
    {
        "orange": {
            "serialnumber": "<Seriennummer der Orange-SIM>"
        }
    }

```
Wenn die Organisation erfolgreich konfiguriert ist, wird der Abschnitt *Erweiterungen* unterhalb des Abschnitts zur Erweiterungskonfiguration in der Drilldown-Ansicht für Geräte angezeigt.

## Speicherung archivierter Daten
{: #historical_data}

Die Erweiterung für die Speicherung archivierter Daten ermöglicht Ihnen, kompatible Services für das Speichern von Nachrichten wie beispielsweise [{{site.data.keyword.cloudantfull}}](../../cloudant_connector.html) oder [{{site.data.keyword.messagehub_full}}](../../message_hub.html) für Ihre IoT-Daten zu lokalisieren und zu konfigurieren.

## Angepasste Gerätemanagementpakete
{: #device_mgmt}

Gerätemanagement ist eine zentrale Funktion von {{site.data.keyword.iot_short_notm}}; es kann jedoch erweitert werden, um zusätzliche Funktionen zu entwickeln.

Die Gerätemanagementerweiterung ermöglicht es Ihnen, angepasste Funktionen für das Gerätemanagement zu installieren. Weitere Informationen zu angepassten Gerätemanagementfunktionen finden Sie in [angepasste Erweiterungen für das Gerätemanagement](../../devices/device_mgmt/custom_actions.html){: new_window}.

## Blockchain
{: #blockchain}

{{site.data.keyword.iot_short_notm}} mit Blockchain ermöglicht es IoT-Geräten, Daten für Blockchain-Transaktionen zur Verfügung zu stellen, wodurch die Daten im nicht veränderbaren Blockchain-Konto gespeichert und in Geschäftsregeln für intelligente Verträge verwendet werden. {{site.data.keyword.iot_short_notm}} ordnet Gerätedaten dem Datenformat zu, das für intelligente Blockchain-Verträge erforderlich ist, und übergibt sie zur Speichern im Blockchain-Konto an ein Blockchain-Fabric.

### Unterstützte Operationen für Blockchain
- Auslösen von Aktualisierungen für intelligente Verträge durch Geräteereignisse.
- Ausführen von Geschäftslogik für intelligente Verträge, um den Kontostatus durch Ereignisdaten von Geräten zu aktualisieren.
- Überwachen von Blockchain, von Transaktionen und des Kontostatus mit der Benutzerschnittstelle für die Überwachung.

### Konfiguration für Blockchain

{{site.data.keyword.iot_short_notm}}-Blockchain-Integration ist ein Serviceangebot, das in {{site.data.keyword.iot_short_notm}} nicht standardmäßig aktiviert ist. Führen Sie folgende Schritte aus, um die Funktion in Ihrer Umgebung zu aktivieren:
 1. Wählen Sie im {{site.data.keyword.iot_short_notm}}-Dashboard die Option **Erweiterungen** aus.
 2. Klicken Sie neben der Blockchain-Erweiterung auf den Link **Weitere Informationen**, um auf die Seite mit den Serviceangeboten von IoT-Blockchain zu wechseln.
 3. Füllen Sie das Serviceanforderungsformular aus und übergeben Sie es.   
Die Genehmigung des Service dauert in der Regel ca. einen Tag. Nach der Genehmigung Ihrer Anforderung erhalten Sie eine E-Mail mit Anweisungen, wie die Blockchain-Integration in Ihrer {{site.data.keyword.iot_short_notm}}-Organisation aktiviert wird.
 5. Kehren Sie zu dem für Ihre Organisation gültigen {{site.data.keyword.iot_short_notm}}-Dashboard zurück, um das Setup zu beenden. Weitere Informationen finden Sie in [{{site.data.keyword.iot_short_notm}}-Blockchain-Integration](../../bl_blockchain_integration.html).

## The Weather Company
{: #weathercompany}

Die Erweiterung 'The Weather Company' kombiniert Ihre vorhandenen {{site.data.keyword.iot_short_notm}}-Geräte mit Wetterdaten. Wetterdaten von The Weather Company werden in der Ansicht 'Gerätedetails' angezeigt, wenn mithilfe der API die Anforderung 'Position aktualisieren' vorgenommen wurde oder wenn das Gerät seine Position bereits mithilfe einer Gerätemanagementnachricht festgelegt hat.

**Hinweis:** Nur verwaltete Geräte können ihre eigene Position festlegen. Für alle nicht verwalteten Geräte muss die Position manuell mithilfe der API festgelegt werden. Weitere Informationen zum Festlegen einer Geräteposition finden Sie in [Anforderung 'Position aktualisieren'](../../devices/device_mgmt/index.html#update-location).

### Wetterdaten

Zum Anzeigen der für eine Geräteposition abgerufenen Wetterdaten suchen Sie das Gerät im Teilfenster **Geräte** und klicken Sie auf das Gerät. Blättern Sie in der detaillierten Ansicht für Geräte zum Abschnitt **Erweiterungen**. Folgende Wetterdaten werden aufgelistet:

- Aktuelles Wetter.
- Aktuelle Temperatur.
- Vorhergesagte minimale und maximale Temperatur.
- Relative Feuchtigkeit.
- Druck.
- Sichtweite.
- Windgeschwindigkeit.
- Windrichtung.
- Breitengrad.
- Längengrad.

<!-- Weather data from The Weather Company extension can be retrieved by using the API. For information on the Weather Company API, see [The Weather Company API documentation](https://docs.internetofthings.ibmcloud.com/swagger/ext-twc.html). -->
