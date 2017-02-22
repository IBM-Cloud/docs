---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Berechtigungsnachweise für Web-Browser konfigurieren
{: #configure-credential-for-browsers}
Letzte Aktualisierung: 11. Januar 2017
{: .last-updated}

Der IBM Service {{site.data.keyword.mobilepushshort}} verfügt nun über erweiterte Funktionen zum Senden von Benachrichtigungen an Ihren Browser. 

Die Website-URL oder der Domänenname Ihrer Website wird vom {{site.data.keyword.mobilepushshort}}-Service benötigt, um die Anforderungen zu identifizieren, die zugelassen werden müssen. Jede Instanz des {{site.data.keyword.mobilepushshort}}-Service unterstützt nur einen Domänennamen. Stellen Sie daher sicher, dass für Chrome, Firefox und Safari der gleiche Wert festgelegt ist. 

In Chrome- und Safari-Browsern sind zusätzliche Konfigurationsschritte für Web-Push erforderlich. Sie benötigen einen FCM-API-Schlüssel, da Nachrichten in Chrome über einen FCM-Endpunkt gesendet werden. Informationen zum Abrufen Ihres FCM-API-Schlüssels finden Sie im Abschnitt [Berechtigungsnachweise für FCM generieren](t_push_provider_android.html).



##Web-Push für Chrome und Firefox konfigurieren 
{: #config-chrome-firefox}

1. Wählen Sie in der Push-Dashboardanzeige **Konfigurieren** aus.
2. Wählen Sie die Webregisterkarte aus.	![WebPush-Konfigurationen](images/webpush_configure.jpg)
3. Konfigurieren Sie den FCM/GCM-API-Schlüssel und die URL Ihrer Webseite, die für den Empfang von Push-Benachrichtigungen registriert wird.
4. Klicken Sie auf **Speichern**.
5. Nächste Schritte: [Benachrichtigungen für Google Chrome- und Mozilla Firefox-Browser aktivieren](c_enable_push.html).


## Web-Push für Safari konfigurieren 
{: #configure-safari}

Für den {{site.data.keyword.mobilepushshort}}-Service wird die Version Safari 10.0 unterstützt. Sie müssen zunächst über Ihr Apple Developer-Konto ein Zertifikat generieren, bevor Sie Ihren Browser für den Empfang von Benachrichtigungen konfigurieren.

### Zertifikat generieren
{: #certificate-generation}

Stellen Sie sicher, dass Sie über ein Apple Developer-Konto verfügen. Sie müssen eine 'Website Push ID' registrieren und ein Zertifikat generieren, um Ihren Safari-Browser für den Empfang von Benachrichtigungen zu konfigurieren. Führen Sie zur Einführung die folgenden Schritte aus.

1. Klicken Sie im Apple Developer Member Center auf **Certificates, ID & Profiles**. 
2. Klicken Sie auf **Identifiers** und anschließend auf **Website Push IDs**.
3. Erstellen Sie durch Auswahl des Plussymbols einen neuen Eintrag.
  ![Push-Dashboard](images/safari_1.jpg)

4. Geben Sie in der Anzeige 'Register Website Push ID' eine entsprechende Beschreibung der Website Push ID sowie eine ID an. Es ist empfehlenswert, das Namensformat für reverse Domänen zu verwenden, das mit 'web' beginnt. Beispiel: web.com.example.dailyweatherreports.
5. Registrieren Sie die 'Website Push ID'. Sie haben jetzt Ihre Website Push ID 
6. Wählen Sie **Edit** aus, um ein Zertifikat für die Verwendung für die Website Push ID zu erstellen.
7. Geben Sie im Fenster 'Certificate Assistant' als Zertifikatsinformationen Ihre E-Mail-ID und einen allgemeinen Namen an. Lassen Sie das Feld für die E-Mail-Adresse der Zertifizierungsstelle leer.
8. Klicken Sie auf **Save to disk** und wählen Sie **Continue** aus.
9. Wählen Sie für die Speicherung des Zertifikats einen entsprechenden Ordner aus.
10. Wählen Sie die auf der Platte erstellte Datei `.certSigningRequest` aus, wenn Sie vom Assistenten zum Generieren des Zertifikats aufgefordert werden. Stellen Sie sicher, dass Sie das im `.cer`-Format erstellte Website-Push-Zertifikat herunterladen.
11. Öffnen Sie das Zertifikat im Tool KeyChain Access. Klicken Sie mit der rechten Maustaste und exportieren Sie es als p12-Zertifikat. Beachten Sie das während der Generierung des p12-Zertifikats bereitgestellte Kennwort.


### Für Benachrichtigungen konfigurieren
  {: #configuration-notification}
 
Nach dem Generieren des Zertifikats können Sie den Service für das Senden von Benachrichtigungen an Safari konfigurieren. 

Führen Sie die folgenden Schritte aus:

1. Klicken Sie im Dashboard des Push Notifications-Service auf **Configure**. 
2. Wählen Sie die Webregisterkarte aus. 
3. Aktualisieren Sie im Abschnitt 'Safari Push' das Formular mit den erforderlichen Informationen. 
	- **Website Name**: Dies ist der Name, den Sie im Benachrichtigungscenter angegeben haben.
	- **Website Push ID**: Aktualisieren Sie den Wert durch die umgekehrte Zeichenfolge der Domäne für Ihre Website Push ID. Beispiel: web.com.example.www.
	- **Website URL**: Geben Sie die URL der Website für die Subskription von Push-Benachrichtigungen an. Beispiel: https://www.example.com.
	- **Allowed Domains**: Dies ist ein optionaler Parameter. Dies ist die Liste der Websites, die eine Berechtigung vom Benutzer anfordern. Stellen Sie sicher, dass es sich bei den URLs um durch Kommas getrennte Werte handelt. Beachten Sie, dass der Wert für die Website-URL verwendet wird, wenn an dieser Stelle nichts angegeben wird. 
	- **URL Format String**: Die URL für die Auflösung, wenn die Benachrichtigung angeklickt wird. Beispiel: ["https://www.example.com"]. Stellen Sie sicher, dass die URL das Schema http oder https verwendet.
	- **Safari web push certificate**: Laden Sie das .p12-Zertifikat hoch und geben Sie ein Kennwort an.
4. Klicken Sie auf **Speichern**.	

![Push-Dashboard](images/push_configure_safari.jpg)	

Sie können jetzt Push-Benachrichtigungen an den Safari-Browser senden.

	
