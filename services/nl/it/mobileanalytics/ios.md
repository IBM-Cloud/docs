<!-- Attribute definitions -->
{:codeblock: .codeblock}
{:screen: .screen}

# Introduzione all'esempio HelloWorld
{: #gettingstarted-ios}
Se desideri iniziare a lavorare con una nuova applicazione iOS, puoi utilizzare l'applicazione HelloWorld. Questa applicazione illustra come stabilire una connessione al tuo backend {{site.data.keyword.Bluemix}} da un'applicazione mobile senza autenticazione. Nell'applicazione è già installato l'SDK. Quando sei pronto, puoi ottenere le specifiche librerie che desideri utilizzare nella tua applicazione.

1. Crea il tuo backend mobile in {{site.data.keyword.Bluemix_notm}}.
<ol>
	<li>Nella sezione Contenitori tipo del catalogo {{site.data.keyword.Bluemix_notm}}, fare clic su **MobileFirst Services Starter**.</li>
    <li>Immetti un nome e un host per la tua applicazione e fai clic su **Crea**.</li>
    <li>Fai clic su **Fine**. </li>
</ol>
2. Ottieni il progetto da GitHub.
Dal tuo computer, apri il terminale e immetti il seguente comando:
```
git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloworld
```

3. Inizializza il progetto.
Per inizializzare l'SDK, copia il seguente codice nel metodo `didFinishLaunchingWithOptions` nel delegato dell'applicazione.
   * Objective-C:
```
// inizializza l'SDK con l'ID e la rotta dell'applicazione IBM Bluemix
IMFClient *imfClient = [IMFClient sharedInstance];
[imfClient initializeWithBackendRoute:@"<insert route>" backendGUID:@"<insertGUID>"];
return YES;
```{: codeblock}
   * Swift:
```
// inizializza l'SDK con l'ID e l'instradamento dell'applicazione IBM Bluemix
IMFClient.sharedInstance().initializeWithBackendRoute("<insert route>", backendGUID: "<insertGUID>")
return true
```{: codeblock}

4. Esegui l'esempio nel tuo ambiente di sviluppo.
In Xcode, fai clic su **Prodotto &gt; Esegui**. Viene avviato un simulatore iOS.
Nel simulatore, fai clic su **Esegui ping di {{site.data.keyword.Bluemix_notm}}**. L'applicazione di esempio ottiene l'intestazione di autorizzazione dal servizio Mobile Client Access. Se il ping ha esito positivo, il testo nel simulatore viene aggiornato.
<>Quando stabilisci correttamente una connessione a {{site.data.keyword.Bluemix_notm}} dall'applicazione mobile in Xcode, viene visualizzato un messaggio che indica che la connessione è stata stabilita correttamente (Yay! You are connected):<br/>
![Applicazione Hello World connessa correttamente a {{site.data.keyword.Bluemix_notm}}](images/yayconnected.jpg "Figura 1. Applicazione Hello World connessa correttamente a {{site.data.keyword.Bluemix_notm}}")
<br/>
Se stabilisci correttamente una connessione, l'Xcode di accesso di debug contiene un messaggio che indica che la connessione è stata stabilita correttamente:
```
Connessione a {{site.data.keyword.Bluemix_notm}} stabilita correttamente
```
5. Risolvi gli eventuali problemi.
Quando la connessione non riesce, viene visualizzato un messaggio che indica che qualcosa è andato storto ("Bummer Something went wrong"). Sono incluse ulteriori informazioni sull'errore.<br/>
![Applicazione Hello World non connessa a {{site.data.keyword.Bluemix_notm}}](images/bummer_android.jpg "Figura 2. Applicazione Hello World non connessa a Bluemix")
<br/>Verifica di avere incollato correttamente i valori di rotta e GUID:
   * Objective-C:
  ```
  [imfClient initializeWithBackendRoute:@"https://hellotest.mybluemix.net"
  backendGUID:@"9d48d73a-0878-4254-test-bdcbe6c79c31"];
  ``` {: codeblock}
   * Swift:
  ```
  IMFClient.sharedInstance().initializeWithBackendRoute("https://hellotest.mybluemix.net", backendGUID: "9d48d73a-0878-4254-test-bdcbe6c79c31")
  ```{: codeblock}


Puoi anche controllare il log di debug per ulteriori informazioni.

## Passi successivi:
{: #next}
Per informazioni su come ottenere l'SDK e integrarlo nella tua applicazione mobile, consulta le informazioni relative all'impostazione dei servizi {{site.data.keyword.Bluemix}}.
   * [Mobile Client Access](../../services/mobileaccess/index.html)
   * [Push](../../services/mobilepush/index.html)

# rellinks

## samples
   * [HelloWorld (iOS)](https://github.com/ibm-bluemix-mobile-services/bms-samples-ios-helloworld)

## sdk
   * [bms-clientsdk-ios-core](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-ios-core)

## api
   *
[API Core](https://www.{DomainName}/docs/api/content/api/mobilefirst/ios/IMFCore_api-doc/html/index.html)
