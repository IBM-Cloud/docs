---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Messaggi di errore del servizio {{site.data.keyword.mobilepushshort}}
{: #errors}
Ultimo aggiornamento: 13 febbraio 2017
{: .last-updated}


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

## FPWSE0001E
{: #error_fpwse0001e}

**Spiegazione**: la  risorsa che stai tentando di sottoporre a query, come una tag o sottoscrizione, non è disponibile sul server.

**Risposta utente**: crea la risorsa indicata nel messaggio. In alternativa, fornisci l'identificativo corretto per eseguire la query della risorsa.


## FPWSE0002E
{: #error_fpwse0002e}

**Spiegazione**: la risorsa che stai tentando di creare è già disponibile sul server. La
        risorsa potrebbe essere una tag, una sottoscrizione e così via.

**Risposta utente**: crea la risorsa con un identificativo differente.


## FPWSE0003E
{: #error_fpwse0003e}

**Spiegazione**: la  configurazione dei prerequisiti per il servizio {{site.data.keyword.mobilepushshort}} non è completa. È possibile che tu stia tentando
        di richiamare le credenziali del servizio APNS (Apple Push Notification Service) prima della loro
        configurazione.

**Risposta utente**: assicurati che il servizio {{site.data.keyword.mobilepushshort}} sia stato configurato con certificati di sicurezza validi per APNs. Per ulteriori informazioni, vedi [Configurazione delle credenziali per APNs ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](t_push_provider_ios.html){: new_window}.


## FPWSE0004E
{: #error_fpwse0004e}

**Spiegazione**: il corpo JSON incluso nella richiesta non è valido.


**Risposta utente**: assicurati di utilizzare la sintassi JSON corretta nella richiesta.



## FPWSE0005E
{: #error_fpwse0005e}

**Spiegazione**: la richiesta al server {{site.data.keyword.mobilepushshort}} è errata o incompleta perché il corpo JSON non contiene i valori di proprietà necessari per completare la richiesta API. Ad esempio, una password non è valida o
        manca un token del dispositivo.


**Risposta utente**: esamina il messaggio per individuare quale valore di proprietà risulta non valido o mancante, quindi fornisci le informazioni richieste.



## FPWSE0006E
{: #error_fpwse0006e}

**Spiegazione**: il corpo JSON della richiesta contiene dei parametri non riconosciuti dal server {{site.data.keyword.mobilepushshort}}.


**Risposta utente**: verifica che il corpo JSON nella richiesta rispetti il formato della richiesta previsto dal server {{site.data.keyword.mobilepushshort}}. Per ulteriori informazioni, vedi [API REST![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://mobile.{DomainName}/imfpush/){: new_window}.



## FPWSE0007E 
{: #error_fpwse0007e}

**Spiegazione**: l'URL della richiesta ha una stringa di query con parametri non riconosciuti. Ad esempio, se la richiesta di eliminazione della sottoscrizione ha parametri diversi da deviceId e tagName, si potrebbe verificare questo errore.


**Risposta utente**: verifica che il corpo JSON nella richiesta rispetti il formato della richiesta previsto dal server {{site.data.keyword.mobilepushshort}}. Per ulteriori informazioni, vedi [API REST![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://mobile.{DomainName}/imfpush/){: new_window}.



## FPWSE0008E
{: #error_fpwse0008e}

**Spiegazione **: l'URL della richiesta ha una stringa di query in cui mancano dei parametri richiesti. Ad esempio, i parametri deviceId e tagName potrebbero non essere presenti nella richiesta di eliminazione della sottoscrizione.


**Risposta utente**: verifica che il corpo JSON nella richiesta rispetti il formato della richiesta previsto dal server {{site.data.keyword.mobilepushshort}}. Per ulteriori informazioni, vedi [API REST![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://mobile.{DomainName}/imfpush/){: new_window}.



## FPWSE0009E
{: #error_fpwse0009e}

**Spiegazione**: è stato effettuato un tentativo di inviare le notifiche ma non ci sono dispositivi registrati con l'applicazione.

**Risposta utente**: assicurati che i dispositivi siano stati registrati con l'applicazione prima di tentare l'invio delle notifiche.



## FPWSE0010E
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



## FPWSE0011E
{: #error_fpwse0011e}

**Spiegazione**: la sottoscrizione per la tag è già presente sul server. Questo errore si verifica, ad esempio, quando crei una
        sottoscrizione già esistente.

**Risposta utente**: crea la sottoscrizione con un nome tag univoco.



## FPWSE0012E
{: #error_fpwse0012e}

**Spiegazione**: la sottoscrizione per la tag non esiste sul server. Questo errore si verifica quando
        viene inoltrata una richiesta per richiamare o eliminare una sottoscrizione che non esiste.


**Risposta utente**: utilizza il nome tag e l'identificativo del dispositivo corretti nella richiesta.



## FPWSE0013E
{: #error_fpwse0013e}

**Spiegazione**: il payload JSON nella richiesta non è valido.


**Risposta utente**: assicurati che il payload JSON sia valido.


## FPWSE0025E
{: #error_fpwse0025e}

**Spiegazione**: il server non è attualmente in grado di gestire la richiesta.

**Risposta utente**: reinvia la richiesta in un secondo momento.


## FPWSE1007E 
{: #error_fpwse1007e}

**Spiegazione**: il servizio {{site.data.keyword.mobilepushshort}} è stato disabilitato per questa applicazione. Questo potrebbe essere dovuto a motivi di fatturazione o l'applicazione
potrebbe essere stata disabilitata dall'amministratore.


**Risposta utente**: consulta gli argomenti relativi alla Risoluzione dei problemi nella documentazione Bluemix per controllare lo stato del servizio, per esaminare le informazioni sulla risoluzione dei problemi o per informazioni sulla richiesta di assistenza.



## FPWSE1079E
{: #error_fpwse1079e}

**Spiegazione**: il valore di offset fornito per l'operazione di query non è valido.

**Risposta utente**: assicurati che il valore di offset sia superiore o uguale a zero.



## FPWSE1080E 
{: #error_fpwse1080e}

**Spiegazione**: il valore della dimensione fornito per l'operazione di query non è valido.

**Risposta utente**: assicurati che il valore della dimensione sia maggiore di zero.



