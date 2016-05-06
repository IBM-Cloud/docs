---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# About {{site.data.keyword.iotdriverinsights_short}}
{: #iotdriverinsights_overview}

You can use {{site.data.keyword.iotdriverinsights_full}} to analyze driver's behavior from car probe data and contextual data.
{:shortdesc}

## Driver behavior analysis
{: #driver_behavior_analysis}
You can analyze driver behavior such as harsh acceleration or braking, frequent braking, speeding, sharp turns, and other actions from car probe data and contextual data.

The following activities and contexts are included:
 - Driving behaviors 
    - Speed-related
       - Harsh acceleration
       - Harsh braking
       - Speeding
       - Frequent stops
       - Frequent acceleration
       - Frequent braking
    - Turn-related
       - Sharp turn (high speed turn)
       - Acceleration before turn
       - Over-braking during a turn
    - Others
       - Fatigued driving
 - Driving context
    - Time range
       - Morning peak hours
       - Evening peak hours
       - Day
       - Night
    - Road type
       - Motorway
       - Urban highway
       - Urban primary
       - Urban road
       - Others
    - Speed pattern based on road type
       - Free flow
       - Steady flow
       - Congestion
       - Severe congestion
       - Mixed conditions

## Big data analysis infrastructure
{: #big_data_analysis_infrastructure}
{{site.data.keyword.iotdriverinsights_short}} uses Hadoop as the back-end infrastructure. Hadoop enables  {{site.data.keyword.iotdriverinsights_short}} to  realize high scalability for analyzing big data from car probe data and contextual data.

## REST API
{: #rest_api}
Developers can retrieve the analysis results by REST API and use them in the {{site.data.keyword.Bluemix_notm}} application.
 1. Vehicle data
   - `sendCarProbeData` sends the car probe data to be analyzed.
   - `getCarProbeDataListAsDate` returns the list of car probe data by date basis.
   - `deleteCarProbeDataListByDate` deletes the car probe data.
 2. Analysis Job
   - `sendJobRequest` sends the driving behavior analysis job request.
   - `getJobInfo` returns the information of the specified job.
   - `getJobInfoList` returns the list of job information.
 3. Analysis Result 
   - `getAnalyzedTripSummaryList` returns the list of analyzed trajectory summary information.
   - `getAnalyzedTripInfo` returns the information of specified analyzed trajectory.
   - `deleteJobResult` deletes all of analyzed result related to a job.

## Configurability
{: #configurability}
Some of analysis threshold parameters (such as speed range per road type, turn angle range, and so on) can be configured from the user interface (UI).
