---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# MQA mit einer iOS-App instrumentieren (veraltet)
{: #instrumentios}

Zur Verwendung von {{site.data.keyword.mqafull}} mit Ihrer iOS-App müssen Sie das SDK herunterladen und es instrumentieren, indem Sie mithilfe der Xcode-Entwicklungsumgebung einige Änderungen vornehmen.
{: shortdesc}

Bevor Sie eine App instrumentieren mit {{site.data.keyword.mqa}} instrumentieren können, müssen Sie über ein {{site.data.keyword.Bluemix}}-Konto und die ordnungsgemäß installierte Version der Entwicklungsumgebung für die Plattformen der App verfügen, die Sie instrumentieren.

Führen Sie die folgenden Tasks aus, um {{site.data.keyword.mqa}} für die Arbeit mit Ihrer Objective-C- oder Swift-App zu instrumentieren:

1. Fügen Sie die erforderlichen Berechtigungen und das heruntergeladene SDK zu Ihrem iOS-Projekt hinzu.

	1. Erstellen Sie Ihr Projekt in Xcode bzw. öffnen Sie es.

	2. Fügen Sie die folgenden Abhängigkeitsbibliotheken hinzu, und zwar durch Auswahl von `+` im Abschnitt mit den verlinkten Frameworks und Bibliotheken auf der Registerkarte *Allgemein* Ihres Xcode-Projekts:

		* AssetsLibrary.framework
		* AudioToolbox.framework
		* AVFoundation.framework
		* CoreData.framework
		* CoreLocation.framework
		* CoreMedia.framework
		* CoreMotion.framework
		* CoreTelephony.framework
		* CoreText.framework
		* CoreVideo.framework
		* MediaPlayer.framework
		* QuartzCore.framework
		* Security.framework
		* SystemConfiguration.framework

	3. Ziehen Sie den Ordner `Q4M.framework` des {{site.data.keyword.mqa}}-SDK für iOS in die Gruppe **Frameworks** der Navigationsstruktur. Wählen Sie im Fenster zum Auswählen der Optionen die Option zum Kopieren von Elementen bei Bedarf, zum Erstellen von Gruppen sowie das Feld für Ihren Projektnamen als Ziel aus.

	4. Legen Sie im Abschnitt 'Linking' der Registerkarte *Build Settings* die Option *Other Linker Flags* für 'Debug' und 'Release' auf **-ObjC** fest. Wichtig: Stellen Sie sicher, dass die Registerkarte *All* ausgewählt ist, sodass 'Other Linker Flags' in die Liste aufgenommen werden.

	5. *Nur für Objective-C:* Fügen Sie die folgende Importanweisung zu den Dateien `AppDelegate.m` und `ViewController.m` hinzu:

		```
		#import <Q4M/MQALogger.h>
		```
		{: codeblock}

	6. *Nur für Swift:* Fügen Sie einen Objective-C-Überbrückungsheader für das {{site.data.keyword.mqa}}-SDK für iOS durch Ausführen der folgenden Schritte hinzu:

		1. Klicken Sie mit der rechten Maustaste auf den Projektstammknoten und wählen Sie **Neue Datei** aus.

		2. Klicken Sie im Fenster für die Auswahl der Vorlage unter iOS auf die Vorlage für die Headerdatei im Abschnitt 'Quelle'.

		3. Geben Sie der Datei den Namen `MyProject-Bridging-Header.h`; dabei ist *MyProject* der Name des Swift-Projekts; wählen Sie den Namen Ihres Projekts als Ziel aus. Geben Sie der Datei beispielsweise den Namen `MyProject-Bridging-Header.h`.

		4. Klicken Sie auf die Option zum Erstellen, um die Datei im Stammverzeichnis Ihres Projekts zu speichern.

		5. Fügen Sie in der neuen Überbrückungsheaderdatei die folgende Importanweisung für die Überbrückungsheaderdatei hinzu:

			```
			#import <Q4M/MQALogger.h>
			```
			{: codeblock}

		6. Klicken Sie mit Ihrem im
			Xcode-Projektnavigator ausgewählten Projekt auf **Build Settings** und suchen Sie nach `Objective-C Bridging Header`.

		7. Setzen Sie unter **Swift Compiler - General** den Wert für **Objective-C Bridging Header** auf den Pfad für den Überbrückungsheader. Der Pfad ist in Bezug auf das Stammverzeichnis Ihres Projekts relativ. Beispiel: Wenn das Projekt 'MQASampleApp' im Verzeichnis `/user/example/MQASampleApp` enthalten ist, lautet der Pfad `/user/example/MQASampleApp/MQASampleApp-Bridging-Header.h`. Wenn Ihre gespeicherte Datei im Stammverzeichnis des Projekts enthalten ist, können Sie die Umgebungsvariable verwenden, um den Pfad durch Eingabe von `${SRCROOT}/${PROJECT}-Bridging-Header.h` festzulegen.

		8. Speichern und erstellen Sie die App, um zu überprüfen, ob der Pfad korrekt ist.

	7. Überprüfen Sie in der Datei `info.plist` die folgenden Einstellungen in Ihren Projektangaben:

		* Bundle version - {{site.data.keyword.mqa}} verwendet den Wert aus diesem Feld, um zu bestimmen, wann eine Benachrichtigung über einen neuen Build an die Tester gesendet werden soll. Stellen Sie beim Hochladen eines neuen Builds nach {{site.data.keyword.mqa}} sicher, dass diese Zahl erhöht wird. Die Zeichenfolge im Feld für die Bundleversion ist auf Zahlen und den Punkt (.) beschränkt. Da es sich bei dieser Einschränkung um eine Xcode-Voraussetzung handelt, folgen die meisten Anwendungen dieser Konvention und es sind keine Änderungen erforderlich.
		* Bundle versions string - Dieses Feld enthält eine Zeichenfolgedarstellung Ihrer Versionsnummer. Für die Zeichenfolge gelten nicht dieselben Einschränkungen wie für das Feld mit der Bundleversion.

2. Konfigurieren Sie bei jeder Anmeldung einen neue zu startende Sitzung.

    1. Suchen Sie die Methode `didFinishLaunchingWithOptions` in Ihrer `AppDelegate`-Datei:

        * Objective-C: Datei `AppDelegate.m`
        * Swift: Datei `AppDelegate.swift`

	2. Starten Sie die {{site.data.keyword.mqa}}-Sitzung.

		* Objective-C

			1. Starten Sie die neue Sitzung in einer Methode innerhalb der Methode `applicationDelegate`, z. B. `didFinishLaunchingWithOptions`. Sie finden Ihren Delegierten durch Öffnen des Ordners mit demselben Namen wie Ihr Projekt im Projektnavigator. Suchen Sie nach der Datei `projectDelegate.m`.

			2. Fügen Sie den folgenden Code in der Methode `didFinishLaunchingWithOptions` vor der Zeile mit `return YES;` ein:

				```
				// Starts a quality assurance session using a
				    placeholder key and QA mode
				[MQALogger startNewSessionWithApplicationKey:@"Eigener Anwendungsschlüssel"];
				```
				{: codeblock}

			3. Ersetzen Sie die Variable *Eigener Anwendungsschlüssel* durch Ihren Anwendungsschlüssel aus {{site.data.keyword.mqa}}.
               Tipp: Ihr App-Schlüssel ist im {{site.data.keyword.mqa}}-Webbereich bei den App-Einstellungen zu finden.

		* Swift

			1. Suchen Sie die Methode `didFinishLaunchingWithOptions` in der Datei `AppDelegate.swift`:

			2. Fügen Sie den folgenden Code in der Methode vor der Zeile `return true` ein; dabei ist *Eigener Anwendungsschlüssel* ein gültiger Schlüssel für Ihre App:

				```
				// Set the application key
				MQALogger.startNewSession(withApplicationKey: "Your_Application_Key")
				```
				{: codeblock}

	3. Legen Sie fest, ob der Vorproduktionsmodus oder der Produktionsmodus verwendet werden soll. Informationen zu den Unterschieden zwischen Vorproduktions- und Produktionsmodus finden Sie im Abschnitt zu den [Unterschieden zwischen Vorproduktions- und Produktionsmodus ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/cPreprodvsProd.html){: new_window} im IBM Knowledge Center.

		* Objective-C

			1. Suchen Sie die Methode `didFinishLaunchingWithOptions`.

			2. Fügen Sie eine der folgenden Codezeilen innerhalb der Methode 'didFinishLaunchingWithOptions' vor der Zeile mit `return YES;` ein:

			Fügen Sie für die Verwendung des Vorproduktionsmodus die folgende Codezeile hinzu:

				```
				[[MQALogger settings] setMode:MQAModeQA];
				```
				{: codeblock}

			Fügen Sie für die Verwendung des Produktionsmodus die folgende Codezeile hinzu:

				```
				[[MQALogger settings] setMode:MQAModeMarket];
				```
				{: codeblock}

				**Objective-C - vollständiges Beispiel**
				<pre><code>
					- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
						{
					   // Override point for customization after application launch.
					   if ([[UIDevice currentDevice] userInterfaceIdiom] == UIUserInterfaceIdiomPad) {
					      UISplitViewController *splitViewController = (UISplitViewController*)self.window.rootViewController;
					      UINavigationController *navigationController = [splitViewController.viewControllers lastObject];
					      splitViewController.delegate = (id)navigationController.topViewController;
						}
					     #ifdef Debug
					   [[MQALogger settings] setMode:MQAModeQA];
					   #else
					   [[MQALogger settings] setMode:MQAModeMarket];
					   #endif
					      // Starts a quality assurance session using a placeholder key
					      [MQALogger startNewSessionWithApplicationKey:@"Your-Application-Key"];
					      // Enables the quality assurance application crash reporting
					      NSSetUncaughtExceptionHandler(&MQAUncaughtExceptionHandler);
					      return YES; }
				</code></pre>
				{: codeblock}

        * Swift

			1. Suchen Sie in der Datei 'AppDelegate.swift' nach der Methode `didFinishLaunchingWithOptions`.

			2. Fügen Sie die folgenden Zeilen zu Ihrer Methode `didFinishLaunchingWithOptions` vor der Zeile ein, in der `return true` steht:

				```
				//Set the SDK mode Market vs QA for Production
				   and Pre-Production
				#if Debug
				  MQALogger.settings().mode = MQAMode.QA
				#elseif Release
				  MQALogger.settings().mode = MQAMode.Market
				#endif
				```
				{: codeblock}

			Im Folgenden sehen Sie ein Codebeispiel:

				```
				func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

				//Set the SDK mode Market vs QA for Production
				   and Pre-Production
				#if Debug
					MQALogger.settings().mode = MQAMode.QA
				#elseif Release
					MQALogger.settings().mode = MQAMode.Market
				#endif

				// Set the application key
				MQALogger.startNewSession(withApplicationKey: "Your_Application_Key")

				// Override point for customization after
				   application launch.
				return true
				```
				{: codeblock}

				**Swift - vollständiges Beispiel**
				<pre><code>				
				func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions:[NSObject: AnyObject]?) -> Bool {
					// Override point for customization after application launch.
					//Set the Shake Device option to true or false. If this is not explicitly set, the Shake Device is enabled by default.
					MQALogger.settings().reportOnShakeEnabled = true
					//Set the SDK mode Market vs QA for Production and Pre-Production
					#if Debug
					MQALogger.settings().mode = MQAMode.QA
					#elseif Release
					MQALogger.settings().mode = MQAMode.Market
					#endif

				//Start the MQA session with the specified app key
					   MQALogger.startNewSession(withApplicationKey: "Your_Application_Key")
				// Enables MQA crash reporting to catch uncaught exceptions
					   NSSetUncaughtExceptionHandler(exceptionHandlerPointer);

					   return true
					}
				</code></pre>
				{: codeblock}

3. Führen Sie Ihre App aus, um sicherzustellen, dass {{site.data.keyword.mqa}} beim Start der App gestartet wird.

4. Fahren Sie mit den Schritten auf der Seite [Einführung in {{site.data.keyword.mqa}}](index.html) fort.

# Zugehörige Links
{: #rellinks notoc}

## Zugehörige Links
{: #general notoc}
* [Einführung in {{site.data.keyword.mqa}}](index.html){:new_window}
