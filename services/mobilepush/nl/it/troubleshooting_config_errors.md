---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Risoluzione degli errori di configurazione push web
{: #errors}
Ultimo aggiornamento: 11 gennaio 2017
{: .last-updated}

Utilizza questa sezione come una guida per risolvere gli errori comuni relativi alla configurazione del push web. Gli errori push web dal `BMSPushSDK.js` contengono informazioni sull'errore. 

Per analizzare un errore restituiti nel callback, considera il seguente codice di esempio:

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
