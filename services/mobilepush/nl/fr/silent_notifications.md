------

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Traitement des notifications silencieuses pour iOS
{: #silent-notifications}
Dernière mise à jour : 16 janvier 2017
{: .last-updated}

Les notifications silencieuses n'apparaissent pas sur l'écran de l'appareil. Elles sont reçues par l'application en arrière-plan, qui sort alors de veille pendant une durée maximale de 30 secondes pour effectuer la tâche d'arrière-plan spécifiée. Un utilisateur peut ne pas être conscient de l'arrivée de la notification. Pour
envoyer des notifications silencieuses pour iOS, utilisez l'[API REST
![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://mobile.{DomainName}/imfpush/ "Icône de lien externe"){: new_window}. 

1. Pour envoyer des notifications push en mode silencieux, implémentez la méthode suivante dans le fichier `appDelegate.m` dans votre projet. Dans
Swift, la valeur `contentAvailable` envoyée par le serveur pour les notifications silencieuses est égale à 1.
```
//For Swift

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

