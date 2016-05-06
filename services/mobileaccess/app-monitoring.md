---

copyright:
  years: 2015, 2016
  
---

# Application monitoring
{: #app-monitoring}

In addition to security features, the {{site.data.keyword.amafull}} also provides monitoring and analytics for your mobile applications. You can record client logs and monitor data with the {{site.data.keyword.amashort}} client SDK. Developers can control when to send this data to the {{site.data.keyword.amashort}} Service. All the security events, such as authentication success or failure, that occur in {{site.data.keyword.amashort}} Service are logged automatically.

When data is delivered to {{site.data.keyword.amashort}}, you can use the {{site.data.keyword.amashort}} Monitoring Dashboard to get analytics insights about your mobile applications, devices, and client logs. Information about requests that your application makes to resources that are protected by {{site.data.keyword.amashort}} are recorded by default.

The automatically recorded data includes information such as number of authentications, new devices, and new users. In addition you can configure the {{site.data.keyword.amashort}} client SDK to report the following information:

### Usage statistics of your mobile applications
{: #usage-stats}

You can configure your mobile applications to record application lifecycle events and send the recorded data to the {{site.data.keyword.amashort}} service with a few simple API calls. You can record the number of app opens, push notifications that are received, and so on.

### Client-side log capture
{: #client-side-logcapture}

Applications in the field occasionally experience problems that require a developer's attention to fix. It is often difficult to reproduce these problems. <!--in R&D.--> Developers who worked on the code might lack the environment or exact device with which to test. In these situations, it is helpful to be able to retrieve debug logs from the client devices as the problems occur in the environment in which they happen.

## Preserving captured data
{: #preserve-captureddata}

There is no way to guarantee that all captured data is preserved on the client side. Your users might be running the mobile application offline and simultaneously accumulating captured analytic and log data. Because the client is offline with limited file system space, older logged events must be purged in favor of preserving more recently logged events. It is up to the developer to decide when to send captured data to the {{site.data.keyword.amashort}} Service by using the supplied APIs.

## Using the {{site.data.keyword.amashort}} Monitoring Dashboard
{: #monitoring-dashboard}

1. Open the {{site.data.keyword.Bluemix}} Dashboard and click on your {{site.data.keyword.Bluemix_notm}} application

2. When your {{site.data.keyword.Bluemix_notm}} application dashboard is open, click on a {{site.data.keyword.amashort}} tile

3. In the {{site.data.keyword.amashort}} Dashboard click the `Monitoring` link in the left-hand menu

## Next steps
{: #next-steps}
* [Enabling, configuring and using Logger](app-monitoring-logger.html)
* [Gathering usage analytics](app-monitoring-gathering-analytics.html)
