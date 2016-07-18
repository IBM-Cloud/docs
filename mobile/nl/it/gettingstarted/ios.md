---

copyright:
  years: 2015-2016

---

<!-- Attribute definitions -->
{:codeblock: .codeblock}

# Introduzione all'esempio Hello Bluemix per iOS
{: #gettingstarted-android}
*Ultimo aggiornamento: 1 giugno 2016*
{: .last-updated}  

Se desideri iniziare a lavorare con una nuova applicazione iOS, puoi utilizzare l'applicazione HelloWorld. Questa applicazione illustra come stabilire una connessione al tuo backend {{site.data.keyword.Bluemix}} da un'applicazione mobile senza autenticazione. Nell'applicazione è già installato l'SDK. Quando sei pronto, puoi ottenere le specifiche librerie
    che desideri utilizzare nella tua applicazione.

1. Crea il tuo backend mobile in {{site.data.keyword.Bluemix_notm}}.
    1. Nella sezione Contenitori tipo del catalogo {{site.data.keyword.Bluemix_notm}}, fai clic su MobileFirst Services Starter.
    2. Immetti un nome e un host per la tua applicazione e fai clic su **Crea**.
    3. Fai clic su **Fine**.
2. Ottieni il progetto da GitHub. Per ottenere il progetto puoi, facoltativamente, utilizzare il comando git clone. Dal tuo computer, apri il terminale e immetti quindi il seguente comando:
    ```
    git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloworld.git
    ```

3. Inizializza il progetto. Per inizializzare l'SDK, copia il seguente codice nel metodo `didFinishLaunchingWithOptions` nel delegato dell'applicazione.

	###Ojbective-C
	{: initializeobjc}

	**Importante**: mentre l'SDK Objective-C rimane completamente supportato ed è ancora considerato l'SDK primario per i servizi mobili {{site.data.keyword.Bluemix}}, è stato pianificato di abbandonarlo più avanti quest'anno a favore del nuovo SDK Swift.

	l'SDK Objective-C riporta i dati di monitoraggio alla console di monitoraggio del servizio {{site.data.keyword.amashort}}. Se ti affidi alle funzioni di monitoraggio del servizio {{site.data.keyword.amashort}}, continua ad utilizzare l'SDK Objective-C.

	```
	// inizializza l'SDK con l'ID e la rotta dell'applicazione IBM Bluemix
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:@"<insert route>" backendGUID:@"<insertGUID>"];
return YES;
	```

	###Swift
	{: initializeswift}
	```
	// inizializza l'SDK con l'ID e l'instradamento dell'applicazione IBM Bluemix
IMFClient.sharedInstance().initializeWithBackendRoute("<insert route>", backendGUID: "<insertGUID>")
return true
	```

4. Esegui l'esempio nel tuo ambiente di sviluppo. In Xcode, fai clic su **Product&gt;Run**. Viene avviato un simulatore iOS.
5. Nel simulatore,
                fai clic su **Ping {{site.data.keyword.Bluemix_notm}}**. L'applicazione di esempio ottiene l'intestazione di autorizzazione dal servizio Mobile Client Access. Se il ping ha esito positivo,
            il testo nel simulatore viene aggiornato.

  Dopo che hai stabilito correttamente una connessione a {{site.data.keyword.Bluemix_notm}} dall'applicazione mobile in Xcode, viene visualizzato il seguente messaggio:

  `Yay! You are connected`
  {: screen}

  ![Applicazione Hello World connessa correttamente a {{site.data.keyword.Bluemix_notm}}](images/yayconnected.jpg "Figura 1. Applicazione Hello World connessa correttamente a Bluemix")

  Se la connessione non riesce, visualizzerai:
  `Bummer. Something went wrong`
  {: screen}

  ![Applicazione Hello World non connessa a Bluemix](images/bummer_android.jpg "Figura 2. Applicazione Hello World non connessa a Bluemix")

	Puoi risolvere il problema riguardo la connessione non riuscita nel seguente modo:
	* Verifica di aver incollato correttamente i valori di instradamento e GUID.
		####Objective-C
		{: #objcvals}
		```
		[imfClient initializeWithBackendRoute:@"https://hellotest.mybluemix.net"
  backendGUID:@"9d48d73a-0878-4254-test-bdcbe6c79c31"];
		```

		####Swift
		{: #swiftvals}
		```
		IMFClient.sharedInstance().initializeWithBackendRoute("https://hellotest.mybluemix.net", backendGUID: "9d48d73a-0878-4254-test-bdcbe6c79c31")
		```

	* Rivedi il log di debug per ulteriori informazioni.


## Passi successivi:
{: #next}
Per informazioni su come ottenere l'SDK e integrarlo nella tua applicazione mobile, consulta le informazioni relative all'impostazione dei servizi Bluemix.
   * [Mobile Client Access](../../services/mobileaccess/index.html)
   * [Push](../../services/mobilepush/index.html)

# rellinks

## samples
   * [Esempio Hello Bluemix](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloworld)

## sdk
   * [Core SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)

## api
   * [API Core](https://www.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)
