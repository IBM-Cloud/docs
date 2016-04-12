---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Getting started with {{site.data.keyword.iotdriverinsights_short}} (Experimental)
{: #gettingstartedtemplate}
*Last updated: 12 April 2016*

With {{site.data.keyword.iotdriverinsights_full}}, you can run analytics on drivers' behavior by using the {{site.data.keyword.iotdriverinsights_short}} API to gather and analyze car probe data and contextual data.
{:shortdesc}

Follow these steps to integrate your application with the {{site.data.keyword.iotdriverinsights_short}} API after you create and deploy an unbound service instance. 

1. (Optional) Before sending car probe data to {{site.data.keyword.iotdriverinsights_short}} API, you can add additional data to your car probe data by using the {{site.data.keyword.iotmapinsights_short}} API.
     - Get map matched car probe data by using `mapMatching` API.
        - [Request] Car probe data
        - [Resonse] Map matched car probe data
     - Get road type data by using `getLinkInformation` API.
        - [Request] Road link id
        - [Response] Road type
2. Send car probe data to store and to be analyzed by using `sendCarProbe` API.
   - [Request] Map matched car probe data and Road type
3. Send a job request to analyze car probe data by using `sendJobRequest` API.
   - [Request] Date from and to
   - [Response] Job id
4. Check the job status by using `getJobInfo` API.
   - [Request] Job id
   - [Response] Job status
5. Get the analyzed trip summary list by using `getAnalyzedTripSummaryList` API.
   - [Request] Job id
   - [Response] List of analyzed trip summary
6. Get a detail analyzed trip info by using `getAnalyzedTripInfo` API.
   - [Request] Trip uuid
   - [Response] Detail of analyzed trip 

The following sequence diagram shows the sequene of steps.

![Typical analysis sequence](images/sequence_diagram.png "Typical analysis sequence")

See the [About {{site.data.keyword.iotdriverinsights_short}}](iotdriverinsights_overview.html) topic for details about analyzable behaviors and contexts. 


# Related Links
{: #rellinks}

## API Reference
{: #api}
* [API docs](https://new-console.ng.bluemix.net/apidocs/165){:new_window}

## Related Links
{: #general}
* [Getting started with {{site.data.keyword.iotmapinsights_short}}](../IotMapInsights/index.html){:new_window}
* [Getting started with {{site.data.keyword.iot_full}}](https://www.ng.bluemix.net/docs/services/IoT/index.html){:new_window}
* [dW Answers on IBM developerWorks](https://developer.ibm.com/answers/topics/iot-driver-behavior){:new_window}
* [Stack Overflow](http://stackoverflow.com/questions/tagged/iot-driver-behavior){:new_window}
* [What's new in Bluemix Services](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}

