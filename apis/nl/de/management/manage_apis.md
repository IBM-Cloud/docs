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

Wenn Sie Ihre API integriert haben, sodass sie vom API-Managementsystem verwaltet und überwacht wird, können Sie die API-Einstellungen anzeigen und ändern. Wenn Sie Ihre API nicht integriert haben, müssen Sie eine API durch die unter [APIs aus {{site.data.keyword.openwhisk_short}}-Aktionen erstellen](manage_openwhisk_apis.html) beschriebene Vorgehensweise integrieren.  

Führen Sie die folgenden Schritte aus, um die Einstellungen für Ihre API zu verwalten: 

Wenn Sie eine neue API erstellt haben und diese bereits in der Schnittstelle geöffnet ist, können Sie die ersten drei Schritte überspringen. 

1. Wählen Sie die API aus, die Sie verwalten wollen, indem Sie eine Aktion im Dashboard für den {{site.data.keyword.openwhisk_short}}-Service auswählen, wenn die Informationen für Ihre API noch nicht angezeigt werden. 
2. Wählen Sie die Registerkarte **APIs** aus, sofern erforderlich. 
3. Wählen Sie die API aus, die Sie verwalten wollen, sofern erforderlich. Wenn eine Verbindung hergestellt ist, sind die folgenden Optionen verfügbar, die Sie anzeigen und aktualisieren können: 
    * Zusammenfassung
    * Definition
    * Gemeinsame Nutzung
    * API-Explorer
4. Wählen Sie das Auswahlfeld 'Verwaltete API zugänglich machen' aus, um es zu aktivieren und Ihre API zugänglich zu machen. Hinweis: Einige Einstellungen können nicht festgelegt werden, wenn die API nicht zugänglich gemacht ist.   

