---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Cloud Analytics
{: #cloud_analytics}

By using {{site.data.keyword.iot_short}} cloud analytics, you specify rule conditions that are based on real-time device data and that trigger alerts and optional actions when met.    
{: shortdesc}

For example, you might create a rule to ensure that when the device is dropped or when the temperature of the device spikes, an alert is sent to the dashboard on a user's device, and an email is sent to the administrator.

## Before you begin
{: #byb}
Make sure that the device properties that you want to use as conditions in your rules have been mapped to schemas. See [Connecting devices](iotplatform_task.html) and [Creating schemas](im_schemas.html) for more information.

Also, review the recipe [Using Rules and Actions with {{site.data.keyword.iot_short}} Cloud Analytics ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/using-rules-and-actions-with-ibm-watson-iot-platform-cloud-analytics/){: new_window} to understand the rules and actions that are used in Cloud Analytics.

## Managing rules and actions  
{: #managing_rules}

Use the **Rules** dashboard to create and manage rules and actions for your organization.

To get an overview of rules and alerts that have been triggered for your devices, use the following boards:

 |Board Name | Description |  
 |:---|:---|  
  |Rule-Centric Analytics | Shows the rules for your organization. Additional cards list triggered alerts, associated devices, device properties, and alert information. |  
 |Device-Centric Analytics | Shows the devices that are connected to your organization. Additional cards show alerts for a selected device, information for a selected device, device properties, and alert information. |

 For more information about the default analytics boards, see [Visualizing real-time data by using boards and cards](data_visualization.html#default_boards).


## Creating rules
{: #rules}

Rules are condition-based decision points that match real-time device data with predefined threshold values or other property data to trigger an alert if a condition is met. In addition to the alert that is displayed in the {{site.data.keyword.iot_short}} dashboard, you can add one or more actions to run business logic when a rule is triggered.

**Important:** Before you can create rules for a device type, you must create a schema for the device type. For information, see [Create device type schemas](im_schemas.html).

To create a rule:
1. In the {{site.data.keyword.iot_short}} dashboard, go to **Rules**.
2. Click **Create A Rule**, give the rule a name, provide a description, select a device type that the rule applies to, and then click **Next**.  
3. To set up the rule logic, add one or more IF conditions to use as triggers for the rule.  
You can add conditions in parallel rows to apply them as OR conditions, or you can add conditions in sequential columns to apply them as AND conditions.  
**Important:** To trigger a condition that compares two properties or to trigger two or more property conditions that are combined sequentially by using AND, the triggering data points must be included in the same device message. If the data is received in more than one message, the condition or sequential conditions do not trigger.  
**Examples:**   
A simple rule might trigger an alert if a parameter value is larger than a specified value:
Condition = `temp_cpu>80`  
A more complex rule might trigger when a combination of thresholds are met:
Condition = `temp_cpu>60 AND cpu_load>90`   

4. Configure conditional trigger requirements for your rule.  
To control the number of alerts that are triggered for a rule over a time period, you can configure conditional trigger requirements for your rule.  
**Important:**  The conditional triggering acts on any condition in the rule. For example, if a rule has five different parallel conditions set by using OR, each condition that is true counts towards the conditional trigger count.
To set conditional triggering for a rule:
 1. In the rule editor, click the default **Trigger each time conditions are met** link to open the set frequency requirement dialog box.
 2. Select and configure the conditional trigger that you want to use in the rule.
 <ul>
 <li>Trigger every time conditions are met</li>
 <li>Trigger if conditions are met N times in M *Unit of time*</li>
 </ul>  
 For a more detailed description of the conditional triggers, see [Conditional rule triggering](#conditional "Conditional triggering overview").
5. Create or select one or more actions that occur if the rule conditions are met.  
For more information about actions, see [Using actions with your rules](#shared "Create actions").   
 For example: An action can be to send an email or post a webhook.
3. **Optional:** Select an alert priority for the rule.  
 The priority is used to classify the alerts that are displayed in the **Rule-Based Analytics** board. The default priority is Low.
6. When you are satisfied with your rule, click **Save** to save without activating or click **Activate** to save and activate the rule.

Your rule is created. If you activate the rule, when the conditions of the rule are met, an alert is added to the **Boards > Rule-Based Analytics** board, and any rule action is run.

## Conditional rule triggering
{: #conditional}

To control the number of alerts that are triggered for a rule over a time period, you can configure conditional trigger requirements for your rule.

Depending on the message frequency and the rule conditions, a rule might trigger a large number of times after a trigger condition is met. For example, if the condition is `temp >= 90` and the temperature increases and stabilizes at 91, the rule is triggered with each incoming message. Depending on the frequency of the device messages and the actions that the rule is set to run, this volume of alerts might quickly fill your email inbox or flood a Twitter feed with messages that do not provide any additional value.

**Important:** The conditional triggering acts on any condition in the rule. For example, if a rule has five different parallel conditions set by using OR, each condition that is met counts towards the conditional trigger count.

Condition | Description
------------- | -------------
Trigger every time conditions are met | The rule is triggered every time the rule conditions are met.
Trigger if conditions are met *N* times in *M* *days/hours/minutes/custom* | The rule is triggered when the conditions are met *N* times in the selected time interval and is then not triggered again until the configured time period has passed. </br>Example: The conditional trigger requirement =`Trigger only once if conditions are met 4 times in 30 minutes`. The device sends one new message every five minutes. At noon, the temperature initially exceeds 90 degrees, which meets the condition. The conditional trigger counter is started, but the rule is not yet triggered.  After 15 minutes and three more messages that indicate that `temp > 90` were received, the rule is triggered. The rule is then not triggered for another 15 minutes regardless of the temperature.
Trigger only the first time conditions are met and reset when conditions are no longer met. | The rule is triggered when conditions are met but is then not triggered for consecutive messages that also meet the conditions. The triggering criteria is reset by the first message that does not meet the rule conditions.
Trigger if conditions persist for *M* *days/hours/minutes/custom*. | The rule is triggered after the selected time interval if all data points that are received during the time interval meet the conditions or if no additional data points are received. The time interval starts when the conditions are initially met.



## Using actions in your rules
{: #shared}

In addition to displaying alerts in the alerts dashboard, {{site.data.keyword.iot_short}} supports several types of rule-triggered actions, such as sending emails and posting webhooks.

You can create actions directly in the rule editor or create the actions in the Actions tab and then select the actions when you create your rules.

To create an action on the Actions tab:
1. In the {{site.data.keyword.iot_short}} dashboard, go to **Rules**.
2. In the Rules dashboard, select the **Actions** tab.
2. Click **Create An Action**, give the action a name and a description and select an action type, then click **Next**.
3. Provide the required parameters for the type of action that you are creating.  
Action types:  
 - [Send email](#email "Send email")
 - [IFTTT](#ifttt "IFTTT")
 - [Node-RED](#nodered "Node-RED")
 - [Webhook](#webhook "Webhook")
4. Click **OK** to create the new action.

The action is now available in the rule editor.

**Note:** The examples that follow all represent an action that notifies a service engineer when the temperature, which is represented by the `temp_cpu` property of a device, exceeds 80 degrees, by using the following rule condition: `temp_cpu >= 80`

### Send email  
{: #email}
Use the send email action to send an email to one or more recipients when a rule is triggered.

Example: [Send email](#emailex).

The following parameters are used to configure the send email action:

Parameter | Description
---|---
Name | The name of the action, which is used in the Alerts Dashboard.
Description | A brief description of the action.
Subject | The subject line of the email. The default subject line is "IBM Watson IoT Alert: Mail action".
To | Select to send the alert to just yourself or to a comma-separated list of email addresses. If you select to send to yourself, the email is sent to the email address of the {{site.data.keyword.iot_short}} that you are logged in as.
Cc | None, or a comma separated list of email addresses.
The body of the email is automatically created from the message of the device at the time that the rule was triggered.  
**Important:** By default, emails do not include device data that might include sensitive information. Change the **Include Data** setting to include device data.

#### Example: Use send email
{: #emailex}

In this example, the action is configured to use the send email feature to send an email to the main service engineer and also send a backup email to his manager.

To create the email action:
1. In the {{site.data.keyword.iot_short}} dashboard, go to **Rules**.
2. Click **Create An Action**.
4. Enter the action name `Send service request email`.
5. Enter the description `Send an email to the service engineer and his manager`.
3. Select the **Email** type.
6. In the To field, select **Specific people** and enter `service.engineer@company.com`.
7. In the CC field, select **Specific people** and enter: `service.manager@company.com`.
8. In the subject line, enter: `Service required.`
10. Select **Include Data** to include the device data in the email.
11. Click **Finish** to save the action.  


### IFTTT  
{: #ifttt}

Use the IFTTT action to trigger an IFTTT recipe when a rule is triggered. For more information about triggering actions as IFTTT recipes, see [Maker Channel ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://ifttt.com/maker){: new_window} on the IFTTT site.

Example: [Use IFTTT to post a Trello card](#iftttex).

The following parameters are used to configure an IFTTT action:

Parameter | Description
---|---
Name | The name of the action, which is used in the Alerts dashboard.
Description | A brief description of the action.
Key | The Maker Channel key to use to trigger the event.
Event | The event name that you configured as a trigger for the Maker Event. You can create multiple recipes with different triggers, each with a different event name.
Value 1-3 | You can pass any content in these parameters, which are passed to the action in your IFTTT recipe. **Tip:** You can use [variable substitution](#variable_substitution) to dynamically include additional data in the header.

#### Example: Use IFTTT to post a Trello card {: #iftttex}

In this example, the action is configured to use IFTTT to post a card to a service requests list on Trello.

To create the post a card on Trello action:
1.	In IFTTT, connect to the Trello channel.
2.	In IFTTT, connect to the Maker channel. Make a note of your IFTTT key. You need this key to connect to IFTTT from {{site.data.keyword.iot_short_notm}}.
5.	In IFTTT, create a recipe:
 1. Click **THIS**.
 2. Select the **Maker** channel.  
 2. Click **Recieve a web request**.
 3. Enter the event name `post-Trello-card`.
 4. Click **THAT**.
 5. Select the **Trello** channel.
 6. Select the Trello board in which to create the card.
 7. Enter a list name in which to add the cards.
 8. Edit the title and description.
 9. Assign the @service.engineer and @service.manager members.
 8. Click **Create Action**.   
3. In the {{site.data.keyword.iot_short}} dashboard, go to **Rules > Actions** and create a new action that has the following parameters:
<ul>
<li>Type - **IFTTT**</li>
<li>Name - `Post service request card`</li>
<li>Description - `Use IFTTT to post a card in the service requests list in Trello.`</li>
<li>Key - Your IFTTT key</li>
<li>Event - `post-Trello-card`</li>
<li>Optionally, add values for Value 1-3. **Tip:** You can use [variable substitution](#variable_substitution) to dynamically include device data.</li>
</ul>
4. Click **OK** to save the action.


### Node-RED
{: #nodered}

Use the Node-RED action to connect to a Node-RED application when a rule is triggered. For more information about using Node-RED, see [Creating apps with the Internet of Things starter application](https://www.ng.bluemix.net/docs/starters/IoT/iot500.html).

Example: [Use Node-RED to send a text message](#noderedex).

The following parameters are used to configure a Node-RED action:

Parameter | Description
---|---
Name | The name of the action, which is used in the Alerts dashboard.
Description | A brief description of the action.
URL | The URL of the target Node-RED HTTP input node.
User name | Include if required by the Node-RED service.
Password | Include if required by the Node-RED service. **Important:** The password is sent in cleartext.
Body | By default, the body field is pre-populated with all variables that are listed in [variable substitution](#variable_substitution).

#### Example: Use Node-RED to send a text message
{: #noderedex}

In this example, the action is configured to use Node-RED with a Twilio node to send a text message to the service engineer.

To create the send text message action:
1. In Twilio, locate or create a new Messaging Service to use to send text messages from your Twilio account. For information, see the [Twilio documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.twilio.com/help){: new_window}.
2. In Bluemix, set up and access your Node-RED account with the Node-RED URL `http://mynodered.mybluemix.net/red/`. For more information, see the [Creating apps with Node-RED Starter](https://www.ng.bluemix.net/docs/starters/Node-RED/nodered.html) topic in the Bluemix documentation.
3. In Node-RED, create a simple two node flow, such as [RTI-alert]->[SMS].  
Where the first node is an http node, and the second is a twilio node.
 1. Add the "http" input node and configure it with the following attributes:
  <ul>
  <li>Method - POST</li>
  <li>URL - `RTI-alert`</li>
  <li>Name - RTI Action</li>
  </ul>
  2. Add an "http response" output node and connect it and the "http" input nodes together by dragging between the output port of one to the input port of the other.
  3. Add a "twilio" output node and configure the it with the following attributes:
  <ul>
  <li>Service - **External service**</li>
  <li>Twilio - Add new twilio-api</li>
  <li>SMS to - `Phone number for the service engineer`</li>
  <li>Name - **SMS**</li>
  </ul>
  4. Wire the nodes together  
  Connect the http and twilio nodes together by dragging between the output port of one to the input port of the other.
  5. Click the **Deploy** button to deploy the flow to the server
4. In the {{site.data.keyword.iot_short}} dashboard, go to **Rules > Actions** and create a new action that has the following parameters:
 - Type - **Node-RED**
 - Name - `Send text using Node-RED and Twilio`
 - Description - `Send a text message alert to the service engineer.`
 - URL - `http://mynodered.mybluemix.net/RTI-alert`
 - BODY   
 ```json
 {"text":"*A device needs your attention*\n Time: {{timestamp}}\n {{site.data.keyword.iot_short}} instance: {{tenantId}}\n Device: {{deviceId}}\n Rule: {{ruleName}}\n Description: {{ruleDescription}}\n Condition: {{ruleCondition}}\n Raw device message: \n{{message}}"}
 ```  
5. Click **Finish** to save the action.



### Webhook
{: #webhook}

Use the webhook action to make an HTTP request to a webhook-enabled web service when an alert is triggered. For example, a webhook can be used to open a service request for an asset if a sensor in the device reports an abnormal reading.

Example: [Use webhook to post on Slack](#webhookex).

The following parameters are used to configure a webhook action:

Parameter | Description
---|---
Name | The name of the action, which is used in the Alerts dashboard.
Description | A brief description of the action.
URL | The URL of the target webhook-enabled server. **Tip:** You can use [variable substitution](#variable_substitution) to dynamically include additional data in the URL.
Method | The type of webhook call to run. Select one of the following types: GET, HEAD, OPTIONS, PATCH, PUT, POST, or DELETE.
User name | Include if required by the web service.
Password | Include if required by the web service. **Important:** The password is sent in cleartext.
Header | Headers are made up from key and value pairs. **Tip:** You can use [variable substitution](#variable_substitution) to dynamically include additional data in the header.
Content type | The type of content of the body: JSON, XML, WWW form URL encoded, or plain text.  Available for the OPTIONS, PATCH, PUT, POST, and DELETE methods.
Body | The body of the webhook call.  Available for the OPTIONS, PATCH, PUT, POST, and DELETE methods. By default, the body field is pre-populated with all variables that are listed in [variable substitution](#variable_substitution). **Important:** The webhook server might require certain specific fields to be included in the body. For example, a Slack webhook must contain the "text" field.   

#### Example: Use a webhook to post on Slack
{: #webhookex}

In this example, the action is configured to use a webhook to post a message to the #service-requests Slack channel.

To create the post to slack action:
1. In Slack, set up the Incoming Webhooks integration for the channel #service-requests. Make a note of the webhooks URL. For more information, see the [Slack documentation ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://api.slack.com/incoming-webhooks){: new_window}.
2. In the {{site.data.keyword.iot_short}} dashboard, go to **Rules > Actions** and create a new action that has the following parameters:
 - Name - `Post service request on Slack`
 - Type - **Webhook**
 - URL - `Your Slack webhooks URL`
 - Method - **POST**
 - Content type - `application/json`
 - Body   
 ```json
 {"text":"*A device needs your attention*\n Time: {{timestamp}}\n {{site.data.keyword.iot_short}} instance: {{tenantId}}\n Device: {{deviceId}}\n Rule: {{ruleName}}\n Description: {{ruleDescription}}\n Condition: {{ruleCondition}}\n Raw device message: \n{{message}}"}
 ```  
  **Important:** The Slack webhook must at a minimum contain the "text" field. For information, see [Incoming Webhooks ![External link icon](../icons/launch-glyph.svg)](https://api.slack.com/incoming-webhooks "Slack documentation"){: new_window} in the Slack documentation.
11. Click **Finish** to save the action.


### Variable substitution  
{: #variable_substitution}

Include the following variable substitutions to dynamically include device data. The variable must be surrounded by double curly brackets.

Variable | Description
---|---
**URL, Head, and Body** |
`{{timestamp}}` | The timestamp from the message.
`{{orgId}}` | The organization ID of the {{site.data.keyword.iot_short_notm}} service.
`{{tenantId}}` | Deprecated: The ID of the {{site.data.keyword.iotrtinsights_full}} service.
`{{deviceId}}` | The ID of the device.
`{{ruleName}}` | The name of the rule that includes the action.
`{{ruleID}}` | The ID of the rule that includes the action.
**Body only** |
`{{ruleDescription}}`| The description of the rule that includes the action.
`{{ruleCondition}}` | The rule condition that triggered the action.
`{{message}}` | The raw device message that included the data point value that triggered the rule.

## Recipes on Cloud Analytics

The following recipes describe how to use Cloud Analytics features for different use cases:

- [Real Time Data Analysis Using IBM Watson™ IoT Platform Analytics ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/real-time-data-analysis-using-ibm-watson-iot-platform-analytics/){: new_window}

- [Predictive Analytics on IOT Sample Data ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/predictive-analytics-on-iot-sample-data/){: new_window}

- [Device List Card SIMPLIFIES Real Time Device Monitoring on WIoTP Dashboard ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/device-list-card-simplifies-real-time-device-monitoring-on-wiotp-dashboard/){: new_window}

- [Perform Actions in IBM Watson IoT Platform Cloud Analytics ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/perform-actions-in-ibm-watson-iot-platform-cloud-analytics/){: new_window}

- [Use IBM Data Science Experience to detect time series anomalies ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/recipes/tutorials/use-ibm-data-science-experience-to-detect-time-series-anomalies/){: new_window}
