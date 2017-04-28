---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Risoluzione dei problemi
{: #errors}
Ultimo aggiornamento: 12 aprile 2017
{: .last-updated}

Questo argomento ti guida nell'identificazione e nella risoluzione dei possibili scenari di errore che potrebbero verificarsi durante l'utilizzo del servizio Push Notifications.

## Risoluzione dei problemi comuni delle notifiche di push
{: #troubleshooting_notification_errors}

### Si è verificato un errore server interno. Per favore contatta l'amministratore. (Codice errore interno: PUSHD102E)
{: #troubleshooting_notification_internal}

**Spiegazione**: questo errore potrebbe verificarsi se hai creato un'istanza di push prima del novembre 2015.  

**Risposta utente**: per risolvere il problema, elimina l'istanza di push e creane una nuova. Nota che quando elimini l'istanza di push, le tue tag non vengono conservate.


### Registrazione non autorizzata
{: #troubleshooting_notification_unauth}

**Spiegazione**: Chrome Web Push non funziona con le chiavi FCM (Firebase Cloud Messaging). Se non puoi ricevere le notifiche push web su Chrome dopo lo spostamento a FCM da GCM, questo succede perché il sito web era stato precedentemente configurato per utilizzare il progetto GCM mentre il nuovo progetto è stato creato in FCM. I token generati che identificano il browser vengono memorizzati nella cache dal browser Chrome.

**Risposta utente**: puoi risolvere questo problema rimuovendo i cookie e reimpostando le autorizzazioni del browser. Questo richiederà alle autorizzazioni di abilitare Push Notifications. 


### I worker del servizio non sono supportati in questo browser
{: #troubleshooting_notification_service_workers}

**Spiegazione**: l'SDK che era stato incluso come parte di `BMSPushSDK.js` mediante il worker del servizio non è disponibile. 

**Risposta utente**: si consiglia di passare a un browser che supporti il worker del servizio. Le versioni supportate dei browser sono Firefox versione 49 o successive e Chrome versione 53 (64 bit) o successive.


### SecurityError: l'operazione non è sicura
{: #troubleshooting_notification_insecure}

**Spiegazione**:  si potrebbe visualizzare l'errore durante l'abilitazione della console web in Firefox. Il supporto push web nel servizio Push Notification richiede l'accesso al sito web tramite il protocollo `https` invece di `http`.

**Risposta utente**: si consiglia di provare a connettersi al sito web utilizzando il protocollo `https` dal browser.


## Risoluzione degli errori di configurazione push web
{: #troubleshooting_configuration_errors}

Puoi diagnosticare gli errori correlati alla configurazione push web utilizzando il file `BMSPushSDK.js`. Il file contiene informazioni relative all'errore. 

Per analizzare un errore restituito nel callback, considera il seguente codice di esempio:

```
function showStatus(response) {
 if(response.statusCode == 200 || response.statusCode == 201) {
   		document.getElementById("status").innerHTML = "Response is " + response.response;
   	}
   	else if(response.statusCode == 0) {
  		if(response.response) {
  			document.getElementById("status").innerHTML = response.response;	
    		}
    		else {
    			document.getElementById("status").innerHTML = "There is a possible CORS or access issue while attempting the request.";	
   		}   		
   	}
   	else {
   		document.getElementById("status").innerHTML = "Response is " + response.response + " with the error " 
		+ response.error + " and the status code " + response.statusCode;
   	}
 	}
```
	{: codeblock}


- Se l'`applicationId` non è configurato correttamente, la richiesta iniziale al servizio {{site.data.keyword.mobilepushshort}} avrà esito negativo, pertanto lo statusCode verrà impostato su zero (0).
- Il codice di stato 200 o 201 indica una risposta positiva.
- Nel caso in cui il `clientSecret` non sia valido, sullo statusCode verrà impostata una risposta 401. L'elemento `response.reponse` conterrà la descrizione dell'errore.


## Risoluzione dei messaggi di errore del servizio Push Notifications
{: #troubleshooting_service_errors}

I seguenti messaggi di errore di {{site.data.keyword.mobilepushshort}} vengono restituiti in risposta alle richieste della API REST.

Esempio di risposta di errore:
```
	{
		"message": "Missing APNs credentials",
     "docUrl": "https://www.ng.bluemix.net/docs/troubleshoot/errors/mobilepush/index.html#FPWSE0003E",
     "code":   "FPWSE0003E"
	}
```
		    {: codeblock}

Per ottenere ulteriori informazioni su un errore, cerca il relativo codice di errore nella documentazione.

### FPWSE0001E
{: #error_fpwse0001e}

**Spiegazione**: la  risorsa che stai tentando di sottoporre a query, come una tag o sottoscrizione, non è disponibile sul server.

**Risposta utente**: crea la risorsa indicata nel messaggio. In alternativa, fornisci l'identificativo corretto per eseguire la query della risorsa.


### FPWSE0002E
{: #error_fpwse0002e}

**Spiegazione**: la risorsa che stai tentando di creare è già disponibile sul server. La
        risorsa potrebbe essere una tag, una sottoscrizione e così via.

**Risposta utente**: crea la risorsa con un identificativo differente.


### FPWSE0003E
{: #error_fpwse0003e}

**Spiegazione**: la  configurazione dei prerequisiti per il servizio {{site.data.keyword.mobilepushshort}} non è completa. È possibile che tu stia tentando
        di richiamare le credenziali del servizio APNS (Apple Push Notification Service) prima della loro
        configurazione.

**Risposta utente**: assicurati che il servizio {{site.data.keyword.mobilepushshort}} sia stato configurato con certificati di sicurezza validi per APNs. Per ulteriori informazioni, vedi [Configurazione delle credenziali per un provider di notifica ![icona link esterno](../../icons/launch-glyph.svg "External link icon")](t__main_push_config_provider.html){: new_window}.


### FPWSE0004E
{: #error_fpwse0004e}

**Spiegazione**: il corpo JSON incluso nella richiesta non è valido.


**Risposta utente**: assicurati di utilizzare la sintassi JSON corretta nella richiesta.



### FPWSE0005E
{: #error_fpwse0005e}

**Spiegazione**: la richiesta al server {{site.data.keyword.mobilepushshort}} è errata o incompleta perché il corpo JSON non contiene i valori di proprietà necessari per completare la richiesta API. Ad esempio, una password non è valida o
        manca un token del dispositivo.


**Risposta utente**: esamina il messaggio per individuare quale valore di proprietà risulta non valido o mancante, quindi fornisci le informazioni richieste.



### FPWSE0006E
{: #error_fpwse0006e}

**Spiegazione**: il corpo JSON della richiesta contiene dei parametri non riconosciuti dal server {{site.data.keyword.mobilepushshort}}.


**Risposta utente**: verifica che il corpo JSON nella richiesta rispetti il formato della richiesta previsto dal server {{site.data.keyword.mobilepushshort}}. Per ulteriori informazioni, vedi [API REST![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://mobile.{DomainName}/imfpush/){: new_window}.



### FPWSE0007E 
{: #error_fpwse0007e}

**Spiegazione**: l'URL della richiesta ha una stringa di query con parametri non riconosciuti. Ad esempio, se la richiesta di eliminazione della sottoscrizione ha parametri diversi da deviceId e tagName, si potrebbe verificare questo errore.


**Risposta utente**: verifica che il corpo JSON nella richiesta rispetti il formato della richiesta previsto dal server {{site.data.keyword.mobilepushshort}}. Per ulteriori informazioni, vedi [API REST![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://mobile.{DomainName}/imfpush/){: new_window}.



### FPWSE0008E
{: #error_fpwse0008e}

**Spiegazione **: l'URL della richiesta ha una stringa di query in cui mancano dei parametri richiesti. Ad esempio, i parametri deviceId e tagName potrebbero non essere presenti nella richiesta di eliminazione della sottoscrizione.


**Risposta utente**: verifica che il corpo JSON nella richiesta rispetti il formato della richiesta previsto dal server {{site.data.keyword.mobilepushshort}}. Per ulteriori informazioni, vedi [API REST![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://mobile.{DomainName}/imfpush/){: new_window}.



### FPWSE0009E
{: #error_fpwse0009e}

**Spiegazione**: è stato effettuato un tentativo di inviare le notifiche ma non ci sono dispositivi registrati con l'applicazione.

**Risposta utente**: assicurati che i dispositivi siano stati registrati con l'applicazione prima di tentare l'invio delle notifiche.



### FPWSE0010E
{: #error_fpwse0010e}

**Spiegazione**: la richiesta inoltrata al server ha provocato una condizione di eccezione. L'errore potrebbe essere stato causato da una delle
seguenti condizioni:

- Un sottosistema interno utilizzato da {{site.data.keyword.mobilepushshort}} non
                    risponde.
- La richiesta ha provocato una condizione di errore che potrebbe non essere gestita da
 {{site.data.keyword.mobilepushshort}}.
- Il servizio {{site.data.keyword.mobilepushshort}}
                    richiede l'attenzione da parte dell'amministratore.

**Risposta utente**: ritenta la richiesta. Se il problema persiste, contatta il supporto software IBM.



### FPWSE0011E
{: #error_fpwse0011e}

**Spiegazione**: la sottoscrizione per la tag è già presente sul server. Questo errore si verifica, ad esempio, quando crei una
        sottoscrizione già esistente.

**Risposta utente**: crea la sottoscrizione con un nome tag univoco.



### FPWSE0012E
{: #error_fpwse0012e}

**Spiegazione**: la sottoscrizione per la tag non esiste sul server. Questo errore si verifica quando
        viene inoltrata una richiesta per richiamare o eliminare una sottoscrizione che non esiste.


**Risposta utente**: utilizza il nome tag e l'identificativo del dispositivo corretti nella richiesta.



### FPWSE0013E
{: #error_fpwse0013e}

**Spiegazione**: il payload JSON nella richiesta non è valido.


**Risposta utente**: assicurati che il payload JSON sia valido.


### FPWSE0025E
{: #error_fpwse0025e}

**Spiegazione**: il server non è attualmente in grado di gestire la richiesta.

**Risposta utente**: reinvia la richiesta in un secondo momento.


### FPWSE1007E 
{: #error_fpwse1007e}

**Spiegazione**: il servizio {{site.data.keyword.mobilepushshort}} è stato disabilitato per questa applicazione. Questo potrebbe essere dovuto a motivi di fatturazione o l'applicazione
potrebbe essere stata disabilitata dall'amministratore.


**Risposta utente**: consulta gli argomenti relativi alla Risoluzione dei problemi nella documentazione Bluemix per controllare lo stato del servizio, per esaminare le informazioni sulla risoluzione dei problemi o per informazioni sulla richiesta di assistenza.



### FPWSE1079E
{: #error_fpwse1079e}

**Spiegazione**: il valore di offset fornito per l'operazione di query non è valido.

**Risposta utente**: assicurati che il valore di offset sia superiore o uguale a zero.



### FPWSE1080E 
{: #error_fpwse1080e}

**Spiegazione**: il valore della dimensione fornito per l'operazione di query non è valido.

**Risposta utente**: assicurati che il valore della dimensione sia maggiore di zero.


