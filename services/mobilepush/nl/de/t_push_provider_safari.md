
---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
# Berechtigungsnachweise für Safari-Web-Browser generieren
{: #configure-credential-for-safari}
Letzte Aktualisierung: 15. November 2016
{: .last-updated}

Der IBM Service {{site.data.keyword.mobilepushshort}} verfügt nun über erweiterte Funktionen zum Senden von Benachrichtigungen an Ihren Safari-Browser. 

Stellen Sie sicher, dass Sie über ein Apple Developer-Konto verfügen. Sie müssen eine 'Website Push ID' registrieren und ein Zertifikat generieren, um Ihren Safari-Browser für den Empfang von Benachrichtigungen zu konfigurieren. Führen Sie zur Einführung die folgenden Schritte aus.

1. Klicken Sie im Apple Developer Member Center auf **Certificates, ID & Profiles**. 
2. Klicken Sie auf **Identifiers** und anschließend auf **Website Push IDs**.
3. Erstellen Sie durch Auswahl des Plussymbols einen neuen Eintrag.
  ![Push-Dashboard](images/safari_1.jpg)

4. Geben Sie in der Anzeige 'Register Website Push ID' eine entsprechende Beschreibung der Website Push ID sowie eine ID an. Es ist empfehlenswert, das Namensformat für reverse Domänen zu verwenden, das mit 'web' beginnt. Beispiel: web.com.example.dailyweatherreports.
5. Registrieren Sie die 'Website Push ID'.
6. Wählen Sie **Edit** aus, um die 'Website Push ID' zu aktualisieren.
7. Geben Sie im Fenster 'Certificate Assistant' als Zertifikatsinformationen Ihre E-Mail-ID und einen allgemeinen Namen an. Lassen Sie das Feld für die E-Mail-Adresse der Zertifizierungsstelle leer.
8. Klicken Sie auf **Save to disk** und wählen Sie **Continue** aus.
9. Wählen Sie für die Speicherung des Zertifikats einen entsprechenden Ordner aus.

 
