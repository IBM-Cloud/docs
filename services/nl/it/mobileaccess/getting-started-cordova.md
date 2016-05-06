---

copyright:
  years: 2015, 2016
  
---

# Configurazione del plugin Cordova
{: #getting-started-cordova}

Strumenta la tua applicazione Cordova con l'SDK client {{site.data.keyword.amashort}}, inizializza l'SDK ed effettua richieste alle risorse protette e non protette.

## Prima di cominciare
{: #before-you-begin}

- Devi disporre di un'istanza di un backend mobile protetto dal servizio {{site.data.keyword.amashort}}. Per ulteriori informazioni su come creare un backend mobile, consulta [Introduzione](getting-started.html).

- Crea un'applicazione Cordova o utilizza un progetto esistente. Per ulteriori informazioni su come configurare la tua applicazione Cordova, consulta il [sito web di Cordova](https://cordova.apache.org/).

## Installazione del plugin Cordova {{site.data.keyword.amashort}}
{: #getting-started-cordova-plugin}

L'SDK client {{site.data.keyword.amashort}} è un plugin Cordova che racchiude gli SDK client {{site.data.keyword.amashort}} nativi. Viene distribuito utilizzando
l'interfaccia riga di comando (CLI) Cordova e `npmjs`, un repository di plug-in per i progetti Cordova. La CLI Cordova scarica automaticamente i plugin dai repository e li rende disponibili alla tua applicazione Cordova.

1. Aggiungi le piattaforme Android e iOS alla tua applicazione Cordova. Dalla riga di comando, esegui uno dei seguenti comandi, o entrambi:

	```Bash
	cordova platform add android
	```

	```Bash
	cordova platform add ios
	```

1. Se hai aggiunto la piattaforma Android, devi aggiungere il livello API minimo supportato al file `config.xml` della
tua applicazione Cordova. Apri il file `config.xml` e aggiungi la seguente riga all'elemento `<platform name="android">`:

	```XML
	<platform name="android">  
		<preference name="android-minSdkVersion" value="15"/>
  	<preference name="android-targetSdkVersion" value="23"/>
		<!-- add minimum and target Android API level declaration -->
	</platform>
	```

	Il valore *minSdkVersion* deve essere maggiore di `15`. Il valore *targetSdkVersion* deve essere l'SDK Android più recente disponibile da Google.

1. Se hai aggiunto il sistema operativo iOS, aggiorna l'elemento `<platform name="ios">` con una dichiarazione di destinazione:

	```XML
	<platform name="ios">
    <preference name="deployment-target" value="8.0"/>
		<!-- add deployment target declaration -->
	</platform>
	```

1. Installa il plugin Cordova {{site.data.keyword.amashort}}:

 	```Bash
	cordova plugin add ibm-mfp-core
	```

1. Configura la tua piattaforma per Android, iOS o entrambi.

	* **Android**

		Prima di aprire il tuo progetto in Android Studio, genera la tua applicazione Cordova tramite l'interfaccia riga di comando (CLI) per evitare errori di generazione.

		```
		cordova build android
		```

	* **iOS**

		Per evitare errori durante la generazione, configura il tuo progetto Xcode nel seguente modo.

		1. Utilizza la versione più recente di Xcode per aprire il tuo file xcode.proj nella directory &lt;*nome_applicazione*&gt;/platforms/ios.

		**Importante:** se ricevi un messaggio che indica di eseguire la conversione alla sintassi Swift più recente ("Convert to Latest Swift Syntax"), fai clic su Cancel.

		2. Vai a **Build Settings > Swift Compiler - Code Generation > Objective-C Bridging Header** e aggiungi il seguente percorso:

			```
			<il_nome_del_tuo_progetto>/Plugins/ibm-mfp-core/Bridging-Header.h
			```

		3. Vai a **Build settings > Linking > Runpath Search Paths** e aggiungi il seguente parametro Frameworks:

			```
			@executable_path/Frameworks
			```

		4. Genera ed esegui la tua applicazione con Xcode.

1. Verifica che il plugin sia stato installato correttamente eseguendo questo comando:

	```Bash
	cordova plugin list
	```

## Inizializzazione del plugin client {{site.data.keyword.amashort}}
{: #getting-started-cordova-initialize}

Per utilizzare l'SDK client {{site.data.keyword.amashort}}, devi inizializzare l'SDK passando i parametri *applicationGUID* e *applicationRoute*.

1. Trova i tuoi valori di rotta e GUID applicazione sula pagina principale del dashboard {{site.data.keyword.Bluemix_notm}}. Fai clic sul nome della tua applicazione e quindi su **Opzioni mobili** per visualizzare i valori rotta applicazione (**Application Route**) e GUID applicazione (**Application GUID**) per inizializzare l'SDK.

3. Aggiungi la seguente chiamata al tuo file `index.js` per inizializzare l'SDK client {{site.data.keyword.amashort}}. Sostituisci *applicationRoute* e *applicationGUID* con i valori da **Opzioni mobili** nel dashboard {{site.data.keyword.Bluemix_notm}}.

	```JavaScript
	BMSClient.initialize("applicationRoute", "applicationGUID");
	```

## Effettuazione di una richiesta al backend mobile
{: #getting-started-request}

Dopo che l'SDK client {{site.data.keyword.amashort}} è stato inizializzato, puoi iniziare a effettuare richieste al tuo backend mobile.

1. Prova a inviare una richiesta a un endpoint protetto del tuo nuovo backend mobile. Nel tuo browser, apri il seguente URL: `{applicationRoute}/protected`. Ad esempio:

	```
	http://my-mobile-backend.mybluemix.net/protected
	```

	L'endpoint `/protected` di un backend mobile creato con il contenitore tipo MobileFirst Services Starter è protetto con {{site.data.keyword.amashort}}. Nel tuo browser viene restituito un messaggio `Unauthorized`. Questo messaggio viene restituito perché a questo endpoint accedono solo le applicazioni mobili strumentate con l'SDK client {{site.data.keyword.amashort}}.

1. Utilizza la tua applicazione Cordova per effettuare una richiesta allo stesso endpoint. Aggiungi il seguente codice dopo che hai inizializzato `BMSClient`:

	```Javascript
	var success = function(data){
	console.log("success", data);
	}

	var failure = function(error){
		console.log("failure", error);
	}

	var request = new MFPRequest("/protected", MFPRequest.GET);

	request.send(success, failure);
	```

1. Quando la tua richiesta ha esito positivo, vedrai il seguente output nella console LogCat o Xcode (a seconda della piattaforma che stai usando):

	![immagine](images/getting-started-android-success.png)

	## Fasi successive
	{: #next-steps}

	Quando ti sei connesso all'endpoint protetto, non è stata richiesta alcuna credenziale. Per richiedere ai tuoi utenti di accedere alla tua applicazione, devi configurare l'autenticazione Facebook, Google o personalizzata.
	* [Facebook](facebook-auth-cordova.html)
	* [Google](google-auth-cordova.html)
	* [Personalizzata](custom-auth-cordova.html)
