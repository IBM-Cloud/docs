
---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
# Berechtigungsnachweise für Google Cloud Messaging (GCM) konfigurieren
{: #create-push-enable-gcm}
Letzte Aktualisierung: 16. August 2016
{: .last-updated}

Rufen Sie Ihre Berechtigungsnachweise für Google Cloud Messaging (GCM) ab und richten Sie anschließend den {{site.data.keyword.mobilepushshort}}-Service im Push-Dashboard ein. 

##Absender-ID und API-Schlüssel abrufen

Der API-Schlüssel wird geschützt gespeichert und vom {{site.data.keyword.mobilepushshort}}-Service für die Verbindungsherstellung zum GCM-Server verwendet. Die Absender-ID (Projektnummer) wird vom Android-SDK auf der Clientseite verwendet. Weitere Informationen zur Absender-ID finden Sie unter [Google Cloud Messaging](https://developers.google.com/cloud-messaging/gcm#arch).

1. Richten Sie ein Google Development-Konto unter [Google Dev Console](https://console.developers.google.com/start){: new_window} ein. Weitere Informationen zu Google Cloud Messaging (GCM) finden Sie in [Creating a Google API Project](https://developers.google.com/console/help/new/){: new_window}.

2. Erstellen Sie in Google Developers Console ein neues Projekt. Beispiel: "hello world".

![Projekt erstellen](images/gcm_createproject.jpg)

3. Geben Sie in das Feld **Project name** (Projektname) den Namen für Ihr Projekt ein und klicken Sie anschließend auf die Schaltfläche **Create** (Erstellen).
4. Klicken Sie auf **Home** (Ausgangsposition), um die Projektnummer anzuzeigen. Notieren Sie Ihre Projektnummer.

![GCM-Projektnummer](images/gcm_projectnumber.jpg)

	**Hinweis**: Wenn Sie ein eigenes Projekt erstellen, wird eine Projektnummer (Absender-ID) erstellt. Verwenden Sie diese Nummer zum Einrichten von Push Notifications Service in der Anzeige des Push-Dashboards.

5. Klicken Sie auf **APIs & Auth** (APIs & Authentifizierung) und klicken Sie im Bereich **Mobile APIs** auf die Option **Cloud Messaging for Android**.

![APIs](images/gcm_mobileapi.jpg)

6. Klicken Sie auf **APIs** und anschließend auf die Schaltfläche **Enable API** (API aktivieren), um den API-Schlüssel für Ihr Projekt zu erstellen. 

![API aktivieren](images/gcm_enable_api.jpg)

7. Rufen Sie die Anzeige **APIs & Auths -> Credentials** (APIs & Authentifizierung -> Berechtigungsnachweise) auf. Klicken Sie auf **Add Credentials** (Berechtigungsnachweise hinzufügen) und anschließend auf **API Key** (API-Schlüssel).

![API-Berechtigungsnachweise](images/api_credentials.jpg)

8. Klicken Sie auf die Option **Server Key** (Serverschlüssel), um einen GCM-API-Schlüssel zu generieren, den Sie im Bluemix-Push-Dashboard verwenden können.
9. Geben Sie in das Feld **Name** den Namen für den Server-API-Schlüssel ein.

![GCM-Serverschlüssel](images/gcm_serverkey.jpg)

10. Klicken Sie auf die Schaltfläche **Create** (Erstellen). 
Der API-Schlüssel wird angezeigt.

![GCM-API-Schlüssel](images/gcm_apikey.jpg)

11. Kopieren Sie Ihren GCM-API-Schlüssel und klicken Sie anschließend auf die Schaltfläche **OK**. Sie benötigen die Projektnummer (Absender-ID) und den API-Schlüssel, um Ihre Berechtigungsnachweise in der Konfigurationsanzeige im Dashboard für Bluemix-Push-Benachrichtigungen zu konfigurieren. 


##{{site.data.keyword.mobilepushshort}}-Service für Android einrichten

###Vorbemerkungen
{: before-you-begin}

Rufen Sie einen GCM-API-Schlüssel und eine Absender-ID (Projektnummer) ab. 

1. Öffnen Sie Ihre Back-End-Anwendung im Bluemix-Dashboard und klicken Sie anschließend auf den Service 'IBM {{site.data.keyword.mobilepushshort}}', um das Dashboard zu öffnen. 
 
![Push-Dashboard](images/bluemixdashboard_push.jpg)

Das Push-Dashboard wird angezeigt.
	
![Push-Einrichtung](images/setup_push_main.jpg)
Um einen nicht gebundenen {{site.data.keyword.mobilepushshort}}-Service für Android einzurichten, wählen Sie das Symbol für 'Nicht gebundener Service' für Push-Benachrichtigungen aus, um das Dashboard für den {{site.data.keyword.mobilepushshort}}-Service zu öffnen. 
 
	![Push-Dashboard](images/push_unbound.jpg)

2. Klicken Sie auf die Schaltfläche **Push einrichten**, um die GCM-Berechtigungsnachweise zu konfigurieren.
1. Konfigurieren Sie auf der Registerkarte **Konfiguration** im Abschnitt **Google Cloud Messaging** die Absender-ID (GCM-Projektnummer) und den API-Schlüssel.

4. Klicken Sie auf die Schaltfläche **Speichern**. 
5. Nächste Schritte: [Benachrichtigungen für Android aktivieren](c_enable_push.html).


##Nicht gebundenen {{site.data.keyword.mobilepushshort}}-Service für Android erstellen 

###Vorbemerkungen
{: before-you-begin}

Erstellen Sie eine Instanz des {{site.data.keyword.mobilepushshort}}-Service. Sie können die Instanz des {{site.data.keyword.mobilepushshort}}-Service ohne Bindung an jegliche Back-End-Anwendung verwenden. 

1. Binden Sie die Instanz des {{site.data.keyword.mobilepushshort}}-Service an eine Bluemix-Anwendung. Durch das Binden werden alle Details im Zusammenhang mit dem Service, die in JSON-Format in der Umgebungsvariablen 'VCAP_SERVICES' gespeichert sind, sichtbar.  

![Binden eines Service für Push-Benachrichtigungen](images/unbound_1.jpg)
 
2. Klicken Sie auf **Binden** und wählen Sie die Instanz des {{site.data.keyword.mobilepushshort}}-Service aus, die gebunden werden soll. Nachdem Ihre Anwendung an den {{site.data.keyword.mobilepushshort}}-Service gebunden worden ist, werden die Informationen zum Service in JSON-Format in der Umgebungsvariablen 'VCAP_SERVICES' für Ihre App gespeichert. Beispiel: 

```
{
   "imfpush_Dev": [
   {
         "name": "neekrish_20JulUnbound",
         "label": "imfpush_Dev",
         "plan": "Basic",
         "credentials": null
      }
   ]
}
```
