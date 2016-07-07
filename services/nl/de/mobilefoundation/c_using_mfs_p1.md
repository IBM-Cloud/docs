---

copyright:
  years: 2016

---

#	Developer-Plan verwenden
{: #using_mobilefoundation_p1}

*Letzte Aktualisierung: 15. Juni 2016*
{: .last-updated}

Stimmen Sie nach der Erstellung der {{site.data.keyword.mobilefoundation_short}}: Developer-Serviceinstanz den Lizenzbedingungen für {{site.data.keyword.mfp_full_notm}} Version 8.0 zu, um mit der Verwendung des Service zu beginnen. Nach ein paar Sekunden können Sie in {{site.data.keyword.Bluemix_notm}} auf die Seite `Übersicht` zugreifen, die Ihnen Lernprogramme und Videos bietet, die Ihnen den Einstieg in den Service {{site.data.keyword.mobilefoundation_short}} erleichtern.

## {{site.data.keyword.mobilefirst}} Server starten
{: #start_mobilefoundation_p1}
* Um den {{site.data.keyword.mfserver_short_notm}} mit den Standardeinstellungen zu starten, klicken Sie auf **Basisserver starten**.

Diese Auswahl stellt einen {{site.data.keyword.mfserver_long_notm}} mit den folgenden Einstellungen bereit:
*	1 GB Hauptspeicher und 64 GB Speicher. Diese Menge ist für Entwicklungsaktivitäten und kleinere Testaktivitäten
ausreichend.

*	`Benutzername` und `Kennwort` werden automatisch
für Sie generiert. Sie können darauf zugreifen, wenn der Server betriebsbereit ist.

Der Prozess der Bereitstellung wird gestartet. Dieser Prozess dauert ungefähr 10 Minuten;
in einem Nachrichtenfenster wird der Fortschritt dieser Operation angezeigt. Ist der Vorgang abgeschlossen, wird ein Dashboard mit folgenden
Informationen angezeigt:
*	Status Ihres Servers, der ausgeführt wird (Zustand, Größe, Speicher).

*	Für Sie erstellte Serverroute. Mit dieser Route können Sie Ihren mobilen Server aus dem öffentlichen Internet erreichen. Ihre mobilen Anwendungen nutzen diese Route, um auf den Server zuzugreifen.

*	Ihr persönlicher `Benutzername` und das `Kennwort` für den Zugriff auf die {{site.data.keyword.mfp_oc_short_notm}}. Das `Kennwort` wird ausgeblendet. Klicken Sie auf **Kennwort anzeigen**, um es einzublenden. 

*	Klicken Sie auf **Konsole starten**, um die {{site.data.keyword.mfp_oc_short_notm}} zu starten.


Diese Konsole wird innerhalb des Containers ausgeführt. Mit der Konsole können Sie Ihre mobilen Apps und Einheiten verwalten, Ihren Server als mobiles Back-End verwenden, Push-Benachrichtigungen senden usw.

## {{site.data.keyword.mobilefirst}} Server erneut erstellen
{: #recreate_mobilefoundation_p1}

*	Klicken Sie auf die Schaltfläche **Neu erstellen**, um den Server erneut zu erstellen.

* Diese Aktion stoppt Ihre vorhandenen Server und löscht diese. Alle Daten Ihres mobilen Servers gehen verloren. Eine neue Serverinstanz wird erstellt. Diese Aktion dauert einige Minuten.

##	Erweiterte Konfiguration einrichten
{: #using_mfs_advanced_p1}

Mit der Option **Server mit erweiterter Konfiguration starten** auf der Seite `Übersicht` können Sie einen Server mit erweiterten oder benutzerdefinierten Einstellungen erstellen. Sie können die Servereinstellungen auch aktualisieren, um Ihre Serverkonfiguration anzupassen; klicken Sie hierfür auf die Registerkarte **Konfiguration**. {{site.data.keyword.mobilefoundation_short}} bietet Ihnen Zugriff auf einige erweiterte Einstellungen.

*	Auf der Registerkarte **Topologie** können Sie die Größe des Containers auswählen. Die Standardgröße von 1 GB für den Server ist für die Entwicklung und kleinere Tests ausreichend.

  - Wählen Sie in Abhängigkeit von Ihrem Bedarf die richtige Größe für Ihren Server aus.


* **Knoten** zeigt die Anzahl der erstellten Knoten an. Dieses Feld ist nicht in {{site.data.keyword.mobilefoundation_short}}: Developer bearbeitbar. Die Anzahl der Knoten in der {{site.data.keyword.IBM_notm}} Containergruppe beträgt standardmäßig **1** im Developer-Plan.

Weitere Details finden Sie in der Dokumentation zu [{{site.data.keyword.mobilefoundation_long}} ](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}.
