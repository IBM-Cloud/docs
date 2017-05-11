---

copyright:
  years: 2017
lastupdated: "2017-04-13"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# APIs verwalten
{: #manage_apis}

Wenn die API integriert wurde und somit vom API-Verwaltungssystem verwaltet und überwacht wird, können die API-Einstellungen angezeigt und geändert werden. Wenn die API noch nicht integriert wurde, müssen Sie die Integration mithilfe der im Abschnitt [APIs aus {{site.data.keyword.openwhisk_short}}-Aktionen erstellen](manage_openwhisk_apis.html) beschriebenen Prozedur vornehmen. 

Führen Sie die folgenden Schritte aus, um die Einstellungen für Ihre API zu verwalten:

Wenn Sie eine neue API erstellt haben und diese in der Schnittstelle bereits geöffnet ist, können Sie die ersten drei Schritte überspringen.

1. Wählen Sie die API aus, die Sie verwalten möchten, indem Sie im Dashboard für den {{site.data.keyword.openwhisk_short}}-Service eine Aktion auswählen, sofern die Informationen für die API noch nicht angezeigt werden.
2. Wählen Sie gegebenenfalls die Registerkarte **APIs** aus.
3. Wählen Sie gegebenenfalls die API aus, die verwaltet werden soll. Nachdem eine Verbindung hergestellt wurde, können die folgenden Optionen angezeigt und aktualisiert werden:
    * Zusammenfassung
    * Definition
    * Gemeinsame Nutzung
    * API-Explorer
4. Wählen Sie den Schieberegler für die Bereitstellung verwalteter APIs aus, um die API zu aktivieren und verfügbar zu machen. Hinweis: Einige Einstellungen können nicht festgelegt werden, wenn die API nicht bereitgestellt wurde.  

## Zusammenfassung der Einstellungen für APIs
{: #overview_api}

Die Registerkarte 'Zusammenfassung' ist bei Auswahl einer API standardmäßig ausgewählt und in zwei Abschnitte unterteilt:
* Eigenschaften - Im Abschnitt 'Eigenschaften' können die folgenden Informationen angezeigt werden:
    * Basisinformationen zur API
	* Sicherheitsrichtlinien
	* Informationen zur Ratenbegrenzung
    * Details zur gemeinsamen Nutzung
* Abschnitt für Analyse und Protokollierung - In diesem Abschnitt können die folgenden Statistiken angezeigt werden:
	* Anzahl der Antworten und durchschnittliche Antwortzeit im zuletzt angegebenen Zeitintervall
    * Anzahl der API-Aufrufe pro Minute im Grafikformat
    * Letzte 100 Antworten in der Tabelle 'Antwortprotokoll'
	
In der Grafik *Antworten* wird zusammenfassend dargestellt, wie viele Antworten die API empfangen hat. Ferner enthält sie eine Aufgliederung des Status der Antworten. Anhand dieser Daten Sie feststellen, ob vorwiegend Fehlerantworten empfangen werden. Eine Überzahl an Fehlerantworten kann darauf hinweisen, dass der Datenverkehr die festgelegte Begrenzung in den Rateneinstellungen übersteigt. Wenn Sie den Mauszeiger auf das Informationssymbol setzen, wird eine numerische Aufgliederung der Antworten nach Antwortcode angezeigt. Häufig vorkommende Antwortcodes:
* 200  OK
* 201  Erstellt
* 302  Gefunden
* 304  Nicht geändert
* 400  Fehlerhafte Anforderung
* 401  Nicht autorisiert
* 403  Unzulässig
* 500  Interner Serverfehler
* 503  Service nicht verfügbar

Die Tabelle 'Antwortprotokoll' enthält Details zu den letzten 100 Antworten. Wählen Sie eine Spaltenüberschrift aus, um die Informationen gemäß den Einträgen in der Spalte zu sortieren. Mithilfe von *Suchantworten* können Sie nach bestimmten Einträgen in der Tabelle 'Antwortprotokoll' suchen. Weitere Informationen zu einem Ereignis können Sie aufrufen, indem Sie das betreffende Ereignis oder **Details anzeigen** im Auswahlmenü (drei vertikale Punkte) neben dem Eintrag auswählen.


## API-Einstellungen bearbeiten
{: #settings_api}

Auf der Registerkarte **Definition** können Sie die Basisinformationen für die API aktualisieren. Dazu gehören Dokumentation, Name und Basis-URL. Im Abschnitt für Sicherheit und Ratenbegrenzung können Sie eine Aufruf- und Intervallbegrenzung festlegen, um sicherzustellen, dass nur eine bestimmte Anzahl Aufrufe pro Sekunde, Minute oder Stunde erfolgt. Ferner können Sie angeben, dass zur Erstellung von API-Aufrufen eine Authentifizierung erfolgen muss, um eine unerwünschte Verwendung Ihrer Daten zu verhindern oder Statistiken für die API zu erfassen.

Führen Sie die folgenden Schritte aus, um die Einstellungen für eine API zu ändern:

1. Klicken Sie im Dashboard für die API-Verwaltung auf die Registerkarte **Definition**.
2. Im Abschnitt für die API-Informationen können Sie der API einen Namen geben bzw. den Namen aktualisieren und eine API-Definition importieren.
3. Im Abschnitt für Sicherheit und Ratenbegrenzung können Sie die folgenden Richtlinien aktualisieren:
    * API-Schlüssel erforderlich - Gibt an, ob der API-Aufruf nur bei Angabe des richtigen API-Schlüssels verarbeitet werden kann. Bei der Standardeinstellung ist kein zusätzlicher Schlüssel erforderlich.
    * Sicherheitsmethode - Bei Auswahl der Option für den API-Schlüssel gibt diese Richtlinie an, ob für die Verarbeitung der API nur der API-Schlüssel oder der API-Schlüssel und der geheime Schlüssel erforderlich sind.
    * Position des API-Schlüssels und geheimen Schlüssels - Gibt je nach Einstellung für die Methode an, wie die API-Sicherheitsinformationen in den Aufruf einbezogen werden. Die Aufrufnamen geben an, wie die Sicherheitsinformationen identifiziert werden.
    * API-Aufrufrate begrenzen - Legt die Anzahl der API-Aufrufe fest, die in einem bestimmten Zeitintervall zulässig sind. Diese Einstellung kann pro Schlüssel festgelegt werden. Beachten Sie, dass bei der Ratenbegrenzung eine Blockmethode verwendet wird. Die Durchschnittsrate der API-Aufrufe wird für das gesamte in der Rate angegebene Zeitintervall berechnet. Wenn die Rate der API-Aufrufe in einem Intervall die Durchschnittsrate der API-Aufrufe übersteigt, können Aufrufe eine Zeit lang verweigert werden, und zwar bis zu dem in der Rate angegebene Zeitlimit.   
    * OAuth-Provider - Stellt sicher, dass Benutzer mit den richtigen Sicherheitsparametern auf die APIs zugreifen können. Dazu wird OAuth über Anmeldeberechtigungsnachweise von Providern wie Google, Facebook, IBM und GitHub angewendet.
4. CORS aktivieren - Mit CORS (Cross-origin requests) können bestimmte Anforderungen aus einer anderen Domäne verarbeitet werden.
5. Klicken Sie auf **Speichern**.

## APIs gemeinsam nutzen
{: #share_api}

APIs können innerhalb und außerhalb der {{site.data.keyword.Bluemix_notm}}-Organisation mit anderen Benutzern gemeinsam genutzt werden.

Im Falle der gemeinsamen Nutzung von APIs, entweder innerhalb oder außerhalb der {{site.data.keyword.Bluemix_notm}}-Organisation, können für die APIs Schlüssel erstellt werden. Jede verwaltete API unterstützt 5 Schlüssel, die erstellt und dieser API zugeordnet werden können. Durch Senden eines eindeutigen Schlüssels an eine Einzelperson oder ein Unternehmen können Statistiken zur Nutzung dieser API erfasst werden. Beispielsweise ist es möglich, die Anzahl der API-Aufrufe der Person oder des Unternehmens zu erfassen.

Ferner können Schlüssel inaktiviert oder die Aufrufe eines Schlüssels begrenzt werden. Die kann bei der Durchführung von Tests, beim Lastausgleich, der gewinnbringenden Nutzung oder der Behebung von Sicherheitsproblemen hilfreich sein.  

1. Klicken Sie im Dashboard für die API-Verwaltung auf die Registerkarte für die **gemeinsame Nutzung**.
2. Wählen Sie im Bereich für die gemeinsame Nutzung innerhalb der {{site.data.keyword.Bluemix_notm}}-Organisation die Option **API mit allen Benutzern in der Bluemix-Organisation gemeinsam nutzen** aus, wenn die API anderen Benutzern mit Zugriff auf die {{site.data.keyword.Bluemix_notm}}-Organisation zur Verfügung gestellt werden soll. Diese Option muss ausgewählt werden, um einen Schlüssel zu generieren.
3. Klicken Sie auf **API-Schlüssel erstellen**, um einen eindeutigen Schlüssel für die API zu erstellen. Daraufhin wird das Dialogfenster 'API-Schlüssel erstellen' angezeigt. Der API-Schlüssel wird automatisch generiert.
4. Mit dem API-Schlüssel kann festgestellt werden, welcher Benutzer auf die API zugreift. Zu diesem Zweck wird ein eindeutiger Schlüssel an den Benutzer gesendet. Das Gateway kann feststellen, welcher Schlüssel (und Kunde) den Aufruf generiert.
5. Klicken Sie auf das **Menüsymbol** (drei vertikale Punkte) neben einem API-Schlüssel, um diesen Schlüssel zu bearbeiten oder zu löschen.

Im Abschnitt für die gemeinsame Nutzung außerhalb der {{site.data.keyword.Bluemix_notm}}-Organisation können Sie die API mit anderen Benutzern gemeinsam nutzen, die über kein {{site.data.keyword.Bluemix_notm}}-Konto verfügen. Bei dieser Methode wird ein direkter Link zum Anzeigen der Informationen zu dieser API im API-Explorer bereitgestellt. Die API enthält eine Schaltfläche zur Ausführung der API in der API-Exploreransicht. Führen Sie die folgenden Schritte aus, um einen Link für die API anzufordern:

1. Im Abschnitt für die gemeinsame Nutzung außerhalb der {{site.data.keyword.Bluemix_notm}}-Organisation: Klicken Sie auf **API-Schlüssel erstellen**. Daraufhin wird das Dialogfenster 'API-Schlüssel erstellen' angezeigt. Beachten Sie, dass der Benutzer über einen geheimen Schlüssel verfügt, der nicht Ihrer Kontrolle unterliegt.
2. Geben Sie einen eindeutigen Namen für den API-Schlüssel an.
3. Wählen Sie **Schlüssel erstellen** aus. 
4. Senden Sie den API-Portallink an den Kunden ohne {{site.data.keyword.Bluemix_notm}}-Konto. Der API-Schlüssel und gegebenenfalls der geheime Schlüssel sind in diesem Link enthalten. Somit kann weiterhin festgestellt werden, welcher Schlüssel den Link generiert hat.
  
Der Link für die API-Dokumentation öffnet die API auf der Registerkarte **API-Explorer**.

## Mit API-Explorer anzeigen und testen
{: #explore_api}

Wählen Sie die Registerkarte 'API-Explorer' aus, um generierte HTML aus dem Swagger-Dokument anzuzeigen. 

Der API-Explorer zeigt alle API-Aktionen sowie die Dokumentation an, die sich auf die API beziehen. Sie können die Operationen und Aktionen mit den zugehörigen Beschreibungen anzeigen und die API in der Benutzerschnittstelle testen. Ferner können Sie das Swagger-Dokument zur Wiederverwendung des Inhalts herunterladen.

Führen Sie die folgenden Schritte aus, um die API zu testen:
1. *Beispiele* ist standardmäßig ausgewählt. Es handelt sich hier um ein Codebeispiel für die ausgewählte API.
2. Ändern Sie gegebenenfalls das Beispielformat, indem Sie im Menü neben der angegebenen Sprache eine Sprache auswählen. 
3. Wählen Sie **Ausprobieren** aus.
4. Wählen Sie **Operation aufrufen** aus. 

Die Antwort auf die Anforderung wird angezeigt.   
