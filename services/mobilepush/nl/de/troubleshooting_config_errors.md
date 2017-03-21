---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Fehler in der Web-Push-Konfiguration beheben
{: #errors}
Letzte Aktualisierung: 11. Januar 2017
{: .last-updated}

In diesem Abschnitt finden Sie Anweisungen für die Behebung von allgemeinen Fehlern in der Web-Push-Konfiguration. Web-Push-Fehler aus der Datei `BMSPushSDK.js` enthalten Informationen zu dem Fehler. 

Das folgende Codebeispiel veranschaulicht das Analysieren eines Fehlers im Callback:

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


- Wenn `applicationId` nicht ordnungsgemäß konfiguriert ist, schlägt die ursprüngliche Anforderung an den {{site.data.keyword.mobilepushshort}}-Service fehl, da 'statusCode' auf Null (0) gesetzt wird.
- Der Statuscode 200 oder 201 bezeichnet eine erfolgreiche Antwort.
- Wenn `clientSecret` ungültig ist, wird für 'statusCode' ein Antwortcode 401 festgelegt. Das Element `response.reponse` enthält eine Beschreibung des Fehlers.
