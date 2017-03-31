---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-03"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Administering Driving Behavior Analysis
{: #1stanchor}

Administer your {{site.data.keyword.iotdriverinsights_full}} service instance by using the administration console on the {{site.data.keyword.Bluemix_notm}} dashboard. From the administration console, you can configure parameters for {{site.data.keyword.iotdriverinsights_short}}, and manage the data that is stored in the service. You can also view the tenant information and reset the tenant password.

{:shortdesc}

## Starting the administration console
{: #start-admin-console}

To access the administration console for the {{site.data.keyword.iotdriverinsights_short}} service:

1. From the {{site.data.keyword.Bluemix_notm}} dashboard, click the {{site.data.keyword.iotdriverinsights_short}} service tile.
2. Select the **Manage** view of your service instance.
Make a note of the *Username* and *Password* credentials. To access the administration console, your IBMid is required, which might not be the same as your {{site.data.keyword.Bluemix_notm}} credentials.
3. Click **Launch**, and when prompted, enter your IBMid credentials.
4. Click **LOG IN**. The **Admin Console** is opened in a new window.

## Managing tenant information
{: #viewtenantinfo}

To view the tenant information, click **Tenant Information**.

### Resetting the tenant password
{: #resettenantpassword}

To reset the tenant password:

1. From the **Tenant Information** window, click **RESET**.
2. On the confirmation dialog box, click **OK**.
A new password is generated and displayed in the **Tenant Information** view.  
**Important:** Make sure that you update the password in all of your applications that access the {{site.data.keyword.iotdriverinsights_short}} API.

## Configuring the service parameters
{: #configureparameters}

Service parameters control how the trip data is analyzed. To modify the service parameters:

1. Open the **Parameters** view and adjust the following service parameters, as required:
  - Click the **Behavior** tab, and update the [driving behavior parameters](#behavior_parameters) to suit your requirements.
  - Click the **Context** tab, and update the [context mapping parameters](#context_parameters) to suit your requirements.
2. Click **SAVE**.
3. Click **OK**.

The updated parameter values are applied to the next job that is submitted.

### Driving behavior parameters
{: #behavior_parameters}

The following tables describe the driving behavior parameters for the categories that you can configure on the **Behavior** tab.

#### Speed limit settings

You can specify the speed limit in km/h for each road type. If the speed exceeds the speed limit value that you specify for the road type, speeding is detected.

|Parameter name|Description|Default value(km/h)|
|:--------|:--------|:-------|
|Motorway|Speed limit for a motorway road type|120|
|Urban Highway|Speed limit for an urban highway road type|90|
|Urban Primary|Speed limit for an urban primary road type|60|
|Urban Road|Speed limit for an urban road type|40|
|Others|Speed limit for a road type that is classified as 'Others'|30|
|Unknown|Speed limit for unknown road types|120|

#### Turn settings

|Parameter name|Description|Default value|
|:--------|:--------|:-------|
|Angular Velocity (Min \- Max, deg/s)|Normal angular velocity value of a turn. The Min value is used as a threshold to identify the turn segment. The Max value is used to detect sharp turn behavior.|10 \- 25|
|Average Speed (km/h)|Normal speed during a turn. This value is used to identify behaviors in a turn segment that has angular velocity values.|60|

#### Fatigue driving settings

|Parameter name|Description|Default value|
|:--------|:--------|:-------|
|Time of Continuous Driving (s)|The maximum length of continuous driving that is permitted.|10800|


### Context mapping parameters
{: #context_parameters}

The following tables describe the context mapping parameters for the categories that you can configure on the **Context** tab.

#### Time zone and time range settings

Specify the time zone and the hours for each time period.

|Parameter name|Description|Default value|
|:--------|:--------|:-------|
|Analysis time zone|Applied time zone for analysis. |+00:00|
|Day Time|Time range of day time.|1030 \- 1730|
|Night Time|Time range of night time.|2030 \- 0700|
|Morning Peak|Time range of morning peak time.|0700 \- 1030|
|Evening Peak|Time range of evening peak time.|1730 \- 2030|

#### Road types

Road types parameters are used to map the road type values of your input data to the  {{site.data.keyword.iot4auto_short}} road type classifications. If you do not have a road type value, you can retrieve the road type value by using the "getLinkInformation" REST API, which is provided by "{{site.data.keyword.iotmapinsights_short}}".

 The road type value is stored in the "properties > type" in the response. For an example that shows the position of "type" in the response, see [Sample JSON response for `getLinkInformation`](#sampleJson).

 |Parameter name|Description|Default value|
 |:--------|:--------|:-------|
|Motorway|Road type value that is mapped to Motorway.|1|
|Urban Highway|Road type value that is mapped to Urban Highway.|2|
|Urban Primary|Road type value that is mapped to Urban Primary.|3|
|Urban Road|Road type value that is mapped to Urban Road.|4|
|Others|Road type value that is mapped to Others.|5|

#### Speed threshold

The speed threshold parameters define the medium speed range for each road type in km/h. The medium speed range is the range between the lowest and highest values that are specified.

|Parameter name|Description|Default value|
|:--------|:--------|:-------|
|Motorway|Medium speed range for the Motorway road type.|55 \- 85|
|Urban Highway|Medium speed range for the Urban Highway road type.|35 \- 65|
|Urban Primary|Medium speed range for the Urban Primary road type.|20 \- 40|
|Urban Road|Medium speed range for the Urban Road road type.|15 \- 35|
|Others|Medium speed range for the Others road type.|10 \- 20|
|Unknown|Medium speed range for the Unknown road type.|20 \- 60|

#### Sample JSON Response of "getLinkInformation" REST API
{: #sampleJson}

```
{
	"links": [{
		"internal_link_id": "32088220365736308",
		"external_link_id": "3846419005",
		...
		"properties": {
			"type": "5",
			...
		},
		...
	}]
}
```
{: screen}


## Managing data stored in the service
{: #managedata}

The car probe data, context data, and the analysis results are stored in the service until they are deleted.

To delete data that is stored in the service:

1. Click **Data Management** to view the car probe and analysis result data.
2. Select a record, and then in the record, click **DELETE**.
