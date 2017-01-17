------

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Handling silent notifications for iOS
{: #silent-notifications}
Last updated: 16 January 2017
{: .last-updated}

Silent notifications do not appear on the device screen. These notifications are received by the application in the background, which wakes up the application for up to 30 seconds to perform the specified background task. A user might not be aware of the notification arrival. To send silent notifications for iOS, use the [REST API ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://mobile.{DomainName}/imfpush/){: new_window}.   

1. To send silent push notifications, implement the following method in the `appDelegate.m` file in your project. In Swift, the `contentAvailable` value that is sent by the server for silent notifications is equal to 1.
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

