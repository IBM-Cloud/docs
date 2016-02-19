{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Administering
{: #1stanchor}
*Last updated: 07 Feb 2016*


Administration of {{site.data.keyword.iotdriverinsights_full}} includes the following activities:
- View Tenant Information
- Reset Tenant Password
- Configure Parameters for the service
- Manage data stored in the service
{:shortdesc}


You can work on those activities by **{{site.data.keyword.iotdriverinsights_full}} Administration Console (Admin Console)**.

To access to **Admin Console**:

1. Go to **Manage** view of your service instance.
2. Click **Launch** button, then **Admin Console** is opened as a new window.
3. Enter *username* and *password* showed in the **Manage** view, then click **LOG IN** button.

## View tenant information
{: #viewtenantinfo}

After logging in to **Admin Console**, you can see **Tenant Information** view and tenant information.

## Reset tenant password
{: #resettenantpassword}

In **Tenant Information** view, 

1. Click **RESET** button. Then, you can see confirmation dialog.
2. Click **OK**.
Then, you can see new password in **Tenant Information** view

## Configure parameters for the service
{: #configureparameters}

Click **Parameters** on the left navigation menu, then you can see **Parameters** view and parameters.
You can edit parameters so that you can get the analysis results that you want.

The following table describes behavior parameters:

|Category|Parameter Name|Description|Default Value|
|:-------:|:--------:|:--------|:-------:|
|Speed Limit (km/h)|\-|Speed limit for each road type. If the speed of vehicle exceeds this value on the road of each type, service identifies it as "over speed".|\-|
|Speed Limit (km/h)|Motorway|Speed limit for Motorway|120|
|Speed Limit (km/h)|Urban Highway|Speed limit for Urban Highway|90|
|Speed Limit (km/h)|Urban Primary|Speed limit for Urban Primary|60|
|Speed Limit (km/h)|Urban Road|Speed limit for Urban Road|40|
|Speed Limit (km/h)|Others|Speed limit for Others|30|
|Speed Limit (km/h)|Unknown|Speed limit for Unknown|120|
|Turn|Angular Velocity (Min \- Max, deg/s)|Normal angular velocity value in turn. Min value is used as threshold to identify turn segment. Max value is used to detect sharp turn behavior.|10 \- 25|
|Turn|Average Speed (km/h)|Normal speed during turn. This value is used to identify behaviors in turn segment in conjunction with Angular Velocity values.|60|


The following table describes context parameters:

|Category|Parameter Name|Description|Default Value|
|:-------:|:--------:|:--------|:-------:|
|Time Range|\-|This value defines time period type.|\-|
|Time Range|Day Time|Time range of day time|1030 \- 1730|
|Time Range|Night Time|Time range of night time|2030 \- 0700|
|Time Range|Morning Peak|Time range of morning peak time|0700 \- 1030|
|Time Range|Evening Peak|Time range of evening peak time|1730 \- 2030|
|Road Type|\-|This values are used to map user road type value in input data to Driver Insights unique road type classification. If you do not have Road Type value, you can retrieve Road Type value via "getLinkInformation" REST API which is provided by "IBM Watson IoT Map Insights". The road type value is stored in the "properties > type" in the response. [Sample JSON](#sampleJson) represents the position of "type" in the response.|\-|
|Road Type|Motorway|Road type value map to Motorway|1|
|Road Type|Urban Highway|Road type value map to Urban Highway|2|
|Road Type|Urban Primary|Road type value map to Urban Primary|3|
|Road Type|Urban Road|Road type value map to Urban Road|4|
|Road Type|Others|Road type value map to Others|5|
|Speed Threshold (Low \- High, km/h)|\-|This value defines medium speed range for each road types.|\-|
|Speed Threshold (Low \- High, km/h)|Motorway|Medium speed range for Motorway|55 \- 85|
|Speed Threshold (Low \- High, km/h)|Urban Highway|Medium speed range for Urban Highway|35 \- 65|
|Speed Threshold (Low \- High, km/h)|Urban Primary|Medium speed range for Urban Primary|20 \- 40|
|Speed Threshold (Low \- High, km/h)|Urban Road|Medium speed range for Urban Road|15 \- 35|
|Speed Threshold (Low \- High, km/h)|Others|Medium speed range for Others|10 \- 20|
|Speed Threshold (Low \- High, km/h)|Unknown|Medium speed range for Unknown|20 \- 60|


To apply changes of parameters:

1. Click **SAVE** button. Then, you can see confirmation dialog.
2. Click **OK**.

Then, new parameters are applied and they become effective for next submitted job.

##### <a name="sampleJson"> Sample JSON Response of "getLinkInformation" REST API
```
{
	"links": [{
		"internal_link_id": 32088220365736308,
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

## Manage data stored in the service
{: #managedata}

Click **Data Management** on the left navigation menu, then you can see **Data Management** view and car probe and analysis result data.
You can delete data by clicking **DELETE** button in a record.
