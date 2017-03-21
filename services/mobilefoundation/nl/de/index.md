---

copyright:
  years: 2016, 2017
lastupdated:  "2017-02-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Einführung in Mobile Foundation
{: #gettingstartedtemplate}

{{site.data.keyword.mobilefoundation_long}} beschleunigt die Einrichtung einer {{site.data.keyword.mfp_full}}-Umgebung, von der Sie mobile Unternehmens-Apps entwickeln, testen und betreiben können. {{site.data.keyword.mobilefoundation_short}} ist mit zwei verschiedenen Serviceplänen verfügbar: Developer und Professional 1 Application.
{:shortdesc}

<!-- The Professional 1 Application plan allows the {{site.data.keyword.mobilefoundation_short}} server to be deployed on a scalable container group.--> Mit dem Professional 1 Application-Plan kann eine einzelne Anwendung, die auf einer oder mehreren der unterstützten Betriebsplattformen, wie z. B. Android, iOS, Windows oder Mobile Web, erstellt wird, verwaltet werden. Dieser Plan <!-- does not support {{site.data.keyword.mobilefoundation_short}} deployment on a container group with more than 1 node. This plan --> ist am besten für Entwicklungs- und Testzwecke geeignet.

## Einführung in den Mobile Foundation: Developer-Plan
{: #gettingstartedtemplate_dev}

Nachdem Sie eine Instanz von {{site.data.keyword.mobilefoundation_short}}: Developer-Service erstellt haben, können Sie mit der Erstellung Ihres mobilen Kanals mit wenigen Klicks beginnen.

*	Klicken Sie auf **Basisserver starten**, um eine {{site.data.keyword.mobilefirst_notm}}-Serverinstanz mit der Standardkonfiguration zu erstellen.

  `Die Basisserverinstanz umfasst einen zentralen Knoten und 1 GB Speicherkapazität.`

* Zur Erstellung einer {{site.data.keyword.mobilefirst_notm}}-Serverinstanz mit erweiterter Konfiguration für Topologie, Sicherheit und weitere Serverkonfigurationen klicken Sie auf **Server mit erweiterter Konfiguration starten**. Weitere Informationen finden Sie in [Erweiterte Konfiguration einrichten](c_using_mfs_p1.html#using_mfs_advanced_p1).

## Einführung in den Mobile Foundation: Professional 1 Application-Plan
{: #gettingstartedtemplate_prof}

Nachdem Sie eine Instanz von {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application-Service erstellt haben, können Sie mit der Erstellung Ihres mobilen Kanals beginnen, indem Sie die folgenden Schritte ausführen.

1.  Stellen Sie eine Verbindung zu einem vorhandenen {{site.data.keyword.dashdbshort}} for Transactions-Service in {{site.data.keyword.Bluemix_notm}} her.

    1.  Wählen Sie die {{site.data.keyword.Bluemix_notm}} `Organisation` aus, in der sich die {{site.data.keyword.dashdbshort_notm}}-Serviceinstanz befindet.

    + Wählen Sie den {{site.data.keyword.Bluemix_notm}}-`Bereich`, in dem sich die {{site.data.keyword.dashdbshort_notm}}-Serviceinstanz befindet, in der Liste der Bereiche aus, die in der ausgewählten `Organisation` verfügbar sind.

    + Wählen Sie den `Servicenamen` und die `Berechtigungsnachweise` für {{site.data.keyword.dashdbshort_notm}} aus, um eine Verbindung zur vorhandenen {{site.data.keyword.dashdbshort_notm}}-Serviceinstanz herzustellen.

    + Testen Sie die Verbindung zu der ausgewählten {{site.data.keyword.dashdbshort_notm}} for Transactions-Serviceinstanz, indem Sie auf **Verbindung testen** klicken.

    + Klicken Sie auf **Hinzufügen** und anschließend auf **Weiter** in dem Popup-Fenster, in dem Sie zur Bestätigung des ausgewählten {{site.data.keyword.dashdbshort_notm}} for Transactions-Service aufgefordert werden. Mit dieser Aktion werden die erforderlichen Tabellen in der konfigurierten {{site.data.keyword.dashdbshort_notm}}-Datenbankserviceinstanz erstellt.

    **Hinweis:** Nach dem Hinzufügen einer {{site.data.keyword.dashdbshort_notm}}-Verbindung zur {{site.data.keyword.mobilefoundation_short}}-Instanz kann diese nicht mehr geändert werden.

2.  Erstellen Sie den Server und starten Sie ihn.

    * Klicken Sie auf **Basisserver starten**, um eine {{site.data.keyword.mobilefirst_notm}}-Serverinstanz mit der Standardkonfiguration zu erstellen.

      `Die Basisserverinstanz umfasst einen zentralen Knoten und 1 GB Speicherkapazität.`

    * Zur Erstellung einer {{site.data.keyword.mobilefirst_notm}}-Serverinstanz mit erweiterter Konfiguration für Topologie, Sicherheit und weitere Serverkonfigurationen klicken Sie auf **Server mit erweiterter Konfiguration starten**. Weitere Informationen finden Sie in [Erweiterte Konfiguration einrichten](c_using_mfs_p2.html#using_mfs_advanced_p2).

## Einführung in den Mobile Foundation: Developer Pro-Plan
{: #gettingstartedtemplate_devpro}

Nachdem Sie eine Instanz von {{site.data.keyword.mobilefoundation_short}}: Developer Pro-Service erstellt haben, können Sie mit der Erstellung Ihres mobilen Kanals beginnen, indem Sie die folgenden Schritte ausführen.

  1.  Stellen Sie eine Verbindung zu einem vorhandenen {{site.data.keyword.dashdbshort}} for Transactions-Service in {{site.data.keyword.Bluemix_notm}} her.

      1.  Wählen Sie die {{site.data.keyword.Bluemix_notm}} `Organisation` aus, in der sich die {{site.data.keyword.dashdbshort_notm}}-Serviceinstanz befindet.

      + Wählen Sie den {{site.data.keyword.Bluemix_notm}}-`Bereich`, in dem sich die {{site.data.keyword.dashdbshort_notm}}-Serviceinstanz befindet, in der Liste der Bereiche aus, die in der ausgewählten `Organisation` verfügbar sind.

      + Wählen Sie den `Servicenamen` und die `Berechtigungsnachweise` für {{site.data.keyword.dashdbshort_notm}} aus, um eine Verbindung zur vorhandenen {{site.data.keyword.dashdbshort_notm}}-Serviceinstanz herzustellen.

      + Testen Sie die Verbindung zu der ausgewählten {{site.data.keyword.dashdbshort_notm}} for Transactions-Serviceinstanz, indem Sie auf **Verbindung testen** klicken.

      + Klicken Sie auf **Hinzufügen** und anschließend auf **Weiter** in dem Popup-Fenster, in dem Sie zur Bestätigung des ausgewählten {{site.data.keyword.dashdbshort_notm}} for Transactions-Service aufgefordert werden. Mit dieser Aktion werden die erforderlichen Tabellen in der konfigurierten {{site.data.keyword.dashdbshort_notm}}-Datenbankserviceinstanz erstellt.

      **Hinweis:** Nach dem Hinzufügen einer {{site.data.keyword.dashdbshort_notm}}-Verbindung zur {{site.data.keyword.mobilefoundation_short}}-Instanz kann diese nicht mehr geändert werden.

  2.  Erstellen Sie den Server und starten Sie ihn.

      * Klicken Sie auf **Basisserver starten**, um eine {{site.data.keyword.mobilefirst_notm}}-Serverinstanz mit der Standardkonfiguration zu erstellen.

      * Diese Auswahl stellt einen {{site.data.keyword.mfserver_long_notm}} mit den folgenden Einstellungen bereit:

          - Einzelner Knoten mit 1 GB Hauptspeicher. Diese Größe ist für Entwicklungs- und kleinere Testaktivitäten sowie für kleinere Produktionsworkloads ausreichend.

          -	`Benutzername` und `Kennwort` werden automatisch für Sie generiert. Sie können darauf zugreifen, wenn der Server betriebsbereit ist.

      * Zur Erstellung einer {{site.data.keyword.mobilefirst_notm}}-Serverinstanz mit erweiterter Konfiguration für Topologie, Sicherheit und weitere Serverkonfigurationen klicken Sie auf **Server mit erweiterter Konfiguration starten**. Weitere Informationen finden Sie in [Erweiterte Konfiguration einrichten](c_using_mfs_p3.html#using_mfs_advanced_p3).

## Einführung in den Mobile Foundation: Professional Per Capacity-Plan
{: #gettingstartedtemplate_profper}

Nachdem Sie eine Instanz von {{site.data.keyword.mobilefoundation_short}}: Professional Per Capacity-Service erstellt haben, können Sie mit der Erstellung Ihres mobilen Kanals beginnen, indem Sie die folgenden Schritte ausführen.

  1.  Stellen Sie eine Verbindung zu einem vorhandenen {{site.data.keyword.dashdbshort}} for Transactions-Service in {{site.data.keyword.Bluemix_notm}} her.

      1.  Wählen Sie die {{site.data.keyword.Bluemix_notm}} `Organisation` aus, in der sich die {{site.data.keyword.dashdbshort_notm}}-Serviceinstanz befindet.

      + Wählen Sie den {{site.data.keyword.Bluemix_notm}}-`Bereich`, in dem sich die {{site.data.keyword.dashdbshort_notm}}-Serviceinstanz befindet, in der Liste der Bereiche aus, die in der ausgewählten `Organisation` verfügbar sind.

      + Wählen Sie den `Servicenamen` und die `Berechtigungsnachweise` für {{site.data.keyword.dashdbshort_notm}} aus, um eine Verbindung zur vorhandenen {{site.data.keyword.dashdbshort_notm}}-Serviceinstanz herzustellen.

      + Testen Sie die Verbindung zu der ausgewählten {{site.data.keyword.dashdbshort_notm}} for Transactions-Serviceinstanz, indem Sie auf **Verbindung testen** klicken.

      + Klicken Sie auf **Hinzufügen** und anschließend auf **Weiter** in dem Popup-Fenster, in dem Sie zur Bestätigung des ausgewählten {{site.data.keyword.dashdbshort_notm}} for Transactions-Service aufgefordert werden. Mit dieser Aktion werden die erforderlichen Tabellen in der konfigurierten {{site.data.keyword.dashdbshort_notm}}-Datenbankserviceinstanz erstellt.

      **Hinweis:** Nach dem Hinzufügen einer {{site.data.keyword.dashdbshort_notm}}-Verbindung zur {{site.data.keyword.mobilefoundation_short}}-Instanz kann diese nicht mehr geändert werden.

  2.  Erstellen Sie den Server und starten Sie ihn.

      * Klicken Sie auf **Basisserver starten**, um eine {{site.data.keyword.mobilefirst_notm}}-Serverinstanz mit der Standardkonfiguration zu erstellen.

      * Diese Auswahl stellt einen {{site.data.keyword.mfserver_long_notm}} mit den folgenden Einstellungen bereit:
          -  2 Knoten mit jeweils 1 GB Hauptspeicher. Diese Größe ist für Entwicklungs- und kleinere Testaktivitäten sowie für kleinere Produktionsworkloads ausreichend.

          -	`Benutzername` und `Kennwort` werden automatisch für Sie generiert. Sie können darauf zugreifen, wenn der Server betriebsbereit ist.

      * Zur Erstellung einer {{site.data.keyword.mobilefirst_notm}}-Serverinstanz mit erweiterter Konfiguration für Topologie, Sicherheit und weitere Serverkonfigurationen klicken Sie auf **Server mit erweiterter Konfiguration starten**. Weitere Informationen finden Sie in [Erweiterte Konfiguration einrichten](c_using_mfs_p4.html#using_mfs_advanced_p4).

Lesen Sie den Abschnitt [Using the Mobile Foundation service to set up MobileFirst Server<!-- on IBM Containers--> ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/bluemix/using-mobile-foundation/){: new_window}, um mehr darüber zu erfahren, wie Sie mit der Verwendung von {{site.data.keyword.mobilefoundation_short}} beginnen.

##  Bekannte Einschränkungen
{: #knownlimitations_mfp}

* In der Benutzerschnittstelle des {{site.data.keyword.mobilefoundation_short}}-Service wird zum Anzeigen von Zahlen nicht das vom Benutzer ausgewählte ländereinstellungsspezifische Muster verwendet.


# Zugehörige Links
{: #rellinks  notoc}

## Zugehörige Links
{: #general notoc}

*	[Produktdokumentation für IBM MobileFirst Platform Foundation V8.0.0 ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}
*	[IBM MobileFirst Platform Developer Center ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://mobilefirstplatform.ibmcloud.com){: new_window}
