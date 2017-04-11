---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-03"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# About Driving Behavior Analysis
{: #iotdriverinsights_overview}

Driving Behavior Analysis is a service that you can use to analyze the behavior of a driver from car probe and contextual data.
{:shortdesc}


## Architecture
{: #drb}

You can identify and analyze several kinds of driving behavior that relates to speed, turns, and other categories. For example, you can determine instances of harsh acceleration, speeding, sharp turns, frequent or harsh braking, and other types of driver behavior.

## Analytic configuration
{: #configurability}  

Analysis threshold parameters determine how the different types of driver behavior are detected and analyzed from car probe and contextual data that is fed into the system. You can configure some of the threshold parameters for the driving behavior analytics from the {{site.data.keyword.iotdriverinsights_short}} service administration console. For example, you can configure the speed range per road type and the turn angle range.

For more information about how to configure the threshold parameters for the analytics of the Driving Behavior Analysis, see [Configuring parameters for the service](drb_iotdriverinsights_admin.html#configureparameters).

### Driving behavior categories and activities

The following tables list the types of driving behavior by category that can be detected and analyzed by the service:

#### Table 1: Speed related driving behavior types

|Behavior name|Behavior ID|Description|
|--------|:-------:|------|
|Harsh acceleration|1|Harsh acceleration threshold value in accordance with the speed is internally set. Harsh acceleration is recognized if acceleration data exceeds the threshold value.|
|Harsh braking|2|Harsh deceleration threshold value in accordance with the speed is internally set. Harsh braking is recognized if the braking data for a trip exceeds the threshold value.|
|Speeding|3|Over speed threshold value per road type is set. Speeding is recognized if the speed data for the trip exceeds the threshold value. You can configure the threshold for speeding. |
|Frequent stopping|4|A stop is detected when the speed value is zero. Frequent stops are recognized if there are many stop instances within a certain time frame in the trip.|
|Frequent acceleration|5|Acceleration threshold value in accordance with the speed is internally set. Frequent acceleration is detected if the driver frequently exceeds the threshold value within a certain time frame during the trip.|
|Frequent braking|6|Deceleration threshold value in accordance with the speed is internally set. Frequent deceleration is recognized if the driver exceeds the threshold value frequently within a certain time frame during the trip.|

#### Table 2: Turn related driving behavior

|Behavior name|Behavior ID|Description|
|-------|:--------:|-------|
|Sharp turn (high-speed turn)|7|Speed threshold value in turn is set. A sharp turn is recognized if the driver exceeds the threshold value. You can configure the sharp turn threshold.
|Acceleration before turn|8|Acceleration threshold value in accordance with the speed is internally set. Acceleration before a turn is recognized if the driver exceeds the threshold value.
|Over-braking before exiting a turn|9|Deceleration threshold value in accordance with the speed is internally set. Over-braking before exiting turn is recognized if the driver exceeds the threshold value.

#### Table 3: Other types of driving behavior

|Behavior name|Behavior ID|Description|
|-------|:--------:|-------|
|Fatigued driving|10|Deceleration threshold value in accordance with the speed is internally set. Fatigue in a driver is recognized if the speed exceeds the threshold value.|


### Driving context
|Context<br/>category|Context<br/>category ID|Context name|Context ID|
|-------|:-----:|--------|:-------:|
|**Time range**|**4**|\-|\-|
|Time range|4|Day|1|
|Time range|4|Night|2|
|Time range|4|Morning peak hours|3|
|Time range|4|Evening peak hours|4|
|**Road type**|**3**|\-|\-|
|Road type|3|Motorway|1|
|Road type|3|Urban highway|2|
|Road type|3|Urban primary|3|
|Road type|3|Urban road|4|
|Road type|3|Others|5|
|**Speed pattern**|**0**|\-|\-|
|Speed pattern|0|Free flow|0|
|Speed pattern|0|Steady flow|1|
|Speed pattern|0|Severe congestion|2|
|Speed pattern|0|Congestion|3|
|Speed pattern|0|Mixed conditions|4|


## REST API
{: #rest_api}

The {{site.data.keyword.iotdriverinsights_short}} REST API provides requests that you can use to customize and build your {{site.data.keyword.Bluemix_notm}} applications:

 1. Car data commands:
   - `sendCarProbeData` sends the car probe data to be analyzed
   - `getCarProbeDataListAsDate` returns the list of car probe data by date
   - `deleteCarProbeDataListByDate` deletes the car probe data
 2. Analysis job commands:
   - `sendJobRequest` sends the driving behavior analysis job request
   - `getJobInfo` returns the information of the specified job
   - `getJobInfoList` returns the list of job information
 3. Analysis result commands:
   - `getAnalyzedTripSummaryList` returns the list of analyzed trajectory summary information
   - `getAnalyzedTripInfo` returns the information of the specified analyzed trajectory
   - `deleteJobResult` deletes all analyzed results that are related to a job

For more information, see the [{{site.data.keyword.iotdriverinsights_short}} API ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://ibm.biz/IoTDriverBehavior_APIdoc){:new_window} documentation.

## Big data analysis infrastructure
{: #big_data_analysis_infrastructure}
{{site.data.keyword.iotdriverinsights_short}} uses Hadoop as the back-end infrastructure. Hadoop provides high scalability so that the {{site.data.keyword.iotdriverinsights_short}} service can retrieve and analyze large volumes of car probe and contextual data.
