---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Enabling Rich Media notifications
{: #interactive-notifications}
Last updated: 09 March 2017
{: .last-updated}


You can enable Rich Media {{site.data.keyword.mobilepushshort}} in iOS 10 and later. Push notifications can be sent with Audio, Video, GIFs and images. 

To set up your application to receive rich push on iOS 10, complete the steps:  

1. In Xcode, select **File** > **New** > **Target** > **Notification Service Extension**.
2. On the method `didReceive()` in the `UNNotificationServiceExtension`, add the  code.
```
BMSPushRichPushNotificationOptions.didReceive(request, withContentHandler: contentHandler)
```
	
To send a Rich Media {{site.data.keyword.mobilepushshort}} from the Push dashboard, ensure that you specify the message, title, subtitle, and attachmentURL fields.