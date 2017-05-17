---

copyright:
  years: 2016, 2017
lastupdated: "2017-05-02"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# Einführung in {{site.data.keyword.iotinsurance_short}}
{: #gettingstarted}

{{site.data.keyword.iotinsurance_full}} ist ein {{site.data.keyword.Bluemix_notm}}-Service, den Sie zum Erfassen, Verwalten und Analysieren von Daten von verbundenen Versicherungsnehmern verwenden können. {{site.data.keyword.iotinsurance_short}} ermöglicht Ihnen eine personalisierte Risikobewertung, Echtzeitschutz und eine Reduzierung der Versicherungskosten.
{:shortdesc}

Um diesen Service in Betrieb zu nehmen, müssen Sie die erforderlichen Services und Apps bereitstellen und die Services anschließend konfigurieren. Eine Übersicht der Services und Apps sowie ein Architekturdiagramm finden Sie unter [Informationen zu {{site.data.keyword.iotinsurance_short}}](iotinsurance_overview.html).

**Voraussetzungen:** Stellen Sie zunächst sicher, dass folgende Voraussetzungen erfüllt sind:
- Eine Instanz des Service [{{site.data.keyword.iotinsurance_short}}](https://console.ng.bluemix.net/catalog/services/iot-for-insurance/) muss sich in Ihrem {{site.data.keyword.Bluemix_notm}}-Bereich befinden.
- Es müssen mindestens 2 GB freier Speicher in Ihrer {{site.data.keyword.Bluemix_notm}}-Organisation verfügbar sein, um die Bereitstellungsfunktion zu aktivieren. Für ein Upgrade von einer Vorgängerversion benötigen Sie mindestens 2,5 GB. 

## Erforderliche Services und Anwendungen bereitstellen
{: #deploying_services}

1. Um alle erforderlichen Services und Anwendungen bereitzustellen, klicken Sie in der [{{site.data.keyword.Bluemix_notm}}-Konsole](https://console.ng.bluemix.net/#all-items) auf den Service {{site.data.keyword.iotinsurance_short}} und klicken Sie anschließend auf **Bereitstellen**.

  {{site.data.keyword.iotinsurance_short}} stellt alle erforderlichen Services und Node.js-Anwendungen bereit. Die Anwendungen werden automatisch an die Services gebunden.

  Jede Serviceinstanz verwendet den Standardserviceplan. Sie können für jeden Serviceplan zu einem späteren Zeitpunkt ein Upgrade durchführen, und zwar über die Servicekonsole. Sie haben außerdem die Möglichkeit, eine vorhandene Instanz eines Service zu verwenden, indem Sie die neue Instanz löschen und die vorhandene Instanz manuell an den Service {{site.data.keyword.iotinsurance_short}} binden. Weitere Informationen zu den Anwendungen finden Sie unter [Informationen zu {{site.data.keyword.iotinsurance_short}}](iotinsurance_overview.html).

  **Wichtig:** Wenn Sie die Testversion von {{site.data.keyword.iotinsurance_short}} bereitstellen, beachten Sie, dass die kostenfreien Versionen der anderen, ebenfalls bereitgestellten Services und Anwendungen in ihrer Funktionalität eingeschränkt werden. Für {{site.data.keyword.iot_short_notm}} gilt ein Grenzwert von maximal 500 Geräten und für {{site.data.keyword.cloudant_short_notm}} ein Grenzwert von 1 GB an Daten sowie eine Einschränkung der Lese-/Schreib-Threading-Funktionalität. 

  **Hinweis**: {{site.data.keyword.iotinsurance_short}} stellt weder {{site.data.keyword.amafull}} noch {{site.data.keyword.mobilepushfull}} weiterhin bereit. Frühere Versionen von {{site.data.keyword.iotinsurance_short}} nutzten den Service {{site.data.keyword.amashort}}, um die Antworten aus der mobilen App zu verarbeiten. Dieser Prozess funktioniert weiterhin für alle vorhandenen Instanzen von {{site.data.keyword.iotinsurance_short}}. Sie müssen jedoch einen angepassten Authentifizierungsprozess einrichten, um die mobile App mit neuen Instanzen von
{{site.data.keyword.iotinsurance_short}} zu verwenden. Optional können Sie auch [eine Instanz von {{site.data.keyword.mobilepushshort}}](https://console.ng.bluemix.net/docs/services/mobilepush/index.html) erstellen, konfigurieren und an die {{site.data.keyword.iotinsurance_short}}-API binden.

2. Überprüfen Sie, ob das {{site.data.keyword.iotinsurance_short}}-Dashboard funktionsbereit ist und ob Sie auf die APIs zugreifen können.
  1. Öffnen Sie das {{site.data.keyword.iotinsurance_short}}-Dashboard, indem Sie auf **Öffnen** klicken. Akzeptieren Sie die vorab ausgefüllten Berechtigungsnachweise, indem Sie auf die Option zum **Anmelden** klicken.
  2. Kehren Sie zur {{site.data.keyword.iotinsurance_short}}-Servicekonsole zurück und zeigen Sie die APIs durch Klicken auf **APIs** an.

  **Anmerkung:** Nach der Bereitstellung können Sie auf das Dashboard oder die APIs direkt zugreifen, indem Sie die entsprechenden URLs in Ihren Browser eingeben. Bei dieser Methode müssen Sie Ihre Berechtigungsnachweise für den {{site.data.keyword.iotinsurance_short}}-Service eingeben. Um nach Ihren Berechtigungsnachweisen zu suchen, müssen Sie zur {{site.data.keyword.iotinsurance_short}}-Servicekonsole zurückkehren. Klicken Sie auf die Registerkarte **Serviceberechtigungsnachweise** und klicken Sie anschließend auf **Berechtigungsnachweise anzeigen**. Notieren Sie sich die Benutzer-ID und das Kennwort.


<!--
## Configuring
{: #iot4i_configservices}



### Configuring {{site.data.keyword.amashort}}
{: #config_ama}
1. Return to your Bluemix console. All apps and services that were deployed by {{site.data.keyword.iotinsurance_short}} are displayed.

2. Copy the URL of the {{site.data.keyword.iotinsurance_short}} API application. Right-click the API application and select **Copy Link Location**.

3. Open the {{site.data.keyword.amashort}} service. The service is available in the Services section of your {{site.data.keyword.Bluemix_notm}} console.

4. Enable authentication by clicking **On**.

5. In the **Custom** section, enter the following authentication credentials:

  - **Realm name**: `IoT4I`

  - **Custom Identity Provider Url**: Paste the URL of the API application that you copied in a previous step.

  - **Your Web Application Redirect URIs**: Leave this field blank.

6. Save your settings. You can now return to the {{site.data.keyword.iotinsurance_short}} service console or your {{site.data.keyword.Bluemix_notm}} console.
-->


## Erstellung und Konfiguration von {{site.data.keyword.mobilepushshort}}
{: #config_push}

(Optional) Um Push-Benachrichtigungen für eine vorhandene mobile App zu aktivieren, können Sie optional eine Instanz des Service '{{site.data.keyword.mobilepushshort}}' erstellen, diese an die {{site.data.keyword.iotinsurance_short}}-APi binden und eine PKCS 12-Datei (PKCS = Public Key Cryptography Standards) hinzufügen. Weitere Informationen zu der mobilen App finden Sie unter [Mobile Beispiel-App installieren und verbinden](iotinsurance_mobile_app.html). Informationen zu {{site.data.keyword.mobilepushshort}} finden Sie im Abschnitt zur [Einführung in Push Notifications](https://console.ng.bluemix.net/docs/services/mobilepush/index.html).

Führen Sie die folgenden Schritte aus, um den Service nach der Erstellung zu konfigurieren:

  1. Öffnen Sie den Service '{{site.data.keyword.mobilepushshort}}'.
  2. Klicken Sie auf **Konfigurieren**.
  3. Laden Sie im Abschnitt zum Zertifikat für Apple-Push-Benachrichtigungen die PKCS 12-Datei für Ihre mobile App hoch und geben Sie das Kennwort ein.

## Weather Company-Daten verwenden
{: #weather_company}

(Optional) {{site.data.keyword.iotinsurance_short}} stellt statische Daten der Weather Company bereit, die Sie zu Demonstrationszwecken anzeigen können. Optional können Sie auch auf Livedaten der Weather Company zugreifen, indem Sie eine Instanz des [{{site.data.keyword.weatherfull}}-Service](../Weather/index.html) erstellen und an die {{site.data.keyword.iotinsurance_short}}-Wetter-App binden. 

**Wichtig:** Die kostenfreie Version des {{site.data.keyword.weather_short}}-Service ist auf 10.000 Anforderungen begrenzt. Sie können ein Upgrade auf eine gebührenpflichtige Version durchführen, wenn Sie zusätzliche Anforderungen benötigen.

Weitere Schritte
{: #whats_next}
Hier erfahren Sie, wofür Sie {{site.data.keyword.iotinsurance_short}} einsetzen können.

- Verwenden Sie die Anweisungen und APIs im Shield Toolkit, um einen [Benutzer und eine Shield-Zuordnung](iotinsurance_shield_toolkit.html) zu erstellen.
<!-- - Install and connect the [sample mobile app](iotinsurance_mobile_app.html). -->
- Sie können alle [API-Beispiele auf der GitHub-Site ![Symbol für externen Link](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window} anzeigen und von dort herunterladen. 
