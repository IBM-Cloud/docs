---

copyright:
  years: 2016

---

#	{{site.data.keyword.mobilefoundation_short}}: Professional 1 Application verwenden
{: #using_mobilefoundation_p2}


Nach der Erstellung der Serviceinstanz von {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application lesen Sie die folgende Prozedur, um die Arbeit mit dem Service zu beginnen. 

## Voraussetzungen
{: #prerequisites_p2}

Beachten Sie Folgendes, bevor Sie die Serviceinstanz von {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application konfigurieren. 
* {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application wird  nur von {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional (Unterstützung für OLTP) {{site.data.keyword.Bluemix_notm}}-Plänen unterstützt. 

* Die {{site.data.keyword.dashdbshort_notm}}-Serviceinstanz und die zugehörigen Berechtigungsnachweise sollten verfügbar sein, bevor Sie die Einstellungen Ihrer {{site.data.keyword.mobilefoundation_short}}-Serviceinstanz konfigurieren können.

**Hinweis**: Die {{site.data.keyword.dashdbshort_notm}}-Serviceinstanz kann in jedem *Bereich* innerhalb Ihrer {{site.data.keyword.Bluemix_notm}} *Organisation* vorhanden sein.  

## Die Serviceinstanz von {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application konfigurieren
{: #configure_dashdb_p2}

###  Erste Schritte
{: #firststeps_p2}

Nach der Erstellung der Serviceinstanz von {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application führen Sie folgende Schritte aus, um die Arbeit mit dem Service zu beginnen: 

* Stimmen Sie den Lizenzbedingungen für {{site.data.keyword.mfp_full_notm}} V8.0.0.0 zu.

* Geben Sie Ihre {{site.data.keyword.Bluemix_notm}}-Berechtigungsnachweise ein. Danach darf der Service Änderungen an Ihrem {{site.data.keyword.Bluemix_notm}}-Bereich vornehmen und einen {{site.data.keyword.containerlong}} erstellen, auf dem Ihr {{site.data.keyword.mobilefirst_notm}} Server gehostet wird.


### Stellen Sie eine Verbindung zur {{site.data.keyword.dashdbshort_notm}}-Serviceinstanz her. 
{: #connect_dashdb_p2}

Nachdem die Serviceinstanz {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application erstellt wurde, sehen Sie die Seite *Übersicht*, auf der Sie die Verbindungsinformationen für die Serviceinstanz {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional angeben müssen. 

* Geben Sie die {{site.data.keyword.Bluemix_notm}} **Organisation** und den **Bereich** an, in der bzw. dem die Serviceinstanz {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional vorhanden ist. 
* Wählen Sie im Dropdown-Menü den **Servicenamen** der {{site.data.keyword.dashdbshort_notm}}-Serviceinstanz aus, die Sie mit Ihrer {{site.data.keyword.mobilefoundation_short}}-Serviceinstanz verwenden möchten, falls Sie mehr als eine {{site.data.keyword.dashdbshort_notm}}-Serviceinstanz erstellt haben. 
* Wählen Sie **Berechtigungsnachweise** für die ausgewählte {{site.data.keyword.dashdbshort_notm}}-Serviceinstanz aus. 

* Klicken Sie auf **Testverbindung**, um zu überprüfen, ob Ihre {{site.data.keyword.dashdbshort_notm}} verfügbar ist. Klicken Sie dann auf **Speichern**.

**Hinweis**: Sie sind nicht in der Lage, diese {{site.data.keyword.dashdbshort_notm}}-Serviceinstanz zu ändern, die für die Verwendung durch Ihre {{site.data.keyword.mobilefoundation_short}}-Serviceinstanz konfiguriert wurde. Sie können jedoch dieselbe {{site.data.keyword.dashdbshort_notm}}-Serviceinstanz über mehrere {{site.data.keyword.mobilefoundation_short}}-Serviceinstanzen hinweg verwenden, da jede {{site.data.keyword.mobilefoundation_short}}-Serviceinstanz ihr eigenes Schema in der ausgewählten {{site.data.keyword.dashdbshort_notm}}-Serviceinstanz erstellt.

* Nach ein paar Sekunden können Sie auf die Seite *Übersicht* zugreifen, die Ihnen Lernprogramme und Videos bietet, die Ihnen den Einstieg in den Service {{site.data.keyword.mobilefoundation_short}} erleichtern. 

### {{site.data.keyword.mobilefirst}}-Server starten
{: #start_mobilefoundation_p2}

* Um den {{site.data.keyword.mfserver_short_notm}} mit den Standardeinstellungen zu starten, klicken Sie auf **Basisserver starten**.

![Basisserver starten](images/start_basic_server.png "Abbildung 1. Basisserver starten")
{: screen}
* Diese Auswahl stellt einen {{site.data.keyword.mfserver_long_notm}} mit den folgenden Einstellungen bereit: 
    -  1 GB Hauptspeicher und 64 GB Speicher. Diese Größe ist für Entwicklungs- und kleinere Testaktivitäten ausreichend. 

    -	*Benutzername* und *Kennwort* werden automatisch
für Sie generiert. Sie können darauf zugreifen, wenn der Server betriebsbereit ist.

Der Prozess der Bereitstellung Ihres Servers wird gestartet. Dieser Prozess dauert ungefähr 10 Minuten;
in einem Nachrichtenfenster wird der Fortschritt dieser Operation angezeigt. Ist der Vorgang abgeschlossen, wird ein Dashboard mit folgenden
Informationen angezeigt:

  -	Status Ihres Servers, der ausgeführt wird (Zustand, Größe, Speicher).

  -	Für Sie erstellte Serverroute. Mit dieser Route können Sie Ihren mobilen Server aus dem öffentlichen Internet
erreichen. Ihre mobilen Anwendungen nutzen diese Route, um auf den Server zuzugreifen.

  -	Ihr persönlicher *Benutzername* und das *Kennwort* für den Zugriff auf die {{site.data.keyword.mfp_oc_short_notm}}. Das *Kennwort* wird ausgeblendet. Klicken Sie auf das kleine Symbol mit dem Auge, um es anzuzeigen.

*	Klicken Sie auf **Konsole starten**, um die {{site.data.keyword.mfp_oc_short_notm}} zu öffnen.

![Konsole starten](images/launch_console.png "Abbildung 2. Konsole starten")
{: screen}

Diese Konsole wird innerhalb des Containers ausgeführt. Mit der Konsole können Sie Ihre mobilen Apps und Einheiten verwalten, Ihren Server als mobiles Back-End verwenden, Push-Benachrichtigungen senden usw. 

### Den {{site.data.keyword.mobilefirst}} Server erneut erstellen
{: #recreate_mobilefoundation_p2}

*	Klicken Sie auf die Schaltfläche **Neu erstellen**, um den Server erneut zu erstellen. 

![Neu erstellen](images/recreate.png "Abbildung 3. Neu erstellen")
{: screen}

* Diese Aktion stoppt Ihre vorhandenen Server und löscht diese. Eine neue Serverinstanz wird erstellt. Diese Aktion
dauert einige Minuten.

**Hinweis**: Alle Daten der vorherigen Serverinstanz einschließlich der Informationen zu den Apps und Adaptern sind in der konfigurierten {{site.data.keyword.dashdbshort_notm}}-Serviceinstanz dauerhaft festgelegt. 

##	Erweiterte Konfiguration einrichten
{: #using_mfs_advanced_p2}

Mit der Option **Server mit erweiterter Konfiguration starten** auf der Seite *Übersicht* können Sie einen Server mit erweiterten oder benutzerdefinierten Einstellungen erstellen. Sie können die
Servereinstellungen auch aktualisieren, um Ihre Serverkonfiguration anzupassen; klicken Sie hierfür auf die
Registerkarte **Konfiguration**. {{site.data.keyword.mobilefoundation_short}} bietet Ihnen Zugriff auf einige erweiterte Einstellungen. 

*	Auf der Registerkarte **Topologie** können Sie die Topologiegröße Ihrer Container auswählen. Die Standardgröße von 1 GB für den Server ist für die Entwicklung und kleinere Tests ausreichend. Für die Durchführung von kleineren Testaktionen benötigen Sie jedoch möglicherweise mehr Kapazität. 
  - Wählen Sie in Abhängigkeit von Ihrem Bedarf die richtige Größe für Ihren Server aus. 

  - **Knoten** zeigt die Anzahl der erstellten Knoten an. 
      - Sie können die Mindest- und Höchstanzahl der in Ihren {{site.data.keyword.IBM_notm}}-Containergruppen erforderlichen Knoten konfigurieren. Containergruppen bieten eine hohe Verfügbarkeit und Skalierbarkeit.

      - Die {{site.data.keyword.mobilefirst}}-Server-Farm kann durch die Konfiguration der Anzahl der Knoten hier unterstützt werden. 

Weitere Details finden Sie in der [{{site.data.keyword.mobilefoundation_long}} Dokumentation](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}. 
