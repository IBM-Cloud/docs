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

# Strumentazione di MQA con un'applicazione iOS (Obsoleto)
{: #instrumentios}

Per utilizzare {{site.data.keyword.mqafull}} con la tua applicazione iOS, devi scaricare l'SDK e strumentarla effettuando alcune modifiche utilizzando l'ambiente di sviluppo Xcode.
{: shortdesc}

Prima di poter strumentare un'applicazione con {{site.data.keyword.mqa}}, devi avere un account {{site.data.keyword.Bluemix}} e aver correttamente installato la versione dell'ambiente di sviluppo per le piattaforme dell'applicazione che stai strumentando. 

Per strumentare {{site.data.keyword.mqa}} in modo che utilizzi la tua applicazione Objective-C o Swift, completa la seguente procedura: 

1. Aggiungi le autorizzazioni necessarie e la SDK scaricata al tuo progetto iOS.

	1. Crea o apri il tuo progetto in Xcode.

	2. Aggiungi le seguenti librerie di dipendenze selezionando `+` nella sezione *Linked Frameworks and Libraries* della scheda *General* del tuo progetto Xcode:

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

	3. Trascina l'SDK {{site.data.keyword.mqa}} per la cartella `Q4M.framework` iOS nel gruppo **Frameworks** nella struttura ad albero del navigator. Nella finestra delle opzioni di scelta, seleziona *Copy items if needed*, **Create groups** e spunta la casella del tuo nome progetto come destinazione.

	4. In sezione di collegamento della scheda *Build Settings*, configura *Other Linker flags* per il debug e il rilascio di **-ObjC**. Importante: assicurati che la scheda *All* sia selezionata in modo che gli indicatori Other Linker siano inclusi nell'elenco.

	5. *Solo per Objective-C:* aggiungi la seguente importante istruzione ai file `AppDelegate.m` e `ViewController.m`:

		```
		#import <Q4M/MQALogger.h>
		```
		{: codeblock}

	6. *Solo per Swift:* aggiungi un'intestazione di collegamento Objective-C per l'SDK {{site.data.keyword.mqa}} per iOS completando la seguente procedura:

		1. Fai clic con il tasto destro sul nodo root e seleziona **New File**.

		2. Nella finestra Choose Template in iOS, fai clic sul template Header File nella sezione Source.

		3. Denomina il file `MyProject-Bridging-Header.h`, dove *MyProject* è il nome del tuo progetto Swift e seleziona il nome del tuo progetto come destinazione. Ad esempio, denomina il file `MyProject-Bridging-Header.h`.

		4. Fai clic su **Create** per salvare il file nella root del tuo progetto.

		5. Nel file dell'intestazione di collegamento, aggiungi la seguente importante istruzione per il file dell'intestazione di collegamento:

			```
			#import <Q4M/MQALogger.h>
			```
			{: codeblock}

		6. Con il tuo progetto selezionato nel
			Xcode Project Navigator, fai clic su **Build Settings** e cerca `Objective-C Bridging Header`.

		7. In **Swift Compiler - General**, imposta il valore di **Objective-C Bridging Header** sul percorso dell'intestazione di collegamento. Il percorso è correlato alla root del tuo progetto. Ad esempio, se il progetto  MQASampleApp si trova in `/user/example/MQASampleApp`, di conseguenza il percorso è `/user/example/MQASampleApp/MQASampleApp-Bridging-Header.h`. Se hai salvato il tuo file nella root del progetto, puoi quindi utilizzare la variabile di ambiente per impostare il percorso immettendo `${SRCROOT}/${PROJECT}-Bridging-Header.h`.

		8. Salva e crea l'applicazione per verificare che il percorso sia corretto.

	7. Nel file `info.plist`, verifica le seguenti impostazioni nelle tue informazioni sul progetto:

		* Versione bundle - {{site.data.keyword.mqa}} utilizza il valore da questo campo per determinare quando inviare una nuova notifica di creazione ai tester. Quando carichi una nuova build in {{site.data.keyword.mqa}}, assicurati di incrementare questo numero. La stringa nel campo della versione bundle è limitato a numeri a e al carattere punto (.). Poiché questa restrizione è un requisito Xcode, molte applicazioni seguono questa convenzione e non richiedono modifiche.
		* Stringa delle versioni bundle - Questo campo contiene una rappresentazione della stringa del tuo numero di versione. La stringa non ha le stesse limitazioni del campo della versione bundle.

2. Configura una nuova sessione da avviare per ogni accesso.

    1. Individua il metodo `didFinishLaunchingWithOptions` nel tuo file `AppDelegate`:

        * Objective-C: file `AppDelegate.m`
        * Swift: file `AppDelegate.swift`

	2. Avvia la sessione {{site.data.keyword.mqa}}.

		* Objective-C

			1. Avvia la nuova sessione in un metodo nel tuo metodo `applicationDelegate`, come ad esempio il metodo `didFinishLaunchingWithOptions`. Puoi trovare il tuo delegato aprendo la cartella con lo stesso nome del tuo progetto nel navigator del progetto. Ricerca il file `projectDelegate.m`.

			2. Aggiungi il seguente codice nel metodo `didFinishLaunchingWithOptions` prima della linea con `return YES;`:

				```
				// Avvia una sessione di controllo qualità utilizzando una chiave segnaposto
				    e la modalità QA
				[MQALogger startNewSessionWithApplicationKey:@"Your_Application_Key"];
				```
				{: codeblock}

			3. Sostituisci la variabile *Your_Application_Key* con la tua chiave dell'applicazione da {{site.data.keyword.mqa}}.
               Suggerimento: puoi trovare la chiave dell'applicazione nel pannello web {{site.data.keyword.mqa}} nelle impostazioni dell'applicazione:

		* Swift

			1. Individua il metodo `didFinishLaunchingWithOptions` nel file `AppDelegate.swift`.

			2. Aggiungi il seguente codice nel metodo prima della linea che legge `return true`, dove *Your_Application_Key* è una chiave valida per la tua applicazione:

				```
				// Configura la chiave dell'applicazione
				MQALogger.startNewSession(withApplicationKey: "Your_Application_Key")
				```
				{: codeblock}

	3. Definisci se utilizzare la modalità di preproduzione o di produzione. Per informazioni sulle differenze tra la modalità di preproduzione e di produzione, consulta [Differences between preproduction and production modes ![icona link esterno](../../icons/launch-glyph.svg "icona link esterno")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/cPreprodvsProd.html){: new_window} nel IBM Knowledge Center.

		* Objective-C

			1. Individua il metodo `didFinishLaunchingWithOptions`.

			2. Aggiungi uno delle seguenti righe al codice nel metodo didFinishLaunchingWithOptions prima della riga con `return YES;`:

			Per utilizzare la modalità di preproduzione, aggiungi questa riga al codice:

				```
				[[MQALogger settings] setMode:MQAModeQA];
				```
				{: codeblock}

			Per utilizzare la modalità di produzione, aggiungi questa riga al codice:

				```
				[[MQALogger settings] setMode:MQAModeMarket];
				```
				{: codeblock}

				**Esempio completo Objective-C**
				<pre><code>
					- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
						{
					   // Punto di sovrascrittura per la personalizzazione dopo l'avvio dell'applicazione.
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
					      // Avvia una sessione di controllo qualità utilizzando una chiave segnaposto
					      [MQALogger startNewSessionWithApplicationKey:@"Your-Application-Key"];
					      // Abilita il report di arresto dell'applicazione del controllo qualità
					      NSSetUncaughtExceptionHandler(&MQAUncaughtExceptionHandler);
					      return YES; }
				</code></pre>
				{: codeblock}

        * Swift

			1. Nel file AppDelegate.swift, ricerca il metodo `didFinishLaunchingWithOptions`.

			2. Aggiungi le seguenti righe al tuo metodo `didFinishLaunchingWithOptions` prima della riga che legge `return true`:

				```
				//Configura la modalità SDK Market vs QA for Production
				   and Pre-Production
				#if Debug
				  MQALogger.settings().mode = MQAMode.QA
				#elseif Release
				  MQALogger.settings().mode = MQAMode.Market
				#endif
				```
				{: codeblock}

			Un esempio del codice è:

				```
				func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

				//Configura la modalità SDK Market vs QA for Production
				   and Pre-Production
				#if Debug
				  MQALogger.settings().mode = MQAMode.QA
				#elseif Release
				  MQALogger.settings().mode = MQAMode.Market
				#endif

				// Configura la chiave dell'applicazione
				MQALogger.startNewSession(withApplicationKey: "Your_Application_Key")

				// Punto di sovrascrittura per la personalizzazione dopo
				   l'avvio dell'applicazione.
				return true
				```
				{: codeblock}

				**Esempio completo Swift**
				<pre><code>				
				func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions:[NSObject: AnyObject]?) -> Bool {
					// Punto di sovrascrittura per la personalizzazione dopo l'avvio dell'applicazione.
					//Imposta l'opzione Shake Device su true o false. Se questa opzione non viene impostata esplicitamente, Shake Device viene abilitato per impostazione predefinita.
					MQALogger.settings().reportOnShakeEnabled = true
					//Configura la modalità SDK Market vs QA for Production and Pre-Production
					#if Debug
					MQALogger.settings().mode = MQAMode.QA
					#elseif Release
					MQALogger.settings().mode = MQAMode.Market
					#endif

				//Avvia la sessione MQA con la chiave dell'applicazione specificata
					   MQALogger.startNewSession(withApplicationKey: "Your_Application_Key")
				// Abilita il report degli arresti MQA per acquisire le eccezioni non rilevate
					   NSSetUncaughtExceptionHandler(exceptionHandlerPointer);

					   return true
					}
				</code></pre>
				{: codeblock}

3. Esegui la tua applicazione per assicurarti che {{site.data.keyword.mqa}} si avvii quando si avvia l'applicazione.

4. Continua con la procedura nella pagina [Introduzione a {{site.data.keyword.mqa}}](index.html).

# Link correlati
{: #rellinks notoc}

## Link correlati
{: #general notoc}
* [Introduzione a {{site.data.keyword.mqa}}](index.html){:new_window}
