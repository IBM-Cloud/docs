---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Berechtigungsnachweise für FCM generieren
{: #create-push-enable-gcm}
Letzte Aktualisierung: 16. Januar 2017
{: .last-updated}

Firebase Cloud Messaging (FCM) ist das Gateway, das für die Übermittlung von Push-Benachrichtigungen an Android-Geräte sowie an Google Chrome verwendet wird. FCM ist die neue Version von Google Cloud Messaging (GCM). Sie müssen Ihre FCM-Berechtigungsnachweise abrufen, um den {{site.data.keyword.mobilepushshort}}-Service im Dashboard einzurichen. Achten Sie darauf, für neue Apps FCM-Konfigurationen zu verwenden. Vorhandene Apps können mit GCM-Konfigurationen weiterhin betrieben werden.

##Absender-ID und API-Schlüssel abrufen
{: #android-senderid-apikey}

Der API-Schlüssel wird geschützt gespeichert und vom {{site.data.keyword.mobilepushshort}}-Service für die Verbindungsherstellung zum FCM-Server verwendet. Die Absender-ID (Projektnummer) wird vom Android-SDK und dem JS-SDK für Google Chrome und Mozilla Firefox auf der Clientseite verwendet. 

Zum Einrichten von FCM generieren Sie den API-Schlüssel und die Absender-ID und führen Sie folgende Schritte aus:

1. Rufen Sie die [Firebase-Konsole ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://console.firebase.google.com/?pli=1 "Symbol für externen Link"){: new_window} auf.
2. Wählen Sie **Neues Projekt erstellen** aus. 
3. Geben Sie im Fenster 'Projekt erstellen' einen Projektnamen ein, wählen Sie ein Land/eine Region aus und klicken Sie auf **Projekt erstellen**.
3. Klicken Sie im Navigationsfenster auf das Symbol 'Einstellungen' und wählen Sie **Projekteinstellungen** aus.
4. Wählen Sie die Registerkarte 'Cloud Messaging' aus, um einen Server-API-Schlüssel und eine Absender-ID zu generieren.

##{{site.data.keyword.mobilepushshort}}-Service für Android und Chrome Apps und Erweiterungen einrichten
{: #setup-push-android}

**Hinweis:** Sie benötigen Ihren FCM/GCM-API-Schlüssel und die Absender-ID (Projektnummer).

1. Öffnen Sie Ihr Bluemix-Dashboard und klicken Sie anschließend auf die von Ihnen erstellte Serviceinstanz von {{site.data.keyword.mobilepushfull}}, um das Dashboard zu öffnen. Das Push-Dashboard wird angezeigt. Um einen nicht gebundenen {{site.data.keyword.mobilepushshort}}-Service für Android einzurichten, wählen Sie das Symbol für 'Nicht gebundenen {{site.data.keyword.mobilepushshort}}-Service' aus, um das {{site.data.keyword.mobilepushshort}}-Servicedashboard anzuzeigen. 

![Push-Dashboard](images/push_unbound.jpg)

2. Klicken Sie auf die Schaltfläche **Push einrichten**, um die FCM/GCM-Berechtigungsnachweise für Android-Anwendungen und Google Chrome-Apps und Erweiterungen zu konfigurieren.
3. Für Android öffnen Sie auf der Seite **Konfiguration** die Registerkarte **Mobile** und konfigurieren Sie die Absender-ID (GCM-Projektnummer) und den API-Schlüssel. Für Google Chrome Apps und Erweiterungen öffnen Sie die Registerkarte **Web** und konfigurieren Sie die Absender-ID (FCM/GCM-Projektnummer) und den API-Schlüssel entsprechend.
4. Klicken Sie auf **Speichern**.
5. Nächste Schritte: [Benachrichtigungen für Android aktivieren](c_enable_push.html) oder [Benachrichtigungen für Google Chrome-Apps & Erweiterungen aktivieren](c_enable_push.html).


