ka---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Notifications interactives
{: #interactive-notifications}
Dernière mise à jour : 18 janvier 2017
{: .last-updated}

Les notifications interactives permettent aux utilisateurs de répondre à une notification sans ouvrir l'application. Lorsqu'une notification interactive est reçue, l'appareil affiche
les boutons d'action avec le message de notification. Les notifications sont prises en charge sur les unités iOS avec version 8 ou ultérieure. Dans le cas de
notifications interactives envoyés à des unités iOS antérieures à la version 8, les actions de notification ne sont pas affichées.

##Envoi de notifications interactives de type {{site.data.keyword.mobilepushshort}}


Une notification interactive peut être envoyée en utilisant le tableau de bord Push ou la [documentation de l'API REST](t_restapi.html).

Depuis la console {{site.data.keyword.mobilepushshort}} : 

1. Sous l'onglet de notification du tableau de bord Push, cliquez sur la commande relative à l'envoi de la notification. 
2. Choisissez les destinataires de votre notification et cliquez sur **Suivant**. 
3. Dans la page de rédaction de la notification, une notification push interactive peut être envoyée en définissant Défaut ou Mixte comme type et en spécifiant la valeur Catégorie sous l'onglet Options avancées. Pour configurer la valeur de catégorie du client, lisez la section Traitement des notifications interactives de type {{site.data.keyword.mobilepushshort}} dans une application iOS native.

## Traitement des notifications interactives de type {{site.data.keyword.mobilepushshort}} dans une application iOS native


### Swift

Procédez comme suit pour recevoir des notifications interactives :

1. Activez la fonction d'application pour effectuer des tâches en arrière-plan lors de la réception des notifications distantes. 
1. Initialisez le SDK `BMSPush` avec votre catégorie d'action.
	```
	let myBMSClient = BMSClient.sharedInstance
	myBMSClient.initialize(bluemixRegion: BMSClient.Region.usSouth)
	let push =  BMSPushClient.sharedInstance
    let actionOne = BMSPushNotificationAction(identifierName: "FIRST", buttonTitle: "Accept", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
   	let actionTwo = BMSPushNotificationAction(identifierName: "SECOND", buttonTitle: "Reject", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
   	let category = BMSPushNotificationActionCategory(identifierName: "category", buttonActions: [actionOne, actionTwo])
   	let notifOptions = BMSPushClientOptions(categoryName: [category])
	push.initializeWithAppGUID(appGUID: "YOUR_APP_GUID", clientSecret:"YOUR_APP_CLIENT_SECRET", options: notifOptions)
	```
		{: codeblock}

1. Implémentez la nouvelle méthode de rappel sur AppDelegate :
	```
	 func userNotificationCenter(_ center: UNUserNotificationCenter,
       didReceive response: UNNotificationResponse,
       withCompletionHandler completionHandler: @escaping () -> Void) {
            switch response.actionIdentifier {
		    case "FIRST":
		      print("FIRST")
		    case "SECOND":
		      print("SECOND")  
		    default:
		      print("Unknown action")
		    }
		completionHandler
	}
	```
	{: codeblock} 
5. Cette nouvelle méthode de rappel est appelée lorsque l'utilisateur clique sur le bouton d'action. L'implémentation de cette méthode doit effectuer les tâches associées à l'identificateur spécifié et exécuter le bloc dans le paramètre `completionHandler`.


### Cordova

Pour obtenir une notification interactive dans une application Cordova sous iOS, procédez comme suit :

1. Ajoutez une zone de catégorie dans la méthode `BMSPush.initialize`.
   ```
	var category =  {"Category_Name":[{"IdentifierName_1":"actionName_1"},{"IdentifierName_2":"actionName_2"}]}
       BMSPush.initialize(appGUID,clientSecret,category);
    ```
	{: codeblock} 
2. Implémentez la nouvelle méthode de rappel sur AppDelegate.
3. Cette nouvelle méthode de rappel est appelée lorsque l'utilisateur clique sur le bouton d'action. L'implémentation de cette méthode
doit effectuer les tâches associées à l'identificateur spécifié et exécuter le bloc stipulé par le paramètre
completionHandler.
