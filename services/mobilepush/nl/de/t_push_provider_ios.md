---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Berechtigungsnachweise für APNs generieren
{: #create-push-credentials-apns}
Letzte Aktualisierung: 16. Januar 2017
{: .last-updated}

Apple Push Notification Service (APNs) ermöglicht Anwendungsentwicklern das Senden ferner Benachrichtigungen aus der Bluemix-Instanz des {{site.data.keyword.mobilepushshort}}-Service (d. h. dem Provider) an iOS-Geräte und -Anwendungen. Die Nachrichten werden an eine Zielanwendung auf dem Gerät gesendet. 

Rufen Sie Ihre APNs-Berechtigungsnachweise ab und konfigurieren Sie sie. Die APNs-Zertifikate werden vom {{site.data.keyword.mobilepushshort}}-Service sicher verwaltet und zum Herstellen einer Verbindung zum APNs-Server als Provider verwendet.

<!-- 1. Obtain an [Apple Developers ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.apple.com/){: new_window} account.-->

<!--2. [Register an App ID](#create-push-credentials-apns-register)
3. [Create a development and distribution APNs SSL certificate](#create-push-credentials-apns-ssl)
4. [Create a development provisioning profile](#create-push-credentials-dev-profile)
5. [Create a store distribution provisioning profile](#create-push-credentials-apns-distribute_profile)
6. [Creating .p12 push certificate file for Bluemix push](#create-p12-push-certificate-file-for-Bluemix-push)
7. [Set up APNs on the Push Dashboard](#create-push-credentials-apns-dashboard)
-->


##App-IDs registrieren
{: #create-push-credentials-apns-register}


Die App-ID (Bundle-ID) ist eine eindeutige Kennung für eine bestimmte Anwendung. Für jede Anwendung ist eine App-ID erforderlich. Services wie der {{site.data.keyword.mobilepushshort}}-Service werden für die App-ID konfiguriert.

1. Stellen Sie sicher, dass Sie über ein [Apple Developers-Konto ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.apple.com/){: new_window} verfügen.
2. Rufen Sie das [Apple Developer-Portal ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.apple.com){: new_window} auf, klicken Sie auf **Member Center** und wählen Sie **Certificates, Identifiers & Profiles** aus.
3. Navigieren Sie zum Abschnitt **Registering App IDs** der [Apple Developer Library ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html#//apple_ref/doc/uid/TP40012582-CH30-SW991){: new_window} und befolgen Sie die Anweisungen zum Registrieren der App-ID.

Wählen Sie beim Registrieren einer App-ID die folgenden Optionen aus:

* Push Notifications
![App Services](images/appID_appservices_enablepush.jpg)
* Explicit ID Suffix
![Explicit ID](images/appID_bundleID.jpg)
4. Erstellen Sie ein SSL-Zertifikat zum Entwickeln und Verteilen von APNs.

##SSL-Zertifikat zum Entwickeln und Verteilen von APNs erstellen
{: #create-push-credentials-apns-ssl}

Bevor Sie ein APNs-Zertifikat anfordern, müssen Sie zunächst eine Zertifikatssignieranforderung (Certificate Signing Request, CSR) generieren und an die Zertifizierungsstelle (Certificate Authority, CA) von Apple schicken. Die CSR enthält Informationen zum Identifizieren Ihres Unternehmens und beinhaltet Ihren öffentlichen sowie Ihren privaten Schlüssel, den Sie zum Signieren Ihrer Apple-Push-Benachrichtigungen verwenden. Generieren Sie anschließend das SSL-Zertifikat in iOS Developer Portal. Das Zertifikat mit dem zugehörigen öffentlichen und privaten Schlüssel wird in Keychain Access gespeichert.

<!-- ###Before you begin -->
<!-- {: before-you-begin-certificate} -->

<!--[Register an App ID](#create-push-credentials-apns-register)-->

Sie können APNs auf zwei Weisen verwenden: 

* Sandboxmodus zum Entwickeln und Testen.
* Produktionsmodus zum Verteilen von Anwendungen über den App
Store (oder über die Verteilungsmechanismen anderer Unternehmen.

Sie müssen separate Zertifikate für Ihre Entwicklungs- und Verteilungsumgebungen anfordern. Die Zertifikate werden einer App-ID für die App zugeordnet, die der Empfänger für ferne Benachrichtigungen ist. Für die Produktion können Sie bis zu zwei Zertifikate erstellen. Bluemix verwendet diese Zertifikate, um eine SSL-Verbindung mit APNs herzustellen.

<!-- Create a development and distribution SSL certificate. -->

1. Rufen Sie die [Apple Developer-Website ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.apple.com){: new_window} auf, klicken Sie auf **Member Center** und wählen Sie **Certificates, Identifiers & Profiles** aus.
2. Klicken Sie im Bereich **Identifiers** auf **App IDs**.
3. Wählen Sie in der Liste Ihrer App-IDs zunächst die <!--newly created--> App-ID und anschließend **Einstellungen** aus.
4. Erstellen Sie im Bereich **Push Notifications** zunächst ein SSL-Zertifikat für Entwicklung und anschließend ein SSL-Zertifikat für Produktion.

	![SSL-Zertifikate für Push Notifications](images/certificate_createssl.jpg)

5. Wenn die Anzeige zur Erstellung einer Zertifikatssignieranforderung (CSR) **About Creating a Certificate Siging Request (CSR)** angezeigt wird, starten Sie auf Ihrem Mac-Computer die Anwendung **Keychain Access**, um eine Zertifikatssignieranforderung (Certificate Signing Request, CSR) zu erstellen.
6. Wählen Sie im Menü **Keychain Access > Certificate Assistant > Request a Certificate From a Certificate Authority…** aus. 
7. Geben Sie unter **Certificate Information** die E-Mail-Adresse ein, die Ihrem App Developer-Konto zugeordnet ist, sowie einen allgemeinen Namen. Verwenden Sie einen aussagefähigen Namen, der erkennen lässt, ob es sich um ein Zertifikat für die Entwicklung (Sandbox) oder für die Verteilung (Produktion) handelt (z. B. *sandbox-apns-certificate* oder *production-apns-certificate*).
8. Wählen Sie die Option **Save to disk** aus, um die Datei `.certSigningRequest` auf Ihren Desktop herunterzuladen, und klicken Sie anschließend auf **Continue**.
9. Geben Sie in der Menüoption **Save As** einen Namen für die Datei `.certSigningRequest` an und klicken Sie anschließend auf **Save**.
10. Klicken Sie auf **Done**. Sie haben eine CSR erstellt.
11. Kehren Sie zum Fenster **About Creating a Certificate Siging Request (CSR)** zurück und klicken Sie auf **Continue**. 
12. Klicken Sie in der Anzeige **Generate** auf die Option **Choose File ... ** und wählen Sie die CSR-Datei aus, die Sie auf Ihrem Desktop gespeichert haben. Klicken Sie anschließend auf **Generate**.
	![Zertifikat generieren](images/generate_certificate.jpg)
13. Nachdem das Zertifikat erstellt wurde, klicken Sie auf **Done**.
14. Klicken Sie in der Anzeige **Push Notifications** auf **Download**, um Ihr Zertifikat herunterzuladen, und klicken Sie anschließend auf **Done**. 
	![Download certificate](images/certificate_download.jpg)
15. Navigieren Sie auf Ihrem Mac-Computer zu **Keychain Access > My Certificates** und suchen Sie nach dem neu installierten Zertifikat. Doppelklicken Sie auf das Zertifikat, damit es in Keychain Access installiert wird.
16. Wählen Sie das Zertifikat und den privaten Schlüssel aus und klicken Sie anschließend auf **Export**, um das Zertifikat in das Format zum Austauschen personenbezogener Daten (`.p12`) umzuwandeln.
	![Zertifikat und Schlüssel exportieren](images/keychain_export_key.jpg)
17. Geben Sie im Feld **Save As** einen aussagefähigen Namen für das Zertifikat an. Zum Beispiel `sandbox_apns.p12_certifcate` oder `production_apns.p12` und klicken Sie anschließend auf **Save**.
	![Zertifikat und Schlüssel exportieren](images/certificate_p12v2.jpg)
18. Geben Sie im Feld **Enter a password** ein Kennwort zum Schützen der exportierten Elemente ein und klicken Sie anschließend auf **OK**. Dieses Kennwort können Sie später verwenden, um Ihre APNs-Einstellungen im Push-Dashboard zu konfigurieren.{: #step18}
	![Zertifikat und Schlüssel exportieren](images/export_p12.jpg)
19. **Key Access.app** fordert Sie zum Exportieren Ihres Schlüssels aus der Anzeige **Keychain** auf. Geben Sie Ihr Administratorkennwort für Ihren Mac-Computer ein, um den Export dieser Elemente zuzulassen, und wählen Sie anschließend die Option **Always Allow** aus. Auf Ihrem Desktop wird ein `.p12`-Zertifikat erstellt.


##Entwicklungsbereitstellungsprofil erstellen
{: #create-push-credentials-dev-profile}

Das Bereitstellungsprofil ermittelt anhand der App-ID, auf welchen Geräten Ihre App installiert und ausgeführt werden kann und auf welche Services die App zugreifen kann. Sie erstellen für jede App-ID zwei Bereitstellungsprofile, eines für die Entwicklung und das zweite für die Verteilung. Xcode ermittelt anhand des Entwicklungsbereitstellungsprofils, welche Entwickler den Build für die App durchführen dürfen und welche Geräte in der Anwendung
getestet werden dürfen.

Stellen Sie sicher, dass die App-ID registriert, für den {{site.data.keyword.mobilepushshort}}-Service aktiviert und für die Verwendung eines SSL-Zertifikats für APNs im Entwicklungs- sowie im Produktionsmodus konfiguriert wurde.

Erstellen Sie ein Entwicklungsbereitstellungsprofil wie folgt:

1. Rufen Sie das [Apple Developer-Portal ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.apple.com){: new_window} auf, klicken Sie auf **Member Center** und wählen Sie **Certificates, Identifiers & Profiles** aus.
2. Rufen Sie die [Mac Developer Library ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/MaintainingProfiles/MaintainingProfiles.html#//apple_ref/doc/uid/TP40012582-CH30-SW62site){: new_window}  auf, navigieren Sie zum Abschnitt **Creating Development Provisioning Profiles** und befolgen Sie die Anweisungen zum Erstellen eines Entwicklungsprofils.
**Hinweis**: Wählen Sie beim Konfigurieren eines Entwicklungsbereitstellungsprofils die folgenden Optionen aus:
	* **iOS App Development**
	* **For iOS and watchOS apps **



##Bereitstellungsprofil für Store-Verteilung erstellen
{: #create-push-credentials-apns-distribute_profile}

Mithilfe des Store-Bereitstellungsprofils können Sie Ihre App für die Verteilung
an den App-Store übergeben.

1. Rufen Sie das [Apple Developer-Portal ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.apple.com){: new_window} auf, klicken Sie auf **Member Center** und wählen Sie **Certificates, Identifiers & Profiles** aus.
2. Doppelklicken Sie auf das heruntergeladene Bereitstellungsprofil, um das Profil in Xcode zu installieren.

##APNs im {{site.data.keyword.mobilepushshort}}-Dashboard einrichten
{: #create-push-credentials-apns-dashboard}

Um den {{site.data.keyword.mobilepushshort}}-Service zum Senden von Benachrichtigungen verwenden zu können, laden Sie die SSL-Zertifikate hoch, die für Apple Push Notification Service (APNs) erforderlich sind. Sie können auch die REST-API verwenden, um ein APNs-Zertifikat hochzuladen.

<!-- Get your development and production APNs SSL certificate and the password associated with each type of certificate. For information, see Creating and configuring push credentials for APNs.-->

Die für APNs erforderlichen Zertifikate sind `.p12`-Zertifikate. Diese Zertifikate enthalten den privaten Schlüssel und SSL-Zertifikate, die zum Erstellen und Veröffentlichen Ihrer Anwendung erforderlich sind. Sie müssen die Zertifikate über das Member Center der Apple Developer-Website (wofür Sie ein gültiges Apple Developer-Konto benötigen) generieren. Für die Entwicklungsumgebung (Sandbox) und die Produktionsumgebung (Verteilung) sind unterschiedliche Zertifikate erforderlich.

**Hinweis**: Nachdem sich die `.cer`-Datei in Ihrem Key Chain-Zugriff befindet, exportieren Sie sie auf Ihrem Computer, um ein `.p12`-Zertifikat zu erstellen.

Weitere Informationen zur Verwendung der APNs finden Sie in der Veröffentlichung [iOS Developer Library: Local and Push Notification Programming Guide ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ProvisioningDevelopment.html#//apple_ref/doc/uid/TP40008194-CH104-SW4){: new_window}.

Führen Sie die folgenden Schritte aus, um APNs im Push Notifications-Services-Dashboard einzurichten:

1. Wählen Sie im Push Notifications-Services-Dashboard die Option **Konfigurieren** aus.
2. Wählen Sie die Option **Mobile** aus, um die Informationen im Formular mit den APNs-Push-Berechtigungsnachweisen zu aktualisieren.
3. Wählen Sie je nach Bedarf **Sandbox** (Entwicklung) oder **Produktion** (Verteilung) aus und laden Sie dann das `p.12`-Zertifikat hoch, das Sie im vorherigen [Schritt](#step18) erstellt haben.
  ![Dashboard zum Festlegen von Push-Benachrichtigungen](images/wizard.jpg)
3. Geben Sie in das Feld **Kennwort** das zugehörige Kennwort für die `.p12`-Zertifikatsdatei ein und klicken Sie anschließend auf **Speichern**.

Nachdem die Zertifikate erfolgreich mit einem gültigen Kennwort hochgeladen wurden, können Sie mit dem Senden von Benachrichtigungen beginnen.