## Zusammenfassung der Einstellungen für APIs
{: #overview_api}

Die Registerkarte 'Zusammenfassung' wird standardmäßig ausgewählt, wenn Sie eine API auswählen. Sie ist in zwei Abschnitte untergliedert: 
* Eigenschaften - Im Abschnitt 'Eigenschaften' können Sie die folgenden Informationen anzeigen: 
    * Basisinformationen zu Ihrer API
	* Sicherheitsrichtlinien
	* Informationen zur Ratenbegrenzung
    * Details zur gemeinsamen Nutzung
* Abschnitt für Analyse und Protokollierung - In diesem Abschnitt können Sie die folgenden Statistiken anzeigen: 
	* Anzahl der Antworten und durchschnittliche Antwortzeit während des letzten angegebenen Zeitintervalls
    * Anzahl API-Aufrufe pro Minute im Grafikformat
    * Letzte 100 Antworten in der Antwortprotokolltabelle
	
Das Diagramm *Antworten* zeigt eine schnelle Darstellung der Anzahl Antworten, die von Ihrer API empfangen wurden, und die Aufgliederung des Status der Antworten an. Dies kann Ihnen dabei helfen, zu ermitteln, ob Sie mehrheitlich Fehlerantworten empfangen. Eine Mehrheit von Fehlerantworten kann darauf hinweisen, dass bei Ihnen mehr Datenverkehr stattfindet, als Sie in den Rateneinstellungen zugelassen haben. Die können die numerische Aufgliederung der Antworten nach Antwortcode anzeigen, indem Sie den Mauscursor über das Informationssymbol bewegen. Die folgenden Antwortcodes kommen häufiger vor: 
* 200  OK
* 201 Created (Erstellt)
* 302  Found (Gefunden)
* 304  Not Modified (Nicht geändert)
* 400  Bad Request (Fehlerhafte Anforderung)
* 401  Unauthorized (Keine Berechtigung)t
* 403  Forbidden (Unzulässig)
* 500  Internal Server Error (Interner Serverfehler)
* 503  Service Unavailable (Service nicht verfügbar)

Die Antwortprotokolltabelle enthält einzelne Details zu den letzten 100 Antworten. Sie können die Informationen nach den Einträgen in einer Spalte sortieren, indem Sie die Spaltenüberschrift auswählen. Über die Leiste *Antworten durchsuchen* können Sie nach bestimmten Einträgen in der Antwortprotokolltabelle suchen. Weitere Informationen zu einem Ereignis werden angezeigt, wenn Sie es auswählen oder wenn Sie die Option **Details anzeigen** in der Liste des Optionsmenüs (drei vertikale Punkte) neben dem Eintrag auswählen. 


## API-Einstellungen bearbeiten
{: #settings_api}

Auf der Registerkarte **Definition** können Sie Basisinformationen zu Ihrer API aktualisieren. Die Informationen umfassen die Dokumentation, den Namen und die Basis-URL. Im Abschnitt für Sicherheit und Ratenbegrenzung geben Sie eine Aufruf- und Intervallbegrenzung an, um sicherzustellen, dass nur eine bestimmte Anzahl an Aufrufen pro Sekunde, Minute oder Stunde ausgeführt werden kann. Sie können außerdem eine Authentifizierung für das Erstellen von API-Aufrufen erforderlich machen, um eine unerwünschte Verwendung Ihrer Daten zu verhindern oder Statistiken zu der API zu erfassen. 

Führen Sie die folgenden Schritte aus, um die Einstellungen für eine API zu ändern: 

1. Klicken Sie im API-Management-Dashboard auf die Registerkarte **Definition**. 
2. Sie können Ihre API benennen oder den Namen der API aktualisieren und eine API-Definition in den API-Informationsabschnitt importieren. 
3. Im Abschnitt für Sicherheit und Ratenbegrenzung können Sie die folgenden Richtlinien aktualisieren: 
    * API-Schlüssel erforderlich - Gibt an, ob der API-Aufruf nur verarbeitet werden kann, wenn der richtige API-Schlüssel angegeben wird. Bei der Standardeinstellung ist kein zusätzlicher Schlüssel erforderlich. 
    * Sicherheitsmethode - Wenn die API-Schlüsseloption ausgewählt ist, gibt diese Option an, ob für die Verarbeitung der API nur der API-Schlüssel oder sowohl der API-Schlüssel als auch der geheime Schlüssel für die API erforderlich sind. 
    * Position des API-Schlüssels und des geheimen API-Schlüssels - Abhängig von Ihrer Einstellung für die Methode gibt diese Option an, wie Ihre API-Informationen in den Aufruf eingeschlossen werden. Die Aufrufnamen geben an, wie die Sicherheitsinformationen ermittelt werden. 
    * API-Aufrufrate begrenzen - Legt die Anzahl API-Aufrufe fest, die während eines angegebenen Zeitintervalls zulässig sind. Dazu ist auch die Option verfügbar, dies für jeden einzelnen Schlüssel anzugeben. Beachten Sie, dass eine Bursting-Methode zur Ratenbegrenzung verwendet wird. Die durchschnittliche Rate der API-Aufrufe wird über das gesamte Zeitintervall berechnet, das Sie in der Rate angegeben haben. Wenn die Rate von API-Aufrufen während eines Intervalls die durchschnittliche Rate der API-Aufrufe überschreitet, können Aufrufe eine Zeit lang bis zu der Zeitbegrenzung, die Sie in der Rate angegeben haben, verweigert werden.    
    * OAuth-Provider - Stellen Sie sicher, dass Benutzer mit den richtigen Sicherheitsparametern auf Ihre APIs zugreifen können, indem Sie OAuth mithilfe von Anmeldeberechtigungsnachweisen von Social Service-Anbietern wie Google, Facebook, IBM und GitHub umsetzen. 
4. CORS aktivieren - Cross-Origin Requests (CORS) ermöglichen einige eingeschränkte Anforderungen aus einer anderen Domäne. 
5. Klicken Sie auf **Speichern**. 

## APIs gemeinsam nutzen
{: #share_api}

Sie können APIs mit anderen Benutzern innerhalb oder außerhalb Ihrer {{site.data.keyword.Bluemix_notm}}-Organisation gemeinsam nutzen. 

Wenn Sie Ihre APIs mit anderen Personen innerhalb oder außerhalb Ihrer {{site.data.keyword.Bluemix_notm}}-Organisation gemeinsam nutzen, können Sie Schlüssel für Ihre APIs erstellen. Jede verwaltete API unterstützt fünf Schlüssel, die erstellt und der API zugewiesen werden können. Durch das Senden eines eindeutigen Schlüssels an eine Einzelperson oder ein Unternehmen können Sie eine Reihe von Statistiken zur Verwendung der API verfolgen. Sie können zum Beispiel die Anzahl der Aufrufe Ihrer API durch die betreffende Person oder das betreffende Unternehmen verfolgen. 

Sie können darüber hinaus die Anzahl Aufrufe auf Schlüsselebene begrenzen, einen Schlüssel inaktivieren oder die Aufrufe durch einen Schlüssel begrenzen. Dies kann beim Testen, beim Lastausgleich, bei der Gebührenerhebung oder bei der Lösung verschiedener Sicherheitssituationen hilfreich sein.   

1. Klicken Sie im API-Management-Dashboard auf die Registerkarte **Gemeinsame Nutzung**. 
2. Wählen Sie im Bereich "Innerhalb der {{site.data.keyword.Bluemix_notm}}-Organisation gemeinsam nutzen" die Option **API mit allen anderen Benutzern in eigener Bluemix-Organisation gemeinsam nutzen** aus, wenn Ihre API für andere Benutzer mit Zugriff auf Ihre {{site.data.keyword.Bluemix_notm}}-Organisation verfügbar sein soll. Diese Option muss ausgewählt werden, um einen Schlüssel zu generieren. 
3. Klicken Sie auf **API-Schlüssel erstellen**, um einen eindeutigen Schlüssel für Ihre API zu erstellen. Das Dialogfenster 'API-Schlüssel erstellen' wird angezeigt. Der API-Schlüssel wird automatisch generiert. 
4. Bestimmen Sie mithilfe des API-Schlüssels, welcher Benutzer auf die API zugreift, indem Sie einem Benutzer einen eindeutigen Schlüssel senden. Das Gateway kann feststellen, welcher Schlüssel (und Kunde) den Aufruf generiert. 
5. Klicken Sie auf das Symbol **Menü** (drei vertikale Punkte) neben dem Schlüssel, um den API-Schlüssel zu bearbeiten oder zu löschen. 

Im Abschnitt 'Außerhalb der {{site.data.keyword.Bluemix_notm}}-Organisation gemeinsam nutzen' können Sie Ihre API Benutzern zur gemeinsamen Nutzung zur Verfügung stellen, die kein {{site.data.keyword.Bluemix_notm}}-Konto haben. Diese Methode der gemeinsamen Nutzung stellt einen direkten Link zum Anzeigen der Informationen zu der API im API-Explorer bereit. Die API enthält eine Schaltfläche zum Ausführen der API in der API-Exploreransicht. Führen Sie die folgenden Schritte aus, um einen Link für Ihre API anzufordern: 

1. Klicken Sie im Abschnitt 'Außerhalb der {{site.data.keyword.Bluemix_notm}}-Organisation gemeinsam nutzen' auf **API-Schlüssel erstellen**. Das Dialogfenster 'API-Schlüssel erstellen' wird angezeigt. Beachten Sie, dass der Benutzer einen geheimen Schlüssel hat, den Sie nicht kontrollieren können. 
2. Geben Sie einen eindeutigen Namen für den API-Schlüssel an. 
3. Wählen Sie **Schlüssel erstellen** aus.  
4. Senden Sie den API-Portallink an den Kunden ohne {{site.data.keyword.Bluemix_notm}}-Konto. Der API-Schlüssel und der geheime Schlüssel (falls verwendet) werden in den Link eingeschlossen, sodass Sie noch feststellen können, welcher Schlüssel den Link generiert hat. 
  
Der API-Dokumentationslink öffnet die API auf der Registerkarte **API-Explorer**. 

## Mit dem API-Explorer anzeigen und testen
{: #explore_api}

Wählen Sie die Registerkarte für den API-Explorer aus, um den generierten HTML-Code aus Ihrem Swagger-Dokument anzuzeigen.  

Der API-Explorer zeigt alle API-Aktionen und die Dokumentation an, die zu der API gehören. Über die Benutzerschnittstelle können Sie die Operationen und Aktionen sowie ihre Beschreibungen anzeigen und die API testen. Sie können außerdem das Swagger-Dokument herunterladen, um den Inhalt wiederzuverwenden. 

Führen Sie die folgenden Schritte aus, um die API zu testen: 
1. *Beispiele* ist standardmäßig ausgewählt. Hier wird ein Beispiel für den Code für die ausgewählte API angezeigt. 
2. Ändern Sie das Beispielformat, wenn erforderlich, indem Sie eine Sprache im Menü neben der angegebenen Sprache auswählen.  
3. Wählen Sie **Versuchen** aus. 
4. Wählen Sie **Operation aufrufen** aus.  

Die Antwort auf die Anforderung wird angezeigt.    
