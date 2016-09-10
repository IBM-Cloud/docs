---

copyright:
 years: 2015, 2016

---

# About {{site.data.keyword.mobilepushshort}}
{: #overview-push}
Last updated: 29 August 2016
{: .last-updated}

IBM {{site.data.keyword.mobilepushshort}} is a service that you can use to send notifications to iOS and Android mobile devices. Notifications can be targeted to all application users or to a specific set of users and devices using tags. You can administer devices, tags, and subscriptions. You can also use an SDK (software development kit) and Representational State Transfer (REST) application program interface (APIs) to further develop your client applications. 

{{site.data.keyword.mobilepushshort}} is also available as a Bluemix Dedicated service. For information about {{site.data.keyword.mobilepushshort}} as a dedicated service, see [Dedicated Services](../../dedicated/index.html). Note that the {{site.data.keyword.mobilepushshort}} monitoring tab does not show analytics data.

The {{site.data.keyword.mobilepushshort}} service is now OpenWhisk enabled. For more information, see [OpenWhisk](../../openwhisk/index.html).


## {{site.data.keyword.mobilepushshort}} service process
{: #overview_push_process}

Mobile and browser clients can subscribe and register for the {{site.data.keyword.mobilepushshort}} service. On startup, the client applications will register and subscribe themselves to the {{site.data.keyword.mobilepushshort}} service. The notifications are dispatched to the Apple Push Notification Service (APNs) or Google Cloud Messaging (GCM) server and then sent to registered mobile or browser clients.

![Push Overview](images/overview.jpg)


###Mobile applications
{: mobile-applications}

On startup, mobile and browser applications register and subscribe themselves to the {{site.data.keyword.mobilepushshort}} service to receive notifications.

###Back end applications
{: backend-applications}

Back end applications can be either on premise, or in a public cloud. Back end applications will use the {{site.data.keyword.mobilepushshort}} service to send context-sensitive notifications to mobile and browser application users. The back end applications are not required to maintain and manage mobile devices, browser agents and user information for sending push notifications. Instead, back end applications can use the {{site.data.keyword.mobilepushshort}} service which will manage and maintain them.

###App backend owner
{: app-backend-owner}

The App backend owner creates the mobile back end application which bundles an instance of the {{site.data.keyword.mobilepushshort}} service. The App back end owner also configures and sets up the {{site.data.keyword.mobilepushshort}} service to suit the back end applications using the service along with mobile  and browser applications that are target for {{site.data.keyword.mobilepushshort}}.

###{{site.data.keyword.mobilepushshort}} service
{: push-notification-service}

The {{site.data.keyword.mobilepushshort}} service manages all information related to mobile devices that are registered for notifications. The service keeps your applications transparent to the technology details of sending notifications to heterogeneous mobile platforms, handling all of this within.

###Gateways
{: gateways}

Platform specific Push Notifications cloud services such as Google Cloud Messaging (GCM) or Apple Push Notification Service (APNs) that is used by IBM {{site.data.keyword.mobilepushshort}} service to dispatch notifications to the mobile and browser applications.

###Push Security
{: push-security}

{{site.data.keyword.mobilepushshort}} APIs are secured by two types of secrets - i) appSecret ii) clientSecret.  The 'appSecret' protects APIs that are typically invoked by back end applications- such as the API to send {{site.data.keyword.mobilepushshort}} and the API to configure settings.   The'clientSecret' protects APIs that are typically invoked by mobile client applications.  The 'appSecret' and 'clientSecret' are allocated to every service instance at the time of binding an application with {{site.data.keyword.mobilepushshort}} service. Refer the ReST API documentation for more information on how the secrets are to be passed and for what APIs.

NOTE : Earlier applications were required to pass the clientSecret only when registering or updating devices with userId field.  All other APIs invoked by mobile / browser clients did not require the clientSecret.  These old applications can continue with this behaviour of optionally using the clientSecret for the device registration / update calls.  However it is strongly recommended that clientSecret check is enforced for all client API calls.  To enforce this in old applications there is a new 'verifyClientSecret' API that is published.  For all new applications clientSecret check will be enforced on all client API calls and this behaviour cannot be changed even with the 'verfiyClientSecret' API.

## {{site.data.keyword.mobilepushshort}} types
{: #overview-push-types}

###Broadcast
{: broadcast}

When a mobile application registers itself with {{site.data.keyword.mobilepushshort}} service, it can start receiving broadcasts. Broadcast notifications are messages targeted to all devices that have an application installed and configured for the {{site.data.keyword.mobilepushshort}} service. Broadcast notifications are enabled by default for any application enabled for {{site.data.keyword.mobilepushshort}}. Applications enabled for {{site.data.keyword.mobilepushshort}} service has a predefined subscription to the Push.ALL tag, which is used by server to broadcast notification messages to all devices. To send a broadcast notification that uses the REST Push API, ensure that the "target" is an empty JSON file when posting to the messages resource.

###Tag-based notifications
{: tag-based-notifications}

Tag notifications are messages targeted to all devices that are subscribed to a particular tag. Tags-based notifications allow segmentation of notifications based on subject areas or topics. Notification recipients can choose to receive notifications only if it is about a subject or topic that is of interest. Therefore, tags-based notification provides a means to segment recipients. This feature enables the ability to define tags and then send and receive messages by tags. A message is targeted to only the devices that are subscribed to a tag. You must first create tags for the application, set up the tag subscriptions and then initiate the tag-based notifications. To send a tag-based notification that uses the REST API, ensure that the "tagNames" are provided when posting to the message resource.

###Unicast notifications
{: unicast-notifications}

Unicast notifications are messages targeted to a particular device or user. Unicast notifications targeted to devices do not require any additional setup and are enabled by default when the application is enabled for {{site.data.keyword.mobilepushshort}}.

However, Unicast notifications targeted at users require:

- Associating a user ID with a device at the time of registering the mobile device for {{site.data.keyword.mobilepushshort}}.  

- Authorizing such a user ID registration by passing a 'clientSecret' which is allocated when binding a back-end application to the {{site.data.keyword.mobilepushshort}} service. 

Typically, a mobile application will first run an authentication cycle where the mobile app user is authenticated against a authentication service [like Mobile Client Access](https://console.ng.bluemix.net/docs/services/mobileaccess/index.html). On successful authentication, the authenticated user ID is then passed into the Push Device Registration API along with a clientSecret. The presence of a clientSecret enforces only authorized association of User IDs with mobile device registrations.
To send a Unicast notifications through REST API, ensure that the deviceIds or userIds are provided when posting to a message resource.

###Platform-based notifications
{: platform-based-notifications}

Notifications can be targeted to reach a particular device platform. For example, a notification can be sent to all Android users only. To send a platform-based notification that uses the REST API, make sure that the targeted platforms are provided when posting to a message resource. Specify the platforms as an array. The supported platforms are as follows:
* A (Apple)
* G (Google)


## {{site.data.keyword.mobilepushshort}} message size
{: #push-message-size}

The {{site.data.keyword.mobilepushshort}} message payload size is dependent on the constraints laid out by the Gateways (GCM, APNs) and client platforms. 

###iOS
{: ios-message-size}

For iOS 8 and later, the maximum size allowed is 2 kilobytes. Apple Push Notification service does not send notifications that exceeds this limit.

###Android
{: android-message-size}

There is a limitation of 4 kilobyes as the maximum allowed message size.  
