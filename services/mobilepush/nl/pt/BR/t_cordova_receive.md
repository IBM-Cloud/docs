---

copyright:
 years: 2015, 2016

---

# Recebendo notificações push em dispositivos
{: #cordova_receive}

Copie e cole os fragmentos de código a seguir para receber
notificações push em dispositivos.

##JavaScript

Inclua o seguinte fragmento de código JavaScript
na web part do seu aplicativo Cordova.


```
var notification = function(notification){
    // notification is a JSON object.
    alert(notification.message);
};
MFPPush.registerNotificationsCallback(notification);
```

##Propriedades de notificação do Android

A seção a seguir lista as propriedades de notificação de Android:

* message - mensagem de notificação push
* payload - objeto JSON contendo uma carga útil de notificação


##Propriedades de notificação do iOS

A seguinte seção lista as propriedades de notificação iOS:

* message - mensagem de notificação push
* payload - objeto JSON que contém uma carga útil de notificação
action-loc-key - A sequência é usada como chave para obter uma sequência localizada na
localização atual a ser usada para o título do botão direito, em vez de “Visualizar".
* badge - O número a ser exeibido como o badge do ícone de app. Se essa propriedade
estiver ausente, o badge não será mudado. Para remover o badge,
configure o valor dessa propriedade para 0.
* sound - O nome de um arquivo de som no pacote configurável de app
ou na pasta Biblioteca/sons do contêiner de dados de app.

##Objective-C

Inclua os fragmentos de código Objective-C a seguir em sua classe de delegação de
aplicativo.

```
// Handle receiving a remote notification
-(void)application:(UIApplication *)application
didReceiveRemoteNotification:(NSDictionary *)userInfo
fetchCompletionHandler:(void
(^)(UIBackgroundFetchResult))completionHandler {

 [[CDVMFPPush sharedInstance] didReceiveRemoteNotification:userInfo];
}
```

```
// Handle receiving a remote notification on launch
- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions

    [[CDVMFPPush sharedInstance] didReceiveRemoteNotificationOnLaunch:launchOptions];
}
```

##Swift

Inclua os fragmentos de código Swift a seguir em sua classe de delegação de
aplicativo.

```
// Handle receiving a remote notification
funcapplication(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: ){

    CDVMFPPush.sharedInstance().didReceiveRemoteNotification(userInfo)
}
```

```
// Handle receiving a remote notification on launch
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {

    CDVMFPPush.sharedInstance().didReceiveRemoteNotificationOnLaunch(launchOptions)
}

```
Próxima Etapa. [Enviar notificações push básicas](t_send_push_notifications.html).
