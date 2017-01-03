---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Enabling Rich Media notifications
{: #interactive-notifications}
Last updated: 16 December 2016
{: .last-updated}


You can enable Rich Media {{site.data.keyword.mobilepushshort}} in iOS 10 and above. Push notifications can be sent with Audio, Video, GIFs and images. 

To set up your application to receive rich push on iOS 10, complete the steps:  

1. In Xcode, select **File** > **New** > **Target** > **Notification Service Extension**.
2. On the method `didReceive()` in the `UNNotificationServiceExtension`, add the  code.
```
BMSPushRichPushNotificationOptions.didReceive(request, withContentHandler: contentHandler)
```
	
To send a Rich Media {{site.data.keyword.mobilepushshort}} from the Push dashboard, ensure that you specify, message, title, subtitle, attachmentURL fields.