---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}

# Inizializzazione del plugin Cordova
{: #cordova_enable}

Prima di poter utilizzare il plugin Cordova del servizio Push Notification, devi inizializzarlo passando
la rotta e il GUID dell'applicazione. Dopo che hai inizializzato il plugin, puoi stabilire una connessione all'applicazione server che hai creato nel dashboard Bluemix. Il plugin Cordova è il contenitore per gli SDK client Android e iOS per abilitare un'applicazione Cordova a comunicare con i servizi Bluemix.

1. Inizializza il BMSClient copiando e incollando il seguente frammento di codice nel tuo file JavaScript principale (normalmente ubicato nella directory **www/js**).

	```
	BMSClient.initialize("https://myapp.mybluemix.net","abcd1234-abcd-1234-abcd-abcd1234abcd");
	```
1. Modifica il frammento di codice per utilizzare la tua rotta Bluemix e i parametri appGUID. Fai clic sul link **Opzioni mobili** nel tuo dashboard dell'applicazione Bluemix per ottenere rotta e GUID dell'applicazione. Utilizza i valori rotta e GUID dell'applicazione come tuoi parametri nel tuo frammento di codice `BMSClient.initialize`.


	**Nota**: se hai creato un'applicazione Cordova utilizzando la CLI di Cordova, ad esempio, con il comando Cordova create app-name, inserisci questo codice Javascript nel file **index.js**, dopo la funzione `app.receivedEvent` nella funzione `onDeviceReady: function()` per inizializzare il client BMS.

	```
	onDeviceReady: function() {
	    app.receivedEvent('deviceready');
	    BMSClient.initialize("https://myapp.mybluemix.net","abcd1234-abcd-1234-abcd-abcd1234abcd");
	    },
	```
1. Fase successiva. [Registrazione di dispositivi](t_cordova_register.html).
