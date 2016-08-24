---

copyright:
 years: 2015, 2016

---

# Enabling notifications
{: #c_enable_push-notifications}
<<<<<<< HEAD
Last updated: 23 August 2016
=======
Last updated: 16 August 2016
>>>>>>> 659bec289ef614725483fb60c244d9f26cadce1f
{: .last-updated}

You can enable applications to receive and send push notifications to your devices.

This section describes how to enable your mobile and web browser applications to receive push notifications, how to create basic notifications, get and initialize the SDK or plug-in, and how to register your device or browser to receive push notifications. You can also enable your mobile and web browser applications to receive push notifications by using the [REST API](t_restapi.html).

<<<<<<< HEAD
Note: For device and browser registrations, the {{site.data.keyword.mobilepushshort}} service maintains a unique reference to tokens issued from notification providers -
APNs for Apple or GCM for Google. The tokens can be invalidated by the {{site.data.keyword.mobilepushshort}} service notification provider for several reasons. 

For example, during un-installation of an app on the device. In such a scenario, when a notification is attempted to be delivered based on the providers response that the device is invalidated, the {{site.data.keyword.mobilepushshort}} service will remove the device or web browser registrations. This in turn would restrain consequent attempts in sending notification to those invalidated devices.
=======
Note: For device registrations with push, the {{site.data.keyword.mobilepushshort}} service maintains a unique reference to tokens issued from notification providers -
APNs for Apple or GCM for Google. The tokens can be invalidated by the {{site.data.keyword.mobilepushshort}} service notification provider for several reasons. 

For example, during un-installation of an app on the device. In such a scenario, when a notification is attempted to be delivered based on the providers response that the device is invalidated, the {{site.data.keyword.mobilepushshort}} service will remove the device registrations. This in turn would restrain consequent attempts in sending notification to those invalidated devices.
>>>>>>> 659bec289ef614725483fb60c244d9f26cadce1f
