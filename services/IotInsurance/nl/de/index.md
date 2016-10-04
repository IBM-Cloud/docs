---

copyright:
  years: 2016

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# Einführung in {{site.data.keyword.iotinsurance_short}} (Beta)
{: #iotins_gettingstarted}
Letzte Aktualisierung: 12. September 2016
{: .last-updated}

{{site.data.keyword.iotinsurance_full}} ist ein {{site.data.keyword.Bluemix_notm}}-Service, den Sie zum Erfassen, Verwalten und Analysieren von Daten von verbundenen Versicherungsnehmern verwenden können. {{site.data.keyword.iotinsurance_short}} ermöglicht Ihnen eine personalisierte Risikobewertung, Echtzeitschutz und eine Reduzierung der Versicherungskosten.
{:shortdesc}

Um diesen Service in Betrieb zu nehmen, müssen Sie die erforderlichen Services und Apps bereitstellen und die Services anschließend konfigurieren. 

**Voraussetzungen:** Stellen Sie zunächst sicher, dass folgende Voraussetzungen erfüllt sind: 
- Eine Instanz des Service [{{site.data.keyword.iotinsurance_short}}](https://new-console.ng.bluemix.net/catalog/services/iot-for-insurance/) muss sich in Ihrem {{site.data.keyword.Bluemix_notm}}-Bereich befinden.
- Auf Ihrem Computer müssen mindestens 10 GB Speicher verfügbar sein.

## Erforderliche Services und Anwendungen bereitstellen
{: #deploying_services}

1. Um alle erforderlichen Services und Anwendungen bereitzustellen, klicken Sie im {{site.data.keyword.Bluemix_notm}}-Dashboard auf die Kachel für den Service {{site.data.keyword.iotinsurance_short}} und klicken Sie anschließend auf **Bereitstellen**. 

  {{site.data.keyword.iotinsurance_short}} stellt alle erforderlichen Services und Node.js-Anwendungen bereit. Die Anwendungen werden automatisch an die Services gebunden. 

  Jede Serviceinstanz verwendet den Standardserviceplan. Sie können für jeden Serviceplan zu einem späteren Zeitpunkt ein Upgrade durchführen, und zwar über die Servicekonsole. Sie haben außerdem die Möglichkeit, eine vorhandene Instanz eines Service zu verwenden, indem Sie die neue Instanz löschen und die vorhandene Instanz manuell an den Service {{site.data.keyword.iotinsurance_short}} binden. Weitere Informationen zu den Anwendungen finden Sie unter [Informationen zu {{site.data.keyword.iotinsurance_short}}](iotinsurance_overview.html).

2. Stellen Sie sicher, dass alle Services und Apps ordnungsgemäß erstellt wurden und funktionieren. Überprüfen Sie in Ihrem {{site.data.keyword.Bluemix_notm}}-Dashboard, ob alle Apps den Status `Aktiv` aufweisen. 

3. Überprüfen Sie, ob das {{site.data.keyword.iotinsurance_short}}-Dashboard funktionsbereit ist und ob Sie auf die APIs zugreifen können. 
  1. Klicken Sie auf die Kachel für den Service {{site.data.keyword.iotinsurance_short}} und wählen Sie die Registerkarte **Serviceberechtigungsnachweise** aus.
  2. Klicken Sie auf **Serviceberechtigungsnachweise anzeigen** und notieren Sie sich die Benutzer-ID und das Kennwort. Sie benötigen diese Berechtigungsnachweise für die folgenden Schritte. 
  3. Öffnen Sie das {{site.data.keyword.iotinsurance_short}}-Dashboard, indem Sie die Registerkarte **Verwalten** auswählen und auf **Öffnen** klicken. 
  4. Zeigen Sie die APIs an, indem Sie auf **APIs** klicken. 

## Services konfigurieren
{: #iot4i_configservices}
Führen Sie die folgenden Schritte aus, um die Services zu konfigurieren:

### Service '{{site.data.keyword.amashort}}' konfigurieren
{: #config_ama}
1. Geben Sie die Basis-URL der {{site.data.keyword.iotinsurance_short}}-API-Anwendung an. Diese URL wird auf der Anwendungskachel angezeigt und hat das Format *App-Name*-api.mybluemix.net. 

2. Öffnen Sie den Service '{{site.data.keyword.amashort}}'. 

3. Klicken Sie im Abschnitt **Angepasst** auf **Konfigurieren** und geben Sie die folgenden Authentifizierungsnachweise ein:

  - **Realmname**: `IoT4I`

  - **URL des angepassten Identitätsproviders**: Die URL der API-Anwendung mit folgendem Format:
  ```
  https://appName-api.mybluemix.net
  ```

  - **Weiterleitungs-URIs Ihrer Webanwendung**: Lassen Sie dieses Feld leer. 

### Service '{{site.data.keyword.mobilepushshort}}' konfigurieren
{: #config_push}
Um Push-Benachrichtigungen für eine vorhandene mobile App zu aktivieren, müssen Sie den Service '{{site.data.keyword.mobilepushshort}}' konfigurieren und eine PKCS 12-Datei (PKCS = Public Key Cryptography Standards) hinzufügen. Weitere Informationen zu der mobilen App finden Sie unter [Mobile Beispiel-App installieren und verbinden](iotinsurance_mobile_app.html). Weitere Informationen zum Service '{{site.data.keyword.mobilepushshort}}' finden Sie unter [Einführung in Push Notifications](https://new-console.stage1.ng.bluemix.net/docs/services/mobilepush/index.html). 

  1. Öffnen Sie den Service '{{site.data.keyword.mobilepushshort}}'. 
  2. Klicken Sie auf die Option zum **Einrichten der Push-Benachrichtigung**. 
  3. Laden Sie im Abschnitt zum Zertifikat für Apple-Push-Benachrichtigungen die PKCS 12-Datei für Ihre mobile App hoch und geben Sie das Kennwort ein. 

Weitere Schritte
{: #whats_next}
Hier erfahren Sie, wofür Sie {{site.data.keyword.iotinsurance_short}} einsetzen können. 

- [Benutzer und Shield-Zuordnung](iotinsurance_create_users.html) erstellen. 
- [Mobile Beispiel-App](iotinsurance_mobile_app.html) installieren und verbinden. 
- Leistung mit [erweiterten Services](iotinsurance_advancedservices.html) verbessern. 
- [APIs](https://iot4i-docs-api.mybluemix.net/dist/) anzeigen. 

# Zugehörige Links
{: #rellinks}

## Lernprogramme und Beispiele
{: #samples}
* [Code einer mobilen Beispiel-App unter Github](https://github.com/ibm-watson-iot/ioti-mobile){:new_window}

## API-Referenz
{: #api}
* [{{site.data.keyword.iotinsurance_short}}-API-Beispiele](https://iot4i-docs-api.mybluemix.net/dist/){:new_window}

## Zugehörige Links
{: #general}
* [{{site.data.keyword.iot_full}}-Dokumentation](https://new-console.ng.bluemix.net/docs/services/IoT/index.html)
* [Support-Forum für Entwickler](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [Stack Overflow-Support-Forum](http://stackoverflow.com/questions/tagged/ibm-bluemix)
