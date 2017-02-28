---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-28"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# About Trajectory Pattern Analysis
{: #tp_iotdriverinsights_overview}

Trajectory Pattern Analysis API is a service that is provided by {{site.data.keyword.iotdriverinsights_full}} that you can use to analyze the Origin/Destination (O/D) and route patterns of driving trips from car probe data.

{:shortdesc}

## Route trajectory pattern analysis
{: #tpa}

You can identify and analyze O/D and route patterns from multiple driving trips.
The following diagram shows a simple example of the O/D and route patterns of a vehicle (vehicle-1) taken from of multiple trips. In this example, Trajectory Pattern Analysis  identifies two O/D patterns:
- An O/D pattern from Home (Origin1) to Office (Destination1) that has two route patterns
- An O/D pattern from Home (Origin1) to Shop (Destination2) that has one route pattern.

![od route example](images/tp_odroute_example.png "O/D and route pattern example")

Trajectory Pattern Analysis also calculates some driving diversity metrics for each vehicle as listed in the following table. You can use these metrics to judge the driving characteristics of a driver.

|Metrics name|Description|
|:---|:---|
|Rare O/D ratio|The ratio of the number of trips that are not covered by O/D patterns to the total number of input trips.|
|Rare mileage ratio|The ratio of the mileage that is not covered by route patterns to the total mileage of the input trips.|
|Rare trip ratio|The ratio of the number of trips that are not covered by route patterns to the total number of input trips.|


## REST API
{: #rest_api}

The Trajectory Pattern Analysis REST API provides requests that you can use to customize and build your {{site.data.keyword.Bluemix_notm}} applications:

 1. Car data commands:
   - `sendCarProbeData` sends the car probe data to be analyzed
   - `getCarProbeDataListAsDate` returns the list of car probe data by date
   - `deleteCarProbeDataListByDate` deletes the car probe data
 2. Analysis job commands:
   - `sendJobRequest` sends the trajectory pattern analysis job request
   - `getJobInfo` returns the information of the specified job
   - `getJobInfoList` returns the list of job information
 3. Analysis result commands:
   - `getResultSummary` returns the analyzed summary information of trajectory pattern analysis
   - `getAnalyzedODDetail` returns the detail information of the specified analyzed O/D pattern
   - `getRouteGPSList` returns the list of GPS information of the specified analyzed route pattern
   - `getODList` returns the list of O/D pattern information of the specified arguments
   - `deleteJobResult` deletes all of the analyzed results that are related to a job

For more information, see the [{{site.data.keyword.iotdriverinsights_short}} API](http://ibm.biz/IoTDriverBehavior_APIdoc){:new_window} documentation.
