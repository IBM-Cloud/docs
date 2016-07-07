---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Einführung in {{site.data.keyword.mobilefoundation_short}}
{: #gettingstartedtemplate}

*Letzte Aktualisierung: 15. Juni 2016*
{: .last-updated}

{{site.data.keyword.mobilefoundation_long}} beschleunigt die Einrichtung einer {{site.data.keyword.mfp_full}}-Umgebung, von der Sie mobile Unternehmens-Apps entwickeln, testen und betreiben können. {{site.data.keyword.mobilefoundation_short}} ist mit zwei verschiedenen Serviceplänen verfügbar: Developer und Professional 1 Application.
{:shortdesc}

Der Professional 1 Application-Plan ermöglicht die Bereitstellung des {{site.data.keyword.mobilefoundation_short}}-Servers für eine skalierbare Containergruppe. Mit dem Professional 1 Application-Plan kann eine einzelne Anwendung, die auf einer oder mehreren der unterstützten Betriebsplattformen, wie z. B. Android, iOS, Windows oder Mobile Web, erstellt wird, verwaltet werden. Der Developer-Plan bietet keine Unterstützung für die {{site.data.keyword.mobilefoundation_short}}-Bereitstellung für eine Containergruppe mit mehr als einem Knoten. Dieser Plan ist am besten für Entwicklungs- und Testzwecke geeignet.

## Einführung in den {{site.data.keyword.mobilefoundation_short}}: Developer-Plan

Nachdem Sie eine Instanz von {{site.data.keyword.mobilefoundation_short}}: Developer-Service erstellt haben, können Sie mit der Erstellung Ihres mobilen Kanals mit wenigen Klicks beginnen. 

*	Klicken Sie auf **Basisserver starten**, um eine {{site.data.keyword.mobilefirst_notm}}-Serverinstanz mit der Standardkonfiguration zu erstellen.

  `Die Basisserverinstanz umfasst einen zentralen
Knoten, 1 GB Hauptspeicher sowie 64 GB Speicherkapazität.`

* Zur Erstellung einer {{site.data.keyword.mobilefirst_notm}}-Serverinstanz mit erweiterter Konfiguration für Topologie, Sicherheit und weitere Serverkonfigurationen klicken Sie auf **Server mit erweiterter Konfiguration starten**. Weitere Informationen finden Sie in [Erweiterte Konfiguration einrichten](c_using_mfs_p1.html#using_mfs_advanced_p1).

## Einführung in den {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application-Plan

Nachdem Sie eine Instanz von {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application-Service erstellt haben, können Sie mit der Erstellung Ihres mobilen Kanals beginnen, indem Sie die folgenden Schritte ausführen.

1.  Stellen Sie eine Verbindung zu einem vorhandenen {{site.data.keyword.dashdbshort}}: Enterprise Transactional-Service in {{site.data.keyword.Bluemix_notm}} her.

    1.  Wählen Sie den {{site.data.keyword.Bluemix_notm}}-`Bereich`, in dem sich die {{site.data.keyword.dashdbshort_notm}}-Serviceinstanz befindet, in der Liste der Bereiche aus, die in der aktuellen `Organisation` verfügbar sind.

    2.  Wählen Sie den `Servicenamen` und die `Berechtigungsnachweise` für {{site.data.keyword.dashdbshort_notm}} aus, um eine Verbindung zur vorhandenen {{site.data.keyword.dashdbshort_notm}}-Serviceinstanz herzustellen.

    3.  Testen Sie die Verbindung zur ausgewählten {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional-Serviceinstanz, indem Sie auf **Verbindung testen** klicken.

    4.  Klicken Sie auf **Hinzufügen** und anschließend auf **Weiter** im Popup-Fenster, in dem Sie zur Bestätigung des ausgewählten {{site.data.keyword.dashdbshort_notm}}-Service aufgefordert werden. Mit dieser Aktion werden die erforderlichen Tabellen in der konfigurierten {{site.data.keyword.dashdbshort_notm}}-Datenbankserviceinstanz erstellt.

2.  Erstellen Sie den Server und starten Sie ihn.

    * Klicken Sie auf **Basisserver starten**, um eine {{site.data.keyword.mobilefirst_notm}}-Serverinstanz mit der Standardkonfiguration zu erstellen.

      `Die Basisserverinstanz umfasst einen zentralen
Knoten, 1 GB Hauptspeicher sowie 64 GB Speicherkapazität.`

    * Zur Erstellung einer {{site.data.keyword.mobilefirst_notm}}-Serverinstanz mit erweiterter Konfiguration für Topologie, Sicherheit und weitere Serverkonfigurationen klicken Sie auf **Server mit erweiterter Konfiguration starten**. Weitere Informationen finden Sie in [Erweiterte Konfiguration einrichten](c_using_mfs_p2.html#using_mfs_advanced_p2).

Lesen Sie im Abschnitt zur Verwendung des Mobile Foundation-Service zur Einrichtung des MobileFirst-Servers in IBM Containern ([Using the Mobile Foundation service to set up MobileFirst Server on IBM Containers](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/ibm-containers/using-mobile-foundation/)), um mehr darüber zu erfahren, wie Sie mit der Verwendung von {{site.data.keyword.mobilefoundation_short}} beginnen.

# Zugehörige Links
{: #rellinks}

## Zugehörige Links
{: #general}

*	[IBM MobileFirst Platform Foundation V8.0.0 - Produktdokumentation](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}
*	[IBM MobileFirst Platform Developer Center](https://mobilefirstplatform.ibmcloud.com){: new_window}
