---

copyright:
  years: 2016
lastupdated: "2016-10-21"

---
{:new_window: target="_blank"}

# Lernprogramm - Code-Starter für Watson Language
{: #tutorial_watson_language}

Der {{site.data.keyword.Bluemix}} Mobile-Code-Starter für Watson Language veranschaulicht die Services 'Text To Speech' und 'Language Translation' von Watson und bietet Ihnen Integrationspunkte für jeden der {{site.data.keyword.Bluemix_notm}} Mobile-Services.


## Voraussetzungen
{: #tutorial_requirements}

* Ein [Bluemix](http://bluemix.net)Konto
* Vom [Bluemix Catalog](https://console.{DomainName}/catalog/) abgerufene [Language Translator](https://console.{DomainName}/catalog/services/language-translator/)- und [Text to Speech](https://console.{DomainName}/catalog/services/text-to-speech/)-Serviceinstanzen


## Einführung
{: #tutorial_gs}

Zur schnellen Einrichtung und Ausführung mit dem Code-Starter für Watson Language befolgen Sie diese Schritte:

1. Erstellen Sie ein Mobile-Dashboard-Projekt in {{site.data.keyword.Bluemix_notm}}.

   1. Klicken Sie auf der Seite **Einführung** des Mobile-Dashboards auf **Projekt erstellen**.

      Alternativ können Sie auf der Seite **Projekte** auf **Projekt erstellen** klicken.

   2. Klicken Sie auf **Code-Starter**.

   3. Wählen Sie **Watson Language** aus und klicken Sie auf **Projekt erstellen**.

   4. Geben Sie Ihren Projektnamen ein und klicken Sie auf **Erstellen**.

2. Optional: Fügen Sie die Push Notifications-Funktion hinzu.

   1. Klicken Sie auf der Seite **Projektübersicht** für **Push Notifications** auf **Hinzufügen**.

      Alternativ können Sie auf der Seite **Push Notifications** auf **Erstellen** klicken.

   2. Geben Sie Ihren Servicenamen ein und klicken Sie auf **Erstellen**.

   3. Unter iOS [konfigurieren Sie den Apple-Service 'Push Notification'](/docs/services/mobilepush/t_push_provider_ios.html){: new_window}.

   4. Unter Android [konfigurieren Sie Google Cloud Messaging](/docs/services/mobilepush/t_push_provider_android.html){: new_window}.
   
3. Optional: Fügen Sie die Analytics-Funktion hinzu.

   1. Klicken Sie auf der Seite **Projektübersicht** für **Analytics** auf **Hinzufügen**.

      Alternativ können Sie auf der Seite **Analytics** auf **Erstellen** klicken.

   2. Geben Sie Ihren Servicenamen ein und klicken Sie auf **Erstellen**.
   
   3. Inaktivieren Sie den Demo-Modus, um Ihre Analysedaten nach Ausführung der App anzuzeigen.

4. Optional: Fügen Sie die Authentication-Funktion hinzu.

   1. Klicken Sie auf der Seite **Projektübersicht** für **Authentication** auf **Hinzufügen**.

      Alternativ können Sie auf der Seite **Authentication** die Option **Erstellen** auswählen.

   2. Geben Sie Ihren Servicenamen ein und klicken Sie auf **Erstellen**.
   
   3. Wechseln Sie zu **Authentication**.
   
   4. Wählen Sie Ihren Identitätsprovider aus und geben Sie für dessen Konfiguration die erforderlichen Informationen ein. Sie können nur einen einzigen Identitätsprovider aktivieren.

   5. Weitere Informationen zur Konfiguration von Authentication finden Sie in der [Einführung zu Mobile Client Access](/docs/services/mobileaccess/index.html){: new_window}.

5. Laden Sie Ihr Projekt herunter.

   1. Klicken Sie auf **Code** und wählen Sie Ihre bevorzugte Sprache aus.

   2. Klicken Sie auf **Code herunterladen**.

6. Extrahieren Sie das Archiv und zeigen Sie die `README.md`-Datei in einem Markdown-Viewer an, um die Einrichtung zu beenden.


## Nächste Schritte
{: #tutorial_next}

[Testen Sie Ihre App!](http://console.{DomainName}/mobile/create-project?starter=512568a1-72db-35c7-b9c4-4f3e3bc89375){: new_window}
