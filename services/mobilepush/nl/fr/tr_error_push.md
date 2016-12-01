---

copyright:
 years: 2015, 2016

---

# Message d'erreur de service {{site.data.keyword.mobilepushshort}}
{: #errors}
Dernière mise à jour : 25 octobre 2016
{: .last-updated}


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

## FPWSE0001E
{: #error_fpwse0001e}

###Explication

La ressource que vous essayez d'interroger, par exemple une étiquette
ou un abonnement, n'est pas disponible sur le serveur.

###Réponse de l'utilisateur

**Action :** Créez la ressource qui a été signalée dans le message. Vous pouvez également fournir l'identifiant correct pour interroger la ressource.


## FPWSE0002E
{: #error_fpwse0002e}

###Explication

La ressource que vous essayez de créer est déjà disponible sur le
serveur. Il peut s'agir d'une étiquette, d'un abonnement, etc.

###Réponse de l'utilisateur

**Action :** Créez la ressource avec un identifiant différent.


## FPWSE0003E
{: #error_fpwse0003e}

###Explication

La configuration requise pour le service {{site.data.keyword.mobilepushshort}} n'est pas terminée. Vous essayez peut-être d'obtenir les données d'identification du service
de notifications Push Apple (APNs) avant qu'elles ne soient configurées.

###Réponse de l'utilisateur

**Action :** Assurez-vous que le service {{site.data.keyword.mobilepushshort}}  a été configuré avec des certificats de sécurité valides pour les APN. Pour plus d'informations, voir [Configuration des données d'identification pour le service APNs](t_push_provider_ios.html){: new_window}.


## FPWSE0004E
{: #error_fpwse0004e}

###Explication

Le corps JSON inclus dans la demande n'est pas valide.


###Réponse de l'utilisateur

**Action :** Assurez-vous d'utiliser une syntaxe JSON valide dans la requête.



## FPWSE0005E
{: #error_fpwse0005e}

###Explication

The
request to the {{site.data.keyword.mobilepushshort}} server is incorrect or incomplete because the JSON body does not contain the property
        values that are needed to complete the API request. Par exemple, un mot de passe n'est pas valide ou un jeton d'appareil manque.


###Réponse de l'utilisateur

**Action :** Passez en revue le message pour savoir quelle valeur de propriété manque ou n'est pas valide et fournissez ensuite les informations requises.



## FPWSE0006E
{: #error_fpwse0006e}

###Explication

The JSON body of the request has parameters that are not understood by the {{site.data.keyword.mobilepushshort}} server.


###Réponse de l'utilisateur

**Action :** Vérifiez que le corps JSON dans la requête suit le format de la requête attendue par le serveur {{site.data.keyword.mobilepushshort}}. Pour plus d'informations, voir [API REST](https://mobile.{DomainName}/imfpush/).



## FPWSE0007E 
{: #error_fpwse0007e}

###Explication

L'adresse URL de la demande comporte une chaîne de requête qui inclut
des paramètres non reconnus. Par exemple, si la demande de suppression de l'abonnement comporte des paramètres autres que deviceId et tagName, cette erreur peut se produire.


###Réponse de l'utilisateur

**Action :** Vérifiez que le corps JSON dans la requête suit le format de la requête attendue par le serveur {{site.data.keyword.mobilepushshort}}. Pour plus d'informations, voir [API REST](https://mobile.{DomainName}/imfpush/).



## FPWSE0008E
{: #error_fpwse0008e}

###Explication

L'adresse URL de la demande comporte une chaîne de paramètres dans
laquelle il manque des paramètres requis. Par exemple, les paramètres deviceId et tagName peuvent être absents de la demande de suppression de l'abonnement.


###Réponse de l'utilisateur

**Action :** Vérifiez que le corps JSON dans la requête suit le format de la requête attendue par le serveur {{site.data.keyword.mobilepushshort}}. Pour plus d'informations, voir [API REST](https://mobile.{DomainName}/imfpush/).



## FPWSE0009E
{: #error_fpwse0009e}

###Explication

Une tentative d'envoi de notifications a été effectuée mais aucun
appareil n'est enregistré auprès de l'application.


###Réponse de l'utilisateur

**Action :** Assurez-vous que les appareils sont enregistrés auprès de l'application avant d'envoyer des notifications.



## FPWSE0010E
{: #error_fpwse0010e}

###Explication

La demande soumise au serveur a généré une condition d'exception. Il se peut que l'une des conditions suivantes soit à l'origine de l'erreur :

- Un sous-système interne utilisé par
{{site.data.keyword.mobilepushshort}} ne répond pas.
- La demande a généré une erreur qui ne peut pas être traitée par {{site.data.keyword.mobilepushshort}}.
- Le service {{site.data.keyword.mobilepushshort}} requiert l'attention d'un administrateur.


###Réponse de l'utilisateur

**Action :** Réessayez la demande. Si le problème persiste, contactez le service de support logiciel IBM.



## FPWSE0011E
{: #error_fpwse0011e}

###Explication

L'abonnement à l'étiquette existe déjà sur le serveur. C'est le cas, par
exemple, lorsque vous créez un abonnement qui existe déjà.


###Réponse de l'utilisateur

**Action :**  Créez l'abonnement avec un nom d'étiquette unique.



## FPWSE0012E
{: #error_fpwse0012e}

###Explication

L'abonnement à l'étiquette n'existe pas sur le serveur. Cette erreur
survient lorsqu'une demande d'extraction ou de suppression d'un abonnement qui n'existe pas est soumise.


###Réponse de l'utilisateur

**Action :** Utilisez le nom d'étiquette et l'identificateur d'appareil corrects dans la demande.



## FPWSE0013E
{: #error_fpwse0013e}

###Explication

Le contenu JSON de la demande n'est pas valide.


###Réponse de l'utilisateur

**Action :** Assurez-vous que la charge utile JSON est valide.



## FPWSE1007E 
{: #error_fpwse1007e}

###Explication

The {{site.data.keyword.mobilepushshort}} service has
        been disabled for this application. Cela
est peut-être dû à la facturation, ou l'application a peut-être été désactivée
par l'administrateur.


###Réponse de l'utilisateur

**Action :** Consultez les rubriques de Traitement des incidents la documentation Bluemix pour vérifier l'état du service, consulter les informations de traitement des problèmes ou pour obtenir des informations sur l'obtention d'aide.



## FPWSE1079E
{: #error_fpwse1079e}

###Explication

La valeur de décalage fournie pour l'opération de requête n'est pas
valide.

###Réponse de l'utilisateur

**Action :** Assurez-vous que la valeur de décalage est supérieure ou égale à zéro.



## FPWSE1080E 
{: #error_fpwse1080e}

###Explication

La valeur de taille fournie pour l'opération de requête n'est pas
valide.

###Réponse de l'utilisateur

**Action :** Assurez-vous que la valeur de la taille est supérieure à zéro.



