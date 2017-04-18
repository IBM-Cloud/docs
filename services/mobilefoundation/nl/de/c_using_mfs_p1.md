---

copyright:
  years: 2016, 2017
lastupdated:  "2017-02-17"

---

#	Developer-Plan verwenden
{: #using_mobilefoundation_p1}

Einige Sekunden nach der Erstellung der Serviceinstanz von {{site.data.keyword.mobilefoundation_short}}: Developer können Sie auf die Seite `Übersicht` in {{site.data.keyword.Bluemix_notm}} zugreifen. Dort stehen Lernprogramme und Videos zum Einstieg in die Verwendung des {{site.data.keyword.mobilefoundation_short}}-Service zur Verfügung.

## MobileFirst-Server starten
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

##  Mobile Analytics-Server hinzufügen
{: #adding_analytics_server_dev}

 Sie können Ihre mobile Anwendung nun auf dem {{site.data.keyword.mobilefirst}}-Server überwachen, indem Sie einen Mobile Analytics-Server zur Instanz des Service {{site.data.keyword.mobilefoundation_short}} hinzufügen. Durch den Entwicklerplan wird der Mobile Analytics-Server in einer Containergruppe mit einem einzigen Knoten und 1 GB Speicherplatz erstellt.

* Klicken Sie auf die Option zum Hinzufügen der Analyse, um den Mobile Analytics-Server zur Instanz des {{site.data.keyword.mobilefoundation_short}}-Service hinzuzufügen.

Der Prozess der Bereitstellung wird gestartet. Dieser Prozess dauert ungefähr 10 Minuten; in einem Nachrichtenfenster wird der Fortschritt dieser Operation angezeigt.  

* Starten Sie die MobileFirst Analytics Console über die {{site.data.keyword.mfp_oc_short_notm}}.

* Für den {{site.data.keyword.mfserver_short_notm}} und den Mobile Analytics-Server ist Single Sign-on aktiviert. Der Mobile Analytics-Server ist mit denselben LTPA-Schlüsseln und denselben Benutzerberechtigungen konfiguriert wie der {{site.data.keyword.mfserver_short_notm}}. Sie können für die Anmeldung an der Mobile Analytics Console den `Benutzernamen` und das `Kennwort` verwenden, die Sie auch für die Anmeldung bei der {{site.data.keyword.mfp_oc_short_notm}} verwendet haben.

Weitere Informationen zu MobileFirst Analytics finden Sie unter [MobileFirst Foundation Operational Analytics ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/analytics/){: new_window}.

**Anmerkung:** Der Mobile Analytics-Server wird entfernt, wenn Sie die Instanz des Service {{site.data.keyword.mobilefoundation_short}} löschen oder wenn Sie versuchen, den {{site.data.keyword.mfserver_short_notm}} erneut zu erstellen.

##  Mobile Analytics-Server löschen
{: #deleting_analytics_server_dev}

Sie können jetzt den Mobile Analytics-Server, der zur {{site.data.keyword.mobilefoundation_short}}-Serviceinstanz hinzugefügt wurde, im {{site.data.keyword.mobilefoundation_short}}-Service-Dashboard löschen.

* Klicken Sie auf die Option zum Löschen der Analyse****, um den Mobile Analytics-Server zu löschen, der zur {{site.data.keyword.mobilefoundation_short}}-Serviceinstanz hinzugefügt wurde.

 Bei dieser Aktion wird die Analytics-Containergruppe gelöscht. Das Löschen der Analytics-Container dauert ca. 10 Minuten. Sie können die Anzeige aktualisieren, um den aktuellen Status anzuzeigen. Nach dem Löschen der Analysecontainer wird die Schaltfläche zum Hinzufügen der Analyse**** wieder aktiviert und kann verwendet werden, um den Mobile Analytics-Server bei Bedarf erneut hinzuzufügen.


## MobileFirst-Server erneut erstellen
{: #recreate_mobilefoundation_p1}

*	Klicken Sie auf die Schaltfläche **Neu erstellen**, um den Server erneut zu erstellen.

* Diese Aktion stoppt Ihre vorhandenen Server und löscht die Daten. Alle Daten Ihres mobilen Servers gehen verloren. Eine neue Serverinstanz wird mit einer aktualisierten Version erstellt, falls verfügbar. Diese Aktion dauert einige Minuten.

##	Erweiterte Konfiguration einrichten
{: #using_mfs_advanced_p1}

Mit der Option **Server mit erweiterter Konfiguration starten** auf der Seite `Übersicht` können Sie einen Server mit erweiterten oder benutzerdefinierten Einstellungen erstellen. Sie können die Servereinstellungen auch aktualisieren, um Ihre Serverkonfiguration anzupassen; klicken Sie hierfür auf die Registerkarte **Konfiguration**. {{site.data.keyword.mobilefoundation_short}} bietet Ihnen Zugriff auf einige erweiterte Einstellungen.

*	Auf der Registerkarte **Topologie** können Sie die Servergröße und die Anzahl der Instanzen auswählen, die den jeweiligen Anforderungen entsprechen. Die Standardgröße von 1 GB für den Server ist für die Entwicklung und kleinere Tests ausreichend.

  - Wählen Sie in Abhängigkeit von Ihrem Bedarf die richtige Größe für Ihren Server aus.

* **Knoten** zeigt die Anzahl der erstellten Knoten an. Dieses Feld ist nicht in {{site.data.keyword.mobilefoundation_short}}: Developer bearbeitbar. Die Anzahl der Knoten <!--in your {{site.data.keyword.IBM_notm}} container group--> beträgt standardmäßig **1** im Developer-Plan.

Weitere Details finden Sie in der [{{site.data.keyword.mobilefoundation_long}}-Dokumentation ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}.
