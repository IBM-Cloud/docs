---

copyright:
  years: 2016

---

#	Professional 1 Application-Plan verwenden
{: #using_mobilefoundation_p2}

Letzte Aktualisierung: 04. August 2016
{: .last-updated}

Mit dem Professional 1 Application-Plan können Benutzer 1 mobile Anwendung mit mehreren Betriebssystemen für mobile Geräte erstellen.
Nach der Erstellung der Serviceinstanz von {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application lesen Sie die folgende Prozedur, um die Arbeit mit dem Service zu beginnen.

## Voraussetzungen
{: #prerequisites_p2}

Beachten Sie Folgendes, bevor Sie die Serviceinstanz von {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application konfigurieren.
* {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application wird  nur von {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional (Unterstützung für OLTP) {{site.data.keyword.Bluemix_notm}}-Plänen unterstützt.

* Sie benötigen Zugriff auf die Berechtigungsnachweise der {{site.data.keyword.dashdbshort_notm}}-Serviceinstanz, bevor Sie die Einstellungen für die {{site.data.keyword.mobilefoundation_short}}-Serviceinstanz konfigurieren.

**Hinweis**: Die {{site.data.keyword.dashdbshort_notm}}-Serviceinstanz kann sich in jedem `Bereich` in Ihrer {{site.data.keyword.Bluemix_notm}}-`Organisation` bzw. in jeder anderen `Organisation`, auf die Sie zugreifen können, befinden. Stellen Sie sicher, dass Sie über die Berechtigungen für den Zugriff auf den `Bereich` verfügen, in dem sich die {{site.data.keyword.dashdbshort_notm}}-Serviceinstanz befindet.


## Datenbankverbindung hinzufügen
{: #configure_dashdb_p2}

###  Erste Schritte
{: #firststeps_p2}

Führen Sie nach der Erstellung der Serviceinstanz von {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application die nachfolgend beschriebene Prozedur aus, um mit der Verwendung des Service zu beginnen.

### Stellen Sie eine Verbindung zur {{site.data.keyword.dashdbshort_notm}}-Serviceinstanz her.
{: #connect_dashdb_p2}

Nachdem die Serviceinstanz {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application erstellt wurde, sehen Sie die Seite *Übersicht*, auf der Sie die Verbindungsinformationen für die Serviceinstanz {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional angeben müssen.

1. Wählen Sie die {{site.data.keyword.Bluemix_notm}} `Organisation` aus, in der sich die {{site.data.keyword.dashdbshort_notm}}-Serviceinstanz befindet.

+ Wählen Sie den {{site.data.keyword.Bluemix_notm}}-`Bereich`, in dem sich die {{site.data.keyword.dashdbshort_notm}}-Serviceinstanz befindet, in der Liste der Bereiche aus, die in der ausgewählten `Organisation` verfügbar sind.

**Hinweis:** Wenn die `Organisation` und der `Bereich`, in denen sich Ihre {{site.data.keyword.dashdbshort_notm}}-Serviceinstanz befindet, nicht aufgeführt sind, prüfen Sie, ob Sie ein Mitglied der betreffenden `Organisation` bzw. des betreffenden `Bereichs` sind.

+ Wählen Sie den `Servicenamen` und die `Berechtigungsnachweise` für {{site.data.keyword.dashdbshort_notm}} aus, um eine Verbindung zur vorhandenen {{site.data.keyword.dashdbshort_notm}}-Serviceinstanz herzustellen.

+  Testen Sie die Verbindung zur angegebenen {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional-Serviceinstanz.

+  Klicken Sie auf **Weiter**. Mit dieser Aktion werden die erforderlichen Tabellen in der konfigurierten {{site.data.keyword.dashdbshort_notm}}-Datenbankserviceinstanz erstellt.

**Hinweis**: Sie können die {{site.data.keyword.dashdbshort_notm}}-Serviceinstanz, die zur Verwendung durch die {{site.data.keyword.mobilefoundation_short}}-Serviceinstanz konfiguriert ist, nicht ändern. Sie können jedoch dieselbe {{site.data.keyword.dashdbshort_notm}}-Serviceinstanz für mehrere {{site.data.keyword.mobilefoundation_short}}-Serviceinstanzen verwenden, da jede {{site.data.keyword.mobilefoundation_short}}-Serviceinstanz ein eigenes Schema in der ausgewählten {{site.data.keyword.dashdbshort_notm}}-Serviceinstanz erstellt.

* Nach einigen Sekunden können Sie auf die Seite `Übersicht` zugreifen, auf der die Lernprogramme und Videos zur Verfügung stehen, die Sie beim Einstieg in die Verwendung des {{site.data.keyword.mobilefoundation_short}}-Service unterstützten.

## {{site.data.keyword.mobilefirst}}-Server starten
{: #start_mobilefoundation_p2}

* Um den {{site.data.keyword.mfserver_short_notm}} mit den Standardeinstellungen zu starten, klicken Sie auf **Basisserver starten**.

* Diese Auswahl stellt einen {{site.data.keyword.mfserver_long_notm}} mit den folgenden Einstellungen bereit:
    -  1 GB Hauptspeicher. Diese Größe ist für Entwicklungs- und kleinere Testaktivitäten sowie für kleinere Produktionsworkloads ausreichend.

    -	`Benutzername` und `Kennwort` werden automatisch
für Sie generiert. Sie können darauf zugreifen, wenn der Server betriebsbereit ist.

Der Prozess der Bereitstellung Ihres Servers wird gestartet. Dieser Prozess dauert ungefähr 10 Minuten;
in einem Nachrichtenfenster wird der Fortschritt dieser Operation angezeigt. Ist der Vorgang abgeschlossen, wird ein Dashboard mit folgenden
Informationen angezeigt:

  -	Status Ihres Servers, der ausgeführt wird (Zustand, Größe).

  -	Für Sie erstellte Serverroute. Verwenden Sie diese Route in Ihrer mobilen Anwendung, um eine Verbindung zum {{site.data.keyword.mfserver_short_notm}} herzustellen.

  -	Ihr persönlicher `Benutzername` und das `Kennwort` für den Zugriff auf die {{site.data.keyword.mfp_oc_short_notm}}. Das `Kennwort` wird ausgeblendet. Klicken Sie auf das Symbol **Kennwort anzeigen**, um es einzublenden.

*	Klicken Sie auf **Konsole starten**, um die {{site.data.keyword.mfp_oc_short_notm}} zu öffnen.


<!--This console runs inside the container.--> Mit der Konsole können Sie Ihre mobilen Apps, Adapter und Geräte verwalten, Ihren Server als mobiles Back-End verwenden, Push-Benachrichtigungen senden usw.

## {{site.data.keyword.mobilefirst}} Server erneut erstellen
{: #recreate_mobilefoundation_p2}

*	Klicken Sie auf die Schaltfläche **Neu erstellen**, um den Server erneut zu erstellen.

* Diese Aktion stoppt Ihre vorhandenen Server und löscht die Daten. Eine neue Serverinstanz wird mit einer aktualisierten Version erstellt, falls verfügbar. Diese Aktion nimmt einige Minuten in Anspruch.

**Hinweis**: Alle Daten der vorherigen Serverinstanz, einschließlich Informationen zu den Apps und Adaptern, werden in der konfigurierten {{site.data.keyword.dashdbshort_notm}}-Serviceinstanz beibehalten; diese Daten werden zur erneuten Erstellung des Servers verwendet.

##	Erweiterte Konfiguration einrichten
{: #using_mfs_advanced_p2}

Mit der Option **Server mit erweiterter Konfiguration starten** auf der Seite `Übersicht` können Sie einen Server mit erweiterten oder benutzerdefinierten Einstellungen erstellen. Sie können die
Servereinstellungen auch aktualisieren, um Ihre Serverkonfiguration anzupassen; klicken Sie hierfür auf die
Registerkarte **Konfiguration**. {{site.data.keyword.mobilefoundation_short}} bietet Ihnen Zugriff auf einige erweiterte Einstellungen.

*	Auf der Registerkarte **Topologie** können Sie die Servergröße und die Anzahl der Serverinstanzen auswählen, die den jeweiligen Anforderungen entsprechen. Die Standardgröße von 1 GB für den Server ist für die Entwicklung und kleinere Tests ausreichend.
  - Wählen Sie in Abhängigkeit von Ihrem Bedarf die richtige Größe für Ihren Server aus.

  - **Knoten** zeigt die Anzahl der erstellten Knoten an.

      - Die {{site.data.keyword.mobilefirst}}-Server-Farm kann durch die Konfiguration der Anzahl der Knoten hier unterstützt werden.

Weitere Details finden Sie in der [{{site.data.keyword.mobilefoundation_long}}-Dokumentation](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}.
