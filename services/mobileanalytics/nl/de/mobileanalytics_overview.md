---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-13"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Informationen zu {{site.data.keyword.mobileanalytics_short}}  
{: aboutmobileanalytics}

{: shortdesc}
Vom {{site.data.keyword.mobileanalytics_full}}-Service werden wichtige Erkenntnisse zur Nutzung und Leistung einer Anwendung für die Entwickler mobiler Anwendungen und die Anwendungseigner bereitgestellt. Wenn Sie {{site.data.keyword.mobileanalytics_short}} verwenden, können die Anwendungseigner und -Entwickler verstehen, wie der Benutzer eine App wahrnimmt und diese Erkenntnisse zum Erstellen besserer Apps nutzen, die für die Benutzer noch viel attraktiver sind und sich von der riesigen Vielfalt der mobilen Apps deutlicher abheben. 

{: #overview}  
Der Service umfasst die {{site.data.keyword.mobileanalytics_short}}-Konsole, in der Entwickler und Anwendungseigner die Leistung einer mobilen Anwendung überwachen, die Nutzungsstatistikdaten anzeigen und die Geräteprotokolle durchsuchen können.  Von {{site.data.keyword.mobileanalytics_short}} werden Client-SDKs für iOS 8+ (nur Swift) und Android 4+ bereitgestellt.

<!-- Mobile Analytics Server SDKs - set of server SDKs to protect resources that are-->
<!--hosted on {{site.data.keyword.Bluemix_notm}}. Currently supported runtimes are-->
<!--Node.js and Java for Liberty.-->

Mit dem {{site.data.keyword.mobileanalytics_short}}-Service haben Sie folgende Möglichkeiten:
<!-- and includes the following capabilities: -->
<!-- * Near real-time analytics for client activity. Exp -->
<!--* Network latency analytics. GA only -->
<!-- * Client log search and download. Exp -->
<!--* Server log search and download. GA only -->
<!-- Crash and stack trace search. Exp -->

<dl>
	<dt>Sofort Erkenntnisse gewinnen</dt>
		<dd>Metriken zu Leistung und Nutzung in Echtzeit anzeigen.</dd>
	<dt>In Minuten implementieren</dt>
		<dd>Erstellen Sie eine Serviceinstanz in {{site.data.keyword.Bluemix}}, fügen Sie das SDK zum Projekt hinzu, fügen Sie zwei Codezeilen in die Anwendung ein, und Sie können Dutzende an vordefinierten Metriken erfassen.</dd>
	<dt>So viele Daten erfassen, wie Sie möchten</dt>
		<dd>Sie können Apps mit angepassten Ereignissen instrumentieren, ermitteln, wie Benutzer mit Ihrer App interagieren, Einkäufe verfolgen und die App-Aktivität überwachen.  
</dd>
<dt>Metriken für alle Anwendungen auf einen Blick anzeigen</dt>
	<dd>In der {{site.data.keyword.mobileanalytics_short}}-Konsole werden <!-- both --> gebrauchsfertige <!--and custom--> Diagramme bereitgestellt, für die keine Abfragen geschrieben werden müssen.</dd>
<dt>Gewünschte Schwerpunkte selbst festlegen</dt>
	<dd>Filtern Sie die Metriken nach Zeit, Adapter, Anwendung, Anwendungsversion, Betriebssystem, Betriebssystemversion oder Gerätemodell.</dd>
<dt>Schnell Probleme aufspüren</dt>
	<dd>Überprüfen Sie den Absturzstatus. Legen Sie Alert-Trigger für kritische Metriken fest und leiten Sie Alerts an einen beliebigen REST-Endpunkt weiter. </dd>
<dt>Fehlerbehebung für Fehlerursache</dt>
	<dd>Verwenden Sie die benutzerdefinierte Protokollierung in der Anwendung, laden Sie automatisch die Protokolle hoch und durchsuchen Sie sie in der Konsole. Führen Sie für Absturzereignisse einen Drilldown durch, um die Stack-Traces anzuzeigen. </dd>
</dl>
 

## Metriken und Ereignisse verwenden
{: #usingmetrics}

Mit **vordefinierten Metriken** können Sie Fragen wie die folgenden beantworten:

* Wie viele Benutzer sind neue Benutzer?  
* Von wie vielen Benutzern wird meine Anwendung derzeit aktiv verwendet?  
* Wie häufig verwenden die Benutzer meine Anwendung? 
* Zu welcher Tageszeit verwenden die Benutzer meine Anwendung?  
* Welches Gerätemodell bevorzugen meine Benutzer? 
* Ab wann sollte ich die Unterstützung für veraltete Betriebssysteme einstellen? 
* Bei welchen Anwendungen treten Leistungsprobleme auf?  

Durch das Hinzufügen Ihrer eigenen **angepassten Ereignisse** können Sie Fragen wie die folgenden beantworten: 

* Welche Features werden am meisten, welche am wenigsten verwendet?  
* Wo treten Benutzer in meine App ein und wo verlassen Sie sie wieder?  
* Welche Aktivitäten zeigen Benutzer am meisten an?  
* Führen Benutzer in der App Workflows durch (z. B. Konversionstrichter)?   

Clientseitige Protokolle und Nutzungsdaten werden automatisch gesammelt und bei Bedarf an den Mobile Analytics-Service gesendet. Entwickler und Administratoren können das {{site.data.keyword.mobileanalytics_short}}-Service-Dashboard zum Anzeigen von Daten verwenden, die vom Client-SDK erfasst werden.

## Datenvisualisierung
{: data-visualization}

Alle Daten, die vom Analyseservice erfasst werden, können über das {{site.data.keyword.mobileanalytics_short}}-Dashboard, auf das über Ihr {{site.data.keyword.Bluemix_notm}}-Dashboard durch Klicken auf die Kachel für Ihre IBM {{site.data.keyword.mobileanalytics_short}}-Serviceinstanz zugegriffen werden kann, visualisiert werden. <!--You can also create custom charts, based on data that is collected by the analytics service in the dashboard.--> Zusätzlich zu einer Übersicht Ihrer mobilen Analyse umfasst das Analysefeature die Funktion zum Durchführen einer unformatierten Suche für Clientprotokolle, für erfasste Daten zu einem Clientabsturz sowie beliebige zusätzliche Daten, die Sie explizit über Client-API-Funktionsaufrufe bereitstellen, die dem {{site.data.keyword.mobileanalytics_short}}-Service zugeführt werden. 

## {{site.data.keyword.mobileanalytics_short}} - Häufig gestellte Fragen 
{: #faq}

<dl>
	<dt>Was ist {{site.data.keyword.mobileanalytics_full}}?</dt>
		<dd>{{site.data.keyword.mobileanalytics_full}} ist ein Service, der Echtzeit- und Langzeitinformationen zur Leistung und Nutzung Ihrer mobilen Anwendungen liefert. Mithilfe von {{site.data.keyword.mobileanalytics_short}} können Anwendungsentwickler und -besitzer datengestützte Entscheidungen treffen, indem sie Trends bei aktiven Benutzern, Sitzungen, mobile Plattformen und App-Abstürze überwachen. Sie können auch Alerts zu ausgewählten Metriken einstellen, die nach ihrer Auslösung Nachrichten an jeden REST-Endpunkt senden, einschließlich eines Push-Service oder Ihrer internen Nachrichtenservices.</dd>
	<dt>Welche Möglichkeiten habe ich mit {{site.data.keyword.mobileanalytics_short}} for {{site.data.keyword.Bluemix_notm}}?</dt>
		<dd>Als Produktmanager für mobile Anwendungen können Sie sehen, wie viele Personen Ihre Anwendung nutzen (Benutzermetriken) und wann sie sie nutzen (Sitzungsmetriken). Diese Informationen werden in Form einer Zeitreihe dargestellt und in Echtzeit aktualisiert, sodass Sie sehen können, wie sich Ihre Änderungen an der Anwendung auswirken. Sie können nach bestimmten Anwendungsversionen oder Betriebssystemen filtern, um fundierte Entscheidungen über die Einstellung der Unterstützung oder Priorisierung treffen zu können. </dd>
		<dd>Als Anbieter mobiler Anwendungen können Sie Benutzer- und Sitzungsmetriken zur Überwachung von Kundenprojekten, zum Umgang mit der Abwanderung von Kunden und zur Auswertung der Effektivität von Marketingmaßnahmen im Bereich mobiler Apps nutzen, indem Sie Änderungen im Zeitverlauf beobachten und diese mit Ihren Ereignisdaten in Korrelation setzen.</dd>
		<dd>Als Entwickler mobiler Anwendungen können Sie anhand von Absturzmetriken Leistungsprobleme mobiler Apps aufspüren und beheben, bevor sich Benutzer darüber ärgern müssen und die Reputation der App Schaden nimmt. Sie können die Absturzanzahl und die Absturzrate an der Analysekonsole überwachen und die Bearbeitung derjenigen Abstürzen priorisieren, die die größte Benutzeranzahl betreffen. Sie können Alerts so einstellen, dass diese Benachrichtigungen senden oder automatisierte Abläufe auslösen, wenn Abstürze einen definierten Schwellenwert überschreiten. Außerdem können Sie Fehler beheben, indem Sie Absturzinstanzen eingehend untersuchen und sich Einheitenprotokolle und Anwendungsstack-Traces ansehen.</dd>
	<dt>Muss ich mich mit der Datenanalyse auskennen, um Mobile Analytics verwenden zu können?</dt>
		<dd>Nein, {{site.data.keyword.mobileanalytics_short}} bietet eine gebrauchsfertige Analysekonsole für Verantwortliche und Anwendungsentwickler. Spezialkenntnisse über Abfragen sind nicht erforderlich.</dd>
	<dt>Kann ich angepasste Abfragen anhand meiner Analysedaten durchführen?</dt>
		<dd>{{site.data.keyword.mobileanalytics_short}} ermöglicht keine angepassten Abfragen. Für die Zukunft wird dieses Feature jedoch erwogen.</dd>
	<dt>Wie verbinde ich meine Anwendung mit {{site.data.keyword.mobileanalytics_short}}?</dt>
		<dd>[Laden Sie unser Open-Source-SDK für iOS oder Android herunter](install-client-sdk.html), oder verwenden Sie die {{site.data.keyword.mobileanalytics_short}}-[REST-API](https://mobile-analytics-dashboard.{DomainName}/analytics-service/) für andere Plattformen. </dd>
	<dt>In welchen Bluemix-Regionen ist {{site.data.keyword.mobileanalytics_short}} verfügbar?</dt>
		<dd>Derzeitig ist Mobile Analytics in den USA (Süden) und im Vereinigtes Königreich verfügbar. Eine Verfügbarkeit in weiteren Regionen ist in Planung, der Zeitrahmen ist jedoch noch nicht festgelegt.</dd>
	<dt>Wie viel kostet dieser Service?</dt>
		<dd>Die ersten 100 Millionen Ereignisse, die jeden Monat erfasst werden, sind kostenlos. Danach kosten Ereignisse 1 $ pro einer Millionen Ereignisse.</dd>
	<dt>Was ist ein Ereignis?</dt>
		<dd>Zu derzeitig gemeldeten Ereignissen zählen der Start der Anwendungssitzung, das Ende der Anwendungssitzung (einschließlich Anwendungsabsturz), Alertbenachrichtigungen und Protokolleinträge.</dd>
	<dt>Wie kann die voraussichtlichen Kosten pro Monat für den Service ermitteln?</dt>
		<dd>Da die Preisbestimmung von der Anzahl der Ereignisse abhängt, die pro Clientkonto an den Service gesendet werden, wird durch die Anzahl der Ereignisse der Preis bestimmt.  
<p>
Der berechnete Preis ist die Summe aller Ereignisse aus allen Anwendungen, die mit {{site.data.keyword.mobileanalytics_short}} verbunden sind. Für eine bestimmte Anwendung hängt die Anzahl der Ereignisse vom Grad der Instrumentierung, die im Rahmen der Anwendung implementiert wurde, der Anzahl der Benutzer und dem Aktivitätsgrad der Benutzer ab.   
</p>
<p>
Verwenden Sie diese Format zur Kostenschätzung:
Ereignisse pro Monat pro App = (Benutzer pro Tag)(Sitzungen pro Benutzer pro Tag)(Tage pro Monat)(Ereignisse pro Sitzung)
</p>
<p>
Pro Sitzungen können zwischen zwei und mehrere Hundert Ereignisse auftreten. Dies hängt davon, welche Netzaufrufe, angepassten Analysen, Protokollerfassungen und Alertdefinitionen der Entwickler für die Anwendung konfiguriert hat.
</p>
	<dt>Wie lange werden meine Analysedaten aufbewahrt?</dt>
		<dd>Die Daten werden mindestens 30 Tage lang aufbewahrt.</dd>
	<dt>Wie lange dauert es, bis Daten in der {{site.data.keyword.mobileanalytics_short}}-Konsole angezeigt werden?</dt>
		<dd>Daten werden in der {{site.data.keyword.mobileanalytics_short}}-Konsole nahezu in Echtzeit angezeigt, d. h. innerhalb weniger Sekunden nach dem tatsächlichen Ereignis.</dd>
	<dt>Worin liegt der Unterschied zwischen {{site.data.keyword.mobileanalytics_full}} und der mobilen Analyse in MobileFirst Platform Foundation?</dt>
		<dd>Benutzer und Sitzungen unterscheiden sich bei beiden Konsolen kaum. Die Analysedaten von MobileFirst Platform Foundation enthalten allerdings zusätzliche Metriken und Einstellungen, die es Kunden ermöglichen, ihre eigenen Analysecluster lokal zu verwalten. Außerdem werden in der Analysekonsole von MobileFirst Platform Foundation Metriken für Adapter und Adapterprozeduren aufgegliedert, während beim {{site.data.keyword.mobileanalytics_short}}-Service diese Metriken in Netzanforderungsdiagramme und -tabellen integriert sind.</dd>
	<dt>Ich verwende MobileFirst Platform Foundation lokal zur Entwicklung meiner Apps, möchte aber nicht meinen eigenen Analysecluster hosten. Kann ich stattdessen {{site.data.keyword.mobileanalytics_full}} verwenden?</dt>
		<dd>Ja. Sie haben mehrere Optionen zur Auswahl: Wenn Sie MobileFirst Platform Foundation 7.x oder 8.0 verwenden und Ihre Apps mit MobileFirst Platform-SDKs instrumentiert sind, können Sie Ihren Worklight Server so konfigurieren, dass er Analysedaten an {{site.data.keyword.mobileanalytics_short}} for {{site.data.keyword.Bluemix_notm}} meldet. Im Blogbeitrag [Configuring Mobile Analytics and Mobile Foundation Bluemix services![Symbol für externen Link](https://mobilefirstplatform.ibmcloud.com/blog/2016/07/11/analytics-bm-service/){: new_window}(../../icons/launch-glyph.svg "Symbol für externen Link")] finden Sie weitere Details. Alternativ können Sie Ihre Apps auch mit dem {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobileanalytics_short}}-SDK instrumentieren und Daten direkt an den {{site.data.keyword.mobileanalytics_short}}-Service melden.</dd>
	<!-- <dt>My instance of  {{site.data.keyword.mobileanalytics_short}} does not look like the screen shots in the catalog. What's going on?</dt> -->
		<!-- <dd>Most likely you are using the Classic view interface for {{site.data.keyword.Bluemix_notm}}. Classic view is deprecated, so {{site.data.keyword.mobileanalytics_short}} runs best in the new {{site.data.keyword.Bluemix_notm}} interface. If you are in Classic view, you will see a link in the {{site.data.keyword.Bluemix_notm}} header that says <strong>Try the new {{site.data.keyword.Bluemix_notm}}</strong>. Click that link to use the new interface.</dd> -->
</dl>


# Zugehörige Links
 {:class="linklist"}

## SDK
{: rellink-sdk}
<!-- Links to SDK download and SDK Developer Guide -->
* [Android-SDK ![Symbol für externen Link](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}(../../icons/launch-glyph.svg "Symbol für externen Link")] 
* [iOS-SDK ![Symbol für externen Link](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window}(../../icons/launch-glyph.svg "Symbol für externen Link")]

<!-- {:elementKind="article" id="rellinks"} -->
