---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Registrando um dispositivo com userId
{: #register_device_with_userId}
Última atualização: 11 de janeiro de 2017
{: .last-updated}

Para registrar-se para notificação baseada em userId, conclua as etapas a seguir:

## Android
{: android-register}

Inicialize a classe MFPPush com a chave `AppGUID` e `clientSecret` do serviço {{site.data.keyword.mobilepushshort}}.
```
// Initialize the MFPPush
push = MFPPush.getInstance();
push.initialize(getApplicationContext(),"AppGUID", "clientSecret");
```
	{: codeblock}


- **AppGUID**: esta é a chave AppGUID do serviço
{{site.data.keyword.mobilepushshort}}.
- **clientSecret**: esta é a chave clientSecret do serviço
{{site.data.keyword.mobilepushshort}}.

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
	{: codeblock}


- **userId**: transmita o valor exclusivo de userId para registrar-se no {{site.data.keyword.mobilepushshort}}.

**Nota:** para ativar
{{site.data.keyword.mobilepushshort}} destinado por UserId, assegure-se de
registrar o dispositivo com um userId e também de passar o 'clientSecret'
que é alocado quando os serviços {{site.data.keyword.mobilepushshort}} são
provisionados. O registro do dispositivo falhará sem um clientSecret válido.

## Cordova
{: cordova}

Use as APIs a seguir para registrar para {{site.data.keyword.mobilepushshort}} baseadas em UserId.

```
// Register device for push notification with UserId
var options = {"userId": "Your User Id value"};
BMSPush.registerDevice(options,success, failure); 
```
	{: codeblock}


- **userId**: transmita o valor exclusivo de userId para registrar-se no {{site.data.keyword.mobilepushshort}}.


## Swift
{: swift-register}

```
// Initialize the BMSPushClient
let push =  BMSPushClient.sharedInstance
push.initializeWithAppGUID("appGUID", clientSecret:"clientSecret")
```
	{: codeblock}


- **AppGUID**: esta é a chave AppGUID do serviço
{{site.data.keyword.mobilepushshort}}.
- **clientSecret**: esta é a chave clientSecret do serviço
{{site.data.keyword.mobilepushshort}}.

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
	{: codeblock}

- **userId**: transmita o valor exclusivo de userId para registrar-se no {{site.data.keyword.mobilepushshort}}.

## Google Chrome, Safari e Mozilla Firefox
{: web-register}

Use as APIs a seguir para registrar-se para notificações baseadas em userId. Inicialize
o SDK com `app GUID`, `app Region` e
`Client Secret`.

```
var bmsPush = new BMSPush();
var params = {
    "appGUID":"push app GUID",
    "appRegion":"App Region",
    "clientSecret":"Push Client Secret" 
    }
  bmsPush.initialize(params, function(response){
          alert(response.response)
    })
```
	{: codeblock}
  
Após inicializado com sucesso o registro do aplicativo da web com o userId.

```
bmsPush.registerWithUserId("UserId", function(response) {
 alert(response.response)
  })
```
	{: codeblock}

## Apps Google Chrome e Extensões
{: web-register-new}

Use as APIs a seguir para registrar-se para notificações baseadas em userId. Inicialize
o SDK com `app GUID`, `app Region` e
`Client Secret`.

```
var bmsPush = new BMSPush();
var params = {
    "appGUID":"push app GUID",
    "appRegion":"App Region",
    "clientSecret":"Push Client Secret" 
    }
  bmsPush.initialize(params, function(response){
          alert(response.response)
    })
```
	{: codeblock}
  
Após a inicialização bem-sucedida, será necessário registrar o aplicativo da web com o userId.

```
bmsPush.registerWithUserId("UserId", function(response) {
 alert(response.response)
  })
```
	{: codeblock}

# Usando notificações baseadas em userId
{: #using_userid}

As notificações baseadas em userId são mensagens de notificação destinadas a
um usuário específico. Muitos dispositivos podem ser
registrados com um usuário. As etapas a seguir descrevem como enviar notificações baseadas em ID do usuário.

1. No painel **Notificação push**, selecione a opção
**Enviar notificações**.
1. Selecione **UserId** na lista de opções **Enviar para**.
1. No campo **ID do usuário**, procure o ID do usuário que deseja usar e, em seguida, clique em
**+Incluir**.![Tela de notificações](images/user_notification.jpg)
1. No campo **Mensagem**, insira o texto que você deseja enviar em sua notificação.
1. Clique em **Enviar**.
