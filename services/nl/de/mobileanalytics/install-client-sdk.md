---

copyright:
  years: 2015, 2016

---

# {{site.data.keyword.mobileanalytics_short}} installieren
Client-SDKs
{: #mobileanalytics_sdk}
*Letzte Aktualisierung: 21. April 2016*
{: .last-updated}

Die Client-SDKs für {{site.data.keyword.mobileanalytics_short}} sind derzeit für Android, iOS und WatchOS verfügbar.
{: #shortdesc}

## Client-SDK für Android installieren
{: #install-sdk-android}

Im Lieferumfang des Client-SDKs für {{site.data.keyword.mobileanalytics_short}} ist derzeit Gradle enthalten, ein Abhängigkeitsmanager für Android-Projekte. Gradle lädt automatisch Artefakte aus Repositorys herunter und macht sie für die Android-Anwendung verfügbar.

1. Erstellen Sie ein [Android Studio](http://developer.android.com/sdk/index.html)-Projekt oder öffnen Sie ein vorhandenes Projekt.

2. Öffnen Sie die Datei `build.gradle`, die sich im Anwendungsmodul befindet.

  **Tipp:** Ein Android-Projekt kann über zwei Dateien mit der Bezeichnung `build.gradle` verfügen: eine für das Projekt und eine für das Anwendungsmodul. Stellen Sie sicher, dass die Datei für das **Anwendungsmodul** verwendet wird.

3. Suchen Sie den Abschnitt `Dependencies` der Datei `build.gradle` und fügen Sie wie folgt eine Kompilierungsabhängigkeit für das {{site.data.keyword.mobileanalytics_short}}-Client-SDK hinzu:

  ```Gradle
    compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
      name:'analytics',
      version: '1.+',
      ext: 'aar',
      transitive: true
  ```
  {: codeblock}

  Die Anweisung für die Repositorys sollte dem folgenden Codebeispiel ähneln:

	```Gradle
      dependencies {
        compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',    
          name:'analytics',
          version: '1.+',
          ext: 'aar',
          transitive: true
    	// weitere Abhängigkeiten  
      }
  ```
  {: screen}

4. Synchronisieren Sie das Projekt mit Gradle durch Klicken auf **Tools &gt; Android &gt; Sync Project with Gradle Files**.

5. Öffnen Sie die Datei `AndroidManifest.xml` für das Android-Projekt und fügen Sie unter dem Element `<manifest>` eine Berechtigung für den Internetzugriff hinzu:

	```XML
	 <uses-permission android:name="android.permission.INTERNET" />
   ```
   {: codeblock}


## Swift-SDK installieren
{: #installing-sdk-ios}

Mit dem {{site.data.keyword.mobileanalytics_full}}-SDK können Sie die mobile Anwendung instrumentieren. Das Swift-SDK ist für iOS und WatchOS verfügbar.

### Vorbemerkungen
{: #before-you-begin-ios}

Stellen Sie sicher, dass Xcode ordnungsgemäß konfiguriert ist. Informationen zum Konfigurieren einer iOS-Entwicklungsumgebung finden Sie auf der [Apple-Entwickler-Website](https://developer.apple.com/support/xcode/).

Das {{site.data.keyword.mobileanalytics_short}}-SDK ist im Lieferumfang von [Cocoapods](https://cocoapods.org/) und [Carthage](https://github.com/Carthage/Carthage#getting-started) enthalten, den Abhängigkeitsmanagern für Cocoa-Projekten. Von CocoaPods and Carthage werden automatisch Artefakte aus den Repositorys heruntergeladen und für die Anwendung verfügbar gemacht.

#### Cocoapods
{: #cocoapods}
1. Wenn CocoaPods nicht installiert ist, führen Sie den folgenden Befehl aus:

    ```
    sudo gem install cocoapods
    ```
    {: codeblock}

2. Wenn der Arbeitsbereich noch nicht für CocoaPods initialisiert ist, führen Sie den Befehl `pod init` im Stammverzeichnis des Projekts aus. Von CocoaPods wird die Datei `Podfile` erstellt, in der Sie die Abhängigkeiten für das Xcode-Projekt definieren.

3. Fügen Sie den Pod `BMSAnalytics` zum Ziel in der Datei 'Podfile' hinzu; Beispiel:

	### iOS

  ```
  use_frameworks!

  target 'MyApp' do
     platform :ios, '8.0'
     pod 'BMSAnalytics'
  end
  ```

4. Speichern Sie die Datei `Podfile` und führen Sie in der Befehlszeile den Befehl `pod install` aus.

5. Öffnen Sie den Xcode-Projektarbeitsbereich mithilfe der Datei `.xcworkspace`, die von CocoaPods generiert wurde.

#### Carthage
{: #carthage}

Fügen Sie Frameworks mit [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos) zum Projekt hinzu.

1. Fügen Sie `BMSAnalytics`-Frameworks zur Cartfile hinzu:
  ```
  github "ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics"
  ```
2. Führen Sie den Befehl `carthage update` aus. Wenn die Erstellung abgeschlossen ist, ziehen Sie `BMSAnalytics.framework`, `BMSCore.framework` und `BMSAnalyticsAPI.framework` in das Xcode-Projekt.
3. Gehen Sie gemäß den Anweisungen auf der [Carthage](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos)-Site zum Ausführen der Integration vor.

# Zugehörige Links

## SDK
* [Android-SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [iOS-SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}

## API-Referenz
{: #api}
* [REST-API](https://mobile-analytics-dashboard.eu-gb.bluemix.net/analytics-service/){:new_window}
