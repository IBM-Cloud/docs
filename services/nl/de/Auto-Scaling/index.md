{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.autoscaling}}-Service - Einführung
{: #autoscaling}

*Letzte Aktualisierung: 18. Januar 2015*

In {{site.data.keyword.Bluemix_notm}} kann die Anwendungskapazität automatisch verwaltet werden. Mithilfe des {{site.data.keyword.autoscalingfull}}-Service kann die Verarbeitungsleistung der Anwendung automatisch erhöht oder reduziert werden.
Die Anzahl der Anwendungsinstanzen wird auf der Basis der von Ihnen definierten {{site.data.keyword.autoscaling}}-Richtlinie dynamisch angepasst.
{:shortdesc} 

## Verwendung des {{site.data.keyword.autoscaling}}-Service in {{site.data.keyword.Bluemix_notm}}
{: #as-service}

Um den {{site.data.keyword.autoscaling}}-Service verwenden zu können, müssen Sie die folgenden Schritte ausführen: 

1. Klicken Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard auf die Option *Service oder API hinzufügen* und wählen Sie anschließend im Abschnitt 'DevOps ' des Servicekatalogs den {{site.data.keyword.autoscaling}}-Service aus. Es wird ein neues Fenster für eine Übersicht des {{site.data.keyword.autoscaling}}-Service angezeigt. 
2. Wählen Sie die Anwendung aus, an die Sie den {{site.data.keyword.autoscaling}}-Service binden möchten, und klicken Sie auf *Erstellen*. <br/>
*Hinweis:* Sie können nur einen {{site.data.keyword.autoscaling}}-Service an eine Anwendung binden. Wählen Sie die Anwendung in diesem Schritt nicht aus, wenn sie bereits mit einem anderen {{site.data.keyword.autoscaling}}-Service verbunden ist. Andernfalls wird der Fehler CWSCV2004E ausgegeben.<br/>Das Fenster 'Erneutes Staging für Anwendung' wird angezeigt.
3. Klicken Sie im Fenster 'Erneutes Staging für Anwendung' auf *Erneutes Staging*, um für Ihre Anwendung ein erneutes Staging durchzuführen, bevor Sie den neuen {{site.data.keyword.autoscaling}}-Service verwenden, den Sie soeben hinzugefügt haben. Nach dem erneuten Staging der Anwendung können Sie mit der Konfiguration des {{site.data.keyword.autoscaling}}-Service für Ihre Anwendung beginnen. 
4. Für die Konfiguration von {{site.data.keyword.autoscaling}} für eine Anwendung müssen Sie in der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle auf Ihre Anwendung klicken, an die der {{site.data.keyword.autoscaling}}-Service gebunden ist. 
5. Klicken Sie im Serviceabschnitt des Dashboards auf das Symbol für *Auto-Scaling*.

6. Falls Sie die {{site.data.keyword.autoscaling}}-Richtlinie für die Anwendung noch nicht definiert haben, definieren Sie sie durch Klicken auf die Option *Richtlinie für {{site.data.keyword.autoscaling}} erstellen*.

Nun können Sie die {{site.data.keyword.autoscaling}}-Richtlinie konfigurieren, die Metrikstatistiken anzeigen oder den Skalierungsverlauf für die Anwendung anzeigen. 
<dl>
<dt>Richtlinienkonfiguration</dt>
<dd>Dieser Abschnitt enthält Informationen zur Erstellung oder Bearbeitung der Skalierungsregeln für die Angabe der Bedingungen, unter denen bestimmte Skalierungsaktivitäten ausgelöst werden sollen.<ul>
<li> Bei Liberty for Java™-Anwendungen können Sie Skalierungsregeln für JVM-Heapspeicher, Hauptspeicher und Durchsatz definieren.
<li> Bei Node.js-Anwendungen können Sie Skalierungsregeln für den Hauptspeicher definieren.
<li> Bei Ruby-Anwendungen können Sie Skalierungsregeln für den Hauptspeicher definieren. </ul>
*Hinweis:* Sie können mehrere Skalierungsregeln für mehr als einen Metriktyp definieren. Der {{site.data.keyword.autoscaling}}-Service ermittelt jedoch keine Konflikte zwischen den Skalierungsrichtlinien. Wenn Sie die Skalierungsrichtlinie definieren, müssen Sie sicherstellen, dass die verschiedenen Skalierungsrichtlinien nicht miteinander in Konflikt geraten. Andernfalls schwankt die Gesamtzahl der Instanzen möglicherweise, da für die Anwendung in rascher Folge Scale-in- und Scale-out-Aktionen durchgeführt werden.<br/><br/>
Wenn die Workload Ihrer Anwendung sich zur Spitzenzeit und zur Zeit ohne Nutzung drastisch verändert, können Sie einen Skalierungszeitplan erstellen, um die unterschiedlichen Skalierungsanforderungen für unterschiedliche Zeiträume abzuwickeln. Verwenden Sie für die Definition der Referenzversion der Anzahl der Anwendungsinstanzen den in einem Zeitplan angegebenen Parameter 'Anzahl der Instanzen - Minimum'; gleichzeitig gelten die dynamischen Skalierungsregeln für den Zeitplan zur Auslösung der Scale-in- und Scale-out-Aktionen weiterhin. </dd>
<dt>Statistiken zu Metriken</dt>
<dd>Es werden für die Instanzen Ihrer Anwendung die Statistiken zu den Metriken angezeigt.
Sie können die Durchschnittsstatistik sehen und eine bestimmte Instanz auswählen,
um deren Statistikdaten anzuzeigen. </dd>
<dt>Skalierungsverlauf</dt>
<dd>Es wird der Skalierungsverlauf für Ihre Anwendungen angezeigt. <ul>
<li> Vergangene Woche:
Es wird der Skalierungsverlauf für die vergangene Woche angezeigt. <li> Vergangener Monat:
Es wird der Skalierungsverlauf für den vergangenen Monat angezeigt. <li> Benutzerdefinierter Bereich:
Sie können einen Zeitraum festlegen. </ul>
*Hinweis:* Durch die Auswahl von Skalierungsstatus bzw. der Option zum Skalieren (Anzahl reduzieren/erhöhen) können Sie den Protokollsatz filtern.</dd>
</dl>


## Richtlinienfelder für den {{site.data.keyword.autoscaling}}-Service
{: #policyfields}

| Feldname  | Beschreibung |
|-------------|----------------------|
|*Zulässige maximale Instanzanzahl* |	Die maximale Anzahl an Anwendungsinstanzen, die
gestartet werden können. Wenn die momentane Anzahl der Anwendungsinstanzen diesem Wert entspricht,
führt der {{site.data.keyword.autoscaling}}-Service keine weiteren Scale-out-Aktionen für die Anwendung durch.
Standardmäßige minimale Instanzanzahl - Die minimale Anzahl an Anwendungsinstanzen, die gestartet werden können. Wenn die Anzahl der Instanzen diesem Wert entspricht,
führt der {{site.data.keyword.autoscaling}}-Service keine weiteren Scale-in-Aktionen für die Anwendung durch.
 |
| *Metriktyp*	| 	Die unterstützten Metriktypen, die überwacht werden
können. Weitere Informationen finden Sie in Tabelle 2. |
| *Skalieren (Anzahl erhöhen)* | 	Gibt
den Schwellenwert an, durch den eine Scale-out-Aktion ausgelöst wird, und gibt
an, wie viele Instanzen hinzukommen, wenn die Scale-out-Aktion ausgelöst wird.  |
| *Skalieren (Anzahl reduzieren)* |	Gibt
einen Schwellenwert an, durch den eine Scale-in-Aktion ausgelöst wird, und gibt
an, wie viele Instanzen reduziert werden, wenn die Scale-in-Aktion ausgelöst wird.  |
| *Statistikfenster* |	Die Länge des vergangenen Zeitraums, in dem empfangene Metrikwerte
als gültig erkannt wurden. Metrikwerte sind nur gültig, wenn
die Zeitmarken in diesem Zeitraum liegen. Die Einheit für den Parameter 'Statistikfenster' ist Sekunden. |
| *Überschreitungsdauer*	| Die Länge des vergangenen Zeitraums, in dem möglicherweise eine
Skalierungsaktion ausgelöst wird. Eine Skalierungsaktion wird ausgelöst, sobald
gesammelte Metrikwerte entweder über dem oberen Schwellenwert oder unter dem
unteren Schwellenwert liegen, und zwar länger als angegeben. Die Einheit für den Parameter 'Überschreitungsdauer' ist Sekunden. |
| *Cooldown-Zeitraum für Herunterskalierung* | Nach dem Auftreten einer Scale-in-Aktion werden während der Länge des durch die Option 'Cooldown-Zeitraum für Herunterskalierung' angegebenen Zeitraums weitere Skalierungsanforderungen ignoriert. Die Einheit für diesen Parameter ist Sekunden.
 |
| *Cooldown-Zeitraum für Hochskalierung*	| Nach dem Auftreten einer Scale-out-Aktion werden während der Länge des durch die Option 'Cooldown-Zeitraum für Hochskalierung' angegebenen Zeitraums weitere Skalierungsanforderungen ignoriert. Die Einheit für diesen Parameter ist Sekunden.
 |
| *Zeitzone*	| Die Zeitzone, in der der Zeitplan gültig ist.  |
| *Startzeit*  |	Die Startzeit eines sich wiederholenden Zeitplans.  |
| *Endzeit*    |	Die Endzeit eines sich wiederholenden Zeitplans. 	|
| *Wiederholungszeitpunkt*	|	Der Tag der Woche, für den ein sich wiederholender Zeitplan gültig ist.  |
| *Anzahl der Instanzen - Minimum* |	Die minimale Anzahl an Instanzen, die für die Anwendung während des im Zeitplan angegebenen Zeitraums
gestartet werden können.  |
| *Startdatum & -zeit* |	Startdatum und -zeit des Zeitplans, der für ein bestimmtes Datum eingerichtet ist.  |
| *Enddatum & und -zeit* |	Enddatum und -zeit des Zeitplans, der für ein bestimmtes Datum eingerichtet
ist. 	|

Tabelle 1. Richtlinienfelder in der Skalierungsrichtlinie

| Metrikname | Beschreibung | Unterstützter Anwendungstyp
 |
|-------------|----------------------| ------------------- |
| *JVM-Heapspeicher* |	Prozentsatz der JVM-Heapspeicherbelegung.
	| Liberty for Java |
| *Hauptspeicher*   |	Prozentsatz der Hauptspeicherbelegung.
	|  Liberty for Java<br/> Node.js <br/> Ruby <br/> |
| *Durchsatz* | Anzahl der verarbeiteten Anforderungen pro Sekunde.
| Liberty for Java |
| *Antwortzeit* |	Die Antwortzeit
für die verarbeiteten Anforderungen. 	| Liberty for Java |

Tabelle 2. Unterstützte Metriknamen

## Fehlernachrichten
{: #errmsgs}
In diesem Abschnitt werden die Warnungen und Fehlernachrichten aufgeführt, die vom
{{site.data.keyword.autoscaling}}-Service generiert werden. 
 
### CWSCV2004E Es ist bereits ein anderer
{{site.data.keyword.autoscaling}}-Service an die Anwendung gebunden.
**Sie können nur einen {{site.data.keyword.autoscaling}}-Service an eine Anwendung binden. Dieser Fehler tritt auf, wenn Sie den {{site.data.keyword.autoscaling}}-Service an eine Anwendung binden möchten, die bereits an einen anderen {{site.data.keyword.autoscaling}}-Service gebunden ist.**

Wählen Sie eine andere Anwendung aus, an die kein weiterer {{site.data.keyword.autoscaling}}-Service gebunden ist, und binden Sie den {{site.data.keyword.autoscaling}}-Zielservice an diese Anwendung. Wenn dieser Fehler auch in allen anderen Fällen auftritt, wenden Sie sich an den IBM Support. 

### CWSCV6001E Der API-Server kann die JSON-Eingabezeichenfolgen für die folgende API nicht parsen: {0}.
**Das Problem tritt beim Parsen von JSON-Eingabezeichenfolgen auf. **

Prüfen Sie die JSON-Eingabe im API-Dokument und beheben Sie darin den Fehler. 

### CWSCV6002E Der API-Server kann die JSON-Ausgabezeichenfolgen für die folgende API nicht parsen: {0}.
**Das Problem tritt beim Parsen von JSON-Ausgabezeichenfolgen auf.**

Wenden Sie sich für weitere Informationen an den Cloudadministrator. 

### CWSCV6003E Formatfehler {0} für JSON-Eingabezeichenfolgen in JSON-Eingabe für folgende API: {1}.
**Beim Parsen von JSON-Eingabezeichenfolgen wurde ein Formatfehler entdeckt. **

Prüfen Sie die JSON-Eingabe im API-Dokument und beheben Sie darin den Fehler. 

### CWSCV6004E Formatfehler {0} für JSON-Ausgabezeichenfolgen für folgende API: {1}.
**Beim Parsen von JSON-Ausgabezeichenfolgen wurde ein Formatfehler entdeckt. **

Wenden Sie sich für weitere Informationen an den Cloudadministrator. 

### CWSCV6005E Interner Serverfehler während {0}.
**Beim Verarbeiten der Anforderung tritt ein interner Serverfehler auf. **

Wenden Sie sich für weitere Informationen an den Cloudadministrator. 

### CWSCV6006E Aufrufen von CloudFoundry-APIs schlug fehl: {0}
**Beim Aufrufen von CloudFoundry-APIs ist ein Fehler aufgetreten.**

Wenden Sie sich für weitere Informationen an den Cloudadministrator. 

### CWSCV6007E Die folgende Anwendung wurde nicht gefunden: {0}
**Die Anwendung wurde nicht gefunden.**

Prüfen Sie die Anwendungsinformationen, um weitere Informationen zu erhalten.

### CWSCV6008E Beim Abrufen von Informationen für Anwendung {0} ist folgender Fehler aufgetreten: {1}
**Das Abrufen von Anwendungsinformationen ist mit Fehlern fehlgeschlagen. **

Prüfen Sie die Anwendungsinformationen, um weitere Informationen zu erhalten.

### CWSCV6009E Service {0} für App {1} wurde nicht gefunden.
**Der Service für diese Anwendung konnte nicht gefunden werden. **

Prüfen Sie die Servicebindung für diese Anwendung, um weitere Informationen zu erhalten. 

### CWSCV6010E Richtlinie für App {0} wurde nicht gefunden
**Die Richtlinie für diese Anwendung konnte nicht gefunden werden.**

Prüfen Sie die Anwendungskonfiguration, um weitere Informationen zu erhalten. 

### CWSCV6011E Interne Authentifizierung fehlgeschlagen während {0}
**Die interne Authentifizierung ist fehlgeschlagen. **

Wenden Sie sich für weitere Informationen an den Cloudadministrator. 


# rellinks
## Beispiele
* [Lernprogramm: Machen Sie Ihre Anwendung in {{site.data.keyword.Bluemix_notm}}](http://www.ibm.com/developerworks/cloud/library/cl-autoscale-app/index.html){:new_window} elastisch
* [Cloud Foundry Architecture Labs](https://developer.ibm.com/bluemix/docs/category/cloud-foundry-docs/){:new_window}

## sdk
* [Rest-API von IBM {{site.data.keyword.autoscaling}} for {{site.data.keyword.Bluemix_notm}}](https://www.{DomainName}/docs/api/content/api/auto-scaling/index.html){:new_window}

## Allgemein
* [{{site.data.keyword.Bluemix_notm}} - Preisliste](https://console.{DomainName}/pricing/){:new_window}
* [{{site.data.keyword.Bluemix_notm}} - Voraussetzungen](https://developer.ibm.com/bluemix/support/#prereqs){:new_window}
* [{{site.data.keyword.autoscaling}}-CLI](../../cli/plugins/auto-scaling/index.html){:new_window}

