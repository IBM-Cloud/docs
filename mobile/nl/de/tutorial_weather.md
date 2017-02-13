---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}

# Lernprogramm - Starter für Weather Code
{: #tutorial_weather}

Der {{site.data.keyword.Bluemix}} Mobile-Code-Starter für Weather veranschaulicht ein Gerüstprojekt als Einführung in die Arbeit mit Weather unter Verwendung von Swift. Außerdem enthält es die Push- und Analytics-Integrationspunkte.


## Voraussetzungen
{: #tutorial_requirements}

* Ein [Bluemix ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](http://bluemix.net "Symbol für externen Link")-Konto
* Eine [Weather Company Data ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://console.{DomainName}/catalog/services/weather-company-data/ "Symbol für externen Link")-Serviceinstanz aus dem [Bluemix-Katalog ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://console.{DomainName}/catalog/ "Symbol für externen Link")


## Einführung
{: #tutorial_gs}

Zur schnellen Einrichtung und Ausführung mit dem Code-Starter für Weather befolgen Sie diese Schritte:

1. Erstellen Sie ein Mobile-Dashboard-Projekt in {{site.data.keyword.Bluemix_notm}}.

   1. Klicken Sie auf der Seite **Einführung** des Mobile-Dashboards auf **Projekt erstellen**.

      Alternativ können Sie auf der Seite **Projekte** auf **Neues Projekt** klicken.

   2. Klicken Sie auf **Code-Starter**.

   3. Wählen Sie **Weather** aus und klicken Sie auf **Projekt erstellen**.

   4. Geben Sie Ihren Projektnamen ein und klicken Sie auf **Erstellen**.

2. Optional: Fügen Sie die {{site.data.keyword.mobilepushshort}}-Funktion hinzu.

   1. Klicken Sie auf der Seite **Projektübersicht** für **{{site.data.keyword.mobilepushshort}}** auf **Hinzufügen**.

      Alternativ können Sie auf der Seite **{{site.data.keyword.mobilepushshort}}** auf **Erstellen** klicken.

   2. Geben Sie Ihren Servicenamen ein und klicken Sie auf **Erstellen**.

   3. Für iOS: [Apple Push Notification Service konfigurieren ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](/docs/services/mobilepush/t_push_provider_ios.html "Symbol für externen Link"){: new_window}.

   4. Für Android: [Google Cloud Messaging konfigurieren ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](/docs/services/mobilepush/t_push_provider_android.html "Symbol für externen Link"){: new_window}.
   
3. Optional: Fügen Sie die Analytics-Funktion hinzu.

   1. Klicken Sie auf der Seite **Projektübersicht** für **Analytics** auf **Hinzufügen**.

      Alternativ können Sie auf der Seite **Analytics** auf **Erstellen** klicken.

   2. Geben Sie Ihren Servicenamen ein und klicken Sie auf **Erstellen**.
   
   3. Inaktivieren Sie den Demo-Modus, um Ihre Analysedaten nach Ausführung der App anzuzeigen.

   4. Weitere Informationen zum Konfigurieren von Analytics finden Sie unter [Einführung in {{site.data.keyword.mobileanalytics_short}} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](/docs/services/mobileanalytics/index.html "Symbol für externen Link"){: new_window}.

4. Optional: Fügen Sie die Authentication-Funktion hinzu.

   1. Klicken Sie auf der Seite **Projektübersicht** für **Authentication** auf **Hinzufügen**.

      Alternativ können Sie auf der Seite **Authentication** die Option **Erstellen** auswählen.

   2. Geben Sie Ihren Servicenamen ein und klicken Sie auf **Erstellen**.
   
   3. Wechseln Sie zu **Authentication**.
   
   4. Wählen Sie Ihren Identitätsprovider aus und geben Sie für dessen Konfiguration die erforderlichen Informationen ein. Sie können nur einen einzigen Identitätsprovider aktivieren.

   5. Weitere Informationen zum Konfigurieren der Authentifizierung finden Sie unter [Einführung in Mobile Client Access ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](/docs/services/mobileaccess/index.html "Symbol für externen Link"){: new_window}. 

5. Laden Sie Ihr Projekt herunter.

   1. Klicken Sie auf **Code** und wählen Sie Ihre bevorzugte Sprache aus.

   2. Klicken Sie auf **Code herunterladen**.

5. Extrahieren Sie das Archiv und befolgen Sie die Anweisungen in der `README.md`-Datei.


## Nächste Schritte
{: #tutorial_next}

[Testen Sie Ihre App! ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](http://console.{DomainName}/mobile/create-project?starter=fad1d49e-f7b6-3aff-9b53-14673fca4399 "Symbol für externen Link"){: new_window}


### Lernprogramme zu Benutzerschnittstellenstartern
{: #tutorials_UI}

* [Lernprogramm - Store Catalog](tutorial_store_catalog.html)


### Lernprogramme zu Code-Startern
{: #tutorials_Code}

* [Lernprogramm - Basic](tutorial.html)
* [Lernprogramm - Cloudant Sync](tutorial_cloudant_synd.html)
* [Lernprogramm - {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [Lernprogramm - {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [Lernprogramm - Watson Language](tutorial_watson_language.html)
