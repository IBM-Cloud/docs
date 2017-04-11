---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} Mobile-SDK verwenden
{: #openwhisk_mobile_sdk}

{{site.data.keyword.openwhisk}} stellt ein Mobile-SDK für iOS- und watchOS-Geräte bereit, mit dem mobile Apps dazu eingerichtet werden können, ohne großen Aufwand ferne Auslöser zu aktivieren und ferne Aktionen aufzurufen. Gegenwärtig ist keine Version für Android verfügbar. Android-Entwickler können die {{site.data.keyword.openwhisk}}-REST-API direkt verwenden.

Das Mobil-SDK wurde in Swift 3.0 geschrieben und unterstützt iOS 10 und höhere Releases. Sie können das Mobil-SDK mithilfe von Xcode 8.0 erstellen. Bisherige Swift 2.2/Xcode 7-Versionen des SDK sind bis 0.1.7 verfügbar, obgleich sie nicht mehr verwendet werden.

## SDK der App hinzufügen
{: #openwhisk_add_sdk}

Sie können das Mobil-SDK mithilfe von CocoaPods, Carthage oder aus dem Quellenverzeichnis installieren.

### Mithilfe von CocoaPods installieren
{: #openwhisk_add_sdk_cocoapods}

Das {{site.data.keyword.openwhisk_short}}-SDK für den mobilen Einsatz ist nur über CocoaPods für die öffentliche Verteilung verfügbar. Wenn CocoaPods installiert ist, fügen Sie die folgenden Zeilen in eine Datei mit dem Namen 'Podfile' im Projektverzeichnis der Starter-App ein.

```
install! 'cocoapods', :deterministic_uuids => false
use_frameworks!

target 'MyApp' do
     pod 'OpenWhisk', :git => 'https://github.com/openwhisk/openwhisk-client-swift.git', :tag => '0.2.2'
end

target 'MyApp WatchKit Extension' do
     pod 'OpenWhisk', :git => 'https://github.com/openwhisk/openwhisk-client-swift.git', :tag => '0.2.2'
end
```
{: codeblock}

Geben Sie über die Befehlszeile den Befehl `pod install` ein. Dieser Befehl installiert das SDK für eine iOS-App mit einer watchOS-Erweiterung.  Verwenden Sie die Arbeitsbereichsdatei, die CocoaPods für Ihre App erstellt, um das Projekt in Xcode zu öffnen.

Nach der Installation öffnen Sie Ihren Projektarbeitsbereich.  Bei der Erstellung kann folgende Warnmeldung angezeigt werden: `Use Legacy Swift Language Version” (SWIFT_VERSION) is required to be configured correctly for targets which use Swift. Use the [Edit > Convert > To Current Swift Syntax…] menu to choose a Swift version or use the Build Settings editor to configure the build setting directly.`
Dies geschieht, wenn Cocoapods die Swift-Version im Pods-Projekt nicht aktualisiert.  Zur Behebung wählen Sie das Pods-Projekt und das {{site.data.keyword.openwhisk_short}}-Ziel aus.  Rufen Sie den Editor zum Erstellen der Einstellungen auf und ändern Sie die Einstellung `Bisherige Swift-Sprachversion verwenden` in `no`. Alternativ können Sie am Ende Ihrer Podfile die folgenden Nachinstallationsschritte hinzufügen:

```
post_install do |installer|
  installer.pods_project.targets.each do |target|
    target.build_configurations.each do |config|
      config.build_settings['SWIFT_VERSION'] = '3.0'
    end
  end
end
```
{: codeblock}

### Mithilfe von Carthage installieren
{: #openwhisk_add_sdk_carthage}

Erstellen Sie eine Datei im Projektverzeichnis Ihrer App mit dem Namen 'Cartfile'. Fügen Sie die folgende Zeile in die Datei ein:
```
github "openwhisk/openwhisk-client-swift.git" ~> 0.2.2 # Oder aktuelle Version
```
{: codeblock}

Geben Sie über die Befehlszeile den Befehl `carthage update --platform ios` ein. Carthage lädt das SDK herunter und führt einen Build durch, erstellt ein Verzeichnis mit dem Namen 'Carthage' im Projektverzeichnis Ihrer App und fügt eine {{site.data.keyword.openwhisk_short}}.framework-Datei in Carthage/build/iOS ein.

Anschließend müssen Sie {{site.data.keyword.openwhisk_short}}.framework den eingebetteten Frameworks in Ihrem Xcode-Projekt hinzufügen.

### Aus Quellcode installieren
{: #openwhisk_add_sdk_source}

Der Quellcode wird unter https://github.com/openwhisk/openwhisk-client-swift.git zur Verfügung gestellt.
Öffnen Sie mit Xcode ein Projekt unter Verwendung von `OpenWhisk.xcodeproj`.
Das Projekt enthält die beiden Schemas 'OpenWhisk' (für iOS) und 'OpenWhiskWatch' (für watchOS 2).
Erstellen Sie das Projekt (Build) für die Ziele, die Sie benötigen, und fügen Sie die resultierenden Frameworks Ihrer App (in der Regel in ~/Library/Developer/Xcode/DerivedData/Ihr App-Name) hinzu.

## Starter-App-Beispiel installieren
{: #openwhisk_install_sdkstart}

Sie können die {{site.data.keyword.openwhisk_short}}-CLI zum Herunterladen von Beispielcode verwenden, der in das {{site.data.keyword.openwhisk_short}}-SDK-Framework eingebettet wird.  

Geben Sie den folgenden Befehl ein, um das Starter-App-Beispiel zu installieren:
```bash
wsk sdk install iOS
```
{: pre}

Mit diesem Befehl wird eine komprimierte Datei mit der Starter-App heruntergeladen. Im Projektverzeichnis befindet sich eine Podfile.

Geben Sie den folgenden Befehl ein, um das SDK zu installieren:
```bash
pod install
```
{: pre}

## Erste Schritte mit dem SDK
{: #openwhisk_sdk_getstart}

Um die Arbeit rasch aufnehmen zu können, erstellen Sie ein Objekt 'WhiskCredentials' mit Ihren {{site.data.keyword.openwhisk_short}}-API-Berechtigungsnachweisen und eine {{site.data.keyword.openwhisk_short}}-Instanz aus diesem Objekt.

Sie können zum Beispiel folgenden Beispielcode zum Erstellen des Berechtigungsnachweisobjekts verwenden:

```swift
let credentialsConfiguration = WhiskCredentials(accessKey: "myKey", accessToken: "myToken")

let whisk = Whisk(credentials: credentialsConfiguration!)
```
{: codeblock}

Im obigen Beispiel werden die aus {{site.data.keyword.openwhisk_short}} abgerufenen Parameter `myKey` und `myToken` übergeben. Sie können den Schlüssel (Key) und das Token mit dem folgenden CLI-Befehl abrufen:

```bash
wsk property get --auth
```
{: pre}
```
whisk auth        kkkkkkkk-kkkk-kkkk-kkkk-kkkkkkkkkkkk:tttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttttt
```
{: screen}

Die Zeichenfolgen vor dem Doppelpunkt sind der Schlüssel und die Zeichenfolge nach dem Doppelpunkt ist das Token.

## {{site.data.keyword.openwhisk_short}}-Aktion aufrufen
{: #openwhisk_sdk_invoke}


Zum Aufrufen einer fernen Aktion können Sie `invokeAction` mit dem Aktionsnamen aufrufen. Sie können den Namensbereich angeben, zu dem die Aktion gehört, oder Sie können den Namensbereich leer lassen, um den Standardnamensbereich zu übernehmen. Verwenden Sie ein Wörterverzeichnis (Dictionary), um die erforderlichen Parameter an die Aktion zu übergeben.

Beispiel:

```swift
// In diesem Beispiel wird eine Aktion zur Ausgabe einer Nachricht auf der {{site.data.keyword.openwhisk_short}}-Konsole aufgerufen.
var params = Dictionary<String, String>()
params["payload"] = "Hi from mobile"

do {
    try whisk.invokeAction(name: "helloConsole", package: "mypackage", namespace: "mynamespace", parameters: params, hasResult: false, callback: {(reply, error) -> Void in
        if let error = error {
            //Operationen ausführen
            print("Error invoking action \(error.localizedDescription)")
        } else {
            print("Action invoked!")
        }

    })
} catch {
    print("Error \(error)")
}
```
{: codeblock}

Im obigen Beispiel wird die Aktion `helloConsole` unter Verwendung des Standardnamensbereichs aufgerufen.

## {{site.data.keyword.openwhisk_short}}-Auslöser aktivieren
{: #openwhisk_sdk_fire}

Zur Aktivierung eines fernen Auslösers können Sie die Methode `fireTrigger` aufrufen. Übergeben Sie die erforderlichen Parameter durch ein Wörterverzeichnis.

```swift
// In diesem Beispiel wird ein Auslöser aktiviert, wenn sich der Standort um eine bestimmte Entfernung geändert hat.

var locationParams = Dictionary<String, String>()
locationParams["payload"] = "{\"lat\":41.27093, \"lon\":-73.77763}"

do {
    try whisk.fireTrigger(name: "locationChanged", package: "mypackage", namespace: "mynamespace", parameters: locationParams, callback: {(reply, error) -> Void in

        if let error = error {
            print("Error firing trigger \(error.localizedDescription)")
        } else {
            print("Trigger fired!")
        }
    })
} catch {
    print("Error \(error)")
}
```
{: codeblock}

Im obigen Beispiel wird ein Auslöser mit dem Namen `locationChanged` aktiviert.

## Aktionen mit Rückgabe eines Ergebnisses verwenden
{: #openwhisk_sdk_actionresult}

Wenn die Aktion ein Ergebnis zurückgibt, geben Sie im Aufruf von 'invokeAction' für 'hasResult' den Wert 'true' an. Das Ergebnis der Aktion wird im Reply-Wörterverzeichnis zurückgegeben. Beispiel:

```swift
do {
    try whisk.invokeAction(name: "actionWithResult", package: "mypackage", namespace: "mynamespace", parameters: params, hasResult: true, callback: {(reply, error) -> Void in

        if let error = error {
            //Operationen ausführen
            print("Error invoking action \(error.localizedDescription)")

        } else {
            var result = reply["result"]
            print("Got result \(result)")
        }


    })
} catch {
    print("Error \(error)")
}
```
{: codeblock}

Standardmäßig gibt das SDK nur die Aktivierungs-ID und das durch die aufgerufene Aktion erzeugte Ergebnis zurück. Wenn Sie Metadaten des gesamten Antwortobjekts abrufen wollen, zu denen der HTTP-Antwortstatuscode gehört, verwenden Sie die folgende Einstellung:

```swift
whisk.verboseReplies = true
```
{: codeblock}

## SDK konfigurieren
{: #openwhisk_sdk_configure}

Sie können das SDK mithilfe des Parameters 'baseURL' zur Arbeit mit verschiedenen Installationen von {{site.data.keyword.openwhisk_short}} konfigurieren. Beispiel:

```swift
whisk.baseURL = "http://localhost:8080"
```
{: codeblock}

In diesem Beispiel wird eine Installation verwendet, die unter 'localhost:8080' ausgeführt wird. Wenn Sie den Parameter 'baseUrl' nicht angeben, verwendet das Mobil-SDK die Instanz, die unter https://openwhisk.ng.bluemix.net ausgeführt wird.

Sie können einen angepassten Parameter NSURLSession übergeben, wenn Sie eine besondere Netzverwaltung benötigen. Sie könnten zum Beispiel eine eigene {{site.data.keyword.openwhisk_short}}-Installation haben, die mit selbst signierten Zertifikaten arbeitet:

```swift
// Netzdelegate erstellen, der allen vertraut
class NetworkUtilsDelegate: NSObject, NSURLSessionDelegate {
    func URLSession(session: NSURLSession, didReceiveChallenge challenge: NSURLAuthenticationChallenge, completionHandler: (NSURLSessionAuthChallengeDisposition, NSURLCredential?) -> Void) {
        completionHandler(NSURLSessionAuthChallengeDisposition.UseCredential, NSURLCredential(forTrust: challenge.protectionSpace.serverTrust!))
    }
}

// NSURLSession erstellen, die den vertrauenden Delegate verwendet
let session = NSURLSession(configuration: NSURLSessionConfiguration.defaultSessionConfiguration(), delegate: NetworkUtilsDelegate(), delegateQueue:NSOperationQueue.mainQueue())

// Festlegen, dass das SDK diese urlSession anstelle der gemeinsam genutzten Standardsitzung verwendet
whisk.urlSession = session
```
{: codeblock}

### Unterstützung für qualifizierte Namen
{: #openwhisk_sdk_configure_qual}

Alle Aktionen und Auslöser haben einen vollständig qualifizierten Namen, der aus einem Namensbereich, einem Paketnamen und einem Aktions- bzw. Auslösernamen besteht. Das SDK kann diese Elemente als Parameter beim Aufruf einer Aktion bzw. Aktivieren eines Auslösers akzeptieren. Das SDK stellt zudem eine Funktion bereit, die einen vollständig qualifizierten Namen akzeptiert, der wie folgt aussieht: `/mynamespace/mypackage/nameOfActionOrTrigger`. Die Zeichenfolge für den qualifizierten Namen unterstützt unbenannte Standardwerte für Namensbereiche und Pakete, die alle {{site.data.keyword.openwhisk_short}}-Benutzer haben, sodass die folgenden Syntaxanalyseregeln gelten:

- qName = "foo" ergibt: Namensbereich = Standard, Paket = Standard, Aktion/Auslöser = "foo"
- qName = "mypackage/foo" ergibt: Namensbereich = Standard, Paket = mypackage, Aktion/Auslöser = "foo"
- qName = "/mynamespace/foo" ergibt: Namensbereich = mynamespace, Paket = Standard, Aktion/Auslöser = "foo"
- qName = "/mynamespace/mypackage/foo ergibt: Namensbereich = mynamespace, Paket = mypackage, Aktion/Auslöser = "foo"

Alle anderen Kombinationen haben einen Fehler WhiskError.QualifiedName zur Folge. Daher müssen Sie bei Verwendung von qualifizierten Namen den Aufruf in ein Konstrukt "`do/try/catch`" einschließen.

### SDK-Schaltfläche
{: #openwhisk_sdk_configure_button}

Aus Gründen der Verwendungsfreundlichkeit enthält das SDK eine Schaltfläche `WhiskButton`, die die Schaltfläche `UIButton` erweitert, sodass sie Aktionen aufrufen kann.  Gehen Sie zur Verwendung von `WhiskButton` wie im folgenden Beispiel vor:

```swift
var whiskButton = WhiskButton(frame: CGRectMake(0,0,20,20))

whiskButton.setupWhiskAction("helloConsole", package: "mypackage", namespace: "_", credentials: credentialsConfiguration!, hasResult: false, parameters: nil, urlSession: nil)

let myParams = ["name":"value"]

// Dies aufrufen, wenn Tastendrückereignis erkannt wird, z. B. in IBAction, um Aktion aufzurufen
whiskButton.invokeAction(parameters: myParams, callback: { reply, error in
    if let error = error {
        print("Oh no, error: \(error)")
    } else {
        print("Success: \(reply)")
    }
})

// Alternativ können Sie eine eigenständige Schaltfläche einrichten, die selbst für Tastenereignisse empfangsbereit ist und eine Aktion aufruft.

var whiskButtonSelfContained = WhiskButton(frame: CGRectMake(0,0,20,20))
whiskButtonSelfContained.listenForPressEvents = true
do {

   // Verwendung der API für qualifizierte Namen erfordert do/try/catch.
   try whiskButtonSelfContained.setupWhiskAction("mypackage/helloConsole", credentials: credentialsConfiguration!, hasResult: false, parameters: nil, urlSession: nil)
   whiskButtonSelfContained.actionButtonCallback = { reply, error in

       if let error = error {
           print("Oh no, error: \(error)")
       } else {
           print("Success: \(reply)")
       }
   }
} catch {
   print("Error setting up button \(error)")
}
```
{: codeblock}
