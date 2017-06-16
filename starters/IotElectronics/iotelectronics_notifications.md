---

copyright:
  years: 2016, 2017
lastupdated: "2017-06-07"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Enabling notifications
{: #notifications}

The {{site.data.keyword.iotelectronics_full}} starter supports customized notifications with Node-RED. A sample Node-RED flow and rule are provided to help you get started.
{: shortdesc}

## Before you begin

Before you begin, you must deploy an instance of the {{site.data.keyword.iotelectronics}} in your {{site.data.keyword.Bluemix_notm}} organization. Deploying an instance automatically deploys the component applications, services, and Node-RED sample notification flow.

## Viewing the sample Node-RED notification flow
{: #viewFlow}

This flow is triggered by a specific change in appliance status, such as a failure. The type of change that can trigger the flow is defined by a rule that is created in {{site.data.keyword.iot_short_notm}}. For more information about the sample rule, see  [sample {{site.data.keyword.iotelectronics}} rule](#sampleRule).

After the flow is triggered, APIs are used to identify the owner of the appliance and the owner's email. A generated email that has the following information is sent to the owner:
  - DeviceID
  - Time of action triggered
  - Event type
  - Device type

You can create more Node-RED flows or edit the sample flow to create different actions for rules. For more information about programming with Node-RED, see the [Node-RED documentation ![External link icon](../../icons/launch-glyph.svg)](https://nodered.org/docs/){:new_window}.

Perform the following steps to access the Node-RED flow:

  1. In your {{site.data.keyword.Bluemix_notm}} dashboard, start your {{site.data.keyword.iotelectronics}} starter application by clicking the starter application.

    ![{{site.data.keyword.iotelectronics}} in the dashboard.](images/IoT4E_bm_dashboard.svg "{{site.data.keyword.iotelectronics}} in the dashboard")

  2. Wait for the *Your app is running* status message in the header and then click **View App** to display the starter app.

    ![{{site.data.keyword.iotelectronics}} view app.](images/IoT4E_view_app.svg "{{site.data.keyword.iotelectronics}} view app")

  3. In the browser, add `/red` to the end of the URL, for example, `https://mywebapp.mybluemix.net/red`. Node-RED is displayed.

## Viewing the sample rule
{: #sampleRule}

{{site.data.keyword.iotelectronics}} includes a sample rule that triggers the notification flow when an appliance sends a failure status. The rule is located in the Rules tab of the {{site.data.keyword.iot_short_notm}} dashboard. You can create more rules or edit the sample rule to trigger the sample notification Node-RED flow or new flows that you create.

To view or create rules to trigger Node-RED flows, perform the following steps:

  1. Open your {{site.data.keyword.Bluemix_notm}} dashboard and click the name of the {{site.data.keyword.iot_short_notm}} service.  

    **Tip:** The service name ends with `iotf-service` and is described as *Internet of Things Platform* in the Service Offering column.
  2. On the Welcome page, click **Launch**.
  3. On the menu, select **Rules**.
  4. On the Browse Rules page, click the sample rule, **IoT for Electronics notification**, to display the conditions and trigger action.
  5. Click **Actions** to display the **Rule Actions** page, which lists all actions that are associated with the rule.

## Understanding the notification nodes
{: #understandingNodes}

|Node| Description|
|-----|-----|
|IoT Platform Rule API  |  Retrieves information from the rule that is defined in {{site.data.keyword.iot_short_notm}}.|
|Rule Trigger Message |Retrieves the message from the rule.|
|Get Appliance Registration Details |Calls the {{site.data.keyword.iotelectronics}} API to get registration details for the appliance, including the device type.|
|Get User Registration Details | Calls the {{site.data.keyword.iotelectronics}} API to get registration details for the appliance owner, including owner email.|
|Generate Notification Email |Generates an email that includes details about the event that triggered the flow.|
