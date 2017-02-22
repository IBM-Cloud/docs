---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Push-Benachrichtigungen überwachen 
{: #monitor-notifications}
Letzte Aktualisierung: 16. Januar 2017
{: .last-updated}


Der IBM {{site.data.keyword.mobilepushshort}}-Service verfügt nun über erweiterte Funktionen zum Überwachen des Durchsatzes von Push-Operationen, indem aus Ihren Benutzerdaten Diagramme generiert werden. Sie können das Dienstprogramm zum Auflisten aller gesendeten Push-Benachrichtigungen oder aller registrierten Geräte sowie für die tägliche, wöchentliche oder monatliche Analyse der Informationen verwenden.

Verwenden Sie zum Generieren von Berichten für alle Ihre gesendeten Benachrichtigungen die in [REST-APIs](https://mobile.{DomainName}/imfpush/){: new_window} beschriebene Berichtsmethode 'GET report' für Push-Nachrichten. 

![Bericht über gesendete Benachrichtigungen](images/monitoring_messages.jpg)


Verwenden Sie zum Generieren von Berichten für alle Ihre registrierten Geräte die in [REST-APIs](https://mobile.{DomainName}/imfpush/){: new_window} beschriebene Berichtsmethode 'GET report' für Push-Geräteregistrierungen.

![Bericht über registrierte Geräte](images/monitoring_devices.jpg)

Informationen zum Aktualisieren Ihres Android-SDK für die Überwachung Ihrer Benachrichtigungsinformationen finden Sie in [Push-Benachrichtigungen in Android-Geräten überwachen](c_android_enable.html#android_monitor).


 
