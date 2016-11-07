---

copyright:
  years: 2016

---

{:new_window: target="\_blank"}

{:shortdesc: .shortdesc}


# Starter-App verwenden
*Letzte Aktualisierung: 15. September 2016*
{: .last-updated}

Erstellen Sie in der Starter-App für {{site.data.keyword.iotelectronics_full}} simulierte Appliances. Erfahren Sie, wie ein Produktionsunternehmen Appliances überwachen kann, die mit {{site.data.keyword.iot_short_notm}} verbunden sind. Interagieren Sie manuell mit simulierten Appliances, um Alerts, Benachrichtigungen und Aktionen auszulösen.
{:shortdesc}


## Starter-App öffnen
{: #iot4e_openAppMain}

Da der Prozess zum Öffnen der Starter-App je nach Version Ihrer {{site.data.keyword.Bluemix_notm}}-Konsole variiert, lesen Sie die Anweisungen zur entsprechenden Version.

Sie können die verwendete Version bestimmen, indem Sie nach den folgenden Optionen suchen:
  - [Neue {{site.data.keyword.Bluemix_notm}}](#iot4e_openApp)-Ansicht. Wenn Sie die neue {{site.data.keyword.Bluemix_notm}}-Ansicht verwenden, wird **Neue Bluemix-Ansicht testen** *nicht* im Abschnitt oben angezeigt.
  - [Klassische {{site.data.keyword.Bluemix_notm}}](#iot4e_openApp_c)-Ansicht. Wenn Sie die klassische {{site.data.keyword.Bluemix_notm}}-Ansicht verwenden, wird **Neue Bluemix-Ansicht testen** im Abschnitt oben angezeigt.  

**Tipp:** Um zur klassischen {{site.data.keyword.Bluemix_notm}}-Ansicht zu wechseln, klicken Sie im Abschnitt oben auf den Benutzernamen, blättern Sie nach unten und klicken Sie auf **Zu klassischer Ansicht wechseln**. Um zur neuen {{site.data.keyword.Bluemix_notm}}-Ansicht zu wechseln, klicken Sie auf **Neue Bluemix-Ansicht testen** im Abschnitt oben.

### Öffnen Sie die Starter-App in der neuen {{site.data.keyword.Bluemix_notm}}-Ansicht.
{: #iot4e_openApp}
1. Starten Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard Ihre {{site.data.keyword.iotelectronics}}-Starteranwendung, indem Sie auf die Kachel für die Starteranwendung klicken.

    ![{{site.data.keyword.iotelectronics}} im Dashboard, neue Ansicht.](images/IoT4E_bm_dashboard.png "{{site.data.keyword.iotelectronics}} im Dashboard, neue Ansicht")

2. Warten Sie, bis die Statusnachricht *Ihre App ist aktiv* im Header angezeigt wird, und klicken Sie anschließend auf **App anzeigen**, um die Starter-App anzuzeigen.   

    ![{{site.data.keyword.iotelectronics}} im Dashboard, neue Ansicht.](images/IoT4E_view_app.png "{{site.data.keyword.iotelectronics}} im Dashboard, neue Ansicht")

### Öffnen Sie die Starter-App in der klassischen {{site.data.keyword.Bluemix_notm}}-Ansicht.
{: #iot4e_openApp_c}

1. Starten Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard Ihre {{site.data.keyword.iotelectronics}}-Starteranwendung, indem Sie auf die Kachel für die Starteranwendung klicken.

    ![{{site.data.keyword.iotelectronics}} im Dashboard, klassische Ansicht.](images/IoT4E_bm_dashboard_c.png "{{site.data.keyword.iotelectronics}} im Dashboard, klassische Ansicht")

2. Warten Sie, bis die Statusnachricht *Ihre App ist aktiv* im Abschnitt 'Anwendungsstatus' angezeigt wird, und klicken Sie im Hauptfenster beim Anwendungsnamen auf die **Routes**-URL, um die Starter-App anzuzeigen.  

    ![{{site.data.keyword.iotelectronics}} im Dashboard, klassische Ansicht.](images/IoT4E_view_app_c.png "{{site.data.keyword.iotelectronics}} im Dashboard")

## Simulierte Appliance erstellen
{: #iot4eCreateAppliances}

In der Starter-App können Sie simulierte Appliances als Appliance-Hersteller oder als Nutzer erstellen und steuern. Die Status- und Ereignisdaten für diese simulierten Appliances werden gespeichert und können in {{site.data.keyword.iot_full}} angezeigt werden.

1. Wählen Sie eine der folgenden Optionen:
    - **Verbinden und verwalten Sie simulierte Appliances**, um als Appliance-Hersteller simulierte Appliances zu erstellen.
    - **Steuern Sie Ihre verbundenen Appliances über Fernzugriff**, um als Appliance-Eigentümer simulierte Appliances zu erstellen und mit der [mobilen Beispiel-App](iotelectronics_config_mobile.html) zu verbinden.

    ![{{site.data.keyword.iotelectronics}} Starter-Erfahrung](images/IoT4E_remotely_option.png "{{site.data.keyword.iotelectronics}} Starter-Erfahrung")

2. Blättern Sie zum Abschnitt mit der Bezeichnung **Wählen Sie nun eine simulierte Waschmaschine aus oder erstellen Sie eine neue Waschmaschine** und klicken Sie auf das Symbol '+'. Eine neue Waschmaschine wird erstellt.

    ![Waschmaschine hinzufügen.](images/IoT4E_add_washer.png "Waschmaschine hinzufügen")

3. Klicken Sie auf eine Waschmaschine, um Details zur Waschmaschine, Ausgabebefehle und Fehlerursachen anzuzeigen.

  ![Waschmaschinen-Statusdetails.](images/IoT4E_washer_control.png "Waschmaschinen-Statusdetails")


# Zugehörige Links
{: #rellinks}

## API-Dokumentation
{: #api}
* [{{site.data.keyword.iotelectronics}} API](http://ibmiotforelectronics.mybluemix.net/public/iot4eregistrationapi.html)
* [{{site.data.keyword.iot_short}} API](https://developer.ibm.com/iotfoundation/recipes/api-documentation/)


## Komponenten
{: #general}

* [{{site.data.keyword.iotelectronics}}-Dokumentation](iotelectronics_overview.html)
* [{{site.data.keyword.iot_full}}-Dokumentation](https://new-console.ng.bluemix.net/docs/services/IoT/index.html)
*  [{{site.data.keyword.amashort}}-Dokumentation](https://new-console.ng.bluemix.net/docs/services/mobileaccess/overview.html)
* [{{site.data.keyword.sdk4nodefull}}-Dokumentation](https://new-console.ng.bluemix.net/docs/runtimes/nodejs/index.html#nodejs_runtime)

## Beispiele
{: #samples}
* [Beispiel für mobile App](https://new-console.ng.bluemix.net/docs/starters/IotElectronics/iotelectronics_config_mobile.html)
