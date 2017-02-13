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

# Umfassendes Lernprogramm zum Cloudant Sync-Code-Starter
{: #tutorial}

Das folgende umfassende Lernprogramm führt Sie durch die Schritte zur Erstellung eines Projekts aus dem Cloudant Sync-Code-Starter, inklusive der Tools, die Sie installiert haben müssen, sowie durch die Schritte zum Ausführen des Starters in Android Studio.


### Entwicklertools installieren
{: #dev_tools}

Stellen Sie sicher, dass die [vorausgesetzten Entwicklertools ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](get_code.html#prereq-dev-tools "Symbol für externen Link"){: new_window} installiert sind.


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

   1. Klicken Sie auf der Seite **Projektübersicht** in der Kachel **Daten** auf **Anzeigen**.

      Alternativ können Sie auf der Seite **Daten** auf **Erstellen** oder **Vorhandene hinzufügen** und anschließend auf **Cloudant NoSQL DB** klicken.
      
   2. Optional: Wenn Sie eine neue Serviceinstanz erstellen möchten, geben Sie Ihren Servicenamen ein und klicken Sie auf **Erstellen**.

   3. Optional: Wenn Sie eine vorhandene Serviceinstanz hinzufügen möchten, wählen Sie Ihre Serviceinstanz in der Liste aus und klicken Sie auf **Vorhandene hinzufügen**.

   4. Klicken Sie in Ihrer Servicekachel auf das Symbol **Menü** und wählen Sie **Starten...** aus, um Ihre Serviceinstanz zu starten.

      1. Klicken Sie auf **STARTEN**, um Ihre {{site.data.keyword.cloudant}}-Konsole zu starten.

      2. Klicken Sie auf **Datenbank erstellen**, geben Sie Ihren Datenbanknamen ein und klicken Sie auf **Erstellen**.

      3. Klicken sie auf das Symbol **+** neben **Alle Dokumente**, um Dokumente hinzuzufügen.

3. Optional: Fügen Sie die {{site.data.keyword.mobilepushshort}}-Funktion hinzu.

   1. Klicken Sie auf der Seite **Projektübersicht** für **{{site.data.keyword.mobilepushshort}}** auf **Hinzufügen**.

      Alternativ können Sie auf der Seite **{{site.data.keyword.mobilepushshort}}** auf **Erstellen** klicken.

   2. Geben Sie Ihren Servicenamen ein und klicken Sie auf **Erstellen**.

   3. Für Android: [Firebase Cloud Messaging konfigurieren ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](/docs/services/mobilepush/t_push_provider_android.html "Symbol für externen Link"){: new_window}.
   
4. Optional: Fügen Sie die Analytics-Funktion hinzu.

   1. Klicken Sie auf der Seite **Projektübersicht** für **Analytics** auf **Hinzufügen**.

      Alternativ können Sie auf der Seite **Analytics** auf **Erstellen** klicken.

   2. Geben Sie Ihren Servicenamen ein und klicken Sie auf **Erstellen**.
   
   3. Inaktivieren Sie den Demo-Modus, um Ihre Analysedaten nach Ausführung der App anzuzeigen.
   
   4. Weitere Informationen zum Konfigurieren von Analytics finden Sie unter [Einführung in {{site.data.keyword.mobileanalytics_short}} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](/docs/services/mobileanalytics/index.html "Symbol für externen Link"){: new_window}.
  
5. Optional: Fügen Sie die Authentication-Funktion hinzu.

   1. Klicken Sie auf der Seite **Projektübersicht** für **Authentication** auf **Hinzufügen**.

      Alternativ können Sie auf der Seite **Authentication** die Option **Erstellen** auswählen.

   2. Geben Sie Ihren Servicenamen ein und klicken Sie auf **Erstellen**.
   
   3. Wechseln Sie zu **Authentication**.
   
   4. Wählen Sie Ihren Identitätsprovider aus und geben Sie für dessen Konfiguration die erforderlichen Informationen ein. Sie können nur einen einzigen Identitätsprovider aktivieren.

   5. Weitere Informationen zum Konfigurieren der Authentifizierung finden Sie unter [Einführung in {{site.data.keyword.amashort}} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](/docs/services/mobileaccess/index.html "Symbol für externen Link"){: new_window}.

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
* [Lernprogramm - {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [Lernprogramm - {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [Lernprogramm - Watson Language](tutorial_watson_language.html)
* [Lernprogramm - Weather](tutorial_weather.html)
