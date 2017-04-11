---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-08"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# Mobile Beispiel-App installieren und verbinden
{: #iot4i_gettingstarted}

Die mobile Beispiel-App {{site.data.keyword.iotinsurance_full}} ist eine Referenzimplementierung für einen mobilen Client von {{site.data.keyword.iotinsurance_short}}. Sie können die App verwenden, um neue Geräte im System zu registrieren und um Alerts für die Geräte zu empfangen.
{:shortdesc}

**Hinweis**: {{site.data.keyword.iotinsurance_short}} stellt weder {{site.data.keyword.amafull}} noch {{site.data.keyword.mobilepushfull}} weiterhin bereit. Frühere Versionen von {{site.data.keyword.iotinsurance_short}} nutzten den Service {{site.data.keyword.amashort}}, um die Antworten aus der mobilen App zu verarbeiten. Dieser Prozess funktioniert weiterhin für alle vorhandenen Instanzen von {{site.data.keyword.iotinsurance_short}}. Sie müssen jedoch einen angepassten Authentifizierungsprozess einrichten, um die mobile App mit neuen Instanzen von
{{site.data.keyword.iotinsurance_short}} zu verwenden. Optional können Sie auch [eine Instanz von {{site.data.keyword.mobilepushshort}}](../mobilepush/index.html) erstellen, konfigurieren und an die {{site.data.keyword.iotinsurance_short}}-API binden.

**Voraussetzungen:** Folgendes wird vorausgesetzt:
  - Integrierte Entwicklungsumgebung Apple Xcode Version 8 (oder höher).
  - iPhone mit iOS 9.0 (oder höher).
  - CocoaPods muss auf Ihrem Computer installiert sein. Weitere Informationen finden Sie auf der [CocoaPods-Website ![Symbol für externen Link](../../icons/launch-glyph.svg)](https://guides.cocoapods.org/using/getting-started.html){: new_window}.
  - [Parameter](#iot4i_mobileParam), die erforderlich sind, um die mobile Beispiel-App mit Ihrer Instanz des Service zu verbinden.

## Mobile Beispiel-App erstellen
{: #building_mobile}
Führen Sie die folgenden Tasks aus, um die mobile Beispiel-App zu testen:

1. Klonen Sie das [Quellcode-Repository für die mobile Beispiel-App ![Symbol für externen Link](../../icons/launch-glyph.svg)](https://github.com/ibm-watson-iot/ioti-mobile){: new_window} auf einem Computer, auf dem Xcode Version 7.3 (oder höher) installiert ist.
2. Installieren Sie die erforderlichen Pakete und generieren Sie die Datei IoT4I.xcworkspace, indem Sie einen CocoaPods-Pod-Installationsbefehl für Ihr Projekt ausführen. CocoaPods muss installiert sein, damit diese Task ausgeführt werden kann.
3. Öffnen Sie das Projekt in Xcode, indem Sie doppelt auf die Datei IoT4I.xcworkspace klicken.
4. Verbinden Sie Ihr iPhone mit dem Computer und wählen Sie es als Buildziel aus.
5. Wählen Sie die IoT4I-Datei in der Dateiliste aus, um das Dialogfeld 'Identity' anzuzeigen.
6. Nehmen Sie im Feld 'Identity' in Xcode die folgenden Änderungen vor:
  - Ändern Sie die Bundle-ID (**Bundle Identifier**) in eine eindeutige Kennung. Beispiel: **myIoT4Ibundle**.
  - Geben Sie für **Team** Ihren persönlichen Teamnamen an und klicken Sie anschließend auf **Fix Issue**.
7. Um eine Verbindung zwischen Ihrer App und Ihrer Instanz von {{site.data.keyword.iotinsurance_short}} herzustellen, legen Sie folgende Parameter in der Datei **constants.swift** fest:  
    - [applicationRoute](#iot4i_mobileParam) = Die URL für die {{site.data.keyword.iotinsurance_short}}-API-Anwendung. Sie finden diesen Wert auf der Registerkarte 'Serviceberechtigungsnachweise' der {{site.data.keyword.iotinsurance_short}}-Servicekonsole.
    - [applicationId](#iot4i_mobileParam) = Die GUID für Ihre Instanz von {{site.data.keyword.amashort}}. Diesen Wert erhalten Sie durch Öffnen von {{site.data.keyword.amashort}} und anschließendes Klicken auf **Mobile Optionen**.  Der Wert lautet App GUID / TenantId.
8. Klicken Sie auf Ihrem Computer auf den Pfeil für den Build und die Ausführung des aktuellen Schemas. Die mobile Beispiel-App wird auf Ihrem Mobiltelefon installiert. Weitere Informationen finden Sie auf der Seite mit den [Anweisungen für Apple-Entwickler zum Ausführen von Apps auf Geräten von Xcode ![Symbol für externen Link](../../icons/launch-glyph.svg)](https://developer.apple.com/library/mac/documentation/IDEs/Conceptual/AppDistributionGuide/LaunchingYourApponDevices/LaunchingYourApponDevices.html){: new_window}.

  **Hinweis:** Angenommen, bei einem Buildversuch wird folgende Nachricht angezeigt: *Could not launch IoT4I because you have not yet verified that your Developer App certificate is trusted on your device*. Wählen Sie in diesem Fall wie folgt sich selbst als 'Trusted Developer' (Vertrauenswürdiger Entwickler) aus:  
    1. Wechseln Sie auf Ihrem Mobiltelefon zu **Einstellungen > Allgmein > Geräteverwaltung > IhreEntwicklerID (yourDeveloperID)**.
    2. Tippen Sie den Kontonamen Ihrer Entwickler-ID an, um Ihre Entwickler-ID als vertrauenswürdig zu definieren.
    3. Bestätigen Sie bei entsprechender Aufforderung, dass die Entwickler-ID vertrauenswürdig ist.

## Push-Benachrichtigungen für die mobile App aktivieren
{: #iot4i_pushNotification}

Führen Sie die folgenden Tasks aus, um Push-Benachrichtigungen für Ihr Mobiltelefon zu aktivieren. Sie müssen über ein gültiges Apple-Entwicklerkonto verfügen, um den Service für die Push-Benachrichtigung verwenden zu können.

1. Melden Sie sich bei Ihrem [Apple-Entwicklerkonto ![Symbol für externen Link](../../icons/launch-glyph.svg)](https://developer.apple.com/account){: new_window} an.

2. Erstellen Sie eine Zertifikatsdatei.
  1. Wählen Sie **Certificates, Identifiers & Profiles** aus.
  2. Wählen Sie IDs aus: App IDs.
  3. Klicken Sie auf die Schaltfläche 'Add' (+), um eine neue App-ID zu erstellen.
  4. Geben Sie im Feld **Description** eine Beschreibung für die App ein.
  5. Wählen Sie **Explicit App ID** aus und geben Sie eine Bundle-ID ein (z. B. com.YourOrganizationName.iot4i.mobileApp).
  6. Wählen Sie (V) unter **Push Notifications** aus und klicken Sie auf **Continue > Register > Done**.

3. Erstellen Sie ein Zertifikat für Push-Benachrichtigungen.
  1. Wählen Sie **Certificates: All** aus.
  2. Klicken Sie auf die Schaltfläche 'Add' (+), um ein neues APN-Zertifikat zu erstellen.
  3. Wählen Sie auf der Seite 'Add iOS Certificate' die Option **Apple Push Notification service SSL (Sandbox)** aus und klicken Sie auf **Continue**.
  4. Wählen Sie die App-ID aus, die Sie im vorherigen Schritt erstellt haben, und klicken Sie auf **Continue**.
  5. Erstellen Sie eine CSR-Datei, indem Sie den Anweisungen auf der Seite folgen, und klicken Sie auf **Continue**.
  6. Wählen Sie die CSR-Datei aus, die Sie erstellt haben, und klicken Sie auf **Continue**.
  7. Laden Sie die Zertifikatsdatei herunter und führen Sie sie aus.

4. Erstellen Sie ein Profil.
  1. Wählen Sie **Provisioning profile: Development** aus.
  2. Klicken Sie auf die Schaltfläche 'Add' (+), um ein neues Entwicklungsprofil zu erstellen.
  3. Wählen Sie **iOS App Development** aus und klicken Sie auf **Continue**.
  4. Wählen Sie die App-ID aus, die Sie zuvor erstellt haben.
  5. Wählen Sie **Developer Certificates: All** aus und klicken Sie auf **Continue**.
  5. Wählen Sie **All development devices (testing devices)** aus und klicken Sie auf **Continue**.
  6. Geben Sie einen Profilnamen ein und klicken Sie auf **Continue**.
  7. Laden Sie das generierte Profil herunter und führen Sie es aus.

5. Erstellen Sie eine PKCS 12-Datei (PKCS = Public Key Cryptography Standards) und fügen Sie sie dem Service '{{site.data.keyword.mobilepushshort}}' hinzu.
  1. Öffnen Sie 'Keychain Access' und wählen Sie **My Certificates** aus.
  2. Klicken Sie mit der rechten Maustaste auf **Apple Development IOS Push Service: (bundleID)** und exportieren Sie die Datei, speichern Sie sie und geben Sie ein Kennwort für sie ein.
  3. Öffnen Sie in Ihrer {{site.data.keyword.Bluemix_notm}}-Konsole den Service '{{site.data.keyword.mobilepushshort}}'.
  4. Klicken Sie auf **Konfigurieren**.
  5. Laden Sie im Abschnitt 'Apple Push Notifications Certificate' die PKCS 12-Datei hoch und geben Sie das Kennwort ein.
  6. Ändern Sie die Bundle-ID in Xcode in die zuvor von Ihnen erstellte Bundle-ID.
  7. Führen Sie die App aus und erteilen Sie Berechtigungen für den Service für Push-Benachrichtigungen.
