
---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
# Berechtigungsnachweise für Apple Push Notification-Service (APNs) konfigurieren

{: #create-push-credentials-apns}

Apple Push Notification-Service (APNs) ermöglicht dem Anwendungsentwickler das Senden ferner Benachrichtigungen aus der Push Service-Instanz in Bluemix (dem Provider) an iOS-Einheiten und -Anwendungen. Die Nachrichten werden an eine Zielanwendung in dem Gerät gesendet. Rufen Sie die Berechtigungsnachweise für Ihren APNs ab und konfigurieren Sie sie. Berechtigungsnachweise von APNs werden von Push Notifications Service sicher verwaltet und sie werden verwendet, um die Verbindung zum APNs-Server als Provider herzustellen.

1. Fordern Sie ein [Apple Developers](https://developer.apple.com/)-Konto an.
2. [Registrieren Sie eine App-ID](#create-push-credentials-apns-register).
3. [SSL-Zertifikat zum Entwickeln und Verteilen von APNs erstellen](#create-push-credentials-apns-ssl)
4. [Erstellen Sie ein Entwicklungsbereitstellungsprofil](#create-push-credentials-dev-profile).
5. [Erstellen Sie ein Bereitstellungsprofil für Store-Verteilung](#create-push-credentials-apns-distribute_profile).
6. [Richten Sie APNs im Push-Dashboard ein](#create-push-credentials-apns-dashboard).



##App-IDs registrieren
{: #create-push-credentials-apns-register}


Die App-ID (Bundle-ID) ist eine eindeutige Kennung für eine bestimmte Anwendung. Für jede Anwendung ist eine App-ID erforderlich. Services wie Push Notifications Service werden für die App-ID konfiguriert.




1. Rufen Sie das [Apple Developer](https://developer.apple.com)-Portal auf, klicken Sie auf **Member Center** und wählen Sie **Certificates, Identifiers & Profiles** aus.
2. Navigieren Sie zum Abschnitt **Registering App IDs** der [Apple Developer Library](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html#//apple_ref/doc/uid/TP40012582-CH30-SW991) und befolgen Sie die Anweisungen zum Registrieren der App-ID.

	**Hinweis**: Wählen Sie beim Registrieren einer App-ID die folgenden Optionen aus:
	* Push Notifications

	![App Services](images/appID_appservices_enablepush.jpg)

	* Explicit ID Suffix

	![Explizite ID](images/appID_bundleID.jpg)
3. Nächste Schritte: SSL-Zertifikat zum Entwickeln und Verteilen von APNs erstellen.

##SSL-Zertifikat zum Entwickeln und Verteilen von APNs erstellen
{: #create-push-credentials-apns-ssl}

Vor dem Anfordern eines APNs-Zertifikats müssen Sie zunächst eine Zertifikatssignieranforderung (Certificate Signing Request, CSR) generieren und an die Apple-Zertifizierungsstelle (Certificate Authority, CA) abschicken. Die CSR enthält Informationen zum Identifizieren Ihres Unternehmens sowie Ihren öffentlichen und Ihren privaten Schlüssel, den Sie zum Signieren Ihrer Apple-Push-Benachrichtigungen verwenden. Generieren Sie anschließend das SSL-Zertifikat in iOS Developer Portal. Das Zertifikat mit dem zugehörigen öffentlichen und privaten Schlüssel wird in Keychain Access gespeichert.

**Vorbemerkungen**

[Registrieren Sie eine App-ID](#create-push-credentials-apns-register).

APNs kann im Sandboxmodus oder im Produktionsmodus verwendet werden.

* Der Sandboxmodus wird zum Entwickeln und Testen verwendet.
* Der Produktionsmodus wird beim Verteilen von Anwendungen über den App
Store (oder über die Verteilungsmechanismen anderer Unternehmen) verwendet.

Sie müssen separate Zertifikate für Ihre Entwicklungs- und Verteilungsumgebungen anfordern. Die Zertifikate werden einer App-ID für die App zugeordnet, die der Empfänger für ferne Benachrichtigungen ist. Für die Produktion können Sie bis zu zwei Zertifikate erstellen. Bluemix verwendet diese Zertifikate, um eine SSL-Verbindung mit APNs herzustellen.

Erstellen Sie ein SSL-Zertifikat zum Entwickeln und Verteilen.


1. Rufen Sie das [Apple Developer](https://developer.apple.com)-Portal auf, klicken Sie auf **Member Center** und wählen Sie **Certificates, Identifiers & Profiles** aus.
2. Klicken Sie im Bereich **Identifiers** auf **App IDs**.
3. Wählen Sie in der Liste Ihrer App-IDs zunächst die neu erstellte App-ID und anschließend **Settings** aus.
4. Erstellen Sie im Bereich **Push Notifications** zunächst ein SSL-Zertifikat für Entwicklung und anschließend ein SSL-Zertifikat für Produktion.
 
	![SSL-Zertifikate für Push Notifications](images/certificate_createssl.jpg)

	Die Anzeige 'About Creating a Certificate a Signing Request' wird angezeigt.

	![Signieranforderung für ein Zertifikat erstellen](images/request.jpg)

5. Starten Sie auf Ihrem Mac-Computer die Anwendung **Keychain Access**, um eine Zertifikatssignieranforderung (Certificate Signing Request, CSR) zu erstellen.
6. Wählen Sie **Keychain Access > Certificate Assistant > Request a Certificate From a Certificate Authority…** aus ![Keychain Access](images/keychain_request_certificate.jpg).
7. Geben Sie unter **Certificate Information** die E-Mail-Adresse ein, die Ihrem App Developer-Konto zugeordnet ist, sowie einen allgemeinen Namen. Verwenden Sie einen aussagefähigen Namen, der erkennen lässt, ob es sich um ein Zertifikat für die Entwicklung (Sandbox) oder für die Verteilung (Produktion) handelt (z. B. **sandbox-apns-zertifikat** oder **produktions-apns-zertifikat**. 

8. Wählen Sie die Option **Saved to disk ** aus, um die Datei **.certSigningRequest** auf Ihren Desktop herunterzuladen, und klicken Sie anschließend auf **Continue**.
9. Geben Sie unter **Save As** einen Namen für die Datei **.certSigningRequest**
an (z. B. **sandbox.certSigningRequest**) und klicken Sie anschließend auf **Save**.
10. Klicken Sie auf **Done**. Sie haben eine CSR erstellt.
11. Klicken Sie in der Anzeige **About Creating a Certificate a Siging Request (CSR)** auf **Continue**. 12. ![Certificate a Siging Request](images/request.jpg)
12. Klicken Sie in der Anzeige **Generate** auf die Option **Choose File ... ** und wählen Sie die CSR-Datei aus, die Sie auf Ihrem Desktop gespeichert haben. Klicken Sie anschließend auf **Generate**. 

	![Zertifikat generieren](images/generate_certificate.jpg)

13. Nachdem das Zertifikat erstellt wurde, klicken Sie auf **Done**.
14. Klicken Sie in der Anzeige **Push Notifications** auf **Download**, um Ihr Zertifikat herunterzuladen, und klicken Sie anschließend auf **Done**. ![Download certificate](images/certificate_download.jpg)
15. Navigieren Sie auf Ihrem Mac-Computer zu **Keychain Access > My Certificates** und suchen Sie nach dem neu installierten Zertifikat. Doppelklicken Sie auf das Zertifikat, damit es in Keychain Access installiert wird.
16. Wählen Sie das Zertifikat und den privaten Schlüssel aus und klicken Sie anschließend auf **Export**, um das Zertifikat in das Format zum Austauschen personenbezogener Daten (.p12) umzuwandeln.

	![Zertifikat und Schlüssel exportieren](images/keychain_export_key.jpg)

17. Geben Sie im Feld **Save As** einen aussagefähigen Namen für das Zertifikat an, um die spätere Identifizierung zu erleichtern (z. B. **sandbox-apns.p12-zertifikat** oder **produktion_apns.p12**) und klicken Sie anschließend auf **Save**.

   	![Zertifikat und Schlüssel exportieren](images/certificate_p12v2.jpg)

18. Geben Sie im Feld **Enter a password** ein Kennwort zum Schützen der exportierten Elemente ein und klicken Sie anschließend auf **OK**. Dieses Kennwort verwenden Sie später, um Ihre APNs-Einstellungen im Push-Dashboard zu konfigurieren.

	![Zertifikat und Schlüssel exportieren](images/export_p12.jpg)
19. **Key Access.app** fordert Sie zum Exportieren Ihres Schlüssels aus der Anzeige **Keychain** auf. Geben Sie Ihr Administratorkennwort für Ihren Mac-Computer ein, um den Export dieser Elemente zuzulassen, und wählen Sie anschließend die Option **Always Allow** aus. Auf Ihrem Desktop wird ein .p12-Zertifikat erstellt.


##Entwicklungsbereitstellungsprofil erstellen
{: #create-push-credentials-dev-profile}

Das Bereitstellungsprofil ermittelt anhand der App-ID, auf welchen Geräten Ihre App installiert und ausgeführt werden kann und auf welche Services die App zugreifen kann. Sie erstellen für jede App-ID zwei Bereitstellungsprofile, eines für die Entwicklung und das zweite für die Verteilung. Xcode ermittelt anhand des Entwicklungsbereitstellungsprofils, welche Entwickler den Build für die App durchführen dürfen und welche Geräte in der Anwendung
getestet werden dürfen.

**Vorbemerkungen**

Stellen Sie sicher, dass die App-ID registriert, für Push Notifications Service aktiviert und für die Verwendung eines APNs-SSL-Zertitikats für Entwicklung und Produktion konfiguriert wurde.

Erstellen Sie ein Entwicklungsbereitstellungsprofil.

1. Rufen Sie das [Apple Developer](https://developer.apple.com)-Portal auf, klicken Sie auf **Member Center** und wählen Sie **Certificates, Identifiers & Profiles** aus.
2. Rufen Sie die Website für [Mac Developer Library](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html#//apple_ref/doc/uid/TP40012582-CH30-SW62site) auf, navigieren Sie zum Abschnitt **Creating Development Provisioning Profiles** und befolgen Sie die Anweisungen zum Erstellen eines Entwicklungsprofils.

	**Hinweis**: Wählen Sie beim Konfigurieren eines Entwicklungsbereitstellungsprofils die folgenden Optionen aus:
	* **iOS App Development**
	* **For iOS and watchOS apps **



##Bereitstellungsprofil für Store-Verteilung erstellen
{: #create-push-credentials-apns-distribute_profile}

Mithilfe des Store-Bereitstellungsprofils können Sie Ihre App für die Verteilung
an den App-Store übergeben.

1. Rufen Sie das [Apple Developer](https://developer.apple.com)-Portal auf, klicken Sie auf **Member Center** und wählen Sie **Certificates, Identifiers & Profiles** aus.
2. Doppelklicken Sie auf das heruntergeladene Bereitstellungsprofil, um das Profil in Xcode zu installieren.

##APNs im Push Notification-Dashboard einrichten
{: #create-push-credentials-apns-dashboard}

Um mit Push Notifications Service Benachrichtigungen senden zu können, laden Sie die SSL-Zertifikate hoch, die für Apple Push Notification Service (APNs) erforderlich sind. Sie können auch die REST-API verwenden, um ein APNs-Zertifikat hochzuladen.


**Vorbemerkungen**


Rufen Sie Ihr APNs-SSL-Zertifikat für die Entwicklung und für die Produktion sowie das zugehörige Kennwort für jedes dieser Zertifikate ab. Informationen hierzu finden Sie in 'Push-Berechtigungsnachweise für APNs erstellen und konfigurieren'.

Die für den APNs benötigten Zertifikate sind .p12-Zertifikate, die den privaten Schlüssel und die SSL-Zertifikate enthalten, die zum Erstellen und Veröffentlichen der Anwendung erforderlich sind. Sie müssen die Zertifikate über das Member Center der Apple Developer-Website (wofür Sie ein gültiges Apple Developer-Konto benötigen) generieren. Für die Entwicklungsumgebung (Sandbox) und die Produktionsumgebung (Verteilung) sind unterschiedliche Zertifikate erforderlich.

**Hinweis**:Nachdem die .**cer** in Ihrem Keychain Access vorhanden sind, exportieren Sie sie auf Ihren Computer, um ein .p12-Zertifikat zu erstellen.

Weitere Informationen zur Verwendung des APNs finden Sie in der Veröffentlichung [iOS Developer Library: Local and Push Notification Programming Guide](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ProvisioningDevelopment.html#//apple_ref/doc/uid/TP40008194-CH104-SW4).

Richten Sie APNs im Push-Dashboard ein.

1. Öffnen Sie Ihre Back-End-Anwendung im Bluemix-Dashboard und klicken Sie anschließend auf den **IBM Push Notifications**-Service, um das Push-Dashboard zu öffnen.

	![IBM Push Notifications](images/bluemixdashboard_push.jpg)

	Das Push-Dashboard wird angezeigt.
	
	![Push-Benachrichtigungen festlegen](images/wizard.jpg)
1
2. Navigieren Sie auf der Registerkarte **Konfiguration** zum Abschnitt **Apple-Push-Zertifikat**, wählen Sie **Sandbox** (Entwicklung) oder **Produktion** (Verteilung) aus und laden Sie das p12-Zertifikat in Bluemix hoch.

	![Push-Benachrichtigungen festlegen](images/credential_screen.jpg)
3. Geben Sie in das Feld **Kennwort** das zugehörige Kennwort für die **.p12**-Zertifikatsdatei ein und klicken Sie anschließend auf **Speichern**. Nachdem die Zertifikate erfolgreich mit einem gültigen Kennwort hochgeladen wurden, können Sie mit dem Senden von Benachrichtigungen beginnen.

