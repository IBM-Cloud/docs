ka---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Notificações interativas
{: #interactive-notifications}
Última atualização: 18 de janeiro de 2017
{: .last-updated}

As notificações interativas permitem que os usuários respondam a uma notificação sem abrir o aplicativo. Quando uma notificação interativa chega, o dispositivo mostra os botões de ação junto com a mensagem de notificação. As notificações interativas são suportadas em dispositivos iOS com a versão 8 ou mais recente. Para notificações interativas enviadas para dispositivos iOS que são anteriores à versão 8, as ações de notificação não são exibidas.

##Enviando {{site.data.keyword.mobilepushshort}} interativo


A notificação interativa pode ser enviada usando o painel Push ou usando a [Documentação da API de REST](t_restapi.html).

No console de {{site.data.keyword.mobilepushshort}}: 

1. Na guia de notificação no painel Push, clique em **Enviar notificação**. 
2. Escolha seus destinatários de notificação e clique em **Avançar**. 
3. Na página de composição de notificação, o push interativo pode ser enviado configurando o Tipo como Padrão ou Combinado e especificando o valor de Categoria na guia Opções avançadas. Para configurar o valor de categoria no cliente, marque **Manipulando o {{site.data.keyword.mobilepushshort}}** interativo na seção de aplicativo iOS nativo.

## Manipulando o {{site.data.keyword.mobilepushshort}} interativo em um aplicativo iOS


### Swift

Conclua as etapas para receber notificações interativas:

1. Ative o recurso do aplicativo para executar tarefas em segundo plano no recebimento de notificações remotas. 
1. Inicialize o SDK de `BMSPush` com sua categoria de ação.
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

1. Implemente o novo método de retorno de chamada em AppDelegate:
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
5. Este novo método de retorno de chamada é chamado quando o usuário clica no botão de ação. A implementação desse método deve executar tarefas associadas ao identificador especificado e executar o bloco no parâmetro `completionHandler`.


### Cordova

Para obter notificação acionável em um aplicativo Cordova iOS, conclua as etapas:

1. Inclua o campo de categoria no método `BMSPush.initialize`.
   ```
	var category =  {"Category_Name":[{"IdentifierName_1":"actionName_1"},{"IdentifierName_2":"actionName_2"}]}
       BMSPush.initialize(appGUID,clientSecret,category);
    ```
	{: codeblock} 
2. Implemente o novo método de retorno de chamada em AppDelegate.
3. Este novo método de retorno de chamada é chamado quando o usuário clica no botão de ação. A implementação desse método deve executar tarefas associadas ao identificador especificado e executar o bloco no parâmetro completionHandler.
