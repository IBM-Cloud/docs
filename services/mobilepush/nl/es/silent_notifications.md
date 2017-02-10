------

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Manejo de notificaciones silenciosas para iOS
{: #silent-notifications}
Última actualización: 16 de enero de 2017
{: .last-updated}

Las notificaciones silenciosas no aparecen en la pantalla del dispositivo. Estas notificaciones se reciben mediante la aplicación en segundo plano, que activa la aplicación durante 30 segundos para realizar la tarea en segundo plano. Puede que el usuario no tenga en cuenta la llegada de la notificación. Para enviar notificaciones silenciosas para iOS, utilice la [API REST ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://mobile.{DomainName}/imfpush/ "icono de enlace externo"){: new_window}.   

1. Para enviar notificaciones push silenciosas, implemente el siguiente método en el archivo `appDelegate.m` del proyecto.En Swift, el valor `contentAvailable` que envía el servidor para las instalaciones silenciosas es igual a 1.
```
// Para Swift
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

