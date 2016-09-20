---

copyright:
  years: 2015-2016

---

<!-- Attribute definitions -->
{:codeblock: .codeblock}

# Introduzione all'esempio Hello Bluemix per iOS
{: #gettingstarted-android}
Ultimo aggiornamento: 1 giugno 2016
{: .last-updated}  

Se desideri iniziare a lavorare con una nuova applicazione iOS, puoi utilizzare l'applicazione Hello Bluemix. Questa applicazione illustra come stabilire una connessione al tuo backend {{site.data.keyword.Bluemix}} da un'applicazione mobile senza autenticazione. Quando sei pronto, puoi ottenere le specifiche librerie
    che desideri utilizzare nella tua applicazione.

1. Crea il tuo backend mobile in {{site.data.keyword.Bluemix_notm}}.
    1. Nella sezione Contenitori tipo del catalogo {{site.data.keyword.Bluemix_notm}}, fai clic su MobileFirst Services Starter.
    2. Immetti un nome e un host per la tua applicazione e fai clic su **Crea**.
    3. Fai clic su **Fine**.
2. Esegui l'applicazione di esempio Hello Bluemix:
	1. Ottieni il progetto da GitHub. Per ottenere il progetto puoi, facoltativamente, utilizzare il comando git clone. Dal tuo computer, apri il terminale e immetti quindi il seguente comando:
    ```
    git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-hellobluemix.git
    ```
	2. Esegui il comando `pod install` dall'interno della directory `bms-samples-swift-hellobluemix`, in cui è stato clonato il progetto. Se non hai installato Cocoapods, scaricalo da [https://cocoapods.org](https://cocoapods.org).
	3. Apri lo spazio di lavoro Xcode con il comando `open HelloBluemix.xcworkspace`.
	4. Nel tuo file `AppDelegate.swift`, aggiorna i valori appRoute e appGuid con quelli ottenuti dal backend di Bluemix che hai creato precedentemente.

3. Esegui l'esempio nel tuo ambiente di sviluppo. In Xcode, fai clic su **Product&gt;Run**. Viene avviato un simulatore iOS.

	**Importante:** il tuo appRoute deve utilizzare un protocollo `https` e non `http` o potresti riscontrare un errore di connessione dovuto alle impostazioni ATS (App Transport Security). Puoi avere maggiori informazioni su queste impostazioni nel post del blog [Connect your iOS 9 app to Bluemix today](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/).
	
4. Nel simulatore,
                fai clic su **Ping {{site.data.keyword.Bluemix_notm}}**. L'applicazione di esempio ottiene l'intestazione di autorizzazione dal servizio Mobile Client Access. Se il ping ha esito positivo,
            il testo nel simulatore viene aggiornato.

  Dopo che hai stabilito correttamente una connessione a {{site.data.keyword.Bluemix_notm}} dall'applicazione mobile in Xcode, viene visualizzato:
  `Yay! You are connected`
  {: screen}

  <!--
  ![Hello World application successfully connected to {{site.data.keyword.Bluemix_notm}}](images/yayconnected.jpg "Figure 1. Hello World application successfully connected to Bluemix")
-->

  Se la connessione non riesce, visualizzerai:
  `Bummer. Something went wrong`
  {: screen}

 <!--
  ![Hello World application not connected to Bluemix](images/bummer_android.jpg "Figure 2. Hello World application not connected to Bluemix")
  -->

	Puoi risolvere il problema riguardo la connessione non riuscita nel seguente modo:
	* Verifica di aver incollato correttamente i valori di instradamento e GUID.
	* Rivedi il log di debug per ulteriori informazioni.


## Passi successivi:
{: #next}
Per informazioni su come ottenere l'SDK e integrarlo nella tua applicazione mobile, consulta le informazioni relative all'impostazione dei servizi Bluemix.
   * [Mobile Client Access](../../services/mobileaccess/index.html)
   * [Push](../../services/mobilepush/index.html)

# rellinks

## samples
   * [Hello Bluemix sample (iOS)](https://github.com/ibm-bluemix-mobile-services/bms-samples-swift-hellobluemix)

## sdk
   * [Core SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)

## api
   * [API Core](https://www.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)
