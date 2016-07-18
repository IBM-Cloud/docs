---

copyright:
 years: 2015, 2016

---

# Notificações interativas
{: #interactive-notifications}

As notificações interativas permitem que os usuários executem uma ação quando uma notificação chega, sem abrir o aplicativo. Quando uma notificação interativa chega, o dispositivo mostra os botões de ação junto com a mensagem de notificação. As notificações interativas são suportadas em dispositivos iOS com a versão 8 e
posterior. Se uma notificação interativa for enviada a dispositivos iOS com a versão menor que 8, as ações de notificação não serão exibidas.

##Enviando notificações push interativas


A notificação interativa pode ser enviada usando o painel Push ou usando a API REST (consulte a documentação da API REST).

No Console de Push: 

Na guia de notificação no painel Push, clique em Enviar notificação. Escolha seus destinatários de notificação e clique em avançar. Na página
de composição de notificação, o push interativo pode ser enviado, configurando o Tipo para Padrão ou Combinado e especificando o valor da
Categoria na guia Opções avançadas. Para configurar o valor de categoria no cliente, marque Manipulando a notificação push interativa na seção de aplicativo iOS nativo.

## Manipulando notificações push interativas em um aplicativo iOS

Deve-se seguir essas etapas para receber notificações interativas:

1. Ative o recurso do aplicativo para executar tarefas em segundo plano no recebimento de notificações remotas. Esta etapa será necessária se
algumas das ações forem ativadas para segundo plano.
1. No `AppDelegate (aplicativo: didRegisterForRemoteNotificationsWithDeviceTokenapplication:)`, configure as categorias antes de configurar o `deviceToken` no `WLPush Object`.

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

1. Implemente o novo método de retorno de chamada no AppDelegate:

```
	-(void)application:(UIApplication *)application handleActionWithIdentifier:(NSString *)identifier forRemoteNotification:(NSDictionary *)userInfo completionHandler:(void (ˆ)())completionHandler
``` 

5. Este novo método de retorno de chamada é chamado quando o usuário clica no botão de ação. A implementação desse método deve executar a tarefa que está associada ao identificador especificado e executar o bloco no parâmetro `completionHandler`.
