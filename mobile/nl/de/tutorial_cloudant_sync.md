---

copyright:
  years: 2016
lastupdated: "2016-12-02"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Umfassendes Lernprogramm zum Cloudant Sync-Code-Starter
{: #tutorial}

Das folgende umfassende Lernprogramm führt Sie durch die Schritte zur Erstellung eines Projekts aus dem Cloudant Sync-Code-Starter, inklusive der Tools, die Sie installiert haben müssen, sowie durch die Schritte zum Ausführen des Starters in Android Studio.


### Entwicklertools installieren
{: #dev_tools}

Stellen Sie sicher, dass Sie die [vorausgesetzten Entwicklertools](get_code.html#prereq-dev-tools){: new_window} installiert haben.


### Projekt aus dem Cloudant Sync-Code-Starter erstellen
{: #create_project}

1. Erstellen Sie ein Mobile-Dashboard-Projekt in {{site.data.keyword.Bluemix}}.

   1. Klicken Sie auf der Seite **Einführung** des Mobile-Dashboards auf **Projekt erstellen**.

      Alternativ können Sie auf der Seite **Projekte** auf **Projekt erstellen** klicken.

   2. Klicken Sie auf **Code-Starter**.

   3. Wählen Sie **Cloudant Sync** aus und klicken Sie auf **Projekt erstellen**.

   4. Geben Sie Ihren Projektnamen ein. Verwenden Sie für dieses Lernprogramm `CloudantSyncProject`.
   
   5. Klicken Sie auf **Erstellen**.

2. Fügen Sie die Data-Funktion hinzu. Sie können eine neue {{site.data.keyword.cloudant}}-Serviceinstanz erstellen oder eine vorhandene Serviceinstanz hinzufügen.

   1. Klicken Sie auf der Seite **Projektübersicht** für **Data** auf **Hinzufügen**.

      Sie können alternativ auf der Seite **Data** auf **Erstellen** oder **Vorhandene hinzufügen** klicken.
      
   2. Optional: Wenn Sie eine neue Serviceinstanz erstellen möchten, geben Sie Ihren Servicenamen ein und klicken Sie auf **Erstellen**.

   3. Optional: Wenn Sie eine vorhandene Serviceinstanz hinzufügen möchten, wählen Sie Ihre Serviceinstanz in der Liste aus und klicken Sie auf **Hinzufügen**.

   4. Klicken Sie in Ihrer Servicekachel auf das Symbol **Menü** und wählen Sie **Starten...** aus, um Ihre Serviceinstanz zu starten.

      1. Klicken Sie auf **STARTEN**, um Ihre {{site.data.keyword.cloudant}}-Konsole zu starten.

      2. Klicken Sie auf **Datenbank erstellen**, geben Sie Ihren Datenbanknamen ein und klicken Sie auf **Erstellen**.

      3. Klicken sie auf das Symbol **+** neben **Alle Dokumente**, um Dokumente hinzuzufügen.

3. Optional: Fügen Sie die Push Notifications-Funktion hinzu.

   1. Klicken Sie auf der Seite **Projektübersicht** für **Push Notifications** auf **Hinzufügen**.

      Alternativ können Sie auf der Seite **Push Notifications** auf **Erstellen** klicken.

   2. Geben Sie Ihren Servicenamen ein und klicken Sie auf **Erstellen**.

   3. Unter Android [konfigurieren Sie Firebase Cloud Messaging](/docs/services/mobilepush/t_push_provider_android.html){: new_window}.
   
4. Optional: Fügen Sie die Analytics-Funktion hinzu.

   1. Klicken Sie auf der Seite **Projektübersicht** für **Analytics** auf **Hinzufügen**.

      Alternativ können Sie auf der Seite **Analytics** auf **Erstellen** klicken.

   2. Geben Sie Ihren Servicenamen ein und klicken Sie auf **Erstellen**.
   
   3. Inaktivieren Sie den Demo-Modus, um Ihre Analysedaten nach Ausführung der App anzuzeigen.
   
   4. Weitere Informationen zur Konfiguration von Analytics finden Sie in der [Einführung zu {{site.data.keyword.mobileanalytics_short}}](/docs/services/mobileanalytics/index.html){: new_window}.
  
5. Optional: Fügen Sie die Authentication-Funktion hinzu.

   1. Klicken Sie auf der Seite **Projektübersicht** für **Authentication** auf **Hinzufügen**.

      Alternativ können Sie auf der Seite **Authentication** die Option **Erstellen** auswählen.

   2. Geben Sie Ihren Servicenamen ein und klicken Sie auf **Erstellen**.
   
   3. Wechseln Sie zu **Authentication**.
   
   4. Wählen Sie Ihren Identitätsprovider aus und geben Sie für dessen Konfiguration die erforderlichen Informationen ein. Sie können nur einen einzigen Identitätsprovider aktivieren.

   5. Weitere Informationen zur Konfiguration von Authentication finden Sie in der [Einführung zu {{site.data.keyword.amashort}}](/docs/services/mobileaccess/index.html){: new_window}.

6. Generieren Sie Ihren Projektcode.

   1. Klicken Sie auf der Seite **Projektübersicht** auf **Code abrufen**, um Ihre Plattform und Ihre Sprache auszuwählen.
   
      Alternativ können Sie auf die Seite **Code** klicken.
      
   2. Klicken Sie für Android auf **Android**.
   
   3. Wenn die Projektcodegenerierung fertig ist, klicken Sie auf **Code herunterladen**, um Ihr Projektarchiv herunterzuladen.


### Android-Projekt in Android Studio ausführen
{: #run_android}

1. Extrahieren Sie die Datei `CloudantSyncProject-Android.zip`.

2. Öffnen Sie die Datei `README.md` in einem Markdown-Viewer, um Ihr Projekt zu konfigurieren.

   1. Öffnen Sie Ihr `CloudantSyncProject-Android`-Projekt in Android Studio.

   2. Fügen Sie Ihre Cloudant-Berechtigungsnachweise hinzu.

      1. Klicken Sie auf der Seite **Data** auf das Symbol **Menü** in Ihrer Servicekachel und wählen Sie **Starten...** aus, um Ihre Serviceinstanz zu starten.

         1. Klicken Sie auf **STARTEN**, um Ihre {{site.data.keyword.cloudant}}-Konsole zu starten.

         2. Klicken Sie auf Ihren Datenbanknamen und klicken Sie auf **Berechtigungen**.

         3. Geben Sie Ihren Datenbanknamen in der Zeichenfolge `cloudant_dbname` in der Datei `res/values/cloudant_credentials.xml` ein.

         4. Klicken Sie auf **API-Schlüssel generieren**.

             1. Kopieren Sie den Wert für **Schlüssel** und fügen Sie ihn in die Zeichenfolge `cloudant_api_key` in der Datei `res/values/cloudant_credentials.xml` ein.

             2. Kopieren Sie den Wert für **Kennwort** und fügen Sie ihn in die Zeichenfolge `cloudant_api_password` in der Datei `res/values/cloudant_credentials.xml` ein.

             3. Wählen Sie die Berechtigung **_admin** aus.
      
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
* [Lernprogramm - {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [Lernprogramm - Watson Language](tutorial_watson_language.html)
* [Lernprogramm - Weather](tutorial_weather.html)
