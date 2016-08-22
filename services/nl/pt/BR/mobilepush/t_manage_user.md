---

copyright:
 years: 2015, 2016

---


# Registrar dispositivo com UserId
{: #register_device_with_userId}
*Última atualização: 20 de julho de 2016*
{: .last-updated}

Para registrar para notificação baseada em ID do usuário, conclua as etapas a seguir:

## Android
 
Inicialize a classe IMFPush com as chaves `pushTenantId` e `clientSecret` do serviço de Notificação push.

```
// Initialize the MFPPush push = MFPPush.getInstance();
push.initializeBluemixPushWithClientSecret(getApplicationContext(),"clientSecret");
```

**clientSecret** 

Esta é a chave clientSecret do serviço de Notificações push.


Use a API **registerWithUserId** para registrar o dispositivo para notificações push.

```
// Register the device to push notifications service.
push.registerWithUserId("userId",new MFPPushResponseListener<String>() {
    @Override
	    public void onSuccess(String deviceId) {
        updateTextView("Device is registered with Push Service.");
        displayTags();
    }

    @Override
    public void onFailure(MFPPushException ex) {
        updateTextView("Error registering with Push Service...\n"
        + "Push notifications will not be received.");
    }
});
```

**userId** 

Passe o valor do ID do usuário exclusivo para registrar para notificações push.

>**Nota:** para ativar notificações push visadas pelo UserId, assegure-se de registrar o dispositivo com um UserId e também
passe o 'clientSecret' alocado quando os serviços de Notificação push são provisionados. Se você não passar um clientSecret válido, o registro de
dispositivo falhará.
## Cordova

Copie o fragmento de código a seguir em seu aplicativo móvel para registrar para notificações baseadas em ID do usuário.

Inicialize `MFPPush` com `clientsecret`. 

```
MFPPush.initializeBluemixPushWithClientSecret("clientSecret");
```

**clientSecret** 

Esta é a chave clientSecret do serviço de Notificações push.

```
//Register for Push notification with userId var userId = "userId";
MFPPush.registerWithUserId(userId,success,failure);
```
**userId** 

Passe o valor do ID do usuário exclusivo para registrar para serviço de Notificação push.


## Objective-C


Use as APIs a seguir para registrar para notificações push baseadas em ID do usuário.


```
// Initialize the MFPPush IMFPushClient* push = [IMFPushClient
sharedInstance]; [push
initializeBluemixPushWithClientSecret:@"clientSecret"];
```

**clientSecret** 

Esta é a chave clientSecret do serviço de Notificações push.


Use a API **registerWithUserId** para registrar o dispositivo para notificações push.


```
// Register the device to push notifications service.
[push registerDeviceToken:deviceToken WithUserId:@"userId" completionHandler:^(IMFResponse *response, NSError *error) {
    NSString *message=@"";
    
	if (error){
        message = [NSString stringWithFormat:@"Error registering for push notifications: %@", error.description];
        NSLog(@"%@",message);
    } else {
        message=@"Successfully registered for push notifications";
        NSLog(@"%@",message);
    }
}];
```


**userId** 

Passe o valor do ID do usuário exclusivo para registrar para notificações push.

## Swift

```
// Initialize the BMSPushCliet let push =
BMSPushClient.sharedInstance
push.initializeBluemixPushWithClientSecret("clientSecret")
```

**clientSecret** 

Esta é a chave clientSecret do serviço de Notificações push.

Use a API **registerWithUserId** para registrar o dispositivo para notificações push.

```
// Register the device to Push Notifications service.
push.registerDeviceToken("deviceToken", WithUserId: "userId")  { (response, statusCode, error) -> Void in
if error.isEmpty {

    print( "Response during device registration : \(response)")

        print( "status code during device registration : \(statusCode)")

    } else {

        print( "Error during device registration \(error) ")
    }
}
```

**userId** 

Passe o valor do ID do usuário exclusivo para registrar para notificações push.


# Usando notificações baseadas em ID do usuário
{: #using_userid}


Notificações baseadas em ID do usuário são mensagens de notificação que são destinadas a um usuário específico. Muitos dispositivos podem ser
registrados com um usuário. As etapas a seguir descrevem como enviar notificações baseadas em ID do usuário. 

1. A partir do painel **Notificação push**,
clique na guia **Notificações**.
1. Selecione a opção **UserId** para enviar notificações baseadas em userId.
1. No campo UserId **Procurar**, procure o userid que deseja usar e, em seguida, clique no botão
**+Incluir**.![Tela de notificações](images/tag_notification.jpg)
1. No campo **Texto da mensagem**, insira o texto que deseja enviar em sua notificação.
1. Clique no botão **Enviar**.
