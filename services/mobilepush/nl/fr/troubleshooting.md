---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Traitement des incidents
{: #errors}
Dernière mise à jour : 12 avril 2017
{: .last-updated}

Cette rubrique vous aide à identifier et à résoudre les scénarios d'erreur que vous pouvez rencontrer lors de l'utilisation du service Push Notifications.

## Résolution des incidents courants liés aux notifications push
{: #troubleshooting_notification_errors}

### Une erreur serveur interne s'est produite. Veuillez contacter l'administrateur. (Code d'erreur interne : PUSHD102E)
{: #troubleshooting_notification_internal}

**Explication** : Cette erreur peut se produire si vous avez créé une instance push avant le mois de novembre 2015.  

**Réponse de l'utilisateur **: pour résoudre ce problème, supprimez l'instance push et créez-en une nouvelle. Notez que lorsque vous supprimez l'instance push, vos balises ne sont pas conservées.


### UnauthorizedRegistration
{: #troubleshooting_notification_unauth}

**Explication** : Chrome Web Push ne fonctionne pas avec les clés de Firebase Cloud Messaging (FCM). Si vous ne parvenez pas à recevoir des notifications push Web sur Chrome après avoir migré vers FCM à partir de GCM, c'est parce que le site Web a été configuré pour fonctionner avec le projet GCM et que le nouveau projet est créé dans FCM. Les jetons générés qui identifient le navigateur sont mis en cache par le navigateur Chrome.

**Réponse de l'utilisateur **: vous pouvez résoudre ce problème en supprimant les cookies et en redéfinissant les autorisations du
navigateur. Cela demanderait des autorisations pour activer les notifications Push. 


### Les agents de service ne sont pas pris en charge dans ce navigateur
{: #troubleshooting_notification_service_workers}

**Explication **: Le SDK inclus avec `BMSPushSDK.js` et utilisant l'agent de service n'est pas disponible. 

**Réponse utilisateur **: Il est recommandé d'adopter un navigateur prenant en charge l'agent de service. Les versions de navigateur prises en
charge sont Firefox version 49 (ou ultérieure) et Chrome (64 bits) version 53 (ou ultérieure).


### SecurityError : L'opération n'est pas sécurisée
{: #troubleshooting_notification_insecure}

**Explication ** : Vous pourriez rencontrer cette erreur lors de l'activation de la console Web dans
Firefox. La prise en charge de notifications Web push dans le service Push Notification requiert d'accéder au site Web avec le protocole
`https` et non pas `http`.

**Réponse utilisateur **: Il est recommandé d'essayer de vous connecter au site Web sous
`https` depuis le navigateur.


## Résolution des erreurs de configuration push Web
{: #troubleshooting_configuration_errors}

Vous pouvez diagnostiquer les erreurs relatives à la configuration push Web en parcourant le fichier `BMSPushSDK.js`. Ce fichier comporte des informations sur l'échec. 

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


## Résolution des messages d'erreur du service Push Notifications
{: #troubleshooting_service_errors}

Les messages d'erreur {{site.data.keyword.mobilepushshort}} suivants sont
renvoyés en réponse aux demandes d'API REST.

Exemple de réponse contenant une erreur :
```
	{
		"message": "Missing APNs credentials",
     "docUrl": "https://www.ng.bluemix.net/docs/troubleshoot/errors/mobilepush/index.html#FPWSE0003E",
     "code":   "FPWSE0003E"
	}
```
		    {: codeblock}

Pour obtenir des informations supplémentaires sur une erreur, recherchez les documents pour le code d'erreur associé.

### FPWSE0001E
{: #error_fpwse0001e}

**Explication **: la ressource que vous tentez d'interroger, par exemple une balise ou un abonnement,
n'est pas disponible sur le serveur.

**Réponse de l'utilisateur **: créez la ressource signalée dans le message. Vous pouvez également fournir l'identifiant correct pour interroger la ressource.


### FPWSE0002E
{: #error_fpwse0002e}

**Explication **: la ressource que vous tentez de créer est déjà disponible sur le serveur. Il peut s'agir d'une étiquette, d'un abonnement, etc.

**Réponse de l'utilisateur **: créez la ressource avec un identificateur différent.


### FPWSE0003E
{: #error_fpwse0003e}

**Explication **: la configuration requise pour le service {{site.data.keyword.mobilepushshort}} est incomplète. Vous essayez peut-être d'obtenir les données d'identification du service
de notifications Push Apple (APNS) avant qu'elles ne soient configurées.

**Réponse de l'utilisateur **: vérifiez que le service {{site.data.keyword.mobilepushshort}} a été configuré avec des certificats de sécurité valides pour les APN. Pour plus d'informations, voir [Configuration des données d'identification pour un fournisseur de notification![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](t__main_push_config_provider.html){: new_window}.


### FPWSE0004E
{: #error_fpwse0004e}

**Explication **: le corps JSON inclus dans la demande n'est pas valide.


**Réponse de l'utilisateur **: veillez à utiliser une syntaxe valide dans la demande.



### FPWSE0005E
{: #error_fpwse0005e}

**Explication **: la demande adressée au serveur {{site.data.keyword.mobilepushshort}} est incorrecte ou incomplète étant donné que le corps JSON ne contient pas les valeurs de propriété nécessaires pour remplir la demande d'API. Par exemple, un mot de passe n'est pas valide ou un jeton d'appareil manque.


**Réponse de l'utilisateur **: examinez le message pour déterminer quelle valeur de propriété est manquante ou non valide et soumettez les informations requises.



### FPWSE0006E
{: #error_fpwse0006e}

**Explication **: le corps JSON de la demande comporte des paramètres que ne comprend pas le serveur {{site.data.keyword.mobilepushshort}}.


**Réponse de l'utilisateur **: vérifiez que le corps JSON dans la demande respecte le format de demande attendu par le serveur {{site.data.keyword.mobilepushshort}}. Pour plus d'informations, voir [API REST ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://mobile.{DomainName}/imfpush/){: new_window}.



### FPWSE0007E 
{: #error_fpwse0007e}

**Explication **: l'URL de la demande comporte une chaîne de requête avec des paramètres non reconnus. Par exemple, si la demande de suppression de l'abonnement comporte des paramètres autres que deviceId et tagName, cette erreur peut se produire.


**Réponse de l'utilisateur **: vérifiez que le corps JSON dans la demande respecte le format de demande attendu par le serveur {{site.data.keyword.mobilepushshort}}. Pour plus d'informations, voir [API REST ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://mobile.{DomainName}/imfpush/){: new_window}.



### FPWSE0008E
{: #error_fpwse0008e}

**Explication **: l'URL de la demande comporte une chaîne de requête avec des paramètres requis manquants. Par exemple, les paramètres deviceId et tagName peuvent être absents de la demande de suppression de l'abonnement.


**Réponse de l'utilisateur **: vérifiez que le corps JSON dans la demande respecte le format de demande attendu par le serveur {{site.data.keyword.mobilepushshort}}. Pour plus d'informations, voir [API REST ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://mobile.{DomainName}/imfpush/){: new_window}.



### FPWSE0009E
{: #error_fpwse0009e}

**Explication **: une tentative d'envoi de notifications a été effectuée mais aucun appareil n'est enregistré auprès de l'application.

**Réponse de l'utilisateur **: vérifiez que des appareils ont été enregistrés auprès de l'application avant de tenter d'envoyer des notifications.



### FPWSE0010E
{: #error_fpwse0010e}

**Explication **: la demande soumise au serveur a généré une situation d'exception. Il se peut que l'une des conditions suivantes soit à l'origine de l'erreur :

- Un sous-système interne utilisé par
{{site.data.keyword.mobilepushshort}} ne répond pas.
- La demande a généré une erreur qui ne peut pas être traitée par {{site.data.keyword.mobilepushshort}}.
- Le service {{site.data.keyword.mobilepushshort}} requiert l'attention d'un administrateur.

**Réponse de l'utilisateur **: relancez la demande. Si le problème persiste, contactez le service de support logiciel IBM.



### FPWSE0011E
{: #error_fpwse0011e}

**Explication **: l'abonnement à la balise existe déjà sur le serveur. C'est le cas, par
exemple, lorsque vous créez un abonnement qui existe déjà.

**Réponse de l'utilisateur **: créez l'abonnement avec un nom de balise unique.



### FPWSE0012E
{: #error_fpwse0012e}

**Explication **: l'abonnement à la balise n'existe pas sur le serveur. Cette erreur
survient lorsqu'une demande d'extraction ou de suppression d'un abonnement qui n'existe pas est soumise.


**Réponse de l'utilisateur **: utilisez le nom d'étiquette et l'identificateur d'appareil corrects dans la demande.



### FPWSE0013E
{: #error_fpwse0013e}

**Explication **: le contenu JSON dans la demande n'est pas valide.


**Réponse de l'utilisateur **: vérifiez que le contenu JSON est valide.


### FPWSE0025E
{: #error_fpwse0025e}

**Explication** : Le serveur est actuellement incapable de traiter la demande.

**Réponse de l'utilisateur** : Soumettez à nouveau la demande plus tard.


### FPWSE1007E 
{: #error_fpwse1007e}

**Explication **: le service {{site.data.keyword.mobilepushshort}} a été désactivé pour cette application. Cela
est peut-être dû à la facturation, ou l'application a peut-être été désactivée
par l'administrateur.


**Réponse de l'utilisateur **: accédez aux rubriques de Traitement des incidents dans la documentation
Bluemix pour vérifier le statut du service, consultez les informations de traitement des incidents ou les informations sur l'obtention
d'une assistance.



### FPWSE1079E
{: #error_fpwse1079e}

**Explication **: la valeur de décalage soumise pour l'opération de requête n'est pas valide.

**Réponse de l'utilisateur **: vérifiez que la valeur de décalage est supérieure ou égale à zéro.



### FPWSE1080E 
{: #error_fpwse1080e}

**Explication **: la valeur de taille soumise pour l'opération de requête n'est pas valide.

**Réponse de l'utilisateur **: vérifiez que la valeur de taille est supérieure à zéro.


