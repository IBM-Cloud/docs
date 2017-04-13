---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Monitoring for Push Notifications 
{: #monitor-notifications}
Last updated: 12 April 2017
{: .last-updated}


The IBM {{site.data.keyword.mobilepushshort}} service now extends capabilities to monitor the push performance by generating graphs from your user data. You can use the utility to list all the sent push notifications, or to list all the registered devices and to analyze information on a daily, weekly, or monthly basis.

To generate reports for all your the sent notifications, use the Push Messages GET report method in [REST APIs](https://mobile.{DomainName}/imfpush/){: new_window}. 

![Sent notifications report](images/monitoring_messages.jpg)


To generate reports for all your registered devices, use the Push Device Registrations GET report method in [REST APIs](https://mobile.{DomainName}/imfpush/){: new_window}.

![Registered devices report](images/monitoring_devices.jpg)

For information on how to update your Android SDK to monitor notification information, see topic 'Monitoring push notifications on Android devices' in [Enabling notifications for mobile devices](c_enable_push.html).


 