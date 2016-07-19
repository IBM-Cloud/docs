---

copyright:
 years: 2015, 2016

---

# Enabling notifications
{: #c_enable_push-notifications}
*Last updated: 14 June 2016*
{: .last-updated}

You can enable applications to receive and send push notifications to your devices.

This section describes how to enable your mobile applications to receive push notifications, how to create basic notifications, get and initialize the SDK or plug-in, and how to register your device to receive push notifications. You can also enable your mobile applications to receive push notifications by using the [REST API](t_restapi.html).

Note: For device registrations with push, the Push Notification service maintains a unique reference to tokens issued from notification providers -
APNS for Apple or GCM for Google. The tokens can be invalidated by the Push Notification service notification provider for several reasons. 

For example, during uninstallation of app on the device. In such a scenario, when a notification is attempted to be delivered based on the providers response that the device is invalidated, the Push Notification service will remove the device registrations. This in turn would restrain consequent attempts in sending notification to those invalidated devices.
