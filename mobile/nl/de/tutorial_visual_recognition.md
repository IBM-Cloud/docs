---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}

# Umfassendes Lernprogramm zum {{site.data.keyword.visualrecognitionshort}}-Code-Starter
{: #tutorial_vr}

Das folgende umfassende Lernprogramm führt Sie durch die Schritte zur Erstellung eines Projekts aus dem {{site.data.keyword.visualrecognitionshort}}-Code-Starter, inklusive der Tools, die Sie installiert haben müssen, sowie durch die Schritte zum Ausführen des Starters in Xcode und Android Studio.


### Entwicklertools installieren
{: #dev_tools}

Stellen Sie sicher, dass die [vorausgesetzten Entwicklertools ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](get_code.html#prereq-dev-tools "Symbol für externen Link"){: new_window} installiert sind.


### Ein Projekt aus dem {{site.data.keyword.visualrecognitionshort}}-Code-Starter erstellen
{: #create_project}

1. Erstellen Sie ein Mobile-Dashboard-Projekt in {{site.data.keyword.Bluemix}}.

   1. Klicken Sie auf der Seite **Einführung** des Mobile-Dashboards auf **Projekt erstellen**.

      Alternativ können Sie auf der Seite **Projekte** auf **Projekt erstellen** klicken.

   2. Klicken Sie auf **Code-Starter**.

   3. Wählen Sie **Visual Recognition** aus und klicken Sie auf **Projekt erstellen**.

   4. Geben Sie Ihren Projektnamen ein. Verwenden Sie für dieses Lernprogramm `VisualRecognitionProject`.
   
   5. Klicken Sie auf **Erstellen**.

2. Optional: Fügen Sie die {{site.data.keyword.mobilepushshort}}-Funktion hinzu.

   1. Klicken Sie auf der Seite **Projektübersicht** für **{{site.data.keyword.mobilepushshort}}** auf **Hinzufügen**.

      Alternativ können Sie auf der Seite **{{site.data.keyword.mobilepushshort}}** auf **Erstellen** klicken.

   2. Geben Sie Ihren Servicenamen ein und klicken Sie auf **Erstellen**.

   3. Für iOS: [Apple Push Notification Service konfigurieren ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](/docs/services/mobilepush/t_push_provider_ios.html "Symbol für externen Link"){: new_window}.

   4. Für Android: [Firebase Cloud Messaging konfigurieren ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](/docs/services/mobilepush/t_push_provider_android.html "Symbol für externen Link"){: new_window}.
   
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

   5. Weitere Informationen zum Konfigurieren der Authentifizierung finden Sie unter [Einführung in {{site.data.keyword.amashort}} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](/docs/services/mobileaccess/index.html "Symbol für externen Link"){: new_window}.

5. Generieren Sie Ihren Projektcode.

   1. Klicken Sie auf der Seite **Projektübersicht** auf **Code abrufen**, um Ihre Plattform und Ihre Sprache auszuwählen.
   
      Alternativ können Sie auf die Seite **Code** klicken.
      
   2. Klicken Sie für iOS auf **iOS Swift**.
   
   3. Klicken Sie für Android auf **Android**.
   
   4. Wenn die Projektcodegenerierung fertig ist, klicken Sie auf **Code herunterladen**, um Ihr Projektarchiv herunterzuladen.


### Eigenes Projekt in Xcode ausführen
{: #run_xcode}

1. Extrahieren Sie die Datei `VisualRecognitionProject-Swift.zip`.

2. Öffnen Sie die Datei `README.md` in einem Markdown-Viewer, um die Schritte zur Konfiguration Ihres Projekts zu überprüfen.

   1. Erstellen Sie Ihre [{{site.data.keyword.visualrecognitionshort}} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://console.{DomainName}/catalog/services/visual-recognition/ "Symbol für externen Link"){: new_window}-Serviceinstanz.
   
   2. Öffnen Sie Ihr Terminal und navigieren Sie zu Ihrem Projektordner.
   
      1. Führen Sie `pod setup` aus, wenn Sie Ihr CocoaPods-Repository einrichten müssen.
      
      2. Führen Sie `pod update` aus, wenn Sie Ihre bereits vorhandenen Pods aktualisieren müssen.
      
      3. Führen Sie `pod install` aus, um die Pods zu installieren, die für Ihr Projekt erforderlich sind.
      
      4. Führen Sie `carthage update --platform iOS` aus, um die Abhängigkeiten und Frameworks zur Verwendung des {{site.data.keyword.ibmwatson}} Developer Cloud iOS SDK aufzubauen.
      
   3. Öffnen Sie Ihren Xcode-Arbeitsbereich `VisualRecognitionProject.xcworkspace`.
   
   4. Fügen Sie Ihre {{site.data.keyword.visualrecognitionshort}}-Serviceberechtigungsnachweise hinzu.
   
      1. Kopieren Sie Ihren API-Schlüssel (`api_key`) aus Ihren {{site.data.keyword.visualrecognition}}-Serviceberechtigungsnachweisen.
      
      2. Fügen Sie Ihren API-Schlüssel (`api_key`) in den Schlüssel `VisualRecognitionAPIKey` in die Datei `WatsonCredentials.plist`.
      
3. Führen Sie Ihre App aus.


### Eigenes Projekt in Android Studio ausführen
{: #run_studio}

1. Extrahieren Sie die Datei `VisualRecognitionProject-Android.zip`.

2. Öffnen Sie die Datei `README.md` in einem Markdown-Viewer, um Ihr Projekt zu konfigurieren.

   1. Erstellen Sie Ihre [{{site.data.keyword.visualrecognitionshort}} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://console.{DomainName}/catalog/services/visual-recognition/ "Symbol für externen Link"){: new_window}-Serviceinstanz.
   
      Überspringen Sie diesen Schritt, falls Sie bereits über eine Instanz des Service {{site.data.keyword.visualrecognitionshort}} verfügen.
   
   2. Öffnen Sie Ihr Projekt `VisualRecognitionProject-Android` in Android Studio.
   
   4. Fügen Sie Ihre {{site.data.keyword.visualrecognitionshort}}-Serviceberechtigungsnachweise hinzu.
   
      1. Kopieren Sie Ihren API-Schlüssel (`api_key`) aus Ihren {{site.data.keyword.visualrecognitionshort}}-Serviceberechtigungsnachweisen.
      
      2. Fügen Sie Ihren API-Schlüssel (`api_key`) in den Schlüssel `watson_visual_recognition_api_key` in die Datei `res/values/watson_credentials.xml`.
      
3. Führen Sie Ihre App aus.


## Nächste Schritte
{: #what_next}

Öffen Sie weitere Lernprogramme.


### Lernprogramme zu Benutzerschnittstellenstartern
{: #tutorials_UI}

* [Lernprogramm - Store Catalog](tutorial_store_catalog.html)


### Lernprogramme zu Code-Startern
{: #tutorials_Code}

* [Lernprogramm - Basic](tutorial.html)
* [Lernprogramm - Cloudant Sync](tutorial_cloudant_synd.html)
* [Lernprogramm - {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [Lernprogramm - Watson Language](tutorial_watson_language.html)
* [Lernprogramm - Weather](tutorial_weather.html)

