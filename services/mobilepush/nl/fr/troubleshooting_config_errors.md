---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Résolution des erreurs de configuration push Web
{: #errors}
Dernière mise à jour : 11 janvier 2017
{: .last-updated}

Utilisez cette section comme guide pour résoudre des erreurs de configuration courantes associées aux notifications push Web. Les erreurs Web push de
`BMSPushSDK.js` contiennent des informations sur l'échec. 

Examinez l'exemple de code suivant pour analyser une erreur renvoyée dans le rappel :

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


- Si l'ID d'application (`applicationId`) est configuré incorrectement, la demande initiale au service
{{site.data.keyword.mobilepushshort}} échouera et donc son code de statut (statusCode) recevra la valeur zéro (0).
- Un code de statut 200 ou 201 dénote une réponse réussie.
- Si la valeur confidentielle (`clientSecret`) n'est pas valide, une réponse 401 est affectée à statusCode. L'élément
`response.reponse` contiendra une description de l'erreur.
