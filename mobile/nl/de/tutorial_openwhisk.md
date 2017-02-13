---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Umfassendes Lernprogramm zum {{site.data.keyword.openwhisk_short}}-Starter
{: #tutorial}

Das folgende umfassende Lernprogramm führt Sie durch die Schritte zur Erstellung eines Projekts aus dem {{site.data.keyword.openwhisk_short}}-Code-Starter, inklusive der Tools, die Sie installiert haben müssen, sowie durch die Schritte zum Ausführen des Starters in Xcode und Android Studio.


### Entwicklertools installieren
{: #dev_tools}

Stellen Sie sicher, dass die [vorausgesetzten Entwicklertools ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](get_code.html#prereq-dev-tools "Symbol für externen Link"){: new_window} installiert sind.


### Ein Projekt aus dem {{site.data.keyword.openwhisk_short}}-Code-Starter erstellen
{: #create_project}

1. Erstellen Sie ein Mobile-Dashboard-Projekt in {{site.data.keyword.Bluemix}}.

   1. Klicken Sie auf der Seite **Einführung** des Mobile-Dashboards auf **Projekt erstellen**.

      Alternativ können Sie auf der Seite **Projekte** auf **Projekt erstellen** klicken.

   2. Klicken Sie auf **Code-Starter**.

   3. Wählen Sie **{{site.data.keyword.openwhisk_short}}** aus und klicken Sie auf **Projekt erstellen**.

   4. Geben Sie Ihren Projektnamen ein. Verwenden Sie für dieses Lernprogramm `{{site.data.keyword.openwhisk_short}}Project`.
   
   5. Klicken Sie auf **Erstellen**.

2. Optional: Fügen Sie die {{site.data.keyword.mobilepushshort}}-Funktion hinzu.

   **Hinweis**: Wenn Sie `pushAction` ausführen möchten, müssen Sie {{site.data.keyword.mobilepushshort}} hinzufügen und konfigurieren.

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

   2. Klicken Sie für Swift auf **iOS Swift**.
   
   3. Klicken Sie für Android auf **Android**.
   
   4. Wenn die Projektcodegenerierung fertig ist, klicken Sie auf **Code herunterladen**, um Ihr Projektarchiv herunterzuladen.


### Swift-Projekt in Xcode ausführen
{: #run_swift}

1. Extrahieren Sie die Datei `{{site.data.keyword.openwhisk_short}}Project-Swift.zip`.

2. Öffnen Sie die Datei `README.md` in einem Markdown-Viewer, um die Schritte zur Konfiguration Ihres Projekts zu überprüfen.

   1. Öffnen Sie Ihr Terminal und navigieren Sie zu Ihrem Projektordner.
   
      1. Führen Sie `pod setup` aus, wenn Sie Ihr CocoaPods-Repository einrichten müssen.
      
      2. Führen Sie `pod update` aus, wenn Sie Ihre bereits vorhandenen Pods aktualisieren müssen.
      
      3. Führen Sie `pod install` aus, um die Pods zu installieren, die für Ihr Projekt erforderlich sind.
      
   3. Öffnen Sie Ihren Xcode-Arbeitsbereich `{{site.data.keyword.openwhisk_short}}Project.xcworkspace`.

   4. Wenn Sie `pushAction` ausführen möchten, müssen Sie {{site.data.keyword.mobilepush}} konfigurieren.
      
3. Führen Sie Ihre App aus.


### Android-Projekt in Android Studio ausführen
{: #run_android}

1. Extrahieren Sie die Datei `{{site.data.keyword.openwhisk_short}}Project-Android.zip`.

2. Öffnen Sie die Datei `README.md` in einem Markdown-Viewer, um Ihr Projekt zu konfigurieren.

   1. Öffnen Sie Ihr `{{site.data.keyword.openwhisk_short}}Project-Android`-Projekt in Android Studio.

   2. Wenn Sie `pushAction` ausführen möchten, müssen Sie {{site.data.keyword.mobilepush}} konfigurieren.
      
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
* [Lernprogramm - {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [Lernprogramm - Watson Language](tutorial_watson_language.html)
* [Lernprogramm - Weather](tutorial_weather.html)
