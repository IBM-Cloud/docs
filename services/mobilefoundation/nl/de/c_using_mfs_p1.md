---

copyright:
  years: 2016

---

#	Developer-Plan verwenden
{: #using_mobilefoundation_p1}

Letzte Aktualisierung: 04. August 2016
{: .last-updated}

Einige Sekunden nach der Erstellung der Serviceinstanz von {{site.data.keyword.mobilefoundation_short}}: Developer können Sie auf die Seite `Übersicht` in {{site.data.keyword.Bluemix_notm}} zugreifen. Dort stehen Lernprogramme und Videos zum Einstieg in die Verwendung des {{site.data.keyword.mobilefoundation_short}}-Service zur Verfügung.

## {{site.data.keyword.mobilefirst}} Server starten
{: #start_mobilefoundation_p1}
* Um den {{site.data.keyword.mfserver_short_notm}} mit den Standardeinstellungen zu starten, klicken Sie auf **Basisserver starten**.

Diese Auswahl stellt einen {{site.data.keyword.mfserver_long_notm}} mit den folgenden Einstellungen bereit:
*	1 GB Hauptspeicher. Diese Größe ist für Entwicklungs- und kleinere Testaktivitäten sowie für kleinere Produktionsworkloads ausreichend.

*	`Benutzername` und `Kennwort` werden automatisch für Sie generiert. Sie können darauf zugreifen, wenn der Server betriebsbereit ist.

Der Prozess der Bereitstellung wird gestartet. Dieser Prozess dauert ungefähr 10 Minuten; in einem Nachrichtenfenster wird der Fortschritt dieser Operation angezeigt. Ist der Vorgang abgeschlossen, wird ein Dashboard mit folgenden Informationen angezeigt:
*	Status Ihres Servers, der ausgeführt wird (Zustand, Größe).

*	Für Sie erstellte Serverroute. Verwenden Sie diese Route in Ihrer mobilen Anwendung, um eine Verbindung zum {{site.data.keyword.mfserver_short_notm}} herzustellen.

*	Ihr persönlicher `Benutzername` und das `Kennwort` für den Zugriff auf die {{site.data.keyword.mfp_oc_short_notm}}. Das `Kennwort` wird ausgeblendet. Klicken Sie auf das Symbol **Kennwort anzeigen**, um es einzublenden.

*	Klicken Sie auf **Konsole starten**, um die {{site.data.keyword.mfp_oc_short_notm}} zu starten.


<!--This console runs inside the container.--> Mit der Konsole können Sie Ihre mobilen Apps und Geräte verwalten, Ihren Server als mobiles Back-End verwenden, Push-Benachrichtigungen senden usw.

## {{site.data.keyword.mobilefirst}} Server erneut erstellen
{: #recreate_mobilefoundation_p1}

*	Klicken Sie auf die Schaltfläche **Neu erstellen**, um den Server erneut zu erstellen.

* Diese Aktion stoppt Ihre vorhandenen Server und löscht die Daten. Alle Daten Ihres mobilen Servers gehen verloren. Eine neue Serverinstanz wird mit einer aktualisierten Version erstellt, falls verfügbar. Diese Aktion dauert einige Minuten.

##	Erweiterte Konfiguration einrichten
{: #using_mfs_advanced_p1}

Mit der Option **Server mit erweiterter Konfiguration starten** auf der Seite `Übersicht` können Sie einen Server mit erweiterten oder benutzerdefinierten Einstellungen erstellen. Sie können die Servereinstellungen auch aktualisieren, um Ihre Serverkonfiguration anzupassen; klicken Sie hierfür auf die Registerkarte **Konfiguration**. {{site.data.keyword.mobilefoundation_short}} bietet Ihnen Zugriff auf einige erweiterte Einstellungen.

*	Auf der Registerkarte **Topologie** können Sie die Servergröße und die Anzahl der Instanzen auswählen, die den jeweiligen Anforderungen entsprechen. Die Standardgröße von 1 GB für den Server ist für die Entwicklung und kleinere Tests ausreichend.

  - Wählen Sie in Abhängigkeit von Ihrem Bedarf die richtige Größe für Ihren Server aus.

* **Knoten** zeigt die Anzahl der erstellten Knoten an. Dieses Feld ist nicht in {{site.data.keyword.mobilefoundation_short}}: Developer bearbeitbar. Die Anzahl der Knoten <!--in your {{site.data.keyword.IBM_notm}} container group--> beträgt standardmäßig **1** im Developer-Plan.

Weitere Details finden Sie in der Dokumentation zu [{{site.data.keyword.mobilefoundation_long}} ](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}.
