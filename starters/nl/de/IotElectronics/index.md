---

copyright:
  years: 2016

---

{:new_window: target="_blank"}

{:shortdesc: .shortdesc}


# Apps mit dem {{site.data.keyword.iotelectronics}}-Starter erstellen
*Letzte Aktualisierung: 14. Juni 2016*

Bei {{site.data.keyword.iotelectronics_full}} handelt es sich um eine integrierte End-to-End-Lösung, die es Ihren Apps ermöglicht, mit verbundenen Appliances zu kommunizieren und diese zu steuern, zu analyiseren und zu aktualisieren. Der Starter beinhaltet eine Starter-App, mit der Sie simulierte Appliances erstellen und steuern können, sowie ein Beispiel einer mobilen App, mit dem Sie diese Appliances über Ihr Mobilgerät steuern können.
{:shortdesc}

**Voraussetzung**:  
Stellen Sie sicher, dass Sie den {{site.data.keyword.iotelectronics}}-Starter über den Abschnitt 'Boilerplates' im Bluemix-Katalog bereitgestellt haben. Dabei werden die Komponentenanwendungen und Services des Starters einschließlich {{site.data.keyword.amafull}} automatisch bereitgestellt.

Führen Sie die in den folgenden Abschnitten enthaltenen Tasks wie beschrieben aus, um mit der Nutzung von {{site.data.keyword.iotelectronics}} zu beginnen:

1. Ermöglichen Sie die Kommunikation mit dem Beispiel für eine mobile App, indem Sie {{site.data.keyword.amashort}} konfigurieren.
2. Erstellen Sie mithilfe der {{site.data.keyword.iotelectronics}}-Starter-Webanwendung simulierte Appliances.
3. Installieren Sie das Beispiel für eine mobile App und stellen Sie eine Verbindung zu dieser Beispiel-App her.

## {{site.data.keyword.amashort}} konfigurieren
{: #configureMCA}
Für die Verwendung der mobilen App müssen Sie {{site.data.keyword.amashort}} wie folgt konfigurieren:
1. Öffnen Sie in Ihrem {{site.data.keyword.Bluemix_notm}}-Dashboard folgende Seite: [{{site.data.keyword.amashort}}](https://new-console.ng.bluemix.net/docs/services/mobileaccess/overview.html).
2. Klicken Sie im Abschnitt **Angepasst** auf **Konfigurieren**.
3. Geben Sie die folgenden Authentifizierungsnachweise ein:
  - **Realmname**: myRealm.
  - **URL**: https://<*myIoT4eStarterApp*>.mybluemix.net  

    **Tipp:** Stellen Sie sicher, dass Sie in der URL das Präfix für sichere Verbindungen `https://` verwenden. Sie finden die URL Ihrer Starter-App durch Klicken auf **Mobile Optionen** heraus.)
4. Speichern Sie alles.

  Ausführliche Anweisungen finden Sie in [{{site.data.keyword.amashort}} konfigurieren](iotelectronics_config_mobile.html#iot4e_configureMCA)

##Simulierte Appliances erstellen
Führen Sie die folgenden Schritte aus, um eine simulierte Appliance zu erstellen:
1. Starten Sie in Ihrem {{site.data.keyword.Bluemix_notm}}-Dashboard Ihre {{site.data.keyword.iotelectronics}}-Anwendung.
2. Warten Sie, bis die Statusnachricht `Ihre App ist aktiv` angezeigt wird, und klicken Sie anschließend auf **App anzeigen**, um die Starter-App anzuzeigen.  
3. Wählen Sie **Verbundene Appliances über Fernzugriff steuern** aus.
4. Blättern Sie bis zu dem Abschnitt mit dem Titel **Wählen Sie nun eine simulierte Waschmaschine aus oder erstellen Sie eine neue Waschmaschine** und klicken Sie auf die Schaltfläche zum Hinzufügen (+). Es wird eine neue Waschmaschine erstellt.

## Beispiel für mobile App installieren und eine Verbindung zu dieser Beispiel-App herstellen
Gehen Sie wie folgt vor, um das Beispiel für eine mobile App zu installieren und eine Verbindung zu dieser Beispiel-App herzustellen:

*Anmerkung*: Für die Verwendung des Beispiels für eine mobile App müssen Sie ein iOS-Gerät haben.

1. Öffnen Sie den App-Store auf Ihrem Telefon und suchen Sie nach `ibm iot`. Wählen Sie **IBM IoT for Electronics** aus und nehmen Sie die Installation vor.
2. Stellen Sie eine Verbindung zwischen Ihrem Telefon und Ihrer Organisation her, indem Sie den QR-Code für die Verbindung scannen, der in Ihrer Starter-App ermittelt wurde.
3. Stellen Sie eine Verbindung zu Ihrer simulierten Appliance her, indem Sie den QR-Code für die Appliance scannen, der in Ihrer Starter-App ermittelt wurde.

  Ausführliche Anweisungen finden Sie in [Verbindung zwischen mobiler App und eigener {{site.data.keyword.iotelectronics}}-Umgebung herstellen](iotelectronics_config_mobile.html#iot4e_connecting_mobile).

##Weitere Schritte
Hier finden Sie Informationen dazu, wie Sie {{site.data.keyword.iotelectronics}} einsetzen können.

- Erkunden Sie die Starter-App, um einen Eindruck davon zu bekommen, wie ein EM (Enterprise Manufacturer) Appliances überwachen kann, die mit der {{site.data.keyword.iot_short_notm}} verbunden sind.
- Erkunden Sie das Beispiel für eine mobile App, um einen Eindruck davon zu bekommen, wie Appliance-Eigner ihre Appliances registrieren und mit diesen interagieren können.
- Sie können manuell einen Gerätefehler kreieren, um Alerts, Benachrichtigungen und Aktionen auszulösen, die sich sowohl an den Hersteller als auch an den Appliance-Eigner richten.
- Sie können eine Zuordnung zwischen operativen Daten und Benutzerdaten herstellen, um einen Einblick in die Funktionsweise Ihrer Produkte und Geräte zu erhalten und um zu wissen, wer mit diesen arbeitet.


# Zugehörige Links
{: #rellinks}
## API-Dokumentation
{: #api}
* [{{site.data.keyword.iotelectronics}}](http://ibmiotforelectronics.mybluemix.net/public/iot4eregistrationapi.html)
* [{{site.data.keyword.iotrtinsights_short}}](https://iotrti-prod.mam.ibmserviceengage.com/apidoc/)  
* [{{site.data.keyword.iot_short}}](https://developer.ibm.com/iotfoundation/recipes/api-documentation/)


## Komponenten
{: #general}

* [{{site.data.keyword.iotelectronics_full}}-Dokumentation](iotelectronics_overview.html)
* [{{site.data.keyword.iot_full}}](https://new-console.ng.bluemix.net/docs/services/IoT/index.html)
* [{{site.data.keyword.iotrtinsights_full}}](https://new-console.ng.bluemix.net/docs/services/iotrtinsights/iotrtinsights_overview.html)
* [{{site.data.keyword.amafull}}](https://new-console.ng.bluemix.net/docs/services/mobileaccess/overview.html)
* [{{site.data.keyword.sdk4nodefull}}](https://new-console.ng.bluemix.net/docs/runtimes/nodejs/index.html#nodejs_runtime)

## Beispiele
{: #samples}
* [Beispiel für mobile App](https://new-console.ng.bluemix.net/docs/starters/IotElectronics/iotelectronics_config_mobile.html)
