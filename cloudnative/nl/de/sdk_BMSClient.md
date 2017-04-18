---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# BMSClient initialisieren
{: #sdk_BMSClient}

`BMSCore` stellt die HTTP-Infrastruktur bereit, die die anderen {{site.data.keyword.Bluemix}} Mobile-Services-Client-SDKs zur Kommunikation mit ihren entsprechenden {{site.data.keyword.Bluemix_notm}}-Services verwenden.


## Eigene Android-Anwendung initialisieren
{: #init-BMSClient-android}

Sie können das `BMSCore`-Paket entweder in Ihr Android Studio-Projekt herunterladen und importieren oder Gradle verwenden.

1. Importieren Sie das Client-SDK durch Hinzufügen der folgenden Anweisung des Typs `import` an den Anfang Ihrer Projektdatei:

  ```
  import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
  ```
  {: codeblock}

2. Initialisieren Sie das `BMSClient`-SDK in Ihrer Android-Anwendung, indem Sie den Initialisierungscode in der Methode `onCreate` der Hauptaktivität in Ihrer Android-Anwendung oder an einer Position hinzufügen, die für Ihr Projekt am geeignetsten ist.

  ```Java
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_US_SOUTH); // Make sure that you point to your region
  ```
  {: codeblock}

  Sie müssen `BMSClient` mit dem Parameter **bluemixRegion** initialisieren. Im Initialisierungsoperator gibt der Wert **bluemixRegion** an, welche {{site.data.keyword.Bluemix_notm}}-Bereitstellung Sie verwenden, z. B. `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK` oder `BMSClient.REGION_SYDNEY`.


## Eigene iOS-Anwendung initialisieren
{: #init-BMSClient-ios}

Sie können mithilfe von [CocoaPods](https://cocoapods.org){: new_window} oder [Carthage](https://github.com/Carthage/Carthage){: new_window} das `BMSCore`-Paket abrufen.

1. Fügen Sie zur Installation von `BMSCore` mithilfe von CocoaPods die folgenden Zeilen zu Ihrer Podfile hinzu. Wenn Ihr Projekt noch keine Podfile aufweist, verwenden Sie den Befehl `pod init`.

  ```Swift
  use_frameworks!

  target 'MyApp' do
    pod 'BMSCore'
  end
  ```
  {: codeblock}

  Führen Sie anschließend den Befehl `pod install` aus und öffnen Sie die generierte Datei des Typs `.xcworkspace`. Zur Aktualisierung auf ein neueres Release von `BMSCore` müssen Sie den Befehl `pod update BMSCore` verwenden.

  Weitere Informationen zur Verwendung von CocoaPods finden Sie auf der Seite [CocoaPods Guides ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://guides.cocoapods.org/using/index.html){: new_window}.

2. Befolgen Sie zur Installation von `BMSCore` mithilfe von Carthage diese [Anweisungen ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/Carthage/Carthage#getting-started){: new_window}.

  1. Fügen Sie die folgende Zeile zu Ihrer Cartfile hinzu:

      ```
      github "ibm-bluemix-mobile-services/bms-clientsdk-swift-core"
      ```
      {: codeblock}

  2. Führen Sie den Befehl `carthage update` aus.

  3. Fügen Sie nach Fertigstellung des Builds `BMSCore.framework` zu Ihrem Projekt hinzu. Führen Sie dazu [Schritt 3 ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://github.com/Carthage/Carthage#getting-started) in den Carthage-Anweisungen durch.

      Verwenden Sie für Anwendungen, die mit Swift 2.3 aufgebaut sind, den Befehl `carthage update --toolchain com.apple.dt.toolchain.Swift_2_3`. Verwenden Sie andernfalls den Befehl `carthage update`.

3. Importieren Sie das Modul.

  ```Swift
  import BMSCore
  ```
  {: codeblock}

4. Initialisieren Sie mithilfe des folgenden Codes die Klasse `BMSClient`.

  Platzieren Sie den Initialisierungscode in der Methode `application(_:didFinishLaunchingWithOptions:)` Ihres Anwendungsbeauftragten oder an einer Position, die für Ihr Projekt am geeignetsten ist.

  ```Swift
    BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // Make sure that you point to your region
  ```
  {: codeblock}

  Sie müssen `BMSClient` mit dem Parameter **bluemixRegion** initialisieren. Im Initialisierungsoperator gibt der Wert **bluemixRegion** an, welche {{site.data.keyword.Bluemix_notm}}-Bereitstellung Sie verwenden, z. B. `BMSClient.Region.usSouth`, `BMSClient.Region.unitedKingdom` oder `BMSClient.Region.sydney`.


## Eigene Cordova-Anwendung initialisieren
{: #init-BMSClient-cordova}

1. Fügen Sie das Cordova-Plug-in hinzu, indem Sie den folgenden Befehl im Stammverzeichnis Ihrer Cordova-Anwendung ausführen:

  ```
  cordova plugin add bms-core
  ```
  {: codeblock}

2. Initialisieren Sie die Klasse `BMSClient` in Ihrer Cordova-Anwendung, indem Sie den Initialisierungscode in der Haupt-JavaScript-Datei oder an einer Position hinzufügen, die für Ihr Projekt am geeignetsten ist.

  ```
  BMSClient.initialize(BMSClient.REGION_US_SOUTH);
  ```
  {: codeblock}
	
  Sie müssen `BMSClient` mit dem Parameter **bluemixRegion** initialisieren. Im Initialisierungsoperator gibt der Wert **bluemixRegion** an, welche {{site.data.keyword.Bluemix_notm}}-Bereitstellung Sie verwenden, z. B. `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK` oder `BMSClient.REGION_SYDNEY`.


# Zugehörige Links
{: #rellinks notoc}

## Zugehörige Links
{: #general notoc}

* [BMSCore-Android-SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core){: new_window}
* [BMSCore-iOS-SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core){: new_window}
* [BMSCore-Cordova-Plug-in](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-core){: new_window}
