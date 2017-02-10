---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

#Ativando notificações push avançadas
Última atualização: 11 de janeiro de 2017
{: .last-updated}

Configure um badge iOS, som, carga útil JSON adicional, notificações acionáveis e notificações de participação.

## Configure o som, a carga útil e o badge do iOS
{: #badge-sound-payload}

Configure um badge iOS, som e carga útil JSON adicional.

1. No painel {{site.data.keyword.mobilepushshort}}, acesse a guia **Notificações**.
2. Acesse a seção **Campos opcionais** para configurar os recursos do {{site.data.keyword.mobilepushshort}}. 
	- **Arquivo de som** - insira uma sequência para apontar para o arquivo de som em
seu app móvel. Na carga útil, especifique o nome da sequência do arquivo de som a ser usado.
	- **Badge iOS** - para dispositivos iOS, o
número a ser exibido como o badge do ícone do aplicativo. Se essa propriedade
estiver ausente, o badge não será mudado. Para remover o badge,
configure o valor dessa propriedade para 0.
	
###Android

Inclua seu arquivo de som no diretório `res/raw` do aplicativo Android. Ao enviar a notificação, inclua o nome do arquivo de som no campo de som do {{site.data.keyword.mobilepushshort}}.

```
"settings": {
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
		
**Carga útil adicional** - Essa carga útil pode ser qualquer par de valores de chave e deve ser um objeto JSON que você deseja enviar com o {{site.data.keyword.mobilepushshort}}.

```
{"key":"value", "key2":"value2"}
```
	{: codeblock}

## Participação de notificações do Android 
{: #hold-notifications-android}

Quando seu aplicativo entra em segundo plano, é possível que você queira que o {{site.data.keyword.mobilepushshort}} retenha as notificações enviadas para seu aplicativo. Para reter notificações, chame o método hold() no método onPause() da atividade que está manipulando o {{site.data.keyword.mobilepushshort}}.

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
## Ativando notificações acionáveis de iOS  
{: #enable-actionable-notifications-ios}

Ao contrário do {{site.data.keyword.mobilepushshort}} tradicional, as notificações acionáveis solicitam que os usuários façam uma seleção no recebimento do alerta de notificação sem abrir o app. 

Conclua as etapas para ativar o {{site.data.keyword.mobilepushshort}} acionável em seu aplicativo.

1. Crie uma ação de resposta do usuário.
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

2. Crie a categoria de notificação e configure uma ação. **UIUserNotificationActionContextDefault** ou
                **UIUserNotificationActionContextMinimal** são contextos válidos.
```
// For Swift
	let pushCategory = UIMutableUserNotificationCategory()
	pushCategory.identifier = "TODO_CATEGORY"
	pushCategory.setActions([acceptAction, declineAction], forContext: UIUserNotificationActionContext.Default)
```
	{: codeblock}

1. Crie a configuração de notificação e designe as categorias da etapa anterior.
```
// For Swift
	let categories = NSSet(array:[pushCategory]);
```
	{: codeblock}

1. Crie a notificação local ou remota e designe a ela a identidade da
categoria.
```
//For Swift
	let settings = UIUserNotificationSettings(forTypes: [.Alert, .Badge, .Sound], categories: categories as? Set<UIUserNotificationCategory>)
    UIApplication.sharedApplication().registerUserNotificationSettings(settings)
    UIApplication.sharedApplication().registerForRemoteNotifications() 
```
	{: codeblock}
	
## Manipulando notificações acionáveis do iOS  
{: #actionable-notifications}

Quando uma notificação acionável é recebida, o controle é passado para o método a seguir com base no identificador escolhido.

 
```
func application(application: UIApplication, handleActionWithIdentifier identifier: String?, forRemoteNotification userInfo: [NSObject : AnyObject], completionHandler: () -> Void) {
      //must call completion handler when finished
      completionHandler()
  }
```    
	{: codeblock}
    
