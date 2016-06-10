---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}


#Ativando notificações push avançadas

Configure um badge iOS, som, carga útil JSON adicional, notificações acionáveis e notificações de participação.

## Configure o som, a carga útil e o badge do iOS
{: #badge-sound-payload}

Configure um badge iOS, som e carga útil JSON adicional.

1. No painel Notificações push, vá para a guia
                        **Notificações**.
2. Vá para a seção **Campos opcionais**
para configurar os seguintes recursos de notificação push. 
	- **Arquivo de som** - insira uma sequência para apontar para o arquivo
de som em seu app móvel. Na carga útil, especifique o nome da sequência do
arquivo de som a ser usado.
	- **Badge iOS** - para dispositivos iOS, o
número a ser exibido como o badge do ícone do aplicativo. Se essa propriedade
estiver ausente, o badge não será mudado. Para remover o badge,
configure o valor dessa propriedade para 0.
	
	


###Android

```
"settings": {
     "gcm" : {
     "sound":"tt.wav",
	  }
 }  
```
	
	
###iOS

```
"settings": {
     "apns" : {
      "badge": 10,
	      "sound": "tt.wav",
	  }
}
``` 		
**Carga útil adicional** - essa carga útil pode ser qualquer
par de valores de chave e deve ser um objeto JSON que você queira enviar com a
notificação push.

```
{"key":"value", "key2":"value2"}
```


## Participação de notificações do Android 
{: #hold-notifications-android}

Quando seu aplicativo entrar no plano de fundo, você provavelmente desejará que Push
restrinja as notificações enviadas para ele. Para reter notificações, chame o método
hold() no método onPause() da atividade que está manipulando as notificações push.

```
@Override
protected void onPause() {
    super.onPause();

    if (push != null) {
        push.hold();
    }
} 
```

## Ativando notificações acionáveis de iOS  
{: #enable-actionable-notifications-ios}

Ao contrário das notificações push tradicionais, as notificações que permitem ações solicita que os usuários façam uma
seleção no recebimento do alerta de notificação sem abrir o app. Use as instruções
a seguir para ativar notificações push que permitem ações no aplicativo.

1. Crie uma ação de resposta do usuário.

   Objective-C

	```
	// For Objective-C
	UIMutableUserNotificationAction *acceptAction = [[UIMutableUserNotificationAction alloc] init];
	    acceptAction.identifier = @"ACCEPT_ACTION";
	    acceptAction.title = @"Accept";
	     /* Optional properties
	     acceptAction.destructive = NO;
	  acceptAction.authenticationRequired = NO; */
	  
	 ```
   Swift

	```
	//For Swift
	let acceptAction = UIMutableUserNotificationAction()
	acceptAction.identifier = "ACCEPT_ACTION"
	acceptAction.title = "Accept"
	acceptAction.destructive = false
	acceptAction.authenticationRequired = false
	acceptAction.activationMode = UIUserNotificationActivationMode.Foreground*/
	```
	
	```
	//For Swift
	let declineAction = UIMutableUserNotificationAction()
	declineAction.identifier = "DECLINE_ACTION"
	declineAction.title = "Decline"
	declineAction.destructive = true
	declineAction.authenticationRequired = false
	declineAction.activationMode = UIUserNotificationActivationMode.Background
	```

2. Crie a categoria de notificação e configure uma ação. **UIUserNotificationActionContextDefault** ou
                **UIUserNotificationActionContextMinimal** são contextos válidos.

	Objective-C

	```
	// For Objective-C
	UIMutableUserNotificationCategory *callCat = [[UIMutableUserNotificationCategory alloc] init];
	    callCat.identifier = @"POLL_CATEGORY";
	    [callCat setActions:@[acceptAction, declineAction] forContext:UIUserNotificationActionContextDefault];
	```    

	Swift

	```
	// For Swift
	let pushCategory = UIMutableUserNotificationCategory()
	pushCategory.identifier = "TODO_CATEGORY"
	pushCategory.setActions([acceptAction, declineAction], forContext: UIUserNotificationActionContext.Default)
	```

1. Crie a configuração de notificação e designe as categorias da etapa
anterior.

	Objective-C

	```
	// For Objective-C
	NSSet *categories = [NSSet setWithObjects:callCat, nil];
	```

	Swift

	```
	// For Swift
	let categories = NSSet(array:[pushCategory]);
	```

1. Crie a notificação local ou remota e designe a ela a identidade da
categoria.

	Objective-C

	```
	//For Objective-C

	[[UIApplication sharedApplication] registerUserNotificationSettings:[UIUserNotificationSettings settingsForTypes:(UIUserNotificationTypeSound | UIUserNotificationTypeAlert | UIUserNotificationTypeBadge) categories:categories]];

	[[UIApplication sharedApplication] registerForRemoteNotifications];
	```

	Swift

	```
	//For Swift
	let notificationTypes: UIUserNotificationType = UIUserNotificationType.Badge | UIUserNotificationType.Alert | UIUserNotificationType.Sound
	let notificationSettings: UIUserNotificationSettings = UIUserNotificationSettings(forTypes: notificationTypes, categories: categories)

	application.registerUserNotificationSettings(notificationSettings)
	application.registerForRemoteNotifications()
	```
	
## Manipulando notificações de iOS acionáveis  
{: #actionable-notifications}

Quando uma notificação que permite ação é recebida, o controle é passado para o
método a seguir com base no identificador escolhido.

###Objective-C

```
(void)application:(UIApplication *)application handleActionWithIdentifier:(NSString *)identifier forRemoteNotification:
(UILocalNotification *)notification completionHandler:(void (^)())completionHandler
{
  NSLog(@"actionable notification received.");
  //must call completion handler when finished
  completionHandler();
}
```

###Swift
 
```
func application(application: UIApplication, handleActionWithIdentifier identifier: String?, forRemoteNotification userInfo: [NSObject : AnyObject], completionHandler: () -> Void) {
      //must call completion handler when finished
      completionHandler()
  }
```    
    
