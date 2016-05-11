---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Administering {{site.data.keyword.iotdriverinsights_short}}
{: #1stanchor}
*Last updated: 6 May 2016*


Administering {{site.data.keyword.iotdriverinsights_full}} includes viewing tenant information and resetting the tenant password, configuring parameters for the service, and managing data stored in the service.
{:shortdesc}

You can perform administration tasks by using the {{site.data.keyword.iotdriverinsights_full}} Administration Console (Admin Console).

To access the Admin Console:

1. Go to the **Manage** view of your service instance.
2. Click **Launch**. The **Admin Console** is opened as a new window.
3. Enter the *username* and *password* as shown in the **Manage** view, then click **LOG IN**.

## Viewing tenant information
{: #viewtenantinfo}

After logging in to the **Admin Console**, you can see the **Tenant Information** view and tenant information.

## Resetting the tenant password
{: #resettenantpassword}

In the **Tenant Information** view, 

1. Click **RESET**.
2. On the confirmation dialog, click **OK**.
Then, the new password is shown in **Tenant Information** view

## Configuring parameters for the service
{: #configureparameters}

Click **Parameters** in the navigation pane. The **Parameters** view and parameters are displayed.

You can edit parameters to modify the analysis results.

The following table describes the behavior parameters:

|Category|Parameter Name|Description|Default Value|
|:-------:|:--------:|:--------|:-------:|
|Speed Limit (km/h)|\-|Speed limit for each road type. If the speed of vehicle exceeds this value on the road of each type, service identifies it as speeding.|\-|
|Speed Limit (km/h)|Motorway|Speed limit for Motorway|120|
|Speed Limit (km/h)|Urban Highway|Speed limit for Urban Highway|90|
|Speed Limit (km/h)|Urban Primary|Speed limit for Urban Primary|60|
|Speed Limit (km/h)|Urban Road|Speed limit for Urban Road|40|
|Speed Limit (km/h)|Others|Speed limit for Others|30|
|Speed Limit (km/h)|Unknown|Speed limit for Unknown|120|
|Turn|Angular Velocity (Min \- Max, deg/s)|Normal angular velocity value in turn. Min value is used as threshold to identify turn segment. Max value is used to detect sharp turn behavior.|10 \- 25|
|Turn|Average Speed (km/h)|Normal speed during turn. This value is used to identify behaviors in turn segment in conjunction with Angular Velocity values.|60|
|Fatigue Driving|Time of Continuous Driving (s)|If a vehicle is driven continuously for more than this value, service identifies it as "Fatigue Driving".|10800|

The following table describes the context parameters:

|Category|Parameter Name|Description|Default Value|
|:-------:|:--------:|:--------|:-------:|
|Analysis Time Zone|\-|Applied timezone for analysis |+00:00|
|Time Range|\-|This value defines time period type.|\-|
|Time Range|Day Time|Time range of day time|1030 \- 1730|
|Time Range|Night Time|Time range of night time|2030 \- 0700|
|Time Range|Morning Peak|Time range of morning peak time|0700 \- 1030|
|Time Range|Evening Peak|Time range of evening peak time|1730 \- 2030|
|Road Type|\-|These values are used to map the user road type value in the input data to {{site.data.keyword.iotdriverinsights_short}}-unique road type classifications. If you do not have a Road Type value, you can retrieve the Road Type value by using the `getLinkInformation` REST API, which is provided by **{{site.data.keyword.iotmapinsights_short}}**. The road type value is stored in the **properties > type** in the response. [Sample JSON](#sampleJson) represents the position of `type` in the response.|\-|
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


To apply changes to parameters:

1. Click **SAVE**. 
2. On the confirmation dialog, click **OK**.

Then, new parameters are applied and they become effective for next submitted job.

### Sample JSON Response of "getLinkInformation" REST API
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

- Click **Data Management** in the navigation pane. You can see the **Data Management** view and car probe and analysis result data.
- You can delete data by clicking **DELETE** in a record.
