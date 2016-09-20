---

copyright:
 years: 2015, 2016

---


# Registrar dispositivo com ID do usuário
{: #register_device_with_userId}
Última atualização: 16 de agosto de 2016
{: .last-updated}

Para registrar para notificação baseada em ID do usuário, conclua as etapas a seguir:

## Android
{: android-register}
 
Inicialize a classe MFPPush com a chave `AppGUID` e `clientSecret` do serviço {{site.data.keyword.mobilepushshort}}.

```
// Initialize the MFPPush
push = MFPPush.getInstance();
push.initialize(getApplicationContext(),"AppGUID", "clientSecret");
```

####AppGUID
{: push-app-guid}

Esta é a chave AppGUID do serviço {{site.data.keyword.mobilepushshort}}.

####clientSecret
{: android-client-secret}

Esta é a chave clientSecret do serviço {{site.data.keyword.mobilepushshort}}.

Use a API **registerDeviceWithUserId** para registrar o dispositivo para {{site.data.keyword.mobilepushshort}}.

```
// Register the device to {{site.data.keyword.mobilepushshort}}.
push.registerDeviceWithUserId("userId",new MFPPushResponseListener<String>() {
    @Override
	    public void onSuccess(String deviceId) {
        Log.d("Device is registered with Push Service.");
    }

    @Override
    public void onFailure(MFPPushException ex) {
        Log.d("Error registering with Push Service...\n"
        + "Push notifications will not be received.");
    }
});
```

####userId
{: android-user-id}

Passe o valor do ID de usuário exclusivo para registro para {{site.data.keyword.mobilepushshort}}.

**Nota:** para ativar {{site.data.keyword.mobilepushshort}} destinados por UserId, assegure-se de registrar o dispositivo com um UserId e também de passar o 'clientSecret' alocado quando os serviços de {{site.data.keyword.mobilepushshort}} são provisionados. Se você não passar um clientSecret válido, o registro de
dispositivo falhará.


## Cordova
{: cordova-register}

Copie o fragmento de código a seguir para seu aplicativo móvel para registrar para notificações baseadas em userId.

Inicialize `MFPPush` com `clientsecret`. 

```
MFPPush.initialize("appGUID", "clientSecret");
```

###appGUID 
{: cordova-pushappguid}

Esta é a chave AppGUID do serviço {{site.data.keyword.mobilepushshort}}. 

####clientSecret 
{: cordova-client-secret}

Esta é a chave clientSecret do serviço {{site.data.keyword.mobilepushshort}}.

```
//Register for {{site.data.keyword.mobilepushshort}} with userId
var userId = "userId";
MFPPush.registerDevice({},success,failure,userId); 
```
####userId
{: cordova-user-id}

Passe o valor do ID de usuário exclusivo para registro para o serviço {{site.data.keyword.mobilepushshort}}.


## Objective-C
{: objc-register}

Use as APIs a seguir para registrar para {{site.data.keyword.mobilepushshort}} baseadas em UserId.

```
// Initialize the MFPPush
IMFPushClient* push = [IMFPushClient sharedInstance];
[push initializeWithAppGUID:@"appGUID" clientSecret:@"clientSecret"]; 
```
###AppGUID 
{: objc-pushappguid}

Esta é a chave AppGUID do serviço {{site.data.keyword.mobilepushshort}}.

####clientSecret
{: objc-client-secret}

Esta é a chave clientSecret do serviço {{site.data.keyword.mobilepushshort}}.

Use a API **registerWithUserId** para registrar o dispositivo para {{site.data.keyword.mobilepushshort}}.

```
// Register the device to push notifications service.
[push registerWithDeviceToken:deviceToken WithUserId:@"userId" completionHandler:^(IMFResponse *response, NSError *error) {
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


####userId 
{: objc-user-id}

Passe o valor do ID de usuário exclusivo para registro para {{site.data.keyword.mobilepushshort}}.

## Swift
{: swift-register}

```
// Initialize the BMSPushClient
let push =  BMSPushClient.sharedInstance
push.initializeWithAppGUID("appGUID", clientSecret:"clientSecret")
```

####AppGUID 
{: swift-pushappguid}
Esta é a chave AppGUID do serviço {{site.data.keyword.mobilepushshort}}.

####clientSecret
{: swift-client-secret} 

Esta é a chave clientSecret do serviço {{site.data.keyword.mobilepushshort}}.

Use a API **registerWithUserId** para registrar o dispositivo para {{site.data.keyword.mobilepushshort}}.

```
// Register the device to Push Notifications service.
push.registerWithDeviceToken("deviceToken", WithUserId: "userId")  { (response, statusCode, error) -> Void in
if error.isEmpty {

    print( "Response during device registration : \(response)")

        print( "status code during device registration : \(statusCode)")

    } else {

        print( "Error during device registration \(error) ")
    }
}
```

####userId 
{: swift-user-id}

Passe o valor do ID de usuário exclusivo para registro para {{site.data.keyword.mobilepushshort}}.


# Usando notificações baseadas em ID do usuário
{: #using_userid}


Notificações baseadas em ID do usuário são mensagens de notificação que são destinadas a um usuário específico. Muitos dispositivos podem ser
registrados com um usuário. As etapas a seguir descrevem como enviar notificações baseadas em ID do usuário. 

1. A partir do painel **Notificação push**,
clique na guia **Notificações**.
1. Selecione a opção **UserId** para enviar notificações baseadas em userId.
1. No campo **Procurar** UserId, procure o ID do usuário que deseja usar e, em seguida, clique no botão **+Incluir**.![Tela Notificações](images/user_notification.jpg)
1. No campo **Texto da mensagem**, insira o texto que deseja enviar em sua notificação.
1. Clique no botão **Enviar**.
