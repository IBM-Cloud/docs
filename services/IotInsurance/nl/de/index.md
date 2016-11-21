---

copyright:
  years: 2016
lastupdated: "2016-10-26"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# Einführung in {{site.data.keyword.iotinsurance_short}}

{{site.data.keyword.iotinsurance_full}} ist ein {{site.data.keyword.Bluemix_notm}}-Service, den Sie zum Erfassen, Verwalten und Analysieren von Daten von verbundenen Versicherungsnehmern verwenden können. {{site.data.keyword.iotinsurance_short}} ermöglicht Ihnen eine personalisierte Risikobewertung, Echtzeitschutz und eine Reduzierung der Versicherungskosten.
{:shortdesc}

Um diesen Service in Betrieb zu nehmen, müssen Sie die erforderlichen Services und Apps bereitstellen und die Services anschließend konfigurieren. Eine Übersicht der Services und Apps sowie ein Architekturdiagramm finden Sie unter [Informationen zu {{site.data.keyword.iotinsurance_short}}](iotinsurance_overview.html).

**Voraussetzungen:** Stellen Sie zunächst sicher, dass folgende Voraussetzungen erfüllt sind:
- Eine Instanz des Service [{{site.data.keyword.iotinsurance_short}}](https://console.ng.bluemix.net/catalog/services/iot-for-insurance/) muss sich in Ihrem {{site.data.keyword.Bluemix_notm}}-Bereich befinden.
- Es müssen mindestens 2 GB freier Speicher in Ihrer {{site.data.keyword.Bluemix_notm}}-Organisation verfügbar sein, um die Bereitstellungsfunktion zu aktivieren.

## Erforderliche Services und Anwendungen bereitstellen
{: #deploying_services}

1. Um alle erforderlichen Services und Anwendungen bereitzustellen, klicken Sie in der [{{site.data.keyword.Bluemix_notm}}-Konsole](https://console.ng.bluemix.net/#all-items) auf den Service {{site.data.keyword.iotinsurance_short}} und klicken Sie anschließend auf **Bereitstellen**.

  {{site.data.keyword.iotinsurance_short}} stellt alle erforderlichen Services und Node.js-Anwendungen bereit. Die Anwendungen werden automatisch an die Services gebunden.

  Jede Serviceinstanz verwendet den Standardserviceplan. Sie können für jeden Serviceplan zu einem späteren Zeitpunkt ein Upgrade durchführen, und zwar über die Servicekonsole. Sie haben außerdem die Möglichkeit, eine vorhandene Instanz eines Service zu verwenden, indem Sie die neue Instanz löschen und die vorhandene Instanz manuell an den Service {{site.data.keyword.iotinsurance_short}} binden. Weitere Informationen zu den Anwendungen finden Sie unter [Informationen zu {{site.data.keyword.iotinsurance_short}}](iotinsurance_overview.html).

2. Überprüfen Sie, ob das {{site.data.keyword.iotinsurance_short}}-Dashboard funktionsbereit ist und ob Sie auf die APIs zugreifen können.
  1. Öffnen Sie das {{site.data.keyword.iotinsurance_short}}-Dashboard, indem Sie auf **Öffnen** klicken. Akzeptieren Sie die vorab ausgefüllten Berechtigungsnachweise, indem Sie auf die Option zum **Anmelden** klicken.
  2. Kehren Sie zur {{site.data.keyword.iotinsurance_short}}-Servicekonsole zurück und zeigen Sie die APIs durch Klicken auf **APIs** an.

  **Anmerkung:** Nach der Bereitstellung können Sie auf das Dashboard oder die APIs direkt zugreifen, indem Sie die entsprechenden URLs in Ihren Browser eingeben. Bei dieser Methode müssen Sie Ihre Berechtigungsnachweise für den {{site.data.keyword.iotinsurance_short}}-Service eingeben. Um nach Ihren Berechtigungsnachweisen zu suchen, müssen Sie zur {{site.data.keyword.iotinsurance_short}}-Servicekonsole zurückkehren. Klicken Sie auf die Registerkarte **Serviceberechtigungsnachweise** und klicken Sie anschließend auf **Berechtigungsnachweise anzeigen**. Notieren Sie sich die Benutzer-ID und das Kennwort.

## Services konfigurieren
{: #iot4i_configservices}
Führen Sie die folgenden Schritte aus, um die Services zu konfigurieren:

### Service '{{site.data.keyword.amashort}}' konfigurieren
{: #config_ama}
1. Kehren Sie zu Ihrer Bluemix-Konsole zurück. Es werden alle Apps und Services angezeigt, die von {{site.data.keyword.iotinsurance_short}} bereitgestellt wurden.

1. Kopieren Sie die URL der {{site.data.keyword.iotinsurance_short}}-API-Anwendung. Klicken Sie mit der rechten Maustaste auf die API-Anwendung und wählen Sie die Option zum Kopieren der Linkposition aus.

2. Öffnen Sie den Service '{{site.data.keyword.amashort}}'. Der Service steht im Abschnitt 'Services' Ihrer {{site.data.keyword.Bluemix_notm}}-Konsole zur Verfügung.

3. Aktivieren Sie die Authentifizierung, indem Sie auf **Ein** klicken.

4. Klicken Sie im Abschnitt **Angepasst** auf **Konfigurieren** und geben Sie die folgenden Authentifizierungsnachweise ein:

  - **Realmname**: `IoT4I`

  - **URL des angepassten Identitätsproviders**: Fügen Sie die URL der API-Anwendung ein, die Sie im ersten Schritt kopiert haben.

  - **Weiterleitungs-URIs Ihrer Webanwendung**: Lassen Sie dieses Feld leer.

5. Speichern Sie Ihre Einstellungen. Sie können nun zur {{site.data.keyword.iotinsurance_short}}-Servicekonsole oder zu Ihrer {{site.data.keyword.Bluemix_notm}}-Konsole zurückkehren.

### Service '{{site.data.keyword.mobilepushshort}}' konfigurieren
{: #config_push}
Um Push-Benachrichtigungen für eine vorhandene mobile App zu aktivieren, müssen Sie den Service '{{site.data.keyword.mobilepushshort}}' konfigurieren und eine PKCS 12-Datei (PKCS = Public Key Cryptography Standards) hinzufügen. Weitere Informationen zu der mobilen App finden Sie unter [Mobile Beispiel-App installieren und verbinden](iotinsurance_mobile_app.html). Weitere Informationen zum Service '{{site.data.keyword.mobilepushshort}}' finden Sie unter [Einführung in Push Notifications](https://console.stage1.ng.bluemix.net/docs/services/mobilepush/index.html).

  1. Öffnen Sie den Service '{{site.data.keyword.mobilepushshort}}'.
  2. Klicken Sie auf **Konfigurieren**.
  3. Laden Sie im Abschnitt zum Zertifikat für Apple-Push-Benachrichtigungen die PKCS 12-Datei für Ihre mobile App hoch und geben Sie das Kennwort ein.


Weitere Schritte
{: #whats_next}
Hier erfahren Sie, wofür Sie {{site.data.keyword.iotinsurance_short}} einsetzen können.

- Verwenden Sie die Anweisungen und APIs im Shield Toolkit, um einen [Benutzer und eine Shield-Zuordnung](iotinsurance_shield_toolkit.html) zu erstellen.
- [Mobile Beispiel-App](iotinsurance_mobile_app.html) installieren und verbinden.
- Laden Sie die gesamten [APIs auf der GitHub-Site](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples) herunter oder zeigen Sie sie an.

# Zugehörige Links
{: #rellinks}

## Lernprogramme und Beispiele
{: #samples}
* [Code einer mobilen Beispiel-App unter GitHub](https://github.com/ibm-watson-iot/ioti-mobile){:new_window}

## API-Referenz
{: #api}
* [{{site.data.keyword.iotinsurance_short}}-API](https://iot4i-api-docs.mybluemix.net/){:new_window}
* [{{site.data.keyword.iotinsurance_short}}-API-Beispiele](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window}


## Zugehörige Links
{: #general}
* [{{site.data.keyword.iot_full}}-Dokumentation](https://console.ng.bluemix.net/docs/services/IoT/index.html)
* [Support-Forum für Entwickler](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [Stack Overflow-Support-Forum](http://stackoverflow.com/questions/tagged/ibm-bluemix)
