---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

#Activation des notifications push avancées
Dernière mise à jour : 11 janvier 2017
{: .last-updated}

Configurez un badge iOS, un son, un contenu JSON supplémentaire, des notifications interactives et la conservation des notifications.

## Configuration d'un son, d'un contenu et d'un badge iOS
{: #badge-sound-payload}

Configurez un badge, un son et un contenu JSON supplémentaire iOS.

1. Dans le tableau de bord {{site.data.keyword.mobilepushshort}}, accédez à l'onglet **Notifications**.
2. Accédez à la section des zones facultatives pour configurer les fonctions {{site.data.keyword.mobilepushshort}}. 
	- **Fichier son** - Entrez une chaîne pour pointer vers le fichier son dans votre application mobile. Dans le contenu, spécifiez le nom de chaîne du fichier son à utiliser.
	- **Badge iOS** - Pour les appareils iOS, numéro à afficher comme badge de l'icône d'application. Si cette propriété manque, le badge n'est pas changé. Pour supprimer le badge, associez cette propriété à la valeur 0.
	
###Android

Ajoutez votre fichier son dans le répertoire `res/raw` de votre application Android. Lors de l'envoi de la notification, ajoutez le nom du fichier son dans la zone son de {{site.data.keyword.mobilepushshort}}.

```
"settings":{
     "gcm" : {
     "sound":"tt.wav",
	  }
 }  
```
    {: codeblock}	
	
###iOS

```
"settings": {
     "apns" : {
      "badge": 10,
	      "sound": "tt.wav",
	  }
}
``` 
	{: codeblock}
		
**Contenu supplémentaire** - Ce contenu peut être représenté par toute paire clé-valeur et doit être un objet JSON que vous voulez envoyer avec la notification de type {{site.data.keyword.mobilepushshort}}.

```
{"clé":"valeur", "clé2":"valeur2"}
```
	{: codeblock}

## Conservation des notifications Android 
{: #hold-notifications-android}

Quand votre application passe en arrière-plan, vous pouvez vouloir que le service {{site.data.keyword.mobilepushshort}} conserve les notifications qui sont envoyées à cette application. Pour conserver des notifications, appelez la méthode hold() dans la méthode onPause() de l'activité qui traite les
notifications de type {{site.data.keyword.mobilepushshort}}.

```
@Override
protected void onPause() {
    super.onPause();
    if (push != null) {
        push.hold();
    }
} 
```
	{: codeblock}
## Activations des notifications iOS interactives  
{: #enable-actionable-notifications-ios}

A la différence des notifications de type {{site.data.keyword.mobilepushshort}} traditionnelles, les notifications interactives invitent les utilisateurs à effectuer une sélection quand ils reçoivent l'alerte de notification sans ouvrir l'application. 

Procédez comme suit pour activer les notifications de type {{site.data.keyword.mobilepushshort}} dans votre application.

1. Créez une réponse utilisateur.
```
//For Swift
	let acceptAction = UIMutableUserNotificationAction()
	acceptAction.identifier = "ACCEPT_ACTION"
	acceptAction.title = "Accept"
	acceptAction.destructive = false
	acceptAction.authenticationRequired = false
	acceptAction.activationMode = UIUserNotificationActivationMode.Foreground
```
	{: codeblock}
```
//For Swift
	let declineAction = UIMutableUserNotificationAction()
	declineAction.identifier = "DECLINE_ACTION"
	declineAction.title = "Decline"
	declineAction.destructive = true
	declineAction.authenticationRequired = false
	declineAction.activationMode = UIUserNotificationActivationMode.Background
```
	{: codeblock}

2. Créez une catégorie de notification et définissez une action. **UIUserNotificationActionContextDefault** ou **UIUserNotificationActionContextMinimal** sont des contextes valides.
```
// For Swift
	let pushCategory = UIMutableUserNotificationCategory()
	pushCategory.identifier = "TODO_CATEGORY"
	pushCategory.setActions([acceptAction, declineAction], forContext: UIUserNotificationActionContext.Default)
```
	{: codeblock}

1. Créez le paramètre de notification et affectez les catégories de l'étape antérieure.
```
// For Swift
	let categories = NSSet(array:[pushCategory]);
```
	{: codeblock}

1. Créez la notification locale ou éloignée et affectez-lui l'identité de la catégorie.
```
//For Swift
	let settings = UIUserNotificationSettings(forTypes: [.Alert, .Badge, .Sound], categories: categories as? Set<UIUserNotificationCategory>)
    UIApplication.sharedApplication().registerUserNotificationSettings(settings)
    UIApplication.sharedApplication().registerForRemoteNotifications() 
```
	{: codeblock}
	
## Traitement des notifications iOS interactives  
{: #actionable-notifications}

Lors de la réception d'une notification interactive, le contrôle est transmis à la méthode suivante en fonction de l'identificateur choisi.

 
```
func application(application: UIApplication, handleActionWithIdentifier identifier: String?, forRemoteNotification userInfo: [NSObject : AnyObject], completionHandler: () -> Void) {
      //must call completion handler when finished
      completionHandler()
  }
```    
	{: codeblock}
    
