---

copyright:
  years: 2015, 2016

---
{:shortdesc: .shortdesc}

# Informationen zu {{site.data.keyword.mobileanalytics_short}}  
{: aboutmobileanalytics}
*Letzte Aktualisierung: 21. April 2016*
{: .last-updated}

{: shortdesc}
Vom {{site.data.keyword.mobileanalytics_full}}-Service werden wichtige Erkenntnisse zur Nutzung und Leistung einer App für die Entwickler mobiler Apps und die App-Eigner bereitgestellt.  Wenn Sie {{site.data.keyword.mobileanalytics_short}} verwenden, können die App-Eigner und -Entwickler verstehen, wie der Benutzer eine App wahrnimmt und diese Erkenntnisse zum Erstellen besserer Apps nutzen, die für die Benutzer noch viel attraktiver sind und sich von der riesigen Vielfalt der mobilen Apps deutlicher abheben. 

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
	<dt>Alle gewünschten Daten erfassen</dt>
		<dd>Instrumentieren Sie Apps mit benutzerdefinierten Ereignissen, stellen Sie fest, wie die Benutzer mit der App interagieren, verfolgen Sie Einkäufe und überwachen Sie die App-Aktivität.  
</dd>
<dt>Metriken für alle Apps auf einen Blick anzeigen</dt>
	<dd>In der {{site.data.keyword.mobileanalytics_short}}-Konsole werden gebrauchsfertige und benutzerdefinierte Diagramme bereitgestellt, für die keine Abfragen geschrieben werden müssen.</dd>
<dt>Gewünschte Schwerpunkte selbst festlegen</dt>
	<dd>Filtern Sie die Metriken nach Zeit, Adapter, App, App-Version, Betriebssystem, Betriebssystemversion oder Gerätemodell.</dd>
<dt>Schnell Probleme aufspüren</dt>
	<dd>Überprüfen Sie den Absturzstatus. Legen Sie Alert-Trigger für kritische Metriken fest und leiten Sie Alerts an einen beliebigen REST-Endpunkt weiter. </dd>
<dt>Fehlerbehebung für Fehlerursache</dt>
	<dd>Verwenden Sie die Protokollierung für benutzerdefinierte Clients in der App, laden Sie automatisch die Protokolle hoch und durchsuchen Sie sie in der Konsole. Führen Sie für Absturzereignisse einen Drilldown durch, um die Stack-Traces anzuzeigen. </dd>
</dl>
 

## Metriken und Ereignisse verwenden
{: #usingmetrics}

Mit **vordefinierten Metriken** können Sie Fragen wie die folgenden beantworten:

*Wie viele Benutzer sind neue Benutzer?*  
*Von wie vielen Benutzern wird meine App derzeit aktiv verwendet?*  
*Wie häufig verwenden die Benutzer meine App?*  
*Zu welcher Tageszeit verwenden die Benutzer meine App?*  
*Welches Gerätemodell bevorzugen meine Benutzer?*  
*Ab wann sollte ich die Unterstützung für veraltete Betriebssysteme einstellen?*  
*Bei welchen Apps treten Leistungsprobleme auf?*  

Wenn Sie eigene **benutzerdefinierte Ereignisse** hinzufügen, können Sie Fragen wie die folgenden stellen:  

*Welche Funktionen werden am meisten und am seltensten verwendet?*  
*Wo starten und beenden die Benutzer meine App?*  
*Welche Aktivitäten zeigen die Benutzer am meisten an?*  
*Führen die Benutzer in der App Arbeitsabläufe aus? (zum Beispiel Konversionstrichter)*  

<!--Client-side logs and usage data are gathered automatically and sent to the Mobile Analytics -->
<!-- service on demand. Developers and -->
<!-- administrators can use the {{site.data.keyword.mobileanalytics_short}} service dashboard to view data that -->
<!-- is gathered by the client SDK. -->

<!--## Data visualization
{: data-visualization}

All data that is collected by the analytics service can be visualized through the {{site.data.keyword.mobileanalytics_short}} dashboard which is accessible from your {{site.data.keyword.Bluemix_notm}} dashboard by clicking your IBM {{site.data.keyword.mobileanalytics_short}} service tile instance. You can also create custom charts, based on data that is collected by the analytics service in the dashboard. In addition to an at-a-glance view of your mobile analytics, the analytics feature includes the capability to perform a raw search against client logs, captured client crash data, and any extra data that you explicitly provide through client API function calls that feed into the {{site.data.keyword.mobileanalytics_short}} service. -->

># Zugehörige Links {:class="linklist"}
<!-->## Lernprogramme und Beispiele {:id="samples"}-->
<!-->* [Link 1](https://github.com/)-->
>
># Zugehörige Links {:class="linklist"}
>## Zugehörige Links {:id="general"}
## SDK
<!-- Links to SDK download and SDK Developer Guide -->
* [Android-SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core )  
* [iOS-SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core)  
>
>{:elementKind="article" id="rellinks"}
