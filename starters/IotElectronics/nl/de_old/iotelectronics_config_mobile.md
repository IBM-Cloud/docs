---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-15"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Mobile App verwenden
{: #iot4e_using_mobile}

Anhand der ersten Schritte mit der mobilen {{site.data.keyword.iotelectronics_full}}-App erfahren Sie, wie über Ihr Mobilgerät wie Smartphone oder Tablet Alerts empfangen, Befehle gesendet und der Status Ihrer verbundenen Appliances angezeigt werden.
{:shortdesc}

Bevor Sie die mobile App verwenden können, müssen Sie eine Instanz des {{site.data.keyword.iotelectronics}}-Starters in Ihrer {{site.data.keyword.Bluemix_notm}}-Organisation bereitstellen. Durch die Bereitstellung einer Instanz des Starters werden die Komponentenanwendungen und Services des Starters automatisch bereitgestellt.

Führen Sie die folgenden Tasks aus, um mit der Nutzung der mobilen App zu beginnen:
1. [Mobile App](#iot4e_downloadmobile) auf eigenes Mobilgerät herunterladen.
2. [Verbindung zwischen der mobilen App und der {{site.data.keyword.iotelectronics}}-Umgebung herstellen](#iot4e_connecting_mobile) und eigene Appliances registrieren.


## Mobile App herunterladen
{: #iot4e_downloadmobile}
Sie können die mobile App für iOS- oder Android-Mobilgeräte abrufen.
- **iOS-Geräte** - Laden Sie die App vom Apple App Store herunter.  Öffnen Sie den App-Store auf Ihrem Mobilgerät und suchen Sie nach "ibm iot". Wählen Sie **IBM IoT for Electronics** aus und nehmen Sie die Installation vor.  Alternativ dazu können Sie die App mithilfe von [iTunes](https://itunes.apple.com/de/app/ibm-iot-for-electronics/id1103404928?ls=1&mt=8) auf Ihrem Mobilgerät installieren.
- **Android-Geräte** - Laden Sie die App vom Google Play Store herunter. Öffnen Sie den App-Store auf Ihrem Mobilgerät und suchen Sie nach "ibm iot". Wählen Sie **IBM IoT for Electronics** aus und nehmen Sie die Installation vor.

## Mobile App verbinden
{: #iot4e_connecting_mobile}

Führen Sie die folgenden Tasks aus, um eine Verbindung zwischen der mobilen App und Ihrer Umgebung herzustellen und Ihre Appliances zu registrieren:

1. Öffnen Sie Ihre {{site.data.keyword.iotelectronics}}-Starter-App. Anweisungen hierzu finden Sie im Thema zum [Öffnen der Starter-App](iot4ecreatingappliances.html#iot4e_openAppMain).

2. Wählen Sie **Verbundene Appliances über Fernzugriff steuern** aus.

    ![{{site.data.keyword.iotelectronics}} Starter Experience](images/IoT4E_remotely_option.svg "{{site.data.keyword.iotelectronics}} Starter Experience")

3. Blättern Sie bis zu dem Abschnitt mit dem Titel **Wählen Sie nun eine simulierte Waschmaschine aus oder erstellen Sie eine neue Waschmaschine** und klicken Sie auf das Plussymbol, um eine oder mehrere Waschmaschinen zu erstellen. Es wird eine neue Waschmaschine erstellt.

    ![Waschmaschine hinzufügen](images/IoT4E_add_washer.svg "Waschmaschine hinzufügen")

4.	Blättern Sie zum QR-Code für die Verbindung und scannen Sie ihn mithilfe Ihres Mobilgeräts. Der QR-Code für die Verbindung befindet sich im Abschnitt **Zur Herstellung einer Verbindung von der App zur Umgebung werden Sie dazu aufgefordert, diesen QR-Code zu scannen**.

  ![QR-Code für die Verbindung.](images/iot4e_mobile_connect_QR.svg "{{site.data.keyword.iotelectronics}} - QR-Code für die Verbindung")

5. Geben Sie auf Ihrem Mobilgerät die Anmeldeberechtigungsnachweise ein. Ihre Benutzer-ID und Ihr Kennwort können eine beliebige Länge haben. Merken Sie sich Ihre Anmeldeberechtigungsnachweise für zukünftige Sitzungen. Ihr Mobilgerät ist nun in Ihrer {{site.data.keyword.iotelectronics}}-Umgebung registriert und Sie können einzelne Appliances registrieren.

6. Blättern Sie auf Ihrem Computer zu einer simulierten Waschmaschine und klicken Sie darauf, um die Daten und den Appliance-QR-Code dieser Waschmaschine anzuzeigen.

  ![Wählen Sie eine Waschmaschine aus.](images/IoT4E_mobile_washer_QR.svg "Waschmaschine auswählen.")

7.	Verwenden Sie Ihr Mobilgerät, um den QR-Code der Waschmaschine zu scannen. Die Waschmaschine ist nun registriert und der Status der Waschmaschine wird auf Ihrem Mobilgerät angezeigt.

**Weitere Schritte**
Sie können jetzt Alerts anzeigen und die Waschmaschine mithilfe Ihres Mobilgeräts steuern. Probieren Sie es durch Ausführen der folgenden Schritte aus:
  - Wählen Sie auf Ihrem Computer ein Problem mit der Waschmaschine aus, z. B. 'Boardfehler' oder 'Starke Vibrationen'. Durch das Problem wird ein Alert an Ihr Mobilgerät gesendet.
  - Klicken Sie auf Ihren Mobilgerät auf die Option zum Starten des Waschvorgangs, um die Maschine zu starten. Sie können auf Ihrem Computer sehen, wie sich der Status der Waschmaschine während des Waschvorgangs ändert.
