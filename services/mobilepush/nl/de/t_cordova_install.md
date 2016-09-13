---

copyright:
 years: 2015, 2016

---

# Cordova Push-Plug-in installieren
{: #cordova_install}

Installieren und verwenden Sie das Client-Push-Plug-in für die weitere Entwicklung Ihrer Cordova-Anwendungen. Dieser Befehl installiert auch das Cordova Core-Plug-in,
das Ihre Verbindung zu Bluemix initialisiert.

### Vorbemerkungen

1. Laden Sie die aktuellen Version für das Android Studio-SDK und Xcode herunter.
1. Richten Sie den Emulator ein. Verwenden Sie für Android Studio einen Emulator, der die Google Play-API unterstützt.
1. Installieren Sie das Git-Befehlszeilentool. Stellen Sie unter Windows sicher, dass Sie die Option zum Ausführen von Git über die Windows-Eingabeaufforderung auswählen. Informationen zum Herunterladen und Installieren dieses Tools finden Sie unter [Git](https://git-scm.com/downloads).

1. Installieren Sie Node.js und das NPM-Tool (NPM = Node Package Manager). Das NPM-Befehlszeilentool wird als Produktpaket mit Node.js bereitgestellt. Informationen zum Herunterladen und Installieren von Node.js finden Sie unter [Node.js](https://nodejs.org/en/download/).
1. Installieren Sie über die Befehlszeile die Cordova-Befehlszeilentools mithilfe des Befehls **npm install -g cordova**. Dies ist eine Voraussetzung für die Verwendung
des Cordova-Plug-ins. Informationen zum Installieren von Cordova und zum Einrichten Ihrer Cordova-App finden Sie unter [Cordova Apache](https://cordova.apache.org/#getstarted).

	**Hinweis**: Die Readme-Datei für das Cordova Push-Plug-in finden Sie unter [https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push).


## Cordova Push-Plug-in installieren
1. Wechseln Sie in den Ordner, in dem Sie Ihre Cordova-App erstellen möchten, und führen
Sie den folgenden Befehl aus, um eine Cordova-Anwendung zu erstellen. Wenn Sie bereits über eine
Cordova-App verfügen, fahren Sie mit Schritt 3 fort.


	cordova create your_app_name
	cd your_app_name
	```
1. Optional: Bearbeiten Sie die Datei **config.xml** und ersetzen Sie im Element <name> den Standardnamen 'HelloCordova' durch einen eigenen Namen.

	**Hinweis**: Stellen Sie sicher, dass Sie die richtige Bundle-ID angeben. Falls Sie dies nicht tun, werden in Xcode die folgenden Fehlernachrichten angezeigt.
	* The executable was signed with invalid entitlements (Die ausführbare Funktion ist mit ungültigen Berechtigungen signiert).
	* The entitlements specified in your application’s Code Signing Entitlements file do not match those specified in your provisioning profile (Die in der Berechtigungsdatei für die Codeunterzeichnung Ihrer Anwendung angegebenen Berechtigungen stimmen nicht mit den angegebenen Berechtigungen in Ihrem Bereitstellungsprofil überein).

	Um dieses Problem zu beheben, geben Sie korrekte Bundle-ID in Xcode oder in der Datei **config.xml** Ihrer Cordova-App an.

1. Fügen Sie die Mindestversion der unterstützten API oder die Bereitstellungszieldeklaration zur Datei 'config.xml' Ihrer Cordova-Anwendung hinzu: Der Wert für 'minSdkVersion' muss größer als 15 sein. Der Wert für 'targetSdkVersion' muss immer das neueste Android-SDK angeben, das bei Google verfügbar ist.
	* **Android**:  Öffnen Sie die Datei 'config.xml' in einem Texteditor und aktualisieren Sie das
Element `<platform name="android">` mit der SDK-Mindestversion und der SDK-Zielversion:

	```
	<!-- add deployment target declaration -->
	<platform name="android">  
			  <preference name="android-minSdkVersion" value="15" />
			  <preference name="android-targetSdkVersion" value="23" />
			</platform>
	```
   * **iOS**: Aktualisieren Sie das Element <platform name="ios"> mit einer Bereitstellungszieldeklaration:

	```
	<platform name="ios">
	    <preference name="deployment-target" value="8.0" />
	    <!-- other properties -->
	</ platform>
	```

1. Fügen Sie über die Cordova-Befehlszeilenschnittstelle (CLI) Ihre Plattform (iOS und/oder Android) mit den folgenden Befehlen hinzu.

	```
	cordova platform add ios
	cordova platform add android
	```
1. Geben Sie im Stammverzeichnis Ihrer Cordova-Anwendung den folgenden Befehl ein, um das Cordova Push-Plug-in **cordova plugin add ibm-mfp-push** zu installieren.

	Je nachdem, welche Plattformen Sie hinzugefügt haben, sehen Sie eine Anzeige
ähnlich der folgenden:

	```
	Installing "ibm-mfp-push" for android
	Installing "ibm-mfp-push" for ios
	```
1. Überprüfen Sie in *eigenes_anwendungsstammverzeichnis* mit dem Befehl **cordova plugin list**, dass die Plug-ins Cordova Core und Cordova Push erfolgreich installiert wurden.

	Je nachdem, welche Plattformen Sie hinzugefügt haben, sehen Sie eine Anzeige
ähnlich der folgenden:

	```
	ibm-mfp-core 1.0.0 "MFPCore"
	ibm-mfp-push 1.0.0 “MFPPush"
	```
1. (nur iOS): Konfigurieren Sie Ihre iOS-Entwicklungsumgebung.
	a. Öffnen Sie die Datei 'ihr_app-name.xcodeproj' im Verzeichnis *ihr_app-name***/platforms/ios** mit Xcode.

	b. Fügen Sie den Bridging-Header hinzu. Rufen Sie **Build settings > Swift Compiler - Code Generation > Objective-C Bridging Header** auf und fügen Sie den folgenden Pfad hinzu: *ihr_projektname***/Plugins/ibm-mfp-core/Bridging-Header.h**.

	c. Fügen Sie die Frameworks-Parameter hinzu. Rufen Sie **Build Settings > Linking > Runpath Search Paths** auf und fügen Sie die folgenden Parameter hinzu:
	```
	@executable_path/Frameworks
	```
	d. Entfernen Sie die Kommentarzeichen aus den folgenden Push-Importanweisungen im Bridging-Header. Wechseln Sie in das Verzeichnis *ihr_projektname***/Plugins/ibm-mfp-core/Bridging-Header.h**.

	```
	//#import <IMFPush/IMFPush.h>
	//#import <IMFPush/IMFPushClient.h>
	//#import <IMFPush/IMFResponse+IMFPushCategory.h>
	```
	e. Erstellen Sie die Anwendung und führen Sie sie mit Xcode aus.
1. (Nur Android): Erstellen Sie Ihr Android-Projekt mit dem folgenden Befehl:
**cordova build android**.

	**Hinweis**: Bevor Sie das Projekt in Android Studio öffnen, müssen Sie zuerst die Cordova-Anwendung über die Cordova-Befehlszeilenschnittstellen erstellen. Andernfalls kann es zu Buildfehlern kommen.

1. Nächster Schritt: [Cordova-Plug-in
initialisieren](t_cordova_initalize.html).
