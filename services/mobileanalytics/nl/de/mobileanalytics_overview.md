---

copyright:
  years: 2015, 2016

---
{:shortdesc: .shortdesc}

# Informationen zu {{site.data.keyword.mobileanalytics_short}}  
{: aboutmobileanalytics}
Letzte Aktualisierung: 29. August 2016
{: .last-updated}

{: shortdesc}
Vom {{site.data.keyword.mobileanalytics_full}}-Service werden wichtige Erkenntnisse zur Nutzung und Leistung einer App für die Entwickler mobiler Apps und die App-Eigner bereitgestellt. Wenn Sie {{site.data.keyword.mobileanalytics_short}} verwenden, können die App-Eigner und -Entwickler verstehen, wie der Benutzer eine App wahrnimmt und diese Erkenntnisse zum Erstellen besserer Apps nutzen, die für die Benutzer noch viel attraktiver sind und sich von der riesigen Vielfalt der mobilen Apps deutlicher abheben. 

{: #overview}  
Der Service umfasst die {{site.data.keyword.mobileanalytics_short}}-Konsole, in der Entwickler und App-Eigner die Leistung einer mobilen Anwendung überwachen, die Nutzungsstatistikdaten anzeigen und die Geräteprotokolle durchsuchen können.  Von {{site.data.keyword.mobileanalytics_short}} werden Client-SDKs für iOS 8+ (nur Swift) und Android 4+ bereitgestellt.

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
		<dd>Erstellen Sie eine Serviceinstanz in {{site.data.keyword.Bluemix}}, fügen Sie das SDK zum Projekt hinzu, fügen Sie zwei Codezeilen in die App ein, und Sie können Dutzende an vordefinierten Metriken erfassen.</dd>
	<!--<dt>Collect any data you want</dt>-->
		<!--<dd>Instrument apps with custom events, discover how users are interacting with your app, track purchases, and monitor app activity.  
</dd>-->
<dt>Metriken für alle Apps auf einen Blick anzeigen</dt>
	<dd>In der {{site.data.keyword.mobileanalytics_short}}-Konsole werden <!-- both --> gebrauchsfertige <!--and custom--> Diagramme bereitgestellt, für die keine Abfragen geschrieben werden müssen.</dd>
<dt>Gewünschte Schwerpunkte selbst festlegen</dt>
	<dd>Filtern Sie die Metriken nach Zeit, Adapter, App, App-Version, Betriebssystem, Betriebssystemversion oder Gerätemodell.</dd>
<dt>Schnell Probleme aufspüren</dt>
	<dd>Überprüfen Sie den Absturzstatus. Legen Sie Alert-Trigger für kritische Metriken fest und leiten Sie Alerts an einen beliebigen REST-Endpunkt weiter. </dd>
<dt>Fehlerbehebung für Fehlerursache</dt>
	<dd>Verwenden Sie die benutzerdefinierte Protokollierung in der App, laden Sie automatisch die Protokolle hoch und durchsuchen Sie sie in der Konsole. Führen Sie für Absturzereignisse einen Drilldown durch, um die Stack-Traces anzuzeigen. </dd>
</dl>
 

## Metriken und Ereignisse verwenden
{: #usingmetrics}

Mit **vordefinierten Metriken** können Sie Fragen wie die folgenden beantworten:

* Wie viele Benutzer sind neue Benutzer?  
* Von wie vielen Benutzern wird meine App derzeit aktiv verwendet?  
* Wie häufig verwenden die Benutzer meine App? 
* Zu welcher Tageszeit verwenden die Benutzer meine App?  
* Welches Gerätemodell bevorzugen meine Benutzer? 
* Ab wann sollte ich die Unterstützung für veraltete Betriebssysteme einstellen? 
* Bei welchen Apps treten Leistungsprobleme auf?  

<!--By adding your own **custom events** you can answer questions like:--> 

<!--* What features are used most and least?-->  
<!--* Where are users entering and leaving my app?-->  
<!--* What activities are users viewing most? --> 
<!--* Are users completing workflows in the app (for example, conversion funnels)? -->  

<!--Client-side logs and usage data are gathered automatically and sent to the Mobile Analytics -->
<!-- service on demand. Developers and -->
<!-- administrators can use the {{site.data.keyword.mobileanalytics_short}} service dashboard to view data that -->
<!-- is gathered by the client SDK. -->

<!--## Data visualization
{: data-visualization}

All data that is collected by the analytics service can be visualized through the {{site.data.keyword.mobileanalytics_short}} dashboard which is accessible from your {{site.data.keyword.Bluemix_notm}} dashboard by clicking your IBM {{site.data.keyword.mobileanalytics_short}} service tile instance. You can also create custom charts, based on data that is collected by the analytics service in the dashboard. In addition to an at-a-glance view of your mobile analytics, the analytics feature includes the capability to perform a raw search against client logs, captured client crash data, and any extra data that you explicitly provide through client API function calls that feed into the {{site.data.keyword.mobileanalytics_short}} service. -->

## {{site.data.keyword.mobileanalytics_short}} - Häufig gestellte Fragen 
{: #faq}

<dl>
	<dt>Was ist {{site.data.keyword.mobileanalytics_full}}?</dt>
		<dd>{{site.data.keyword.mobileanalytics_full}} ist ein Service, der Echtzeit- und Langzeitinformationen zur Leistung und Nutzung Ihrer mobilen Apps liefert.  Mithilfe von {{site.data.keyword.mobileanalytics_short}} können Entwickler und Besitzer von Apps datengestützte Entscheidungen treffen, indem sie Trends bei aktiven Benutzern, Sitzungen, mobile Plattformen und App-Abstürze überwachen. Sie können auch Alerts zu ausgewählten Metriken einstellen, die nach ihrer Auslösung Nachrichten an jeden REST-Endpunkt senden, einschließlich eines Push-Service oder Ihrer internen Nachrichtenservices.</dd>
	<dt>Welche Möglichkeiten habe ich mit {{site.data.keyword.mobileanalytics_short}} for {{site.data.keyword.Bluemix_notm}} (Beta)?</dt>
		<dd>Als Produktmanager für mobile Apps können Sie sehen, wie viele Personen Ihre App nutzen (Benutzermetriken) und wann sie sie nutzen (Sitzungsmetriken).  Diese Informationen werden in Form einer Zeitreihe dargestellt und in Echtzeit aktualisiert, sodass Sie sehen können, wie sich Ihre Änderungen an der App auswirken.  Sie können nach bestimmten App-Versionen oder Betriebssystemen filtern, um fundierte Entscheidungen über die Einstellung der Unterstützung oder Priorisierung treffen zu können. </dd>
		<dd>Als Anbieter mobiler Apps können Sie Benutzer- und Sitzungsmetriken zur Überwachung von Kundenprojekten, zum Umgang mit der Abwanderung von Kunden und zur Auswertung der Effektivität von Marketingmaßnahmen im Bereich mobiler Apps nutzen, indem Sie Änderungen im Zeitverlauf beobachten und diese mit Ihren Ereignisdaten in Korrelation setzen.</dd>
		<dd>Als Entwickler mobiler Apps können Sie anhand von Absturzmetriken Leistungsprobleme mobiler Apps aufspüren und beheben, bevor sich Benutzer darüber ärgern müssen und die Reputation der App Schaden nimmt. Sie können die Absturzanzahl und die Absturzrate an der Analysekonsole überwachen und die Bearbeitung derjenigen Abstürzen priorisieren, die die größte Benutzeranzahl betreffen. Sie können Alerts so einstellen, dass diese Benachrichtigungen senden oder automatisierte Abläufe auslösen, wenn Abstürze einen definierten Schwellenwert überschreiten. Außerdem können Sie Fehler beheben, indem Sie Absturzinstanzen eingehend untersuchen und sich Einheitenprotokolle und App-Stack-Traces ansehen.</dd>
	<dt>Muss ich mich mit der Datenanalyse auskennen, um Mobile Analytics verwenden zu können?</dt>
		<dd>Nein, {{site.data.keyword.mobileanalytics_short}} bietet eine gebrauchsfertige Analysekonsole für Verantwortliche und App-Entwickler. Spezialkenntnisse über Abfragen sind nicht erforderlich.</dd>
	<dt>Kann ich angepasste Abfragen anhand meiner Analysedaten durchführen?</dt>
		<dd>Die {{site.data.keyword.mobileanalytics_short}} Betaversion ermöglicht keine angepassten Abfragen. Für die Zukunft wird dieses Feature jedoch erwogen.</dd>
	<dt>Wie verbinde ich meine App mit {{site.data.keyword.mobileanalytics_short}}?</dt>
		<dd>[Laden Sie unser Open-Source-SDK für iOS oder Android herunter](install-client-sdk.html), oder verwenden Sie die {{site.data.keyword.mobileanalytics_short}}-[REST-API](https://mobile-analytics-dashboard.stage1.ng.bluemix.net/analytics-service/) für andere Plattformen. </dd>
	<dt>In welchen Bluemix-Regionen ist {{site.data.keyword.mobileanalytics_short}} verfügbar?</dt>
		<dd>Zum Zeitpunkt, als dieser Text verfasst wurde, war Mobile Analytics im Süden der USA und in Großbritannien verfügbar. Verfügbarkeit in weiteren Regionen ist in Planung, der Zeitrahmen ist jedoch noch nicht festgelegt.</dd>
	<dt>Wie viel kostet dieser Service?</dt>
		<dd>Die Betaversion des Service ist kostenlos.</dd>
	<dt>Wie lange werden meine Analysedaten aufbewahrt?</dt>
		<dd>Bei der Betaversion werden die Daten mindestens 30 Tage lang aufbewahrt.</dd>
	<dt>Wie lange dauert es, bis Daten in der {{site.data.keyword.mobileanalytics_short}}-Konsole angezeigt werden?</dt>
		<dd>Daten werden in der {{site.data.keyword.mobileanalytics_short}}-Konsole nahezu in Echtzeit angezeigt, d. h. innerhalb weniger Sekunden nach dem tatsächlichen Ereignis.</dd>
	<dt>Worin liegt der Unterschied zwischen {{site.data.keyword.mobileanalytics_full}} und der mobilen Analyse in MobileFirst Platform Foundation?</dt>
		<dd>Benutzer und Sitzungen unterscheiden sich bei beiden Konsolen kaum. Die Analysedaten von MobileFirst Platform Foundation enthalten allerdings zusätzliche Metriken und Einstellungen, die es Kunden ermöglichen, ihre eigenen Analysecluster lokal zu verwalten. Außerdem werden in der  Analysekonsole von MobileFirst Platform Foundation Metriken für Adapter und Adapterprozeduren aufgegliedert, während wir beim {{site.data.keyword.mobileanalytics_short}}-Service planen, diese Metriken in Netzanforderungsdiagramme und -tabellen im {{site.data.keyword.mobileanalytics_short}}-Service zu integrieren (nach der Betaversion).</dd>
	<dt>Ich verwende MobileFirst Platform Foundation lokal zur Entwicklung meiner Apps, möchte aber nicht meinen eigenen Analysecluster hosten. Kann ich stattdessen {{site.data.keyword.mobileanalytics_full}} verwenden?</dt>
		<dd>Ja. Sie haben hier mehrere Optionen zur Auswahl: Wenn Sie MobileFirst Platform Foundation 7.x oder 8.0 verwenden und Ihre Apps mit MobileFirst Platform-SDKs instrumentiert sind, können Sie Ihren Worklight Server so konfigurieren, dass er Analysedaten an {{site.data.keyword.mobileanalytics_short}} for {{site.data.keyword.Bluemix_notm}} meldet. Im Blogbeitrag [Configuring Mobile Analytics and Mobile Foundation Bluemix services](https://mobilefirstplatform.ibmcloud.com/blog/2016/07/11/analytics-bm-service/) finden Sie weitere Details. Alternativ können Sie Ihre Apps auch mit dem {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobileanalytics_short}}-SDK instrumentieren und Daten direkt an den {{site.data.keyword.mobileanalytics_short}}-Service melden.</dd>
	<dt>Ich versuche, {{site.data.keyword.mobileanalytics_short}} zu verwenden und sehe nur Leerraum, wo eigentlich meine Diagramme stehen sollten. Was ist da los?</dt>
		<dd>Sehr wahrscheinlich arbeiten Sie mit der klassischen Ansicht für {{site.data.keyword.Bluemix_notm}}. Die klassische Ansicht wird nicht mehr verwendet, deshalb wird {{site.data.keyword.mobileanalytics_short}} Beta in der neuen {{site.data.keyword.Bluemix_notm}}-Schnittstelle ausgeführt. Wenn Sie sich in der klassischen Ansicht befinden, sehen Sie im {{site.data.keyword.Bluemix_notm}}-Header den Link "Try the new {{site.data.keyword.Bluemix_notm}}!". Klicken Sie auf diesen Link, um die neue Schnittstelle zu verwenden.</dd>
</dl>


# Zugehörige Links
 {:class="linklist"}

## SDK
{: rellink-sdk}
<!-- Links to SDK download and SDK Developer Guide -->
* [Android-SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)  
* [iOS-SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core)  

<!-- {:elementKind="article" id="rellinks"} -->
