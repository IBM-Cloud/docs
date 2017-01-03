---

copyright:
  years: 2016
lastupdated: "2016-10-21"

---
{:new_window: target="_blank"}

# Lernprogramm - Starter für Weather Code
{: #tutorial_weather}

Der {{site.data.keyword.Bluemix}} Mobile-Code-Starter für Weather veranschaulicht ein Gerüstprojekt als Einführung in die Arbeit mit Weather unter Verwendung von Swift. Außerdem enthält es die Push- und Analytics-Integrationspunkte.


## Voraussetzungen
{: #tutorial_requirements}

* Ein [Bluemix](http://bluemix.net)Konto
* Eine Serviceinstanz von [Weather Company Data](https://console.{DomainName}/catalog/services/weather-company-data/), die aus dem [Bluemix-Katalog](https://console.{DomainName}/catalog/) abgerufen wurde.


## Einführung
{: #tutorial_gs}

Zur schnellen Einrichtung und Ausführung mit dem Code-Starter für Weather befolgen Sie diese Schritte:

1. Erstellen Sie ein Mobile-Dashboard-Projekt in {{site.data.keyword.Bluemix_notm}}.

   1. Klicken Sie auf der Seite **Einführung** des Mobile-Dashboards auf **Projekt erstellen**.

      Alternativ können Sie auf der Seite **Projekte** auf **Neues Projekt** klicken.

   2. Klicken Sie auf **Code-Starter**.

   3. Wählen Sie **Weather** aus und klicken Sie auf **Projekt erstellen**.

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

5. Extrahieren Sie das Archiv und befolgen Sie die Anweisungen in der `README.md`-Datei.


## Nächste Schritte
{: #tutorial_next}

[Testen Sie Ihre App!](http://console.{DomainName}/mobile/create-project?starter=fad1d49e-f7b6-3aff-9b53-14673fca4399){: new_window}
