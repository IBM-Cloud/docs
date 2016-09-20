# Push-SDK für iOS-Apps initialisieren
{: #enable-push-ios-notifications-install}

Für ein vorhandenes Xcode-Projekt können Sie das Bluemix Mobile Services-Client-SDK mithilfe des Abhängigkeitsmanagementtools CocoaPods einrichten. Als Alternative dazu können Sie das Software-Development-Kit (SDK) manuell installieren.

**Hinweis**: Die Push-Readme-Datei für Swift finden Sie unter https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master.

##CocoaPods installieren

1. Installieren Sie CocoaPods, indem Sie in Ihrem Mac-Terminal folgenden Befehl verwenden.
```
$ sudo gem install cocoapods
```
2. Geben Sie den folgenden Befehl in das Terminal ein, um CocoaPods zu initialisieren. Stellen Sie beim Absetzen des Befehls sicher, dass Sie ihn in dem Verzeichnis ausführen, in dem sich Ihr Xcode-Projekt befindet. Mit dem Befehl `pod init` wird eine Dateibezeichnung erstellt.  
```
$ pod init
```
3. Fügen Sie in der generierten Datei 'Podfile' die von Ihnen benötigten SDK-Abhängigkeiten hinzu. Kopieren Sie die folgende Datei 'Podfile'.

   Objective-C

    ```
    source 'https://github.com/CocoaPods/Specs.git'
	Copy the following list as is and remove the dependencies you do not need
	pod 'IMFCore'
	pod 'IMFPush'
	```

   Swift

	```
	source 'https://github.com/CocoaPods/Specs.git'
	// Copy the following list as is and remove the dependencies you do not need.
	use_frameworks!

	target 'MyApp' do
	    platform :ios, '8.0'
	    pod 'BMSCore'
	    pod 'BMSPush'
	end
	```
3. Wechseln Sie am Terminal in Ihren Projektordner und installieren Sie die
Abhängigkeiten mithilfe des folgenden Befehls:
```
$ pod update
```
Mit diesem Befehl werden Ihre Abhängigkeiten installiert und es wird ein neuer Xcode-Arbeitsbereich erstellt.  **Hinweis**: Stellen Sie sicher, dass Sie immer den neuen Xcode-Arbeitsbereich öffnen und nicht die ursprüngliche Xcode-Projektdatei:

	```
	$ open App.xcworkspace
	```
Der Arbeitsbereich enthält Ihr ursprüngliches Projekt und das Projekt 'Pods', das Ihre Abhängigkeiten enthält. Wenn Sie einen Bluemix Mobile Services-Quellenordner ändern möchten, finden Sie diesen in Ihrem Projekt 'Pods' unter `Pods/yourImportedSourceFolder`, zum Beispiel: `Pods/IMFGoogleAuthentication`.

##Importierte Frameworks und Quellenordner verwenden

Referenzieren Sie das SDK in Ihrem Code.


### Objective-C

Schreiben Sie #import-Anweisungen für die entsprechenden Header, zum Beispiel:

```
//Objective-C
#import <IMFCore/IMFCore.h>
#import <IMFPush/IMFPush.h>
```

**Hinweis**: Durch Aktualisieren Ihres Projekts 'Pods' mithilfe der CocoaPods-Befehle `pod install` oder `pod update` werden die Bluemix Mobile Services-Quellenorder möglicherweise überschrieben. Wenn Sie Ihre angepassten Versionen der ursprünglichen Dateien aufbewahren möchten, müssen Sie sicherstellen, dass für sie ein Backup durchgeführt wird, bevor Sie einen dieser Befehle absetzen.

###Swift

**Voraussetzungen**

- iOS 8.0 oder höher
- Xcode 7


Schreiben Sie #import-Anweisungen für die entsprechenden Header, zum Beispiel:

```
//swift
import BMSCore
import BMSPush
```


##Buildeinstellungen

Rufen Sie **Xcode > Build Settings > Build Options** auf und setzen Sie **Enable Bitcode** auf **No**.

**Achtung**: Ab iOS 9 können sich Änderungen an der Komponente 'App Transport Security' (ATS) auf
die Verarbeitung des Authentifizierungsprozesses auswirken. Die folgenden Blogeinträge liefern weitere Informationen zu den Änderungen: [ATS and Bitcode in iOS 9](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/) und [Connect your iOS 9 app to Bluemix today](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/).
