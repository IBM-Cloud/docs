---

copyright:
  years: 2016
lastupdated: "2016-10-21"

---
{:new_window: target="_blank"}

# Umfassendes Lernprogramm zum {{site.data.keyword.visualrecognitionshort}}-Code-Starter
{: #tutorial}

Das folgende umfassende Lernprogramm führt Sie durch die Schritte zur Erstellung eines Projekts aus dem {{site.data.keyword.visualrecognitionshort}}-Code-Starter, inklusive der Tools, die Sie installiert haben müssen, sowie durch die Schritte zum Ausführen des Starters in Xcode und Android Studio.


### Entwicklertools installieren
{: #dev_tools}

Stellen Sie sicher, dass Sie die [vorausgesetzten Entwicklertools](get_code.html#prereq-dev-tools){: new_window} installiert haben.


### Ein Projekt aus dem {{site.data.keyword.visualrecognitionshort}}-Code-Starter erstellen
{: #create_project}

1. Erstellen Sie ein Mobile-Dashboard-Projekt in {{site.data.keyword.Bluemix}}.

   1. Klicken Sie auf der Seite **Einführung** des Mobile-Dashboards auf **Projekt erstellen**.

      Alternativ können Sie auf der Seite **Projekte** auf **Projekt erstellen** klicken.

   2. Klicken Sie auf **Code-Starter**.

   3. Wählen Sie **Visual Recognition** aus und klicken Sie auf **Projekt erstellen**.

   4. Geben Sie Ihren Projektnamen ein. Verwenden Sie für dieses Lernprogramm `VisualRecognitionProject`.
   
   5. Klicken Sie auf **Erstellen**.

2. Optional: Fügen Sie die Push Notifications-Funktion hinzu.

   1. Klicken Sie auf der Seite **Projektübersicht** für **Push Notifications** auf **Hinzufügen**.

      Alternativ können Sie auf der Seite **Push Notifications** auf **Erstellen** klicken.

   2. Geben Sie Ihren Servicenamen ein und klicken Sie auf **Erstellen**.

   3. Unter iOS [konfigurieren Sie den Apple-Service 'Push Notification'](/docs/services/mobilepush/t_push_provider_ios.html){: new_window}.

   4. Unter Android [konfigurieren Sie Firebase Cloud Messaging](/docs/services/mobilepush/t_push_provider_android.html){: new_window}.
   
3. Optional: Fügen Sie die Analytics-Funktion hinzu.

   1. Klicken Sie auf der Seite **Projektübersicht** für **Analytics** auf **Hinzufügen**.

      Alternativ können Sie auf der Seite **Analytics** auf **Erstellen** klicken.

   2. Geben Sie Ihren Servicenamen ein und klicken Sie auf **Erstellen**.
   
   3. Inaktivieren Sie den Demo-Modus, um Ihre Analysedaten nach Ausführung der App anzuzeigen.
   
   4. Weitere Informationen zur Konfiguration von Analytics finden Sie in der [Einführung zu {{site.data.keyword.mobileanalytics_short}}](/docs/services/mobileanalytics/index.html){: new_window}.
  
4. Optional: Fügen Sie die Authentication-Funktion hinzu.

   1. Klicken Sie auf der Seite **Projektübersicht** für **Authentication** auf **Hinzufügen**.

      Alternativ können Sie auf der Seite **Authentication** die Option **Erstellen** auswählen.

   2. Geben Sie Ihren Servicenamen ein und klicken Sie auf **Erstellen**.
   
   3. Wechseln Sie zu **Authentication**.
   
   4. Wählen Sie Ihren Identitätsprovider aus und geben Sie für dessen Konfiguration die erforderlichen Informationen ein. Sie können nur einen einzigen Identitätsprovider aktivieren.

   5. Weitere Informationen zur Konfiguration von Authentication finden Sie in der [Einführung zu {{site.data.keyword.amashort}}](/docs/services/mobileaccess/index.html){: new_window}.

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

   1. Erstellen Sie Ihre Instanz des Service [{{site.data.keyword.visualrecognitionshort}}](https://console.{DomainName}/catalog/services/visual-recognition/){: new_window}.
   
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

   1. Erstellen Sie Ihre Instanz des Service [{{site.data.keyword.visualrecognitionshort}}](https://console.{DomainName}/catalog/services/visual-recognition/){: new_window}.
   
      Überspringen Sie diesen Schritt, falls Sie bereits über eine Instanz des Service {{site.data.keyword.visualrecognitionshort}} verfügen.
   
   2. Öffnen Sie Ihr Projekt `VisualRecognitionProject-Android` in Android Studio.
   
   4. Fügen Sie Ihre {{site.data.keyword.visualrecognitionshort}}-Serviceberechtigungsnachweise hinzu.
   
      1. Kopieren Sie Ihren API-Schlüssel (`api_key`) aus Ihren {{site.data.keyword.visualrecognition}}-Serviceberechtigungsnachweisen.
      
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

* [Lernprogramm - Watson Language](tutorial_watson_language.html)
* [Lernprogramm - Weather](tutorial_weather.html)
