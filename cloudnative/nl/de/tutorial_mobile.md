---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Umfassendes Lernprogramm zum mobilen Basis-Starter (Mobile Basic Starter)
{: #tutorial}

Das folgende umfassende Lernprogramm führt Sie durch die Schritte zur Erstellung eines Projekts aus dem mobilen Basis-Starter (Mobile Basic Starter), inklusive der Tools, die Sie installiert haben müssen, sowie durch die Schritte zum Ausführen des Projekts in Xcode und Android Studio.


## Entwicklertools installieren
{: #dev_tools}

Stellen Sie sicher, dass die [vorausgesetzten Entwicklertools ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](get_code.html#prereq-dev-tools){: new_window} installiert sind.


## Projekt mit der {{site.data.keyword.dev_console}} erstellen
{: #create-devex}

1. Erstellen Sie ein {{site.data.keyword.dev_console}}-Projekt in {{site.data.keyword.Bluemix}}. 

   1. Klicken Sie auf der Seite **Einführung** in der {{site.data.keyword.dev_console}} auf **Projekt erstellen**.

      Alternativ können Sie auf der Seite **Projekte** auf **Projekt erstellen** klicken.

   2. Wählen Sie **Mobile App** aus und klicken Sie auf **Weiter**. 

   3. Wählen Sie **Basis** aus und klicken Sie auf **Weiter**. 

   4. Geben Sie Ihren Projektnamen ein. Verwenden Sie für dieses Lernprogramm `MobileBasicProject`. 

   5. Wählen Sie Ihre Plattform aus. Verwenden Sie für dieses Lernprogramm `Swift`.
   
   6. Klicken Sie auf **Erstellen**.

2. Optional: Fügen Sie die Authentication-Funktion hinzu.

   1. Klicken Sie auf der Seite **Projektübersicht** für **Authentication** auf **Hinzufügen**.

      Alternativ können Sie **Erstellen** oder **Vorhandenen hinzufügen** auf der Seite **Funktionen > Authentication** aus. 

   2. Geben Sie Ihren Servicenamen ein und klicken Sie auf **Erstellen**.
   
   3. Wechseln Sie zu **Authentication**.
   
   4. Wählen Sie Ihren Identitätsprovider aus und geben Sie für dessen Konfiguration die erforderlichen Informationen ein. Sie können nur einen einzigen Identitätsprovider aktivieren.
   
   5. Weitere Informationen zum Konfigurieren von Authentication finden Sie unter [Identitätsprovider konfigurieren} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](/docs/services/appid/identity-providers.html){: new_window}. 

3. Optional: Fügen Sie die Analytics-Funktion hinzu.

   1. Klicken Sie auf der Seite **Projektübersicht** für **Analytics** auf **Hinzufügen**.

      Alternativ können Sie auf der Seite **Funktionen > Analytics** auf **Erstellen** oder **Vorhandenen hinzufügen** klicken. 

   2. Geben Sie Ihren Servicenamen ein und klicken Sie auf **Erstellen**.
   
   3. Inaktivieren Sie den Demo-Modus, um Ihre Analysedaten nach Ausführung der App anzuzeigen.
   
   4. Weitere Informationen zum Konfigurieren von Analytics finden Sie unter [Einführung in {{site.data.keyword.mobileanalytics_short}} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](/docs/services/mobileanalytics/index.html){: new_window}.

4. Optional: Fügen Sie die {{site.data.keyword.mobilepushshort}}-Funktion hinzu.

   1. Klicken Sie auf der Seite **Projektübersicht** für **{{site.data.keyword.mobilepushshort}}** auf **Hinzufügen**.

      Alternativ können Sie auf der Seite **Funktionen > {{site.data.keyword.mobilepushshort}}** auf **Erstellen** oder **Vorhandenen hinzufügen** klicken. 

   2. Geben Sie Ihren Servicenamen ein und klicken Sie auf **Erstellen**.

   3. Für iOS: [Apple Push Notification Service konfigurieren ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](/docs/services/mobilepush/t_push_provider_ios.html){: new_window}.

   4. Für Android: [Firebase Cloud Messaging konfigurieren ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](/docs/services/mobilepush/t_push_provider_android.html){: new_window}.

5. Optional: Fügen Sie die Data-Funktion hinzu.

   1. Klicken Sie auf der Seite **Projektübersicht** für **Data** auf **Anzeigen**.

      Alternativ können Sie auf der Seite **Data** die Option **Erstellen** auswählen.
      
   2. Wählen Sie **{{site.data.keyword.cloudant_short_notm}}** oder **{{site.data.keyword.objectstorageshort}}** aus.

   3. Geben Sie Ihren Servicenamen ein und klicken Sie auf **Erstellen**.

   4. Weitere Informationen zum Konfigurieren von {{site.data.keyword.cloudant_short_notm}} finden Sie unter [Einführung in {{site.data.keyword.cloudant_short_notm}} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](/docs/services/Cloudant/index.html){: new_window}.

   5. Weitere Informationen zum Konfigurieren von {{site.data.keyword.objectstorageshort}} finden Sie unter [Einführung in {{site.data.keyword.objectstorageshort}} ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](/docs/services/ObjectStorage/index.html){: new_window}.

6. Generieren Sie den Projektcode.

   1. Klicken Sie auf der Seite **Projektübersicht** auf **Code abrufen**, um Ihre Sprache auszuwählen. 
   
      Alternativ können Sie auf die Seite **Code** klicken.
      
   2. Klicken Sie auf **Swift generieren**. 
   
   3. Wenn die Projektcodegenerierung fertig ist, klicken Sie auf **Swift herunterladen**, um Ihr Projektarchiv herunterzuladen. 

7. Optional: [Aktualisieren Sie das Projekt](project_overview_page.html#update_language), um eine neue Sprache zu generieren. 


## Projekt mit dem {{site.data.keyword.dev_cli_notm}} erstellen
{: #create-cli}

1. Stellen Sie sicher, dass das [{{site.data.keyword.dev_cli_short}}](dev_cli.html) installiert ist. 

2. Navigieren Sie in der Eingabeaufforderung des Terminals zu einem lokalen Verzeichnis Ihrer Wahl und führen Sie den folgenden Befehl aus. 

	```
	bx dev create
	```
	{: codeblock}
	
3. Geben Sie bei Aufforderung die folgenden Werte an: 

	* Wählen Sie ein Muster aus: 2 (für Mobil)
	* Wählen Sie einen Starter aus: 1 (für Basis)
	* Wählen Sie eine Plattform aus: 3 (für iOS Swift)
	* Geben Sie einen Namen für Ihr Projekt ein: `MobileBasicProjectCLI`

4. Wenn Sie Services zu Ihrem Projekt hinzufügen möchten, geben Sie `y` ein, wenn Sie in der Eingabeaufforderung danach gefragt werden, und beantworten Sie die restlichen Fragen. 

5. Navigieren Sie nach dem erfolgreichen Speichern des Projekts `MobileBasicProjectCLI` zum Ordner `MobileBasicProjectCLI/MobileBasicProjectCLI-Swift`. 


## Swift-Projekt in Xcode ausführen
{: #run_swift}

1. Extrahieren Sie die Datei `MobileBasicProject-Swift.zip`. 

2. Öffnen Sie die Datei `README.md` in einem Markdown-Viewer, um die Schritte zur Konfiguration Ihres Projekts zu überprüfen.

   1. Öffnen Sie Ihr Terminal und navigieren Sie zu Ihrem Projektordner.
   
      1. Führen Sie `pod setup` aus, wenn Sie Ihr CocoaPods-Repository einrichten müssen.
      
      2. Führen Sie `pod update` aus, wenn Sie Ihre bereits vorhandenen Pods aktualisieren müssen.
      
      3. Führen Sie `pod install` aus, um die Pods zu installieren, die für Ihr Projekt erforderlich sind.
      
   3. Öffnen Sie Ihren Xcode-Arbeitsbereich `BasicProject.xcworkspace`.
      
3. Führen Sie Ihre App aus.


## Cordova-Projekt in Xcode ausführen
{: #run_cordova_xcode}

1. Extrahieren Sie die Datei `MobileBasicProject-Cordova.zip`. 

2. Öffnen Sie die Datei `README.md` in einem Markdown-Viewer, um Ihr Projekt zu konfigurieren.

   1. Öffnen Sie Ihr `platforms/ios`-Projekt in Xcode.
      
3. Führen Sie Ihre App aus.


## Cordova-Projekt in Android Studio ausführen
{: #run_cordova_studio}

1. Extrahieren Sie die Datei `BasicProject-Cordova.zip`.

2. Öffnen Sie die Datei `README.md` in einem Markdown-Viewer, um Ihr Projekt zu konfigurieren.

   1. Öffnen Sie Ihr `platforms/android`-Projekt in Android Studio.
      
3. Führen Sie Ihre App aus.


## Android-Projekt in Android Studio ausführen
{: #run_android}

1. Extrahieren Sie die Datei `MobileBasicProject-Android.zip`. 

2. Öffnen Sie die Datei `README.md` in einem Markdown-Viewer, um Ihr Projekt zu konfigurieren.

   1. Öffnen Sie Ihr `BasicProject-Android`-Projekt in Android Studio.
      
3. Führen Sie Ihre App aus.
