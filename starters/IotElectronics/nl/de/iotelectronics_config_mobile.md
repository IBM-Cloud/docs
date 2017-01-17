---

copyright:
  years: 2016

---


<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Mobile App verwenden
{: #iot4e_using_mobile}
*Letzte Aktualisierung: 19. September 2016*
{: .last-updated}

Beginnen Sie mit der mobilen App von {{site.data.keyword.iotelectronics_full}}, um zu lernen, wie Sie Alerts empfangen, Befehle senden und den Status der verbundenen Appliances überprüfen können.
{:shortdesc}

## Vorbereitende Schritte

Bevor Sie die mobile App verwenden können, müssen Sie die folgenden Tasks durchführen:
  - Stellen Sie eine Instanz des {{site.data.keyword.iotelectronics}}-Starters in Ihrer {{site.data.keyword.Bluemix_notm}}-Organisation bereit. Mit der Bereitstellung einer Starterinstanz werden automatisch die Komponentenanwendungen und Services des Starters bereitgestellt.
  - [Aktivieren Sie die mobile Kommunikation und Sicherheit](iotelectronics_config_mca.html) durch die Konfiguration von {{site.data.keyword.amafull}}.

## Erste Schritte mit der mobilen App
Führen Sie für den Einstieg in die mobile App die folgenden Tasks aus:
1. [Laden Sie die mobile App auf Ihr mobiles Gerät herunter](#iot4e_downloadmobile).
2. [Verbinden Sie die mobile App mit der {{site.data.keyword.iotelectronics}}-Umgebung](#iot4e_connecting_mobile) und registrieren Sie Ihre Appliances.


 ### Mobile Anwendung herunterladen
 {: #iot4e_downloadmobile}
 Wenn Sie die mobile App abrufen möchten, laden Sie sie vom Apple App Store herunter und installieren Sie auf Ihrem Telefon.  Öffnen Sie im Telefon den App Store und suchen Sie nach "ibm iot". Wählen Sie **IBM IoT for Electronics** aus und installieren Sie diese App.

 Alternativ können Sie sie auch über [iTunes](https://itunes.apple.com/us/app/ibm-iot-for-electronics/id1103404928?ls=1&mt=8) installieren.


### Mobile App verbinden
{: #iot4e_connecting_mobile}

Führen Sie die folgenden Schritte aus, um die mobile App mit Ihrer Umgebung zu verbinden und Ihre Appliances zu registrieren:

1. Öffnen Sie Ihre {{site.data.keyword.itoelectronics}}-Starter-App. Weitere Anweisungen finden Sie im Abschnitt [Starter-App öffnen](iot4ecreatingappliances.html#iot4e_openAppMain).

2. Wählen Sie **Verbundene Appliances über Fernzugriff steuern** aus.

    ![{{site.data.keyword.iotelectronics}} Starter-Erfahrung](images/IoT4E_remotely_option.png "{{site.data.keyword.iotelectronics}} Starter-Erfahrung")

3. Erstellen Sie eine oder mehrere Waschmaschinen, indem Sie im Abschnitt **Wählen Sie nun eine simulierte Waschmaschine aus oder erstellen Sie eine neue Waschmaschine** blättern und dann auf das Symbol '+' klicken. Eine neue Waschmaschine wird erstellt.

    ![Waschmaschine hinzufügen](images/IoT4E_add_washer.png "Waschmaschine hinzufügen")

4.	Blättern Sie zu dem QR-Code für die Verbindung und scannen Sie ihn mit dem mobilen Gerät. Der QR-Code für die Verbindung wird im Abschnitt mit der Bezeichnung **Zur Herstellung einer Verbindung von der App zur Umgebung werden Sie aufgefordert, diese QR-Code zu scannen** gesucht.

  ![QR-Code für die Verbindung.](images/iot4e_mobile_connect_QR.png "{{site.data.keyword.iotelectronics}} QR-Code für die Verbindung")

5. Geben Sie die Berechtigungsnachweise in Ihr mobiles Gerät ein. Die Benutzer-ID kann eine beliebige Länge aufweisen. Notieren Sie die Anmeldeberechtigungsnachweise für zukünftige Sitzungen. Ihr mobiles Gerät ist jetzt bei Ihrer {{site.data.keyword.iotelectronics}}-Umgebung registriert und Sie können einzelne Appliances registrieren.

6. Blättern Sie auf dem Computer zur simulierten Waschmaschine und klicken Sie auf diese, um ihre Daten und den QR-Code für die Appliance anzuzeigen.

  ![Wählen Sie eine Waschmaschine aus.](images/IoT4E_mobile_washer_QR.png "Wählen Sie eine Waschmaschine aus.")

7.	Scannen Sie mit dem mobilen Gerät den QR-Code der Waschmaschine. Die Waschmaschine ist jetzt registriert und der Status der Waschmaschine wird auf Ihrem Mobiltelefon angezeigt.

#### Weitere Schritte
Sie können jetzt Alerts anzeigen und die Waschmaschine mithilfe Ihres mobilen Geräts steuern. Versuchen Sie dies wie folgt:
  - Wählen Sie auf dem Computer ein Problem für die Waschmaschine aus, zum Beispiel einen Platinenfehler oder starke Vibrationen. Das Problem führt dazu, dass ein Alert an das Mobiltelefon gesendet wird.
  - Klicken Sie auf Ihrem mobilen Gerät auf **Waschvorgang starten**, um die Maschine zu starten. Der Status der Waschmaschine wird bei jedem Waschzyklus auf Ihrem Computer geändert.
