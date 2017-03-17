------

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Manipulando notificações silenciosas para iOS
{: #silent-notifications}
Última atualização: 16 de janeiro de 2017
{: .last-updated}

As notificações silenciosas não aparecem na tela do dispositivo. Essas notificações são recebidas pelo aplicativo no segundo plano, que acorda o aplicativo por até 30 segundos para executar a tarefa em segundo plano especificada. É possível que um usuário não perceba a chegada da notificação. Para enviar notificações silenciosas para o iOS, use a [API de REST ![Ícone de link externo](../../icons/launch-glyph.svg "External link icon")](https://mobile.{DomainName}/imfpush/){: new_window}.   

1. Para enviar notificações push silenciosas, implemente o método a seguir no arquivo `appDelegate.m` em seu projeto. Em Swift, o valor `contentAvailable` enviado pelo servidor para notificações silenciosas é igual a 1.
```
// For Swift
func application(application: UIApplication, didReceiveRemoteNotification userInfo: [NSObject : AnyObject], fetchCompletionHandler completionHandler: (UIBackgroundFetchResult) -> Void) {
       let contentAPS = userInfo["aps"] as [NSObject : AnyObject]
       if let contentAvailable = contentAPS["content-available"] as? Int {
           //silent or mixed push
           if contentAvailable == 1 {
               completionHandler(UIBackgroundFetchResult.NewData)
           } else {
               completionHandler(UIBackgroundFetchResult.NoData)
           }
       } else {
    //Default notification
           completionHandler(UIBackgroundFetchResult.NoData)
       }
    }
```
	{: codeblock}

