---

copyright:
 years: 2015, 2016

---

# Interaktive Benachrichtigungen
{: #interactive-notifications}
Letzte Aktualisierung: 16. August 2016
{: .last-updated}

Interaktive Benachrichtigungen ermöglichen es Benutzern, beim Eingang einer Benachrichtigung zu reagieren, ohne dass die Anwendung geöffnet werden muss. Wenn eine interaktive Benachrichtigung eingeht, zeigt das Gerät die Aktionsschaltflächen zusammen mit der Benachrichtigung an. Interaktive Benachrichtigungen werden für iOS-Geräte mit Version 8 oder einer neueren Version unterstützt. Wenn eine interaktive Benachrichtigung an iOS-Geräte gesendet wird, die mit einer älteren Version als Version 8 ausgeführt werden, werden die Benachrichtigungsaktionen nicht angezeigt.

##Interaktive Push-Benachrichtigungen senden


Interaktive Benachrichtigungen können über das Push-Dashboard oder mithilfe der REST-API (siehe REST-API-Dokumentation) gesendet werden.

Über die Push-Konsole: 



1. Klicken Sie auf der Registerkarte 'Benachrichtigungen' im Push-Dashboard auf **Benachrichtigung senden**.  
2. Wählen Sie die Benachrichtigungsempfänger aus und klicken Sie auf **Weiter**.  
3. Auf der Seite für die Benachrichtigungserstellung können Sie beim Senden von interaktiven Push-Benachrichtigungen den Typ 'Standard' oder 'Gemischt' festlegen und auf der Registerkarte mit den erweiterten Optionen den Kategoriewert angeben. Informationen zum Konfigurieren des Kategoriewerts auf dem Client finden Sie im Abschnitt zur Verarbeitung interaktiver Push-Benachrichtigungen in nativen iOS-Anwendungen. 

## Interaktive Push-Benachrichtigungen in einer iOS-Anwendung verarbeiten 

Führen Sie die folgenden Schritte aus, um interaktive Benachrichtigungen zu erhalten: 

1. Aktivieren Sie die Anwendungsfunktion zum Durchführen von Hintergrundtasks beim Empfang der fernen Benachrichtigungen. Dieser Schritt ist erforderlich, wenn einige der Aktionen für die Hintergrundverarbeitung aktiviert sind.
1. Legen Sie in 'AppDelegate' (application: didRegisterForRemoteNotificationsWithDeviceTokenapplication:) die Kategorien fest, bevor Sie `deviceToken` für `WLPush Object` festlegen. 

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

1. Implementieren Sie die neue Callback-Methode in AppDelegate:

```
	-(void)application:(UIApplication *)application handleActionWithIdentifier:(NSString *)identifier forRemoteNotification:(NSDictionary *)userInfo completionHandler:(void (ˆ)())completionHandler
``` 

5. Diese neue Callback-Methode wird aufgerufen, wenn der Benutzer auf die Aktionsschaltfläche klickt. Die Implementierung dieser Methode muss die Aufgaben durchführen, die der angegebenen ID zugeordnet sind, und den Block im Parameter `completionHandler` ausführen.
