---

copyright:
  years: 2016

---

{:new_window: target="_blank"}

{:shortdesc: .shortdesc}


# Apps mit Starter für {{site.data.keyword.iotelectronics}} erstellen
*Letzte Aktualisierung: 14. Juni 2016*
{: .last-updated}

{{site.data.keyword.iotelectronics_full}} ist eine integrierte End-to-End-Lösung, die es Apps ermöglicht, mit verbundenen Appliances zu kommunizieren sowie diese zu steuern, zu analysieren und zu aktualisieren. Der Starter umfasst eine Starter-App, mit dem Sie simulierte Appliances und eine mobile Beispielapp erstellen und steuern können, mit den Sie diese Appliances von dem mobilen Geräte steuern können.
{:shortdesc}

**Voraussetzung**:   
Stellen Sie sicher, dass Sie den Starter für {{site.data.keyword.iotelectronics}} im Abschnitt 'Boilerplates' des Bluemix-Katalogs bereitgestellt haben. Auf diese Art werden automatisch die Komponentenanwendungen und Services des Starters einschließlich {{site.data.keyword.amafull}} bereitgestellt. 

Führen Sie für den Einstieg in {{site.data.keyword.iotelectronics}} die folgenden Tasks wie in den folgenden Abschnitten beschrieben aus: 

1. Aktivieren Sie die Kommunikation mit der mobilen Beispielanwendung durch die Konfiguration von {{site.data.keyword.amashort}}. 
2. Erstellen Sie mit der Starterwebanwendung für {{site.data.keyword.iotelectronics}} simulierte Appliances. 
3. Installieren Sie die mobile Beispielanwendung und stellen Sie eine Verbindung her. 

## {{site.data.keyword.amashort}} konfigurieren
{: #configureMCA}
Damit Sie die mobile App verwenden können, müssen Sie {{site.data.keyword.amashort}} wie folgt konfigurieren: 
1. Öffnen Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard [{{site.data.keyword.amashort}}](https://new-console.ng.bluemix.net/docs/services/mobileaccess/overview.html). 
2. Wählen Sie im Abschnitt **Angepasst** die Option **Konfigurieren** aus. 
3. Geben Sie zur Authentifizierung die folgenden Berechtigungsnachweise ein: 
  - **Realmname**: myRealm
  - **URL**: https://<*myIoT4eStarterApp*>.mybluemix.net  

    **Tipp:** Stellen Sie sicher, dass Sie als Präfix in der URL `https://` verwenden. Die URL der Starter-App finden Sie, wenn Sie auf **Mobile Systemerweiterungen** klicken.
4. Speichern Sie die Einstellungen. 

  Detaillierte Anweisungen finden Sie unter [{{site.data.keyword.amashort}} konfigurieren](iotelectronics_config_mobile.html#iot4e_configureMCA). 

##Simulierte Appliance erstellen
Gehen Sie wie folgt vor, um eine simulierte Appliance zu erstellen: 
1. Starten Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard die {{site.data.keyword.iotelectronics}}-Anwendung. 
2. Warten Sie, bis die Statusnachricht *Ihre App ist aktiv* angezeigt wird, und klicken Sie anschließend auf **App anzeigen**, um die Starter-App anzuzeigen.   
3. Wählen Sie **Verbundene Appliances über Fernzugriff steuern** aus. 
4. Blättern Sie zum Abschnitt mit der Bezeichnung **Wählen Sie nun eine simulierte Waschmaschine aus oder erstellen Sie eine neue Waschmaschine** und klicken Sie auf die Schaltfläche zum Hinzufügen (+). Eine neue Waschmaschine wird erstellt. 

## Mobile Beispielapp installieren und Verbindung herstellen
Gehen Sie wie folgt vor, um eine mobile Beispielapp zu installieren und eine Verbindung zu ihr herzustellen: 

*Hinweis*: Sie müssen über ein iOS-Gerät verfügen, um die mobile Beispielapp verwenden zu können. 

1. Öffnen Sie im Telefon den App Store und suchen Sie nach `ibm iot`. Wählen Sie **IBM IoT for Electronics** aus und installieren Sie diese App. 
2. Verbinden Sie Ihr Telefon durch Scannen des QR-Codes für die Verbindung in der Starter-App mit Ihrer Organisation. 
3. Verbinden Sie die simulierte Appliance durch Scannen des QR-Codes für die Appliance in der Starter-App. 

  Detaillierte Anweisungen hierzu finden Sie in [Mobile App mit {{site.data.keyword.iotelectronics}}-Umgebung verbinden](iotelectronics_config_mobile.html#iot4e_connecting_mobile). 

##Weitere Schritte
Weitere Informationen zu den Möglichkeiten, die {{site.data.keyword.iotelectronics}} bietet. 

- Erfahren Sie anhand der Starter-App, wie ein Produktionsunternehmen Appliances überwachen kann, die mit {{site.data.keyword.iot_short_notm}} verbunden sind. 
- Erfahren Sie anhand der mobilen Beispielapp, wie sich Applianceeigner registrieren und mit ihren Appliances interagieren können. 
- Verursachen Sie manuell einen Geräteausfall, um Alerts, Benachrichtigungen und Aktionen auszulösen, deren Empfänger sowohl der Hersteller als auch der Applianceeigner sind. 
- Ordnen Sie Betriebsdaten Benutzerdaten zu, um zu verstehen, wie Produkte und Geräte funktionieren und wer sie bedient. 


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
