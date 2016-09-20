---

copyright:
 years: 2015, 2016

---

# Notifications interactives
{: #interactive-notifications}
Dernière mise à jour : 16 août 2016
{: .last-updated}

Les notifications interactives permettent aux utilisateurs de réagir sans avoir à ouvrir l'application lorsqu'ils reçoivent une notification. Lorsqu'une notification interactive est reçue, le périphérique affiche
les boutons d'action avec le message de notification. Les notifications interactives sont prises
en charge sur les périphériques iOS versions 8 et ultérieures. Si une notification interactive est envoyée à des périphériques iOS qui s'exécutent sur une version antérieure à la
version 8, les actions de notification ne sont pas affichées.

##Envoi de notifications interactives de type {{site.data.keyword.mobilepushshort}}


Une notification interactive peut être envoyée à l'aide du tableau de bord Push ou de l'API REST (voir la documentation API REST).

A partir de la console push : 



1. Sous l'onglet de notification du tableau de bord Push, cliquez sur la commande relative à l'envoi de la notification. 
2. Choisissez les destinataires de votre notification et cliquez sur **Suivant**. 
3. Dans la page de rédaction de la notification, une notification push interactive peut être envoyée en définissant Défaut ou Mixte comme type et en spécifiant la valeur Catégorie sous l'onglet Options avancées. Pour configurer la valeur de catégorie du client, lisez la section Traitement des notifications interactives de type {{site.data.keyword.mobilepushshort}} dans une application iOS native.

## Traitement des notifications interactives de type {{site.data.keyword.mobilepushshort}} dans une application iOS native

Procédez comme suit pour recevoir des notifications interactives :

1. Activez la fonction d'application pour effectuer des tâches en arrière-plan lors de la réception des notifications distantes. Cette étape est requise si certaines des actions sont activées en arrière-plan.
1. Dans la section AppDelegate (application: didRegisterForRemoteNotificationsWithDeviceTokenapplication:), définissez les catégories avant de définir `deviceToken` sur `WLPush Object`.

```
	if([application respondsToSelector:@selector(registerUserNotificationSettings:)]){
	 UIUserNotificationType userNotificationTypes = UIUserNotificationTypeNone | UIUserNotificationTypeSound | UIUserNotificationTypeAlert | UIUserNotificationTypeBadge;
	      
	 UIMutableUserNotificationAction *acceptAction = [[UIMutableUserNotificationAction alloc] init];
	 acceptAction.identifier = @"OK";
	 acceptAction.title = @"OK";
	      
	 UIMutableUserNotificationAction *rejetAction = [[UIMutableUserNotificationAction alloc] init];
	 rejetAction.identifier = @"NOK";
	 rejetAction.title = @"NOK";
	      
	 UIMutableUserNotificationCategory *cateogory = [[UIMutableUserNotificationCategory alloc] init];
	 cateogory.identifier = @"poll";
	 [cateogory setActions:@[acceptAction,rejetAction] forContext:UIUserNotificationActionContextDefault];
	 [cateogory setActions:@[acceptAction,rejetAction] forContext:UIUserNotificationActionContextMinimal];
	      
	 NSSet *catgories = [NSSet setWithObject:cateogory];
	 [application registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:userNotificationTypes categories:catgories]];
}
```

1. Implémentez une nouvelle méthode de rappel sur AppDelegate :

```
	-(void)application:(UIApplication *)application handleActionWithIdentifier:(NSString *)identifier forRemoteNotification:(NSDictionary *)userInfo completionHandler:(void (ˆ)())completionHandler
``` 

5. Cette nouvelle méthode de rappel est appelée lorsque l'utilisateur clique sur le bouton d'action. L'implémentation de cette méthode doit effectuer les tâches associées à l'identificateur spécifié et exécuter le bloc dans le paramètre `completionHandler`.
